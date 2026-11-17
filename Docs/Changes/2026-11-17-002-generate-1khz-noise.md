# Modification report - Generate 1 kHz noise

- Report ID: 2026-11-17-002
- Date: 2026-11-17 (America/Mexico_City)
- Type: audio authoring

## Request and resulting behavior

Generate only bb_25dB_1kHz.wav for ten seconds from the supplied ALL_generation.m bb branch. User explicitly removed both fades. Completed as a standalone local WAV; not integrated into the app.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Generate source-derived noise without fades | LocalAudio/GeneratedPreview/generate_bb_1khz.m; LocalAudio/GeneratedPreview/bb_25dB_1kHz.wav | MATLAB designfilt bandpassiir order 2; half-power edges 750/1250 Hz; 24 kHz; Gaussian noise, deterministic seed 20261117; source amplitude 0.004*1.41*3*0.5. No normalization, mixing, MP3 conversion or envelope. |
| Save numerical evidence | LocalAudio/GeneratedPreview/verification.json; LocalAudio/GeneratedPreview/matlab.log | Read-back WAV and frequency-response checks. |
| Record authoring | Docs/Changes/2026-11-17-002-generate-1khz-noise.md; Docs/Changes/README.md | Trace source, user-directed no-fade decision and validation. |

## Decisions and implications

Supplied code is provenance, not evidence of clinical/perceptual validation. Its bb label denotes band-limited white noise here. The 25dB filename label is a source preset, not calibrated SPL/HL. Only the standalone generator branch was adapted; unrelated song processing/deletion routines were not executed. No app source, Assets, GUIDs, dependency, scene, schema or participant data changed. No user-visible app feature changed, so FEATURES.md is unchanged. No startup-slider integration requested in this generation-only step. MATLAB preferences scratch directory was created locally after a sandbox startup failure; installed licensing access was needed for successful MATLAB execution. No new recurring workflow identified.

## Validation

| Check | Result | Evidence or reason |
| --- | --- | --- |
| MATLAB generation/read-back | passed | 240000 samples, 10 seconds, mono, 24000 Hz, 16-bit PCM; no fades. |
| Signal content/clipping | passed | Peak 0.010009765625; RMS 0.00209626419164793; 238588 nonzero samples; finite values and peak below 1. |
| Filter response | passed | freqz half-power levels at 750 and 1250 Hz within 0.05 dB of -3.0103 dB. |
| File identity | passed | 480044 bytes; SHA-256 b13f30bdc4a692ebd0f819767ba84371b0984278df24211185c92cfe745b1f99. |
| Listening/acoustic calibration | not run | No acoustic SPL/HL or comfortable-listening claim. |
| Unity compilation/Play Mode/device | not run | No app integration or C# changes. |

## Performance

Not applicable; no app optimization.

## Limitations and follow-up

Noise is not a validated tinnitus percept. A finite causal IIR has its natural startup transient; no intentional fade envelope was added. Endpoint discontinuities are possible, as expected with the requested no-fade file. Audio, executable generator and local logs remain local; only Markdown report/index are published.

## Rollback

Remove only the task-specific WAV, generator, verification and log files if no longer needed. Reverse this report/index row separately. Do not alter existing audio or app configuration.
