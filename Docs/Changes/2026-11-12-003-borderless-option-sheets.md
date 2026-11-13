# Modification report — Integrated borderless option sheets

- Report ID: 2026-11-12-003
- Date: 2026-11-12 (America/Mexico_City)
- Type: UI / fix / documentation

## Request and resulting behavior

The earlier frame treatment only added decoration to outlined boxes. The user requested integrated section/option containers like the supplied examples, within the selected palette. The new implementation removes wireframe outlines, accent strips and shadows from section/popup sheets and option surfaces. It uses wider continuous warm-ivory sheets with larger upper corners and lighter rounded option/topic surfaces. Content, callbacks, scoring, media and research data are unchanged. Codex assisted code and QA; no new artwork is generated or reference imagery copied into the app.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Borderless sheet geometry | Assets/_HearingNotion/Scripts/Navigation/RoundedCardGraphic.cs | New asymmetric Sheet corner treatment; option buttons attach without borders; retain legacy decorative support without enabling it for new sheets. |
| Surface hierarchy | Assets/_HearingNotion/Scripts/Navigation/WindowStyle.cs | Large borderless module/popup sheets, lighter topic/input surfaces, decorative module overhangs and borderless options; preserve controls and selected colors. |
| Neutral option palette | Assets/_HearingNotion/Scripts/Core/AppTheme.cs | Secondary options use existing near-white Background against warm-ivory sheets; primary/selected palettes unchanged. |
| Questionnaire option surface | Assets/_HearingNotion/Scripts/Assessment/AwarenessCheckManager.cs | Unselected answers use near-white against the warm sheet; selected marker/color and original Spanish labels remain unchanged. |
| 2.0/Dwani surfaces | Assets/_HearingNotion/Scripts/Content/DhwaniMockupController.cs | Lighter hub options and borderless dark preview frames, preserving enhanced artwork and Back/Continue. |
| Regression | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Assert module sheets are borderless, undecorated and use large sheet corners; retain full media/assessment/navigation tests. |
| Separate portable mirror | Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/ | Mirror the six scoped C# changes for the personal test build. |
| Architecture/design guidance | AGENTS.md; Docs/AppArchitecture.md; Docs/HomeRedesign.md; Docs/DhwaniFuture.md; Docs/SpanishQuestionnaire.md; Docs/ExposureExplorer.md; Docs/AndroidDeployment.md; Docs/FEATURES.md | Record current structural treatment, palette boundaries, behavior and delivery state. |
| QA/history | Docs/Test.md; Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md; Docs/Changes/README.md; Docs/Changes/2026-11-12-003-borderless-option-sheets.md | Extend recurring review instructions and record feature/modification history. |

## Decisions and implications

The supplied fitness/travel references inform rounded sheet hierarchy and borderless option grouping, not their red/blue colors, account/travel features or imagery. UI uses the existing AppTheme values. Original media/artwork and scientific content are retained. No new assets/GUIDs, dependencies, scenes, routes, data schemas or participant storage changes are introduced. Decorative overhangs ignore layout/input; existing layout dimensions remain authoritative. A presentation-only serialized Sheet flag is added to RoundedCardGraphic, defaulting false for existing components; runtime builders configure it explicitly. No scene YAML migration is required. Home retains its own layout/style. Phone testing stays deferred at the user’s prior request.

The initial visual review exposed neutral HNAI choices blending into the sheet and an existing category-label wrap. Neutral answer fills now contrast with the sheet; compact labels lose excess side margins without reducing type size.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| Initial compile | failed | Local rect name collision in WindowStyle; corrected by renaming the surface variable. |
| Corrected source/model/media checks | passed | Editor/Windows/Android-symbol and Editor-tool compilation, model checks and existing media hashes pass. |
| First native/render review | passed | 100 checks COMPLETE 2026-11-13T00:02:42Z. Actual option screens reviewed; HNAI neutral contrast and compact label spacing then refined for final review. |
| Final native/render review | passed | 100 PASS checks COMPLETE 2026-11-13T00:06:06Z. Actual 4K portrait/landscape SoundHub, HNAI, Explorer, Research, 2.0, video and popup surfaces inspected. Neutral choices remain distinct; category labels fit; navigation, answer revision/reset, media and gestures pass. |
| Android package | passed | Build exited 0; APK 1,448,861,554 bytes; SHA-256 9d6be6ddfc0d3eefd87e816c067ea3337b8c223aebb3989a389fe3ef8cf6ad1c. v1/v2 signatures, all 57 media hashes/sizes and native video DEX class passed. Existing two META-INF coverage warnings remain. |
| Phone touch/install | not run | Deferred by user; no new installation attempted. |
| Bundled skill validator | failed | quick_validate.py cannot import yaml (PyYAML unavailable); no global dependency added. |
| Manual skill/links | passed | Required frontmatter and all affected Markdown file links verified, separately from the unavailable bundled validator. |
| Documentation publication | passed | Authorized Markdown published using expected-head protection, then fetched and compared; verified commit linked with delivery. |

## Performance

Not profiled; no speed or memory improvement claimed. Sheet geometry is rebuilt on normal UI invalidation, not by a new per-frame loop. No new textures, materials, audio processing or hierarchy polling are introduced.

## Limitations and follow-up

Source compilation does not verify appearance. Actual renders, native regression and package verification are recorded separately; phone testing remains deferred. This is a presentation change, not validation of scientific or clinical functionality.

## Rollback

Reverse only the listed Sheet/style/default-surface changes and the matching test assertions. Preserve original assets/GUIDs, media sources, scene, data, callbacks and unrelated work. Do not regenerate Main or delete visitor profiles. Verified prior APK HearingNotion-before-20261112-003.apk is retained, SHA-256 b285f5599640a1cf5297fe14ecc478d16317cf0c18d5957ff078bc7c42af262c.
