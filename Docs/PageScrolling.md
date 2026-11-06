# Page-wide scrolling gestures

Implemented 2026-11-05. FullScreenSwipeSurface on module screen roots forwards drag and mouse-wheel gestures from background/header areas to the visible vertical ScrollRect. Existing direct gestures inside lists still use their own ScrollRect. Buttons remain clickable; once a background/button drag becomes scrolling it is not treated as a click. No invisible overlay covers navigation controls, sliders, popups or game taps.

PageGestureInstaller waits six frames for existing runtime screens/content, installs surfaces once, and uses AppArtwork to keep the old module panel background transparent after resize to remove the heavy boxed appearance. Background gestures choose the active scroll region with the greatest overflow at gesture start; they reuse it until release. Discovery happens per gesture, not every frame. The demographic overlay has its own forwarding surface. Flappy Cloud is excluded so its tap mechanics remain intact; its large results panel scrolls normally.

Headers and bottom navigation stay fixed and accessible while the article/list scrolls. This is page-wide gesture routing, not a rewrite that makes every UI element move or removes clipping. Inner content remains clipped to prevent drawing over navigation. Native synthetic wheel/drag checks and rendered layout are distinct from real touchscreen testing. Manually check diagonal swipes, scrolling over buttons, mouse wheel and navigation in both orientations.

Source: Assets/_HearingNotion/Scripts/Navigation/FullScreenSwipeSurface.cs and PageGestureInstaller.cs, installed explicitly by AppManager. No scene, package or persistent-data changes. See [task report](Changes/2026-11-05-003-results-video-and-swipe.md).
