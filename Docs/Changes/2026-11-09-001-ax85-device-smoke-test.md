# Modification report — AX85 installation and first device smoke test

- Report ID: 2026-11-09-001
- Date: 2026-11-09 (America/Mexico_City)
- Type: validation / documentation

## Request and resulting behavior

Resume pending phone testing with the connected Acer AX85. USB debugging authorization was completed by the user. Installed the existing verified personal-test APK successfully and launched the app. The user confirmed the app was visible and Airport original audio played and stopped. Actual phone screenshots show Home, original Spanish HNAI, sound hub, soundscape details and nonblack educational video output. This is a first smoke test, not complete device certification.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Install existing personal-test app | External AX85: `org.hearingnotion.prototype`, version/code 1 | Streamed `adb install -r` succeeded; no uninstall, data clear or demographic submission. |
| Capture real device evidence | `LocalEvidence/Android-2026-11-09/` | Local startup, Home, HNAI, sound hub, Airport and video screenshots; includes initial locked-screen diagnostic, kept private. |
| Update deployment evidence | `Docs/AndroidDeployment.md` | Distinguish successful installation/initial playback from still-pending tests. |
| Update feature validation | `Docs/FEATURES.md` | Update F-024 and retain historical Editor-only limits. |
| Record test results | `Docs/Test.md`; `Docs/Changes/README.md`; this report | Document the first physical-device checks and open wrapping issue. |

## Decisions and implications

Used the existing patched Unity build; no compilation, rebuild, source change, scene change, dependency change, GUID change or schema change. The APK SHA-256 matched `b80dedcedf7a14012d38798ada0d0a9913136b2a0b8f7d63009f6c04c33a87c1`. Actual phone properties: Android 13, ARM64 support, 720 × 1640 display, approximately 217 GB available before installation. Serial and raw device logs are excluded from publication. Installation preserved app data; no optional local profile was saved or deleted. AI assistance performed scoped device diagnostics, installation, screen inspection and documentation; audible output confirmation came from the user.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| USB debugging authorization | passed | adb reported device after user enabled debugging and approved computer. |
| APK identity/hash and install | passed | Existing verified checksum; streamed installation returned Success; installed ARM64 package version/code 1. |
| Launch | passed | Activity start status ok; process existed; user confirmed visible app. Initial capture was behind the phone lock screen, not proof of app failure. |
| Home/HNAI/sound navigation | passed | Actual screenshots and visible button navigation; original Spanish questionnaire rendered with five choices. No answers submitted by automated test. |
| Page swipe | passed | Soundscape header and navigation moved offscreen while activity details became visible; controls reachable. This does not exhaust every gesture surface. |
| Audible original soundscape and stop | passed | User explicitly confirmed Airport sound played and stopped at low phone volume. |
| Educational video output | passed | Actual nonblack Health effects and Hearing loss video frames on device. Video audio, all five clips and pause/stop lifecycle not comprehensively verified. |
| Environmental category label | failed | Word breaks as Environmental across two lines within the narrow category button; cosmetic open issue. |
| Full physical regression | not run | Both game rounds/results, rotation, all media, focus interruptions, volume slider/startup order, reset and offline-network isolation still pending. Concurrent phone exploration changed screen positions, so automated tapping was paused. |
| New source compilation/profiling | not run | No runtime code changed; no performance conclusion claimed. |

## Performance

No profiling performed. Successful startup/playback does not establish frame-rate, memory or acoustic-safety guarantees.

## Limitations and follow-up

App remains available on the phone for further testing. Do not mark all Android checks complete. Confirm video audio/controls, protected and WHIS variants, game results, startup popup order, physical slider, rotation, safe areas, interruption/Back cleanup and offline operation. Improve category label wrapping in a scoped UI task. Do not infer validated sound levels from phone volume or subjective comfort.

## Rollback

Documentation changes can be reversed independently. Preserve the installed app and any later visitor data; do not uninstall or clear storage automatically. Original desktop project, APK and media were not modified. Local test captures can be archived separately; do not publish device screenshots containing private lock-screen information.
