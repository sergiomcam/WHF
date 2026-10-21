# Modification report — randomized Flappy Cloud courses

- Report ID: 2026-10-21-002
- Date: 2026-10-21 (America/Mexico_City)
- Type: feature / gameplay

## Request and resulting behavior

Increase variability of star/penguin positions and time between obstacles. Implemented seeded random gate heights/gaps, horizontal spacing and star offsets/heights/types. Retry/re-entry chooses a fresh seed, reused by both attempts in that session. Random spacing and increasing speed vary arrival intervals. Player physics, point values and three-minute limit remain stable.

## Modifications

| File | Purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Game/FlappyCloudRun.cs | Seeded bounded sampling; independent star coordinates/type and per-gate openings used by contact/collision. Remove duplicated star initialization. |
| Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs | Fresh in-memory session seed and render sampled star/gap coordinates. |
| Tools/Tests/FlappyCloudChecks.cs | Bounds/variation across 1,000 seeds, adapt pickup tests to sampled positions, retain deterministic replay and three-minute regression. |
| Docs/FlappyCloud.md, Docs/FEATURES.md, Docs/Changes/README.md and report | Current random ranges, session behavior and F-017 history. |

## Decisions and implications

Spacing .48–.66; opening .32–.38; center .24–.76 with adjacent steps <=.24; star lead .20–.29 and height within .10 of gap center; blue probability .65. Bounds avoid overlap and sudden extreme height transitions; no claim of equal course difficulty. Identical session seed makes the two attempts repeat their course without eliminating practice effects. Keep pending/silent noise condition, pause, Retry, temporary results and ±10 scoring. No packages, art, GUIDs, scenes, audio, research schema or storage changes.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| Gameplay checks | Passed | 1,000-seed initial geometry bounds/new-course variation; existing point arithmetic/reset, repeated-seed determinism, collisions, scoring, speed ramp and 180-second completion for regression seed. |
| Editor/Windows compilation | Passed | All app C# compiles with installed Unity 2022.3.12f1; existing Inspector CS0649 warnings only. |
| Unity visuals/input/random-course playability | Not run | Simulation checks do not establish human difficulty or all live layouts. |
| Documentation links | Passed | Relative file references checked before publication. |

## Performance

Not profiled. Three reused gate/star slots; random samples generated at initialization/recycling. No performance gain claimed.

## Limitations and follow-up

Review multiple courses in Play Mode, star/penguin collisions, varied arrival intervals, pause/reset and seeded pair replay. Human playability across seeds is unverified. Scores remain game outcomes, not noise-effect evidence. Final response provides verified documentation publication.

## Rollback

Reverse this task's model/controller/test sampling changes and current docs, preserving prior collectible graphics, scoring, geometry and pause flow. No migration or scene regeneration needed; use a follow-up documentation commit for remote reversal.
