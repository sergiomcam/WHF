# Modification report — make linked audio visible in Explorer

- Report ID: 2026-10-22-005
- Date: 2026-10-22 (America/Mexico_City)
- Type: fix / UI

## Request and resulting behavior

The user reported no uploaded content in Explorer. The screenshot showed the linked-example notice followed by the empty optional upload slot; the player link was farther down the scroll. The activity's audio status and Escuchar ejemplo control now appear directly after its title. Additional uploads are hidden under optional editing controls. Existing linked files need no upload or copy. The button opens Sound Experience; playback still requires Reproducir at comfortable device volume.

## Modifications

| File or asset | Change and purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Exposure/ExposureManager.cs | Move player link above details, collapse optional authoring, reset editing on activity/session changes, check catalog/file availability and show accurate missing-file states |
| Assets/_HearingNotion/Resources/MediaCatalog.json.meta | Use TextScriptImporter for the JSON TextAsset, preserving its GUID |
| Tools/Audio/package_app_media.py | Generate appropriate importer metadata for future JSON catalogs |
| Docs/ExposureExplorer.md, Docs/MediaPlayback.md, Docs/FEATURES.md, Docs/Changes/README.md | Update navigation guidance, feature history and report index |

## Decisions and implications

Existing library files remain in their original external location. No media copies, participant storage, scientific processing, scene, package or build-setting changes. Chart-only activities have no invented recording. Missing pairs disable the comparison link with an explanatory status. Optional imported files remain review-pending. Media availability is checked on activity/status changes, never every frame.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| Existing library integrity | Passed | validate_packaged_media.py: 56 hashes, 23 aligned audio sets, 18 mapped activities, 28 catalog records |
| Editor and Windows source compilation | Passed | Unity 2022.3.12f1 assemblies, existing Inspector-field warnings only |
| Metadata | Passed static inspection | JSON now uses TextScriptImporter with existing GUID retained |
| Unity Play Mode, responsive layout and actual playback | Not run | Screenshot inspected; revised controls and importer need fresh Play Mode confirmation |

## Performance

Not profiled; no speed or memory claim. File availability checks occur only during UI status refresh.

## Limitations and follow-up

Restart Play Mode after Unity imports the changed scripts/catalog. Select an activity and use Escuchar ejemplo, then Reproducir. Confirm both orientations, missing-file messages and optional editing controls. Actual sound output remains unverified by the agent.

## Rollback

Reverse only this task's Explorer control ordering, authoring-group and catalog-availability changes, and related documentation. Preserve existing media and catalog GUID. Do not restore incorrect JSON importer metadata as a routine rollback.
