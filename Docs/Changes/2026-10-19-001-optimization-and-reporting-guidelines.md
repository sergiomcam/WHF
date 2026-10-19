# Modification report — optimization and reporting guidelines

- Report ID: 2026-10-19-001
- Date: 2026-10-19 (America/Mexico_City)
- Type: documentation

## Request and resulting behavior

The user requested optimization guidance and documentation of every future modification. Implemented both in the root AGENTS.md and established a report template and chronological history. These are development instructions; they do not change Unity runtime behavior.

## Modifications

| File | Change and purpose |
| --- | --- |
| AGENTS.md | Added Unity/C# optimization rules, evidence requirements, report naming/content requirements and a reporting delivery gate. |
| Docs/Changes/TEMPLATE.md | Added a reusable structure for task outcomes, file changes, validation, performance, limitations and rollback. |
| Docs/Changes/README.md | Created the history index and linked this report; explicitly excluded invented historical entries. |
| Docs/Changes/2026-10-19-001-optimization-and-reporting-guidelines.md | Recorded this documentation change as the first report. |

## Decisions and implications

One report is required per coherent modifying task, including documentation-only tasks. Each report lists individual meaningful modifications. Reports use the user's local date, unique daily sequence and relative links. Read-only work is exempt unless requested. Reports do not replace module documentation or recursively require another report.

Optimization prioritizes measured improvements, UI responsiveness, memory ownership and preserved behavior. The 60 FPS desktop goal is provisional and unmeasured. No dependencies, code, assets, GUIDs, build settings, participant data or questionnaire content changed.

## Validation

| Check | Result | Evidence or reason |
| --- | --- | --- |
| Guideline and template review | Passed | Both include change purpose, changed files, validation, performance, limitations and rollback. |
| Report/index link and naming check | Passed | Checked required files, relative Markdown links, unique report ID and naming. |
| Unity compilation / Play Mode / device tests | Not run | Documentation-only change with no runtime impact. |

## Performance

Not applicable. No runtime optimization or performance measurement was performed; this change defines future engineering practices.

## Limitations and follow-up

Reporting is an agent workflow requirement, not an automated enforcement hook. Keep the history updated for future modifications. Prior work is documented elsewhere but is not retrospectively reconstructed in this new history.

## Rollback

Remove the Optimization guidelines and Modification reports sections and the added reporting delivery line from AGENTS.md. Remove only the four files/changes introduced by this task as appropriate; preserve any reports added afterward. No project regeneration or runtime rollback is necessary.
