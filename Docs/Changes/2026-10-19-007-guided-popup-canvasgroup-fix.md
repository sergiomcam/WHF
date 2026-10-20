# Modification report — guided popup CanvasGroup fix

- Report ID: 2026-10-19-007
- Date: 2026-10-19 (America/Mexico_City)
- Type: fix

## Request and resulting behavior

The user reported a MissingComponentException when starting the HNAI-first guide. Replaced null-coalescing Unity component checks with explicit Unity-aware null comparisons so a missing CanvasGroup is added before accessing interactable. The runtime fix remains to be confirmed in Unity.

## Modifications

| File | Change and purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Navigation/GuidedExperienceController.cs | Explicit CanvasGroup and footer Transform null checks; mark a stage explained only after the modal opens. |
| AGENTS.md | Document Unity-aware null handling for missing/destroyed objects. |
| Docs/FEATURES.md; Docs/GuidedExperience.md | Record F-015 regression, fix and verification limits. |
| Docs/Changes/README.md; this report | Index and document this correction. |

## Decisions and implications

Unity object wrappers can compare equal to null without being CLR null; ?? does not use Unity's overloaded equality check. The exception identified the unsafe access. Existing component instances are reused; missing instances are added. No scene regeneration, dependencies, GUIDs, questionnaire data, scoring or navigation-order changes are required.

## Validation

| Check | Result | Evidence or reason |
| --- | --- | --- |
| Source compilation | Passed | Compiled all app sources against Unity 2022.3.12f1 assemblies; existing Inspector-field warnings only. |
| Journey checks | Passed | Existing executable checks passed for sequence, completion gating and stage exclusions. They do not verify Unity CanvasGroup behavior. |
| Null-coalescing review | Passed | Reviewed both uses in GuidedExperienceController and replaced Unity-object fallback expressions. |
| Unity Play Mode regression | Not run | Requires rerunning Start guided experience without an existing CanvasGroup, popup dismissal/re-entry and input-blocking checks. |
| Documentation structure/links | Passed | Local relative links checked before publication. |
| GitHub documentation publication | Pending at report preparation | Final response provides the verified outcome. |

## Performance

Not applicable. No performance optimization or profiling performed.

## Limitations and follow-up

The exact Unity runtime correction is not proven by compilation or pure route tests. Confirm the exception is gone and popup keyboard/pointer behavior works in Play Mode.

## Rollback

Reverse only this task's controller/null-guideline/documentation edits if needed, preserving later changes. Restoring the old null-coalescing expressions would reintroduce the reported failure and is not recommended. Use a new documentation commit for remote reversal; do not rewrite remote history.
