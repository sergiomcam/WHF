# Offline audio and informative videos

Updated 2026-11-05: local media source hashes remain intact. A local LocalMediaCache provides five verified H.264/AAC playback copies because the native player failed on two original MP4s in addition to HEVC/MOV compatibility concerns. Catalog PlaybackPath selects an existing compatibility copy, otherwise falls back to the original file. Cache files stay outside Unity Assets and GitHub. Regenerate with Tools/Audio/prepare_video_compatibility.py --ffmpeg <local executable> --all, then rerun native checks. Video now has a separate AudioSource; audio requests and video preparation have 30-second timeout feedback. Do not infer a codec/format failure solely from a file hash or successful FFmpeg decoding.

If media is still silent on the working computer, check the Game view's Mute Audio control, that the scene AudioListener is enabled, the selected Windows output device/headphones and whether the app was paused by focus loss. Press Play again after returning focus. A playing AudioSource does not prove audible speaker output. Processed protection/WHIS examples intentionally retain their lower levels relative to the common-gain reference; do not independently normalize or raise playback until discomfort. Re-indexing the original library removes per-file PlaybackPath overrides; rerun compatibility preparation afterwards if needed.

The final 2026-11-05 isolated muted Unity run exercised all 51 audio variants and all five videos, then released playback on Back. All passed without native test errors. Cache encodings use H.264 baseline, no B-frames, 30 fps and normalized track timestamps; the final log had no earlier timestamp warnings. This establishes tested engine playback/state cleanup, not physical output audibility, perceptual equivalence or universal codec compatibility.

Infrastructure first implemented 2026-10-22; current native checks and remaining physical-device limits are recorded below.

## Where to find the material

- **Exposure Explorer:** the 18 annex activities offer “Explorar este sonido”, which selects their packaged original/protected comparison in Sound Experience. Three chart-only activities have no invented matching recording. Additional manually imported files remain review-pending and do not replace the packaged comparisons.
- **Sound Experience:** One hub separates the 18 environmental pairs from five songs with original, 25-year 95 dBA Lex8h and 25-year 100 dBA Lex8h illustrations. Choose Soundscapes or Hearing examples in the hub, then press the selected example’s version button to start; press it again to stop. Hearing-loss examples retain an additional Play/Pause control. Switching versions during playback reloads the selected version at the same approximate transport time; decoding introduces a gap. This is not sample-synchronous switching.
- **Hearing Health:** prevention recommendations and five informative videos about health effects, hearing loss, protection and tinnitus (two versions). Swipe through separate video topic cards and press Play/Pause or Stop directly below that frame. No separate selection step; playback is optional.

Protection comparisons use direct version Play/Stop buttons; the separate Play/Pause control is hidden for these pairs. The two preset gain buttons are removed. Listening setup supplies one session gain; stop/restart and video Play/Pause remain. The application applies the same output gain to reference and variants. Visitors must begin with their device volume low and comfortable. Digital settings do not establish sound pressure at the ear. Selecting a catalog item or navigating does not play it. Pressing a version button explicitly requests playback; pressing the active version stops it. Hearing-loss switching retains approximate position; protection switching restarts at zero.

## Architecture and assets

AppManager explicitly installs MediaExperienceController. It starts after the guided controller has cloned the informational Noise Meter screen, avoiding copied video controls in that placeholder. It builds scrollable content inside the existing Sound Experience and Hearing Health panels; the saved scene and its GUIDs are preserved.

Resources/MediaCatalog.json is a local generated catalog: stable IDs, activity mappings, labels, method notes, relative media paths, byte sizes and SHA-256 hashes. Assets/StreamingAssets/HearingNotionMedia contains the packaged files. Full media stays outside Resources; only the small catalog loads at startup. A single shared transport loads one audio clip on demand using UnityWebRequestMultimedia, or prepares one VideoPlayer with a reusable 1280×720 RenderTexture. Changing selection/navigation/reset cancels pending audio loads and releases owned clips/textures. Focus or application interruption pauses playback without automatic resume. Playback starts with a short gain ramp; pause/navigation use immediate mute for a predictable stop. No real-time WHIS or protection DSP is added.

