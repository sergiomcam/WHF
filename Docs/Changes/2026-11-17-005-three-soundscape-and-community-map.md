# Modification report — Three-soundscape game, community-map mockup and Android icon

- Report ID: 2026-11-17-005
- Date: 2026-11-17 (America/Mexico_City)
- Type: feature / fix / assets / documentation

## Request and resulting behavior

Flappy Cloud round 2 now combines three distinct original Explorer recordings rather than one. A fictional community soundscape map precedes Dwani's final overview. The Android launcher uses the existing yellow headphones artwork from Home instead of the Unity icon. Implemented; compilation, numerical checks, APK verification and targeted device checks are recorded below. The map remains a mockup, without upload or location access.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Three-source game-only playback | Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs | Deduplicate recordings, load three without replacement, scan peaks, common gain and synchronized DSP start; all-voice pause/cleanup and descriptive notices/results |
| Five-page Dwani sequence | Assets/_HearingNotion/Scripts/Content/DhwaniMockupController.cs | Add fourth-page community concept before final overview; cosmetic progress canceled on exit |
| Fictional map geometry | Assets/_HearingNotion/Scripts/Content/DhwaniCommunityMapGraphic.cs; Assets/_HearingNotion/Scripts/Content/DhwaniCommunityMapGraphic.cs.meta | Nonblocking code-drawn roads/park/water and six illustrative pins; new unique GUID |
| Regression fixtures | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Three distinct clips, common gain/headroom, all-voice lifecycle and five-page/map checks; wait for scheduled playback before assertion |
| Launcher artwork packaging | Assets/_HearingNotion/Editor/AndroidLauncherIcons.cs; Assets/_HearingNotion/Editor/AndroidLauncherIcons.cs.meta | Editor-only CPU composition of existing Home artwork; assign all supported legacy/round/adaptive slots |
| Build icon configuration | Assets/_HearingNotion/Editor/AndroidPrototypeBuild.cs | Apply launcher icon on each personal Android configure/build |
| Generated launcher textures | Assets/_HearingNotion/UI/AndroidIcons.meta; Assets/_HearingNotion/UI/AndroidIcons/headphones-background.png; Assets/_HearingNotion/UI/AndroidIcons/headphones-background.png.meta; Assets/_HearingNotion/UI/AndroidIcons/headphones-foreground.png; Assets/_HearingNotion/UI/AndroidIcons/headphones-foreground.png.meta; Assets/_HearingNotion/UI/AndroidIcons/headphones-legacy.png; Assets/_HearingNotion/UI/AndroidIcons/headphones-legacy.png.meta | 512-pixel palette-charcoal background, padded transparent adaptive foreground and opaque legacy composite; original artwork unchanged |
| Portable Android synchronization | Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/Content/DhwaniMockupController.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/Content/DhwaniCommunityMapGraphic.cs and .meta; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Editor/AndroidPrototypeBuild.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Editor/AndroidLauncherIcons.cs and .meta; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/UI/AndroidIcons and accompanying metadata; Builds/AndroidPatched-2026-11-06/ProjectSettings/ProjectSettings.asset | Matching source/GUIDs, portable settings and media preserved; Android icon settings generated through Unity |
| APK and fallback | Builds/AndroidPatched-2026-11-06/Builds/Android/HearingNotion.apk; Builds/AndroidPatched-2026-11-06/Builds/Android/HearingNotion-before-20261117-005.apk | Updated personal test APK; retained previous tested demonstration APK, without uninstall/data clearing |
| Current feature inventory and guides | Docs/FEATURES.md; Docs/FlappyCloud.md; Docs/DhwaniFuture.md; Docs/AndroidDeployment.md; AGENTS.md | F-017/F-024/F-025 updates, new F-026 map/F-027 icon, algorithm/lifecycle/privacy/icon conventions |
| Recurring QA guidance | Docs/Test.md; Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md | Existing repeated game/media/UI/device workflow updated instead of duplicate skill; explicit invocation only |
| Modification traceability | Docs/Changes/2026-11-17-005-three-soundscape-and-community-map.md; Docs/Changes/README.md | One coherent report and index entry; authorized Markdown publication only |

## Decisions and implications

No package, build-scene, questionnaire schema, participant-data path, permissions or backend changes. Main scene and open desktop Editor preserved. Existing source/artwork GUIDs preserved; new graphic, icon helper and texture metadata are synchronized to the portable copy. No media samples, source levels, media-library hashes or startup-preview gain were changed.

