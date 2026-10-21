# Hearing Notion feature catalog

Last reviewed: 2026-10-20 (America/Mexico_City).

Use this page to review app contents, find implementation details and trace feature changes. This initial inventory is reconstructed from current source, scene configuration and project notes; it is not a claim that all features were added or tested today. Detailed modification records start in [Modification history](Changes/README.md).

**Status meanings:** Implemented means code/assets exist; Partial means only part of the intended experience exists; Planned means no working module is claimed. Verification is recorded separately. No Unity Play Mode/device verification by the agent is recorded for the features below. Earlier user feedback confirmed some UI improvements but also reported questionnaire-loading and animation issues; later fixes still need runtime confirmation.

## Inventory

| ID | Feature and entry point | Implementation | Verification and limits | Last updated |
| --- | --- | --- | --- | --- |
| F-001 | [Home and navigation](#f-001-home-and-navigation): Main scene | Implemented | Source/scene checks previously recorded; full interaction check pending | 2026-10-19 |
| F-002 | [Responsive, readable UI](#f-002-responsive-readable-ui): all screens | Implemented | User reported improved fitting; full portrait/landscape regression pending | 2026-10-19 inventory |
| F-003 | [Exposure Explorer](#f-003-exposure-explorer): home or guided journey | Implemented | Compilation/static checks recorded; runtime interactions pending | 2026-10-19 inventory |
| F-004 | [Spanish HNAI questionnaire](#f-004-spanish-hnai-questionnaire): Conciencia auditiva | Implemented prototype | Loading fix and responses need Play Mode confirmation; no scoring/research administration | 2026-10-19 |
| F-005 | [Personalized Takeaways](#f-005-personalized-takeaways): home or Continue | Partial | Selected activity summary implemented; knowledge outcomes and habit selection pending | 2026-10-19 inventory |
| F-006 | [Visitor session and reset](#f-006-visitor-session-and-reset): Explorer/Takeaways reset | Implemented | Reset/re-entry regression pending; memory only | 2026-10-19 inventory |
| F-007 | [Theme and artwork](#f-007-theme-and-artwork): all screens | Implemented | Images inspected and code compiled; final placement review pending | 2026-10-19 inventory |
| F-008 | [Animated wave sprites](#f-008-animated-wave-sprites): background | Implemented, fix unverified | CanvasRenderer dependency repaired; Play Mode confirmation pending | 2026-10-19 inventory |
| F-009 | [Sound Experience](#f-009-sound-experience): home/Explorer; offline MATLAB authoring | Partial | MATLAB reference/guard checks passed; no reviewed public audio, acoustic verification, runtime DSP or playback | 2026-10-20 |
| F-010 | [Hearing Health and sources](#f-010-hearing-health-and-sources): home | Partial | Introductory panels; full lessons/reference browsing pending | 2026-10-19 |
| F-011 | [Public knowledge check and research mode](#f-011-public-knowledge-check-and-research-mode) | Planned, foundations only | Separate public check, approved consent, scoring, YANS and export pending | 2026-10-19 inventory |
| F-012 | [Noise Meter](#f-012-noise-meter): guided information screen; disabled home card | Partial; measurement deferred | Informational stage implemented; no microphone measurement/calibration | 2026-10-19 |
| F-013 | [Music Lab](#f-013-music-lab) | Planned, future | No functioning laboratory | 2026-10-19 inventory |
| F-014 | [Bilingual controls and settings](#f-014-bilingual-controls-and-settings) | Partial content; settings planned | Spanish HNAI and mostly English modules; no complete language/settings UI | 2026-10-19 inventory |
| F-015 | [Guided screen introductions](#f-015-guided-screen-introductions): Start guided experience | Implemented | Route checks passed; popup interaction/layout verification pending | 2026-10-19 |
| F-016 | [Local sound-source assignment](#f-016-local-sound-source-assignment): Explorer activity details | Implemented | Editor/Windows code compiles; format/catalog tests pass; picker, persistence and UI tests pending | 2026-10-19 |
| F-017 | [Flappy Cloud attention game](#f-017-flappy-cloud-attention-game): Welcome/Home | Partial: playable silent game and reserved noise slot | Model checks and Editor/Windows compilation passed; Unity gameplay/layout verification pending; no noise playback/comparison | 2026-10-19 |

## Feature details

### F-001 Home and navigation

Main.unity uses app-owned panels adapted from Menu Template 1. Home opens modules, Conciencia auditiva is the first option, Back uses navigation history, and the guided flow now proceeds through HNAI, Exposure, Sound, Health recommendations, an informational Noise Meter stage, and Research & Resources. HNAI must be completed before guided continuation; the final stage returns Home. The 5–8-minute target has not been usability-tested. Source: AppManager, NavigationManager, ScreenView in Assets/_HearingNotion/Scripts. See [Home scene](HomeScene.md) and [Architecture](AppArchitecture.md).

### F-002 Responsive, readable UI

Landscape home uses two columns and portrait uses one. Expand scaling, large typography and growing text blocks support small screens and long descriptions. Module content scrolls; outer navigation stays outside the scroll areas. Source: ResponsiveScreenLayout and ReadableTextHeight. Keyboard/device accessibility review remains pending. See [Home scene](HomeScene.md).

### F-003 Exposure Explorer

Three category filters expose 21 source-mapped activity records (18 annex soundscapes plus three chart-only labels), with overlapping category memberships and Spanish details. Visitors open details, inspect classification/source notes, add/remove activities, assign a local WAV/OGG/MP3 per activity and pass the selected activity/filename to Sound Experience. Tips and selections do not quantify acoustic exposure or individual risk. Source: ExposureManager and ScriptableObjects/Activities under Assets/_HearingNotion. See [Explorer details and checks](ExposureExplorer.md) and [soundscape catalog/import guide](SoundscapeCatalog.md).

### F-004 Spanish HNAI questionnaire

The 22 supplied Spanish statements use the confirmed five-point agreement scale. Visitors select/revise answers, navigate Anterior/Siguiente, complete all items with Finalizar and review responses. Answers remain local draft state for the visit. No score, clinical result or export is produced. In guided mode HNAI is first; Finalizar completes the questionnaire and enables the outer Continuar button to open Exposure Explorer. The controller loads Resources/Questionnaires/HNAI.es.json and has startup recovery. This full instrument prototype is separate from a future short public quiz and consented research administration. Source: AwarenessCheckManager and AppSession. See [Spanish questionnaire](SpanishQuestionnaire.md).

### F-005 Personalized Takeaways

Displays selected activity names and suggestions, supports an empty state and links back to Explorer or visitor reset. Knowledge outcomes, individualized hearing-risk results and habit tracking are not implemented. Source: ExposureManager.RefreshTakeaways and AppSession. See [Explorer details](ExposureExplorer.md).

### F-006 Visitor session and reset

In-memory state includes activity selections, sound context and draft HNAI answers/completion. Reset replaces the session and triggers navigation/UI reset subscribers. Returning Home preserves the current visit. Visitor state has no disk persistence, account, automatic analytics or remote participant storage. The separately authored local audio library persists across visits; it contains content assignments, not participant answers. Source: SessionManager, AppSession and module reset subscriptions. See [Architecture](AppArchitecture.md).

### F-007 Theme and artwork

Warm near-white backgrounds, white cards with light borders, yellow primary actions, soft-yellow takeaways and gold selections retain the supplied visual identity while reducing large yellow blocks. Shared button hover/pressed/disabled states apply to home, runtime activity controls, questionnaire controls and modal confirmation. A new transparent isolated headphone illustration replaces the tiny composite header; the static background texture is reduced to 16% opacity. Source: AppTheme and AppArtwork; headphones-hero-v2.png in Resources/Artwork. See [Artwork and prompts](Artwork.md) and [visual refresh](VisualRefresh.md). Code compiles and the image alpha was checked; actual Unity placement remains unverified.

### F-008 Animated wave sprites

Each traveling contour now fades smoothly to transparent across both outer 35% sections, with vertex-interpolated opacity. This removes the hard leading/trailing tips in either travel direction, including paused waves. Temporal fades remain active. Source compilation passed; Unity visual review remains pending. See [soft wave ends](Changes/2026-10-19-011-soft-wave-ends.md).

The previous low-opacity fixed-position sprite drift has been replaced by two procedural 2D UI wave bands. Each band traverses the screen in 10 seconds, rests 4 seconds and fades at entry/exit; the second band starts 7 seconds apart. Initial time is set to 2.5 seconds so a pass is visible on entry. No wave image import is required. AmbientWaveAnimation updates TravelingWaveGraphic with unscaled time; inactive screens do not update, and unfocused standalone players pause. A home button labeled Ondas: activas/pausadas freezes both bands into static contours for the current app session. Controls/header remain still and decorative graphics do not intercept input. Pure timing tests and compilation passed, but the user-reported Unity visibility issue is not yet confirmed resolved in Play Mode. See [visual refresh](VisualRefresh.md).

Wave graphics now explicitly require RectTransform/CanvasRenderer, create the renderer before the graphic, and repair missing renderers during initialization and activation. This addresses the reported clipping exception; Unity runtime confirmation is pending. See [renderer fix report](Changes/2026-10-19-010-wave-canvasrenderer-fix.md).

### F-009 Sound Experience

Offline authoring now has a single MATLAB entry point, Tools/Audio/run_whis.m: choose audio, enter the seven thresholds/compression and modeled-level assumptions, and select an output parent folder. It saves the processed WAV/reference/record to a new folder without playback, or accepts three arguments for scripted use. Interactive values are explicitly illustrative and modeled-only. Dialog interaction still needs manual verification. See [launcher report](Changes/2026-10-20-003-whis-audio-launcher.md).

Explorer passes the active activity ID and the destination displays its description, any assigned local filename and an explicit playback-pending message. Protection/hearing-loss/tinnitus comparisons, transport controls, reviewed audio assets and safety processing are not implemented. See [Architecture](AppArchitecture.md) and [Explorer checks](ExposureExplorer.md).

WHIS-DTVF is the selected hearing-loss authoring method. An offline MATLAB wrapper calls pinned WHIS v302/GCFB v234 reference code with explicit seven-point dB HL, compression health and calibration assumptions. It saves review-pending source/processed pairs and local processing metadata, handles mono/stereo without autoplay, and rejects unsupported input, clipping and overwrites. Reference checkouts/output are local and ignored. MATLAB numerical checks and their actual status are recorded in the [report](Changes/2026-10-20-002-whis-dtvf-offline-processing.md); this does not establish perceptual/device validation or Unity playback. See [steps, sources and use](WHIS.md).

### F-010 Hearing Health and sources

Navigation and introductory panels describe the five educational themes and research background. Health now includes brief recommendations for comfortable volume, quiet breaks, distance from speakers and hearing protection. Full topic content, source cards and browsing interactions remain pending. EducationalTopicDefinition provides a content schema. See [Architecture](AppArchitecture.md).

### F-011 Public knowledge check and research mode

Planned as separate experiences: a short educational quiz and full approved research instruments. Existing route guards, consent fields and questionnaire definitions are foundations only. No complete consent UI, formal research administration, YANS content, approved scoring or export exists. HNAI draft interaction in F-004 does not establish these capabilities. See [Architecture](AppArchitecture.md) and [Spanish questionnaire](SpanishQuestionnaire.md).

### F-012 Noise Meter

The home card remains disabled. Guided mode now includes an informational coming-later screen with its own introduction and Continue control. Microphone acquisition, RMS/weighting, calibration and qualified estimated readings are deferred. No calibrated sound levels are displayed. See [Architecture](AppArchitecture.md).

### F-013 Music Lab

Future music-perception/DSP research module; route reserved and unavailable. No processing pipeline or interactive laboratory is implemented. See [Architecture](AppArchitecture.md).

### F-014 Bilingual controls and settings

Spanish HNAI, Spanish Explorer activity details/import controls and bilingual-capable content fields exist; other UI remains mixed English/Spanish. Home now exposes a session-wide wave pause/resume button. A complete EN/ES language switch, translation catalog, settings screen and persistent accessibility preferences remain pending. See [Architecture](AppArchitecture.md).

### F-015 Guided screen introductions

Six Spanish popups briefly explain the purpose, controls and limitations of each guided stage. Each appears once per stage per guided run; Back does not repeat a dismissed introduction, and restarting the journey/reset allows them again. Entendido or Escape dismisses the modal. The popup blocks underlying controls and focuses its dismiss button. Free exploration does not show these popups. Source: GuidedJourney and GuidedExperienceController; see [Guided experience](GuidedExperience.md). The Noise Meter remains informational and sound playback remains pending. Fixed a user-reported CanvasGroup MissingComponentException by using a Unity-aware null check before adding the component. Popup rendering, keyboard/touch behavior and this runtime fix still require Unity verification.

### F-016 Local sound-source assignment

Each activity can receive a local WAV, OGG or MP3 (50 MB limit). The Editor file picker, Windows native dialog or local-path fallback assigns a copied file to that stable activity ID. A local versioned manifest and copied content persist across app restarts and visitor reset; reimport replaces only the activity mapping. Imported files are unreviewed, do not autoplay, are not decoded/played by this feature and are never uploaded to GitHub. Basic header checks do not prove complete audio validity or licensing/safety approval. Replacement retains old files; cleanup UI is pending. Source: LocalSoundSourceLibrary, LocalAudioFilePicker, SoundSourceImportRules and ExposureManager. See [catalog, storage and verification](SoundscapeCatalog.md).

### F-017 Flappy Cloud attention game

New Flappy Cloud cards on Welcome and Home open a single-scene game adapted from the local Infinite Runner Engine example. Tap/click the sky, press Space or use Subir to flap through scrolling penguin gates. Silent attempts end on collision or at 30 seconds; score/time feedback, restart, pause/resume and Home are available. Focus loss pauses the run. Course generation repeats on restart and a three-gate pool is reused. Leaving the screen or resetting the visitor clears the attempt. No result persistence/export, audio or causal noise-effect interpretation is provided. Con ruido: pendiente is disabled; Settings.DistractionNoise is a reserved authoring slot and remains unused even if assigned. The guided route is unchanged. See [game guide](FlappyCloud.md) and [report](Changes/2026-10-19-012-flappy-cloud-game.md).

## Feature change history

Future feature changes append an entry here and update the current inventory/details. Use stable IDs; keep removed/deprecated entries with their status. Every entry links its detailed modification report.

| Date | Affected IDs | Change | Report |
| --- | --- | --- | --- |
| 2026-10-19 | F-001–F-014 | Initial inventory from existing implementation; no new runtime features added | [2026-10-19-004](Changes/2026-10-19-004-feature-documentation.md) |

| 2026-10-19 | F-001, F-004, F-010, F-012, F-015 | Reorder guided journey, require HNAI completion, add screen introductions and an informational meter stage | [2026-10-19-006](Changes/2026-10-19-006-guided-journey-and-popups.md) |

| 2026-10-19 | F-015 | Fix missing CanvasGroup handling and defer seen-state until popup opens | [2026-10-19-007](Changes/2026-10-19-007-guided-popup-canvasgroup-fix.md) |

| 2026-10-19 | F-003, F-006, F-009, F-014, F-016 | Map annex/chart activities, preserve multi-category contexts and add local per-activity audio assignment | [2026-10-19-008](Changes/2026-10-19-008-annex-catalog-and-audio-import.md) |

| 2026-10-19 | F-002, F-007, F-008, F-014 | Replace faint sprite drift with traveling wave geometry, refresh cards/palette and headphone artwork, add home motion controls | [2026-10-19-009](Changes/2026-10-19-009-traveling-waves-and-visual-refresh.md) |

| 2026-10-19 | F-008 | Explicitly create and require the wave CanvasRenderer, repair reused objects before clipping registration | [2026-10-19-010](Changes/2026-10-19-010-wave-canvasrenderer-fix.md) |

| 2026-10-19 | F-008 | Blend leading and trailing contour ends to transparent | [2026-10-19-011](Changes/2026-10-19-011-soft-wave-ends.md) |

| 2026-10-19 | F-001, F-002, F-006, F-017 | Add optional Flappy Cloud silent practice game, seven-card layout and reserved distraction-noise slot | [2026-10-19-012](Changes/2026-10-19-012-flappy-cloud-game.md) |
| 2026-10-20 | F-009 | Select WHIS-DTVF and add offline reference MATLAB authoring with explicit profile/level assumptions and review records; Unity playback remains pending | [2026-10-20-002](Changes/2026-10-20-002-whis-dtvf-offline-processing.md) |
| 2026-10-20 | F-009 | Add one-entry-point MATLAB audio/settings/output launcher with scripted use | [2026-10-20-003](Changes/2026-10-20-003-whis-audio-launcher.md) |
