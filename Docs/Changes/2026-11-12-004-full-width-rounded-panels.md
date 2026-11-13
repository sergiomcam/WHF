# Modification report — Full-width rounded section panels

- Report ID: 2026-11-12-004
- Date: 2026-11-12 (America/Mexico_City)
- Type: UI / fix / documentation

## Request and resulting behavior

Extend the rounded section frames to full screen width. Module background surfaces now use the actual scaled ScreenView width, while their rounded corners, palette and inner content padding remain. Popup/Home layouts and control geometry are unchanged. Codex assisted the scoped implementation and review.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Full-width decorative surface | Assets/_HearingNotion/Scripts/Navigation/WindowStyle.cs | Replace fixed horizontal overhang with screen-relative width; include inactive ScreenView ancestors. Only the background expands. |
| Width regression | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Measure module surface width against the scaled screen, retaining existing rounded-sheet and behavioral checks. |
| Portable mirror | Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Scripts/Navigation/WindowStyle.cs; Builds/AndroidPatched-2026-11-06/Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs | Apply the same scoped correction to the separate personal Android project. |
| Design/architecture guidance | AGENTS.md; Docs/HomeRedesign.md; Docs/AppArchitecture.md; Docs/AndroidDeployment.md; Docs/FEATURES.md | Document full-width backgrounds and unchanged content geometry, current validation and APK state. |
| QA/history | Docs/Test.md; Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md; Docs/Changes/README.md; Docs/Changes/2026-11-12-004-full-width-rounded-panels.md | Extend existing repeated layout-review skill and maintain traceability. |

## Decisions and implications

The user’s frames refer to the large section backgrounds; their inner options remain padded. ScreenView width is used in Canvas units rather than physical pixel width or a fixed 1080/1920 assumption. Inactive ancestors must be included because the single scene reuses inactive module panels. No artwork/assets/GUIDs, source scene, dependencies, data schema, questionnaires, media bytes/gains or participant storage change. Background decoration remains nonblocking and outside layout sizing.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| Source/model/media checks | passed | Editor/Windows/Android-symbol and Editor-tool compilation, existing model and media integrity checks. |
| Initial geometry review | failed | ExposureExplorer surface did not reach screen width while inactive; root ownership lookup skipped inactive ancestors. Corrected with includeInactive=true. |
| Final native/render review | passed | 100 PASS checks; COMPLETE 2026-11-13T00:20:55Z. Actual portrait/landscape renders show edge-to-edge rounded backgrounds with padded contents. Inactive/reused module width checks now pass; navigation, media, HNAI and scroll regression retained. |
| APK verification | passed | Build exited 0; APK 1,448,861,726 bytes; SHA-256 6fa23d68d7d5a6b9e9f7ab373545098364fafe34c49008dd9b674ecd2f811cc0. v1/v2 signatures, 57 media hashes/sizes and native video DEX class passed. Existing two META-INF coverage warnings remain. |
| Phone install/touch | not run | User previously deferred phone testing; no installation attempted. |
| Bundled skill validator | failed | Missing yaml/PyYAML import; no global dependency added. Manual frontmatter/links checked separately. |
| Manual skill/docs links | passed | Required frontmatter and affected Markdown file links resolve. |
| Documentation publication | passed | Authorized Markdown published with expected-head protection, then fetched and compared. Verified commit linked with delivery. |

## Performance

Not profiled; no performance improvement claimed. Width is calculated during existing styling/navigation/resize calls; no new per-frame polling, texture allocation or layout rebuild loop is introduced.

## Limitations and follow-up

Native geometry/render checks are separate from physical-device verification. Phone testing remains deferred. The change widens module backgrounds, not popup dialogs or option content.

## Rollback

Restore the prior fixed horizontal background overhang in WindowStyle and remove the matching width assertion. Preserve rounded styling, content padding, callbacks, source assets, scene and unrelated work. No data migration or scene regeneration is needed. Verified prior APK HearingNotion-before-20261112-004.apk is retained; SHA-256 9d6be6ddfc0d3eefd87e816c067ea3337b8c223aebb3989a389fe3ef8cf6ad1c.
