# Optional demographic form

Implemented 2026-11-05 for local prototype use. Every launch shows an optional scrollable form: self-described gender, age in years, country, how the visitor heard about the app, and editable device model. “Genre” in the request is interpreted as gender. Model comes from SystemInfo.deviceModel; no serial number, unique device identifier, geolocation, name or contact details are collected by this feature.

All fields are optional. Age, if supplied, must be an integer from 0 to 120. Skip discards the inputs without deleting any previously saved profile. Save, after the explicit local-consent notice, saves a single profile.json under Application.persistentDataPath/Demographics, overwriting an earlier profile on that device. It includes the five fields, notice version, local-save consent flag and UTC save timestamp. This is a single local profile, not a multi-participant research database or a validated consent protocol.

The notice explains purpose, local-only saving, computer-owner access, retention until deletion and possible external backups. No network transfer is implemented. The visitor popup has only Skip and Save. Delete manually from the local application data folder, or use Android Settings > Apps > Hearing Notion > Storage > Clear storage (which also resets other app data). External backups are unaffected. No retention duration or institutional approval is invented. Do not use this convenience profile as consent for a formal study or recruit minors without appropriate procedures.

The legacy preference flag records dismissal only; it no longer suppresses the form at startup and contains no answers. You in the footer reopens the form to review the notice or save a replacement profile. Saved values are not automatically reloaded into the form or linked to HNAI responses. Session reset clears temporary demographics while leaving the explicitly saved local profile until deletion. Optional research export and telemetry remain absent.

Source: DemographicPromptController, DemographicProfile, AppSession and explicit AppManager startup. Review synthetic-value save/delete and both orientations in [Test.md](Test.md). Physical storage/permissions vary by device; the app shows an error if saving or deletion fails.

2026-11-05 UX update: Step 1 has scrollable fields, fixed two-row actions and a separate validation message. Closing it opens [Step 2 listening volume](ListeningSetup.md). Popup scope disables background screen interaction and restores it on close/reset. Demographic inputs clear on reset; local-save consent and storage schema are unchanged. See [corrections report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

Current sequence: About you always opens first, including after earlier dismissals. Continue/Skip then opens listening setup. The scrollable form also accepts drag/wheel gestures from its surrounding overlay through FullScreenSwipeSurface. No new storage, consent scope or fields. See [correction report](Changes/2026-11-05-003-results-video-and-swipe.md).

2026-11-06 shared styling: About you now shares Home typography, rounded white card/field surfaces, neutral borders and bold action labels. Optional fields, validation, Skip, explicit local-save consent and deletion are unchanged. The nested scroll viewport is transparent inside its card; synthetic test storage remains isolated. See [report](Changes/2026-11-06-007-shared-window-style.md).

## Compact content flow — 2026-11-10

The policy text, fields, optional validation message and two action rows share one scrolling content column. The empty message is collapsed rather than reserving a blank strip; action rows use fixed 112-unit preferred heights with 12-unit spacing rather than expanding into a large footer. The centered panel fits its measured content up to 90% of the available height; smaller screens scroll the complete form, including actions. Cached references and size-change checks avoid forced layout rebuilds every frame. All five optional fields, consent/save/delete behavior, storage path, startup order and synthetic-test boundary are unchanged. See [report](Changes/2026-11-10-004-compact-about-you-and-dhwani-mockups.md).

## Two-action form — 2026-11-11

Only Skip and Save remain visible in one fixed-height row. Save records the same explicit consent flag/timestamp; Skip writes nothing. Earlier four-action descriptions are historical. The private deletion routine remains for synthetic tests, with no visitor button. Manual/Android clear-storage deletion is explained in the notice. See [report](Changes/2026-11-11-002-reference-frames-and-startup.md).
