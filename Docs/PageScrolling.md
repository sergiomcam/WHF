# Whole-page scrolling

Updated 2026-11-05. WholePageScroll replaces gesture forwarding as the main-screen architecture. Each ScreenView is itself the content of an outer full-viewport ScrollRect and RectMask2D. The screen’s original direct-child hierarchy stays intact for existing manager lookups. Page content, Back/Home/Exit and the bottom note scroll together. As of 2026-11-10, the branded header and five-action footer remain pinned to viewport edges; this supersedes the earlier all-elements scrolling design.

PageGestureInstaller waits for runtime content, wraps all screen roots once, and leaves the saved scene untouched. Inner module ScrollRects and their viewport masks are disabled; their content expands into the page. Long content extends the module panel and moves navigation/footer below it. Clipping occurs at the full viewport. Short screens retain some scroll travel. Game pages retain their tap mechanics while drag gestures reach the outer page; final results expand for reading.

ResponsiveScreenLayout restores/captures template placements around orientation changes. WholePageScroll accounts for the CanvasScaler viewport resolving a frame later, measures cached content heights and applies layout only when the required height changes. Background artwork keeps viewport proportions rather than stretching down an entire long article. Discovery of inner containers occurs on setup/navigation, not per frame; height checks use cached references. There is no per-frame forced Canvas rebuild.

Activity details and selected audio can request ScrollTo on the outer page. Root transform names and existing references remain valid after wrapping, preserving guided/navigation handlers. Scrolling resets to the top on entry. Demographic/listening popups remain separate modal overlays; the demographic field area retains its own scroll interaction. FullScreenSwipeSurface remains only for that modal; its prior fixed-navigation page behavior is superseded.

Native checks compare header, Back and bottom-note positions before/after scrolling, exercise wheel and drag, and capture both orientations. Real touchscreen feel, long-page usability and keyboard access still require device review. See [task report](Changes/2026-11-05-004-unified-sounds-and-whole-pages.md).

Rounded Home update (2026-11-06): Home overflow now includes the lower Takeaways, Waves and footer rather than compressing all cards. Responsive sizing watches logical Canvas dimensions as well as pixel dimensions. Native captures settle scaler/layout before reflow and distinguish top from bottom; physical device swipe feel remains pending. See [design](HomeRedesign.md) and [report](Changes/2026-11-06-006-rounded-english-interface.md).

## Research and footer expansion — 2026-11-10

Whole-page sizing includes the research selector offset and a footer allowance. The App footer is pinned by DockedScreenChrome rather than participating in lower-page travel. Research summaries/figures remain layout-managed; navigation and notes remain part of the scrolling page.

Flappy gameplay has no artificial page-height tail; Pause/Ready/Retry remain within the viewport, while long result text may expand its page when needed.

## Pinned navigation and simplified media — 2026-11-10

DockedScreenChrome caches chrome references and compensates outer ScrollRect travel after page reflow. It preserves direct-child lookup contracts and modal layering. The footer is 180 logical units in portrait (130 landscape) and touches the viewport bottom; the old 500-unit page allowance is reduced to 250. Flappy retains its immersive game layout. This replaces earlier requirements that branded chrome move with the page. See [modification report](Changes/2026-11-10-002-pinned-navigation-and-media.md).

Requested content targets clear the pinned header (270 logical units portrait, 150 landscape; immersive game retains 80), so automatic navigation does not hide the first song-menu row beneath chrome.

## Content-sized lower edge — 2026-11-10

The fixed 250-unit tail is removed. Module page height follows measured content growth and bottom-note bounds plus the pinned footer height and a 28-unit gap. At the bottom of the page the note ends 28 logical units above the footer box. Required content height is tracked separately from total overflow, so a changing panel still reflows when extra page travel remains zero. Home and immersive game layouts retain their own bounds. ScreenChrome rebuilds footer callbacks on application to each screen, including cloned roots whose runtime UnityEvent listeners do not survive Instantiate. See [report](Changes/2026-11-10-003-footer-volume-and-flappy.md).
