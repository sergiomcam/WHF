# Modification report — exposure-labeled WHIS song batch

- Report ID: 2026-10-21-004
- Date: 2026-10-21 (America/Mexico_City)
- Type: audio authoring / tools / documentation

## Request and resulting behavior

Process five supplied songs into two additional folders approximating 25-year 95/100 dBA LEX8h exposure scenarios using existing WHIS. User explicitly chose flat illustrative profiles and assumed alpha .5 after the average-versus-audiogram distinction was explained. Added a memory-bounded batch and started full-song rendering. Completion/verification remains pending while the numerical reference processes the library.

## Modifications

| File | Purpose |
| --- | --- |
| Tools/Audio/process_whis_song.m | Explicit 24 kHz resampling, context/core segmentation, whole-song level reference, pinned WHIS calls and full-duration stereo WAV/provenance export. |
| Tools/Audio/process_whis_library.m | Two approved flat profile variants, five-song batch, no overwrite, summary/profile/readme output. |
| Tools/Audio/verify_whis_library.py | One-time completion monitor and original/hash/WAV/sidecar verifier; final results pending. |
| Tools/Audio/test_whis_song.m | Single-segment reference parity and segmented synthetic fixture checks. |
| Docs/WHISSongBatch.md | Graph interpretation, approximations, processing/data boundaries and progress. |
| Docs/FEATURES.md, Docs/README.md, Docs/Changes/README.md and report | F-009 history, guide entry and indexed task record. |
| User-designated Sounds folder: two new WHIS_25y_* folders | Local review-pending WAVs and records; originals unchanged by processing. |
| Tools/Audio/song-inspection.log, song-wrapper-validation.log, whis-song-batch.log | Ignored local execution evidence. |
| tmp/song-original-hashes.json and rendered figure | Local inspection/hash evidence, not production assets or publication. |

## Decisions and implications

Read the supplied PDF and visually inspected Figure 1. Approximate 20/30-year chart anchors interpolated to 14.5 and 24.75 dB HL at 25 years; uniform seven-frequency application is user-selected, not an ISO frequency-specific estimate. Model alpha .5 is requested, with upstream effective adjustments recorded. Historical exposure levels are never presentation levels. Five sources are 44.1 kHz stereo; explicitly resample to 24 kHz because the reference supports 24/48 kHz. Context/core segmentation is an engineering adaptation required by memory, not a published equivalence claim. No Unity, package, scene, reference-checkout, questionnaire or participant-data changes. Private song audio/names/paths and records stay local; publish authored Markdown only.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| PDF/chart review | Passed | Local text extracted and Figure 1 rendered/inspected; average threshold shift and chart interpolation distinguished from individual audiograms. |
| Original audio inspection | Passed | MATLAB reports five 44.1 kHz stereo M4A songs, approximately 166–370 seconds each. |
| Song wrapper numerical tests | Passed | Stereo/duration and single-segment reference/export parity; segmented stationary fixture relative RMS error printed 0.000000. |
| Initial test harness | Failed, corrected | Vector/matrix comparison indexing in test corrected; final numerical tests passed. |
| Full ten-file rendering/verification | Pending | Long-running batch is executing; no completion claim. |
| Listening/device/acoustic/Unity | Not run | No playback or physical calibration; music rights and perceptual seam review remain necessary. |

## Performance

Reference rendering is offline and computationally heavy. Source/system inspection found 16 GB RAM; bounded segment processing avoids whole-song filterbank allocations. No speedup or real-time claim.

## Limitations and follow-up

Wait for rendering, verify all ten WAVs and sidecars, confirm rates/durations/channels/peaks and original hashes, then update this report and guide to actual completion status. Numerical fixture checks do not validate all music boundaries or simulate individual long-term loss. No safe output/rights clearance or public-use approval is implied.

## Rollback

Reverse only these new wrapper/test/docs additions if desired. Preserve source M4As and existing WHIS/reference files. Generated local output folders must be reviewed deliberately before any deletion; no recursive cleanup is performed. No Unity regeneration or data migration is needed.

The first full song completed and its WAV was inspected: 24 kHz, stereo, 24-bit, original duration retained, peak below digital clipping. All five original hashes were checked unchanged at that point. The remaining batch continues. A one-time verify_whis_library.py --wait helper checks all ten WAV headers/durations/peaks, sidecars and original hashes after the batch completion marker, then writes Tools/Audio/Output/whis-song-verification.json. The verifier is running; its final result is pending. It is a finite local batch check, not a recurring automation.
