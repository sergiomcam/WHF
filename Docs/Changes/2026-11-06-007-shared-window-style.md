# Modification report — shared window style and simpler Home

- Report ID: 2026-11-06-007
- Date: 2026-11-06 (America/Mexico_City)
- Type: visual / accessibility / feature / documentation

## Request and resulting behavior

Remove the Waves: on button, move its purple accent to another icon, and use the Home text/display style throughout other screens and popups. Home no longer creates a motion control, its footer moves upward, and DHWANI's infinity icon is purple alongside Flappy Cloud. Yellow remains the dominant action/header accent; four module icons are yellow, two turquoise, two purple and the deferred meter is neutral.

WindowStyle and InterfaceStyleController share the Home font family, bold headings/actions, normal explanatory text, charcoal/muted colors, rounded white content cards, inset borders and consistent spacing across module pages, game notices/results, demographics, listening setup and guided popups. Form fields are rounded. Navigation, inputs, scientific content and existing data/audio behavior are preserved.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Simplify Home and recolor DHWANI | Assets/_HearingNotion/Scripts/Navigation/HomeMenuStyle.cs | Hide stale motion controls, move footer up and assign purple to the infinity icon |
| Retire control creation | Assets/_HearingNotion/Scripts/Navigation/RuntimeArtworkController.cs; Assets/_HearingNotion/Editor/StoppedHomePreview.cs | Remove the button from runtime and stopped preview; retain engine SetReducedMotion infrastructure without visitor UI |
| Section hierarchy and branch cards | Assets/_HearingNotion/Scripts/Content/NoiseBasicsController.cs; Assets/_HearingNotion/Scripts/Content/DhwaniFutureController.cs; Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs; Assets/_HearingNotion/Scripts/Audio/SoundHubController.cs | Retain bold topic headings and use white branch cards; presentation only |
| Repair encoding artifacts | Assets/_HearingNotion/Scripts/Content/EnglishPresentation.cs; Tools/Tests/validate_english_content.py; HomeMenuStyle.cs and MediaExperienceController.cs listed above | Recover UTF-8 separators/dashes/ellipsis after visual review and reject known mojibake markers in runtime/Editor source |
| Shared typography and surfaces | Assets/_HearingNotion/Scripts/Navigation/WindowStyle.cs; Assets/_HearingNotion/Scripts/Navigation/WindowStyle.cs.meta | Match Home font/weights, action alignment, rounded content/modal surfaces and form fields while preserving text and selection colors |
| Explicit style initialization | Assets/_HearingNotion/Scripts/Navigation/InterfaceStyleController.cs; Assets/_HearingNotion/Scripts/Navigation/InterfaceStyleController.cs.meta; Assets/_HearingNotion/Scripts/Core/AppManager.cs | Initialize after runtime module/popup creation and refresh on navigation/logical Canvas-size changes |
| Responsive integration | Assets/_HearingNotion/Scripts/Navigation/ResponsiveScreenLayout.cs | Style non-Home screens and game typography during responsive passes without moving the normalized game arena |
| Native regression and renders | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs; Marketing/Screenshots; LocalEvidence | Verify absent control, new palette, matching module/popup fonts, nonblocking rounded surfaces and rounded input targets; keep authentic captures local |
| Local Android snapshot | Builds/AndroidPatched-2026-11-06 | Sync app-owned changes into the separate patched copy; preserve desktop paths/settings and source media |
| Design/module documentation | AGENTS.md; Docs/HomeRedesign.md; Docs/HomeScene.md; Docs/AppArchitecture.md; Docs/Artwork.md; Docs/EditorHomePreview.md; Docs/ListeningSetup.md; Docs/Demographics.md; Docs/GuidedExperience.md; Docs/Test.md; Docs/AndroidDeployment.md; Docs/FEATURES.md | Record shared styling, retired UI and actual validation limits |
| Recurring QA and history | Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md; Docs/Changes/README.md; Docs/Changes/2026-11-06-007-shared-window-style.md | Update the existing repeat-review workflow and task traceability |

## Decisions and implications

