# Modification report — current app GUI on the website

- Report ID: 2026-11-06-003
- Date: 2026-11-06 (America/Mexico_City)
- Type: assets / content

## Request and resulting behavior

Update the existing Canva webpage to show the latest actual app screen. Canva versions 8–9 replace the earlier illustrated interface with the existing authentic portrait Home render. The screenshot sits inside a CSS silver/charcoal phone frame; a shared transform inclines the screen and frame together. Canva confirmed publication to https://sergio-mcam.com/hearingnotion/.

## Modifications

| Main change | Script/document/asset modified | Purpose/effect |
| --- | --- | --- |
| Current GUI preview | External Canva design DAHZ_HY6Lg0, versions 8–9 | Uses existing Marketing/Screenshots/Home-portrait.png rather than invented interface text; no local screenshot changes |
| Device presentation | External Canva Code hero | Shared perspective, responsive phone sizing, accurate caption and alt text |
| Larger-image inspection | External Canva Code image panel | Replaces mispositioned fixed overlay with an inline expandable upright screenshot; Escape collapses and returns focus |
| Modification record | Docs/Changes/2026-11-06-003-website-current-gui.md; Docs/Changes/README.md | Records scope, evidence and rollback |
| Local proof image | Marketing/Website/current-gui-canva-2026-11-06.png | Native browser screenshot of the completed Canva page; kept local |

## Decisions and implications

Source is today's existing 2160×3840 Unity portrait capture, visually reviewed before upload. No ImageGen asset was created. Canva AI assisted HTML/CSS changes. Canva serves a resized 450×800 image; the source remains high resolution locally. Device framing is illustrative and does not imply a released mobile app. No Unity code, scene, dependency, GUID, build setting, questionnaire, participant data or data path changed. No app feature changed, so FEATURES.md is unchanged. Existing webpage copy and motion were retained.

## Validation

| Check | Result: passed / failed / not run | Evidence or reason |
| --- | --- | --- |
| Source capture review | Passed | Actual portrait Home includes Conciencia auditiva, Noise basics, About you and DHWANI future work; no entered personal responses |
| Desktop visual preview | Passed | Native Canva preview shows current screenshot within a coherently inclined phone |
| Initial overlay inspection | Failed, replaced | Full-page iframe centered image thousands of pixels below visible viewport; inline panel avoids fixed-overlay positioning |
| Expand/collapse and Escape | Passed | aria-expanded changed true then false after Escape |
| Publication | Passed | Canva displayed Your changes have been published; public URL references version 9 codelet cpzwy3d5695wj1a8 |
| Physical device testing / Unity compilation | Not run | Website preview update only; no Unity implementation change |

## Performance

Not measured; no performance improvement claimed.

## Limitations and follow-up

Canva controls hosted image resizing. Physical phone usability and the prototype's actual Android behavior are outside this webpage change. Canva publication succeeded and its editor preview rendered; the public embed still showed a blank loading frame during this session, so public visual rendering remains unverified.

## Rollback

Select Canva version 7 and republish the existing hearingnotion subpath to restore the earlier illustrated phone. Preserve other designs and current Unity files. Remove only this report and its index row if rolling back documentation.

