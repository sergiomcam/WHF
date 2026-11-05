# Modification report — game choices, media review, demographics and QA

- Report ID: 2026-11-05-001
- Date: 2026-11-05 (America/Mexico_City)
- Type: feature / fix / content / tools / documentation

## Request and resulting behavior

Add first-round Try again/Continue, diagnose media, gather optional demographics on first launch with user-confirmed explicit local saving, archive official WHO guidance, prepare high-resolution marketing screens and provide Test.md for recurring computer testing and scoped correction. All work remains local except authorized project-authored Markdown publication. No formal study consent, analytics, microphone or noisy game condition is introduced.

## Modifications

| Main change | Script, document or asset modified | Purpose / effect |
| --- | --- | --- |
| First-round choice screen | Assets/_HearingNotion/Scripts/Game/FlappyCloudController.cs | Quiet game over waits for Try again or Continue below it; only Continue starts transition; final Retry remains |
| Fix findings from visual review | Assets/_HearingNotion/Scripts/Navigation/ResponsiveScreenLayout.cs | Fit the additional About you card without footer overlap and replace corrupted duration/placeholder punctuation |
| Optional demographics | Assets/_HearingNotion/Scripts/Core/DemographicPromptController.cs; Assets/_HearingNotion/Scripts/Data/DemographicProfile.cs; Assets/_HearingNotion/Scripts/Data/AppSession.cs; Assets/_HearingNotion/Scripts/Core/AppManager.cs | First-launch notice, optional fields, temporary continuation, explicit local-save consent, deletion and Home re-entry |
| Media correction | Assets/_HearingNotion/Scripts/Audio/MediaExperienceController.cs; Tools/Audio/prepare_video_compatibility.py; local MediaCatalog.json | Dedicated video audio route, local compatibility cache, timeouts and playback-position handling; preserve originals/common audio gain |
| Native QA and authentic renders | Assets/_HearingNotion/Editor/PrototypeReviewRunner.cs; Tools/Tests/run_project_checks.ps1; Marketing/README.md | On-demand native tests, compiler/model/media checks, synthetic demographic tests and 4K portrait/landscape Canvas/camera captures |
| WHO local library | Tools/Tests/fetch_who_references.py; ReferenceLibrary/WHO; Docs/WHO/README.md | Seven official source archives with provenance, hashes and context-specific public guide |
| Recurring QA skill | Docs/Skills/unity-prototype-review/SKILL.md; Docs/Skills.md | Focused explicit-invocation workflow with scope, evidence and privacy boundaries; recurrence evidenced by earlier media/game regression tasks |
| Document and protect boundaries | AGENTS.md; .gitignore; Docs/Test.md; Docs/Demographics.md; Docs/ETHICS.md; Docs/FlappyCloud.md; Docs/MediaPlayback.md; Docs/Marketing.md; Docs/README.md; Docs/FEATURES.md; Docs/Changes/README.md; this report | User-facing scope/status, local-evidence exclusions, updated ethics/data policy and complete traceability |

New C# metadata is grouped with its scripts and preserves existing GUIDs. Generated media/cache/screens/logs are local only; no source media or private paths are included in documentation publication.

## Decisions and implications

The user explicitly selected optional local demographic saving with a consent notice. A preference stores dismissal only; the five demographic fields and consent timestamp are saved only after the consent-labelled button. There is one local profile, not a participant database; HNAI remains separate. Device model is editable, with no device identifier or automatic location. Storage is under Application.persistentDataPath/Demographics; delete removes only the app profile, not OS/cloud backups. Runtime defaults and the ethics guide now describe this exception.

All linked source media passed hash checks. The initial muted native run played 23 audio examples and three videos; two original MP4s failed with Unity Cannot read file despite FFmpeg reading them. Five baseline H.264/AAC playback copies with normalized timestamps are now available in a private cache outside Assets; source files are unchanged. This mitigates native compatibility without claiming a precise underlying decoder defect. Buffered WAV loading avoids the previously documented streamed-clip crash. No original-project scene/build-setting or Unity dependency changes. A minimal isolated copy was used for native testing, preserving the open working Editor and vendor package.

## Validation

| Check | Result | Evidence |
| --- | --- | --- |
| Editor/Windows runtime and Editor-tool compile | Passed | run_project_checks.ps1; existing Inspector warnings and one intentionally test-set field warning |
| Flappy model and source media integrity | Passed | Existing gameplay checks; 28 records/56 source hashes/23 aligned sets/18 activity links |
| Video cache | Passed | Five H.264/AAC outputs decoded end-to-end; original hashes unchanged |
| Initial native regression | Partial / failures documented | All 23 original audio examples and three videos played; two original MP4s failed and were addressed with compatibility cache |
| Final native/visual regression | Passed for tested scope | 51 buffered audio variants and five videos playing; Back releases; synthetic age/temporary/save/delete; first-round buttons and both actions; no test errors or timestamp warnings; 15 real 4K PNG dimensions verified |
| WHO retrieval | Passed | Seven official HTML/PDF downloads, signatures where applicable, SHA-256 and source/resolved URLs recorded |
| Skill structure | Passed | Provided quick_validate.py; PyYAML installed only in ignored temporary tooling directory |
| Physical listening and other target devices | Not run | Muted native playback is not acoustic-level or mobile verification |

## Performance

No FPS or memory benchmark claimed. Media remains on demand; one buffered audio clip at a time. Video cache uses 720p H.264/AAC instead of original decode requirements. Marketing captures are high-resolution Unity renders; their creation does not establish interactive 4K performance.

## Limitations and follow-up

Review the final local evidence and selected screenshots before marketing use. No real visitor demographic profile was used in testing; synthetic records are redirected and deleted. A full research protocol/ethics review remains separate. The WHO folder is a selected reference archive, not a systematic review or endorsement. Test.md enables on-demand testing and scoped correction, not unattended background monitoring. Audio audibility, video speech, comfort and actual public-device behavior require human listening/device review.

## Rollback

Reverse this task's game-flow choices, optional demographic startup/model/controller, media routing/cache lookup and new QA tools if necessary; preserve the earlier buffered-audio crash fix. Do not delete any real demographic profile as part of code rollback without a separate data decision. Re-index original media without PlaybackPath to disable the cache; originals remain intact. Keep historical reports, reference provenance and metadata traceability. No source code/assets or participant data were uploaded to GitHub.