The Waves UI removal is explicit user direction. Background motion itself is retained; an engine-level reduced-motion method remains, but there is no replacement visitor control or operating-system preference integration. No routes or features are silently assigned measurement capabilities.

Styling runs after existing runtime builders and on relevant navigation/Canvas-size changes. Existing content/layout bindings stay intact; text is not translated or rewritten in this task. HNAI statements, choices, response IDs and protocol state are unchanged. Button selected colors are not reset by the styling pass. Inputs retain their TMP_InputField components and callbacks. Game playfield/sprite geometry, audio gains, media paths, consent and persistence rules are unchanged. New rounded surfaces are child-owned decorations with raycastTarget=false and explicit RectTransform/CanvasRenderer dependencies through RoundedCardGraphic.

There are two new script GUIDs and no scene regeneration, scene-binding change, asset move, package update or research-data schema change. Codex assisted the UI code, checks and documentation. No new artwork, scientific claim, participant data collection or external service was added.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| C# / static/model checks | passed | Editor/Windows/Android-symbol compile, Editor helpers, game model and media integrity; Inspector-field warnings only |
| Initial popup centering check | failed | Inactive popup ancestors were excluded from parent Button lookup; corrected to include inactive parents and preserve zero popup-label margin; strengthened checks for all popup actions |
| Native screens/popups | passed | 94 checks; completion 2026-11-07T04:35:17Z (2026-11-06 local); matching fonts/surfaces, absent control, popup action alignment, HNAI revision/reset, synthetic consent save/delete, 51 audio variants and five decoded nonblack videos |
| Initial visual encoding review | failed | Found mojibake in separators/duration/media labels; corrected three UTF-8 source files and added a source-encoding regression check; the task batch build was stopped before final packaging |
| Stopped preview | passed | UTF-8-corrected portrait/landscape renders completed; Main SHA-256 and HNAI JSON hash unchanged |
| Updated personal APK | passed | Unity exit 0; 1,444,413,354 bytes; v1/v2 signature verification; all 57 bundled media hashes match; ARM64/ARMv7, min API 23, target API 36 |
| Physical phone / audible output | not run | Acer not connected in the established workflow; touch, safe areas and physical listening remain pending |
| English content | passed | Original HNAI scale/domains/protocol and study values/figure bindings remain intact |
| QA skill structure | passed | quick_validate.py: Skill is valid; actual native workflow also exercised |
| Profiling | not run | No performance gain claimed |

APK SHA-256: `b80dedcedf7a14012d38798ada0d0a9913136b2a0b8f7d63009f6c04c33a87c1`. Existing Gradle compatibility/META-INF signature warnings remain documented in AndroidDeployment.md; no warning suppression or toolchain upgrade was added. An Editor-only guard prevents the ExecuteAlways responsive pass from authoring module decorations outside Play Mode; it compiles out of the Android player and does not change the verified APK runtime.

## Performance

Shared typography/surface passes are tied to initialization, screen changes and logical Canvas resizing, not continuous hierarchy scans. Surfaces are reused. No comparative CPU/GPU profiling was performed; this is not a measured optimization claim.

## Limitations and follow-up

Physical-device interaction/output and accessibility review remain necessary. The original Spanish HNAI and original-language audiovisual/figure content remain explicit English-interface exceptions. Removing the motion button removes that visitor-facing accessibility control; retained engine methods are not a replacement UI. This remains a local personal-test build, not a store release or distribution-rights approval.

## Publication scope

Publish only this task's project-authored Markdown with the current remote head preserved. Keep unrelated private draft entries local; merge the task's public index/skill rows onto their remote versions. Source, media, screenshots, APKs and raw logs remain local.

## Rollback

Restore the previous Home/runtime artwork/stopped-preview code to reinstate the button and prior icon mapping. Remove InterfaceStyleController initialization and responsive WindowStyle calls before removing the two new scripts and their .meta files. Preserve all other source changes, asset GUIDs, Main, questionnaire JSON, visitor data, original recordings and unrelated draft documentation. Keep the preceding APK separately; do not regenerate the scene or uninstall an app containing real saved data merely to roll back presentation.
