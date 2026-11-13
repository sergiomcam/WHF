# Hearing Notion feature catalog

Last reviewed: 2026-11-10 (America/Mexico_City).

Use this page to review app contents, find implementation details and trace feature changes. This initial inventory is reconstructed from current source, scene configuration and project notes; it is not a claim that all features were added or tested today. Detailed modification records start in [Modification history](Changes/README.md).

**Status meanings:** Implemented means code/assets exist; Partial means only part of the intended experience exists; Planned means no working module is claimed. Verification is recorded separately. Historical entries retain their earlier verification limits; on 2026-11-05 isolated, muted Unity Editor runs exercised page gestures, inline videos, final game feedback, popup order and navigation, audio/video playback, demographic save/delete with synthetic scratch data and first-round game actions. This is not physical listening or target-mobile verification. Earlier user feedback confirmed some UI improvements but also reported questionnaire-loading and animation issues; later fixes still need runtime confirmation.

## Inventory

| ID | Feature and entry point | Implementation | Verification and limits | Last updated |
| --- | --- | --- | --- | --- |
| F-001 | [Home and navigation](#f-001-home-and-navigation): Main scene | Hardware Back, modal priority and pinned footer routes | Compiled; 100 native checks and authentic renders passed; Android build/device verification recorded in the report | 2026-11-11 |
| F-002 | [Responsive, readable UI](#f-002-responsive-readable-ui): all pages/popups | Responsive body, soft popups and pinned header/footer | Compiled; 96 native checks passed; targeted AX85 footer/spacing/game checks passed; acoustic output and all-device coverage unverified | 2026-11-10 |
| F-003 | [Exposure Explorer](#f-003-exposure-explorer): Sound Experience → Soundscapes | Context then same-page protection comparison | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |
| F-004 | [Spanish HNAI questionnaire](#f-004-spanish-hnai-questionnaire): Awareness Check | Original Spanish instrument with left-aligned responses | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |
| F-005 | [Personalized Takeaways](#f-005-personalized-takeaways): home/Continue | Partial; general reminders | Activity-add UI retired; no invented personal outcome; no full takeaway runtime retest | 2026-11-05 |
| F-006 | [Visitor session and reset](#f-006-visitor-session-and-reset): Takeaways reset | Implemented | Draft state and digital gain reset; Explorer reset removed; memory only unless explicit demographic save | 2026-11-05 |
| F-007 | [Theme and artwork](#f-007-theme-and-artwork): all screens | Pinned dark chrome, stronger icons and retained artwork | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |
| F-008 | [Animated wave sprites](#f-008-animated-wave-sprites): background | Procedural contours remain; visitor control retired | Engine SetReducedMotion retained without UI/OS preference integration | 2026-11-06 |
| F-009 | [Sound Experience](#f-009-sound-experience): unified hub/player | Unity-gain direct version toggles; song menu first | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |
| F-010 | [Hearing Health and sources](#f-010-hearing-health-and-sources): home/guided | Stable research stages; four video topics and native touch-return player | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |
| F-011 | [Public knowledge check and research mode](#f-011-public-knowledge-check-and-research-mode) | Planned, foundations only | Separate public check, approved consent, scoring, YANS and export pending | 2026-10-19 inventory |
| F-012 | [Noise Meter](#f-012-noise-meter): guided information screen; disabled home card | Partial; measurement deferred | Informational stage implemented; no microphone measurement/calibration | 2026-10-19 |
| F-013 | [Music Lab](#f-013-music-lab) | Planned, future | No functioning laboratory | 2026-10-19 inventory |
| F-014 | [Bilingual controls and settings](#f-014-bilingual-controls-and-settings) | English presentation; language selector planned | Original Spanish HNAI, original videos/figures and proper titles preserved; not a translated instrument | 2026-11-06 |
| F-015 | [Guided screen introductions](#f-015-guided-screen-introductions): guided journey | Rounded guided popup with hardware Back dismissal | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |
| F-016 | [Local sound-source assignment](#f-016-local-sound-source-assignment) | Visitor UI retired; storage infrastructure retained | No deletion/migration; existing authored library survives | 2026-11-05 |
| F-017 | [Flappy Cloud attention game](#f-017-flappy-cloud-attention-game): home | Taller field, in-arena pause and mixed moving penguin pairs | Compiled; 96 native checks passed; targeted AX85 footer/spacing/game checks passed; acoustic output and all-device coverage unverified | 2026-11-10 |
| F-018 | [Optional demographics](#f-018-optional-demographics): startup/footer You | Content-fitted scrolling form, collapsed empty feedback | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |
| F-019 | [Listening setup](#f-019-listening-setup): after About you | Shared popup hierarchy and centered actions | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |
| F-020 | [Noise basics](#f-020-noise-basics): Home | Implemented sourced education | Seven entries; native navigation/renders; human scroll/device review pending | 2026-11-05 |
| F-021 | [Unified sound hub](#f-021-unified-sound-hub): Home → Sound Experience | Implemented | Native single entry and two choices; reuses existing media/catalog without duplicated lists | 2026-11-05 |
| F-022 | [Hearing Notion 2.0](#f-022-dhwani-future-work-information): Home | Three-button future-work hub with sourced Dwani overview | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |
| F-023 | [Stopped Home preview](#f-023-stopped-home-preview): Main in Editor | Shared rounded English Home preview | Stopped portrait/landscape renders passed; transient; Main unchanged | 2026-11-06 |
| F-024 | [Android personal-test export](#f-024-android-personal-test-export): separate patched project | Corrected APK installed; targeted AX85 retest passed | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |
| F-025 | [DHWANI interface mockups](#f-025-dhwani-interface-mockups): Home → DHWANI | Enhanced illustrative artwork, dark overview and in-frame Back | Borderless presentation compiled; 100 native checks, actual renders and APK verification passed; phone retest deferred | 2026-11-12 |

## Feature details

### F-001 Home and navigation

Android hardware Back uses the same history action as the screen Back control; open startup/guided modals dismiss first. Pinned dark footer links lead to implemented sections; Research and You replace their duplicate Home cards. See [2026-11-10 correction report](Changes/2026-11-10-001-android-interaction-corrections.md).

Seven Home cards include the attributed DHWANI informational future-work page. Research and About you are accessed through the footer. Outside Play Mode an Editor-only labelled Home preview displays current cards/artwork without running managers. See [preview](EditorHomePreview.md).

Main.unity uses app-owned panels adapted from Menu Template 1. Home now has one Sound Experience entry opening Soundscapes / Hearing examples. Home opens modules, Awareness Check is the first option, Back uses navigation history, and the guided flow now proceeds through HNAI, Exposure, Sound, Health recommendations, an informational Noise Meter stage, and Research & Resources. HNAI must be completed before guided continuation; the final stage returns Home. The 5–8-minute target has not been usability-tested. Source: AppManager, NavigationManager, ScreenView in Assets/_HearingNotion/Scripts. See [Home scene](HomeScene.md) and [Architecture](AppArchitecture.md).

### F-002 Responsive, readable UI

Module portrait headings and introductions use separate vertical positions; dark header/footer remain pinned to viewport edges. Shared popup cards use a softer 48-unit corner radius. See [2026-11-10 correction report](Changes/2026-11-10-001-android-interaction-corrections.md).

Current shared style: module and popup typography, bold action/headings, white rounded cards/form fields and transparent inner viewports follow Home. Selection colors, inputs, route bindings and original wording remain. See [design](HomeRedesign.md).

WholePageScroll wraps each screen as the content of a full-viewport ScrollRect. Module content, Back/Home/Exit and bottom note move together; DockedScreenChrome keeps the branded header/artwork and footer at the viewport edges. Inner module scrolling/masks are disabled and long content expands, preserving direct-child lookup bindings. Responsive template layout handles orientation and delayed CanvasScaler viewport updates. Native tests verify actual positions move together; physical touch feel and keyboard usability remain unverified. See [scrolling](PageScrolling.md) and [report](Changes/2026-11-05-004-unified-sounds-and-whole-pages.md).

### F-003 Exposure Explorer

After category/example selection, context, prevention and source information appear before inline original/protection toggle buttons and menu/video links. Protection comparisons omit Stop and rewind. See [2026-11-10 correction report](Changes/2026-11-10-001-android-interaction-corrections.md).

Within Sound Experience → Soundscapes, three category filters expose 21 source-mapped records, including 18 original/protected soundscapes and three chart-only labels. Visitors inspect activity descriptions and prevention tips, then use the comparison at the end of the same page. Original/Protection 3M 1260 buttons directly start or stop their version. Add activities, audio-edit/import and Explorer reset controls are removed. Activity selection is no longer collected by this UI. Data provenance and category overlap remain intact; no personal risk estimate is inferred. See [Explorer](ExposureExplorer.md), [media](MediaPlayback.md) and [corrections report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-004 Spanish HNAI questionnaire

All five original Spanish response labels are left-aligned and retain their numeric values, selection marker and exact wording. See [2026-11-10 correction report](Changes/2026-11-10-001-android-interaction-corrections.md).

The 22 supplied Spanish statements use the confirmed five-point agreement scale. Visitors select/revise answers, navigate Anterior/Siguiente, complete all items with Finalizar and review responses. Answers remain local draft state for the visit. No score, clinical result or export is produced. In guided mode HNAI is first; Finalizar completes the questionnaire and enables the outer Continuar button to open Exposure Explorer. The controller loads Resources/Questionnaires/HNAI.es.json and has startup recovery. This full instrument prototype is separate from a future short public quiz and consented research administration. Source: AwarenessCheckManager and AppSession. See [Spanish questionnaire](SpanishQuestionnaire.md).

### F-005 Personalized Takeaways

Currently provides general prevention reminders and a route back to soundscapes, with session reset. Explorer no longer offers activity-add controls; there is no claim of personalized knowledge gains, measured exposure or a hearing assessment. Legacy selection state remains infrastructure only. Source: ExposureManager. Full personalized knowledge/habit outcomes remain planned. See [Explorer](ExposureExplorer.md) and [report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-006 Visitor session and reset

In-memory state includes activity selections, sound context and draft HNAI answers/completion. Reset replaces the session and triggers navigation/UI reset subscribers. Returning Home preserves the current visit. Visitor state has no disk persistence, account, automatic analytics or remote participant storage. The separately authored local audio library persists across visits; it contains content assignments, not participant answers. Source: SessionManager, AppSession and module reset subscriptions. See [Architecture](AppArchitecture.md).

### F-007 Theme and artwork

Procedural dark header/footer bands have yellow curved edges; existing headphones and balanced module accents remain. Footer labels use real destinations rather than implying an unimplemented analysis tool. See [2026-11-10 correction report](Changes/2026-11-10-001-android-interaction-corrections.md).

Current approved style: [rounded Home and English presentation](HomeRedesign.md), with four yellow/two turquoise/two purple module accents, reusable rounded controls and code-drawn icons. Existing headphone artwork and source media are retained.

Warm near-white backgrounds, white cards with light borders, yellow primary actions, soft-yellow takeaways and gold selections retain the supplied visual identity while reducing large yellow blocks. Shared button hover/pressed/disabled states apply to home, runtime activity controls, questionnaire controls and modal confirmation. A new transparent isolated headphone illustration replaces the tiny composite header; the static background texture is reduced to 16% opacity. Source: AppTheme and AppArtwork; headphones-hero-v2.png in Resources/Artwork. See [Artwork and prompts](Artwork.md) and [visual refresh](VisualRefresh.md). Code compiles and the image alpha was checked; actual Unity placement remains unverified.

### F-008 Animated wave sprites

Current visitor UI: Waves control removed at user request. Animation remains; the retained engine SetReducedMotion method is not a visitor setting or OS integration. Historical control descriptions below refer to earlier versions. See [shared-style report](Changes/2026-11-06-007-shared-window-style.md).

Each traveling contour now fades smoothly to transparent across both outer 35% sections, with vertex-interpolated opacity. This removes the hard leading/trailing tips in either travel direction, including paused waves. Temporal fades remain active. Source compilation passed; Unity visual review remains pending. See [soft wave ends](Changes/2026-10-19-011-soft-wave-ends.md).

The previous low-opacity fixed-position sprite drift has been replaced by two procedural 2D UI wave bands. Each band traverses the screen in 10 seconds, rests 4 seconds and fades at entry/exit; the second band starts 7 seconds apart. Initial time is set to 2.5 seconds so a pass is visible on entry. No wave image import is required. AmbientWaveAnimation updates TravelingWaveGraphic with unscaled time; inactive screens do not update, and unfocused standalone players pause. A home button labeled Ondas: activas/pausadas freezes both bands into static contours for the current app session. Controls/header remain still and decorative graphics do not intercept input. Pure timing tests and compilation passed, but the user-reported Unity visibility issue is not yet confirmed resolved in Play Mode. See [visual refresh](VisualRefresh.md).

Wave graphics now explicitly require RectTransform/CanvasRenderer, create the renderer before the graphic, and repair missing renderers during initialization and activation. This addresses the reported clipping exception; Unity runtime confirmation is pending. See [renderer fix report](Changes/2026-10-19-010-wave-canvasrenderer-fix.md).

### F-009 Sound Experience

Soundscape original/protection controls now live at the end of the Explorer activity details; the same buffered transport and stop-on-navigation behavior remain. See [2026-11-10 correction report](Changes/2026-11-10-001-android-interaction-corrections.md).

**Current navigation:** the hub splits Soundscapes and Hearing examples; the player no longer repeats the soundscape catalog. See [hub](SoundExperienceHub.md).

**Current configuration:** audio and videos reference the existing external library directly; no separate media copies remain in Assets. Local catalog paths are private. The demonstration computer must have this folder available. See [direct-library correction](Changes/2026-10-22-003-existing-media-library.md).

Local playback now integrates 18 original/protected comparisons and five original/95/100 WHIS song sets. Press an audio version to play; press the active version again to stop. Protection restarts at zero when switching; hearing-loss examples retain approximate position and use direct version toggles only. Multimedia uses unity source gain, preserving authored relative levels. Playback stops on navigation/reset and pauses on interruption. One clip loads on demand. All ten prior song exports and completed listening copies now report PASS. Numerical, hash and format checks do not establish listening/device validity. See [media playback](MediaPlayback.md) and [integration report](Changes/2026-10-22-002-media-integration.md).

All 18 source soundscapes now have local 3M 1260 laboratory-reference protected exports, aligned unfiltered references, profile/response records and summary data. Original rates/stereo preserved; common −6.02 dB input headroom, no independent protected normalization. All digital checks and original hashes passed; one full-scale source is flagged for review. These are offline illustrations, with Unity playback infrastructure now implemented; actual playback and listening/fit validation remain pending. See [soundscape batch](SoundscapeProtection.md) and [report](Changes/2026-10-22-001-soundscape-protection-batch.md).

Model-level song exports were found too quiet for practical listening. Separate reference/95/100 listening folders now use one common per-song gain, preserving model differences; raw exports and originals remain unchanged. All completed processed copies now report PASS in the final listening verification record. Listening/device review remains pending. See [level correction](Changes/2026-10-21-005-whis-listening-level-fix.md).

A full-song offline batch for two WHO Figure 1 exposure labels is now rendering five supplied songs per variant. User-selected flat illustrative thresholds are 14.5/24.75 dB HL, alpha .5 assumed; originals are preserved and processing is 24 kHz stereo with documented context segmentation. Numerical wrapper checks passed; full-library export verification now reports PASS; listening remains pending. See [song batch](WHISSongBatch.md).

Offline hearing-protection authoring now has run_hearing_protection.m: select audio/output to generate a generic educational example from a cited laboratory attenuation curve using documented MATLAB fir2/fftfilt. Exports aligned source/protected WAVs, provenance record and response-check CSV; no autoplay/Unity import. Numerical verification passed, including <1 dB target-anchor agreement at four rates. Perceptual/device/field validation is not established. See [method, sources and limitations](HearingProtection.md) and [report](Changes/2026-10-21-003-hearing-protection-authoring.md).

Offline authoring now has a single MATLAB entry point, Tools/Audio/run_whis.m: choose audio, enter the seven thresholds/compression and modeled-level assumptions, and select an output parent folder. It saves the processed WAV/reference/record to a new folder without playback, or accepts three arguments for scripted use. Interactive values are explicitly illustrative and modeled-only. Dialog interaction still needs manual verification. See [launcher report](Changes/2026-10-20-003-whis-audio-launcher.md).

Explorer passes the active activity ID and the destination displays its description, any assigned local filename and an explicit playback-pending message. Protection/hearing-loss/tinnitus comparisons, transport controls, reviewed audio assets and safety processing are not implemented. See [Architecture](AppArchitecture.md) and [Explorer checks](ExposureExplorer.md).

WHIS-DTVF is the selected hearing-loss authoring method. An offline MATLAB wrapper calls pinned WHIS v302/GCFB v234 reference code with explicit seven-point dB HL, compression health and calibration assumptions. It saves review-pending source/processed pairs and local processing metadata, handles mono/stereo without autoplay, and rejects unsupported input, clipping and overwrites. Reference checkouts/output are local and ignored. MATLAB numerical checks and their actual status are recorded in the [report](Changes/2026-10-20-002-whis-dtvf-offline-processing.md); this does not establish perceptual/device validation or Unity playback. See [steps, sources and use](WHIS.md).

### F-010 Hearing Health and sources

Research stage selectors occupy two stable rows above layout-managed summaries and aspect-preserving figures. Android video cards additionally offer full-screen native playback with phone player controls; native playback starts from the beginning and uses phone media volume. See [2026-11-10 correction report](Changes/2026-11-10-001-android-interaction-corrections.md).

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

Guided/startup modal dismissal participates in hardware Back routing, with rounded card surfaces and retained consent/input behavior. See [2026-11-10 correction report](Changes/2026-11-10-001-android-interaction-corrections.md).

Entendido now explicitly centers its TMP label with zero margins; its inherited template alignment no longer offsets the text. See [correction report](Changes/2026-11-05-003-results-video-and-swipe.md).

Six Spanish popups briefly explain the purpose, controls and limitations of each guided stage. Each appears once per stage per guided run; Back does not repeat a dismissed introduction, and restarting the journey/reset allows them again. Entendido or Escape dismisses the modal. The popup blocks underlying controls and focuses its dismiss button. Free exploration does not show these popups. Source: GuidedJourney and GuidedExperienceController; see [Guided experience](GuidedExperience.md). The Noise Meter remains informational; sound playback is implemented separately. Fixed a user-reported CanvasGroup MissingComponentException by using a Unity-aware null check before adding the component. Popup rendering, keyboard/touch behavior and this runtime fix still require Unity verification.

### F-016 Local sound-source assignment

Visitor assignment/import controls are retired as of 2026-11-05. LocalSoundSourceLibrary, LocalAudioFilePicker and import-rule code remain available as authoring infrastructure; existing files and manifests are preserved and still survive session reset. This change does not delete imported content or approve it for playback/distribution. No new visitor upload path is offered. See [catalog](SoundscapeCatalog.md) and [report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-017 Flappy Cloud attention game

The fitted playfield bounds are larger without changing sprite ratios. Continue displays a notice that waits indefinitely for its Ready button; no countdown starts noisy play. See [2026-11-10 correction report](Changes/2026-11-10-001-android-interaction-corrections.md).

Tap/Space starts and flaps; an in-arena Pause/Resume button pauses. Two seeded rounds retain varied stationary/moving penguin pairs and stars, +10 blue/−10 red scoring, progressive speed and a maximum 180 seconds each. At first game over, Try again and Continue appear inside the playfield, with Continue below. Try again restarts quiet play; Continue opens a notice; explicit Ready loads one randomly chosen available original Explorer soundscape for round 2. It loops at unity source gain, pauses on interruption and stops/releases on navigation/reset/game over. Missing audio shows an explicit unavailable notice and blocks sound-round startup. A large scrollable final panel compares both actual points, gaps and times and gives a point difference, sourced focus/cognitive-load/stress/fatigue context, and explicit Retry/Exit/Hearing Health next steps. Final Retry restarts both rounds. Scores are temporary/descriptive: practice, fatigue and chance prevent causal attribution to noise. Compilation/model tests and muted native action/playback/cleanup checks passed; physical listening and human difficulty remain unverified. See [game guide](FlappyCloud.md) and [report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-018 Optional demographics

Startup optional gender, age, country, referral source and editable device model. Only Skip and Save are shown. Save follows an explicit local-consent notice; Skip discards inputs without writing or deleting an older profile. Manual file removal/Android Clear storage is explained; About you reopens the notice. Data is not sent or linked to HNAI. See [demographics](Demographics.md), [testing](Test.md) and [task report](Changes/2026-11-05-001-prototype-review-and-media.md).

### F-019 Listening setup

About you always appears first at startup. After it closes, a fresh visit starts the unchanged 0–0.25 slider at its midpoint, 0.125 (50%). An optional 6 kHz preview and draggable volume slider let visitors choose a comfortable preview gain. Explicit Play/Stop, Accept and continue and Skip prevent automatic preview playback. Accept stores temporary preview gain; Skip restores the prior preview gain. The preview alone has -12 dB attenuation; the preview slider retains its range, while multimedia/game playback uses unity gain and device media volume. The software ceiling is not SPL calibration and comfort does not establish safe exposure. Popup controls block underlying screens. See [setup design and limits](ListeningSetup.md) and [report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-020 Noise basics

An independent Home screen explains dB, dBA, LAeq,T, LAeq,8h, LEX,8h, level/duration/frequency/peaks and digital versus acoustic levels. Seven sourced JSON entries scroll inside the template panel. It does not alter guided order or implement noise measurement. See [definitions and primary references](NoiseBasics.md) and [report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

### F-021 Unified sound hub

One Home card opens SoundHub with Soundscapes and Hearing examples. The former reuses the existing activity/catalog route and selected-pair player; the latter clears activity context and opens the five-song hearing-example list. The hidden Exposure Explorer template remains for startup cloning. An appended enum preserves existing route values; guided order is unchanged. See [hub guide](SoundExperienceHub.md) and [report](Changes/2026-11-05-004-unified-sounds-and-whole-pages.md).

### F-022 DHWANI future-work information

A Home page describes proposed inputs, computed indicators, model estimates, soundscape perception, integration steps and applications from the supplied overview, attributed to Dr Manish Manohare, IIT Delhi. Claims are author-described, not independently validated. No microphone/upload/analysis/model/API is implemented. See [scope and provenance](DhwaniFuture.md).

### F-023 Stopped Home preview

An Editor-only transient Canvas mirrors the complete Home with artwork and current cards while Main is stopped. It clears actions, labels preview status, is removed before Play and excluded from builds/saving. Actual stopped captures are separate from runtime verification. See [preview guide](EditorHomePreview.md).

### F-024 Android personal-test export

Updated portable Android source is rebuilt separately from the open desktop project; final APK/device evidence appears in the task report. See [2026-11-10 correction report](Changes/2026-11-10-001-android-interaction-corrections.md).

A separate portable project contains current source and all media with no Windows dependency in its catalog. Unity 2022.3.62f2 and its Android toolchain are installed; the migrated copy passed 94 native Editor checks. A personal IL2CPP ARM64/ARMv7 APK built successfully, its signature verifies, and all 57 packaged media hashes match. Preparation uses ASCII media paths to avoid the diagnosed archive-encoding failure and refuses overwrites. The open desktop project remains on its older Editor. On 2026-11-09 the verified APK installed and launched on AX85/Android 13. Portrait navigation and page swipe worked, the user confirmed Airport original audio/stop, and educational video frames rendered. Full media, game, orientation, interruption, offline and performance verification remain pending. See [Android build and installation steps](AndroidDeployment.md).

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

| 2026-11-06 | F-001, F-002, F-007, F-008, F-009, F-010, F-015, F-018, F-019, F-022, F-023, F-024 | Remove Waves action, purple DHWANI icon, shared module/popup typography and rounded surfaces/fields; original data/audio preserved | [2026-11-06-007](Changes/2026-11-06-007-shared-window-style.md) |

| 2026-11-09 | F-024 | Install unchanged APK on AX85 and record first physical smoke test; full regression and category wrapping remain open | [2026-11-09-001](Changes/2026-11-09-001-ax85-device-smoke-test.md) |

## Android interaction corrections — 2026-11-10

F-001/F-002: hardware Back routing and shared dark chrome; F-003/F-009: inline protection comparison follows activity information; F-004: left-aligned Spanish response labels; F-007/F-015: rounded surfaces and reference-inspired bands; F-010: stable research layout and native Android full-screen video entry; F-017: larger field and explicit noisy-round Ready; F-024: updated Android source under validation. Source compilation, 95 native checks, APK signature/media verification and targeted final AX85 retest passed. Full media, rotation and interruption coverage remains limited; see the report.

| Date | Affected IDs | Change | Report |
| --- | --- | --- | --- |
| 2026-11-10 | F-001, F-002, F-003, F-004, F-007, F-009, F-010, F-015, F-017, F-024 | Android interaction, inline media, research layout and dark chrome corrections | [2026-11-10-001](Changes/2026-11-10-001-android-interaction-corrections.md) |

## Pinned navigation and simplified media — 2026-11-10

F-001/F-002/F-007: pinned branded header/footer, seven packed Home cards and stronger module icons; Research and You remain footer routes. F-009: hearing-example song list above direct version toggles, with separate Play/Pause and rewind controls hidden. F-010: four displayed video topics, first tinnitus only, and native touch Return to page. F-018: profile remains accessible through You. F-023: stopped preview uses the same seven-card arrangement. F-024: separate Android APK rebuilt with verified signatures, 57 media hashes and native Activity class; targeted AX85 footer/video checks passed. See the report for full-run timing and remaining device-coverage limitations.

| Date | Affected IDs | Change | Report |
| --- | --- | --- | --- |
| 2026-11-10 | F-001, F-002, F-007, F-009, F-010, F-018, F-023, F-024 | Pinned chrome, footer-only routes, stronger icons and simplified media | [2026-11-10-002](Changes/2026-11-10-002-pinned-navigation-and-media.md) |

## Footer, source volume and Flappy Cloud — 2026-11-10

F-001/F-002: footer callbacks rebound on cloned screens and content-sized lower-page spacing. F-009/F-010/F-019: multimedia uses unity source gain; the optional startup slider is preview-only. F-017: taller arena, larger cloud/penguins/star labels, in-field Pause/Resume and mixed stationary/shared-center moving pairs. F-024: Android build/device verification recorded in the report.

| Date | Affected IDs | Change | Report |
| --- | --- | --- | --- |
| 2026-11-10 | F-001, F-002, F-009, F-010, F-017, F-019, F-024 | Clone-safe footer, compact lower spacing, authored media levels and larger moving-pair game | [2026-11-10-003](Changes/2026-11-10-003-footer-volume-and-flappy.md) |

### F-025 DHWANI interface mockups

Home → Hearing Notion 2.0 → Dwani opens full-screen reference interfaces 3 Audio Upload, 4 Psychoacoustic Indicators and 5 Sound Analysis. Continue and Back are the active mockup navigation controls; the third Continue opens the fourth dark framed overview, retaining all seven sourced descriptions. Reentry/reset returns to the three-button 2.0 hub. Enhanced reference-based curves, metrics and predicted-looking labels are static illustrations explicitly marked MOCKUP ONLY; they are not personal results. No file picker, microphone, upload, saving, analysis, prediction, network or new permission is implemented. See [DHWANI guide](DhwaniFuture.md) and [report](Changes/2026-11-10-004-compact-about-you-and-dhwani-mockups.md).

## Compact About you and DHWANI preview — 2026-11-10

F-018 removes fixed empty message/footer space through content-fit layout. F-022 retains the existing attributed future overview after the preview. F-025 adds the requested inert three-screen sequence. F-024 records the personal Android rebuild/device verification in the report.

| Date | Affected IDs | Change | Report |
| --- | --- | --- | --- |
| 2026-11-10 | F-002, F-018, F-022, F-024, F-025 | Compact demographic form and clearly inert DHWANI interfaces 3/4/5 | [2026-11-10-004](Changes/2026-11-10-004-compact-about-you-and-dhwani-mockups.md) |

## Hearing Notion 2.0 hub — 2026-11-11

F-001/F-022: the Home entry is renamed Hearing Notion 2.0, with Multilanguage validation, Dwani and Music for hearing loss. The language/music branches are informational only; Dwani opens F-025 full-screen mockups. F-025 uses full-Canvas modal blocking and Back/Continue navigation, with no recording or analysis. F-019 adds headphone placement guidance in startup popup 2. F-024 tracks the personal build/device outcome. The compact About you work from the previous task is retained.

| Date | Affected IDs | Change | Report |
| --- | --- | --- | --- |
| 2026-11-11 | F-001, F-019, F-022, F-024, F-025 | 2.0 hub, full-screen Dwani and headphone placement guidance; complete pending documentation | [2026-11-11-001](Changes/2026-11-11-001-hearing-notion-2-hub.md) |

## Reference-frame and startup correction — 2026-11-11

F-007/F-015: warm ivory shared cards and near-white inputs. F-018: Skip/Save only, explicit local consent and manual-deletion notice. F-019: short headphone legend below artwork. F-022/F-025: original raster reference interfaces, in-frame Back and a dark fourth overview. Current validation/build/device outcomes are recorded in the report.

| Date | Affected IDs | Main change | Report |
| --- | --- | --- | --- |
| 2026-11-11 | F-007, F-015, F-018, F-019, F-022, F-024, F-025 | Reference artwork/frames, warmer surfaces and simplified startup | [2026-11-11-002](Changes/2026-11-11-002-reference-frames-and-startup.md) |

## Enhanced artwork, cards and video previews — 2026-11-12

F-007/F-015: enriched rounded surfaces with gentle elevation and role-colored accents. F-009: actual four video posters and centered direct play, with poster restoration on Stop/navigation. F-025: >2K AI-enhanced decorative reference atlas; original retained, no measurement fidelity claim. Current native/build/device checks are in the report.

| Date | Affected IDs | Change | Report |
| --- | --- | --- | --- |
| 2026-11-12 | F-007, F-009, F-010, F-015, F-018, F-019, F-024, F-025 | Enhanced Dwani artwork, richer frames and actual video previews | [2026-11-12-002](Changes/2026-11-12-002-enhanced-artwork-video-previews.md) |

## Borderless option sheets — 2026-11-12

F-007/F-015/F-018/F-019: larger borderless section/popup sheets, near-white options/fields and removal of the previous accent-stroke/shadow treatment. F-022/F-025: borderless hub/preview surfaces. F-024: corrected personal APK tracked separately. Source content, answers, media and behaviors are unchanged. Validation is recorded in the report.

| Date | Affected IDs | Change | Report |
| --- | --- | --- | --- |
| 2026-11-12 | F-003, F-004, F-007, F-009, F-010, F-015, F-018, F-019, F-022, F-024, F-025 | Integrated borderless sheets and option surfaces within the existing palette | [2026-11-12-003](Changes/2026-11-12-003-borderless-option-sheets.md) |
