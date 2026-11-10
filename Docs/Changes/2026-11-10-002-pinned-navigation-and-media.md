# Modification report — pinned navigation and simplified media

- Report ID: 2026-11-10-002
- Date: 2026-11-10 (America/Mexico_City)
- Type: feature / fix / documentation

## Request and resulting behavior

Keep branded chrome at screen edges, remove footer duplication from Home, strengthen module icons, provide touch return from native full-screen video, keep the first tinnitus video only and simplify hearing-example playback. Implemented in source and tested in Unity and on AX85; the delivery APK is built, verified and installed in place. This report records Codex-assisted code and documentation, with checks below rather than treating AI output as validation.

## Modifications

| Main change | Script, document or asset modified | Purpose / effect |
| --- | --- | --- |
| Pin branded chrome | Assets/_HearingNotion/Scripts/Navigation/DockedScreenChrome.cs; Assets/_HearingNotion/Scripts/Navigation/DockedScreenChrome.cs.meta; Assets/_HearingNotion/Scripts/Navigation/ScreenChrome.cs | Cache references and compensate page travel after layout; keep header/footer at viewport edges, preserve lookup hierarchy and modal layering; resolve profile on demand if absent during initial creation. |
| Pack seven cards and strengthen icons | Assets/_HearingNotion/Scripts/Navigation/HomeMenuStyle.cs; Assets/_HearingNotion/Scripts/Navigation/HomeIconGraphic.cs | Hide Research/About you cards while retaining footer routes; use 84-unit icons with 1.5-times stroke weight; retain original stable card identities. |
| Reduce page tail | Assets/_HearingNotion/Scripts/Navigation/WholePageScroll.cs | Replace the old 500-unit allowance with 250, measure Home overflow from Takeaways, place requested scroll targets below pinned chrome and retain immersive game behavior. |
| Simplify listening and video topics | Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs | Put song list first, hide separate hearing-example transport buttons, suppress only tinnitus-2 presentation and preserve direct version toggles. |
| Native touch return | Assets/_HearingNotion/Plugins/Android/HearingNotionVideo.androidlib/AndroidManifest.xml; Assets/_HearingNotion/Plugins/Android/HearingNotionVideo.androidlib/project.properties; Assets/_HearingNotion/Plugins/Android/HearingNotionVideo.androidlib/src/main/java/org/hearingnotion/player/HearingNotionVideoActivity.java; Assets/_HearingNotion/Plugins.meta; Assets/_HearingNotion/Plugins/Android.meta; Assets/_HearingNotion/Plugins/Android/HearingNotionVideo.androidlib.meta | Non-exported local-file native Activity, platform VideoView/MediaController, visible Return to page and Back exit; paused inline restoration via temporary process memory. |
| Regression adaptation | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Verify seven cards, pinned chrome positions, five footer actions and four displayed video topics; keep decoded-frame, audio, questionnaire and game checks. |
| Portable Android copy | Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Editor/; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Plugins/ | Mirror app-owned changes only; retain portable catalog, bundled media and scene. Build outputs and evidence remain local. |
| Current architecture and feature documentation | AGENTS.md; Docs/FEATURES.md; Docs/HomeRedesign.md; Docs/PageScrolling.md; Docs/MediaPlayback.md; Docs/AndroidDeployment.md; Docs/Test.md | Supersede scrolling-chrome requirement, describe simplified media/native library and record actual verification boundaries. |
| Recurring QA skill and traceability | Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md; Docs/Changes/README.md; Docs/Changes/2026-11-10-002-pinned-navigation-and-media.md | Update the existing repeated UI/media QA workflow rather than adding a duplicate skill; maintain report/index links. |

## Decisions and implications

