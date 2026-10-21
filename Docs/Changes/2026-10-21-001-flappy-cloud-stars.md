# Modification report — blue/red Flappy Cloud stars

- Report ID: 2026-10-21-001
- Date: 2026-10-21 (America/Mexico_City)
- Type: feature / gameplay

## Request and resulting behavior

Add collectible blue stars (+10) and avoidable red stars (−10). Implemented three reused star slots traveling before the penguin gates, one-time contact scoring, disappearance and recycled respawning. Points can be negative and remain distinct from cleared gates; both attempt summaries show points.

## Modifications

| File | Purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Game/FlappyCloudRun.cs | Collectible state, alternating types, normalized contact checks and separate Points/reset. |
| Assets/_HearingNotion/Scripts/Game/CollectibleStarGraphic.cs and .meta | Five-point UI mesh with explicit native dependencies and new unique GUID; no new bitmap. |
| Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs | Reused star visuals, blue/red colors and value labels, tutorial rule, live points and round summaries. Repair UTF-8 text encoding within the touched script. |
| Tools/Tests/FlappyCloudChecks.cs | Blue/red arithmetic, one-time contact, disappearance, negatives and reset checks. |
| Docs/FlappyCloud.md, Docs/FEATURES.md, Docs/Changes/README.md and report | Current behavior, F-017 history, verification and modification record. |

## Decisions and implications

Three bounded star slots reuse the gate lifecycle without per-frame spawning. Contacts use normalized bounding extents. Stars do not change course generation or end a round. Each run starts at zero; results remain temporary. No audio, package, original sprite, scene, build setting, participant data or guided-route change. A code-native star avoids recoloring the original yellow sprite. Existing GUIDs preserved; one new script GUID added.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| Gameplay suite | Passed | Blue +10, red −10, single collection/disappearance, negative totals and reset plus existing deterministic 180-second course, speed, scoring and boundary checks. |
| Editor/Windows compilation | Passed | All app scripts compiled against installed Unity 2022.3.12f1; existing Inspector-field CS0649 warnings only. |
| Unity rendering/input/device | Not run | Actual star shape, contacts, readability and round-transition display require Play Mode confirmation. |
| Documentation links | Passed | Relative file references checked before publication. |

## Performance

Not profiled; no improvement claim. Reuse three graphics and labels; contact arrays are allocated only with the run model.

## Limitations and follow-up

Check star rewards/penalties, skipping red stars, disappearance/recycling, negative points, pause/resume, both round results, Retry and visitor reset. Review star and label sizes in portrait/landscape. Noise remains pending/silent; scores do not demonstrate a noise effect. Documentation-only publication evidence is provided in the final response.

## Rollback

Reverse the new collectible fields/contact/scoring and corresponding controller/mesh/test changes, retaining preexisting obstacle scoring, geometry, Pause and two-round flow. Update feature documentation through a follow-up commit. No migration or scene regeneration required.
