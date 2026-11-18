# Modification report — Dwani visual contributions and reference gain

- Report ID: 2026-11-17-009
- Date: 2026-11-17 (America/Mexico_City)
- Type: feature / fix / audio presentation / documentation

## Request and resulting behavior

Dwani now offers animated recording feedback and a button-driven soundscape contribution with a points popup. At the owner's request controls say Record audio / Upload soundscape and the reward says +50 points, without demo labels on those controls. This remains a visual-only experience: no microphone, location, audio creation, upload or rewards backend. Existing MOCKUP ONLY page badges remain.

The startup 1 kHz reference is increased by 6 dB through its preview-only trim, from -12 to -6 dB. Slider range, midpoint, headroom preparation, 50 ms fades and all other media gains/source files remain unchanged.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Recording/upload/reward presentation | Assets/_HearingNotion/Scripts/Content/DhwaniMockupController.cs | Record toggle, six-second timer/pulse, on-demand map progress, temporary +50 popup, page input blocking and Back/exit/reset cleanup |
| Animated microphone geometry | Assets/_HearingNotion/Scripts/Content/DhwaniMockupGraphic.cs | Reusable nonblocking microphone-only mode over the unchanged reference artwork; color animation uses existing turquoise/yellow palette |
| Reference level | Assets/_HearingNotion/Scripts/Core/ListeningSetupController.cs | PreviewTrim 0.25118864 to 0.50118723; +6 dB, no source WAV edit or other gain change |
| Regression expectations | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Allow requested visual buttons, verify recording toggle, preserve inert artwork test, assert -6 dB preview trim |
| Portable source synchronization | Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/Content/DhwaniMockupController.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/Content/DhwaniMockupGraphic.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/Core/ListeningSetupController.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Matching app-owned implementation while preserving portable media paths and metadata |
| Personal Android build/fallback | Builds/AndroidPatched-2026-11-06/Builds/Android/HearingNotion.apk; Builds/AndroidPatched-2026-11-06/Builds/Android/HearingNotion-before-20261117-006.apk | Final updated APK and verified preceding build retained for rollback |
| Current behavior and conventions | AGENTS.md; Docs/DhwaniFuture.md; Docs/ListeningSetup.md; Docs/FEATURES.md; Docs/AndroidDeployment.md; Docs/Test.md | F-025/F-026/F-019/F-024 changes, non-acquisition scope and reference-gain distinction |
| Reusable workflow | Docs/Skills/unity-information-page/SKILL.md; Docs/Skills.md | Existing recurring future-work preview skill extended for explicitly requested visual-only controls; no new skill or automatic discovery claim |
| Change traceability | Docs/Changes/2026-11-17-009-dwani-record-upload-rewards.md; Docs/Changes/README.md | Dated report, continuous history and authorized Markdown publication |

## Decisions and implications

Recording animates the microphone at one smooth turquoise/yellow cycle per second, updating its timer once per second and ending after six seconds or a second tap. It does not open a microphone or create a recording. Leaving the page stops its coroutine and restores the idle icon on reentry.

Upload now requires a tap, disables during the existing 1.2-second progress animation, adds the fictional pin, then opens a rounded points popup. Repeated upload reopens the same fixed amount rather than incrementing a balance. Popup Continue dismisses it; hardware Back dismisses it before leaving Dwani. Underlying page controls are blocked while it is visible. Leaving/reentry/reset clears cosmetic state; points have no persistence, account or redemption. No file picker, GPS, network, cloud, permission request or sharing exists. The 50-point amount and animation duration are interface choices, not research measurements. Source artwork and example analysis values remain unchanged.

Preview-only gain is now 10^(-6/20), approximately 0.50118723, versus 0.25118864 before. The ratio is approximately 1.99526 (+6 dB). With prepared 0.25 clip peak and 0.25 slider maximum, the nominal digital peak is approximately 0.0313242 before device/output processing. This is not acoustic calibration or an ear-level dB guarantee. Playback still requires explicit Play and may be skipped.

No new dependencies, scene regeneration, enum/schema changes, asset additions/deletions, GUID changes or participant-data paths. Main/open desktop Editor preserved. APK builds remain debug-signed personal exports using the same app ID and existing headphones launcher icon. Documentation publication excludes code, APK, private paths, logs and screenshots.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| Source/model/media checks | Passed | run_project_checks.ps1: Editor/Windows/Android-symbol compilation, Editor tools, Flappy model and media integrity; checks-final.log |
| English/instrument integrity | Passed | validate_english_content.py; original Spanish HNAI, numeric values and source media preserved |
| Preview gain arithmetic | Passed | -6 dB absolute and +6 dB change within 0.00001 dB; no source sample edits |
| Skill structure | Passed | Existing unity-information-page skill validated with bundled structural validator and existing local PyYAML; behavioral evidence recorded separately |
| Final Android build/signature/media | Passed | Unity 2022.3.62f2 IL2CPP ARM64/ARMv7 build-final.log success and exit 0; v1/v2 signature, 57 unchanged media hashes/sizes and native video DEX; two existing META-INF signature-coverage warnings retained |
| APK identity | Passed | 1,449,613,923 bytes; SHA-256 c60f570bb9a6a8e33c6f001b3aabcd5faa82e1441cc3d3abe718a3ff843c2585 |
| Targeted AX85 interactions | Passed | In-place install Success; microphone turquoise/yellow pulse, six-second auto-stop, manual stop and idle reentry; explicit Upload, added pin, +50 popup, underlying-page blocking, popup Continue, same reward on repeat, hardware Back priority, final overview and canceled-upload cleanup verified with actual captures |
| Device runtime log | Passed | No Exception/FATAL/Error lines in filtered Unity/AndroidRuntime log during targeted checks; returned Home without saving demographic data |
| Complete native Unity suite / 4K renders | Not run | Prior graphical batch initialization blocker retained; compilation/headless build is not full runtime/visual verification |
| Full landscape/all-device/listening review | Not run | Targeted device coverage only; +6 dB arithmetic does not verify perceived loudness or comfortable output |

## Performance

Not profiled; no speedup or memory claim. Animation work is limited to the visible recording state, uses existing geometry, and formats timer text only when seconds change. Owned coroutines are canceled on navigation/disable/reset. No runtime media buffers or network operations added.

## Limitations and follow-up

Visual concept only: no actual recording/upload/location contribution or real reward. Existing mockup scope indicators remain; controls follow the owner's wording. Full native suite, long stress/rotation and acoustic output are unverified. Source reference material is unchanged; no new scientific claims introduced. The increased reference still requires comfortable device volume. Final diagnostics reported headphone output at maximum; no audio was triggered during the visual-only phone checks. Physical listening to the increased preview was not performed.

## Rollback

Reverse only this task's four source files and corresponding portable copies; restore PreviewTrim to 0.25118864 and its fixture assertion to -12 dB if reverting the requested level increase. Preserve original media/artwork and unrelated changes. Install the retained HearingNotion-before-20261117-006.apk with adb install -r to restore the preceding tested phone build without clearing app data; SHA-256 43584804393c9fece98cd7c1aa6d2866efe68552db527701504cb47e2ce23a34. Do not uninstall, clear real profiles or regenerate Main.

Local evidence: LocalEvidence/Android-2026-11-17-009 (actual device screenshots/log) and tmp/20261117-006 (compile/build/hash checks). These files remain local. No full runtime-suite, fresh 4K capture or physical listening claim follows from the targeted checks.
