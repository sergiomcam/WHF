# Modification report — WHIS-DTVF offline processing

- Report ID: 2026-10-20-002
- Date: 2026-10-20 (America/Mexico_City)
- Type: feature / tools / documentation

## Request and resulting behavior

Adopt WHIS-DTVF following the sourced comparison of hearing-loss simulation methods. Added a working offline MATLAB authoring wrapper around the authors' implementation. It requires explicit seven-point hearing levels, compression health, modeled source SPL, calibration mapping/status and provenance notes. It saves a normalized reference/processed pair and local review record without playing audio. Unity Sound Experience remains partial: no runtime DSP, reviewed sound set, playback or safety transport is claimed. The original supplied script is unchanged.

## Modifications

| File or asset | Change and purpose |
| --- | --- |
| Tools/Audio/setup_whis.m | Resolve reference paths, verify exact clean upstream revisions and Signal Processing Toolbox availability. |
| Tools/Audio/process_whis_dtvf.m | DTVF-only reference call; mono/stereo common gain reference, silent-channel bypass, input/clipping/overwrite rejection and local 24-bit WAV/MAT output. |
| Tools/Audio/test_whis_dtvf.m | Synthetic numerical reference comparison and operational guard checks; no playback. |
| Tools/ThirdParty/WHIS and Tools/ThirdParty/gammachirp-filterbank | Local, ignored upstream checkouts with original licenses and source. No vendor code modifications. |
| .gitignore | Exclude reference checkouts and generated Tools/Audio/Output artifacts. |
| Docs/WHIS.md | Evidence scope, citations, pinned versions, installation, each processing step, explicit example assumptions and remaining review requirements. |
| Docs/AppArchitecture.md | Record offline authoring boundary, separate from planned Unity managers. |
| Docs/FEATURES.md | Update F-009 status, behavior, verification limits and history. |
| Docs/README.md | Link WHIS guide. |
| AGENTS.md | Record chosen authoring convention, local-only outputs and explicit modeling/calibration requirements. |
| Docs/Changes/README.md and this report | Index and describe this coherent task. |
| Tools/Audio/whis-validation.log | Local MATLAB execution evidence; not included in documentation publication. |

## Decisions and implications

Use the published reference algorithm rather than a custom approximation or extra smearing stage. WHIS commit `33f5c29f7f2aeb74d0a8b528965f4ba238451921` calls GCFB v234; filterbank commit `fa8e5c10d3a40da524b24f2469b343617d59ca1b` is pinned. Root licenses are CC0-1.0 and Apache-2.0 respectively; original notices remain. MATLAB R2023b and Signal Processing Toolbox are local authoring dependencies only. No Unity dependency, package, build setting, scene, prefab, asset GUID or C# source changes. No scene regeneration.

The reference manual audiogram requires nonnegative hearing levels at seven fixed frequencies. The wrapper rejects old signed attenuation gains and unsupported grids instead of silently reinterpreting them. Alpha is independent of audiogram and can be adjusted internally by GCFB; effective parameters are saved. Stereo is independent-channel processing using one profile, with source SPL offsets derived from channel RMS relative to mean channel power; it is not validated binaural simulation. No implicit resampling, output normalization, limiting or latency compensation is added.

Output schemaVersion=1 is a new local authoring MAT record, not a visitor/research schema. Source and processed WAV plus metadata go only to an explicitly chosen new directory; recommended output location is ignored Tools/Audio/Output. No participant input, private source filenames/paths or audio is published. Local source-assignment persistence and visitor reset are unchanged. The test fixtures and example profile are fictional, not research observations. Review-pending status remains even if the caller declares measured calibration.

Scientific provenance: [Irino 2023](https://doi.org/10.1109/ACCESS.2023.3298673), [Irino et al. 2024](https://www.isca-archive.org/interspeech_2024/irino24_interspeech.pdf), [WHIS authors' code](https://github.com/AMLAB-Wakayama/WHIS) and [filterbank authors' code](https://github.com/AMLAB-Wakayama/gammachirp-filterbank). The guide maps each step to these sources and distinguishes published evaluation from project engineering choices. No claim of individual clinical fidelity or WHO endorsement is added.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| Unity versions | passed | ProjectVersion.txt: 2022.3.12f1; manifest: TMP 3.0.6, Test Framework 1.1.33. Dependencies unchanged. |
| Reference source/path/revision | passed | Both Git revisions recorded above; clean upstream worktrees after MATLAB execution. Current WHIS source uses GCFBv234 and explicitly selects DTVF. |
| First MATLAB launch in sandbox | failed | MATLAB could not create its preferences folder. Retried with approved access to normal preferences/license. |
| MATLAB R2023b execution | passed | `matlab.exe -batch "addpath('Tools/Audio'); test_whis_dtvf"`; exit 0, ALL WHIS WRAPPER CHECKS PASSED in Tools/Audio/whis-validation.log. |
| Mono numerical parity | passed | Synthetic 0.2 s signal, 48 kHz; exported source and processed audio match independent direct WHISv30_Batch call within 2^-23 sample amplitude. |
| Stereo adaptation | passed | Unequal channel source RMS ratio preserved within test tolerance; silent output channel stays exactly zero. |
| Operational rejection | passed | Negative hearing levels, wrong frequency grid, existing output directory, clipping, entirely silent input and 44.1 kHz input rejected. Clipping produces no output directory. |
| Documentation links and remote baseline | passed | Relative file targets in the changed documentation resolve. Existing remote documentation was compared against local content; only task-specific differences were found. |
| C# compilation / questionnaire / scene checks | not run | No affected C#, questionnaire JSON or serialized Unity asset changes. |
| Acoustic calibration / playback / listening | not run | Tests are synthetic numerical checks only; no audio plays and no output-device claims are made. |
| Unity Play Mode, portrait/landscape and device review | not run | Offline authoring only; runtime audio integration remains unimplemented. |

Documentation link checks and publication verification are completed as part of delivery. Only this task's changed AGENTS.md/project Markdown is eligible for publication; source, logs, checkouts and audio remain local. GitHub connector publication does not synchronize the local Git history.

## Performance

Not measured as an optimization study. Reference timing messages are MATLAB execution diagnostics, not a desktop audio performance baseline or real-time readiness claim. No speedup is claimed.

## Limitations and follow-up

No actual source audio or user hearing profile was chosen, processed or approved. Example alpha and levels are explicitly assumptions. Acoustic calibration, licensing/content review, binaural/asymmetric-profile work, timing review, fades, gain/safety controls and actual Unity transport remain pending. Numerical parity confirms use of the reference code; it does not repeat perceptual validation. The test fixture covers 48 kHz; the supported 24 kHz branch has not been independently exercised. An I/O failure during final writes can leave a partial output directory; existing directories are refused on rerun.

## Rollback

Remove only this task's Tools/Audio MATLAB files/log and chosen generated test outputs, and reverse the task-specific .gitignore and documentation additions. Remove the two newly downloaded checkouts only if no later work depends on them. Preserve the original MATLAB script, Unity content and unrelated local edits. If reversing public documentation, make a new documentation commit based on the then-current remote head; do not reset or force-push. There is no local source commit or backup claimed.
