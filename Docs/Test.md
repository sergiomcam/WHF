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
| First launch | Optional form appears once per installation/notice version; Skip, temporary continuation and explicit local save are distinct; About you reopens it |
| Demographics | Use synthetic values only; blank age accepted; invalid/out-of-range age rejected; Save explains local storage; Delete removes the local profile; no networking or device identifier collection |
| HNAI | Original Spanish wording, revise answers, completion guard, scrolling and visitor reset |
| Explorer | All 18 linked recordings, three chart-only missing-example states, optional import controls |
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
| QA-004 | First quiet game over | Automatically advancing prevented retry choice | Flow | Native game/controller run and game-over render | FlappyCloudController.cs | Try again and Continue verified; second round remains silent |

For new findings, record the minimal reproduction, actual observation, cause if supported, correction and retest result. Use open, fixed-awaiting-retest, verified-fixed or blocked; do not silently convert unresolved items into successes.
