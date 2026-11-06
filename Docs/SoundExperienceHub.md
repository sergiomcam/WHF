# Sound Experience entry point

Implemented 2026-11-05. Home has one Sound Experience card and no separate Exposure Explorer card. The retained hidden template object is still available to startup code that clones its style. The new SoundHub route is appended to ScreenId without renumbering existing serialized values. SoundHubController clones an app-owned module template at runtime before media setup.

The hub offers two choices:

| Choice | Content and route |
| --- | --- |
| Soundscapes | Existing activity categories, provenance, prevention and 18 original/protected recordings; internally retains ExposureExplorer route |
| Hearing examples | Existing five music examples and their WHIS versions; clears the activity context before entering the existing SoundExperience player |

The player no longer repeats the 18-item soundscape catalog. Opening an activity shows only its selected comparison; opening Hearing examples shows the hearing-example list. A Sound Experience menu action returns to the hub. Existing stable activity IDs, source mappings, files and processing are unchanged. Three chart-only activities still have no invented recording. This is navigation consolidation, not new or newly validated DSP. The six-stage guided sequence remains unchanged; free exploration uses the hub.

Sources: Assets/_HearingNotion/Scripts/Audio/SoundHubController.cs, MediaExperienceController.cs, AppSession.cs, ResponsiveScreenLayout.cs and PageGestureInstaller.cs. See [report](Changes/2026-11-05-004-unified-sounds-and-whole-pages.md), [Explorer](ExposureExplorer.md) and [media](MediaPlayback.md).
