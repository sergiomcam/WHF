# Modification report — annex activity catalog and local audio assignment

- Report ID: 2026-10-19-008
- Date: 2026-10-19 (America/Mexico_City)
- Type: feature / content

## Request and resulting behavior

The user requested Exposure Explorer activities/classification from the supplied soundscape annex and demographic figure, plus an option to upload a representative sound file for each source. Implemented a 21-record catalog, overlapping category filters and local per-activity audio assignment. Import means a local copy/configuration, not cloud upload. No playback is introduced.

## Modifications

| File or asset | Change and purpose |
| --- | --- |
| Assets/_HearingNotion/Scripts/Exposure/ActivityDefinition.cs | Added multi-category memberships and annex/classification provenance while preserving the old single Category fallback. |
| Assets/_HearingNotion/Scripts/Exposure/ActivityCatalog.cs; Resources/ActivityCatalog.asset | Added authoritative 21-record catalog, loadable even from an older scene instance. |
| Assets/_HearingNotion/ScriptableObjects/Activities/*.asset | Created/updated 21 active annex/chart records with Spanish titles, scene descriptions and provenance; preserved existing GUIDs and retained older inactive sample assets. |
| Assets/_HearingNotion/Scripts/Exposure/ExposureManager.cs | Added catalog loading, multi-category matching, Spanish source details, per-activity import controls, local-path fallback, import status and sound-context filename. Visitor reset clears path UI but keeps authored audio. |
| Assets/_HearingNotion/Scripts/Audio/LocalSoundSourceLibrary.cs | Added asynchronous local file copy and versioned persistent content manifest; assignments remain unreviewed. |
| Assets/_HearingNotion/Scripts/Audio/LocalAudioFilePicker.cs | Added Editor file picker and Windows standalone dialog without a new external dependency. |
| Assets/_HearingNotion/Scripts/Audio/SoundSourceImportRules.cs | Added 50 MB limit, supported extension/basic signature validation and activity-ID validation. |
| Assets/_HearingNotion/Scenes/Main.unity; Tools/build_home_scene.py | Aligned fallback activity references with the authoritative catalog; scene regeneration was not run. |
| Tools/build_annex_catalog.py | Added reproducible reviewed catalog generation; overwrites catalog content when deliberately run. |
| Tools/Tests/SoundSourceImportChecks.cs; Tools/Tests/validate_annex_catalog.py; Tools/Tests/annex_catalog_expected.json | Added import validation and source-mapping/reference checks. |
| New script/content .meta files | Generated missing metadata and preserved existing GUIDs. |
| AGENTS.md; Docs/FEATURES.md; Docs/README.md; Docs/ExposureExplorer.md; Docs/HomeScene.md; Docs/AppArchitecture.md | Updated storage conventions, feature inventory, module behavior and documentation index. |
| Docs/SoundscapeCatalog.md; Docs/Changes/README.md; this report | Added complete classification/import guide and indexed this task. |

## Decisions and implications

The supplied annex has 18 soundscapes. The figure adds distinct carpentry-workshop, construction-workshop and EDM-concert labels; those are retained as three supplementary records without pretending they have annex design entries. Contextual classification is explicitly labeled where the annex has no category. Nightclub appears in all three filters; classical concert, conference, construction and hairdryer preserve overlapping annex contexts. Repeated category appearances share one stable ID and assignment.

Source provenance: user-supplied Soundscapes description and design.pdf (table pages 1–2 and references pages 3–5) and Demographic exposure.png. Read text and visually inspected the table pages. App descriptions paraphrase scene/mix design; they do not copy numeric health claims or convert chart bars into percentages. No raw research input files were copied into the project or public documentation upload.

Authored audio is separate from participant state and persists in Application.persistentDataPath/SoundSources. WAV/OGG/MP3 files are copied locally; manifest records contain filenames, stable activity IDs and import timestamps, not source paths. Basic signatures do not validate complete decoding or licensing. Files remain PlaybackReviewed=false with no automatic playback. Replacing an assignment retains old audio files; no cleanup/removal UI is implemented. Failed manifest writes roll back the in-memory assignment but may leave an unassigned copied file. No cloud service, microphone permission, participant-answer persistence, scoring, packages or build scenes were added.

## Validation

| Check | Result | Evidence or reason |
| --- | --- | --- |
| Annex inspection | Passed | Extracted all five pages; rendered and inspected table pages 1–2 with Poppler. |
| Windows standalone source compilation | Passed | Compiled app with UNITY_STANDALONE_WIN against Unity 2022.3.12f1 assemblies; existing Inspector-field warnings only. |
| Editor source compilation | Passed | Compiled app with UNITY_EDITOR, including the editor picker branch; existing Inspector-field warnings only. |
| Import-rule executable | Passed | Valid WAV/OGG/MP3 signatures, rejected unsupported/spoofed/empty/oversized inputs and invalid activity IDs. |
| Catalog checks | Passed | 21 unique records, 18 annex records, explicit overlapping memberships, activity GUID references and no invented prevalence/levels. |
| Scene/document checks | Passed | Verified activity bindings, local scene references, Markdown links and unique feature IDs before publication. |
| Unity Play Mode / native dialogs / persistence/restart / visual checks | Not run | Requires target Editor/Windows interaction and storage review; checklist is in SoundscapeCatalog.md. |
| GitHub documentation publication | Pending at report preparation | Final response supplies verified publication outcome. Only project-authored documentation is published. |

## Performance

No profiling or performance improvement claim. File copying runs on a background task; manifest/UI updates return to the main thread. Activity rendering remains a small non-virtualized catalog. Imported content uses an explicit 50 MB per-file limit; accumulated storage is not automatically cleaned or quota-managed.

## Limitations and follow-up

Review contextual classifications with the instrument owner. Test the 21 entries, multi-category selection, cancel, import, replacement, invalid/oversized files, missing paths, restart/reset, native dialogs, and responsive scrolling. Non-Windows players have a path fallback where a local filesystem is accessible; no browser/mobile upload adapter is implemented. Audio playback, review approval, normalization, limiting and A/B comparison remain separate work.

## Rollback

Reverse this task's catalog, model, Explorer/import classes and scene fallback changes while preserving existing asset GUIDs, user edits and any later mappings. Do not regenerate Main blindly. Preserve imported content and manifest/backups before manually reverting storage handling; do not silently delete local sound files. Reverse published documentation in a new commit if requested rather than rewriting history.