Tools/Audio/package_app_media.py packages 51 unchanged audio WAVs and five video playback copies. It requires a local FFmpeg executable via `--ffmpeg`; it does not install a global dependency. Videos are converted to H.264/yuv420p with AAC audio, padded to 1280×720, CRF 22 and fast-start metadata. Two supplied videos were HEVC, including a 4K file; originals remain intact. All playback video streams are decoded end-to-end as a file-integrity check. Unity recommends H.264 for broad video compatibility; actual device decoding remains a separate check. [Unity video compatibility](https://docs.unity.cn/2021.1/Documentation/Manual/VideoSources-FileCompatibility.html).

The generated catalog and media folder are locally excluded from Git publication. Documentation synchronization includes project-authored Markdown only, never music, videos, media titles, local source paths or paid assets. Public redistribution rights and editorial review remain separate from the authorized local prototype integration.

## Scientific provenance

Protection pairs retain their original sample rates/stereo and shared −6.02 dB headroom; no resampling or independent normalization is introduced. The 3M 1260 magnitude-only FIR represents cited laboratory attenuation means, with numerical response checks; individual fit, phase and perceptual equivalence are not validated. The concert source with pre-existing full-scale samples remains labeled for listening review. See [protection batch](SoundscapeProtection.md).

Song listening copies retain their common per-song gain and 24 kHz stereo format. The WHIS illustrations use user-selected flat 14.5/24.75 dB HL profiles with assumed alpha 0.5. The 95/100 dBA labels describe historical exposure scenarios inferred approximately from WHO Figure 1, not app output levels or individual predictions. Both prior verification status records now report PASS, including all ten processed exports and completed listening copies. See [WHIS batch](WHISSongBatch.md). No tinnitus tones or noise in Flappy Cloud are introduced by this task.

## Verification and remaining review

Run Tools/Tests/validate_packaged_media.py for all 56 hashes, safe relative paths, 18 activity links and 23 aligned audio comparison sets. Compile the runtime sources against Unity 2022.3.12f1 for Editor and Windows. Neither check proves device playback, synchronization, acoustic safety or UI rendering.

In Unity Main scene Play Mode, verify both orientations, selection-to-player scrolling, long Spanish text, play/pause/stop, switching during loading, rapid navigation, guided popups, session reset, focus loss and all five videos. Check listening at comfortable output levels on the actual demonstration hardware. Verify captions/transcripts and editorial/rights review before a public demonstration; the current videos have no newly authored captions. Mobile/WebGL streaming and codec behavior are unverified. Full-length WAVs remain substantial; no device memory/performance benchmark is claimed.

## Current configuration: existing library, no duplicate copies

This supersedes the packaged configuration above following the user’s correction. Run Tools/Audio/package_app_media.py --link-existing to index the existing external library without copying or converting files. MediaCatalog version 2 stores a private ExternalRoot and relative file paths. The current 51 WAVs and five original videos load directly from that folder, with the same activity links, gain relationships and controls. All 56 referenced files passed hash checks; all 23 comparison sets remain aligned. Generated duplicate files and metadata were verified and removed from Assets.

Keep the external folder available offline. If it moves, rebuild the index; missing files show an actionable message. The app is currently tied to this local library rather than self-contained for distribution. Original videos include HEVC, so actual device codec compatibility must be checked. Packaging/transcoding remains an explicit optional deployment step, not a requirement for this prototype. No media or private configuration was uploaded to GitHub. See [correction report](Changes/2026-10-22-003-existing-media-library.md).

Media button labels use anchored RectTransforms without ReadableTextHeight or LayoutElement. Their parent buttons own layout sizing. Scrolling text retains both components; do not add and destroy required components to adapt a label. See [dependency fix](Changes/2026-10-22-004-media-label-dependency.md).

Explorer now places linked audio status and Escuchar ejemplo above activity details; optional uploads are collapsed. No upload is needed for the existing library. The JSON catalog uses TextScriptImporter. See [Explorer correction](Changes/2026-10-22-005-explorer-linked-audio.md).

## Back-navigation crash mitigation

The observed native crash matched Unity UUM-14330: destroying a streamed AudioClip during cleanup. Local WAVs now explicitly disable streaming and compression and load fully before playback. Stop/detach/release and event cleanup remain explicit. One selected clip is loaded at a time; the largest current WAV needs about 71 MB of decoded float PCM, excluding request/decoder overhead. This is a size calculation, not a runtime benchmark. Back/Home controls are not destroyed; variant buttons hide on exit and return on selection. Runtime confirmation remains pending because a separate batch test could not open the already-open project. See [crash fix report](Changes/2026-10-22-006-soundscape-back-crash.md).

2026-11-05 correction: [Listening setup](ListeningSetup.md) controls the temporary common media/game gain. Flappy Cloud owns a separate buffered source active only in round 2; setup stops shared media before its optional preview. All WAV sources remain fully buffered to preserve the earlier native crash fix. See [corrections report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

## Inline video topics, 2026-11-05

Hearing Health now lists five independent topic cards in one scrollable page. Each has its own title/explanation and 16:9 frame, with Play/Pause and Stop below the frame. Pressing Play internally selects and prepares that card directly; no selection menu or separate global player step is exposed. Merely scrolling never autoplays. Switching cards stops the previous video and detaches its displayed texture; only one VideoPlayer and RenderTexture decode at a time. Pausing, missing-file/error feedback, 30-second preparation timeout, focus interruption and navigation/reset cleanup remain.

Audio comparison controls and gains are unchanged. The tinnitus preview alone has a separate -12 dB trim. See [listening setup](ListeningSetup.md), [gesture behavior](PageScrolling.md) and [correction report](Changes/2026-11-05-003-results-video-and-swipe.md).


## Visible video fix and controls below frames

The RawImage used a black tint, which multiplied the decoded picture by black even when VideoPlayer was playing. It now uses white with a black placeholder texture while unloaded. This distinction explains why earlier isPlaying checks could pass without visible video. Play/Pause and Stop are now in a horizontal row below each frame. Cards still select internally on explicit Play, share one decoder/target and stop on navigation/reset. The strengthened native review checks decoded nonblack texture pixels and advancing frames rather than relying only on playback flags. Actual physical audio remains a separate review.

See [unified sound navigation](SoundExperienceHub.md), [whole-page scrolling](PageScrolling.md) and [report](Changes/2026-11-05-004-unified-sounds-and-whole-pages.md).

2026-11-06 portability: the working catalog continues to use the external desktop library. The separate Android project bundles 57 verified files including an explicit preview record, clears machine paths and uses existing compatibility video bytes. UnityWebRequest uses escaped asset URLs, while VideoPlayer uses native local filesystem paths; this fixes portable filenames containing spaces. Android extracts videos from APK assets to app-private VideoCache on demand and cancels pending extraction on navigation/interruption. All WAV loading stays buffered. A missing or empty optional preview entry falls back to the original desktop preview. Physical Android jar/extraction/playback remains unverified until an actual player run. See [deployment](AndroidDeployment.md) and [report](Changes/2026-11-06-001-editor-dhwani-android.md).

English interface update (2026-11-06): EnglishPresentation applies English media labels/notes in memory by stable ID/kind. Private paths, original files, common comparison gain and codecs are unchanged. Proper music titles and original video language are retained and explained. Playback/status controls are English; shared transport lifecycle and two-frame initialization are preserved. See [design](HomeRedesign.md) and [report](Changes/2026-11-06-006-rounded-english-interface.md).
