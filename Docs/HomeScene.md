# First home scene

Open `Assets/_HearingNotion/Scenes/Main.unity` in Unity and press Play. The layout adapts to the Game view: landscape uses two columns, portrait uses one column. Canvas scaling keeps the full design visible at other aspect ratios. Main is the only enabled scene in Build Settings.

The home adapts Menu Template 1's rounded card sprite, TextMesh Pro typography, button styling, Canvas and EventSystem. The original vendor scene is unchanged. The phone status bar and unrelated template imagery are omitted for the desktop layout.

The six module cards follow the supplied reference. Exposure Explorer, Sound Experience, Hearing Health, Awareness Check and Research & Sources open app-owned introductory panels. Noise Meter is disabled and labeled coming later. Personalized Takeaways opens a separate panel. Start guided experience starts at Exposure Explorer; Continue follows Sound → Health → Awareness → Takeaways. Home returns to the module grid; Back uses navigation history.

Destination panels describe intended content and make unfinished interactions explicit. Audio, questionnaires, scoring, personal results and microphone input are not implemented in this scene. This pass uses English copy; Spanish content and language controls remain a subsequent step.

All UI objects, text, colors and persistent button actions are serialized and editable in the scene. Application Managers contains AppManager, NavigationManager and SessionManager. Each panel has a ScreenView; navigation holds the eight panel references. Keep Application Managers outside panel roots.

Source compilation and scene reference validation are automated. Unity Play Mode and visual inspection are still required: test every enabled card, guided Continue, Back and Home; confirm the disabled meter cannot launch; inspect text wrapping at 1920×1080 and 1280×720. No Unity Play Mode verification has been performed by this change.

`Tools/build_home_scene.py` reproduces this scene from vendor component definitions. It overwrites Main.unity and Build Settings, so do not rerun after manual scene edits without preserving them. Normal subsequent UI changes should be made in Unity.

ResponsiveScreenLayout on Canvas updates home cards and destination panels when the viewport changes, including Edit Mode previews. The camera uses a solid matching background. Source compilation, local scene references and fit calculations at six viewport sizes were checked; Unity visual and interaction checks remain required.