Game candidates are original recordings deduplicated by SHA-256, with path fallback. Three buffered 2D looping sources start together at DSP time +80 ms. A reusable 4096-frame buffer scans finite, nonzero PCM; common gain is min(1, 0.9 / summed absolute sample peaks). This is input sample headroom, not true-peak/acoustic calibration, validated distraction exposure or guaranteed increased perceived loudness. Focus loss while loading/scanning defers playback until another visitor action. Pause, results, exit, reset and destruction affect all owned clips. See [game guide](../FlappyCloud.md) for primary Unity API references. Results remain descriptive: practice, chance and fatigue prevent causal interpretation.

The map's five community pins and sixth demo contribution are fictional. A 1.2-second progress indication changes appearance only. No recording, GPS, upload, network tiles or real community data. Existing three reference interfaces and source overview remain.

Launcher composition reuses headphones-hero-v2.png, with charcoal #4A4C49 background. Adaptive foreground occupies 60% of its canvas; legacy/round artwork 82%. All 18 slots assigned using Unity PlayerSettings API; no runtime icon texture copies or original artwork edits. Launcher branding does not remove the Unity startup splash. App ID/signing identity unchanged.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| C# and model regression | Passed | run_project_checks.ps1: Editor/Windows/Android-symbol runtime compilation, Editor tools, game numerical checks and packaged-media integrity; checks-icon.log |
| Content and skill structure | Passed | English content validator; existing QA skill structural validator with existing local PyYAML; links checked separately |
| Mix numerical headroom | Passed | 18 distinct original source hashes; 816 possible three-source combinations satisfy the common-gain sample-peak bound using existing measured peaks; numerical only |
| Portable player build | Passed | Unity 2022.3.62f2 headless IL2CPP ARM64/ARMv7 build, final build-icon.log success and process exit 0 |
| APK integrity/signature | Passed | v1/v2 signing; 57 bundled media hashes/sizes and native video Activity DEX verified; existing two META-INF signature-coverage warnings unchanged |
| APK identity | Passed | 1,449,602,728 bytes; SHA-256 43584804393c9fece98cd7c1aa6d2866efe68552db527701504cb47e2ce23a34 |
| Packaged launcher resources | Passed | Application resolves adaptive XML with background then foreground; matching density resources generated; 18 Unity slots assigned |
| AX85 game mix | Passed | Actual three-source build played Dentist + Carpentry + Rock concert; shared gain 0.7051 and sample-peak bound 0.9000; user confirmed audible and stopped on pause; resume, final comparison (+10 noisy points), Retry and exit checked |
| AX85 preparation interruption | Passed | Home interruption during preparation returned paused with ready notice, without background start; rapid exit during second load returned Home without later mix-ready log or observed late playback |
| AX85 Dwani map | Passed | Actual page 4/5 progress, sixth demo pin, page 5/5 overview, Continue and Back; authentic local captures |
| Final icon build installation/launcher | Passed | adb install -r returned Success; actual AX85 app drawer shows yellow headphones on charcoal; launcher-icon.png retained locally; tapping it launched the expected optional About you screen, with no filtered Unity/AndroidRuntime exception |
| Full graphical Unity regression and fresh 4K captures | Not run | Prior graphical batch initialization repeatedly stalled; no new full native-suite completion or camera-render claim; headless build/direct device checks separate |
| All-device, landscape and long gameplay | Not run | Targeted AX85 portrait functional checks; final icon launch happened in landscape, but no complete landscape walkthrough; no blanket usability/acoustic claim |

Local native logs/captures stay in LocalEvidence/Android-2026-11-17-005 and tmp/20261117-005, excluded from documentation publication. No demographic profile was saved/deleted.

## Performance

No optimization claim or comparable before/after profiling. One paused three-clip AX85 snapshot reported total PSS 211,802 KB and RSS 344,208 KB; this is an observation, not a memory budget or stress result. Peak scanning yields periodically, allocates once per scan and avoids per-frame reallocation.

## Limitations and follow-up

The mix is educational and uncalibrated. Only one selected triple was physically listened to; numerical all-combination headroom is separate. Real uploads, maps, analysis and community services are not implemented. Full native suite, landscape and every variant's perceived output remain unverified. Existing offline verification from report 004 applies to unchanged bundled media paths; this update did not repeat a complete offline walkthrough. Android is a debug-signed personal-test build.

## Rollback

To restore the previous phone demonstration, install the retained HearingNotion-before-20261117-005.apk in place with adb install -r; do not uninstall or clear storage. Its verified previous SHA-256 is 43e5766b2b96a9f0b210fb425ac0c0aaa7874e6c29e2b225f8cdbb7a6424df8e. For source rollback, reverse only this task's controller/fixture/icon helper/configuration changes and matching portable copies; remove new icon references before removing their assets/metadata. Preserve unrelated work, source media and original artwork. Do not regenerate Main or overwrite open Editor work.
