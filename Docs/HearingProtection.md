# Generic hearing-protection illustration — offline MATLAB

Updated: 2026-10-21 (America/Mexico_City).

## Run

Open Tools/Audio/run_hearing_protection.m in MATLAB and click Run, or add Tools/Audio to the path and call run_hearing_protection. Select source audio and an output parent folder. The generic preset is built automatically; no device/profile input is required. Canceling a dialog stops without processing.

Requires MATLAB and Signal Processing Toolbox. Supported generic-preset rates: 22.05–192 kHz, mono/stereo. No resampling or playback occurs. A new directory receives source.wav, hearing-protection.wav, review-record.mat and response-check.csv. Input material, licensing, comfortable playback, physical calibration and Unity transport/safety integration still require review. Nothing is imported into Unity automatically.

This is a generic educational illustration from one documented reference curve, not an average of all protectors or a validated reproduction of wearing earplugs. The underlying DSP has numerical verification. The magnitude-target interpretation of sparse laboratory data, interpolation, phase and extrapolation are engineering assumptions without perceptual validation. It must not be labeled a validated protector simulation, fit test, dose estimate or protection guarantee.

## Evidence and reference data

1. [3M: Attenuation Data for Hearing Protectors](https://multimedia.3m.com/mws/media/91870O/attenuation-tables.pdf), January 2004, p.2, reusable model 1260. Manufacturer reports average real-ear laboratory attenuation tested according to ANSI S3.19-1974. The historical table supplies the numeric reference, not current product certification or individual fit. No NRR derating rule is adopted.
2. [MATLAB fir2](https://www.mathworks.com/help/signal/ref/fir2.html): documented frequency-sampling FIR design, inverse FFT and windowing. Used instead of an invented filter topology.
3. [MATLAB fftfilt](https://www.mathworks.com/help/signal/ref/fftfilt.html): documented overlap-add linear FIR filtering. Numerical outputs are checked against direct convolution.
4. [NIOSH 2025 individual fit-testing recommendation](https://www.cdc.gov/niosh/publications/numbered/2025-104.html): individual quantitative fit testing evaluates received attenuation. Lab-data-based audio does not replace this.

| Frequency Hz | 125 | 250 | 500 | 1000 | 2000 | 3150 | 4000 | 6300 | 8000 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Reference laboratory mean dB | 27.2 | 27.9 | 31.0 | 30.9 | 34.2 | 35.8 | 37.5 | 39.9 | 41.7 |
| Reported SD dB | 4.3 | 3.7 | 3.6 | 3.1 | 3.8 | 3.0 | 3.9 | 4.2 | 5.1 |

SD is retained as provenance; it is not a random perturbation or personal confidence interval. Laboratory threshold attenuation is not a measured complex transfer function. The example uses these means as a magnitude target only; it is not an ANSI measurement implementation or validation study.

## Documented processing

- generic_hearing_protection_profile creates a dense log-frequency interpolation of attenuation in dB, then converts amplitude using 10^(−attenuation/20).
- Frequencies below 125 Hz and above 8 kHz hold endpoint values. These unmeasured extrapolations are explicitly assumptions, not new measurement results.
- MATLAB fir2 designs a 4096-order linear-phase FIR with the documented Hamming-window frequency-sampling method. Its 2048-sample delay is known; phase is designed rather than measured.
- freqz measures realized attenuation at the nine reference frequencies; design is rejected if maximum error reaches 1 dB. This tolerance is an engineering check, not physiological validation.
- process_hearing_protection applies fftfilt separately to each channel, retaining convolution tails. The same generic response is used on both stereo channels.
- The reference source is delayed by the same 2048 samples and zero-padded to output length. Neither file is independently normalized or loudness matched, preserving the intended attenuation difference.
- Above-unity frequency response, clipping, mismatched rates/channels, invalid profiles and existing output directories are rejected. No limiter, automatic gain compensation or acoustic safety claim is supplied.
- Review record contains the complete FIR, reference values, realized response/error, source/response provenance, assumptions, peaks, rate and MATLAB version. Paths remain local. CSV exposes frequency/target/realized/error for review.

The default magnitude example intentionally excludes fit leakage, bone conduction, occlusion effects, directional/binaural differences, wearer variability, active electronics and level-dependent behavior. It is not suitable for predicting protection in impulse noise or choosing workplace PPE. No physical output measurement was performed.

## Optional advanced input

The three-argument run_hearing_protection(audioFile, newOutputDirectory, profileMAT) calls the same processor. A measured profile must contain samples-by-one/two impulseResponse, sampleRate, device, measurementSource, validationReference, measurementMethod, validityLimits, responseDefinition='protected-over-unprotected', linearPassive=true and reviewed=true. A qualified reviewer must establish calibration, validity and provenance; a boolean or citation is not proof. Absolute ear/room IRs and nonlinear/active protectors are unsupported. Generic metadata explicitly uses a different response definition to avoid pretending its FIR was measured.

Synthetic test profiles require the explicit testOnly flag and receive a test-only record. They are not public presets.

## Verification

Run addpath('Tools/Audio'); test_hearing_protection. MATLAB R2023b tests passed: direct-convolution/export parity within 24-bit quantization, stereo, full tails, reference alignment, CSV, rejection of overwrite/unreviewed synthetic profiles/rate mismatch/gain/channel mismatch. Generic anchor checks passed at 22050, 44100, 48000 and 96000 Hz. The 48 kHz maximum anchor error was 0.047506 dB.

This is numerical response verification, not a repeat of the manufacturer's measurements or a human listening validation. GUI dialogs, device playback, physical SPL, subjective review and Unity integration remain unverified. All generated material stays review-pending in local output; generated audio/reference documents are not included in documentation publication.
