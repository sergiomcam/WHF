# Modification report — wave CanvasRenderer dependency

- Report ID: 2026-10-19-010
- Date: 2026-10-19 (America/Mexico_City)
- Type: fix

## Request and resulting behavior

The user reported MissingComponentException on Traveling sound contours during RectMask2D clipping, triggered by Exposure Explorer startup forcing a canvas update. The wave graphic now explicitly creates/requires its renderer before masking registration. Implemented; runtime confirmation remains pending.

## Modifications

| File or asset | Change and purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Navigation/TravelingWaveGraphic.cs | Require RectTransform/CanvasRenderer; repair missing renderer before base Awake/OnEnable. |
| Assets/_HearingNotion/Scripts/Navigation/AmbientWaveAnimation.cs | Create renderer before graphic; repair reused references during initialization. |
| AGENTS.md | Record explicit custom uGUI component dependency convention. |
| Docs/FEATURES.md | Update F-008 status/details and history. |
| Docs/VisualRefresh.md | Explain dependency fix and runtime retest. |
| Docs/Changes/README.md and this report | Index and document the modification. |

## Decisions and implications

Unity Graphic assumes its CanvasRenderer remains valid; explicit ordering avoids relying on implicit base-component requirements. Use Unity-aware null checks. Do not change ExposureManager: its forced canvas update exposes the invalid graphic, rather than owning it. No package, scene, asset, GUID, schema, data-path, questionnaire or participant-data changes. Documentation publication uses the standing authorization; publication evidence is provided in the final verified commit link.

## Validation

| Check | Result | Evidence or reason |
| --- | --- | --- |
| Editor source compilation | Passed | All app C# compiled with installed Unity 2022.3.12f1 assemblies, UNITY_EDITOR. Only existing Inspector CS0649 warnings. |
| Windows source compilation | Passed | Same compiler/assemblies, UNITY_STANDALONE_WIN. Only existing Inspector CS0649 warnings. |
| Unity dependency inspection | Passed | Reviewed installed Graphic.canvasRenderer accessor and wave creation/activation paths. |
| Play Mode clipping, rendering and navigation | Not run | No Unity runtime execution available in this task; compilation cannot prove this fix. |

## Performance

Not measured; no performance gain claimed. Dependency checks occur during initialization/activation, not every animation frame.

## Limitations and follow-up

Exit Play Mode, wait for compilation, then press Play. Confirm startup and Exposure Explorer category/detail changes produce no CanvasRenderer exception. Observe traveling waves for 15 seconds, switch screens, test portrait/landscape, toggle reduced motion, and verify scrolling/clicks. Do not remove required renderer components while running.

## Rollback

Reverse this task's explicit renderer creation/requirement/lifecycle changes in the two wave scripts while preserving other animation logic. Update the referenced documentation to reflect rollback. No scene regeneration or data migration is needed.
