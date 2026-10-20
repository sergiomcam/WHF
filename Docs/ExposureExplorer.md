# Exposure Explorer

The Explorer now uses the supplied soundscape annex and demographic figure. See the [complete soundscape catalog and import guide](SoundscapeCatalog.md) for the 21 activity records, exact category mappings, classification caveats and local audio workflow.

Categories are Ambiental, Recreativo and Laboral. A source can appear in multiple categories while retaining one stable activity ID, one visitor selection and one audio mapping. Activity details use Spanish titles, scene/mix descriptions and visible provenance notes. Numeric sound levels and demographic percentages are not inferred or displayed as personal exposure.

Open Main.unity, press Play, select a category and open an activity. Scroll to add/remove it from the current visit or assign a local WAV/OGG/MP3. Explore this sound opens the selected context and assigned filename; playback is still pending. Takeaways reflects visitor selections. Reset clears visitor answers/selections/path-input UI but preserves the authored local audio library.

ExposureManager loads Resources/ActivityCatalog.asset, clones template-derived controls and builds a scroll area. ActivityDefinition stores category memberships and source/classification metadata. The local library is separate from session data and does not upload files to a service.

Source compilation, catalog/reference validation and import-rule tests pass. Actual Unity Play Mode, native dialogs, local-storage persistence/replacement, restart/reset and responsive rendering remain to be tested. See the checklist in the catalog guide.
