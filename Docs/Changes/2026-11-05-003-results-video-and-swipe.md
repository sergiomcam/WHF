# Modification report — results, inline videos and page gestures

- Report ID: 2026-11-05-003
- Date: 2026-11-05 (America/Mexico_City)
- Type: fix / feature / content / documentation

## Request and resulting behavior

Implement six requested corrections: reduce only the 6 kHz reference by 12 dB, show complete two-round game feedback and next steps, center Entendido, accept page-wide swipe gestures, always show About you before listening volume, and put video controls inside separate scrollable topic frames. Implemented locally. The original media files, shared gain range and HNAI wording are unchanged.

## Modifications

| Main change | Script, document or asset modified | Purpose / effect |
| --- | --- | --- |
| Preview-only attenuation | Assets/_HearingNotion/Scripts/Core/ListeningSetupController.cs | Multiply preview output by 0.25118864 (-12 dB amplitude); preserve gain slider and other audio; show only after demographic handoff |
| Consistent startup order | Assets/_HearingNotion/Scripts/Core/DemographicPromptController.cs | Always About you first, regardless of earlier dismissal; allow overlay-background gestures; no automatic local saving |
| Visible game comparison | Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs | Large scrollable final panel with both points/gaps/times, point difference, sourced general context and next actions; Retry/Exit remain reachable |
| Centered guided control | Assets/_HearingNotion/Scripts/Navigation/GuidedExperienceController.cs | Explicit centered TMP alignment and zero margins for Entendido; update obsolete Explorer/audio instructions |
| Page-wide gestures | Assets/_HearingNotion/Scripts/Navigation/FullScreenSwipeSurface.cs; Assets/_HearingNotion/Scripts/Navigation/PageGestureInstaller.cs; Assets/_HearingNotion/Scripts/Core/AppManager.cs | Forward background drag/wheel to visible scroll content after runtime setup; preserve inner scrolls, fixed navigation and game taps |
| New component metadata | Assets/_HearingNotion/Scripts/Navigation/FullScreenSwipeSurface.cs.meta; Assets/_HearingNotion/Scripts/Navigation/PageGestureInstaller.cs.meta | Unique GUIDs; pre-existing GUIDs and scene untouched |
| Consistent borderless panels | Assets/_HearingNotion/Scripts/Navigation/AppArtwork.cs | Transparent module-panel background remains after responsive resize |
| Inline video topics | Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs | Five frame/control pairs with explicit Play/Pause and Stop inside each frame; one shared transport; no selection menu or scroll autoplay; compact prevention introduction and remove visitor-facing codec details |
| Native regression | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Popup order, -12 dB constant, in-frame buttons, background wheel/swipe, final results and centered guided dismissal; correct harness tutorial state before testing pause/resume |
| Local evidence and 4K renders | LocalEvidence/2026-11-05-003-prototype-review.txt; LocalEvidence/nov05-003-controls.log; Marketing/Screenshots/*.png | Muted engine evidence and 25 actual app renders including final comparison and guided popup pairs; exclude from publication |
| Behavior and scientific provenance | Docs/ListeningSetup.md; Docs/Demographics.md; Docs/FlappyCloud.md; Docs/MediaPlayback.md; Docs/PageScrolling.md; Docs/GuidedExperience.md | Explain actual UX, sourced general effects and physical-device limitations |
| Architecture and validation guides | AGENTS.md; Docs/AppArchitecture.md; Docs/Test.md; Docs/Marketing.md; Docs/README.md | Record lifecycle, gestures, checks, capture inventory and review navigation |
| Repeated QA skill | Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md | Extend existing recurring QA using skill-creator guidance; explicit invocation only; no extra permissions or global installation |
| Feature/history documentation | Docs/FEATURES.md; Docs/Changes/README.md; Docs/Changes/2026-11-05-003-results-video-and-swipe.md | Trace changed F-002/009/010/015/017/018/019 and this task in required tables |

## Decisions and implications

No dependency, saved-scene, Build Settings, microphone, network service or participant-schema changes. Existing media files and common-gain comparison relationships are preserved. The 6 kHz preview alone receives an output-stage -12 dB factor, so the same slider no longer produces the previous preview level. This is digital attenuation, not measured ear-level SPL, calibration or safe-dose assurance. About you always appears first; the legacy dismissed preference does not bypass it. Explicit local consent remains required to save demographics.

FullScreenSwipeSurface forwards gestures rather than placing an input-blocking overlay over controls. Headers/navigation stay fixed; content remains clipped to protect navigation. Largest visible vertical overflow is selected at gesture start, then reused until release. Discovery occurs per gesture, not per frame. Direct gestures inside ScrollRects remain native. Game taps are excluded; its final panel has its own large scroll region. This is page-wide input, not every element scrolling as one giant document.

Video topics share one VideoPlayer/RenderTexture; only explicit Play starts decoding. Switching cards stops the prior video and detaches its old frame texture. Pause/error/timeout/navigation/reset behavior remains. A black unloaded frame is intentional, not a fabricated thumbnail. No new media is imported or redistributed.

Final game scores are actual temporary runs, with delta defined as soundscape minus quiet. General educational context is supported by [WHO Europe Noise](https://www.who.int/europe/health-topics/noise), [NIOSH noise/stress](https://www.cdc.gov/niosh/bulletin/2018/noise-effects.html), [NIOSH fatigue](https://www.cdc.gov/niosh/fatigue/about/) and [Wright et al. 2016](https://pubmed.ncbi.nlm.nih.gov/27157685/) (54 healthy adults, quiet/urban/social conditions and cognitive tasks). These sources do not validate Flappy Cloud, identify visitor symptoms, or allow attribution of score differences to noise. Practice, fatigue, chance and play duration remain explicit alternatives. See the linked game guide for source context.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| Editor/Windows and Editor-tool compilation | Passed | run_project_checks.ps1; expected Inspector/test-override CS0649 warnings only |
| Game model/media integrity | Passed | 180-second deterministic model checks; 28 records, 56 hashes, 23 comparison sets and 18 activity mappings |
| Preview numeric factor | Passed | 20 log10(0.25118864) = -12 dB within 0.001 dB; session slider stays 0–0.25; comparison source files unchanged |
| Isolated muted Play Mode | Passed | 87 native checks: 51 audio variants, five videos through their actual in-frame Play buttons, direct controls, popup order, trim, modal blocking, inline controls, final game comparison and guided dismissal; delivery run completed 2026-11-06 00:59:46 UTC (2026-11-05 local), including synthetic wheel/swipe |
| Initial test-harness run | Failed, corrected | Pause/resume test entered Begin before marking the tutorial complete; corrected to test the actual post-tutorial state. Subsequent complete run passed; no app failure inferred from that harness error |
| Authentic render capture | Passed with limits | 25 PNGs at 3840×2160 or 2160×3840, including final game/guided popup in both orientations. Representative results and guided alignment visually reviewed; refresh removes panel background restored by resize |
| Skill and documentation checks | Passed | Structural skill validator; changed-document relative links and new metadata GUID checks |
| Physical listening and real touch/device usability | Not run | Native checks are muted/synthetic; real pitch comfort, swipe feel, diagonal gestures and video speech require human/device review |
| GitHub documentation publication | Pending final verification at report authoring | Inspect default-branch head; publish authorized Markdown only with expected-head update and verify contents. Final delivery provides verified commit link |

## Performance

No profiler benchmark or speedup claim. Page gesture discovery runs at gesture start/wheel input, not Update. Five video frames share one decoder and one render target. The game result panel is built once and reused. WAV loading remains buffered to preserve the earlier native crash fix.

## Limitations and follow-up

Review physical headphones and real touch input. Page backgrounds now accept gestures but fixed headers/navigation intentionally remain in place. Black frames load on explicit Play; no thumbnails or autoplay are claimed. The app remains mixed English/Spanish. No score export, clinical interpretation, causal game validation or automatic demographic saving is introduced.

## Rollback

Reverse the preview trim/startup condition, demographic startup/overlay gesture, guided alignment, game final panel, inline video UI and page gesture installer together if needed. Remove new gesture metadata only with its owned scripts; preserve existing GUIDs, buffered media lifecycle and all unrelated user work. Revert AppArtwork transparent panel rule to restore the earlier white panel if desired. Do not delete authored media, private catalogs or consented profiles. Retain this report/history as traceability; connector documentation publication does not synchronize local Git history.
