# Offline audio and informative videos

Implemented 2026-10-22; Unity interaction, listening and device playback verification remain pending.

## Where to find the material

- **Exposure Explorer:** the 18 annex activities offer “Explorar este sonido”, which selects their packaged original/protected comparison in Sound Experience. Three chart-only activities have no invented matching recording. Additional manually imported files remain review-pending and do not replace the packaged comparisons.
- **Sound Experience:** 18 environmental pairs, followed by five songs with original, 25-year 95 dBA Lex8h and 25-year 100 dBA Lex8h illustrations. Select an example, choose a version and press Reproducir. Switching versions during playback reloads the selected version at the same approximate transport time; decoding introduces a gap. This is not sample-synchronous switching.
- **Hearing Health:** prevention recommendations and five informative videos about health effects, hearing loss, protection and tinnitus (two versions). Select a video, then press Reproducir. Playback is optional.

Controls provide play/pause, stop/restart, and two low digital audio gains for sound comparisons. The application applies the same output gain to reference and variants. Visitors must begin with their device volume low and comfortable. Digital settings do not establish sound pressure at the ear. No automatic playback occurs on selection or navigation; changing comparison version while already playing resumes the explicitly requested playback.

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
