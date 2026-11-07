# Modification report — rounded Home and English interface

- Report ID: 2026-11-06-006
- Date: 2026-11-06 (America/Mexico_City)
- Type: feature / visual / localization / tests / documentation

## Request and resulting behavior

Implement the approved first-phone design, with mostly yellow icons, two turquoise and two purple accents, and English presentation. Home now uses rounded cards, consistent code-drawn icons, chevrons, a yellow guided action and comfortable scrolling. Existing modules/routes, scientific methods, session boundaries and original audiovisual recordings are preserved. Interface copy and educational summaries are English; original Spanish HNAI items/choices, source figures, video language and proper song titles remain explicitly identified exceptions.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Rounded controls and icon system | Assets/_HearingNotion/Scripts/Navigation/RoundedCardGraphic.cs; Assets/_HearingNotion/Scripts/Navigation/HomeIconGraphic.cs; Assets/_HearingNotion/Scripts/Navigation/HomeMenuStyle.cs; new matching .meta files | Code-drawn shapes with explicit renderer dependencies and nonblocking decoration; five yellow module icons, two turquoise, Flappy and Waves purple, meter neutral |
| Shared styling and initialization | Assets/_HearingNotion/Scripts/Core/AppTheme.cs; Assets/_HearingNotion/Scripts/Core/AppManager.cs | Rounded Button target graphics, new accent colors and explicit English presentation initialization |
| Responsive layout and motion | Assets/_HearingNotion/Scripts/Navigation/ResponsiveScreenLayout.cs; Assets/_HearingNotion/Scripts/Navigation/WholePageScroll.cs; Assets/_HearingNotion/Scripts/Navigation/RuntimeArtworkController.cs; Assets/_HearingNotion/Scripts/Navigation/AppArtwork.cs; Assets/_HearingNotion/Scripts/Navigation/TravelingWaveGraphic.cs | Roomy Home, lower controls in scroll extent, pixel plus logical Canvas-size detection, English Waves control, subtler decoration |
| English module controls | Assets/_HearingNotion/Scripts/Assessment/AwarenessCheckManager.cs; Assets/_HearingNotion/Scripts/Exposure/ExposureManager.cs; Assets/_HearingNotion/Scripts/Navigation/GuidedExperienceController.cs; Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs; Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs | English prompts/navigation/playback/feedback and activity presentation; original questionnaire data and recordings untouched |
| English presentation and research content | Assets/_HearingNotion/Scripts/Content/EnglishPresentation.cs; Assets/_HearingNotion/Scripts/Content/ResearchSourcesController.cs; Assets/_HearingNotion/Resources/Research/ResearchStages.en.json; new matching .meta files | English media titles/notes in memory and four translated research summaries, retaining numerical evidence, study IDs, figures and uncertainty |
| English activity authoring | Tools/Content/ActivityEnglish.json; Tools/build_annex_catalog.py; 21 assets listed below | Correct English description fields and translated classification notes; authoring source prevents recurrence |
| Native preview and regression | Assets/_HearingNotion/Editor/StoppedHomePreview.cs; Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Same stopped Home; real top/after-scroll captures; palette/nonblocking/scroll checks and HNAI answer revision, completion, invalidation and reset checks |
| Content validation | Tools/Tests/validate_english_content.py | Compare numeric evidence and study bindings, 21 English descriptions and original HNAI domains/scale |
| Local build and evidence | Builds/AndroidPatched-2026-11-06; Marketing/Screenshots; LocalEvidence; tmp/english_interface.py | Update the existing separate Android snapshot; actual renders and temporary one-task text-edit helper stay local |
| Current guidance | AGENTS.md; Docs/HomeRedesign.md; Docs/HomeScene.md; Docs/AppArchitecture.md; Docs/Artwork.md; Docs/SpanishQuestionnaire.md; Docs/ResearchSources.md; Docs/MediaPlayback.md; Docs/ExposureExplorer.md; Docs/GuidedExperience.md; Docs/PageScrolling.md; Docs/EditorHomePreview.md; Docs/Test.md; Docs/AndroidDeployment.md; Docs/FEATURES.md; Docs/README.md | Document current presentation, language exceptions, ownership and build/device limits |
| QA skill and traceability | Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md; Docs/Changes/2026-11-06-006-rounded-english-interface.md; Docs/Changes/README.md | Extend the recurring QA procedure and index this coherent task |

Activity assets modified under Assets/_HearingNotion/ScriptableObjects/Activities/: airport.asset, road-traffic.asset, carpentry.asset, children-party.asset, classical-concert.asset, conference.asset, construction.asset, dentist.asset, hairdryer.asset, urban-ambience.asset, motorcycle-road.asset, nightclubs.asset, car-races.asset, rock-concert.asset, stadium.asset, shooting-range.asset, school.asset, snores.asset, carpentry-workshops.asset, construction-workshops.asset and edm-concert.asset. Existing .meta GUIDs, category memberships, source references and IDs were retained.

