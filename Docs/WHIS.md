# WHIS-DTVF offline hearing-loss illustrations

Last updated: 2026-10-20 (America/Mexico_City).

WHIS with direct time-varying filtering (DTVF) is the selected hearing-loss simulation method. The app-owned MATLAB wrapper calls the authors' reference algorithm; it does not replace it with a custom cascade of Butterworth filters. This is an offline authoring tool, not a Unity DSP implementation, hearing test or reproduction of an individual's experience. Sound Experience playback remains unimplemented. See [F-009](FEATURES.md#f-009-sound-experience) and the [task report](Changes/2026-10-20-002-whis-dtvf-offline-processing.md).

## Evidence and its scope

1. Toshio Irino (2023), *Hearing Impairment Simulator Based on Auditory Excitation Pattern Playback: WHIS*, IEEE Access 11, 78419–78430, [DOI 10.1109/ACCESS.2023.3298673](https://doi.org/10.1109/ACCESS.2023.3298673). [Author-hosted manuscript on arXiv](https://arxiv.org/abs/2206.06604). Documents auditory excitation matching, compression health, active/passive loss and synthesis. Evaluates modeled input-output functions and spectral distances; identifies limitations when compression remains healthy. Model agreement does not establish clinical or individual perceptual equivalence.
2. Irino, Doan and Ishikawa (2024), *Signal processing algorithm effective for sound quality of hearing loss simulators*, Interspeech, 882–886, [paper and DOI 10.21437/Interspeech.2024-111](https://www.isca-archive.org/interspeech_2024/irino24_interspeech.pdf). Sections 2.2.1–2.2.2 describe the attenuation and DTVF synthesis. Paired comparisons in 15 young normal-hearing listeners found less perceived distortion for DTVF than the tested Cambridge and WHIS filterbank-synthesis alternatives. The tested profile/materials and sound-quality outcome do not validate every hearing profile or Spanish material. The study's level matching was for distortion judgments; it is not adopted for audibility A/B files.
3. [Authors' WHIS repository](https://github.com/AMLAB-Wakayama/WHIS), including WHISv302/WHISv30_Batch.m, WHISv302.m, WHISv302dtvf.m, WHISv30_DirectTVF.m and WHISv30_GetSrcSndNrmlz2CalibTone.m. These are the executable source of processing and source-level normalization, not code recreated from a paper summary. The supplied comparison demo invokes playback; this project does not run it.
4. [Authors' gammachirp-filterbank repository](https://github.com/AMLAB-Wakayama/gammachirp-filterbank), particularly GCFBv234/GCFBv23_HearingLoss.m. Establishes the seven-frequency manual profile, nonnegative hearing levels and effective compression-health adjustments.
5. [WHIS setup/calibration notes](https://github.com/AMLAB-Wakayama/WHIS/blob/main/WHISv302/_ReadMeFirst_WHISv302.md). The reference tone's internal digital RMS is -26 dB. Its physical SPL must be established through calibration; the numeric configuration is not evidence that calibration occurred.

## Reference versions and installation

Local reference checkouts are outside Assets under Tools/ThirdParty, ignored by the project repository. No third-party code/audio is published with the documentation.

| Dependency | Local revision inspected and required | Use |
| --- | --- | --- |
| WHIS | `33f5c29f7f2aeb74d0a8b528965f4ba238451921` | WHISv302, DTVF |
| gammachirp-filterbank | `fa8e5c10d3a40da524b24f2469b343617d59ca1b` | GCFBv234 |

The current StartupWHIS.m points to v234; older README statements about v233 are insufficient to describe this checkout. setup_whis.m checks exact revisions and clean worktrees before processing. Keep original license files: WHIS root contains CC0-1.0; the filterbank root contains Apache-2.0. File-level notices and any later redistribution need review; root labels are not clearance for arbitrary sound material.

From the project root, install if absent (do not clone over an existing checkout):

```powershell
git clone https://github.com/AMLAB-Wakayama/WHIS.git Tools/ThirdParty/WHIS
git -C Tools/ThirdParty/WHIS checkout 33f5c29f7f2aeb74d0a8b528965f4ba238451921
git clone https://github.com/AMLAB-Wakayama/gammachirp-filterbank.git Tools/ThirdParty/gammachirp-filterbank
git -C Tools/ThirdParty/gammachirp-filterbank checkout fa8e5c10d3a40da524b24f2469b343617d59ca1b
```

MATLAB with Signal Processing Toolbox is required. No Unity dependency, package, scene, prefab or serialized reference is changed. MATLAB paths are set for the current process only; no savepath or global installation is used.

## Processing steps and provenance

| Step | Implemented behavior | Basis |
| --- | --- | --- |
| 1. Validate authored inputs | Require exactly 125, 250, 500, 1000, 2000, 4000 and 8000 Hz, with nonnegative dB HL; scalar or seven-point alpha in [0,1]. Reject missing assumptions. No implicit interpolation or negation of old attenuation gains. | Reference manual-profile grid/sign, source 4; strict validation is project policy. |
| 2. Establish modeled acoustic levels | Caller specifies source RMS SPL and calibration-tone SPL plus modeled-only/measured status and a note. WHIS normalizes the source to its calibration reference. Neither dB HL nor digital RMS is treated as dB SPL. | Sources 3 and 5. |
| 3. Preserve channels and rate | Accept mono/stereo at 24 or 48 kHz, as supported by WHISv302.m. No implicit downmix/resampling. For stereo, process each ear independently with the same authored profile. Source SPL refers to mean channel power; each channel gets an RMS-relative SPL offset, preserving their common gain reference. An exactly silent channel bypasses upstream normalization and remains zero. | Mono upstream API, source 3; stereo adaptation is a project engineering choice, not independently perceptually validated. |
| 4. Analyse cochlear response | Set HLoss.Type='HL0', explicit hearing levels and compression health; use the reference dynamic GCFB and FreeField outer/middle-ear convention. | Sources 1, 3 and 4. FreeField is a model convention, not headphone equalization. |
| 5. Derive level reduction | Upstream code computes active, level-dependent reduction plus passive reduction. Alpha is an assumption separate from the audiogram. Save effective parameters because the reference code may adjust alpha to fit the supplied loss. | Sources 1, 2 §2.2.1 and 4. |
| 6. DTVF synthesis | Explicit SynthMethod='DTVF'. Upstream synthesis builds time-varying minimum-phase filters and reconstructs the signal. No added spectral smearing, temporal smearing, recruitment expansion or post-EQ is layered onto WHIS. | Sources 1, 2 §2.2.2 and 3. |
| 7. Save a review pair | Save the upstream normalized source and processed output as 24-bit WAV, plus a local MAT processing record. Retain upstream lengths/tails and pad only trailing samples when needed. Reject clipping rather than independently normalize/limit the files. Never autoplay or import into Unity automatically. | Source normalization comes from source 3; file/review controls are project engineering choices. |

This wrapper does not establish a validated binaural model. Different left/right audiograms, headphone transfer compensation and perceptual time alignment require separate work. Do not infer hearing-health risk from chosen profiles.

## Usage

For a single entry point, open Tools/Audio/run_whis.m in MATLAB and click **Run**, or type `run_whis` after adding Tools/Audio to the path. Select an input file, edit the seven hearing levels, alpha and modeled level assumptions, then select a parent output folder. A new run directory contains whis-dtvf.wav (processed audio), source.wav (normalized reference) and review-record.mat. The Command Window prints their paths. Canceling a dialog stops the launcher without processing. The prefilled settings are a fictional example and require deliberate review; the interactive workflow always records modeled-only calibration. It does not play audio. Inputs must already be 24 or 48 kHz.

For automation, `record = run_whis(inputAudio, newOutputDirectory, cfg)` uses the same processing path without dialogs. The launcher calls process_whis_dtvf, which calls setup_whis; running either supporting file separately is unnecessary. See the [launcher report](Changes/2026-10-20-003-whis-audio-launcher.md).

Run in MATLAB from the project root. This fictional flat profile and alpha are examples, not defaults, participant data or a clinical prescription. All seven points must be supplied deliberately; the wrapper does not invent a missing 125 Hz threshold or map a 3000 Hz point automatically.

```matlab
addpath('Tools/Audio');
cfg.audiogram = [[125 250 500 1000 2000 4000 8000]' repmat(25,7,1)];
cfg.compressionHealth = 0.5; % explicit illustrative assumption
cfg.sourceSPLdB = 60;       % modeled source level, not a measured playback level
cfg.calibrationSPLdB = 90;  % digital headroom reference, not a listening instruction
cfg.calibrationStatus = 'modeled-only';
cfg.calibrationNote = 'Illustrative level mapping; playback has not been calibrated.';
cfg.profileNote = 'Fictional flat 25 dB HL educational profile; alpha assumed.';
% Replace inputAudio with a local reviewed input path; use a NEW output directory.
record = process_whis_dtvf(inputAudio, 'Tools/Audio/Output/review-001', cfg);
```

Outputs are source.wav, whis-dtvf.wav and review-record.mat. They remain review-pending. The record contains requested/effective parameters, declared calibration status, reference pins, MATLAB version, peaks, RMS and original/output lengths. It is local authoring metadata; do not publish participant profiles, private paths or sound files. Existing directories are refused. A write/storage failure can leave a partial directory; use a new directory after resolving it.

If clipping is rejected, revise the digital headroom/calibration reference and document it; any actual playback calibration must match the revised mapping. Do not increase listening volume to compensate for the simulated loss. Source provenance/distribution rights, acoustic output, fades, transport/stop controls and safe comfortable playback remain separate review requirements.

## Checks and remaining work

Run `addpath('Tools/Audio'); test_whis_dtvf` in MATLAB. It uses synthetic signals, compares exported mono files against a direct reference call within 24-bit quantization, checks stereo source-level preservation and a silent channel, and exercises input/overwrite/clipping rejection. Generated fixtures live in ignored Tools/Audio/Output. See the task report for actual results.

Numerical checks do not repeat the publications' human validation. Source audio has not been selected or processed for public use, physical calibration/device listening has not been performed, and Unity Play Mode/playback integration is pending. No sample-rate conversion, latency compensation or acoustic safety limit is silently supplied by this tool.
