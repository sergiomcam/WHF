# Noise artwork version 1

Generated with the built-in image generation tool. Both original PNGs are 1536×1024 and are saved in Assets/_HearingNotion/Resources/Artwork. No vendor art is overwritten. AppArtwork loads the textures locally and places them behind the screen content and in its header margin during Play Mode. Raycasts are disabled on both decorative images. Background opacity is 55 percent; opaque content panels preserve readability. Header placement adapts to portrait and landscape. No generated text is used, so headings remain editable/localizable Unity text.

## Final prompt set

Background:
Use case: stylized-concept. Create a finished raster background asset for Hearing Notion, a youth noise-awareness Unity application. Wide landscape 1536x1024 composition. Mostly pure white with very subtle pale warm-gray flowing acoustic wave contours and fine concentric ripple patterns only along edges, restrained buttery yellow #FDD633 and gold #EEC900 accents in lower right and upper left corners. Contemporary editorial paper illustration, very light and calm, beautiful subtle depth. Central 75 percent must remain near-white empty negative space for readable interface panels, no dark shapes behind interface. No text, no letters, no logo, no UI, no mockup, no border. Palette white #FFFFFF, gray #DFDEDD, charcoal #4A4C49 used extremely sparingly, yellow #FDD633. Generate the background alone.

Header:
Use case: illustration-story. Asset type: wide header illustration for Hearing Notion youth noise awareness app. Generate a standalone wide horizontal composition 1536x1024, with the important illustration confined to a shallow horizontal band across the center, clean white background. Refined editorial cut-paper illustration, playful yet professional scientific outreach. On the right two-thirds: sculptural yellow over-ear headphones, abstract speaker and flowing concentric sound waves, simplified urban building silhouettes behind, a tiny concert-stage silhouette at far right. White and pale gray layered paper surfaces, yellow #FDD633 and gold #EEC900 highlights, charcoal #4A4C49 thin details. Left third mostly blank white for a separate app heading overlay. No written words, numbers, logos, watermark, medical diagram, UI elements, or device frame. Soft natural shadows and crisp recognizable forms. Subject is sound and listening, not a medical diagnosis.

The generated images were visually inspected in tool output. Compilation is checked separately; actual image placement and device layout still need Unity Play Mode verification.


## Animated wave sprites

noise-wave-sprite-v1.png is a 1536×1024 RGBA sprite source with verified transparency (alpha range 0–252), generated using the built-in image generation tool. AppArtwork loads it and AmbientWaveAnimation creates two Unity UI Image sprites at runtime, behind the controls and header. Each layer drifts horizontally by at most 16 reference units and vertically by 8, over a 28-second cycle. Layers use 18% and 12% opacity; neither intercepts clicks. Only active screens animate. Motion uses unscaled time and pauses when the application loses focus. Header artwork and UI controls remain static.

During Play Mode, expand a screen's Animated acoustic waves object and enable Reduced Motion on AmbientWaveAnimation to stop motion. Speed and drift are exposed on that component. This setting is per screen and temporary, not yet a persistent app accessibility setting.

Final sprite prompt:
Use case: stylized-concept. Asset type: transparent 2D sprite layer for a Unity hearing-awareness app background. A single elegant bundle of smooth flowing acoustic wave contours sweeping diagonally from lower left to upper right, made from many very fine parallel curved lines. Pale warm gray #DFDEDD lines and a few soft yellow #FDD633 and gold #EEC900 lines, sparse delicate editorial style matching layered paper sound waves. Landscape 1536x1024, plenty of transparent negative space between and around the lines, no opaque white background, no objects, no headphones, no text, no shadows, no border. Fine subtle wave ribbon only, suitable for slow drifting animation behind a white app interface. Genuine transparent background.

Compilation and PNG alpha checks passed. Animation timing and placement still require Unity Play Mode verification.
