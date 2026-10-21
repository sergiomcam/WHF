# Modification report — four research stages

- Report ID: 2026-10-20-004
- Date: 2026-10-20 (America/Mexico_City)
- Type: feature / content / assets

## Request and resulting behavior

Populate Research & Sources from the designated research folder, excluding audiovisual contents: INTER-NOISE pilot, demographic noise sources, HNAI validation and YANS change. Implemented four selectable Spanish tabs with scrollable summaries, source labels, limitations and three original figures. Existing navigation and final guided stage remain intact.

## Modifications

| File/asset | Purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Content/ResearchSourcesController.cs and .meta | Catalog models, runtime tabs, scroll/figure layout, stage/reset handling and source diagnostics. |
| Assets/_HearingNotion/Resources/Research/ResearchStages.es.json and .meta | Four stable, sourced research content records. |
| Assets/_HearingNotion/Resources/Research/demographic-exposure.png, yans-factors.png, yans-sum.png and metadata | Copy original research figures only, with new unique GUIDs; source files unchanged. |
| Assets/_HearingNotion/Resources/Research.meta | New content folder metadata. |
| Assets/_HearingNotion/Scripts/Core/AppManager.cs | Ensure research controller exists at startup. |
| Assets/_HearingNotion/Scripts/Navigation/GuidedExperienceController.cs | Explain the four research tabs in the final introduction. |
| AGENTS.md | Record source/cohort/evidence distinctions and controller responsibility. |
| Docs/ResearchSources.md, Docs/AppArchitecture.md, Docs/GuidedExperience.md | Source mapping, implementation, limitations and review. |
| Docs/FEATURES.md, Docs/README.md, Docs/Changes/README.md and report | Update F-010/F-015, guides and modification history. |

## Decisions and implications

Used the user-designated top-level research files. No audiovisual files, full PDF/DOCX documents, raw responses or private source paths are bundled or published. Statistical summaries retain source limitations: pilot intention is not later behavior; demographics lack group sample sizes; HNAI is preliminary; YANS figures lack sample, test and error-bar definitions. No cohort equivalence, causal effect, clinical scoring or visitor result is inferred. Existing historical discomfort-volume instructions are not adopted. Source figures are local Unity content; GitHub publication covers authored Markdown only. No new package, scene/build setting, route enum, participant schema/storage or audio behavior.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| Source review | Passed | Pilot methods/results pp.5–8 extracted, result pages 6–7 rendered with Poppler and inspected; all three research charts inspected; DOCX report read from XML. |
| Content integrity | Passed | Four-stage order, unique IDs, source fields, samples and reported statistics checked; all three figure paths exist; no audiovisual file in Research resources. |
| Editor/Windows source compilation | Passed | All app C# compiled against Unity 2022.3.12f1 with UNITY_EDITOR and UNITY_STANDALONE_WIN; existing Inspector-field CS0649 warnings only. |
| Documentation links | Passed | Local relative file targets checked before publication. |
| Unity Play Mode, visual/input/device checks | Not run | Compilation does not establish tabs, scrolling or figure readability. |

## Performance

Not profiled. Textures load once; controls/figures are reused and layout recalculates on stage/width changes. No performance improvement claim.

## Limitations and follow-up

Confirm research-owner interpretation and missing demographic/YANS metadata. Test tab selection, mouse/touch scrolling, figure quality, reset, resize, navigation and guided completion. Portrait chart lettering may remain small; summaries remain readable and zoom is future work. Publication evidence is supplied in the final verified documentation link.

## Rollback

Remove the research controller/initialization and new Research resources/metadata, restore placeholder visibility and the earlier guided source explanation. Preserve unrelated research questionnaire/catalog and previous game/wave work. Update docs/catalog to show rollback. No data migration or scene regeneration required; use a follow-up documentation commit for published changes.
