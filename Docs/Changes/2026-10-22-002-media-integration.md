# Modification report — offline audio and video integration

- Report ID: 2026-10-22-002
- Date: 2026-10-22 (America/Mexico_City)
- Type: feature / content / assets / documentation

## Request and resulting behavior

Integrate the processed audio and informative videos into the app. Implemented local playback infrastructure: Exposure Explorer links to 18 original/protected pairs; Sound Experience also provides five three-version WHIS comparisons; Hearing Health contains recommendations and five selectable videos. Playback requires an explicit action and stops on navigation/reset. Unity playback verification remains pending.

## Modifications

| File or asset | Change and purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs and metadata | Shared on-demand transport, cancellable loading, version controls, method notes, video surface, scrolling, interruption/reset cleanup and output-gain cap |
| Assets/_HearingNotion/Scripts/Core/AppManager.cs | Explicit runtime controller installation |
| Assets/_HearingNotion/Scripts/Exposure/ExposureManager.cs | Identify packaged examples and link activity to comparison |
| Assets/_HearingNotion/Scripts/Navigation/GuidedExperienceController.cs | Replace obsolete unavailable-audio introduction |
| Assets/_HearingNotion/Resources/MediaCatalog.json and metadata | Local 28-record catalog with 56 media references/hashes |
| Assets/StreamingAssets/HearingNotionMedia and generated metadata | 51 unchanged comparison WAVs and five compatible video copies; no source originals modified |
| Tools/Audio/package_app_media.py | Reproducible copying, shared-format verification and H.264/AAC video conversion |
| Tools/Tests/validate_packaged_media.py | Hash, path, activity-mapping and comparison-alignment checks |
| .gitignore | Exclude local media and source-derived catalog from accidental publication |
| AGENTS.md, Docs/AppArchitecture.md, Docs/MediaPlayback.md, Docs/FEATURES.md, Docs/README.md, Docs/Changes/README.md | Current architecture, usage, limits, feature history and report index |

## Decisions and implications

Existing Main scene and GUIDs are preserved; no build-setting or package dependency change. StreamingAssets is deliberately at Assets root for offline builds. No visitor data persistence or export. The library is authored content, separate from manually imported review-pending audio. Runtime uses standard Unity AudioSource, UnityWebRequest and VideoPlayer; DSP remains offline. Scientific assumptions and shared gains are preserved; see [playback guide](../MediaPlayback.md), [protection batch](../SoundscapeProtection.md) and [WHIS batch](../WHISSongBatch.md). Locally downloaded FFmpeg is a build-authoring tool under ignored tmp, not an app runtime dependency. GitHub publication is documentation only.

## Validation

| Check | Result | Evidence or reason |
| --- | --- | --- |
| Editor/Windows source compilation | Passed | Unity 2022.3.12f1 assemblies; existing Inspector-field warnings only |
| Audio source/copy preservation | Passed | Packaging checks SHA-256 and stereo WAV content without audio transformations |
| Catalog hashes, activity mappings, aligned comparison formats | Passed | All 56 hashes, 18 activity mappings and 23 aligned sets passed Tools/Tests/validate_packaged_media.py |
| Video conversion/decode integrity | Passed | All five H.264/AAC copies decoded end-to-end without errors; two extracted stills visually inspected |
| Unity Play Mode, actual listening, target-device video, portrait/landscape | Not run | No interactive Unity verification performed |
| Scientific/perceptual/individual-fit validation | Not established | Numerical export checks do not establish perceptual or clinical equivalence |

## Performance

Not benchmarked. One audio clip/one video transport loads on demand; full libraries are not decoded at startup. Packaged media totals 1,392,154,325 bytes (about 1.39 GB), down from about 2.38 GB before video conversion. Full-length audio contributes substantially to build size. No FPS, latency, memory or synchronization claim.

## Limitations and follow-up

Actual output-level and device checks remain required. Switching versions reloads at approximately the same time and can produce a decoding gap. Pause/navigation mute immediately; starts ramp gain. Videos require editorial, caption and public-distribution review. The previously clipped source remains explicitly flagged. No microphone, tinnitus tone playback or Flappy Cloud noise condition is added. See the playback guide for the full runtime checklist.

## Rollback

Remove this controller's AppManager installation and restore the task-specific Explorer/guided wording. Remove only this task's local catalog/media and controller metadata if no longer needed; preserve original research exports, sources, scene GUIDs and unrelated scripts. Revert the corresponding documentation entries and ignore rules deliberately. Documentation publication does not upload media or synchronize local Git history.
