# Modification report — clear English Flappy Cloud text

- Report ID: 2026-10-22-007
- Date: 2026-10-22 (America/Mexico_City)
- Type: fix / content

## Request and resulting behavior

Rewrite incorrectly written Flappy Cloud text in English. Replaced corrupted encoded Spanish strings across both home-card descriptions, title, instructions, all tutorial/ready/pause/transition notices, live status, results and Pause/Resume/Exit controls. Retry remains English. Star penalties now use a plain -10 label. Both rounds are accurately described as silent practice while distraction audio is pending.

## Modifications

| File or asset | Change and purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs | Plain English copy with encoding-safe punctuation; two-line live status with a slightly taller text region; Retry receives primary-action styling |
| Docs/FlappyCloud.md | Current English labels and tutorial descriptions |
| Docs/FEATURES.md | F-017 copy fix and verification status |
| Docs/Changes/README.md | Report index |

## Decisions and implications

Only the game and its menu-card descriptions switch to English. HNAI wording, other module language, game mechanics, timing, scoring, media, scene, GUIDs, build settings and visitor data are unchanged. The UI avoids implying that silent rounds demonstrate noise effects. No dependency or scientific-claim changes.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| Editor/Windows source compilation | Passed | Unity 2022.3.12f1; existing Inspector-field warnings only |
| Existing Flappy Cloud model regression | Passed | FlappyCloudChecks: randomized geometry, scoring, deterministic replay and full-course checks |
| Encoding/source copy review | Passed | No non-ASCII characters remain in FlappyCloudController; tutorial, transition and result strings reviewed |
| Unity visual/layout review | Not run | Check portrait and landscape tutorial wrapping and live status in Play Mode |

## Performance

Not applicable; no optimization claims.

## Limitations and follow-up

Restart Play Mode to recreate runtime controls. English rendering and wrapping still require interactive review. Both game rounds remain silent and are labeled accordingly; this task does not enable the distraction-audio condition.

## Rollback

Restore only this task's text, live-status rectangle and Retry styling if needed; preserve the earlier audio-crash fix and gameplay behavior. Avoid restoring corrupted encoding. Reverse corresponding documentation entries deliberately.
