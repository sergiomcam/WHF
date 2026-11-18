# Modification report - Integrate 1 kHz preview

- Report ID: 2026-11-17-003
- Date: 2026-11-17 (America/Mexico_City)
- Type: feature / audio

## Request and resulting behavior

Replace the startup 6 kHz example with the generated ten-second 1 kHz-centred noise, retaining the same -12 dB attenuation. User explicitly confirmed preserving the existing 50 ms playback edge fades. Implemented in source and bundled assets; physical playback and updated APK remain pending.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Replace startup source and labels | Assets/_HearingNotion/Scripts/Core/ListeningSetupController.cs | Load bundled AudioClip, copy into an owned processed buffer, keep headroom scaling, 50 ms fades, -12 dB factor, ramp and slider controls. Retire startup external-catalog/6 kHz fallback and web request. |
| Bundle authored audio | Assets/_HearingNotion/Resources/Audio.meta; Assets/_HearingNotion/Resources/Audio/bb_25dB_1kHz.wav; Assets/_HearingNotion/Resources/Audio/bb_25dB_1kHz.wav.meta | New folder/asset GUIDs; mono 24 kHz, ten-second, 16-bit PCM; preloaded Decompress On Load, no importer normalization. Existing asset GUIDs preserved. |
| Update existing native fixture | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Remove obsolete asynchronous request wait, require new preview format and retain -12 dB/slider/Accept checks. |
| Prepare portable source | Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/Core/ListeningSetupController.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Resources/Audio.meta; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Resources/Audio/bb_25dB_1kHz.wav; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Resources/Audio/bb_25dB_1kHz.wav.meta | Synchronize only changed preview source/assets; no APK build or installation claimed. |
| Document behavior and limits | Docs/ListeningSetup.md; Docs/Test.md; Docs/AndroidDeployment.md; Docs/FEATURES.md | Current F-019/F-024 configuration, provenance and verification limits. |
| Record task | Docs/Changes/2026-11-17-003-integrate-1khz-preview.md; Docs/Changes/README.md | Indexed modification record. |

## Decisions and implications

Audio provenance: generated from the supplied ALL_generation.m bb branch; see the preceding generation report. Source is band-limited Gaussian noise, half-power edges 750/1250 Hz; filename 25dB is an authoring preset, not SPL/HL. Original WAV has no fades; runtime adds only the requested existing 50 ms treatment. The startup controller owns/destroys its processed clip and never modifies the shared imported resource. Small static resource removes dependence on an external private path or portable catalog preview. Original 6 kHz media/catalog and source audio remain intact. No changes to multimedia/game gain, source files, device volume, demographic persistence, HNAI, research scoring, scenes, packages or build settings. Resource addition increases build content by approximately 480 kB before packaging. Existing QA skill used; no new recurring workflow identified.

## Validation

| Check | Result | Evidence or reason |
| --- | --- | --- |
| Editor/Windows/Android-symbol runtime compilation and Editor tools | passed | Tools/Tests/run_project_checks.ps1; installed Unity 2022.3.12f1; expected Inspector warnings only. Android-symbol compilation is not an APK build. |
| Existing model/media checks | passed | Same script passed game model and 56 catalog media hashes, 23 aligned sets and 18 mappings. |
| Content/encoding checks | passed | validate_english_content.py preserved original study values, figures, Spanish HNAI and activity text; no known source mojibake. |
| New WAV identity/format | passed | Same generated SHA-256 b13f30bdc4a692ebd0f819767ba84371b0984278df24211185c92cfe745b1f99; mono, 24000 Hz, 240000 samples, 16-bit PCM. |
| Preview math | passed | Scale 24.9756097561 to 0.25 peak; fade 1200 samples per edge; 0.25118864 factor equals -12.0000001 dB; ceiling digital peak 0.01569929, midpoint 0.007849645. Not acoustic measurements. |
| Isolated native review | failed / incomplete | Separate QA project remained at ModeService initialization without fresh runner output. Stopped only that task-owned batch process after bounded startup attempt; open Main Editor preserved. Old Nov 6 COMPLETE output explicitly not used as current evidence. |
| Unity playback/render and physical listening | not run | Native initialization did not reach the changed preview. No audible/safety claim. |
| Android build/install/device | not run | Portable source/assets prepared only; installed phone app unchanged. |

## Performance

Not profiled. Loading occurs on explicit first Play, not per frame; processed clip reused during the visit. No speedup claims.

## Limitations and follow-up

Run the updated native fixture and inspect the popup before demonstration. Test actual comfortable listening and interruption behavior on the target phone after rebuilding. New source retains existing gain preparation and trim, not equal perceived loudness or physical calibration. Legacy portable TinnitusPreview metadata can still describe the former clip but is no longer consumed by startup; not deleted to preserve historical catalog integrity.

## Rollback

Restore the prior startup loader/labels and matching native fixture together, remove only the new Resources/Audio WAV and its new metadata/folder if otherwise empty, and synchronize that reversal to the portable copy. Keep generated standalone source and existing 6 kHz media. Reverse only task-specific documentation paragraphs/history/index if needed; never regenerate Main or clear participant storage.
