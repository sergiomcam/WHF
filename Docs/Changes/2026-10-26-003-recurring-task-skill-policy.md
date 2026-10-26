# Modification report — recurring-task skill creation policy

- Report ID: 2026-10-26-003
- Date: 2026-10-26 (America/Mexico_City)
- Type: documentation

## Request and resulting behavior

Require a skill whenever a recurring task is identified and document every created skill. AGENTS.md now requires creating a focused reusable skill or updating an existing equivalent during the same task. It defines recurrence, validation, authorization/discovery boundaries and documentation requirements. Docs/Skills.md is an empty register for future project-created skills, linked from the documentation index.

## Modifications

| Main change | Script, document or asset modified | Purpose / effect |
| --- | --- | --- |
| Define mandatory recurring-workflow skill procedure | AGENTS.md | Require create/update, recurrence evidence, suitable scope, validation and accurate invocation status |
| Establish skill documentation table | Docs/Skills.md | Record future skills, triggers, locations, dependencies, dates, validation and reports |
| Link skill register | Docs/README.md | Provide a navigation entry |
| Index the task | Docs/Changes/README.md | Add main-change and modified-document summary in the continuous table |
| Save the modification report | Docs/Changes/2026-10-26-003-recurring-task-skill-policy.md | Record decisions, checks, limitations and rollback |

## Decisions and implications

Documentation-only policy; no app feature or runtime change, so no feature-catalog entry is required. No skill is created/installed/activated by this task, and no retrospective conversion of earlier tasks is claimed. Skill-creator guidance informed structure, routing, reuse and validation requirements. The rule preserves existing permissions and documentation-only publication scope; it does not grant global installation or automatic discovery. No scene, GUID, dependency, build or data change.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| Policy review | Passed | Requires same-task create/update for genuine recurring workflows; preserves scope, permissions and evidence-based validation |
| Relative links and table structure | Passed | All relative links resolve; history remains a continuous four-column table |
| Skill structural / behavioral validation | Not run | No executable skill created in this policy-only task |
| Runtime compilation / Play Mode | Not run | No runtime changes |

## Performance

Not applicable; documentation only.

## Limitations and follow-up

Skill registration/discovery and validation will be assessed when each actual skill is created. The empty register is intentional and makes no claim of an installed project skill. Future skills must retain scientific/privacy boundaries and recorded validation.

## Rollback

Remove only the new AGENTS.md section, empty register and navigation/index references if intentionally withdrawing the policy. Preserve existing instructions, historical reports and unrelated work. If skills are later registered, preserve their records and document any replacement policy rather than silently deleting them.
