# Modification report — WHIS listening-level correction

- Report ID: 2026-10-21-005
- Date: 2026-10-21 (America/Mexico_City)
- Type: fix / audio authoring

## Request and resulting behavior

User reported no real music in exported WAVs. Samples contained music-correlated signals but were extremely quiet due to retained model calibration/headroom. Created separate listening comparisons using one common per-song gain for reference and both variants, rather than independently normalizing away the intended loss. Eight available processed copies now pass numerical gain checks; two remaining technical renders/final listening copies are pending.

## Modifications

| File or output | Purpose |
| --- | --- |
| Tools/Audio/prepare_whis_listening.m | Reconstruct normalized reference, common presentation gain to −6 dBFS reference peak, preserve both model-level differences, reject clipping and verify quantized sample agreement. |
| Tools/Audio/finish_whis_listening.py | One-time wait/finalize helper, all-ten requirement and local completion JSON. |
| Local Sounds/WHIS_Listening_Comparisons | Reference/95/100 subfolders, gain records, README and short comparison previews. No originals/raw technical exports overwritten. |
| AGENTS.md | Require RMS/audibility/content checks and distinguish common listening gain from independent normalization/physical calibration. |
| Docs/WHISSongBatch.md, Docs/FEATURES.md, Docs/Changes/README.md and report | Diagnosis, F-009 status/history and verification evidence. |
| Tools/Audio/listening-*.log, Output/whis-listening-status.json | Ignored local diagnostics/completion evidence. |

## Decisions and implications

The model's 60/90 dB mapping yielded quiet digital samples; file header and no-clipping checks alone were insufficient. Common presentation gain changes no WHIS parameters and preserves each source/variant relationship within a song. Do not compare absolute playback level across different songs or infer calibrated SPL. Original music and technical WAVs stay intact. No Unity, package, scientific-reference, hearing-profile, participant schema or raw-data publication changes. Finalizer is a finite local batch helper, not a recurring automation.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| Diagnosis | Passed | Nonzero excerpts measured around −70/−80 dBFS RMS in technical variants. |
| Common-gain preparation | Passed for eight available copies | MATLAB checks full-file samples equal technical samples times the same per-source gain within 24-bit quantization; verifies stereo/rate/duration shape and no clipping. |
| Sample levels/content | Passed numerically | Corrected sample RMS approximately −18/−33/−42 dBFS reference/95/100; RMS-envelope correlations .9624/.9499. |
| Remaining two copies | Pending | Source WHIS renders continue; one-time finalizer waits and then requires ten prepared outputs. |
| Listening/device/acoustic output | Not run | No actual listening or physical SPL calibration claimed; previews supplied for user review. |
| Documentation links | Passed | Relative file references checked before publication. |

## Performance

Not benchmarked. Uses existing WAVs; expensive WHIS rendering is not repeated. Processing existing full-song copies is a separate offline operation.

## Limitations and follow-up

Confirm recognizable music through user listening at a comfortable fixed playback setting. The stronger profile remains quieter by design. Wait for source/finalization logs and check the final JSON. Digital scaling does not establish safe acoustic output, clinical equivalence or public music rights. Only authored Markdown is published; audio/private names remain local.

## Rollback

Remove this task's preparation/finalizer scripts and documentation edits if desired. Review new listening copies separately; originals and raw model exports require no restoration. Do not delete sources or stop the original render as part of rollback. Use a follow-up documentation commit for published changes.
