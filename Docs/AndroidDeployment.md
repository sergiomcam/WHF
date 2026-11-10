# Android personal test build

Updated 2026-11-09: the verified APK is installed on the Acer AX85 / Android 13. Launch, portrait navigation, audible Airport original playback/stop and visible educational video output passed a first phone smoke test. Full device regression remains pending. Earlier build records below retain their original dates.

## Verified build

| Item | Actual result |
| --- | --- |
| Project | Builds/AndroidPatched-2026-11-06; separate migrated copy; original desktop project remains on 2022.3.12f1 |
| Editor | Unity 2022.3.62f2, revision 7670c08855a9; listed as remediated for CVE-2025-59489 in Unity's advisory |
| Toolchain | Hub Android Build Support; OpenJDK 11.0.14.1; NDK 23.1.7779620; build tools 34.0.0; SDK platforms 34/35/36 |
| APK | Builds/AndroidPatched-2026-11-06/Builds/Android/HearingNotion.apk; 1,444,413,354 bytes, about 1.44 GB |
| Identity | org.hearingnotion.prototype; version 1 / code 1; Hearing Notion |
| Player | IL2CPP ARM64 + ARMv7; minimum API 23; automatic target selected API 36; Main is the build scene |
| Signing | Personal test/default debug key; apksigner verified v1 and v2; not store-release signing |
| Content | All 57 packaged media files match catalog SHA-256 values; 1,413,452,794 bytes of media payload |
| Regression | Patched Windows Editor passed 94 native checks, including 51 audio variants and five decoded nonblack videos; this does not establish Android playback |
| Phone | User reported not yet connected; adb listed no device; actual ABI, installation, touch, sound, video, memory and safe-area behavior unverified |

APK SHA-256: `b80dedcedf7a14012d38798ada0d0a9913136b2a0b8f7d63009f6c04c33a87c1`.

The first build failed because a Unity-generated AAR marked accented ANSI filenames as UTF-8. The portable preparation tool now uses ASCII SHA-256 names while retaining labels, IDs and original bytes. The corrected build completed successfully with exit 0. Gradle warned that its bundled plugin 7.4.2 was tested up to compile SDK 33; SDK 36 nevertheless built successfully with Unity's supplied AAPT2 override. This is a tested local configuration, not a general compatibility claim. Signature verification reported two META-INF entries outside v1 JAR signature protection; overall v1/v2 verification passed. No warnings were suppressed.

## Install on the Acer

1. Enable Developer options on the phone (usually Settings → About phone → tap Build number seven times), then enable USB debugging. Connect a data-capable cable and approve this computer's RSA prompt on the phone.
2. Use the installed Editor's SDK/platform-tools/adb. Run `adb devices`; continue only when the intended device says `device`, not `unauthorized` or `offline`. Keep serials/logs private. Confirm `adb shell getprop ro.product.cpu.abilist` and `adb shell getprop ro.build.version.release`.
3. Install with `adb install -r <absolute-APK-path>`, then open Hearing Notion. Its launch activity is com.unity3d.player.UnityPlayerActivity. Do not uninstall an existing app with real saved data merely to retry a signing or storage error.
4. Allow several GB free for installation and cache. The APK is about 1.44 GB; installed size is not measured. Five cached videos total about 183.2 MB, and the largest WAV is about 53.2 MB before float decoding overhead.
5. Test offline: About you before volume setup; Skip/temporary/save/delete distinctions; HNAI; both sound branches and original/protection/WHIS variants; every video's Play/Pause/Stop and Back during loading; full-page touch scrolling, orientation and safe areas; both game rounds; reset, focus interruption and restart. Begin with low physical output volume and assess comfort by listening. Software gain is not acoustic calibration.

Android 13 exceeds minimum API 23, but a real install/run must confirm this phone. Android system Back is not comprehensively implemented; use the app's Back/Home controls. Public distribution still requires media/artwork licence review and a release-signing strategy. No store upload is performed.

## Rebuild safely

Tools/Android/prepare_android_project.py creates a new portable folder inside the workspace and refuses existing output. It copies app-owned assets, TMP, Packages and ProjectSettings; preserves existing compatible videos and WAV bytes; clears ExternalRoot/PlaybackPath; adds the tinnitus preview; assigns ASCII media names; and verifies every hash. AndroidAsciiPreparationCheck-2026-11-06 is a preparation test, not the patched deployable project.

Open or batch-run the separate export with the patched Editor; preserve the original open project. Migration automatically updated the portable manifest to TMP 3.0.7, feature.2d 2.0.1, Rider 3.0.36, Visual Studio 2.0.22, Timeline 1.7.7 and Visual Scripting 1.9.4; transitive resolution includes Burst 1.8.21 and Collections 1.2.4. Original desktop dependencies remain unchanged. Preserve the two-frame media initialization delay and existing GUIDs. Do not run the destructive scene generator.

