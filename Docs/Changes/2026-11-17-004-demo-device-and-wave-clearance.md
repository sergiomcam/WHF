# Modification report - Demonstration device review and wave clearance

- Report ID: 2026-11-17-004
- Date: 2026-11-17 (America/Mexico_City)
- Type: visual fix / Android build / device QA / documentation

## Request and resulting behavior

Prepare and test the latest Android app for the November 18 demonstration, incorporating the user's additional request to keep animated background waves clear of section frames. Built, verified and installed the latest APK in place on AX85 Android 13. A broad portrait walkthrough completed all six guided stages and main independent module flows. No crash was observed in the reviewed paths. This is targeted device evidence, not a guarantee of every possible use or all-device compatibility.

Wave contours now exclude full-width module-sheet bounds with 36 reference units of vertical clearance. They remain behind controls and retain timing, transparent tips, palette and reduced-motion behavior. Cached references/corner storage avoid hierarchy searches or recurring allocations in that update. Existing full-width rounded surfaces are unchanged.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Keep wave geometry clear of module frames | Assets/_HearingNotion/Scripts/Navigation/AmbientWaveAnimation.cs; Assets/_HearingNotion/Scripts/Navigation/TravelingWaveGraphic.cs | Track module bounds and omit intersecting contour segments. No layout/input/texture changes. |
| Synchronize wave fix and latest references | Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/Navigation/AmbientWaveAnimation.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/Navigation/TravelingWaveGraphic.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Resources/Research/ResearchStages.en.json; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Resources/Research/ResearchStages.es.json | Preserve the separate patched portable project and include current app content. Other app-owned scripts/Editor files were synchronized without intended content changes. |
| Build and retain fallback | Builds/AndroidPatched-2026-11-06/Builds/Android/HearingNotion.apk; Builds/AndroidPatched-2026-11-06/Builds/Android/HearingNotion-before-20261117-004.apk | Updated personal APK and verified previous delivery preserved locally. |
| Record wave architecture rule | AGENTS.md; Docs/Artwork.md | Explain exclusion interval, rendering order and limitations. |
| Update feature/device/module evidence | Docs/FEATURES.md; Docs/AndroidDeployment.md; Docs/Test.md; Docs/ListeningSetup.md; Docs/MediaPlayback.md; Docs/ResearchSources.md; Docs/DhwaniFuture.md | Current F-008/F-019/F-024 behavior and tested paths without erasing historical limits. |
| Refine existing recurring QA skill | Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md | Document observed graphical initialization stalls, headless-build evidence limits, scroll settling and user-audibility checks. |
| Save indexed task report | Docs/Changes/2026-11-17-004-demo-device-and-wave-clearance.md; Docs/Changes/README.md | Trace modifications, build identity, failures, tests and rollback. |

Local evidence: tmp/20261117-004 and LocalEvidence/Android-2026-11-17-004 contain build/check logs, numerical WAV review and authentic device captures. They remain local and are not part of documentation publication. No new marketing render or fabricated interface was generated.

## Decisions and implications

- Desktop Unity 2022.3.12f1 Editor remained open and was not closed or used for a second instance. Android work used the separate Unity 2022.3.62f2 copy. Unity's official [CVE-2025-59489 advisory](https://unity.com/security/sept-2025-01) was rechecked; this is a listed patched version, not a comprehensive security audit.
- IL2CPP ARM64 and ARMv7; minimum API 23, target 36; existing personal debug signing and package identity retained. No store upload, dependency upgrade, scene regeneration or new permission.
- Generated 1 kHz source, -12 dB preview trim, 50 ms playback edge fades, slider range/midpoint and multimedia gains are unchanged from the preceding task. Bibliography is included without introducing new study-result claims.
- No real demographic profile saved/deleted. HNAI test responses were synthetic, temporary and cleared by restart; no scoring/export. App data was preserved through adb install -r. Rotation override was restored to its original free state. Device volume remained user-controlled.
- New task source changes add no asset or GUID. Existing resource/audio/artwork GUIDs preserved.
- Existing QA workflow has recurred across media/UI/device tasks; updated that skill using skill-creator guidance instead of creating a duplicate. No new tool permissions or delegation requirements added. Automatic discovery remains unclaimed.

## Build identity

| Item | Verified value |
| --- | --- |
| APK bytes | 1,449,335,662 |
| APK SHA-256 | 43e5766b2b96a9f0b210fb425ac0c0aaa7874e6c29e2b225f8cdbb7a6424df8e |
| Package | org.hearingnotion.prototype; version/code 1; Release IL2CPP ARM64 on AX85 |
| Signing | v1 and v2 verification passed; two existing META-INF signature-coverage warnings remain |
| Media | All 57 packaged sizes/hashes match catalog; app-owned native video Activity present in DEX |
| Preview | Build report includes bundled bb_25dB_1kHz.wav |
| Prior fallback | HearingNotion-before-20261117-004.apk; SHA-256 7481b598c8f5af15f5528e2de0cc1114a443c60c9b46077ce43cf54d8a3ea458 |
| Installation | adb install -r returned Success |

## Validation

