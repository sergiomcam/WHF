# Modification report — Android interaction and presentation corrections

- Report ID: 2026-11-10-001
- Date: 2026-11-10 (America/Mexico_City; work began 2026-11-09)
- Type: fix / features / presentation / documentation

## Request and resulting behavior

Address the first phone review: hardware Back, natural full-screen video playback, same-page soundscape comparisons after context, left-aligned HNAI responses, research-stage overlap, softer popup corners, larger game area with explicit noisy-round Ready, and reference-inspired dark header/footer. Implementation preserves Spanish instrument wording, scientific content, source media and stable route IDs. Rebuild and final device status are recorded below; compilation alone does not establish these fixes on Android.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Central Back dispatch | `Assets/_HearingNotion/Scripts/Navigation/NavigationManager.cs`; `Assets/_HearingNotion/Scripts/Navigation/GuidedExperienceController.cs`; `Assets/_HearingNotion/Scripts/Core/DemographicPromptController.cs`; `Assets/_HearingNotion/Scripts/Core/ListeningSetupController.cs` | Hardware Escape/Back follows app history; startup/guided modals dismiss first without saving profile data. Remove duplicate guided Escape handling. |
| Inline soundscape comparison | `Assets/_HearingNotion/Scripts/Exposure/ExposureManager.cs`; `Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs` | Move shared protection transport into activity details after description, prevention and sources. Hide protection rewind; retain direct toggles/menu/video routes and buffered cleanup. |
| Native full-screen video entry | `Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs` | Explicit Android device player uses existing video cache, Full controls and AspectFit; inline remains available. |
| Response alignment | `Assets/_HearingNotion/Scripts/Assessment/AwarenessCheckManager.cs`; `Assets/_HearingNotion/Scripts/Navigation/WindowStyle.cs` | Give responses stable presentation identity and preserve left alignment through shared styling. No JSON wording or response value changes. |
| Preserve research image proportions | `Assets/_HearingNotion/Resources/Research/demographic-exposure.png.meta`; `Assets/_HearingNotion/Resources/Research/yans-factors.png.meta`; `Assets/_HearingNotion/Resources/Research/yans-sum.png.meta`; mirrored portable metadata | Disable non-power-of-two rescaling without changing original figure pixels or GUIDs. |
| Stable research content | `Assets/_HearingNotion/Scripts/Content/ResearchSourcesController.cs`; `Assets/_HearingNotion/Scripts/Navigation/LayoutAspectHeight.cs`; corresponding new `.meta` | Two fixed-height top selector rows; measured wrapped summary and width-derived figure heights avoid absolute overlap. |
| Enlarged game and explicit start | `Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs`; `Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs` | Larger fitted arena with gameplay controls kept within the viewport; Continue waits indefinitely for centered Ready; remove countdown and duplicate Escape pause handling. Regression checks no automatic start after seven seconds. |
| Soft surfaces and dark chrome | `Assets/_HearingNotion/Scripts/Navigation/RoundedCardGraphic.cs`; `Assets/_HearingNotion/Scripts/Navigation/HomeMenuStyle.cs`; `Assets/_HearingNotion/Scripts/Navigation/ScreenChrome.cs`; `Assets/_HearingNotion/Scripts/Navigation/ScreenBandGraphic.cs`; new chrome `.meta` files | Configurable popup radius, curved dark/yellow bands, existing headphones and real footer routes. No fabricated analysis tool. |
| Responsive page geometry | `Assets/_HearingNotion/Scripts/Navigation/ResponsiveScreenLayout.cs`; `Assets/_HearingNotion/Scripts/Navigation/WholePageScroll.cs` | Separate headings/introduction, include research selector offset and footer allowance, preserve whole-page scrolling. |
| Portable source synchronization | `Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/`; `Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Editor/` | Mirror app-owned sources/checks while retaining private portable media catalog and bundled files. Original desktop Editor remains open. |
| Updated guides | `AGENTS.md`; `Docs/AppArchitecture.md`; `Docs/AndroidDeployment.md`; `Docs/ExposureExplorer.md`; `Docs/MediaPlayback.md`; `Docs/ResearchSources.md`; `Docs/SpanishQuestionnaire.md`; `Docs/FlappyCloud.md`; `Docs/HomeRedesign.md`; `Docs/PageScrolling.md` | Document current responsibilities, flow and native-player limits. |
| QA and feature traceability | `Docs/FEATURES.md`; `Docs/Test.md`; `Docs/Skills/unity-prototype-review/SKILL.md`; `Docs/Skills.md`; `Docs/Changes/README.md`; this report | Update affected feature IDs, repeated test workflow, validation and modification history. |

## Decisions and implications

