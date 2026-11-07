---
name: canva-editable-flyer
description: Reconstruct a supplied Hearing Notion flyer or poster as editable Canva objects, preserving artwork and disclosing fidelity limits.
---

# Editable Canva flyer reconstruction

Inputs: reference poster, exact embedded artwork, requested wording/layout and destination. Output: Canva edit link, inspected preview and modification report.

- Inspect automatic image-to-design output before delivery. Verify primary headings and body paragraphs appear as richtext; a successful conversion can leave almost the entire poster flattened and OCR can alter wording.
- If extraction is inadequate, reconstruct text and panels in a native layout. A static HTML ZIP can contain one page with `data-document-role="page"`, explicit canvas dimensions and bundled local images, then be imported with Canva's documented file-import tool. Keep text live; use separate shapes and artwork. Preserve source image proportions/crop deliberately.
- Use recognizable line icons rather than unrelated Unicode placeholders. SVG imports may remain whole graphics; do not claim individual path editability without testing.
- Inspect the Canva editor's object list and actual screenshot. Check typography, wrapping, footer bounds and artwork. Compare with the reference and disclose remaining differences; editable reconstruction does not establish pixel identity.
- Each import creates a new design. Keep intermediate designs distinguishable and deliver only the reviewed final link. Do not delete prior designs or publish to a website merely to complete an import.
- Follow [project guidance](../../../AGENTS.md) and [ethics](../../ETHICS.md). Source imagery stays local/Canva unless its separate publication is authorized. Record the report and preserve unrelated private documentation.

Invocation: explicitly read this file. Automatic discovery unconfirmed. Dependencies: Canva connection, local UTF-8 authoring and ZIP support; no global installation required. Stop after a concrete unsupported import or access error rather than repeating identical conversions.
