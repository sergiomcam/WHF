# Traveling waves and visual refresh

This revision treats “improve the guy” as “improve the GUI.” It keeps the white/yellow identity while replacing the earlier faint, fixed-position sprite drift with a visible traveling-wave effect. This is a code-and-asset implementation; actual Unity rendering still requires verification.

## Background motion

- Two groups of seven fine contours traverse the screen horizontally in opposite directions, near the upper and lower portions of the screen.
- Each group travels for 10 seconds, rests for 4 seconds, and fades at entry and exit. Their schedules are offset by 7 seconds.
- Initial time is 2.5 seconds so a pass is visible when initialized; no pointer movement or resizing is needed.
- TravelingWaveGraphic builds the 2D contours directly in a Unity UI mesh. It does not depend on loading the earlier wave PNG or converting it into a sprite. The image asset is retained as a previous version, not deleted.
- AmbientWaveAnimation advances the clock with unscaled delta time. Inactive screens do not update; unfocused standalone players pause. The editor continues animating without requiring Game view focus.
- Wave geometry is clipped to the screen and placed behind controls. It does not move the text, cards or header and does not receive pointer events.
- **Ondas: activas/pausadas** on Home/Welcome freezes the contours into a static pattern and resumes them. This preference applies across screens for the current app run; it is not saved to disk.

The previous implementation moved a large, low-opacity image around a nearly fixed origin. The new timing moves a wave packet across the width of the screen instead. Explicit runtime initialization and resize updates remain in place. Existing/cloned artwork containers are initialized defensively rather than assumed to contain valid runtime state.

## GUI hierarchy and palette

| Use | Color |
| --- | --- |
| Background | #FFFEF8 |
| Cards and content | #FFFFFF |
| Warm panels | #F6F4EB |
| Body text | #4A4C49 |
| Secondary text | #686B63 |
| Borders | #DFDEDD |
| Primary actions | #FDD633 |
| Soft accents/takeaways | #FFF5C2 |
| Selected responses/categories | #EEC900 |

Home module cards are white with subtle outlines; primary actions stay yellow, and Takeaways uses soft yellow. Shared hover, pressed and disabled states apply to cloned module/questionnaire controls. The questionnaire's visible selection marker and gold selection remain intact. Smaller footer copy and positioning leave room for the Home motion switch. Header/background changes are decorative, not changes to instrument wording or scoring.

## Headphone artwork

The active header is `Assets/_HearingNotion/Resources/Artwork/headphones-hero-v2.png`, an isolated transparent yellow/white headphone illustration. It replaces the small composite city/concert image at runtime, making its silhouette clearer at header size. Original images remain in the project. The static sound-wave texture remains as a very faint background accent at 16% opacity.

The headphone PNG was generated with the built-in image generation tool, visually inspected in its output and checked for RGBA transparency. Actual source dimensions are 1254×1254. The UI texture importer preserves alpha, disables mipmaps/CPU read-write and limits the imported texture to 1024 pixels. See [Artwork history and full prompt](Artwork.md).

## Implementation

- `WaveTravel`: independently testable travel, rest and fade timing.
- `TravelingWaveGraphic`: bounded UI contour mesh; at most 4,480 vertices for two active bands, seven lines and 80 segments per line.
- `AmbientWaveAnimation`: clock and reduced-motion handling, replacing image-layer drift.
- `AppArtwork`: texture-independent wave setup, quiet background, transparent headphone header and outer-control styling.
- `RuntimeArtworkController`: explicit startup, navigation/viewport refresh, shared motion preference and Home switches.
- `AppTheme`: shared palette and button styling; runtime module controls use it when instantiated.

No new package, shader, external service, audio behavior or participant-data persistence is required. Additional UI geometry can affect canvas rebuilds; actual frame cost has not been profiled, so no performance gain is claimed.

## Verification and review

Source compiles against Unity 2022.3.12f1 for Editor and Windows configurations. WaveTravelChecks verifies visible initial phase, monotonic travel, rest/repeat, staggered bands and fade bounds. PNG alpha/contrast and serialized scene checks are recorded in the task report. These checks do not prove the Unity Game view displays the effect.

A generated motion-only GIF in tmp/previews illustrates the same timing/curve equations. It is a mathematical preview, not a Unity capture or runtime verification.

In Unity, exit Play Mode, allow importing/compilation, then press Play and observe for at least 15 seconds. Confirm waves cross the screen rather than merely oscillate. Toggle Ondas on Home, navigate to other screens, return, resize between portrait and landscape, and open/dismiss guided popups. Verify text stays readable, the headphone art does not overlap headings, motion controls remain reachable and no decoration blocks scrolling or clicks. Check frame time on the target demonstration device before treating the visual refresh as presentation-ready.

## Wave renderer dependency repair

The reported RectMask2D clipping exception occurred on Traveling sound contours. Its custom graphic now explicitly requires RectTransform and CanvasRenderer. Creation orders the renderer before the graphic; Awake/OnEnable ensure the dependency before calling base lifecycle methods, and animation initialization also checks reused objects. No renderer lookup is added to Update. Exit Play Mode and allow compilation before retesting so runtime objects are recreated. Editor/Windows source compilation passed; Unity clipping and actual movement remain unverified. See [report 010](Changes/2026-10-19-010-wave-canvasrenderer-fix.md).

## Soft contour ends

WaveTravel.EndOpacity applies a symmetric smoothstep taper over each outer 35% of the ribbon. TravelingWaveGraphic assigns separate alpha values to each segment endpoint, interpolated by the UI renderer. Both tips reach zero opacity; the central 30% retains its original opacity. This spatial taper complements the existing temporal fade and also applies in reduced-motion mode. Geometry counts, timing and palette are unchanged. Source compilation passed for Editor/Windows; inspect the actual entry/exit and paused state in Unity before confirming visual quality.
