# Guided experience

The Start guided experience button follows this sequence:

1. **Cuestionario HNAI:** complete the 22 Spanish items using the supplied five-point scale. Press Finalizar, then the outer Continuar button.
2. **Exposure Explorer:** browse categories, optionally select activities, then Continue/Continuar. Activity selection is not required.
3. **Sound Experience:** review the selected context. Audio remains unavailable; continue without playback.
4. **Hearing Health:** read brief recommendations on volume, breaks, distance and protection, then continue.
5. **Noise Meter:** an informational coming-later screen. It does not request microphone access or display measurements. Continue to the final stage.
6. **Research & Resources:** review the current research introduction. Finalizar returns to Home and ends guided mode.

The original 5–8-minute duration is a target requiring re-evaluation now that the full HNAI begins the experience. HNAI responses are local prototype drafts; no clinical scoring, export or research consent procedure is introduced by this flow.

## Introductions and navigation

Each stage shows a short Spanish modal introduction on its first visit in a guided run. Entendido or Escape dismisses it. It blocks underlying controls and moves keyboard focus to its dismiss button. Revisiting with Back does not repeat the popup. Starting the journey again or resetting clears popup history. The popup itself does not answer questions or advance a stage.

Free module exploration has no automatic introductions. Existing free-mode destinations are preserved: Health can continue to Takeaways. Returning Home exits guided mode. Starting guided mode again preserves the current visitor's HNAI draft; use Reset visitor session for a fresh visitor.

## Implementation

- GuidedJourney is the shared six-stage route and HNAI completion rule.
- NavigationManager starts HNAI, advances with completion checks and permits the informational meter only in guided mode. Music Lab remains unavailable.
- GuidedExperienceController initializes after module Start bindings, wires guided footer actions, creates the meter panel from the existing Health layout and creates a reusable modal overlay. The meter reuses the same responsive panel structure without adding a build scene.
- AwarenessCheckManager owns its guided Continuar button, enables it after completion and refreshes it when the screen is entered or answers change.
- AppManager ensures the controller exists even for an older scene instance. No scene regeneration is required.
- Popup copy does not promise unavailable audio, measurement, clinical scoring or full research resources.

Health recommendations follow general [WHO safe-listening guidance](https://www.who.int/news-room/questions-and-answers/item/deafness-and-hearing-loss-safe-listening), already used for activity tips. They are general prevention information, not a personal health assessment.

## Validation

Source compilation and executable route checks passed. Tools/Tests/GuidedJourneyChecks.cs verifies exact stage order, HNAI completion gating, optional sound-stage continuation, the meter stage, final return Home and exclusion of unrelated routes.

Unity Play Mode and visual/device validation remain pending. Check:

- Guided Start opens HNAI with its introduction; no hidden screen receives modal input.
- Unanswered/incomplete HNAI cannot advance through Continuar; after Finalizar, it can.
- Every stage continues in the requested order; Research Finalizar returns Home.
- Noise Meter is informational in guided mode and its home card remains disabled.
- Back does not replay introductions; restarting does. Free exploration shows no introductions.
- Reset clears answers and popup history, returns Welcome and leaves the interface usable.
- Portrait/landscape changes keep popup copy, dismiss button, content and navigation readable.
- Keyboard focus, Escape, pointer/touch interaction and modal dismissal behave correctly.
