# High-resolution app screens

Local folder: Marketing/Screenshots. The current set contains 21 authentic Unity camera/Canvas renders: eight app screens in both landscape and portrait, plus the first-round Flappy Cloud game-over screen and both setup popups in both orientations. Landscape files are 3840×2160; portrait files are 2160×3840. Dimensions were checked from the actual PNGs.

| Screen / state | Landscape | Portrait |
| --- | --- | --- |
| Home, including About you | Home-editor.png | Home-portrait.png |
| Noise basics | NoiseBasics-editor.png | NoiseBasics-portrait.png |
| Optional demographics | Demographics-editor.png | Demographics-portrait.png |
| Listening setup | ListeningSetup-editor.png | ListeningSetup-portrait.png |
| Spanish HNAI | AwarenessCheck-editor.png | AwarenessCheck-portrait.png |
| Exposure Explorer | ExposureExplorer-editor.png | ExposureExplorer-portrait.png |
| Sound Experience | SoundExperience-editor.png | SoundExperience-portrait.png |
| Hearing Health | HearingHealth-editor.png | HearingHealth-portrait.png |
| Research & Sources | ResearchSources-editor.png | ResearchSources-portrait.png |
| Flappy Cloud tutorial | FlappyCloud-editor.png | FlappyCloud-portrait.png |
| Quiet game over and choice buttons | FlappyCloud-round1-editor.png | Not captured |

These are rendered from the actual app-owned scene/runtime UI in an isolated Unity Editor copy, not painted interface mockups. Capture temporarily uses a camera-rendered Canvas at the requested dimensions, then restores settings. It does not save or modify the working scene. Screens retain prototype limitations and use no real participant responses. Representative Home, game-over, Noise basics and popup images were visually inspected; review the remaining images before publication, including typography, attribution and media/artwork rights. No claim of WHO endorsement, microphone functionality or a validated noise-performance experiment is made.

The images remain local and are not uploaded by documentation synchronization. Regenerate using [Test.md](Test.md) and retain the associated local run evidence. PNG dimensions do not establish target-device performance, audio safety or complete interaction accessibility.

The final native run verified 51 audio variants, five videos, synthetic demographic save/delete and first-round choices with no test errors; see [modification report](Changes/2026-11-05-001-prototype-review-and-media.md). The first capture implementation produced no files in batch mode and was replaced by synchronous camera/Canvas rendering; only the verified PNG set is presented as complete.

Updated capture/test evidence: [corrections report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).
