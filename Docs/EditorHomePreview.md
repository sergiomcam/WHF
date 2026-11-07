# Home visibility outside Play Mode

StoppedHomePreview is an Editor-only helper that displays a complete template-derived Home when Main is open and Play Mode is stopped. It includes current module cards, DHWANI future work, the white/yellow palette and artwork. Its footer says EDITOR PREVIEW - press Play to interact. Controls are visual previews; they do not administer questionnaires or play media while stopped.

The helper creates transient EditorOnly objects with DontSaveInEditor/DontSaveInBuild flags, clears button actions and removes itself before Play Mode. It does not regenerate or save Main.unity, duplicate the application managers, or add a runtime preview layer to builds. The real UI still initializes through existing runtime controllers. Menu commands Hearing Notion → Preview → Show stopped Home / Hide stopped Home let developers inspect the authored scene underneath.

The isolated CaptureIsolated entry renders the stopped Home in both orientations without entering Play Mode and without saving the source scene. Native compilation can perform an initial stale dependency pass while importing new files; only a completed final import/render is verification. Review real output rather than assuming an ExecuteAlways callback displayed it.

Source: Assets/_HearingNotion/Editor/StoppedHomePreview.cs; [task report](Changes/2026-11-06-001-editor-dhwani-android.md).

Rounded Home update (2026-11-06): StoppedHomePreview uses HomeMenuStyle and the same rounded card/icon components, English labels and current module order. Preview decoration is marked transient after layout, and the original scene is not saved. Stopped 4K portrait/landscape captures passed; the visible first viewport uses the roomier design rather than squeezing every module on screen. See [design](HomeRedesign.md) and [report](Changes/2026-11-06-006-rounded-english-interface.md).

2026-11-06 shared styling: The stopped preview no longer adds a Waves card and uses the updated DHWANI purple icon. The preview remains transient, noninteractive and excluded from Main saves/builds. See [report](Changes/2026-11-06-007-shared-window-style.md).