| Check | Result | Evidence or reason |
| --- | --- | --- |
| Runtime/Editor compilation | passed | run_project_checks.ps1: Editor, Windows and Android symbols plus Editor tools; expected CS0649 Inspector warnings. |
| Domain/game/media integrity | passed | Existing model checks include blue/red +/-10, mixed moving/stationary pairs, restart, reproducibility, 180-second reviewed completion fixture, speed ramp and collision. All portable media hashes/sizes passed. |
| Signal-content review | passed | All 51 WAV variants decoded numerically as 16/24/32-bit PCM where applicable, finite nonzero RMS/peak. Minimum RMS 0.0002390801. Initial checker assumed 16-bit and stopped; corrected numerical reader handled existing wider PCM. No media transformed. |
| English/research/instrument invariants | passed | validate_english_content.py preserves study numeric values/IDs/figures, 21 activity descriptions, original Spanish 22-item HNAI and known mojibake checks. |
| Graphical native Editor regression | failed / incomplete | Two task-owned patched batch attempts stalled at ModeService initialization before fresh runner output. Stopped only those processes; prior COMPLETE files not counted. No full native-suite or 4K render pass claimed. |
| Real Android build | passed | -batchmode -nographics -buildTarget Android; BuildApk completed, exit 0; actual signed APK inspected. Headless build does not establish rendered UI behavior. |
| Startup / preview | passed with listening limits | About you precedes preview; Skip/Save visible. Midpoint/range present. Slider moved and displayed 27%/50%. First replay not heard; controlled later replay explicitly confirmed audible by user. No calibrated SPL/HL or equal-perceived-loudness claim. |
| HNAI / guided journey | passed | Phone: unanswered Next blocked; revise/advance; 22/22 completion; original labels left aligned; six numbered introductions; questionnaire to Explorer to hearing examples to Health to informational meter to Research to Home. |
| Explorer | passed for targeted paths | Three category filters; context/prevention before comparison; Original/Protection toggles; Airport protection playing state; phone Back during audio without crash; Carpentry selection and navigation. Did not audition every soundscape on device. |
| Hearing examples | passed for targeted paths | Song list above player; first song Original/95/100 variant transitions shown; user confirmed music audible; no separate rewind/play-pause controls. All five songs numerically checked; not all fifteen variants physically auditioned. |
| Videos | passed for targeted paths | Four actual native topic frames; first inline moving frames/pause/Stop; native pause and seek 00:30 to 00:09; Return; Back can first hide controls. Initial stale-scroll taps were not counted; repeated after layout settled. Audio not separately reconfirmed for every video. |
| Research | passed | All four selector rows stayed positioned; no observed text overlap. New references and original YANS figures visible, Finish returned Home. |
| Independent modules/footer | passed | Noise basics, Takeaways, Sound Hub; Research footer from cloned Sound Hub; You startup sequence; Home routes. |
| Future-work presentation | passed | Three hub branches, all four Dwani pages, inert Record control, Continue and phone Back. No analysis/recording functionality claimed. |
| Flappy Cloud | passed for targeted paths | Tutorial; in-arena Pause/Resume; quiet Retry; Continue; Ready remained waiting; random Rock concert buffered load; noisy pause/resume; final two-round feedback; final Retry restarts tutorial. Device runs were brief; three-minute completion and +/-10 logic tested by model fixture, not human play. |
| Session restart | passed | Cold restart showed About you first, then HNAI Item 1 with 0 of 22 answered. |
| Wave clearance / portrait layout | passed | Actual AX85 module captures show contours outside sheets with rounded edges clear; no input interception observed. |
| Landscape | not verified | Temporary rotation override did not produce a landscape capture; restored original free rotation. Do not count portrait output as landscape evidence. |
| Diagnostics | passed with scope | Checked current app-PID Unity/AndroidRuntime log: no exception/fatal line. Android exit history for this review showed intentional install/force-stop reasons; no observed crash. Logs are not proof of absence of every defect. |
| Skill structural validation | passed | Bundled quick_validate.py with existing local PyYAML dependency: Skill is valid. Applied workflow evidence is the current build/device review; no independent subagent evaluation. |
| Offline disconnection | passed for targeted paths | User confirmed disconnected networks; Android reported Active default network: none before/after. Fresh launch, About you/preview Skip flow, Airport original Playing state, native Health video with actual decoded frames and return to Home passed. Existing app-private video cache retained; first-ever cache extraction was not retested. |
| Persistent profile Save/delete | not run | Per guidance, never test these against a real phone profile; redirected synthetic native suite was not completed today. Historical tests remain separate. |

## Performance

Not profiled; no FPS, CPU/GPU improvement or memory-budget claim. Functional device checks and numerical media scans are not stress testing.

## Limitations and demonstration use

Use the tested portrait flow. Core module paths passed, but the complete native suite, physical landscape and long human gameplay remain unverified. Current questionnaire is Spanish; videos retain original language. Noise Meter, language validation, Dwani analysis and Music Lab remain informational/future work. HNAI responses have no clinical score; game differences are descriptive, not evidence of a causal noise effect.

For the demonstration: launch the installed app, Skip or intentionally Save optional demographics, use low comfortable device volume/headphones and the optional preview, then choose guided mode or independent modules. Full-screen videos have native controls and Return; after closing native playback allow the page to settle before scrolling. Restart the app between visitors to clear temporary answers. No real saved profile is erased by restart. The previous verified APK remains a local fallback; public distribution/media rights are outside this personal demonstration build.

## Rollback

Revert only the two wave source changes and corresponding portable copies to remove exclusion; restore the prior module/skill documentation paragraphs as needed. Preserve generated preview, existing assets/GUIDs, new citations and unrelated work. If necessary, install the verified prior fallback APK in place using the same package/signing; it predates the new preview/references/wave clearance. Do not uninstall, clear storage, force-push or regenerate Main. No participant-data migration.
