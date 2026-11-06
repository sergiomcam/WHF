# Modification report — stopped Home, DHWANI and Android preparation

- Report ID: 2026-11-06-001
- Date: 2026-11-06 (America/Mexico_City)
- Type: feature / fix / content / tools / documentation

## Request and resulting behavior

Show complete Home while the app is stopped, add an informational DHWANI future-work section from the supplied overview, and prepare for a personal Android installation with clear next steps. The stopped Editor preview and DHWANI information page are implemented and rendered. A separate self-contained Android project is prepared and configured; APK/device delivery remains blocked by missing Android Build Support and requires engine-security remediation before deployment. No APK or phone installation is claimed.

## Modifications

| Main change | Script, document or asset modified | Purpose / effect |
| --- | --- | --- |
| Complete stopped Home | Assets/_HearingNotion/Editor/StoppedHomePreview.cs | Transient EditorOnly Canvas with current cards/artwork; no managers or playback outside Play; removed before Play and not saved into Main |
| DHWANI information | Assets/_HearingNotion/Scripts/Content/DhwaniFutureController.cs; Assets/_HearingNotion/Resources/DhwaniFuture.json | Seven attributed sections; no recording, upload, prediction, model/API or ownership/validation claim |
| Startup, route and Home ordering | Assets/_HearingNotion/Scripts/Core/AppManager.cs; Assets/_HearingNotion/Scripts/Data/AppSession.cs; Assets/_HearingNotion/Scripts/Navigation/ResponsiveScreenLayout.cs | Explicit controller installation, appended DhwaniFuture enum and ninth Home card; guided order unchanged |
| Portable media resolver | Assets/_HearingNotion/Scripts/Audio/MediaAssetPath.cs | Separate external local paths and StreamingAssets/jar download URLs |
| Android video and native-path repair | Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs | Optional preview record, on-demand APK video extraction to private cache, native VideoPlayer paths, cancellation/storage error handling; buffered WAV behavior preserved |
| Preview/game portability | Assets/_HearingNotion/Scripts/Core/ListeningSetupController.cs; Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs | Use packaged preview and soundscapes, retain guarded legacy desktop fallback; gains and scientific processing unchanged |
| Android build/configuration guard | Assets/_HearingNotion/Editor/AndroidPrototypeBuild.cs | Personal APK configuration, missing-module check, portable-input build preprocessor and readiness evidence; no store release |
| New metadata | Assets/_HearingNotion/Editor/StoppedHomePreview.cs.meta; Assets/_HearingNotion/Editor/AndroidPrototypeBuild.cs.meta; Assets/_HearingNotion/Scripts/Audio/MediaAssetPath.cs.meta; Assets/_HearingNotion/Scripts/Content/DhwaniFutureController.cs.meta; Assets/_HearingNotion/Resources/DhwaniFuture.json.meta | Unique new GUIDs; pre-existing GUIDs preserved |
| Portable project preparation | Tools/Android/prepare_android_project.py | New-folder-only export, app-owned/TMP copy, 57 verified media files, empty external paths, receipt and local setup README; never overwrites desktop catalog or an existing export |
| Prepared local project | Builds/AndroidPrototype-2026-11-06/Assets/; Builds/AndroidPrototype-2026-11-06/Packages/; Builds/AndroidPrototype-2026-11-06/ProjectSettings/; Builds/AndroidPrototype-2026-11-06/PORTABLE-PROJECT.json; Builds/AndroidPrototype-2026-11-06/README-ANDROID.md | Self-contained snapshot with bundled media and Android identity/IL2CPP/ARM targets; no private visitor profiles copied |
| Expanded tests | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs; Tools/Tests/run_project_checks.ps1; Tools/Tests/validate_packaged_media.py | DHWANI limits, tall phone viewport, Android-symbol compile and portable-project/preview hash validation |
| Local evidence and captures | LocalEvidence/2026-11-06-001-desktop.txt; LocalEvidence/2026-11-06-001-portable.txt; LocalEvidence/2026-11-06-001-stopped-home.txt; LocalEvidence/2026-11-06-001-android-toolchain.txt; LocalEvidence/nov06-desktop-final.log; LocalEvidence/nov06-portable-final.log; LocalEvidence/nov06-stopped-final.log; LocalEvidence/nov06-android-readiness.log; Marketing/Screenshots/*.png | Separate actual runtime/stopped/toolchain evidence; 37 local renders, including 720×1640 representative phone viewport; no APK/phone screenshot implied |
| Module/deployment guides | Docs/EditorHomePreview.md; Docs/DhwaniFuture.md; Docs/AndroidDeployment.md; Docs/AppArchitecture.md; Docs/HomeScene.md; Docs/MediaPlayback.md; Docs/ListeningSetup.md; Docs/Test.md; Docs/Marketing.md; Docs/README.md | Explain implemented scope, source attribution, portable lifecycle, actual blockers and installation steps |
| Recurring workflow skills | Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills/unity-information-page/SKILL.md; Docs/Skills.md | Extend existing QA; add focused information-page workflow after repeated Noise basics/DHWANI pattern; explicit invocation, no global installation/discovery claim |
| Feature/instruction/history traceability | AGENTS.md; Docs/FEATURES.md; Docs/Changes/README.md; Docs/Changes/2026-11-06-001-editor-dhwani-android.md | Add F-022/023/024, update affected entries and preserve required modification/history tables |

## Decisions and implications

The preview is Editor-only and labelled; it does not turn runtime managers into ExecuteAlways components or save generated UI into the scene. Main.unity hashes match the working, isolated test and portable copies. No destructive scene generator was run. Existing dependency versions and desktop Player Settings/catalog remain unchanged. The portable copy alone has org.hearingnotion.prototype, Hearing Notion, IL2CPP ARM64+ARMv7, minimum API 23, auto target SDK and personal debug-signing APK configuration. The export is a snapshot, not an automatic synchronization mechanism.

The user supplied DHWANI_Intro.docx, despite referring to it as a PDF. It describes Dr Manish Manohare/IIT Delhi’s platform, computed psychoacoustics and model-based response estimates. The new page paraphrases and attributes these descriptions without claiming independent validation, partnership or rights to proprietary software. No raw Word document, figures or models are copied. Algorithms/standard versions, calibration, licences, validation conditions and privacy/consent design remain required for any future implementation.

The export contains 57 hash-checked files totaling 1,413,452,794 bytes. The largest WAV is about 53.2 MB; video cache payload is about 183.2 MB. Existing H.264/AAC copies are used; comparison WAVs, shared gains and preview trim remain unchanged. Optional TinnitusPreview is backwards-compatible; Unity JSON can produce an empty object for an absent entry, so both null and empty paths are checked. Native VideoPlayer receives a filesystem path, avoiding the escaped-space failure found in portable testing. Android jar audio/download paths and on-demand file extraction are implemented but remain unverified on a real Android player. The app-private video cache is authored content, not participant data; no visitor profiles/responses were exported.

No APK is produced. The native preflight reports Android Build Support unavailable. Separately, [Unity’s advisory](https://unity.com/security/sept-2025-01) identifies engine remediation needed for the pinned baseline before deployment. No patched-editor migration or binary remediation was performed. The working project was not silently upgraded; the deployment guide directs remediation/testing in the separate copy. See [Android steps and official references](../AndroidDeployment.md).

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| C# and Editor tool compilation | Passed | run_project_checks.ps1: Editor, Windows and Android symbols; expected Inspector/test-override CS0649 warnings only. This is not an IL2CPP/APK compile |
| Game model and desktop media integrity | Passed | 180-second model/scoring/reset checks; 28 records, 56 hashes, 23 aligned sets and 18 mappings |
| Portable bytes and catalog | Passed | 57 file hashes/sizes, preview and safe paths verified; ExternalRoot/PlaybackPath empty; no Windows user paths found in exported runtime JSON/assets/scene |
| External desktop native regression | Passed | 91 checks completed 2026-11-06 22:16:47 UTC; informational page, preview, audio/video, modal, game, navigation and scrolling |
| Portable desktop-engine regression | Passed | 91 checks completed 2026-11-06 22:22:50 UTC; all 51 audio variants and five decoded nonblack videos using bundled files. Does not prove Android jar/device playback |
| Stopped Home | Passed | Clean isolated stopped capture in both orientations; no Play Mode or scene save; labelled preview inspected |
| Legacy preview and spaced video-path failures | Failed initially; corrected and retested | Guarded the empty optional preview object; separated native video paths from escaped URLs. Subsequent desktop/portable native runs passed |
| Rendering | Passed with limits | 37 actual PNGs; standard landscape/portrait plus 720×1640 representative profile. Preview and DHWANI/tall layouts inspected; not actual phone screenshots |
| Android configuration/preflight | Passed as a diagnostic; build blocked | 57 portable inputs validated; actual BuildTarget support false; prepared settings verified. No APK exists |
| Engine deployment review | Blocker identified | Official advisory requires remediation of the pinned baseline; patched-editor migration/build not run |
| Skills, JSON, GUIDs and documentation | Passed | Structural validators; seven sourced DHWANI sections, appended enum, new GUID/link/catalog checks; no auto-discovery claim |
| APK build, install and Acer AX85 testing | Not run | Android toolchain absent; engine remediation pending; no connected-device/ABI, physical listening, touch, safe-area or performance verification |
| Documentation publication | Pending final verification at report authoring | Publish authorized Markdown only with expected-head protection; final delivery supplies verified commit link |

## Performance

No FPS/memory speedup or hardware budget claimed. Media remains on demand with buffered WAVs and one video decoder/render target. On Android, video copies go to disk using DownloadHandlerFile rather than holding complete video bytes in managed memory. Stopped preview work is Editor-only. APK compression, installed size and physical memory/performance remain unmeasured.

## Limitations and next steps

Install a Unity release marked remediated in the official advisory with matching Android modules, open/upgrade only the portable copy and rerun checks, then use Build And Run on the user-reported Acer AX85/Android 13. Google’s supported-device listing confirms the model name, not this device’s ABI or configuration. The guide includes USB debugging/authorization, an optional adb path, offline testing and storage/signing limits. Use on-screen navigation; comprehensive Android system-Back behavior remains unverified. DHWANI is informational only. The core app remains a mixed-language research-awareness prototype, not a medical or calibrated measurement product.

## Rollback

Remove the new Editor preview helper and paired metadata to restore stopped-mode behavior. Remove the DHWANI controller/data/startup/menu addition together while preserving historical enum identity rather than renumbering existing routes. Restore prior external path handling only deliberately, preserving buffered WAV loading and gain assumptions. The working desktop catalog/settings were not replaced. The generated portable project can be retained independently; do not delete or overwrite a copy containing later user changes or real data. No APK/store deployment or global SDK/editor installation occurred. Preserve this report and source provenance.
