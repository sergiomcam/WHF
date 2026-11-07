# Hearing Notion — computer testing and bug correction

Version 1.0 · 2026-11-05. This is an on-demand procedure, not a scheduled watcher or guarantee of automatic correction. The user authorizes local prototype interaction, synthetic-data testing and reversible scoped fixes. Existing tool permissions still apply. Use [the QA skill](Skills/unity-prototype-review/SKILL.md) for repeat runs and [ETHICS.md](ETHICS.md) for data boundaries.

## Run sequence

| Step | Action | Required evidence / stop condition |
| --- | --- | --- |
| Inspect | Confirm Main scene, Unity version, unsaved work, local media and affected behavior | Do not overwrite scenes or close the user's Editor; never start another Editor against the same open project |
| Static/model checks | Run Tools/Tests/run_project_checks.ps1 from the project root, supplying UnityRoot/Python if needed | Record compiler/model/hash failures; passing compilation does not establish playback or UI quality |
| Existing-Editor regression | Create tmp/prototype-review.request containing exactly run, while Main is open | PrototypeReviewRunner consumes it, enters Play Mode if needed, mutes playback, skips demographics without saving, traverses screens, tests catalog audio/video and first-round buttons; allow up to 10 minutes |
| Read outcome | Inspect LocalEvidence/prototype-review.txt and Unity Console | Request creation is not completion. Report timeout, missing output, native crash or every FAIL/UNITY error; investigate before rerunning |
| Visual inspection | Review Marketing/Screenshots and both portrait/landscape in the actual Game view | Direct Unity camera/Canvas renders are captured at 3840×2160 and 2160×3840; check text clipping, navigation, overlays, scrolling, video aspect and missing components; captures are genuine rendered screens, not mockups |
| Scoped correction | Reproduce, identify cause, make a reversible fix and rerun affected checks | After repeated equivalent failure, stop that attempt and report the blocker. No blind upgrades, deleting user data or bypassing permissions |
| Document | Add a modification report, feature history and bug/result rows | Publish only authorized Markdown; exclude raw logs, private paths, responses, media and screenshots |

The regression runner leaves an interactive Editor in Play Mode at Home and restores audio volume after its muted test; an isolated batch run exits after completion. It creates, verifies and deletes only synthetic demographic data in a redirected scratch folder, never the real profile. It does not save scenes. Interruption before completion can require manually restoring the Unity audio listener volume. Do not run it during a real visitor session. For an isolated copy, run Unity with -batchmode -executeMethod HearingNotion.Editor.PrototypeReviewRunner.RunIsolated, using that copy's projectPath. Copy only app-owned and required TMP assets, preserving GUIDs and the private catalog; do not copy the full vendor library or media originals.

## Functional matrix

| Area | Checks |
| --- | --- |
| First launch | Optional form appears first on every launch, before listening volume; Skip, temporary continuation and explicit local save are distinct; About you reopens it |
| Demographics | Use synthetic values only; blank age accepted; invalid/out-of-range age rejected; Save explains local storage; Delete removes the local profile; no networking or device identifier collection |
| HNAI | Original Spanish wording, revise answers, completion guard, scrolling and visitor reset |
| Explorer | All 18 linked recordings, three chart-only missing-example states, no add/import/reset controls; direct version toggles |
| Audio | Original/protected and original/WHIS choices, Play/Pause/Stop, version switching, Back while loading/playing, re-entry and reset; buffered clips, no native crash |
| Video | Prepare, moving image, audio-route state, Pause/Stop/Back, original vs compatibility cache, error/30-second timeout feedback |
| Flappy Cloud | Tutorial, tap/Space, scoring, Pause/Resume, first game over waits indefinitely; Try again repeats quiet round; Continue begins notice then second round; final Retry only at session end |
| Presentation | Home/module navigation, no disappearing Back/Home controls, portrait/landscape, reduced-motion control, placeholder limitations visible |

Muted engine tests do not establish audible output, loudness consistency, codec performance on other computers or safe acoustic levels. For listening checks, begin at a comfortable low device level; never increase until discomfort. An unavailable codec is a reported limitation, not a passed test. Local video compatibility copies preserve originals and are not included in documentation publication.

## Bug/result record

| Bug ID | Screen / trigger | Expected / observed | Severity | Evidence | Modified scripts/documents | Verification / status |
| --- | --- | --- | --- | --- | --- | --- |
| QA-001 | Media library | Two original MP4s failed Unity file reads; initial compatible encodings also raised timestamp warnings | Playback | Local native logs and FFmpeg inspection | MediaExperienceController.cs; prepare_video_compatibility.py | Verified fixed in muted isolated run: 51 audio variants and all five baseline/timestamp-normalized videos playing; audible output still needs human review |
| QA-002 | Home footer and About you | Profile entry overlapped motion control | Layout | Actual 4K render | DemographicPromptController.cs; ResponsiveScreenLayout.cs | Fixed and visually reviewed as a standard eighth card |
| QA-003 | Home copy | Corrupted punctuation in duration and placeholder descriptions | Content | Actual portrait render | ResponsiveScreenLayout.cs | Corrected to plain punctuation and accurate prototype labels |
| QA-004 | First quiet game over | Automatically advancing prevented retry choice | Flow | Native game/controller run and game-over render | FlappyCloudController.cs | Try again and Continue verified; superseded by random soundscape round in corrections report |

