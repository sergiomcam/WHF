# Modification report — ethics and research-integrity policy

- Report ID: 2026-10-26-001
- Date: 2026-10-26 (America/Mexico_City)
- Type: documentation

## Request and resulting behavior

Create an ethics document addressing transparency, data management, documentation procedures and source veracity. Docs/ETHICS.md version 0.1 defines commitments, current data boundaries, source-review fields, responsibilities and corrections. AGENTS.md and the documentation index link to it.

## Modifications

| File or asset | Change and purpose |
| --- | --- |
| Docs/ETHICS.md | New project ethics and research-integrity policy |
| AGENTS.md | Link policy into project guidance |
| Docs/README.md | Navigation entry |
| Docs/Changes/README.md | Report index |

## Decisions and implications

Documentation only: no runtime feature, scene, GUID, dependency, build or storage change. Feature catalog update is not required because no app feature or behavior changes. Policy distinguishes commitments from implemented controls, institutional approval and scientific validation. Current-state review used SessionManager/AppSession, authored sound-library persistence, the questionnaire protocol flag and existing research/module guides. No external legal/medical assertions, approval numbers, retention schedules or named reviewers are invented. Existing unrelated project guidance is preserved.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| Data-boundary review | Passed | Temporary session data; persistent authored sound manifest remains separate; HNAI protocolConfirmed is false |
| Policy consistency | Passed | Preserves preliminary-instrument limits, optional playback, no WHO endorsement and documentation-only publication |
| Local Markdown links | Passed | All relative links in policy/report resolve; AGENTS and documentation index link to policy |
| Runtime compilation / Play Mode | Not run | No code or runtime changes |

## Performance

Not applicable; documentation only.

## Limitations and follow-up

No ethics audit, consent implementation, complete source registry or formal research approval is claimed. Ownership assignments, retention schedules, approved protocols and additional safeguards must be established when their scope is introduced. Publication must be verified separately.

## Rollback

If intentionally withdrawing the policy, remove it and this task's guidance/navigation links while preserving other work and historical reports. Record a later replacement as a new revision rather than silently deleting history.
