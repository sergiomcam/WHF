# Noise basics

Implemented 2026-11-05 as an independent Home card and scrollable template-derived screen. The six-stage guided journey remains unchanged. Back/Home work normally; Explore sounds opens Exposure Explorer. Seven versioned entries in Assets/_HearingNotion/Resources/NoiseBasics.json cover dB, dBA, LAeq,T, LAeq,8h, LEX,8h, sound characteristics, and digital playback versus measured acoustic exposure. Definitions are currently English; the Spanish HNAI is unchanged.

LAeq,T is an energy-equivalent A-weighted level over a stated duration. LAeq,8h specifies an actual eight-hour averaging interval. LEX,8h expresses exposure relative to an eight-hour reference and can describe exposure of another duration. For a single exposure period, LEX,8h = LAeq,T + 10 log10(T / 8 hours). They coincide when T is eight hours. This screen is education, not a meter, dose calculator, legal compliance assessment or individual risk prediction.

## Verified primary references

| Subject | Source and context |
| --- | --- |
| Logarithmic dB, pressure reference, frequency, weighting and impulse/peak context | [OSHA Technical Manual, Section III Chapter 5](https://www.osha.gov/otm/section-3-health-hazards/chapter-5), revised 2022; physical definitions, not a universal exposure limit |
| Equivalent continuous level over T | [Scottish Government noise assessment glossary](https://www.gov.scot/publications/technical-advice-note-assessment-noise/pages/5/), 2011; energy-equivalent definition |
| Eight-hour normalization | [HSE L108](https://www.hse.gov.uk/pubns/priced/l108.pdf), third edition, Schedule 1 Part 1, printed page 30; reference duration 28,800 seconds. Occupational source used for the mathematical definition, not individualized medical advice |
| Why level and duration matter | [WHO safe listening Q&A](https://www.who.int/news-room/questions-and-answers/item/deafness-and-hearing-loss-safe-listening); general education, no app endorsement |
| Measurement context | [NIOSH understanding noise exposure](https://www.cdc.gov/niosh/noise/prevent/understand.html); workplace measurement context, not app microphone functionality |

References checked 2026-11-05. Content paraphrases definitions and displays source names per entry. The app does not acquire microphone data or infer acoustic levels from its volume slider. Implementation: NoiseBasicsController, appended ScreenId.NoiseBasics, ResponsiveScreenLayout. See [task report](Changes/2026-11-05-002-direct-listening-and-noise-basics.md).