Native full-screen playback uses [Unity's documented API](https://docs.unity3d.com/2022.3/Documentation/ScriptReference/Handheld.PlayFullScreenMovie.html), checked 2026-11-09. It starts at the beginning, pauses Unity and uses device media volume rather than app gain. It does not implement background notification transport/MediaSession. Inline playback remains buffered with existing cancellation and cache ownership. No microphone, telemetry, consent collection, research scoring, scientific DSP or original media changed. The supplied reference image informed the dark design; no phone frame was imported into the app. Footer destinations are Home, Sounds, Research, Learn and You; Research replaces the reference's unimplemented Analyze implication.

Existing asset GUIDs were retained. New scripts receive new GUIDs and are copied with metadata. No scene regeneration, package upgrade or desktop build-setting change. The portable build helper retains its established personal-test/debug-signing configuration. No real demographic profile was saved/deleted in tests. AI assistance implemented source/UI and test/documentation changes; compilation and numerical checks do not establish clinical or acoustic validity.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| Editor/Windows/Android-symbol compile | passed | `Tools/Tests/run_project_checks.ps1`; expected Inspector reference warnings only. |
| Domain model and media integrity | passed | Flappy model checks; 28 records, 56 catalog file hashes and 18 activity mappings. |
| Language/instrument invariants | passed | `validate_english_content.py`; four English summaries preserve numbers/figures; 21 activity descriptions; 22 Spanish items and five response mappings intact; UTF-8 scan passed. |
| Updated full native regression | passed | 95 PASS lines; final COMPLETE 2026-11-10T07:28:05.1465698Z in the isolated patched project. Includes seven-second Ready wait and subsequent buffered sound playback. Final footer retest passed, and its actual lower-page render shows the dark band and all five links. |
| Earlier native attempt | failed | Initial new Ready test waited two seconds after starting, missed short unattended play and timed out. Corrected the test timing and obtained the passing run above. A concurrent launch was rejected by Unity's project lock; later process inventory used elevated visibility and preserved the original Editor. |
| Visual review | passed | Actual native portrait/tall Home, HNAI, research and game renders reviewed. Heading/introduction overlap was corrected; Home footer placement received a final retest before build. |
| Final refinement APK | passed | Build exit 0; v1/v2 signatures and all 57 in-APK media hashes/sizes verify. APK 1,444,588,487 bytes; SHA-256 `f74190e9069d6226b887d216966245e0327dff321b904bb21a311f6fc0c9411b`. In-place install returned Success. |
| Final device refinements | passed | Actual AX85 captures show original chart proportions, left-aligned HNAI choices, reachable Pause/Resume, centered Ready still waiting after seven seconds, and native on-screen Pause switching to the Play icon. Native return and Home navigation passed; checked app-specific log filters showed no crash/Unity exception. No demographics saved/deleted or HNAI answers submitted. |
| Skill structural validator | failed | Bundled validator lacks PyYAML; no global install added. Required frontmatter/links reviewed manually; behavioral regression verified separately. |
| Android build/signature/media | passed | Patched IL2CPP ARM64/ARMv7 build exit 0; v1/v2 signatures verify; all 57 in-APK media hashes/sizes match. First deployed correction APK: 1,444,428,207 bytes; SHA-256 `8c6a5ba445ade28efa4dfbfbdb92d7082db680dc9ca60942adfa957c4c60d3aa`. |
| First physical correction retest | passed | Updated APK installed in place. Phone Back dismissed both startup modals and returned from Research, Sound Hub and Health. All four research selectors retained their positions; source/YANS figures remained separate. Inline Original/Protection/menu/video controls followed source context with no rewind. Native full-screen video rendered with transport/seek controls and returned with Back (a first press can hide visible controls). Noisy game waited eight seconds for Ready, then showed final two-round feedback. |

## Performance

No profiling or frame-time improvement claim. Existing procedural icons/graphics and dirty/size-based layout remain; no extra image assets or dependencies introduced.

## Limitations and follow-up

The final refinement APK is installed and a targeted AX85 retest passed. Complete verification of every media file, orientation and interruption case remains beyond this targeted pass. Desktop renders and muted Editor video/audio tests do not prove phone controls, output comfort, rotation or lifecycle behavior. Native video uses phone media volume; start low and stop if uncomfortable. Immersive Flappy retains its own header/exit layout. Native seek controls are available, but precise seek-position and hardware media-key behavior were not conclusively verified. The earlier Environmental category word wrap remains a cosmetic limitation. Stopped Editor Home preview does not establish runtime chrome. No public/store release is performed. Actual device captures remain local under `LocalEvidence/Android-2026-11-10/`; native 4K renders remain in the portable project’s `Marketing/Screenshots/`.

## Rollback

Revert only the listed task source/presentation changes and synchronize those files back into the portable project; preserve unrelated edits and private media/catalog. Keep current and pre-correction APKs separately; use an in-place install only with matching signing identity. Do not uninstall or clear visitor data automatically. Do not regenerate Main. Documentation may be reverted independently of installed app state.
