# Hearing Notion feature catalog

Last reviewed: 2026-10-19 (America/Mexico_City).

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
| F-008 | [Animated wave sprites](#f-008-animated-wave-sprites): background | Implemented, fix unverified | User reported absent motion; explicit startup fix needs confirmation | 2026-10-19 inventory |
| F-009 | [Sound Experience](#f-009-sound-experience): home/Explorer | Partial | Activity context only; no reviewed audio or playback | 2026-10-19 inventory |
| F-010 | [Hearing Health and sources](#f-010-hearing-health-and-sources): home | Partial | Introductory panels; full lessons/reference browsing pending | 2026-10-19 |
| F-011 | [Public knowledge check and research mode](#f-011-public-knowledge-check-and-research-mode) | Planned, foundations only | Separate public check, approved consent, scoring, YANS and export pending | 2026-10-19 inventory |
| F-012 | [Noise Meter](#f-012-noise-meter): guided information screen; disabled home card | Partial; measurement deferred | Informational stage implemented; no microphone measurement/calibration | 2026-10-19 |
| F-013 | [Music Lab](#f-013-music-lab) | Planned, future | No functioning laboratory | 2026-10-19 inventory |
| F-014 | [Bilingual controls and settings](#f-014-bilingual-controls-and-settings) | Partial content; settings planned | Spanish HNAI and mostly English modules; no complete language/settings UI | 2026-10-19 inventory |
| F-015 | [Guided screen introductions](#f-015-guided-screen-introductions): Start guided experience | Implemented | Route checks passed; popup interaction/layout verification pending | 2026-10-19 |

## Feature details

### F-001 Home and navigation

Main.unity uses app-owned panels adapted from Menu Template 1. Home opens modules, Conciencia auditiva is the first option, Back uses navigation history, and the guided flow now proceeds through HNAI, Exposure, Sound, Health recommendations, an informational Noise Meter stage, and Research & Resources. HNAI must be completed before guided continuation; the final stage returns Home. The 5–8-minute target has not been usability-tested. Source: AppManager, NavigationManager, ScreenView in Assets/_HearingNotion/Scripts. See [Home scene](HomeScene.md) and [Architecture](AppArchitecture.md).

### F-002 Responsive, readable UI

Landscape home uses two columns and portrait uses one. Expand scaling, large typography and growing text blocks support small screens and long descriptions. Module content scrolls; outer navigation stays outside the scroll areas. Source: ResponsiveScreenLayout and ReadableTextHeight. Keyboard/device accessibility review remains pending. See [Home scene](HomeScene.md).

### F-003 Exposure Explorer

Three category filters expose nine activity records. Visitors open details, add/remove activities and pass a selected activity to Sound Experience. Tips and selections do not quantify acoustic exposure or individual risk. Source: ExposureManager and ScriptableObjects/Activities under Assets/_HearingNotion. See [Explorer details and checks](ExposureExplorer.md).

### F-004 Spanish HNAI questionnaire

The 22 supplied Spanish statements use the confirmed five-point agreement scale. Visitors select/revise answers, navigate Anterior/Siguiente, complete all items with Finalizar and review responses. Answers remain local draft state for the visit. No score, clinical result or export is produced. In guided mode HNAI is first; Finalizar completes the questionnaire and enables the outer Continuar button to open Exposure Explorer. The controller loads Resources/Questionnaires/HNAI.es.json and has startup recovery. This full instrument prototype is separate from a future short public quiz and consented research administration. Source: AwarenessCheckManager and AppSession. See [Spanish questionnaire](SpanishQuestionnaire.md).

### F-005 Personalized Takeaways

Displays selected activity names and suggestions, supports an empty state and links back to Explorer or visitor reset. Knowledge outcomes, individualized hearing-risk results and habit tracking are not implemented. Source: ExposureManager.RefreshTakeaways and AppSession. See [Explorer details](ExposureExplorer.md).

### F-006 Visitor session and reset

In-memory state includes activity selections, sound context and draft HNAI answers/completion. Reset replaces the session and triggers navigation/UI reset subscribers. Returning Home preserves the current visit. There is no disk persistence, account, automatic analytics or remote participant storage. Source: SessionManager, AppSession and module reset subscriptions. See [Architecture](AppArchitecture.md).

### F-007 Theme and artwork

White surfaces, charcoal text and yellow/gold controls follow the supplied palette. Generated sound-wave background and headphone/noise header artwork load locally. Decorative images do not receive clicks. Source: AppTheme and AppArtwork; PNGs in Resources/Artwork. See [Artwork and generation prompts](Artwork.md).

### F-008 Animated wave sprites

Two transparent sprite layers drift behind the interface and respond slightly to pointer position. RuntimeArtworkController explicitly initializes them in Play Mode. Current defaults: 48 reference-unit horizontal drift, half as much vertical drift, 18-second cycle and 12-unit pointer parallax; layer opacities are 32% and 24%. Reduced Motion is a per-screen Inspector option, not a persistent settings control. Header and controls remain static. User-reported lack of motion prompted a startup fix; actual motion remains unverified. Source: RuntimeArtworkController, AmbientWaveAnimation and AppArtwork. See [Artwork notes](Artwork.md), whose original animation defaults describe an earlier revision; these values reflect current source.

### F-009 Sound Experience

Explorer passes the active activity ID and the destination displays its description and an explicit audio-pending message. Protection/hearing-loss/tinnitus comparisons, transport controls, reviewed audio assets and safety processing are not implemented. See [Architecture](AppArchitecture.md) and [Explorer checks](ExposureExplorer.md).

### F-010 Hearing Health and sources

Navigation and introductory panels describe the five educational themes and research background. Health now includes brief recommendations for comfortable volume, quiet breaks, distance from speakers and hearing protection. Full topic content, source cards and browsing interactions remain pending. EducationalTopicDefinition provides a content schema. See [Architecture](AppArchitecture.md).

### F-011 Public knowledge check and research mode

Planned as separate experiences: a short educational quiz and full approved research instruments. Existing route guards, consent fields and questionnaire definitions are foundations only. No complete consent UI, formal research administration, YANS content, approved scoring or export exists. HNAI draft interaction in F-004 does not establish these capabilities. See [Architecture](AppArchitecture.md) and [Spanish questionnaire](SpanishQuestionnaire.md).

### F-012 Noise Meter

The home card remains disabled. Guided mode now includes an informational coming-later screen with its own introduction and Continue control. Microphone acquisition, RMS/weighting, calibration and qualified estimated readings are deferred. No calibrated sound levels are displayed. See [Architecture](AppArchitecture.md).

### F-013 Music Lab

Future music-perception/DSP research module; route reserved and unavailable. No processing pipeline or interactive laboratory is implemented. See [Architecture](AppArchitecture.md).

### F-014 Bilingual controls and settings

Spanish HNAI and bilingual-capable content fields exist; most other UI currently uses English. A complete EN/ES language switch, translation catalog, settings screen and persistent accessibility preferences remain pending. See [Architecture](AppArchitecture.md).

### F-015 Guided screen introductions

Six Spanish popups briefly explain the purpose, controls and limitations of each guided stage. Each appears once per stage per guided run; Back does not repeat a dismissed introduction, and restarting the journey/reset allows them again. Entendido or Escape dismisses the modal. The popup blocks underlying controls and focuses its dismiss button. Free exploration does not show these popups. Source: GuidedJourney and GuidedExperienceController; see [Guided experience](GuidedExperience.md). The Noise Meter remains informational and sound playback remains pending. Popup rendering, keyboard/touch behavior and scene wiring still require Unity verification.

## Feature change history

Future feature changes append an entry here and update the current inventory/details. Use stable IDs; keep removed/deprecated entries with their status. Every entry links its detailed modification report.

| Date | Affected IDs | Change | Report |
| --- | --- | --- | --- |
| 2026-10-19 | F-001–F-014 | Initial inventory from existing implementation; no new runtime features added | [2026-10-19-004](Changes/2026-10-19-004-feature-documentation.md) |

| 2026-10-19 | F-001, F-004, F-010, F-012, F-015 | Reorder guided journey, require HNAI completion, add screen introductions and an informational meter stage | [2026-10-19-006](Changes/2026-10-19-006-guided-journey-and-popups.md) |