Single-scene architecture, questionnaires, stable IDs, media bytes, source catalog, consent and participant-data handling remain unchanged. Existing GUIDs are preserved; the new component/library metadata receive new GUIDs. No package upgrade, microphone permission, network permission, telemetry or new participant storage is introduced. The Android library is app-owned source, based on documented [VideoView](https://developer.android.com/reference/android/widget/VideoView), [MediaController](https://developer.android.com/reference/android/widget/MediaController) and [Unity Android library plug-ins](https://docs.unity3d.com/2022.3/Documentation/Manual/AndroidAARPlugins.html). Native playback uses the phone media volume; software gain does not establish ear-level sound pressure. Return pauses inline playback rather than automatically restarting it. The second tinnitus asset remains packaged to preserve catalog provenance and hashes; only its duplicate UI section is removed. Flappy retains its immersive game layout.

Only project-authored Markdown documentation is authorized for GitHub publication. Native code, assets, APKs, private catalogs and local evidence are excluded.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| C# compile, game model and media integrity | passed | Tools/Tests/run_project_checks.ps1: Editor/Windows/Android symbols, Editor tools, game model, 28 catalog records and 56 hashes. Expected Inspector-field warnings remain. |
| English/research/instrument integrity | passed | validate_english_content.py: four English summaries, 21 descriptions, unchanged 22-item Spanish HNAI/five choices and UTF-8 source. |
| Java compilation | passed | Installed JDK javac against Android 36 API; Java 8 bootstrap/deprecated Back API warnings, no errors. |
| First native review | failed | Test still expected five video sections after the requested removal; expectation corrected to four. The later run is separately recorded. |
| Final isolated native review | passed | Separate patched Unity project: 95 PASS checks and COMPLETE at 2026-11-10T07:56:17Z; decoded frames, audio cleanup, pinned positions, HNAI/reset and game included. This full run preceded the final Java source-directory correction and initial song-list scroll adjustment; those receive compilation and targeted phone checks. |
| Render inspection | passed | Genuine tall 720x1640 and 4K portrait top/after-scroll renders show pinned chrome, stronger icons and no duplicate cards; local evidence only. |
| Skill structural validator | failed | Bundled quick_validate.py cannot import yaml (PyYAML unavailable); no global dependency installed. Manual name/description/frontmatter and documentation-link checks passed separately. |
| First Android build/signature/install | passed | APK compiled and installed; v1/v2 signatures and all 57 media hashes verified. |
| First native full-screen test | failed | Manifest Activity was packaged but legacy library src Java was excluded by Unity-generated Gradle configuration; moved app-owned Java to standard src/main/java before rebuilding. |
| Final Android build and package verification | passed | Unity 2022.3.62f2 IL2CPP ARM64/ARMv7, min23/target36; APK 1,444,604,960 bytes, SHA-256 e867b1283786a0b6dc081b60909fbf31205bbca4628d00557e86f762cc6e9a54; v1/v2 signatures, 57 media hashes and native Activity DEX presence passed. Existing two META-INF signature-coverage warnings remain. |
| Final installation | passed | adb install -r returned Success on the authorized AX85; app data preserved. |
| Physical-device footer/video return | passed | AX85: all five footer routes, Research/You after scroll, native nonblack playback, visible Return to page, phone Back and resumed inline video inspected. No demographic data saved/deleted. Delivery APK also verified initial song list and first entry clear the header, with direct controls below and no separate transport buttons. |
| Documentation links and manual skill review | passed | All changed Markdown links resolve; name/description/frontmatter reviewed. Bundled YAML validator failure remains separately disclosed. |
| Documentation publication | passed | Markdown-only expected-head publication and fetched-content verification; final verified commit link supplied in delivery. |

## Performance

Not profiled; no speed or memory improvement claimed. Chrome uses cached references with lightweight position compensation after scrolling; no per-frame hierarchy search or forced Canvas rebuild added.

## Limitations and follow-up

Native Windows regression does not establish Android video Activity behavior, acoustic safety or general usability. Comprehensive orientation, interruptions and device coverage remain separate. Manual review of the updated skill does not replace the unavailable bundled validator.

## Rollback

Reverse the scoped changes above, remove the new DockedScreenChrome component/source/meta and Android library after removing their call sites, and restore earlier Home/media/page behavior. Preserve unrelated work and existing GUIDs; do not regenerate Main. The verified pre-task APK is retained locally as HearingNotion-before-20261110-002.apk in the portable build output and can be reinstalled in place if necessary; this does not require deleting visitor data. No data migration is involved.
