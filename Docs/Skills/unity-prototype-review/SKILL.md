---
name: unity-prototype-review
description: Test Hearing Notion Unity navigation, media lifecycle, game controls and responsive screens, capture authentic marketing screens, and document reproducible bugs and verified fixes. Use for recurring prototype QA rather than scientific analysis or unrelated projects.
---

# Hearing Notion prototype review

Use the current AGENTS.md, Docs/ETHICS.md and Docs/Test.md. This recurring workflow replaces improvised compile/playback checks used in earlier media and game fixes.

1. Establish the requested change and affected screens. Record Unity version, local media availability and whether the Main scene is already open. Preserve unsaved work; never open a second Editor against a locked project or close another session to run tests.
2. Run Tools/Tests/run_project_checks.ps1 with configured local Unity/Python paths. Record compiler failures separately from expected Inspector warnings and game/media integrity checks.
3. For native tests in the existing Main Editor, use the explicit PrototypeReviewRunner request described in Docs/Test.md. It uses muted playback and no real demographic submission. Confirm completion from LocalEvidence/prototype-review.txt; a request file or passing compile is not test completion. If UI control is needed, use the installed computer-use skill and returned window state.
4. Test the actual failure trigger, including Back during/after media loading, in-field game first-round actions, random noise pause/cleanup, direct soundscape toggles, listening slider/preview-only trim/Accept, startup popup order, midpoint default and unified sound hub, video controls and actual decoded nonblack frames, final game feedback, whole-page gestures that move header/navigation/footer and modal background blocking, form Skip/save/delete with synthetic values and reset. Check portrait and landscape. Never infer physical listening safety from muted engine playback.
5. Capture actual rendered app screens into Marketing/Screenshots. Inspect dimensions and images. Exclude real visitor data and do not invent working features. Mark unavailable or unverified captures honestly.
6. Fix reproducible, reversible project bugs within scope, rerun affected checks, and record root cause, evidence, changed files, outcome and remaining limitations. Stop a correction attempt after repeated equivalent failure and report the blocker; do not bypass permissions or change external/system settings.
7. Update the feature catalog, module guides, dated modification report, continuous history table and skill register as affected. Publish only authorized project-authored Markdown, preserving the remote head and verifying content. Local logs, media, screenshots, executables and private paths are not authorized for publication.

Inputs: current project, relevant failing behavior and optional synthetic test data. Outputs: local test evidence and authentic captures, scoped fixes and a reviewed modification report. Availability: explicit invocation by reading this file under Docs/Skills; automatic discovery is not claimed.
