# Research & Sources

## Visitor experience

Open Investigación y fuentes from Home or the final guided stage. Four numbered tabs display the research progression in Spanish:

1. Piloto: INTER-NOISE 2025 pilot design, reported findings and limitations.
2. Fuentes: demographic activity reports and the original gender-comparison chart.
3. HNAI: preliminary factor analysis/internal consistency, model alternatives and validation needs.
4. YANS: supplied factor/sum figures and reported change following awareness, with missing metadata explicitly identified.

Use mouse wheel or drag/touch within the panel to read its full text and figures. Back, Home and Continue/Finalizar remain outside that region. Each tab returns the scroll to the top. Re-entry and visitor reset return to the pilot. The four stages describe the research progression; they do not establish that the same cohort participated in each study.

## Local source mapping

Only the six top-level reference files in the user-designated documentation folder were considered. Audiovisual contents was excluded from ingestion; no sound/video was decoded or copied.

| Stage | Reference and exact evidence used | Limits preserved |
| --- | --- | --- |
| Pilot | IN_2025_1074726.e11911e94ac54402be41.pdf, pp. 5–8: 50 students aged 18–24, mean age 20.9/SD 1.94; pilot 18-item questionnaire; 70% daily-noise awareness, 26% exposure-level knowledge, 26% reported protection use, 96% would consider protection afterward | Habitual use and future intention are different questions, not a measured behavioral pre/post change. Small pilot, variable settings/equipment, no causal or lasting-behavior claim. Historical uncomfortable-volume instructions are not adopted. |
| Demographics | Demographic exposure.png, original chart; Soundscapes description and design.pdf provides environmental/recreational/occupational context | Do not read exact bar percentages, infer sample sizes or treat reported activity prevalence as measured exposure/dose/risk. Do not assume this is the pilot or HNAI cohort. |
| HNAI | HNAI_FINAL.docx report: 318 initially/316 complete; 22 items; MINRES/oblimin; KMO .854; Bartlett χ²(231)=2957.93, p<.001; domain α .853/.667/.884, counts 9/5/8; RMSR .0554 vs .0363 | Preliminary evidence. Three factors retained theoretically despite statistical support for four; weaker exposure/impact domain; further validation needed. No clinical cutoff/scoring introduced. |
| YANS | Factor comp (Y1 Y2).png and Sum fact comp (Y1 Y2).png: sum 11.33 ±1.90 vs 10.76 ±2.12; displayed-central-value difference −.57; p<.001 and Cohen dz=−.364 | Sample size, test, ±/error-bar definition, version/coding and follow-up are not supplied in figures. Before/after sequence comes from researcher context. Do not infer favorable direction, causality, clinical benefit or actual protection behavior. Not an HNAI or visitor score. |

The original paper/Word document remain in the user's reference folder; the app bundles authored summaries and three figure PNGs only. No new external medical recommendations are introduced.

## Implementation

- ResearchSourcesController is initialized by AppManager, locates the existing screen and replaces its placeholder text with tab/scroll controls at startup.
- Resources/Research/ResearchStages.es.json contains versioned stage IDs, Spanish tabs/titles/body/source labels and figure resource paths.
- ResearchStage and ResearchStageCatalog are JSON data containers. Original PNGs load as textures once at initialization and are reused.
- Content height is calculated from TMP preferred height and figure aspect ratios. Reflow occurs when a stage or viewport width changes. Figures preserve aspect ratio and do not intercept input; the viewport accepts scroll/drag.
- Missing catalog/figure assets produce diagnostics; a missing catalog leaves an explanatory message. Required UI graphics explicitly include CanvasRenderer.
- No scene regeneration, route change, new package, backend, participant storage, audio playback or original-document file access is required at runtime.

## Verification

Content checks cover stage order, unique IDs, source fields, reported samples/statistics, figure references and absence of audiovisual files. App C# compiles for Unity 2022.3.12f1 Editor/Windows with existing Inspector CS0649 warnings only. The pilot's result pages and all three figures were visually inspected; HNAI report text was extracted directly from DOCX XML.

