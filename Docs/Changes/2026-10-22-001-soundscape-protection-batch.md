# Modification report — 18 protected soundscapes

- Report ID: 2026-10-22-001
- Date: 2026-10-22 (America/Mexico_City)
- Type: audio authoring / tools

## Request and resulting behavior

Filter all 18 source soundscapes as hearing-protection examples and save separately. User selected the existing 3M 1260 laboratory-reference profile. Completed 18 protected WAVs, aligned unfiltered references, per-file provenance/response records, rate-specific profiles and batch summary. Original files remain unchanged.

## Modifications

| File/output | Purpose |
| --- | --- |
| Tools/Audio/process_soundscape_library.m | Batch wrapper, explicit common headroom, reuse existing filter, independent FFT convolution verification, original hashes and metadata/output checks. |
| Local Sounds/Soundscapes_3M1260_Protected | 18 protected WAVs plus aligned source/reference and provenance/profile/summary data. Private filenames/paths/audio remain local. |
| Tools/Audio/soundscape-inspection.log and soundscape-processing.log | Ignored local MATLAB execution evidence. |
| Docs/SoundscapeProtection.md | Outputs, method, primary evidence link, complete verification and remaining review. |
| Docs/FEATURES.md, Docs/README.md, Docs/Changes/README.md and report | F-009 behavior/history and guide/modification index. |

## Decisions and implications

Use the existing documented fir2/fftfilt method and published 3M 1260 laboratory mean data; no new attenuation curve or device inference. This remains a magnitude approximation, not a measured phase response, field/fit validation or clinical guarantee. Preserve source rates/stereo and full filter tail, with aligned reference delay. Common gain .5 gives all pairs 6.0206 dB headroom without independent normalization. One source contains 193,494 full-scale samples, flagged rather than claimed repaired. No Unity, source audio, metadata GUID, package, scene, participant storage or playback changes. Staging cleanup only deletes the task-created temporary file; output relocation is within the named new folder. Documentation-only publication preserves audio/privacy boundaries.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| MATLAB batch | Passed | All 18 completed and verified with rate/channel/length, reference gain/alignment, finite/no-clipping output, SHA-256 and independent whole-signal FFT convolution parity within quantization tolerance. |
| Filter targets | Passed | Maximum anchor errors .043795/.047506/.091556 dB for 44.1/48/96 kHz respectively. |
| Independent Python audit | Passed | 18 top-level WAVs, original rates/stereo, 24-bit export, original-frame count +4096, original SHA-256 and sub-unity peaks. |
| Source quality | Flagged | One supplied source has many full-scale samples; headroom does not repair original clipping. |
| Listening/physical output/fit/Unity | Not run | No playback or individual/acoustic validation performed. |
| Documentation links | Passed | Relative file targets checked before publication. |

## Performance

Not benchmarked. Offline convolution reuses rate-specific profiles; no runtime/performance improvement claim.

## Limitations and follow-up

Listen to pairs at a comfortable consistent setting, inspect flagged source quality and review real output/provenance before public use. Protected versions are intentionally quieter. No actual wearer attenuation or perceptual equivalence is established. Final response supplies verified documentation publication evidence.

## Rollback

Reverse this batch-wrapper/docs change if desired. Deliberately review generated output folder before any removal; original Soundscapes remain intact. Preserve existing generic hearing-protection/WHIS tools and unrelated Unity work. No scene regeneration or migration needed; publish any documentation reversal as a follow-up commit.
