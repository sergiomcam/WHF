# Modification report — patched Android build

- Report ID: 2026-11-06-002
- Date: 2026-11-06 (America/Mexico_City)
- Type: build / fix / documentation

## Request and resulting behavior

The user authorized completing the patched Unity/Android setup and personal phone-build workflow. Unity 2022.3.62f2 and Android modules were installed, and a separate portable project was migrated without changing the open desktop project. The initial APK packaging attempt exposed an archive filename encoding defect; portable media names now use ASCII SHA-256 names with unchanged recordings and display metadata. Final build verification is recorded below.

## Modifications

| Main change | Script, document or asset modified | Purpose / effect |
| --- | --- | --- |
| Install authorized toolchain | External Unity Hub installation; no project source dependency replacement | Patched Unity Editor, Android Build Support, SDK platforms 34/35/36, build tools 34.0.0, NDK 23.1.7779620 and OpenJDK 11.0.14.1 |
| Isolated migration/build copy | Builds/AndroidPatched-2026-11-06/{Assets,Packages,ProjectSettings,PORTABLE-PROJECT.json,README-ANDROID.md} | Keep desktop work on 2022.3.12f1; migrate only the phone snapshot to 2022.3.62f2; generated copy is local and excluded from publication |
| Safe portable archive names | Tools/Android/prepare_android_project.py; portable Assets/_HearingNotion/Resources/MediaCatalog.json and Assets/StreamingAssets/HearingNotionMedia | Stable ASCII names avoid malformed UTF-8 in Unity-generated Android archives; retain labels, IDs, hashes and relative gains |
| Prevent recurring naming regression | Tools/Tests/validate_packaged_media.py | Assert ASCII portable catalog paths while retaining desktop Unicode support |
| Reproduce export preparation | Builds/AndroidAsciiPreparationCheck-2026-11-06 | Fresh local export verifies the changed preparation tool; not the deployable patched project |
| Deployment and feature record | Docs/AndroidDeployment.md; Docs/FEATURES.md; Docs/AppArchitecture.md; Docs/Test.md | Record actual toolchain/build evidence and remaining phone checks |
| Reusable QA guidance | Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md | Extend repeated export/QA procedure for isolated migration, real APK verification and phone authorization |
| Task traceability | Docs/Changes/2026-11-06-002-patched-android-build.md; Docs/Changes/README.md | Index the build, bug correction and results |

## Decisions and implications

Unity's [security advisory](https://unity.com/security/sept-2025-01) explicitly lists 2022.3.62f2 as remediated for CVE-2025-59489. The installed Editor reports revision 7670c08855a9. The original desktop Editor/project remains unchanged; this does not remediate later builds produced with the old Editor.

Unity migration automatically updated the portable manifest: feature.2d 2.0.1, Rider 3.0.36, Visual Studio 2.0.22, TMP 3.0.7, Timeline 1.7.7 and Visual Scripting 1.9.4. Resolved transitive dependencies include Collections 1.2.4 and Burst 1.8.21. No global package upgrades or hand-edited generated projects were used.

The first Gradle attempt failed at lintVitalAnalyzeRelease/ExtractAarTransform with malformed input at an accented filename. Python also failed to decode that generated AAR as UTF-8 at the same byte, supporting an archive encoding cause. Portable source files and their .meta files were renamed together; imported asset GUIDs and Main were preserved. A temporary local repair script applied the same naming rule to the already-migrated snapshot. Future exports use the maintained preparation tool. The desktop catalog, originals, instrument wording, audio processing and scientific claims were not changed. No visitor data was collected. Codex assisted the build procedure, diagnosis, scoped tooling fix and documentation; human physical listening/device validation remains separate.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| Hub installation | passed | All tasks completed successfully; Hub exit 0 |
| Existing source/model checks | passed | Editor/Windows/Android-symbol C# compilation, Editor helpers, deterministic game checks and media integrity; expected serialized-field warnings only |
| Patched native Editor regression | passed | 91 checks before packaging and again after ASCII path correction; final completion 2026-11-06T23:21:30Z; all 51 audio variants and five decoded nonblack videos; muted Windows Editor, not device listening |
| Main scene preservation | passed | SHA-256 identical between working and patched project |
| Portable content | passed | 57 files, 1,413,452,794 bytes; original and renamed copy hashes verified; fresh preparation tool run and validator passed |
| Initial APK build | failed | Gradle archive extraction rejected invalid UTF-8 filename; corrected by ASCII portable paths |
| Corrected APK build and signature | passed | Unity exit 0; 1,444,375,261-byte APK; aapt confirms org.hearingnotion.prototype, min API 23, target API 36 and both ARM ABIs; apksigner v1/v2 verification succeeds |
| Final packaged media | passed | All 57 hashes inside APK match catalog; APK SHA-256 902c21664bd198be149a84db95c9491ab602bacc9be2c9f7c99017bd32fb594c |
| Physical Acer AX85 / Android 13 | not run | User reported not connected; adb devices returned no phone; ABI, installation, touch, output, cache, focus and safe-area checks pending |
| Review skill structure | passed | quick_validate.py: Skill is valid; actual Android device workflow is not thereby validated |

## Performance

No optimization claim or comparable CPU/GPU measurements. Build times are tooling evidence, not runtime performance. The media payload remains approximately 1.413 GB; real installed size and device memory behavior require phone testing.

## Limitations and follow-up

This is a personal debug-signed test workflow, not store-release signing or public redistribution authorization. Media rights, physical listening levels, Android extraction/playback, offline operation and representative phone performance remain to be checked. No phone was connected or authorized during the initial checks.

Gradle 7.4.2 plugin compatibility warning notes testing through compile SDK 33; Unity's bundled AAPT2 override successfully built API 36. SDK package metadata read-only warnings did not prevent compilation. apksigner reported two META-INF entries outside v1 JAR protection while overall v1/v2 verification passed. These diagnostics are recorded rather than suppressed. The APK declares INTERNET permission for UnityWebRequest; no telemetry/cloud feature was added. See the deployment guide for warnings and installation steps.

## Rollback

Keep the original working project and older portable snapshot intact. To undo the tooling fix, restore only the two changed Python tools and the task's documentation; do not regenerate Main. The patched build snapshot and preparation-check folder are independent generated outputs and can be archived separately when no longer needed. Unity 2022.3.62f2 was installed alongside 2022.3.12f1; removing it through Hub is a separate user/system action and is not performed automatically. Do not uninstall an app containing real saved data merely to retry an install.
