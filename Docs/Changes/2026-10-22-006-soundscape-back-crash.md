# Modification report — soundscape Back navigation native crash

- Report ID: 2026-10-22-006
- Date: 2026-10-22 (America/Mexico_City)
- Type: fix

## Request and resulting behavior

The user reported Unity quits when pressing Back from soundscape examples and asked whether disappearing buttons were responsible. The pre-existing crash log ends with purecall, AudioClip::WWWRead and FMOD asynchronous file reads. This matches [Unity issue UUM-14330](https://issuetracker.unity.com/issues/15958/crash-on-purecall-when-an-audio-source-is-trying-to-play-a-destroyed-clip): destroying streamed clips can crash the audio thread. The app requested streamAudio=true and destroyed that clip when leaving a screen.

Local WAV requests now explicitly use streamAudio=false and compressed=false. Playback begins only after the complete request, so the native streaming read path is avoided. Only one selected clip is decoded; stop/detach/release remains on navigation. This is a targeted mitigation supported by the crash signature, not a claim of completed runtime verification.

## Modifications

| File or asset | Change and purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs | Fully decode local WAVs, guard destroyed UI references during cleanup, unsubscribe video callbacks on destruction |
| Assets/_HearingNotion/Editor/MediaNavigationSmoke.cs and metadata | Explicit batch-only muted regression harness: 18 real Main-scene loads, Back release, immediate cancellation and session reset |
| AGENTS.md, Docs/MediaPlayback.md, Docs/FEATURES.md, Docs/Changes/README.md | Preserve non-streaming convention, loading tradeoff, verification limits and modification history |

## Decisions and implications

No Unity upgrade, source-media transformation/copy, scene/navigation-route or research-content change. Back/Home/Continue are retained on their screen roots; the media controller destroys owned clips/textures, not buttons. Variant buttons are intentionally hidden on exit and enabled when a compatible example is selected. Cleanup now tolerates already-destroyed UI objects. No visitor data or external paths are published.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| User crash log diagnosis | Passed | Existing log shows purecall → AudioClip::WWWRead → FMOD async file thread, matching the official issue |
| Editor and Windows runtime compilation | Passed | Unity 2022.3.12f1; existing Inspector-field warnings only |
| Editor regression harness compilation | Passed | Installed Unity Editor/engine/TMP/uGUI references |
| Batch native regression | Not run to completion | Unity refused because the project is open in another instance; the extra batch attempt terminated in HandleProjectAlreadyOpenInAnotherInstance before running tests. The user's existing instance was not closed |
| Button lifecycle source review | Passed | Navigation toggles registered roots; no media button-destruction call exists. Variant visibility is explicit |
| Interactive Play Mode, physical playback, crash-resolution confirmation | Not run | Existing open project prevents separate batch test; user-session checks remain required |

## Performance

Not benchmarked. Fully decoded audio trades additional selected-clip memory and load time for avoiding the native streamed lifetime path. One clip is retained at a time; full-library preloading is not introduced. Decoder/request overhead can coexist with the clip while loading. No frame-time or memory-usage improvement is claimed.

## Limitations and follow-up

Restart Play Mode after compilation. Verify Back during original/protected playback, immediately during loading, after pause/end, rapid variant changes and reset. Confirm Back/Home and variant controls reappear on re-entry. Videos and physical output still need separate verification. The explicit batch harness can run with Unity closed using -batchmode -projectPath followed by -executeMethod HearingNotion.Editor.MediaNavigationSmoke.Run; it mutes audio and does not save the scene. Do not run it against a project already open in another Editor.

## Rollback

Revert the task-specific cleanup guards/callback unsubscription and remove the optional Editor test if needed, preserving metadata and other work. Restoring streamAudio=true reintroduces the known crash path and is not a recommended workaround. A later reviewed engine upgrade or a separately validated streaming-lifetime design can revisit memory tradeoffs.
