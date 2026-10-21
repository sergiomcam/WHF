# Flappy Cloud — attention game

## Current experience

Open Flappy Cloud from either home menu. Three brief popups explain tapping, button pause and the two-round sequence. Tap a free area of the screen (including the sky) or press Space to advance the tutorial and start/flap. A starting tap immediately gives the cloud lift. No Start/Subir/Pause buttons are needed.

Pausa is a separate button during play and the transition countdown; it changes to Reanudar when paused. Tapping the sky always flaps, even when taps arrive rapidly. A tap also resumes a paused round. Escape and focus loss still pause. Salir remains navigation and Retry appears only after both attempts.

The playfield fits inside its reserved region at a fixed width:height ratio of 0.85. Cloud/penguin dimensions follow their imported sprite aspect ratios. Penguin heads anchor to the gap; long bodies extend outside the clipped sky instead of being stretched to the boundary. Sprite ratios are cached at initialization. Original source images are unchanged.

Each round ends on collision or at 180 seconds. Speed rises from 0.20 to 0.38 field-widths/second over the first 45 seconds, then remains capped at 1.9×. Gate center spacing now varies from 0.48 to 0.66 field-widths; vertical gaps vary from 0.32 to 0.38 field-heights. Gate width is 0.14 to match the proportionate tall sprites in the narrow field. Gap centers are sampled from 0.24–0.76 field-heights, while adjacent centers change by at most 0.24 to keep the denser course navigable. Deterministic model checks include a full 180-second run; actual player difficulty still needs device review.

After the quiet round, a six-second notice shows its results and announces the next condition. The second round starts automatically. **Its audio remains pending, so it is explicitly labeled silent/noise pending.** No clip is loaded or played, even if the reserved field is assigned. The UI does not claim a real noise comparison. Each Retry generates a fresh seed; the two rounds within that session repeat the same seeded course and difficulty ramp; this does not control for learning/fatigue or establish a scientific protocol.

After the second attempt, the result area shows both scores/times and a single Retry gameplay button. Retry restarts the tutorial/quiet-first sequence. Leaving/resetting clears all results. No scores are persisted or exported. The six-stage educational guided route is unchanged.

## Source and adaptation

The local FinalGame project's InfiniteRunnerEngine/Demos/FlappyCloud example was inspected: Flappy.cs applies upward velocity on the main action, its prefab supplies gravity, and FlappyCloudPenguin.cs arranges upper/lower scrolling obstacles. Hearing Notion implements this core loop independently in its existing uGUI scene. The full runner framework, FMOD, managers, post-processing, other scenes and thesis-specific logic were not copied.

One existing penguins-characters.png sprite sheet and its original .meta are copied into Assets/_HearingNotion/Resources/FlappyCloud. The cloud uses slice penguins-characters_4 and penguin obstacles slice penguins-characters_2, matching reference asset slicing. Original GUID and slice IDs are retained after a collision check. These local vendor assets are excluded from documentation publication; their inclusion does not establish redistribution rights beyond the user's existing asset license. No new artwork was generated.

## Architecture and authoring

- FlappyCloudRun: normalized playfield, gravity/flap, bounding-rectangle collisions, score, deterministic course seed, 180-second cap and progressive speed and three recycled obstacle pairs. Tick uses fixed 1/120-second steps.
- FlappyCloudController: runtime screen and menu registration, tap/Space input, tutorial/automatic round transitions, fixed-step accumulator, drawing, pause, result text and visitor/navigation cleanup. Frame delta is capped at 0.1 seconds; long stalls do not fast-forward a run. Controls and score text are updated on changes. No global timeScale change.
- FlappyCloudSettings: an authoring ScriptableObject at Assets/_HearingNotion/Resources/FlappyCloud/Settings.asset. The Distraction Noise AudioClip field is left empty. A later task can assign reviewed audio here; assigning a clip alone does not enable playback in this version.

ScreenId.FlappyCloud is appended to the enum. Main and Build Settings stay intact. Runtime cards clone the existing Exposure Explorer button with cleared actions. Responsive home layout reserves a seventh card; the game owns its anchored layout and excludes the generic module artwork. The six-stage guided experience remains unchanged.

## Future noise condition

Before activating a noise round, add deliberate playback controls, gain management/fades, immediate stop on pause/navigation/reset/focus loss and comfortable-level instructions. Review the audio's provenance, levels and distribution permissions. Define any comparison protocol and balanced ordering before making performance claims. No audio is selected, generated or played now.

## Verification

FlappyCloudChecks passes idle input, flap lift, collision, terminal state, restart, deterministic input/course replay, gate recycling/scoring, 180-second completion, a height range exceeding 0.4 field heights, 1.9× speed by 45 seconds and tighter spacing/gaps and reset. Editor/Windows source compilation passed with existing Inspector CS0649 warnings only. These model checks do not verify the Unity UI state transitions or actual input feel.

Unity Play Mode/device checks remain: all tutorial popups, tap-to-start/flap across free screen areas, dedicated Pause/Reanudar control and rapid flap taps, pause/resume without accidental jump loss, focus/suspension during both play and transition, quiet-round collision/timeout, six-second notice, automatic second attempt, final Retry, Salir, visitor reset and portrait/landscape layouts. Confirm audio-pending text and no playback. A future audio task still requires safe gain/fades, stop-on-interruption and explicit user listening instructions before enabling real noise.

## Blue and red collectibles (2026-10-21)

Stars appear before the obstacle pairs and move with the course. Blue stars add 10 points; red stars subtract 10 points, including below zero. Each disappears after contact and can score only once, then is reset when its obstacle slot is recycled. The point total is separate from cleared gaps. Both round results include points, and retry/navigation/session reset clear them. Star colors and +10/−10 labels identify the reward/penalty. Tap/tutorial instructions explain the rule.

Three star objects are reused. CollectibleStarGraphic draws a code-native five-point silhouette with explicit RectTransform/CanvasRenderer dependencies, avoiding image tint distortion or additional asset imports. FlappyCloudRun handles contacts and score; the existing three-minute speed/pause/two-round flow remains. Both conditions still have no noise playback.

Checks cover blue +10, red −10, disappearance, no duplicate score, negative total and reset, alongside the existing complete-course regression. Unity rendering, collision feel, color/label readability and pause/transition behavior remain to inspect in Play Mode.

## Randomized course (2026-10-21)

Retry and re-entry generate a fresh session seed; both attempts in that session use it. Initial and recycled gates sample new spacing, height and gap size. Spacing changes the interval between arrivals, while the existing speed ramp continues. Stars sample their lead distance (0.20–0.29 field-widths), height (within ±0.10 of the associated gap center) and type (65% blue probability, not a fixed quota). The collision and rendering paths use the same sampled coordinates/gaps. Points remain ±10.

Gravity, flap strength, sprite proportions, three-minute limit and point values stay predictable. This variability is bounded rather than randomizing player controls. A repeated seed reproduces its course, permitting regression checks; the seed is temporary and no visitor data is stored. Model checks cover 1,000 initial seeds, valid geometry and existing three-minute simulation/scoring. Bounds do not establish every randomized course is equally easy or scientifically comparable; actual play review remains needed.