Unity Play Mode and device/visual interaction are not verified. Check all four tabs, source text, figure loading/labels, portrait/landscape resizing, mouse/touch scrolling, scroll reset, Back/Home, visitor reset, guided introduction/Finalizar and no overlap with navigation. Wide chart lettering may be small in portrait; readable textual summaries are provided, but a full-screen zoom viewer is not implemented. Confirm research owner approval of summaries and unresolved cohort/YANS metadata before public presentation.

## Current English presentation — 2026-11-06

ResearchSourcesController now loads Resources/Research/ResearchStages.en.json. ResearchStages.es.json remains the source-language record. The four study IDs, figure bindings and numeric values match; uncertainty and cohort distinctions remain explicit. Original figures keep their language. Tools/Tests/validate_english_content.py checks numeric-value multisets, study identities and figures; source links/claims remain those already documented. See [English UI guide](HomeRedesign.md) and [report](Changes/2026-11-06-006-rounded-english-interface.md).

## Stable stage layout — 2026-11-10

Four selectors occupy two fixed-height rows anchored to the top of the module; selection no longer uses proportional positions in an expanding panel. Summaries use measured wrapped-text layout, and figures use width-derived aspect-preserving heights inside a vertical stack. Whole-page expansion includes the selector offset. Research wording, numbers, figure paths and provenance remain unchanged.

Research PNG imports explicitly retain non-power-of-two source dimensions; original bytes and GUIDs are preserved. This prevents texture import from stretching charts before aspect-based layout.


## Additional traffic-noise references — 2026-11-17

All four existing research tabs now end with a separately labelled additional-reading bibliography, following each stage’s original source. English and Spanish catalogs retain the same citations and original publication titles. No fifth tab, scoring change or new scientific result is introduced. URLs are readable plain text in the existing non-rich-text summary; clickable external browsing is not implemented.

1. Manohare, M., Garg, B., Rajasekar, E., & Parida, M. (2022). An Experimental Investigation of Change in Human Brain Waves Due to Heterogeneous Traffic Noise. Proceedings of the 24th International Congress on Acoustics, Gyeongju, Korea, ABS-0650. [Source](https://www.researchgate.net/publication/364364200_An_Experimental_Investigation_of_Change_in_Human_Brain_Waves_Due_to_Heterogeneous_Traffic_Noise).

2. Manohare, M., Aletta, F., Oberman, T., Elangovan, R., Parida, M., & Kang, J. (2024). Cross-country variation in psychophysiological responses to traffic noise exposure: Laboratory experiments in India and the UK. The Journal of the Acoustical Society of America, 156(5), 3067–3079. [Source](https://doi.org/10.1121/10.0034242).

3. Manohare, M., Rajasekar, E., & Parida, M. (2023). Electroencephalography based classification of emotions associated with road traffic noise using Gradient boosting algorithm. Applied Acoustics, 206, 109306. [Source](https://doi.org/10.1016/j.apacoust.2023.109306).

4. Manohare, M., Rajasekar, E., & Parida, M. (2023). Analysing the Change in Brain Waves due to Heterogeneous Road Traffic Noise Exposure Using Electroencephalography Measurements. Noise & Health, 25(116), 36–54. [Source](https://doi.org/10.4103/nah.nah_58_22).

### Source review

Reviewed 2026-11-17. ICA metadata/title/authors and ABS-0650 were checked against the author-uploaded proceedings text; no DOI was established. JASA metadata/DOI were checked against the publisher PDF. Noise & Health DOI resolves to the publisher; title spelling, volume/issue/pages are corroborated by bibliographic records. Applied Acoustics DOI/title/authors were corroborated by the author ORCID record, but publisher retrieval failed, so direct publisher verification remains pending. These are bibliography entries only: no findings, sample sizes, model accuracy, causal effects or validation claims are imported. Full methodological appraisal and redistribution rights are not established; no papers, figures or raw data are copied.

See [modification report](Changes/2026-11-17-001-traffic-noise-references.md).
