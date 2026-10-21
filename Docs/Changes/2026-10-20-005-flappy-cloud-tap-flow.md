# Modification report — Flappy Cloud tap flow and progression

- Report ID: 2026-10-20-005
- Date: 2026-10-20 (America/Mexico_City)
- Type: feature / gameplay / UI

## Request and resulting behavior

Increase obstacle variation/difficulty, allow three-minute rounds, simplify controls with popup tutorial/tapping/double-tap pause, automatically follow quiet play with a noisy-condition notice and show Retry only at the end. Implemented the two-attempt flow. The second attempt is explicitly silent because noise integration remains pending; no artificial noise or playback is added. Salir remains a navigation escape.

## Modifications

| File | Change and purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Game/FlappyCloudRun.cs | 180-second tick-based cap, continuous 1.0–1.9× speed ramp, alternating varied high/low gates. |
| Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs | Three tutorial notices, tap start/flap, double-tap pause, single-tap resume, automatic six-second round transition, two result summaries, final Retry and larger playfield. |
| Assets/_HearingNotion/Scripts/Game/FlappyCloudTapSurface.cs and .meta | Pointer-down forwarding from free screen areas, with a new unique script GUID. |
| Tools/Tests/FlappyCloudChecks.cs | Extend deterministic completion checks to 180 seconds, wide obstacle variation and speed cap. |
| AGENTS.md, Docs/AppArchitecture.md, Docs/FlappyCloud.md | Current flow, audio boundary and review instructions. |
| Docs/FEATURES.md, Docs/Changes/README.md and report | F-017 behavior/history and indexed modification record. |

## Decisions and implications

Each attempt ends on collision or 180 seconds, not a guaranteed three-minute survival. The same fixed seed/difficulty ramp is replayed in both attempts; practice effects remain possible. First tap responds immediately; a second within 0.28 seconds pauses. Free-area pointer handling excludes Retry/Salir controls. Navigation/reset clears both attempts; focus loss freezes game/countdown until resumed. Keep noise clip unused and announce missing audio; automatic sequencing does not establish a noise effect. No scene, package, build setting, imported art, audio, participant schema/storage or guided-route change. Existing metadata/GUIDs preserved; only new tap script receives metadata.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| FlappyCloudChecks | Passed | Mono execution verifies idle/input, flap, collision, terminal state, restart, deterministic course/input, recycled scoring, 180-second completion, >0.4 height range, 1.9× final speed and reset. |
| Editor/Windows C# compilation | Passed | All app scripts compile against installed Unity 2022.3.12f1; existing Inspector CS0649 warnings only. |
| Input/flow source review | Passed | Reviewed tutorial, quiet transition, second results/Retry, pending-audio labeling and focus/navigation cleanup. |
| Unity UI/state/gesture/device checks | Not run | No Play Mode execution available; pure model tests do not validate live UI transitions or double-tap timing. |
| Documentation links/publication | Passed | Relative targets checked; task Markdown published/verified under standing authorization. Final response provides publication evidence. |

## Performance

Not profiled; no performance improvement claim. Reuse three gate pairs; fixed-step simulation is bounded per frame. No per-frame object spawning or audio processing.

## Limitations and follow-up

Verify gestures and tutorial, all transition/interrupt paths, Retry, three-minute difficulty and portrait/landscape readability in Unity. Both attempts remain silent; real noise requires later playback/safety integration. Results do not prove causal noise effects or clinical performance. Double-tap intentionally treats very rapid consecutive flaps as pause.

## Rollback

Reverse this task's model/controller/tap helper/test changes and current documentation additions, preserving original game sprites, settings and unrelated work. Restore the prior 30-second single practice round if desired. No scene regeneration or data migration needed. Use follow-up documentation commits rather than rewriting GitHub history.
