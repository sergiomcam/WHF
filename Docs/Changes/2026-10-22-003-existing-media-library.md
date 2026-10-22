# Modification report — use the existing media library directly

- Report ID: 2026-10-22-003
- Date: 2026-10-22 (America/Mexico_City)
- Type: fix / assets / documentation

## Request and resulting behavior

The existing audiovisual library should be used without adding separate copies. The Windows prototype now indexes and plays the existing 51 comparison WAVs and five original videos directly. The 28 records and section mappings remain unchanged. The previously generated 56 duplicate playback files and their metadata were removed from the project after verifying their hashes and exact cleanup location. Original source media was not changed or removed.

## Modifications

| File or asset | Change and purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs | Catalog ExternalRoot, direct local file URLs, missing-file UI feedback and startup diagnostics |
| Tools/Audio/package_app_media.py | --link-existing indexes files without copying/transcoding; preserves optional packaging mode |
| Tools/Tests/validate_packaged_media.py | Resolve and validate external or packaged libraries |
| Assets/_HearingNotion/Resources/MediaCatalog.json | Local-only version 2 index with external root and relative paths |
| Assets/StreamingAssets/HearingNotionMedia and metadata | Remove only verified generated duplicates; no original assets touched |
| AGENTS.md and affected Docs guides, feature catalog and history | Document direct-library behavior, deployment limitations and this correction |

## Decisions and implications

The local catalog contains private filesystem configuration and remains excluded from publication. No participant storage, scene change, build-setting change or dependency change. Stable item IDs, comparison gains, method labels and source bytes are preserved. The local prototype depends on its existing external folder; a portable build requires deliberately configuring or packaging media later. Original HEVC videos depend on installed codecs; compatible converted duplicates are no longer used. Missing files produce an actionable message rather than automatic replacement or playback.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| External catalog | Passed | 28 unique items, 56 SHA-256 hashes, 23 aligned audio sets, 18 activity links and path containment checks |
| Duplicate cleanup | Passed | Checked all 56 file hashes against original/reference or recorded converted hashes and verified exact project-owned removal root |
| Editor/Windows source compilation | Passed | Unity 2022.3.12f1 assemblies; existing Inspector-field warnings only |
| Unity Play Mode, device playback and missing-folder interaction | Not run | No interactive Unity verification performed |

## Performance

Not profiled. Removed 1,392,154,325 bytes of duplicate media from Assets. This is a disk-content count, not a memory or runtime-speed measurement.

## Limitations and follow-up

Keep external files available offline. Moving the library requires regenerating the local index. Other computers do not inherit this private folder configuration. Original HEVC compatibility and actual audio/video output remain unverified in Unity. The previous integration report describes the earlier packaged configuration, superseded by this correction.

## Rollback

To deliberately return to packaged playback, run the packaging tool with a local FFmpeg executable instead of --link-existing; this creates new playback copies without modifying source media. Restore the corresponding catalog configuration and documentation. Do not restore duplicates merely to validate the direct-library mode.
