# Modification report — WHIS audio launcher

- Report ID: 2026-10-20-003
- Date: 2026-10-20 (America/Mexico_City)
- Type: feature / tools / documentation

## Request and resulting behavior

Provide one code entry point that runs setup and processing, takes an audio input and produces a WHIS output. Tools/Audio/run_whis.m launches audio selection, profile/level entry and output-parent selection dialogs when run without arguments. It calls process_whis_dtvf, which calls setup_whis. It also accepts input file, new output directory and configuration for scripted use. Outputs are the processed WAV, normalized source WAV and local review record; no audio plays.

## Modifications

| File or asset | Change and purpose |
| --- | --- |
| Tools/Audio/run_whis.m | Single launcher with cancellation, literal numeric parsing, explicit modeled-only interactive configuration and output-path feedback. |
| Tools/Audio/test_whis_dtvf.m | Route the existing reference-parity check through the launcher's three-argument interface. |
| Docs/WHIS.md | Run-button instructions, dialogs, output names, scripted invocation and assumptions. |
| Docs/FEATURES.md | Update F-009 behavior and feature history. |
| Docs/Changes/README.md and this report | Index and document the task. |
| Tools/Audio/whis-launcher-validation.log | Ignored local MATLAB validation evidence. |

## Decisions and implications

Reuse existing WHIS-DTVF and setup code without changing the scientific algorithm, reference pins, dependencies or export schema. The dialog's prefilled flat 25 dB HL/alpha 0.5 profile and 60/90 dB model-level mapping are fictional illustrative assumptions, not patient data or prescribed playback levels. Users can edit them; interactive calibration is always recorded as modeled-only. Seven numeric thresholds are parsed without eval/str2num. A new generated directory prevents overwrites; canceled dialogs do not process audio. Inputs must already be 24 or 48 kHz. No Unity code/assets, scene bindings, GUIDs, build settings, package versions, participant persistence or playback behavior change. Scientific provenance and limits remain documented in [WHIS](../WHIS.md).

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| MATLAB numerical suite through launcher | passed | MATLAB R2023b executes test_whis_dtvf; exported mono files from run_whis match a direct reference call within 24-bit quantization. Stereo, silent-channel and rejection checks pass. |
| GUI selection, editing and cancellation | not run | Dialog branch reviewed in source; interactive desktop operation remains to verify. |
| Documentation file links | passed | Relative targets in changed Markdown resolve. |
| Unity/C# compilation and Play Mode | not run | No Unity source/assets or runtime behavior changed. |
| Device output / listening / calibration | not run | Synthetic files only; no playback or calibrated acoustic claim. |

Only task-specific project Markdown is published under the standing documentation authorization. Code, logs, generated audio and reference checkouts remain local; published contents are verified against local files at delivery. Connector publication does not synchronize local Git history.

## Performance

Not measured; no optimization or real-time performance claim.

## Limitations and follow-up

Interactive dialogs require manual verification. Non-24/48 kHz files are rejected with the existing actionable diagnostic; no silent resampling is added. Physical calibration, source selection/rights, listening review and Unity playback remain pending. All exports remain review-pending. A failed final file write may leave a partial output directory as documented for the underlying processor.

## Rollback

Remove run_whis.m, restore the test's direct process_whis_dtvf call and reverse only the task-specific documentation additions. Preserve earlier processing/setup files, reference checkouts, source audio and unrelated edits. Reverse published documentation with a new commit against the current remote head; do not reset or force-push.
