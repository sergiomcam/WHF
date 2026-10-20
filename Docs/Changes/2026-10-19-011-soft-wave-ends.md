# Modification report — soft wave ends

- Report ID: 2026-10-19-011
- Date: 2026-10-19 (America/Mexico_City)
- Type: fix / visual

## Request and resulting behavior

The screenshot shows abruptly cut wave tips. Implemented a smooth spatial alpha taper at both ends so moving waves blend into the background in either travel direction. The existing fade over time remains; paused waves receive the same soft tips.

## Modifications

| File | Change and purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Navigation/WaveTravel.cs | Symmetric smoothstep alpha envelope across each outer 35% of a contour. |
| Assets/_HearingNotion/Scripts/Navigation/TravelingWaveGraphic.cs | Assign separate vertex alpha at each segment endpoint for continuous interpolation. |
| Docs/FEATURES.md | F-008 behavior and history. |
| Docs/VisualRefresh.md | Explain spatial versus temporal fading and review. |
| Docs/Changes/README.md and this report | Modification record and index. |

## Decisions and implications

Keep the central 30% at original opacity; zero-alpha tips have a smooth slope to avoid visible caps. Geometry, timing, reduced-motion controls and palette are unchanged. No new assets, GUIDs, packages, scene edits, schema or data-path changes. No research or participant-data changes. Documentation is published under the standing authorization; final response supplies publication evidence.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| Editor and Windows source compilation | Passed | All app C# compiled against installed Unity 2022.3.12f1 assemblies with UNITY_EDITOR and UNITY_STANDALONE_WIN. Only existing CS0649 Inspector-field warnings. |
| Alpha envelope review | Passed | Symmetric clamped smoothstep gives alpha zero at both endpoints and one in the middle, with per-segment vertex interpolation. |
| Unity visual/interaction review | Not run | No Unity runtime verification in this task. |

## Performance

Not profiled; no performance improvement claimed. Same mesh size, no added collections or component lookups in the mesh loop.

## Limitations and follow-up

Restart Play Mode after compilation. Observe both wave directions for at least 15 seconds, check portrait/landscape, pause motion and verify tips blend into the background. Compilation does not establish visual quality.

## Rollback

Remove EndOpacity and restore uniform segment vertex color in TravelingWaveGraphic; retain the preceding CanvasRenderer dependency fix. Update the feature/visual documentation accordingly. No data migration or scene regeneration required.
