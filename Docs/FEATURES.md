# Hearing Notion feature catalog

Last reviewed: 2026-11-06 (America/Mexico_City).

Use this page to review app contents, find implementation details and trace feature changes. This initial inventory is reconstructed from current source, scene configuration and project notes; it is not a claim that all features were added or tested today. Detailed modification records start in [Modification history](Changes/README.md).

**Status meanings:** Implemented means code/assets exist; Partial means only part of the intended experience exists; Planned means no working module is claimed. Verification is recorded separately. Historical entries retain their earlier verification limits; on 2026-11-05 isolated, muted Unity Editor runs exercised page gestures, inline videos, final game feedback, popup order and navigation, audio/video playback, demographic save/delete with synthetic scratch data and first-round game actions. This is not physical listening or target-mobile verification. Earlier user feedback confirmed some UI improvements but also reported questionnaire-loading and animation issues; later fixes still need runtime confirmation.

## Inventory

| ID | Feature and entry point | Implementation | Verification and limits | Last updated |
| --- | --- | --- | --- | --- |
| F-001 | [Home and navigation](#f-001-home-and-navigation): Main scene | Approved rounded English Home implemented | Native palette/scroll/navigation checks and actual captures; phone review pending | 2026-11-06 |
| F-002 | [Responsive, readable UI](#f-002-responsive-readable-ui): all pages | Rounded controls, roomy Home and whole-page scrolling | Pixel/logical Canvas settling and native scroll checks; physical touch pending | 2026-11-06 |
| F-003 | [Exposure Explorer](#f-003-exposure-explorer): Sound Experience → Soundscapes | English activity descriptions/categories and direct audio | 21 source-mapped records and category/GUID checks; native comparison paths; physical listening pending | 2026-11-06 |
| F-004 | [Spanish HNAI questionnaire](#f-004-spanish-hnai-questionnaire): Awareness Check | Original Spanish instrument, English surrounding UI | Native revision, 22 answers, completion/recompletion and reset passed; no clinical scoring | 2026-11-06 |
| F-005 | [Personalized Takeaways](#f-005-personalized-takeaways): home/Continue | Partial; general reminders | Activity-add UI retired; no invented personal outcome; no full takeaway runtime retest | 2026-11-05 |
| F-006 | [Visitor session and reset](#f-006-visitor-session-and-reset): Takeaways reset | Implemented | Draft state and digital gain reset; Explorer reset removed; memory only unless explicit demographic save | 2026-11-05 |
| F-007 | [Theme and artwork](#f-007-theme-and-artwork): all screens | Rounded cards and balanced code-drawn icons | Five yellow/two turquoise/two purple accents; original headphones retained; device review pending | 2026-11-06 |
| F-008 | [Animated wave sprites](#f-008-animated-wave-sprites): background | Procedural contours; reduced opacity | Renderer dependencies and native rendering checked; physical motion preference/device review pending | 2026-11-06 |
| F-009 | [Sound Experience](#f-009-sound-experience): unified hub/player | Split branches with English controls/metadata | 51 variants tested in native Editor; original recordings and common gain unchanged; device listening pending | 2026-11-06 |
| F-010 | [Hearing Health and sources](#f-010-hearing-health-and-sources): home/guided | English controls and four English study summaries | Five decoded videos; study numbers/figures preserved; original-language media/figures identified | 2026-11-06 |
| F-011 | [Public knowledge check and research mode](#f-011-public-knowledge-check-and-research-mode) | Planned, foundations only | Separate public check, approved consent, scoring, YANS and export pending | 2026-10-19 inventory |
| F-012 | [Noise Meter](#f-012-noise-meter): guided information screen; disabled home card | Partial; measurement deferred | Informational stage implemented; no microphone measurement/calibration | 2026-10-19 |
| F-013 | [Music Lab](#f-013-music-lab) | Planned, future | No functioning laboratory | 2026-10-19 inventory |
| F-014 | [Bilingual controls and settings](#f-014-bilingual-controls-and-settings) | English presentation; language selector planned | Original Spanish HNAI, original videos/figures and proper titles preserved; not a translated instrument | 2026-11-06 |
| F-015 | [Guided screen introductions](#f-015-guided-screen-introductions): guided journey | English explanations and centered Got it | Native alignment/dismissal checks; source-language HNAI identified; human route/device review pending | 2026-11-06 |
| F-016 | [Local sound-source assignment](#f-016-local-sound-source-assignment) | Visitor UI retired; storage infrastructure retained | No deletion/migration; existing authored library survives | 2026-11-05 |
| F-017 | [Flappy Cloud attention game](#f-017-flappy-cloud-attention-game): home | Implemented two-round prototype with random soundscape | In-field choices, random playback, Pause and navigation cleanup passed; no causal research claim | 2026-11-05 |
| F-018 | [Optional demographics](#f-018-optional-demographics): startup/About you | Implemented; always before volume step | Native startup order and synthetic local consent/save/delete checks; local-only | 2026-11-05 |
| F-019 | [Listening setup](#f-019-listening-setup): after About you | Implemented midpoint default | Native 0.125 midpoint in unchanged 0–0.25 range; preview-only -12 dB preserved | 2026-11-05 |
| F-020 | [Noise basics](#f-020-noise-basics): Home | Implemented sourced education | Seven entries; native navigation/renders; human scroll/device review pending | 2026-11-05 |
| F-021 | [Unified sound hub](#f-021-unified-sound-hub): Home → Sound Experience | Implemented | Native single entry and two choices; reuses existing media/catalog without duplicated lists | 2026-11-05 |
| F-022 | [DHWANI future-work information](#f-022-dhwani-future-work-information): Home | Informational page implemented; analysis planned only | Seven attributed sections; no recording, prediction, API or validation claim | 2026-11-06 |
| F-023 | [Stopped Home preview](#f-023-stopped-home-preview): Main in Editor | Shared rounded English Home preview | Stopped portrait/landscape renders passed; transient; Main unchanged | 2026-11-06 |
| F-024 | [Android personal-test export](#f-024-android-personal-test-export): separate patched project | APK built; phone verification pending | Patched Editor regression: 93 checks; signed 1.44 GB APK and 57 in-package hashes verified; no device connected | 2026-11-06 |

## Feature details

### F-001 Home and navigation

A ninth card opens the attributed DHWANI informational future-work page. Outside Play Mode an Editor-only labelled Home preview displays current cards/artwork without running managers. See [preview](EditorHomePreview.md).

Main.unity uses app-owned panels adapted from Menu Template 1. Home now has one Sound Experience entry opening Soundscapes / Hearing examples. Home opens modules, Awareness Check is the first option, Back uses navigation history, and the guided flow now proceeds through HNAI, Exposure, Sound, Health recommendations, an informational Noise Meter stage, and Research & Resources. HNAI must be completed before guided continuation; the final stage returns Home. The 5–8-minute target has not been usability-tested. Source: AppManager, NavigationManager, ScreenView in Assets/_HearingNotion/Scripts. See [Home scene](HomeScene.md) and [Architecture](AppArchitecture.md).

### F-002 Responsive, readable UI

WholePageScroll wraps each screen as the content of a full-viewport ScrollRect. Header, artwork, module content, Back/Home/Exit and bottom note move together. Inner module scrolling/masks are disabled and long content expands, preserving direct-child lookup bindings. Responsive template layout handles orientation and delayed CanvasScaler viewport updates. Native tests verify actual positions move together; physical touch feel and keyboard usability remain unverified. See [scrolling](PageScrolling.md) and [report](Changes/2026-11-05-004-unified-sounds-and-whole-pages.md).

### F-003 Exposure Explorer

Within Sound Experience → Soundscapes, three category filters expose 21 source-mapped records, including 18 original/protected soundscapes and three chart-only labels. Visitors inspect activity descriptions and prevention tips, then open an existing comparison. Original/Protection 3M 1260 buttons directly start or stop their version. Add activities, audio-edit/import and Explorer reset controls are removed. Activity selection is no longer collected by this UI. Data provenance and category overlap remain intact; no personal risk estimate is inferred. See [Explorer](ExposureExplorer.md), [media](MediaPlayback.md) and [corrections report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-004 Spanish HNAI questionnaire

The 22 supplied Spanish statements use the confirmed five-point agreement scale. Visitors select/revise answers, navigate Anterior/Siguiente, complete all items with Finalizar and review responses. Answers remain local draft state for the visit. No score, clinical result or export is produced. In guided mode HNAI is first; Finalizar completes the questionnaire and enables the outer Continuar button to open Exposure Explorer. The controller loads Resources/Questionnaires/HNAI.es.json and has startup recovery. This full instrument prototype is separate from a future short public quiz and consented research administration. Source: AwarenessCheckManager and AppSession. See [Spanish questionnaire](SpanishQuestionnaire.md).

### F-005 Personalized Takeaways

Currently provides general prevention reminders and a route back to soundscapes, with session reset. Explorer no longer offers activity-add controls; there is no claim of personalized knowledge gains, measured exposure or a hearing assessment. Legacy selection state remains infrastructure only. Source: ExposureManager. Full personalized knowledge/habit outcomes remain planned. See [Explorer](ExposureExplorer.md) and [report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-006 Visitor session and reset

In-memory state includes activity selections, sound context and draft HNAI answers/completion. Reset replaces the session and triggers navigation/UI reset subscribers. Returning Home preserves the current visit. Visitor state has no disk persistence, account, automatic analytics or remote participant storage. The separately authored local audio library persists across visits; it contains content assignments, not participant answers. Source: SessionManager, AppSession and module reset subscriptions. See [Architecture](AppArchitecture.md).

### F-007 Theme and artwork

Current approved style: [rounded Home and English presentation](HomeRedesign.md), with five yellow/two turquoise/two purple accents, reusable rounded controls and code-drawn icons. Existing headphone artwork and source media are retained.

Warm near-white backgrounds, white cards with light borders, yellow primary actions, soft-yellow takeaways and gold selections retain the supplied visual identity while reducing large yellow blocks. Shared button hover/pressed/disabled states apply to home, runtime activity controls, questionnaire controls and modal confirmation. A new transparent isolated headphone illustration replaces the tiny composite header; the static background texture is reduced to 16% opacity. Source: AppTheme and AppArtwork; headphones-hero-v2.png in Resources/Artwork. See [Artwork and prompts](Artwork.md) and [visual refresh](VisualRefresh.md). Code compiles and the image alpha was checked; actual Unity placement remains unverified.

### F-008 Animated wave sprites

Each traveling contour now fades smoothly to transparent across both outer 35% sections, with vertex-interpolated opacity. This removes the hard leading/trailing tips in either travel direction, including paused waves. Temporal fades remain active. Source compilation passed; Unity visual review remains pending. See [soft wave ends](Changes/2026-10-19-011-soft-wave-ends.md).

The previous low-opacity fixed-position sprite drift has been replaced by two procedural 2D UI wave bands. Each band traverses the screen in 10 seconds, rests 4 seconds and fades at entry/exit; the second band starts 7 seconds apart. Initial time is set to 2.5 seconds so a pass is visible on entry. No wave image import is required. AmbientWaveAnimation updates TravelingWaveGraphic with unscaled time; inactive screens do not update, and unfocused standalone players pause. A home button labeled Ondas: activas/pausadas freezes both bands into static contours for the current app session. Controls/header remain still and decorative graphics do not intercept input. Pure timing tests and compilation passed, but the user-reported Unity visibility issue is not yet confirmed resolved in Play Mode. See [visual refresh](VisualRefresh.md).

Wave graphics now explicitly require RectTransform/CanvasRenderer, create the renderer before the graphic, and repair missing renderers during initialization and activation. This addresses the reported clipping exception; Unity runtime confirmation is pending. See [renderer fix report](Changes/2026-10-19-010-wave-canvasrenderer-fix.md).

### F-009 Sound Experience

**Current navigation:** the hub splits Soundscapes and Hearing examples; the player no longer repeats the soundscape catalog. See [hub](SoundExperienceHub.md).

**Current configuration:** audio and videos reference the existing external library directly; no separate media copies remain in Assets. Local catalog paths are private. The demonstration computer must have this folder available. See [direct-library correction](Changes/2026-10-22-003-existing-media-library.md).

Local playback now integrates 18 original/protected comparisons and five original/95/100 WHIS song sets. Press an audio version to play; press the active version again to stop. Protection restarts at zero when switching; hearing-loss examples retain approximate position and an extra Play/Pause control. Session listening gain is common to all variants. Playback stops on navigation/reset and pauses on interruption. One clip loads on demand. All ten prior song exports and completed listening copies now report PASS. Numerical, hash and format checks do not establish listening/device validity. See [media playback](MediaPlayback.md) and [integration report](Changes/2026-10-22-002-media-integration.md).

All 18 source soundscapes now have local 3M 1260 laboratory-reference protected exports, aligned unfiltered references, profile/response records and summary data. Original rates/stereo preserved; common −6.02 dB input headroom, no independent protected normalization. All digital checks and original hashes passed; one full-scale source is flagged for review. These are offline illustrations, with Unity playback infrastructure now implemented; actual playback and listening/fit validation remain pending. See [soundscape batch](SoundscapeProtection.md) and [report](Changes/2026-10-22-001-soundscape-protection-batch.md).

Model-level song exports were found too quiet for practical listening. Separate reference/95/100 listening folders now use one common per-song gain, preserving model differences; raw exports and originals remain unchanged. All completed processed copies now report PASS in the final listening verification record. Listening/device review remains pending. See [level correction](Changes/2026-10-21-005-whis-listening-level-fix.md).

A full-song offline batch for two WHO Figure 1 exposure labels is now rendering five supplied songs per variant. User-selected flat illustrative thresholds are 14.5/24.75 dB HL, alpha .5 assumed; originals are preserved and processing is 24 kHz stereo with documented context segmentation. Numerical wrapper checks passed; full-library export verification now reports PASS; listening remains pending. See [song batch](WHISSongBatch.md).

Offline hearing-protection authoring now has run_hearing_protection.m: select audio/output to generate a generic educational example from a cited laboratory attenuation curve using documented MATLAB fir2/fftfilt. Exports aligned source/protected WAVs, provenance record and response-check CSV; no autoplay/Unity import. Numerical verification passed, including <1 dB target-anchor agreement at four rates. Perceptual/device/field validation is not established. See [method, sources and limitations](HearingProtection.md) and [report](Changes/2026-10-21-003-hearing-protection-authoring.md).

Offline authoring now has a single MATLAB entry point, Tools/Audio/run_whis.m: choose audio, enter the seven thresholds/compression and modeled-level assumptions, and select an output parent folder. It saves the processed WAV/reference/record to a new folder without playback, or accepts three arguments for scripted use. Interactive values are explicitly illustrative and modeled-only. Dialog interaction still needs manual verification. See [launcher report](Changes/2026-10-20-003-whis-audio-launcher.md).

Explorer passes the active activity ID and the destination displays its description, any assigned local filename and an explicit playback-pending message. Protection/hearing-loss/tinnitus comparisons, transport controls, reviewed audio assets and safety processing are not implemented. See [Architecture](AppArchitecture.md) and [Explorer checks](ExposureExplorer.md).

WHIS-DTVF is the selected hearing-loss authoring method. An offline MATLAB wrapper calls pinned WHIS v302/GCFB v234 reference code with explicit seven-point dB HL, compression health and calibration assumptions. It saves review-pending source/processed pairs and local processing metadata, handles mono/stereo without autoplay, and rejects unsupported input, clipping and overwrites. Reference checkouts/output are local and ignored. MATLAB numerical checks and their actual status are recorded in the [report](Changes/2026-10-20-002-whis-dtvf-offline-processing.md); this does not establish perceptual/device validation or Unity playback. See [steps, sources and use](WHIS.md).

### F-010 Hearing Health and sources

Current video UX: five topic cards each contain a frame with Play/Pause and Stop directly below it. White RawImage tint replaces black modulation that hid decoded pictures even while playing. No separate selection step; one shared decoder renders only the explicitly played card. Scrolling does not autoplay. See [media playback](MediaPlayback.md) and [correction report](Changes/2026-11-05-003-results-video-and-swipe.md).

Hearing Health now includes five informative video playback copies: health effects, hearing loss, protection and two tinnitus versions, alongside general prevention recommendations. Explicit select/play controls, stop/pause and cleanup use the shared media transport. The existing original video files are referenced directly; codec compatibility needs device checks. Unity/device playback, editorial and caption review remain pending. Research & Sources continues to show its four research stages separately. See [media playback](MediaPlayback.md).

Hearing Health retains prevention content. Research & Sources now offers four English summary tabs (with original-language figures): INTER-NOISE pilot, demographic noise-source reports, preliminary HNAI psychometrics and post-awareness YANS change. Each shows a scrollable sourced summary and limitations; demographics and YANS include three original research figures. Tabs reset to the first stage on entry/visitor reset; navigation stays outside the scroll region. Prior study findings are separate from visitor responses. No audiovisual content or original DOCX/PDF files are bundled. HNAI validation remains preliminary; YANS figure metadata gaps and unknown demographic group sizes are explicit. See [research guide](ResearchSources.md). Full hearing-health lessons and broader source browsing remain partial; actual Unity interaction/figure readability requires review.

### F-011 Public knowledge check and research mode

Planned as separate experiences: a short educational quiz and full approved research instruments. Existing route guards, consent fields and questionnaire definitions are foundations only. No complete consent UI, formal research administration, YANS content, approved scoring or export exists. HNAI draft interaction in F-004 does not establish these capabilities. See [Architecture](AppArchitecture.md) and [Spanish questionnaire](SpanishQuestionnaire.md).

### F-012 Noise Meter

The home card remains disabled. Guided mode now includes an informational coming-later screen with its own introduction and Continue control. Microphone acquisition, RMS/weighting, calibration and qualified estimated readings are deferred. No calibrated sound levels are displayed. See [Architecture](AppArchitecture.md).

### F-013 Music Lab

Future music-perception/DSP research module; route reserved and unavailable. No processing pipeline or interactive laboratory is implemented. See [Architecture](AppArchitecture.md).

### F-014 Bilingual controls and settings

Current presentation is English across navigation, prompts, activity descriptions, media controls and research summaries. HNAI item/choice wording, proper media titles, original videos and source figures remain explicit exceptions. No language-selector or translated validated instrument is claimed. See [design](HomeRedesign.md).

Spanish HNAI, Spanish Explorer activity details and bilingual-capable content fields exist; other UI remains mixed English/Spanish. Home now exposes a session-wide wave pause/resume button. A complete EN/ES language switch, translation catalog, settings screen and persistent accessibility preferences remain pending. See [Architecture](AppArchitecture.md).

### F-015 Guided screen introductions

Entendido now explicitly centers its TMP label with zero margins; its inherited template alignment no longer offsets the text. See [correction report](Changes/2026-11-05-003-results-video-and-swipe.md).

Six Spanish popups briefly explain the purpose, controls and limitations of each guided stage. Each appears once per stage per guided run; Back does not repeat a dismissed introduction, and restarting the journey/reset allows them again. Entendido or Escape dismisses the modal. The popup blocks underlying controls and focuses its dismiss button. Free exploration does not show these popups. Source: GuidedJourney and GuidedExperienceController; see [Guided experience](GuidedExperience.md). The Noise Meter remains informational; sound playback is implemented separately. Fixed a user-reported CanvasGroup MissingComponentException by using a Unity-aware null check before adding the component. Popup rendering, keyboard/touch behavior and this runtime fix still require Unity verification.

### F-016 Local sound-source assignment

Visitor assignment/import controls are retired as of 2026-11-05. LocalSoundSourceLibrary, LocalAudioFilePicker and import-rule code remain available as authoring infrastructure; existing files and manifests are preserved and still survive session reset. This change does not delete imported content or approve it for playback/distribution. No new visitor upload path is offered. See [catalog](SoundscapeCatalog.md) and [report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-017 Flappy Cloud attention game

Tap/Space starts and flaps; a separate Pause button pauses. Two seeded rounds retain varied obstacles/stars, +10 blue/−10 red scoring, progressive speed and a maximum 180 seconds each. At first game over, Try again and Continue appear inside the playfield, with Continue below. Try again restarts quiet play; Continue opens a six-second notice then loads one randomly chosen available original Explorer soundscape for round 2. It loops at the common listening gain, pauses on interruption and stops/releases on navigation/reset/game over. Missing audio shows an explicit unavailable notice and blocks sound-round startup. A large scrollable final panel compares both actual points, gaps and times and gives a point difference, sourced focus/cognitive-load/stress/fatigue context, and explicit Retry/Exit/Hearing Health next steps. Final Retry restarts both rounds. Scores are temporary/descriptive: practice, fatigue and chance prevent causal attribution to noise. Compilation/model tests and muted native action/playback/cleanup checks passed; physical listening and human difficulty remain unverified. See [game guide](FlappyCloud.md) and [report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-018 Optional demographics

Startup optional gender, age, country, referral source and editable device model. Skip, session-only continuation and explicit local-save consent are distinct. One local profile can be deleted; About you reopens the notice. Data is not sent or linked to HNAI. See [demographics](Demographics.md), [testing](Test.md) and [task report](Changes/2026-11-05-001-prototype-review-and-media.md).

### F-019 Listening setup

About you always appears first at startup. After it closes, a fresh visit starts the unchanged 0–0.25 slider at its midpoint, 0.125 (50%). An optional 6 kHz preview and draggable volume slider let visitors choose a comfortable app gain. Explicit Play/Stop, Accept and continue and Skip prevent automatic preview playback. Accept stores temporary gain; Skip restores the prior gain. The preview alone has -12 dB attenuation; the shared slider and all other sounds retain their previous scale. The software ceiling is not SPL calibration and comfort does not establish safe exposure. Popup controls block underlying screens. See [setup design and limits](ListeningSetup.md) and [report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-020 Noise basics

An independent Home screen explains dB, dBA, LAeq,T, LAeq,8h, LEX,8h, level/duration/frequency/peaks and digital versus acoustic levels. Seven sourced JSON entries scroll inside the template panel. It does not alter guided order or implement noise measurement. See [definitions and primary references](NoiseBasics.md) and [report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-021 Unified sound hub

One Home card opens SoundHub with Soundscapes and Hearing examples. The former reuses the existing activity/catalog route and selected-pair player; the latter clears activity context and opens the five-song hearing-example list. The hidden Exposure Explorer template remains for startup cloning. An appended enum preserves existing route values; guided order is unchanged. See [hub guide](SoundExperienceHub.md) and [report](Changes/2026-11-05-004-unified-sounds-and-whole-pages.md).

### F-022 DHWANI future-work information

A Home page describes proposed inputs, computed indicators, model estimates, soundscape perception, integration steps and applications from the supplied overview, attributed to Dr Manish Manohare, IIT Delhi. Claims are author-described, not independently validated. No microphone/upload/analysis/model/API is implemented. See [scope and provenance](DhwaniFuture.md).

### F-023 Stopped Home preview

An Editor-only transient Canvas mirrors the complete Home with artwork and current cards while Main is stopped. It clears actions, labels preview status, is removed before Play and excluded from builds/saving. Actual stopped captures are separate from runtime verification. See [preview guide](EditorHomePreview.md).

### F-024 Android personal-test export

A separate portable project contains current source and all media with no Windows dependency in its catalog. Unity 2022.3.62f2 and its Android toolchain are installed; the migrated copy passed 93 native Editor checks. A personal IL2CPP ARM64/ARMv7 APK built successfully, its signature verifies, and all 57 packaged media hashes match. Preparation uses ASCII media paths to avoid the diagnosed archive-encoding failure and refuses overwrites. The open desktop project remains on its older Editor. Android extraction, installation, listening, touch and performance remain unverified because the phone is not connected. See [Android build and installation steps](AndroidDeployment.md).

## Feature change history

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
| 2026-10-20 | F-010, F-015 | Add four sourced research stages, scrollable summaries/figures and updated guided explanation; exclude audiovisual material | [2026-10-20-004](Changes/2026-10-20-004-research-stages.md) |
| 2026-10-20 | F-017 | Tap tutorial, double-tap pause, progressive three-minute rounds, automatic second-condition notice and final Retry | [2026-10-20-005](Changes/2026-10-20-005-flappy-cloud-tap-flow.md) |
| 2026-10-20 | F-017 | Narrow proportionate playfield, faster speed ramp, closer obstacles and dedicated Pause/Reanudar without double-tap detection | [2026-10-20-006](Changes/2026-10-20-006-flappy-cloud-layout-difficulty.md) |
| 2026-10-21 | F-017 | Add blue/red star collectibles worth +10/−10 with separate points and per-round results | [2026-10-21-001](Changes/2026-10-21-001-flappy-cloud-stars.md) |
| 2026-10-21 | F-017 | Randomize bounded obstacle/star layout and arrival intervals with fresh session seeds | [2026-10-21-002](Changes/2026-10-21-002-flappy-cloud-randomization.md) |
| 2026-10-21 | F-009 | Add generic lab-data-based hearing-protection authoring and evidence/validation rules | [2026-10-21-003](Changes/2026-10-21-003-hearing-protection-authoring.md) |
| 2026-10-21 | F-009 | Start full-song WHIS batch for user-approved flat 25-year 95/100 dBA exposure illustrations; numerical checks passed, render completion pending | [2026-10-21-004](Changes/2026-10-21-004-whis-exposure-song-batch.md) |
| 2026-10-21 | F-009 | Correct overly quiet export presentation with common-gain comparison copies; preserve raw model levels | [2026-10-21-005](Changes/2026-10-21-005-whis-listening-level-fix.md) |
| 2026-10-22 | F-009 | Filter and verify all 18 soundscapes using the selected 3M 1260 lab reference; retain aligned comparisons and originals | [2026-10-22-001](Changes/2026-10-22-001-soundscape-protection-batch.md) |
| 2026-10-22 | F-003, F-006, F-009, F-010, F-015 | Integrate offline comparisons and informative videos, explicit controls and transport cleanup | [2026-10-22-002](Changes/2026-10-22-002-media-integration.md) |
| 2026-10-22 | F-009, F-010 | Use existing external audio/video files directly and remove generated duplicate media; preserve all module mappings | [2026-10-22-003](Changes/2026-10-22-003-existing-media-library.md) |
| 2026-10-22 | F-009, F-010 | Prevent media button labels from creating then removing required text-layout components; Editor/Windows compilation passed, Play Mode pending | [2026-10-22-004](Changes/2026-10-22-004-media-label-dependency.md) |
| 2026-10-22 | F-003, F-009, F-016 | Make linked audio visible at the top of activity details; collapse optional uploads and check real availability | [2026-10-22-005](Changes/2026-10-22-005-explorer-linked-audio.md) |
| 2026-10-22 | F-009, F-010 | Avoid documented streamed-clip native crash on Back by fully loading local WAVs; preserve navigation buttons and harden cleanup; native retest pending | [2026-10-22-006](Changes/2026-10-22-006-soundscape-back-crash.md) |
| 2026-10-22 | F-017 | Rewrite game/tutorial/menu copy in clear English, remove corrupted characters and clarify silent rounds | [2026-10-22-007](Changes/2026-10-22-007-flappy-english-copy.md) |
| 2026-11-05 | F-001, F-002, F-009, F-010, F-017, F-018 | Add game-over choices, repair media compatibility, optional consent-based local profile, native QA and authentic high-resolution captures | [2026-11-05-001](Changes/2026-11-05-001-prototype-review-and-media.md) |

Future feature changes append an entry here and update the current inventory/details. Use stable IDs; keep removed/deprecated entries with their status. Every entry links its detailed modification report.

| 2026-11-05 | F-001, F-002, F-003, F-005, F-006, F-009, F-016–F-020 | In-playfield choices, random game soundscape, optional volume setup, noise terms and direct Explorer audio; retire authoring controls | [2026-11-05-002](Changes/2026-11-05-002-direct-listening-and-noise-basics.md) |

| 2026-11-05 | F-002, F-009, F-010, F-015, F-017, F-018, F-019 | Preview-only -12 dB; always About you first; complete game results; centered guided control; page-wide gestures and inline videos | [2026-11-05-003](Changes/2026-11-05-003-results-video-and-swipe.md) |

| 2026-11-05 | F-001, F-002, F-003, F-009, F-010, F-019, F-021 | Single sound hub, visible videos with controls below, midpoint default and actual whole-page scrolling | [2026-11-05-004](Changes/2026-11-05-004-unified-sounds-and-whole-pages.md) |

| 2026-11-06 | F-001, F-002, F-009, F-019, F-022, F-023, F-024 | Stopped Home visibility, attributed DHWANI future page and portable Android preparation with explicit toolchain/device blockers | [2026-11-06-001](Changes/2026-11-06-001-editor-dhwani-android.md) |
| 2026-11-06 | F-024 | Install patched Android toolchain, verify migrated Editor, fix portable archive names and build/verify personal APK; phone test pending | [2026-11-06-002](Changes/2026-11-06-002-patched-android-build.md) |

| 2026-11-06 | F-001, F-002, F-003, F-004, F-007, F-008, F-009, F-010, F-014, F-015, F-023, F-024 | Approved rounded English presentation, balanced icons, subtle background, HNAI fidelity/revision/reset checks and rebuilt personal APK | [2026-11-06-006-rounded-english-interface](Changes/2026-11-06-006-rounded-english-interface.md) |