For new findings, record the minimal reproduction, actual observation, cause if supported, correction and retest result. Use open, fixed-awaiting-retest, verified-fixed or blocked; do not silently convert unresolved items into successes.

## Corrections regression, 2026-11-05

PrototypeReviewRunner now exercises all 18 direct Original-toggle paths, first-round buttons inside the playfield, random round-2 audio/pause/navigation cleanup, 6 kHz preview loading, live session-gain update and Accept stopping playback. It checks modal background blocking/restoration and captures demographics, listening setup and Noise basics in both orientations. Run an isolated project copy when Main is already open; do not start a second Editor on the same locked directory. Muted playback proves engine state only. Manually review slider dragging, keyboard focus, scrolling, comfortable output, Skip, missing-file feedback and target device behavior. See [task report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

2026-11-05 regression additions: verify About you before listening setup even with a prior dismissal, -12 dB preview-only amplitude factor, centered Entendido and dismissal, five inline video controls, page-background scroll forwarding, and final round comparison/next steps. Capture final game results and guided popup in both orientations. Confirm the fresh completion timestamp; never reuse an older result file as new evidence. Human touch gestures and physical listening remain separate. See [report](Changes/2026-11-05-003-results-video-and-swipe.md).

2026-11-05 stronger regression: assert one Home sound entry and both hub choices; midpoint slider in unchanged range; controls below every video frame; white video tint, advancing decoded frames and nonblack RenderTexture pixels; whole-page wheel/drag that moves Heading, Back and the bottom note together. Do not equate isPlaying with a visible or audible result. Preserve actual playing-frame captures and distinguish physical listening/touch review. See [report](Changes/2026-11-05-004-unified-sounds-and-whole-pages.md).

2026-11-06 checks: compile with Editor, Windows and Android symbols, explicitly distinguishing this from IL2CPP/APK compilation. Use validate_packaged_media.py --project-root <portable-project> for all bundled hashes and preview. Verify stopped Home with StoppedHomePreview.CaptureIsolated, seven informational DHWANI entries, a representative 720×1640 viewport and native playback of the blank-ExternalRoot portable project. Test absent/empty preview entries and native video paths containing spaces. Inspect AndroidPrototypeBuild.Readiness for real toolchain support; do not report an APK or phone installation without one. See [deployment](AndroidDeployment.md) and [report](Changes/2026-11-06-001-editor-dhwani-android.md).

Patched-Editor migration: the separate AndroidPatched-2026-11-06 copy passed all 91 native Editor regression checks under Unity 2022.3.62f2, including 51 audio variants and five decoded nonblack videos. Main's SHA-256 remained identical to the working project. This is Windows Editor evidence, not an Android device result. For a real APK build, start that copy with -buildTarget Android before executing AndroidPrototypeBuild.BuildApk; wait for the final BuildResult and process exit, then inspect the APK's manifest, ABI entries and signature. Check the intended phone with adb without publishing device serials or raw logs. Do not install while its status is unauthorized. See [current deployment record](AndroidDeployment.md) and [follow-up report](Changes/2026-11-06-002-patched-android-build.md).

2026-11-06 approved-design regression: verify the rounded Home, five yellow/two turquoise/two purple icon accents including Waves, disabled/deferred meter, nonblocking geometry, English labels and lower controls reachable by full-page scrolling. Capture top and lower-page Home separately; after a reset return to Home explicitly before capture. Capture settling must complete CanvasScaler logical-size changes and pending page reflow before asserting scrolling. HNAI tests now exercise answer revision, all 22 responses, completion invalidation/recompletion and actual visitor reset while retaining the original Spanish items/choices. validate_english_content.py compares research numeric values/IDs/figures, 21 English descriptions and HNAI scale/domain invariants. See [report](Changes/2026-11-06-006-rounded-english-interface.md).

2026-11-06 shared styling: Shared-window checks now verify absence of Waves, the new 4 yellow/2 turquoise/2 purple module palette, matching Home fonts in module headings and all three popup families, nonblocking rounded surfaces and rounded TMP input target graphics. Retain HNAI revision/reset, synthetic consent save/delete, media lifecycle and game checks; inspect actual modal/page renders in both orientations. See [report](Changes/2026-11-06-007-shared-window-style.md).

Text-encoding regression: validate_english_content.py now rejects known mojibake markers in app-owned runtime/Editor C# sources. Use explicit UTF-8 when editing and visually check labels/durations/separators in native renders. A passing compiler does not establish correct text encoding. See [report](Changes/2026-11-06-007-shared-window-style.md).
