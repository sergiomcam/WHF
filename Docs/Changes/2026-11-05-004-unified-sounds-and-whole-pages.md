# Modification report — unified sounds and whole-page scrolling

- Report ID: 2026-11-05-004
- Date: 2026-11-05 (America/Mexico_City)
- Type: fix / feature / navigation / documentation

## Request and resulting behavior

Fix invisible Hearing Health videos and put controls below each frame; consolidate Sound Experience and Exposure Explorer under one Home entry; initialize volume at midpoint; make entire pages, including navigation and footer, move on swipe. Implemented locally. The Sound Experience hub offers Soundscapes and Hearing examples, with the soundscape catalog shown only once. Video tint is corrected, controls are below their frame, and native tests inspect actual decoded pixels. Page movement replaces the previous fixed-header gesture-forwarding approach.

## Modifications

| Main change | Script, document or asset modified | Purpose / effect |
| --- | --- | --- |
| Visible video and controls below frame | Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs | White RawImage tint, black unloaded placeholder, below-frame Play/Pause/Stop; preserve one decoder and buffered audio lifecycle |
| Separate sound branches without catalog repetition | Assets/_HearingNotion/Scripts/Audio/SoundHubController.cs; Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs | New two-choice hub; reuse activity catalog and selected-pair transport; hearing branch clears activity context and displays songs only |
| Startup, route and gain default | Assets/_HearingNotion/Scripts/Core/AppManager.cs; Assets/_HearingNotion/Scripts/Data/AppSession.cs; Assets/_HearingNotion/Scripts/Core/ListeningSetupController.cs | Explicit hub installation, appended SoundHub enum, fresh-session 0.125 gain and midpoint slider in unchanged 0–0.25 range |
| Full-page content ownership | Assets/_HearingNotion/Scripts/Navigation/WholePageScroll.cs; Assets/_HearingNotion/Scripts/Navigation/PageGestureInstaller.cs | Wrap ScreenView itself as outer scroll content, expand inner modules, disable inner module scroll/masks; all page controls/footer move together |
| Responsive template and eight-card Home | Assets/_HearingNotion/Scripts/Navigation/ResponsiveScreenLayout.cs | Restore/capture layout across orientation, account for delayed viewport size; remove separate Explorer card from Home layout |
| Activity detail targeting | Assets/_HearingNotion/Scripts/Exposure/ExposureManager.cs | Request outer-page ScrollTo for activity details instead of changing a disabled inner scroll |
| New component metadata | Assets/_HearingNotion/Scripts/Navigation/WholePageScroll.cs.meta; Assets/_HearingNotion/Scripts/Audio/SoundHubController.cs.meta | Unique new GUIDs; existing asset GUIDs preserved |
| Stronger native tests | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Midpoint, actual hub actions, below-frame controls/white tint, decoded nonblack video frames, header/navigation/footer movement and updated capture layout |
| Local verification evidence | LocalEvidence/2026-11-05-004-prototype-review.txt; LocalEvidence/nov05-004-delivery.log; Marketing/Screenshots/*.png | Native regression and 32 actual 4K renders including hub and five playing-video views; no media/evidence publication |
| Current module and architecture guides | Docs/SoundExperienceHub.md; Docs/PageScrolling.md; Docs/ExposureExplorer.md; Docs/MediaPlayback.md; Docs/ListeningSetup.md; Docs/HomeScene.md; Docs/AppArchitecture.md | Explain merged entry, real whole-page behavior, video root cause, midpoint and lifecycle constraints |
| Instructions and review documentation | AGENTS.md; Docs/Test.md; Docs/Marketing.md; Docs/README.md | Record changed architecture, stronger visible-frame checks, capture inventory and navigation |
| Recurring QA skill | Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md | Update repeated workflow using skill-creator guidance: visible decoded frames, hub actions, midpoint and actual whole-page movement; explicit invocation only |
| Feature and change traceability | Docs/FEATURES.md; Docs/Changes/README.md; Docs/Changes/2026-11-05-004-unified-sounds-and-whole-pages.md | Update affected IDs and add F-021 unified hub; required three-column modification and four-column history tables |

## Decisions and implications

The video RawImage was black, multiplying the video texture to black. A playing VideoPlayer did not prove a visible result; the new test checks advancing frames and nonblack texture pixels as well as white tint and explicit card controls. Physical speech/output remains a separate check. Existing media files, hashes, compatibility cache and codecs are unchanged. Below-frame controls select the correct card internally; scrolling does not autoplay.

SoundHub is appended to the enum, preserving earlier serialized values. The original ExposureExplorer route and IDs are reused for Soundscapes. Its hidden Home button remains as a styling template until all runtime cloning finishes; the visible Home layout has one sound entry and eight cards. The player no longer repeats all 18 soundscapes. Existing five-song hearing examples and their WHIS/protection provenance are unchanged. The six-stage guided order remains unchanged; free exploration uses the new hub.

WholePageScroll reparents each ScreenView into a full-viewport host at runtime, preserving all direct-child names and manager references. Inner module scrolls/masks are disabled and content expands, moving navigation/footer below it. Headers, artwork, content and navigation actually move with the page; this supersedes the previous fixed-navigation behavior. Background art keeps viewport proportions. Responsive template restoration/capture and a delayed CanvasScaler size check prevent a large top gap observed during portrait capture. Demographic/listening dialogs remain modal overlays; their field scrolling remains separate. No saved scene regeneration, Build Settings change, dependency upgrade, backend, telemetry or participant-storage change.

Fresh sessions use 0.125 midpoint gain within the same 0–0.25 scale. Reopening after acknowledgment preserves the chosen visit gain. The 6 kHz preview keeps its separate -12 dB trim and still requires explicit Play. Midpoint is a digital setting, not acoustic calibration or a safe-exposure claim. HNAI wording, scoring restrictions and local consent rules are unchanged.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| Editor/Windows C# and Editor tools | Passed | Tools/Tests/run_project_checks.ps1; expected Inspector/test-override CS0649 warnings only |
| Game model and source media integrity | Passed | Deterministic model checks through 180 seconds; 28 records, 56 hashes, 23 comparison sets and 18 activity mappings |
| Unified menu and midpoint | Passed | Native single Home entry, actual two hub actions and 0.125 slider default in unchanged range |
| Visible video regression | Passed | All five videos decode nonblack frames through their real below-frame controls; white image tint checked; playing-view captures retained |
| Actual whole-page movement | Passed | Native wheel/drag changes Heading, Back and bottom-note positions together; inner module scrolling disabled; both orientations rendered |
| Broader native regression | Passed | 90 checks, completed 2026-11-06 01:50:20 UTC (2026-11-05 local), including 51 audio variants, five visible videos, buffered cleanup, startup/modal behavior, game results and guided dismissal |
| Visual review and capture | Passed with limits | 32 real Unity PNGs at 3840×2160 or 2160×3840; hub portrait and actual playing video inspected. A portrait top-gap issue found in review was corrected by delayed-viewport sizing; no claim of complete human/device review |
| Skill, metadata and documentation | Passed | Skill structural validator, unique new GUIDs and changed-document relative links; no automatic skill discovery claim |
| Physical listening, real touch feel, keyboard/long-page usability | Not run | Muted/synthetic native checks and camera renders do not establish physical audibility or full accessibility |
| Documentation publication | Pending final verification at report authoring | Publish authorized Markdown on inspected default-branch head, use expected-head protection and verify contents; final delivery provides commit link |

## Performance

No optimization benchmark, FPS or memory improvement claimed. Runtime scroll references and template placements are cached; content-height checks do not force Canvas rebuilds per frame. Layout applies on height/viewport changes. One on-demand media decoder and one render target remain; video frames do not each allocate their own player. Buffered WAV loading preserves the earlier native crash fix.

## Limitations and follow-up

Navigation now scrolls away with the page as requested; return toward page start/end to reach those controls. Very long lists and real touch/keyboard behavior need device review. Dialogs remain separate modal overlays. The external media library must be available offline. The app remains mixed English/Spanish and does not introduce new hearing simulations, clinical interpretation or research data collection. Playing-frame screenshots stay local and require media-rights review before marketing use.

## Rollback

Reverse hub/default-gain changes and remove the runtime whole-page wrapper installation together if needed; restore prior forwarding behavior only deliberately. Revert media tint/controls independently only if another visible-video solution is supplied. Preserve the buffered WAV crash fix, original media and consented local profiles. Remove the new scripts and their metadata together; retain existing GUIDs and the historical appended route identity rather than renumbering serialized routes. Keep reports/history for traceability. Documentation connector commits do not synchronize local Git history.
