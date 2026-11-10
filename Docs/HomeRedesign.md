# Rounded Home and English presentation

Implemented from the user-approved first-phone reference and the yellow/turquoise/purple design proposal on 2026-11-06. This is an implementation guide, not a claim of phone verification.

## Layout and interaction

Home retains nine modules and the existing routes: Awareness Check first, Noise basics, Sound Experience, deferred Noise Meter, Hearing Health, Research & Sources, Flappy Cloud, About you and informational DHWANI. Guided mode and the Soundscapes/Hearing examples split are unchanged. Personalized Takeaways and the footer follow the modules; the Waves button has been removed.

Warm white background, white rounded cards, thin neutral borders, charcoal text and yellow primary actions follow the approved reference. Existing headphone artwork is retained. Four module icons are yellow (Awareness, Sound, Health, About you); Noise basics and Research are turquoise; Flappy Cloud and DHWANI are purple. Noise Meter stays neutral and deferred. Color is reinforced by labels and distinct icons; it conveys no personal risk score.

Portrait uses one roomy column; landscape uses two columns. Cards and text are not reduced to squeeze all modules into one viewport. Header, cards, Takeaways and footer scroll together. Home's page height includes the lower controls. Responsive layout observes both pixel size and logical Canvas size so CanvasScaler settling cannot leave stale geometry after orientation changes. The stopped Editor preview uses the same Home layout, is transient and is removed before Play.

## Components and ownership

| Source | Responsibility |
| --- | --- |
| HomeMenuStyle.cs | Existing named controls, text positions, Home cards/icons and navigation arrows; no route changes |
| RoundedCardGraphic.cs | Code-drawn rounded fill/inset border; reusable Button target graphic; no generated texture or vendor asset replacement |
| HomeIconGraphic.cs | Code-drawn module/play/arrow icons; explicit RectTransform/CanvasRenderer dependency and nonblocking decoration |
| AppTheme.cs | Shared colors and rounded button attachment; existing focus/pressed behavior retained |
| ResponsiveScreenLayout.cs / WholePageScroll.cs | Orientation, logical-size settling and lower-page extent |
| WindowStyle.cs / InterfaceStyleController.cs | Shared Home font, heading/action weights, rounded module/modal cards and fields; explicit startup/navigation/size refresh |
| EnglishPresentation.cs | Initial legacy panel labels and ID/category-based English media presentation; no modification of file paths, recordings or scientific DSP |

Graphics are reused rather than recreated on each frame. Layout changes happen on viewport/input changes; the pre-existing wave animation remains decorative and has lower visual opacity. No performance speedup is claimed without profiling. Rounded surfaces belong to their buttons, icons belong to their cards; imported artwork remains shared. No extra textures, dependencies or scene regeneration are needed.

## English boundaries

Navigation, prompts, playback controls, guided explanations, activity descriptions and research summaries are English. The stable hierarchy names remain internal binding keys, even when an old Spanish object name is retained. Proper song titles, original video language and original research figures are preserved. English captions explain original-language content.

HNAI statements and five agreement-response labels remain the exact supplied Spanish instrument. Home and questionnaire instructions explicitly identify it as Spanish. Changing UI language is not permission to create a translated validated instrument; no English HNAI translation, new scoring or research consent is implied. The questionnaire JSON, IDs, 9/5/8 domains and response values are unchanged.

ResearchSourcesController loads Research/ResearchStages.en.json. The Spanish source JSON remains intact. English summaries preserve the same four study IDs, figures and numeric evidence, including uncertainty and cohort limitations. Tools/Tests/validate_english_content.py checks those invariants and the HNAI scale. Tools/Content/ActivityEnglish.json maintains the 21 English activity descriptions/notes for authoring; build_annex_catalog.py uses it to avoid reintroducing Spanish into English fields. Do not run the scene regeneration tool to update this UI.

## Verification and remaining checks

Use [Test.md](Test.md) and the [QA skill](Skills/unity-prototype-review/SKILL.md). Capture genuine top/after-scroll Home renders in portrait, landscape and a tall viewport. Verify icons do not intercept navigation, all lower controls are reachable, popup order/media lifecycle persist and HNAI revision/completion/reset works. English-content checks do not prove acoustic safety or device usability. See the [task report](Changes/2026-11-06-006-rounded-english-interface.md) for actual outcomes and the [Android guide](AndroidDeployment.md) for the latest build/device state.

## Shared windows — 2026-11-06

All module pages, game notices/results and the three existing popup families now share the Home font and typography hierarchy, charcoal headings/actions, muted explanations, white rounded content cards, neutral borders and spacing. Popup backdrops use consistent translucency. Form fields are rounded; inner scroll backgrounds are transparent. Topic titles remain bold and Sound Experience branch cards are white like Home modules. Bindings, selection colors, input values, consent controls and original research wording are preserved. Shared styling starts after runtime builders and refreshes for navigation and logical Canvas-size changes. No continuous hierarchy scan is introduced.

The removed Waves action is not replaced. RuntimeArtworkController retains an engine SetReducedMotion method, but visitor preference UI/OS integration is unavailable. Background animation otherwise continues unchanged. DHWANI receives the second purple module icon. See [follow-up report](Changes/2026-11-06-007-shared-window-style.md).

## Dark chrome — 2026-11-10

Reference-inspired dark header/footer bands have curved yellow edges, existing headphone artwork and nonblocking procedural decoration. Footer Home, Sounds, Research, Learn and You lead to existing routes/profile entry; no Analyze measurement feature is implied. The footer now remains at the bottom viewport edge, with the header pinned above; Research and About you cards are removed from the Home grid because those routes remain in the footer. Module heading spacing and shared rounded-card radius were adjusted; HNAI response text is left-aligned. Immersive Flappy Cloud retains its game-owned layout.

## Pinned navigation and simplified media — 2026-11-10

Seven packed Home cards remain. Research and You are footer entries. Module icons are 84 logical units with 1.5-times stroke thickness; the remaining palette is three yellow, one turquoise, two purple and the gray deferred meter. Existing routes and questionnaire wording are preserved. See [modification report](Changes/2026-11-10-002-pinned-navigation-and-media.md).
