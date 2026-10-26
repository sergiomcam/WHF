# Hearing Notion — ethics and research integrity

Version 0.1 · Adopted 2026-10-26 · Responsible roles: project maintainer and research lead

This policy guides development, demonstrations and future research, including AI-assisted work. It records commitments, not proof of implementation, institutional ethics approval, legal compliance or clinical validity. Hearing Notion is an educational prototype without WHO endorsement.

## 1. Transparency

- Explain what a module does, what information it uses and what its outputs can support. Identify placeholders, assumptions, missing evidence and unverified behavior where they affect understanding.
- Distinguish observations, interpretations, approximations and proposals. Do not present simulated audio, chart estimates or game scores as direct health measurements.
- Record AI assistance in modification reports: affected code, text, artwork or analysis, checks performed and human review when available. AI output is not scientific evidence or independent validation.
- Disclose known funding, affiliations, commercial interests and ownership relevant to the work. Record unknowns rather than inventing declarations or implying institutional endorsement.
- Explain listening limitations, provide text alternatives and allow visitors to skip media or leave modules. Never require discomfort or imply a diagnosis from an educational interaction.
- Report failed checks and material defects. Compilation, hashes and numerical agreement do not prove usability, acoustic safety or perceptual/clinical validity.

## 2. Data management

| Information | Current boundary | Required handling |
| --- | --- | --- |
| HNAI draft answers, activity selections and game results | Temporary local session/game state; no participant persistence or export implemented for this experience | Reset between visitors; do not copy responses into logs, screenshots, reports or GitHub |
| Research consent/version fields | Session infrastructure exists | A boolean setter is not an approved consent procedure or completed research workflow |
| Existing audiovisual library and local catalog | Authored content loaded from an external folder; catalog contains private paths | Keep source media and configuration private; preserve provenance and permissions; avoid unauthorized copying or publication |
| Additional imported sound sources | Separate authored library persists in the app's local SoundSources directory | Session reset does not delete it; keep imported content review-pending |
| Logs, crash reports, backups and synchronization | Development and operating-system tools may retain copies | Inspect and redact before sharing; do not promise that local app logic prevents cloud backup or eliminates all traces |

Collect only information necessary for a stated purpose. Do not add accounts, telemetry, microphone recording, participant identifiers or persistent research responses by default. A local folder may be synchronized by the computer's cloud software. Session reset replaces app state; it does not securely erase memory or purge operating-system artifacts.

Before collecting or exporting research data, document the responsible researcher, purpose, fields, consent wording/version, access roles, storage location, retention period, deletion process, withdrawal limits and sharing plan. Establish applicable institutional review and legal requirements with the responsible institution before recruitment. Do not invent an approval number, retention period or participant contact. Explain voluntary participation and access to education without research participation. Establish additional safeguards before involving minors or other groups requiring them.

Keep research data and any re-identification key separate from public documentation. Participant codes are pseudonyms, not proof of anonymity. Share only authorized aggregate findings after checking disclosure risk, including small groups. Preserve source data under the approved governance plan and document transformations instead of silently overwriting originals.

## 3. Source veracity

Trace substantive scientific claims, numeric recommendations and simulation methods to identifiable sources. Prefer original papers, official standards, authoritative guidance and reference implementations. Search snippets, AI responses and unattributed diagrams are discovery aids, not verified evidence.

Record the following in the relevant module guide or review record when adding or revising scientific content:

| Field | Required record |
| --- | --- |
| Claim / content ID | Stable identifier and exact app claim or interpretation |
| Source | Author/organization, title, year, version, DOI or stable URL when available |
| Supporting location | Page, figure, table, section or implementation revision |
| Context | Population, sample size, design, units, measurement conditions and uncertainty; mark missing information |
| Derivation | Direct finding, calculation, interpolation, assumption, educational adaptation or AI-assisted draft |
| Review | Reviewer when supplied, review date, outcome and unresolved limitations |
| Rights | Attribution, license/permission and whether public redistribution is established |

Use explicit review states: **unreviewed**, **verified against source**, **supported with limitations**, **conflicting evidence**, or **withdrawn**. These labels define a procedure; they do not claim a complete source registry already exists. Read the supporting passage in context. Flag corrections, retractions, superseded guidance and conflicting findings when identified. Recheck changed claims and versions and review sources before public release. Never fabricate citations, missing sample details or exact percentages from plotted bars.

Project-specific boundaries remain:

- Keep the pilot instrument, refined HNAI and YANS distinct. Preserve supplied HNAI wording and response options; record explicitly authorized instrument changes and versions.
- HNAI psychometric evidence is preliminary. Do not invent clinical cutoffs, diagnostic interpretations or scoring rules.
- Reported activity prevalence is not measured exposure. Attitudes and intentions are not demonstrated behavior change. Do not assume that separate figures share a cohort.
- Preserve WHIS/protection method versions, input provenance, assumptions and checks. Maintain shared reference/variant gain. Do not claim individual hearing-loss equivalence, guaranteed protection or calibrated playback.
- Flappy Cloud scores describe gameplay. Current silent rounds cannot demonstrate a noise effect.

See [Research & Sources](ResearchSources.md), [WHIS](WHIS.md), [hearing protection](HearingProtection.md) and [media playback](MediaPlayback.md) for existing evidence and limitations.

## 4. Documentation procedures

Follow [AGENTS.md](../AGENTS.md) and the [modification-report template](Changes/TEMPLATE.md):

1. Identify the request, scope, source inputs and relevant current behavior.
2. Preserve stable IDs, instrument versions, asset GUIDs and original research/media inputs. Record parameters, reference/code revisions and hashes where useful. Hashes establish file identity, not truth or permission.
3. Save one dated report describing changes, decisions, actual checks, failures, limitations and rollback. Record modifications in a table connecting each main change to its affected scripts/documents/assets and purpose. Maintain a continuous history-index table with date, report, main changes and key modified files. Separate compilation, static checks, native/runtime tests, visual review and physical-device listening.
4. Update affected guides, the report index and the feature catalog for user-visible changes. Preserve history and identify superseding corrections rather than rewriting earlier results as if they had always been correct.
5. Publish only authorized project-authored documentation to GitHub. Inspect the latest remote state, preserve concurrent edits, avoid force-pushes and verify the published content. Exclude participant information, private paths, source media, credentials and vendor material.

Mark unpublished work as pending publication and unrun tests as not run. Implemented fixes are not automatically runtime-verified fixes. AI assistance and automation do not replace accountable review.

## 5. Responsibility, review and corrections

The project maintainer coordinates implementation and documentation; the research lead owns scientific claims, instrument decisions and research protocols. Identify a data custodian before persistent research collection. These are roles to assign, not claims that named appointments or approvals exist. Record when one person fills several roles and seek independent review for consequential scientific/privacy decisions when feasible.

Before public demonstration or research deployment, review the relevant evidence, data boundary, consent requirements, media rights, accessibility, device behavior and listening controls. Record reviewer and outcome. Resolve or clearly restrict affected material when evidence, permission or required safeguards are missing. This policy itself grants no institutional approval.

When an unsupported claim, material error or privacy incident is discovered: contain affected behavior/sharing, preserve only necessary diagnostic evidence, assess affected people/content, involve the responsible maintainer/research institution, correct the material and record the outcome. Follow applicable institutional incident procedures. Do not silently erase evidence or claim that notifications occurred when they did not.

Review this policy when collection, export, networking, methods, audience or publication scope changes, and before formal research use. Record revisions in [Modification history](Changes/README.md). Version 0.1 introduces commitments; it is not a completed ethics audit.
