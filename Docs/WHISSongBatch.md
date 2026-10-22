# WHO Figure 1 exposure-labeled song exports

Updated: 2026-10-21 (America/Mexico_City).

## Approved illustration

The researcher selected flat illustrative hearing profiles and requested WHIS compression health alpha 0.5. WHO's February 2017 monograph, Figure 1 (PDF page 11, printed page 9), plots population-median noise-induced permanent threshold shift averaged over 1, 2, 3 and 4 kHz. It is not a frequency-specific audiogram or a recording-level prescription.

Approximate visual readings at 20/30 years are 13.5/15.5 dB HL for 95 dBA LEX8h, and 23.25/26.25 dB HL for 100 dBA LEX8h. A linear midpoint gives 14.5 and 24.75 dB HL at 25 years. These are visually estimated/interpolated chart values, not exact calculations from ISO 1999:2013. Applying each value uniformly at 125, 250, 500, 1000, 2000, 4000 and 8000 Hz is the explicit, user-approved illustrative simplification. No age-related loss, sex-specific norm or individual prognosis is added.

[Official WHO-hosted monograph](https://cdn.who.int/media/docs/default-source/documents/health-topics/deafness-and-hearing-loss/monograph_on_determination_of_risk_of_hl_due_to_exposure_to_recreational_sounds.pdf) supplies the chart context. See [WHIS method and primary evidence](WHIS.md) for simulator scope and reference pins. The exposure label 95/100 dBA must never become a listening-volume instruction.

## Batch implementation

- process_whis_library reads the five original M4A songs in the user-designated Hearing Loss folder and refuses preexisting destination folders.
- Two sibling folders are named WHIS_25y_95dBA_Lex8h_FLAT_APPROX and WHIS_25y_100dBA_Lex8h_FLAT_APPROX. Each is intended to receive five processed stereo WAVs with individual MAT records, a summary CSV, batch-profile MAT and explanatory README. Originals are preserved.
- process_whis_song explicitly resamples the 44.1 kHz stereo sources to 24 kHz using MATLAB resample before reference WHIS processing. Export is 24-bit stereo WAV with complete resampled song duration.
- Full songs exceed the practical memory budget of the reference 100-channel filterbank on this 16 GB system. Ten-second cores with one second of surrounding source context are processed per channel; only core samples are assembled. Segment origins align with whole-second boundaries. This engineering adaptation bounds memory but is not a published/independently perceptually validated whole-song WHIS mode.
- Each segment uses its RMS-relative modeled source SPL so that the same whole-song gain reference and stereo level differences are retained. Modeled source SPL is 60 dB; calibration mapping is 90 dB, both illustrative and physically uncalibrated. Historical exposure labels are independent of these presentation/model settings.
- Pinned WHISv302 DTVF and GCFBv234 are called without source changes. Requested alpha is 0.5; the reference may adjust effective compression to fit the supplied hearing levels. Effective hearing-loss parameters are recorded per segment/channel.
- Outputs are rejected for nonfinite values or digital clipping. No independent wet normalization, playback, Unity import or music redistribution approval is supplied. Core assembly retains source duration rather than exporting the artificial final context/filter tail as extra music.

## Validation and current status

Synthetic stereo tests passed one-segment agreement against the existing process_whis_dtvf wrapper within 24-bit export quantization. A two-core stationary synthetic fixture with 0.25-second context had RMS-relative difference rounded to 0.000000 against its single-segment reference. That fixture does not establish equivalence for all dynamic music or perceptual seam quality; public use still needs listening review.

The full ten-export batch is in progress. Final sample-rate/channel/duration/peak and original-file hash verification are pending. Runtime progress is local in the ignored Tools/Audio/whis-song-batch.log. Do not label the song library complete until all ten outputs and provenance files have been checked. No audio or private song filenames are included in GitHub documentation publication.

The first full song completed and its WAV was inspected: 24 kHz, stereo, 24-bit, original duration retained, peak below digital clipping. All five original hashes were checked unchanged at that point. The remaining batch continues. A one-time verify_whis_library.py --wait helper checks all ten WAV headers/durations/peaks, sidecars and original hashes after the batch completion marker, then writes Tools/Audio/Output/whis-song-verification.json. The verifier is running; its final result is pending. It is a finite local batch check, not a recurring automation.

## Listening-level correction (2026-10-21)

A user reported no music in the exports. Inspection found nonzero, temporally music-correlated signals at extremely low digital levels: sample passages around −71/−81 dBFS RMS. The modeled source/calibration mapping had been retained in the WAVs; checking only duration/peaks/clipping failed to flag their practical audibility. Technical renders and original M4As remain unchanged.

Tools/Audio/prepare_whis_listening.m creates a separate WHIS_Listening_Comparisons folder beside the technical folders, with Original_reference, 25y_95dBA and 25y_100dBA subfolders. For each song, a single presentation gain places its normalized reference peak at −6 dBFS. Exactly that gain is applied to both model variants; no variant is independently normalized or loudness matched. Each copy has a gain-record MAT. Reference is reconstructed from the explicitly resampled original using the same model source-peak relationship. This is a per-song listening presentation, not physical calibration or an across-song exposure comparison.

Eight available processed copies were created and checked against technical samples times the recorded common gain, within 24-bit export quantization. A sampled comparison measured RMS levels approximately −18/−33/−42 dBFS for reference/95/100. Their 50 ms RMS envelope correlations with the reference were .9624/.9499; this supports retained temporal content but does not replace actual listening review. Short 15-second comparison previews are local only. No audio played automatically.

The last two technical renders remain in progress. A finite finish_whis_listening.py helper waits for the source batch completion marker, reruns the idempotent preparation, and requires ten verified listening copies. It writes Tools/Audio/Output/whis-listening-status.json; final completion remains pending. Start at a low comfortable device volume and compare using the same setting; digital headroom is not guaranteed acoustic safety.
