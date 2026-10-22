# 18 soundscapes — 3M 1260 laboratory-reference filtering

Updated: 2026-10-22 (America/Mexico_City).

The researcher selected the existing 3M 1260 reference to create hearing-protection examples from all 18 source soundscapes. All 18 exports completed and passed numerical/file verification. This is an educational magnitude illustration based on manufacturer laboratory data, not a measured complex transfer function, individual fit test or validated reproduction of wearing the protector.

## Outputs

A new Soundscapes_3M1260_Protected folder sits beside the original Soundscapes folder in the user-designated Sounds library. Its root contains 18 named __3M1260.wav exports. References_and_Records contains one subfolder per source, with aligned unfiltered source.wav, review-record.mat and response-check.csv. Profiles stores complete rate-specific target/FIR data. Root processing-summary.csv, verification.mat and README.txt describe the batch. Original files were preserved and checked by SHA-256.

All original sample rates (44.1, 48 and 96 kHz), full source content and stereo channels are preserved; outputs use 24-bit WAV. No resampling occurs. Full 4096-sample filter tails are retained, with corresponding reference padding/delay; output duration is slightly longer than the input. This is deliberate, not truncated source material.

## Processing and evidence

Tools/Audio/process_soundscape_library.m reuses generic_hearing_protection_profile and process_hearing_protection. The profile metadata identifies the selected 3M 1260 laboratory reference. The frequency-sampling fir2 design and fftfilt convolution are unchanged. See [HearingProtection](HearingProtection.md) for the numeric table, primary manufacturer/MATLAB sources, standard, assumptions and validation scope.

A common 0.5 linear input gain (−6.0206 dB) is applied to every source/reference/protected pair before filtering. This gives consistent digital headroom without independent normalization of the protected versions. One original source has 193,494 full-scale samples and is flagged for listening/source review. Applying headroom does not reconstruct already clipped peaks or certify input quality.

Protected outputs may be substantially quieter, as expected from the reference attenuation. Compare with the aligned reference at the same comfortable playback setting; do not compensate by independently peak/loudness normalizing the protected files. Digital file levels are not measured environmental exposure or calibrated output SPL. No autoplay or Unity import is performed.

## Verification completed

- MATLAB processed and verified all 18 inputs/outputs, rate/channel/length retention, source gain and reference alignment.
- Each fftfilt export was compared with an independent whole-signal FFT linear convolution, within 24-bit quantization tolerance.
- All processed peaks remain below full scale; reference/protected peaks and RMS are in the summary CSV.
- Maximum realized-filter error at manufacturer reference frequencies: 0.043795 dB at 44.1 kHz, 0.047506 dB at 48 kHz and 0.091556 dB at 96 kHz.
- Separate Python checks confirmed 18 root WAVs, stereo, original rates, 24-bit exports, full-tail lengths and all original SHA-256 hashes.

These are digital/numerical checks. Actual listening, physical acoustic output, user fit and perceptual equivalence were not verified. The historical laboratory averages do not establish present-day product certification or workplace protection. Off-table endpoints, phase and other excluded effects remain as documented in the method guide. Review the flagged source and comfortable output before public use.

## Reproducibility

In MATLAB, add Tools/Audio to the path and call process_soundscape_library(sourceDirectory, newOutputDirectory). It requires exactly 18 WAV files and refuses an existing destination. It creates one temporary, common-headroom input at a time in ignored Tools/Audio/Output, deletes only that generated staging file after success, and retains the complete reference/profile records. Inputs, outputs, private names and local logs are excluded from GitHub documentation publication.
