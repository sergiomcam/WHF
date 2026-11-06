# Android personal test build

Updated 2026-11-06 for the user's Acer AX85 / Android 13. A real APK has been built and verified. The phone was not connected, so installation and physical-device behavior remain pending.

## Verified build

| Item | Actual result |
| --- | --- |
| Project | Builds/AndroidPatched-2026-11-06; separate migrated copy; original desktop project remains on 2022.3.12f1 |
| Editor | Unity 2022.3.62f2, revision 7670c08855a9; listed as remediated for CVE-2025-59489 in Unity's advisory |
| Toolchain | Hub Android Build Support; OpenJDK 11.0.14.1; NDK 23.1.7779620; build tools 34.0.0; SDK platforms 34/35/36 |
| APK | Builds/AndroidPatched-2026-11-06/Builds/Android/HearingNotion.apk; 1,444,375,261 bytes, about 1.44 GB |
| Identity | org.hearingnotion.prototype; version 1 / code 1; Hearing Notion |
| Player | IL2CPP ARM64 + ARMv7; minimum API 23; automatic target selected API 36; Main is the build scene |
| Signing | Personal test/default debug key; apksigner verified v1 and v2; not store-release signing |
| Content | All 57 packaged media files match catalog SHA-256 values; 1,413,452,794 bytes of media payload |
| Regression | Patched Windows Editor passed 91 native checks, including 51 audio variants and five decoded nonblack videos; this does not establish Android playback |
| Phone | User reported not yet connected; adb listed no device; actual ABI, installation, touch, sound, video, memory and safe-area behavior unverified |

APK SHA-256: `902c21664bd198be149a84db95c9491ab602bacc9be2c9f7c99017bd32fb594c`.

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
