# Soundscape catalog and local audio assignment

The Explorer uses the supplied soundscape annex (table on pages 1–2, references on pages 3–5) plus the activity labels in the demographic exposure figure. It contains 21 independent records: 18 annex soundscapes and three chart-only labels. Spanish titles are used in the Explorer; the annex name is retained as metadata. No group percentages were estimated from bar heights, and no annex sound-level ranges are presented as measurements or playback targets.

## Activities and classification

| Stable ID | Display title | Annex soundscape | Categories | Classification basis |
| --- | --- | --- | --- | --- |
| airport | Aeropuertos | Airport | Ambiental | Explicit annex category |
| road-traffic | Tráfico de coches | Car Traffic | Ambiental | Explicit annex category |
| carpentry | Carpintería | Carpentry | Laboral | Occupational workshop context in annex |
| children-party | Fiestas de niños | Children’s Party | Recreativo | Explicit annex category |
| classical-concert | Conciertos de música clásica | Concert Hall | Recreativo, Laboral | Both perspectives in annex |
| conference | Conferencias | Conference | Ambiental, Laboral | Both categories in annex |
| construction | Construcción | Construction | Laboral, Ambiental | Both categories in annex |
| dentist | Consultorios de dentistas | Dentist | Laboral | Explicit annex category; audio perspective is the patient chair |
| hairdryer | Secadoras de cabello | Hairdryer | Ambiental, Laboral | Both categories in annex |
| urban-ambience | Paisaje urbano | Urban ambience | Ambiental | Explicit annex category |
| motorcycle-road | Tráfico de motocicletas | Motorcycle road | Ambiental | Explicit annex category |
| nightclubs | Clubes nocturnos | Nightclub | Recreativo, Ambiental, Laboral | All three perspectives in annex |
| car-races | Pistas de carreras | Car races | Recreativo | Explicit annex category |
| rock-concert | Conciertos de rock | Rock concert | Recreativo | Contextual inference; no explicit category label in that row |
| stadium | Eventos deportivos (estadio) | Stadium | Recreativo | Explicit annex category |
| shooting-range | Zonas de tiros | Shooting Camp | Recreativo, Laboral | Provisional context: participants versus staff; annex row does not specify categories |
| school | Patios de escuelas | School Garden | Ambiental | Contextual inference; annex row does not specify category |
| snores | Personas que roncan | Snores | Ambiental | Contextual inference; annex row does not specify category |
| carpentry-workshops | Talleres de carpintería | No separate annex row | Laboral | Chart-only label; provisional; related to Carpentry but independent audio assignment |
| construction-workshops | Talleres de construcción | No separate annex row | Laboral | Chart-only label; provisional; related to Construction but independent audio assignment |
| edm-concert | Conciertos EDM | No annex row | Recreativo | Chart-only label; provisional; no authored mix description supplied |

Overlapping activities appear under multiple filters but retain one stable ID and one audio assignment. Current filter counts are Ambiental 10, Recreativo 8 and Laboral 10; their sum exceeds 21 because categories overlap. Source and classification notes are visible in activity details. Inferred categories can be revised without changing IDs or audio mappings.

Descriptions summarize the annex's scene and mixing design, rather than copying its medical assertions or numeric acoustic ranges. Prevention tips retain the existing general WHO safe-listening principles. Older generic sample activity assets are preserved on disk but excluded from the active catalog, avoiding deletion of project material.

## Assigning audio

1. Press Play, open Exposure Explorer and choose a category.
2. Open an activity and scroll to its details.
3. Choose **Asignar archivo de audio**. In Unity Editor it opens the editor file selector; in a Windows standalone player it uses the Windows file dialog.
4. Select WAV, OGG or MP3, up to 50 MB. The importer checks size, extension and basic container/header signatures, then copies the file to the local content library and assigns it to that activity.
5. If a native picker is unavailable, or if you prefer, use **Usar una ruta local**, paste the complete audio-file path, then **Importar desde ruta**. This fallback requires an accessible local filesystem; it is not a mobile/WebGL file picker.
6. The activity displays its assigned filename and review-pending status. Reimporting replaces the assignment for that activity while leaving other activities unchanged. Cancellation does not change an assignment.
7. **Explorar este sonido** passes the activity and assigned filename to Sound Experience. Playback is still unimplemented. Nothing plays automatically.

Import is local file assignment, not a network upload. It does not certify licensing, content, normalization, peak/loudness safety or complete decoding. Header checks reject obvious mismatches but cannot establish that a file is a fully valid playable recording. All imported records start with PlaybackReviewed=false; review and audio playback/safety work remain separate requirements.

## Storage and ownership

The app uses `Application.persistentDataPath/SoundSources/` for authored sound files and a versioned manifest. Copied files use generated names; the manifest stores activity ID, original filename, stored filename, import time and review state. Source paths are not stored. Manifest writes use a temporary file and replacement/backup where an existing file is present.

The library persists across app restarts and visitor reset. It is content configuration, not participant questionnaire data. Visitor reset clears selections, answers and the path-input UI while retaining audio assignments. Replaced/orphan files are retained rather than silently deleted; library cleanup/removal UI is not yet implemented. A failed manifest write restores the previous in-memory assignment, but its copied file may remain unassigned. Local filenames may contain private information and must not be included in public reports or telemetry.

No cloud upload, GitHub audio publication, microphone permission, automatic playback or participant-data persistence was added. Persistent library behavior and native dialogs require target-device testing.

## Implementation and checks

- Resources/ActivityCatalog.asset contains the 21 ActivityDefinition references and is loaded by ExposureManager at startup. This also updates an older open scene that still has the nine original Inspector references. Main's fallback references and the scene generator are aligned with the active catalog.
- ActivityDefinition retains its original Category field for compatibility and adds Categories plus provenance/classification notes. MatchesCategory uses the category array when present.
- LocalSoundSourceLibrary owns asynchronous local file copy and the persistent manifest. LocalAudioFilePicker provides Editor/Windows selection; the Explorer provides the path fallback. SoundSourceImportRules holds independently testable validation rules.
- Tools/build_annex_catalog.py reconstructs the catalog/assets from the reviewed mapping. It overwrites catalog activity content; do not rerun over manually edited records without preserving changes. Existing GUIDs are retained.
- Tools/Tests/SoundSourceImportChecks.cs tests header/extension/size rules and stable IDs. Tools/Tests/validate_annex_catalog.py checks expected records, overlapping categories and references. Neither test proves native file-dialog or Unity rendering behavior.

In Play Mode, verify all filters, all 21 records, classification notes, multi-category selections, file-picker cancellation, valid import, invalid/oversized files, replacement, app restart, visitor reset and Sound Experience context. Test portrait/landscape wrapping and scrolling. Then verify the Windows player dialog and local storage on the demonstration computer.
