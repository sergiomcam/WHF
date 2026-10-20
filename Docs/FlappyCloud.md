# Flappy Cloud — attention game

## Current experience

Open Flappy Cloud from either home menu after pressing Play. Choose Jugar / reiniciar, then tap/click the sky, use Subir or press Space to flap upward. Avoid the top/bottom boundaries and pass between paired penguins. Attempts end on collision or after 30 seconds. Score counts cleared gaps; feedback shows gaps and elapsed play time. Pausar/Reanudar and Escape pause/resume via the visible control; focus loss or app suspension pauses without automatic resumption. Inicio returns to Home. Leaving the screen or resetting the visitor discards the attempt. Nothing is saved or exported.

This is a silent practice game. Con ruido: pendiente is disabled. It does not demonstrate a causal noise effect or constitute a clinical/cognitive assessment. Practice, fatigue, input hardware and game familiarity would need consideration before interpreting any later comparison.

## Source and adaptation

The local FinalGame project's InfiniteRunnerEngine/Demos/FlappyCloud example was inspected: Flappy.cs applies upward velocity on the main action, its prefab supplies gravity, and FlappyCloudPenguin.cs arranges upper/lower scrolling obstacles. Hearing Notion implements this core loop independently in its existing uGUI scene. The full runner framework, FMOD, managers, post-processing, other scenes and thesis-specific logic were not copied.

One existing penguins-characters.png sprite sheet and its original .meta are copied into Assets/_HearingNotion/Resources/FlappyCloud. The cloud uses slice penguins-characters_4 and penguin obstacles slice penguins-characters_2, matching reference asset slicing. Original GUID and slice IDs are retained after a collision check. These local vendor assets are excluded from documentation publication; their inclusion does not establish redistribution rights beyond the user's existing asset license. No new artwork was generated.

## Architecture and authoring

- FlappyCloudRun: normalized playfield, gravity/flap, bounding-rectangle collisions, score, deterministic course seed, 30-second cap and three recycled obstacle pairs. Tick uses fixed 1/120-second steps.
- FlappyCloudController: runtime screen and menu registration, uGUI input, fixed-step accumulator, drawing, pause, result text and visitor/navigation cleanup. Frame delta is capped at 0.1 seconds; long stalls do not fast-forward a run. Controls and score text are updated on changes. No global timeScale change.
- FlappyCloudSettings: an authoring ScriptableObject at Assets/_HearingNotion/Resources/FlappyCloud/Settings.asset. The Distraction Noise AudioClip field is left empty. A later task can assign reviewed audio here; assigning a clip alone does not enable playback in this version.

ScreenId.FlappyCloud is appended to the enum. Main and Build Settings stay intact. Runtime cards clone the existing Exposure Explorer button with cleared actions. Responsive home layout reserves a seventh card; the game owns its anchored layout and excludes the generic module artwork. The six-stage guided experience remains unchanged.

## Future noise condition

Before activating a noise round, add deliberate playback controls, gain management/fades, immediate stop on pause/navigation/reset/focus loss and comfortable-level instructions. Review the audio's provenance, levels and distribution permissions. Define any comparison protocol and balanced ordering before making performance claims. No audio is selected, generated or played now.

## Verification

FlappyCloudChecks exercises idle input, flap lift, boundary collision, terminal state, restart, repeated-course determinism, gate recycling/scoring, 30-second completion and reset. The existing guided-route checks confirm its order and HNAI gate remain intact. Source compilation against Unity 2022.3.12f1 passed for Editor and Windows, with existing Inspector-field CS0649 warnings only. Sprite PNG/meta hashes match the source; menu rectangle calculations have no card/Takeaways overlap in either orientation.

Unity Play Mode, sprite rendering, keyboard/touch interaction, pause/focus behavior and device testing remain unverified. Test 1920×1080 and 1080×1920: confirm all seven cards, clear menu labels, cloud/penguin visibility, touch/Space/Subir flaps, collision, scoring, restart, completion, pause/focus/resume, Home/back and visitor reset. Resize during play/pause and confirm reachable controls and no clipping. Confirm no sound plays and Con ruido stays disabled. Profile the target device before setting performance expectations.
