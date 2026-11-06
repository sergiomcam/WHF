# Android personal test build

Prepared 2026-11-06 for an Acer AX85 reported by the user to run Android 13. The portable project exists at Builds/AndroidPrototype-2026-11-06. No APK has been produced. Android Build Support, including its SDK/NDK and OpenJDK, is not installed for the current Unity Editor. The pinned 2022.3.12f1 baseline also predates Unity’s CVE-2025-59489 remediation and must be remediated before phone deployment; no editor upgrade or binary patch has been performed. A passing Android-symbol C# check is not an Android player build or a device test.

## What is prepared

| Item | State |
| --- | --- |
| Unity project | Separate app-owned/TMP project with current source, Main build scene and existing dependencies; working desktop catalog/settings preserved |
| Android identity/configuration | org.hearingnotion.prototype; Hearing Notion; IL2CPP with ARM64 and ARMv7; minimum API 23; automatic installed target SDK; APK with default debug signing for personal testing; engine remediation still required |
| Media | 57 verified files, 1,413,452,794 bytes (about 1.413 GB) of media payload; no desktop ExternalRoot or PlaybackPath in the portable catalog |
| Audio | Existing PCM WAV comparisons kept byte-identical, including common relative gains; packaged tinnitus preview included |
| Video | Existing H.264/AAC compatibility copies bundled; Android-specific on-demand extraction from APK assets into the app-private VideoCache before preparing VideoPlayer |
| Engine security | Unity lists 2022.3.62f2 as the remediated LTS release for CVE-2025-59489; choose a release marked patched in the official advisory, upgrade the separate export copy and rerun tests |
| Toolchain | Missing Android Build Support; install with Unity Hub before attempting a build |
| Phone | Model/Android version supplied by user; actual ABI, install, playback, storage, touch, safe-area and performance testing not yet performed |

The largest WAV is about 53.2 MB; buffered float decoding uses more memory than its file size. All five cached videos total about 183.2 MB. APK compression/installed size have not been measured. Leave several GB free for the app, installer and cache; the 1.413 GB figure is not an APK size prediction. The content copy is for local personal testing; public distribution still requires reviewing media/artwork licences.

## Build and run on the phone

1. In Unity Hub install a **security-patched 2022.3 Editor** with **Android Build Support**, **Android SDK & NDK Tools** and **OpenJDK**. [Unity’s CVE-2025-59489 advisory](https://unity.com/security/sept-2025-01) lists **2022.3.62f2** for LTS and a separate xLTS patch; verify the release in that table rather than assuming every higher patch number is remediated. Do not deploy an unremediated 2022.3.12f1 player. Use the Android components supplied for the chosen Editor.
2. Add/open **Builds/AndroidPrototype-2026-11-06** as a separate Unity project, selecting the patched Editor. Keep the working desktop project on its current version; take a copy before accepting the export’s upgrade and rerun the checks. Allow import/compilation to finish. In File → Build Settings, choose Android → Switch Platform. Main should be the enabled build scene.
3. Run Hearing Notion → Android → Configure personal test build. For a saved APK, use Hearing Notion → Android → Build personal APK; output is **Builds/Android/HearingNotion.apk inside the portable project**. Do not choose a path inside Assets. The build command and Android build preprocessor refuse the desktop external-path catalog and reports a missing Android module before building.
4. On the Acer, enable Developer options (usually Settings → About phone → tap Build number seven times), enable USB debugging, connect a data-capable USB cable and approve the computer’s RSA prompt. In Unity Build Settings select the phone under Run Device and use **Build And Run**. Do not publish a store bundle for this personal test.
5. Alternatively install the built APK with the SDK’s adb: `adb devices`, then `adb install -r <path-to-HearingNotion.apk>`. For compatibility diagnosis use `adb shell getprop ro.product.cpu.abilist` and `adb shell getprop ro.build.version.release`. Keep device serials/logs private. Android 13 exceeds the minimum API 23 setting; actual hardware/ABI support still requires this check.
6. Test offline before demonstration: About you → optional volume preview/Accept; HNAI; both sound branches and original/protection/WHIS variants; each video’s Play/Pause/Stop and Back while loading; full-page touch scrolling/orientation; both game rounds; reset, interruption/focus and restart. Start with low physical device volume. Confirm audio comfort by listening, not by the software slider alone.

The first build may need internet for Gradle/package dependencies; the installed demonstration is designed to use bundled media offline. A debug key is suitable for this local test, not a store-release signing strategy. Uninstalling the app removes its app-private saved demographic profile and media cache; do not uninstall a real study installation without a data decision.

## Rebuild and lifecycle

Tools/Android/prepare_android_project.py creates a **new** project folder and refuses to overwrite an existing export. Choose a new --output path inside the workspace after later source changes. It copies app-owned assets, TMP, Packages and ProjectSettings, selects existing compatibility videos, verifies every media copy, clears private machine paths and adds the preview to the catalog. Original research media and the working desktop catalog remain untouched. Do not run the older destructive scene generator.

MediaAssetPath resolves external desktop, ordinary StreamingAssets and Android jar URLs. Audio keeps buffered UnityWebRequest loading. Video extracts on demand to app-private storage using DownloadHandlerFile, uses native filesystem paths for VideoPlayer (download/jar URLs remain escaped), preserves timeout/cancellation/navigation cleanup and reuses one decoder. The video cache is authored media, not participant data, and may survive session reset. Use on-screen Back/Home controls; Android system-Back behavior is not comprehensively implemented or verified. Android extraction itself remains unverified until a player/device run; desktop portable playback does not establish jar behavior.

The isolated tests in this task used 2022.3.12f1. No migration to a patched Editor has been tested yet. Unity also provides an official application-patching route in its advisory; using that requires patch verification and signing review, neither performed here.

## Official references checked 2026-11-06

[Unity 2022.3 Android environment setup](https://docs.unity3d.com/2022.3/Documentation/Manual/android-sdksetup.html), [StreamingAssets on Android](https://docs.unity3d.com/2022.3/Documentation/Manual/StreamingAssets.html), [Android build/run workflow](https://docs.unity3d.com/2022.3/Documentation/Manual/android-BuildProcess.html), and [Android 64-bit Unity guidance](https://developer.android.com/games/optimize/64-bit). Google’s [supported-device list](https://storage.googleapis.com/play_public/supported_devices.html) lists Acer_AX85; that listing does not verify this particular phone’s ABI or current OS.

See [task report](Changes/2026-11-06-001-editor-dhwani-android.md) for actual checks and remaining blockers.
