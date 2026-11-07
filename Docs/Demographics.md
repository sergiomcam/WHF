# Optional demographic form

Implemented 2026-11-05 for local prototype use. Every launch shows an optional scrollable form: self-described gender, age in years, country, how the visitor heard about the app, and editable device model. “Genre” in the request is interpreted as gender. Model comes from SystemInfo.deviceModel; no serial number, unique device identifier, geolocation, name or contact details are collected by this feature.

All fields are optional. Age, if supplied, must be an integer from 0 to 120. Skip discards the form inputs; Continue without saving uses temporary session state. Save locally (I consent) saves a single profile.json under Application.persistentDataPath/Demographics, overwriting an earlier profile on that device. It includes the five fields, notice version, local-save consent flag and UTC save timestamp. This is a single local profile, not a multi-participant research database or a validated consent protocol.

The notice explains purpose, local-only saving, computer-owner access, retention until deletion and possible external backups. No network transfer is implemented. Delete saved profile removes that local file and current session demographic state, but cannot remove copies in OS/cloud backups. No retention duration or institutional approval is invented. Do not use this convenience profile as consent for a formal study or recruit minors without appropriate procedures.

The legacy preference flag records dismissal only; it no longer suppresses the form at startup and contains no answers. About you on Home reopens the form to review the notice or delete the local profile. Saved values are not automatically reloaded into the form or linked to HNAI responses. Session reset clears temporary demographics while leaving the explicitly saved local profile until deletion. Optional research export and telemetry remain absent.

Source: DemographicPromptController, DemographicProfile, AppSession and explicit AppManager startup. Review synthetic-value save/delete and both orientations in [Test.md](Test.md). Physical storage/permissions vary by device; the app shows an error if saving or deletion fails.

2026-11-05 UX update: Step 1 has scrollable fields, fixed two-row actions and a separate validation message. Closing it opens [Step 2 listening volume](ListeningSetup.md). Popup scope disables background screen interaction and restores it on close/reset. Demographic inputs clear on reset; local-save consent and storage schema are unchanged. See [corrections report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).

Current sequence: About you always opens first, including after earlier dismissals. Continue/Skip then opens listening setup. The scrollable form also accepts drag/wheel gestures from its surrounding overlay through FullScreenSwipeSurface. No new storage, consent scope or fields. See [correction report](Changes/2026-11-05-003-results-video-and-swipe.md).

2026-11-06 shared styling: About you now shares Home typography, rounded white card/field surfaces, neutral borders and bold action labels. Optional fields, validation, Skip, explicit local-save consent and deletion are unchanged. The nested scroll viewport is transparent inside its card; synthetic test storage remains isolated. See [report](Changes/2026-11-06-007-shared-window-style.md).