## Decisions and implications

The user-approved generated concept and supplied mockup are visual references, not working-app evidence. This implementation uses new C# UI geometry and existing imported headphone artwork; no new generated raster asset, vendor replacement, package upgrade, scene regeneration or scene binding change is introduced. Managers remain outside screen roots. Main and original Spanish HNAI JSON remain unchanged. Rounded surfaces/icons are owned by existing buttons/cards and reused; the existing event/lifecycle controls remain.

HNAI navigation and surrounding explanations are English, but no translated instrument, scoring, clinical validation or approved research workflow is claimed. English research summaries derive only from the already-authored Spanish summaries, not new scientific inference. Numeric-content checks preserve the evidence. The private media catalog is not rewritten: English metadata is applied in memory by stable identity/kind, preserving paths, bytes, alignment and relative gain. Original source videos/figures keep their language and proper titles keep their identity. No new data collection or persistence is introduced. Codex assisted code, translation, validation and documentation; physical-device and acoustic review remain human checks.

The first Home test exposed a capture/resize sequencing problem: the test restored responsive geometry but asserted scrolling before the pending page reflow. Capture settling and logical Canvas-size observation were corrected, and the test now explicitly reflows before asserting movement. A later HNAI reset test returned navigation to Welcome; the final capture procedure explicitly returns Home before capturing the lower page. These are recorded to distinguish genuine runtime/capture evidence from stale images or failed checks.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| Runtime/Editor C# and models | passed | Editor/Windows/Android-symbol compilation, Editor helpers, deterministic game checks and media integrity; serialized Inspector-field warnings only |
| English content | passed | Four study IDs/figure arrays/numeric-value multisets match Spanish source; 21 English descriptions; original 22-item HNAI choices, 9/5/8 domains and protocolConfirmed=false |
| Activity authoring tool | passed | Modified generator ran in a scratch project; English descriptions and original GUIDs verified without regenerating the working assets |
| Activity bindings | passed | 21 unique records, 18 annex mappings, overlapping categories and original GUID references; no invented prevalence or levels |
| Initial capture/scroll check | failed | Two runs rejected premature Home scroll assertions; corrected sequencing then passed |
| Native regression | passed | 93 checks; completed 2026-11-07T03:25:02Z (2026-11-06 local), including approved Home palette/scrolling, full HNAI revision/completion/reset, 51 audio variants and five nonblack decoded videos; muted Windows Editor under patched Unity |
| Final top/lower-page and stopped renders | passed | Actual 4K portrait/landscape and 720×1640 tall Home captures inspected; lower controls reachable; stopped capture exit 0; Main and HNAI SHA-256 unchanged |
| Updated APK | passed | Unity exit 0; 1,444,402,543 bytes; org.hearingnotion.prototype; IL2CPP ARM64/ARMv7, min API 23, target API 36; v1/v2 signatures verify; all 57 in-APK media hashes match |
| Physical Acer AX85 | not run | Phone not connected in the established workflow; touch/safe-area/output/offline cache/memory checks remain pending |
| QA skill structure | passed | quick_validate.py: Skill is valid; 93 native checks validate the current workflow, not physical device behavior |
| Profiling | not run | No measured optimization claim |

APK SHA-256: `967f40beba3b09595e406bdb5d4747df8cefda994c8747dadb54d091dcc914cf`. The prior APK is retained separately. Existing SDK/Gradle compatibility and signature META-INF warnings remain as documented in AndroidDeployment.md; no warning suppression or dependency upgrade was introduced.

## Performance

No before/after CPU/GPU profiling. Geometry is generated only during UI rebuilds, decorations do not intercept input and layout watches relevant dimensions; these implementation choices are not evidence of a speedup. Buffered audio and single-video transport retain their existing memory behavior.

## Limitations and follow-up

The English interface deliberately preserves the original Spanish research instrument and original-language media/figures. It is not a complete bilingual language selector. Existing education/research limitations, deferred measurement and DHWANI status remain. Confirm comfortable audio, touch, safe areas and actual device performance on the phone; muted Editor playback does not establish these. APK and media are local personal-test content, excluded from Markdown publication.

## Publication scope

Only this task’s project-authored Markdown is published. The public change index and skill register build on the current remote versions plus this task’s entries, so unrelated local-only draft records remain private and existing public work is preserved. Source, APKs, media, captures and raw logs remain local.

## Rollback

Reverse only this task's UI/content/controller/authoring edits and remove the five new runtime/resource assets with their metadata, restoring the prior controller/resource path if removing the English research JSON. Restore the prior English description fields if needed without changing activity GUIDs/IDs or categories. Do not regenerate Main, delete profiles, alter original recordings, remove the user’s Editor installation or discard unrelated website/documentation work. Preserve the prior APK separately when rebuilding. Documentation history is retained; no automatic revert or user-data deletion is performed.