For batch compilation, start with `-batchmode -buildTarget Android -projectPath <patched-copy> -executeMethod HearingNotion.Editor.AndroidPrototypeBuild.BuildApk -quit -logFile <log>`. The helper configures identity, IL2CPP, ABIs, rotation and default debug signing and builds Main to Builds/Android/HearingNotion.apk inside that project. The preprocessor rejects nonportable catalogs or missing media. Wait for the Unity process itself to exit; a persistent Gradle child daemon can outlive a process-tree wait. Record final BuildResult, inspect aapt metadata and apksigner verification, and hash media inside the final APK. Initial dependencies/build may require internet; this is separate from offline app operation.

MediaAssetPath handles desktop files, local portable StreamingAssets and Android jar URLs. Audio remains buffered to retain the native-reader crash fix. Videos extract on demand to app-private VideoCache via DownloadHandlerFile, then use native filesystem VideoPlayer paths. Timeout, cancellation/navigation cleanup and a single shared decoder remain. Cache contents are authored media, not participant data, and survive session reset. Android extraction and output remain unverified until the device run. The manifest contains INTERNET permission for UnityWebRequest; no new telemetry or cloud service was added by this task.

## Official references checked 2026-11-06

[Unity security advisory](https://unity.com/security/sept-2025-01), [Hub CLI reference](https://docs.unity.com/en-us/hub/hub-cli-reference), [Android environment setup](https://docs.unity3d.com/2022.3/Documentation/Manual/android-sdksetup.html), [supported dependencies](https://docs.unity3d.com/2022.3/Documentation/Manual/android-supported-dependency-versions.html), [StreamingAssets](https://docs.unity3d.com/2022.3/Documentation/Manual/StreamingAssets.html), and [build/run workflow](https://docs.unity3d.com/2022.3/Documentation/Manual/android-BuildProcess.html).

See [initial preparation report](Changes/2026-11-06-001-editor-dhwani-android.md) and [patched build report](Changes/2026-11-06-002-patched-android-build.md).

## Approved interface build — 2026-11-06

The current APK includes the rounded English presentation and balanced icon palette. Native regression passed 94 checks; actual top/lower-page/stopped renders were reviewed. The previous APK is retained locally as Builds/Android/HearingNotion-before-rounded-ui.apk inside the patched project. Signature v1/v2 and all 57 media hashes verify for the new APK. Original Spanish HNAI and original-language media/figures remain identified exceptions. Phone verification is still pending. See [design](HomeRedesign.md) and [report](Changes/2026-11-06-006-rounded-english-interface.md).

Shared-window build update (2026-11-06): current APK removes the Waves button, makes DHWANI purple and shares Home typography/rounded cards and fields across modules/popups. Final 94-check native run and stopped renders passed; corrected UTF-8 labels were inspected. Signature v1/v2 and all 57 media hashes verify. The preceding APK is retained as HearingNotion-before-shared-windows.apk inside the build output folder. Device checks remain pending. See [report](Changes/2026-11-06-007-shared-window-style.md).

## First physical-device test — 2026-11-09

USB-authorized AX85 reports Android 13, ARM64 and 720 × 1640. The unchanged verified APK installed successfully with `adb install -r`; package version/code 1 launched. Home, original Spanish HNAI, sound hub, Airport details and page swipes were inspected on-device. The user confirmed original Airport sound plays and stops; Health effects and Hearing loss videos produced visible nonblack frames. No profile was saved or deleted.

Full game, rotation, all media, interruptions, volume setup and offline isolation remain pending. Environmental category text wraps awkwardly in its button. Testing paused when concurrent exploration changed screen positions. See [device smoke-test report](Changes/2026-11-09-001-ax85-device-smoke-test.md).

## Interaction corrections — 2026-11-10

Source changes add Android Back routing with modal dismissal, native full-screen video entry, inline soundscape comparisons after context, left-aligned Spanish HNAI responses, stable research-stage geometry, larger Flappy playfield and explicit Ready before noisy play. Dark header/footer use procedural graphics and real routes. This task's rebuild/device status is recorded in the [modification report](Changes/2026-11-10-001-android-interaction-corrections.md); earlier APK hashes are historical until replaced by an explicitly verified build.

Current correction APK (2026-11-10): 1,444,588,487 bytes; SHA-256 `f74190e9069d6226b887d216966245e0327dff321b904bb21a311f6fc0c9411b`. Build/signature v1/v2/all 57 media hashes passed, followed by in-place AX85 installation. Final native regression passed 95 checks. Targeted physical checks passed for modal/route Back, research switching/figure proportions, HNAI alignment, inline layout, native video Pause/Back, and game Pause/Ready. The pre-task APK is retained as HearingNotion-before-20261110.apk inside the portable Android output. Comprehensive orientation/media/interruption testing remains separate.
