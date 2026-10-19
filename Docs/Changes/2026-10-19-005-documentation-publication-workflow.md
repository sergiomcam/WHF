# Modification report — documentation publication workflow

- Report ID: 2026-10-19-005
- Date: 2026-10-19 (America/Mexico_City)
- Type: documentation / repository publication

## Request and resulting behavior

The user requested that the main documents be maintained and pushed to GitHub whenever new features are added. Added standing documentation-only publication instructions and a documentation landing page. Prepared the current project-authored Markdown documentation and AGENTS.md for one publication commit to sergiomcam/WHF.

## Modifications

| File or location | Change and purpose |
| --- | --- |
| AGENTS.md | Added standing authorization, documentation scope, conflict preservation, verification and failure-reporting rules. |
| Docs/README.md | Added an easy-access index for feature status, architecture, module guides and modification history. |
| Docs/Changes/README.md | Indexed this task report. |
| Docs/Changes/2026-10-19-005-documentation-publication-workflow.md | Recorded the new workflow and publication scope. |
| GitHub: AGENTS.md and Docs/**/*.md | Publication set includes the current local feature catalog, architecture/module guides, all existing reports, template and documentation index. |

## Decisions and implications

Future feature tasks include local documentation maintenance and publication without repeated routine confirmation. Authorization covers project-authored documentation only, excluding Unity/vendor assets, source, private research inputs and participant data. Preserve remote history and concurrent changes. This is an agent delivery requirement, not an automated filesystem watcher. Connector publication does not update the local Git branch automatically.

No runtime code, dependencies, asset GUIDs, build settings, questionnaire wording or participant data changed. No new application feature was added, so the feature catalog's current inventory did not change.

## Validation

| Check | Result | Evidence or reason |
| --- | --- | --- |
| Remote baseline | Passed | Remote main was inspected at b5a9cccf6a76331545796d3dc173960edd270c9c, the initial AGENTS.md publication. |
| Documentation structure and local links | Passed | Checked intended Markdown files, relative links and feature anchors before publication. |
| Publication scope | Passed | Explicit file list contains root AGENTS.md and Markdown files under Docs only. |
| Remote publication | Pending at report preparation | Final response records the outcome after the commit/ref update and read-back verification; this report avoids a self-referential commit SHA. |
| Unity compilation / Play Mode | Not run | Documentation-only task. |

## Performance

Not applicable. No runtime modifications or performance measurements.

## Limitations and follow-up

Future agents must follow this workflow; no automated enforcement hook or scheduled task was installed. Existing runtime verification gaps remain visible in the feature catalog. Full project upload is outside this authorization.

## Rollback

If requested, reverse the publication with a new documentation commit, preserving unrelated remote content and history. Remove only the standing-publication rules and this task's documentation/index additions locally. Do not delete the repository, rewrite history or regenerate Unity scenes.
