# Exercise 01 — ISO 42005 Scaffold and Template

**Estimated effort:** 2 hours
**Grounding chapter:** [01 — ISO/IEC 42005 as the Impact-Assessment Scaffold and the Shared-Template Idea](../01-iso-42005-scaffold-and-shared-template.md)

## Objective

Author the enterprise's shared canonical impact-assessment template, shaped by ISO/IEC 42005, populated once from an already-authored NIST AI RMF MAP walk. The template is the source-of-truth document from which every regulator-shaped view (AIA, FRIA, DPIA, sector) will be generated in exercises 02–06.

After this exercise you should be able to sit down with any MAP-1-to-5 narrative from `mod-103` and produce a 42005-shaped canonical document in an afternoon, with none of the fields left `TBD` and every downstream regulator view reading from it rather than re-authoring the underlying facts.

## Prerequisites

- Chapter 01 read; the seven 42005 documentary elements and nine procedural steps fresh in memory.
- The MCDA MAP walk from [`mod-103` chapter 01](../../mod-103-risk-assessment-authoring/01-nist-rmf-map-walkthrough.md), including the four register entries from [`mod-103` chapter 02](../../mod-103-risk-assessment-authoring/02-iso-23894-risk-sources-overlay.md), open — you are populating a canonical document from that same narrative.
- The [ISO/IEC 42005:2025 abstract](https://www.iso.org/standard/44545.html), the [ISO/IEC 42001:2023 abstract](https://www.iso.org/standard/81230.html), and the [ISO/IEC 23894:2023 abstract](https://www.iso.org/standard/77304.html) skimmed as the standards-stack citation set.
- Optional: an enterprise-licensed copy of ISO/IEC 42005:2025 if available. Absent that, the analyst works from the public abstracts and the SC 42 committee summaries and marks specific-clause claims with `<!-- needs-research: -->`.

## Problem statement

The deliverable is two Markdown files.

### Part 1 — the reusable template

Author `mod-105-ex-01-canonical-impact-assessment-template.md` as an empty template a colleague could fill in for a new system. The template covers the seven 42005 documentary elements from chapter 01, plus a header block and a cross-reference block. Structure:

- **Header.**
  - Enterprise-assigned canonical-document identifier (`CDX-<year>-<sequence>`).
  - System name.
  - Version and date.
  - Author (analyst).
  - Reviewer(s) (risk owner, DPO where applicable, AI governance owner where applicable).
  - Approval status (draft / under review / accepted / superseded).
  - Related regulator views by identifier.
- **Cross-reference block.** The full block described in [chapter 08](../08-cross-referencing-artefacts-and-walk-discipline.md) — inventory row, risk register entries, bias-review note where relevant, model card, system card, datasheets, eval reports, vendor reviews, incident-response plan, monitoring dashboard.
- **§1 System description.** Prompts for purpose, deployment context, users, providers, deployment surface. One prompt per MAP subcategory the section sources from — MAP 1.1, MAP 1.3, MAP 1.4, MAP 2.1, MAP 2.2.
- **§2 Data description.** Prompts for training / evaluation / operational data at the level relevant to impact. Cite MAP 2.1 and MAP 4.1.
- **§3 Affected-stakeholder inventory.** Prompt sourced from MAP 1.2.
- **§4 Enumerated impacts and analysis.** A row-per-impact table with the columns from `mod-103` chapter 02 (Risk ID, Risk title, GenAI Profile hook, ISO 23894 source, NIST subcategory anchor, owner, inherent likelihood / magnitude, proposed mitigation, residual, status, evidence link) plus the two 42005-relevant additions (reversibility per impact, affected-population size).
- **§5 Treatment plan and residual acceptance.** Prompt for the mitigation set, control mapping, and the residual acceptance record (who accepted, on what date).
- **§6 Related-artefact references.** Empty by default — the cross-reference block near the head will already carry the IDs; this section is a place for narrative pointers ("see model card MC-XXX-XXXX Section 8 for the ethical-considerations development of RR-XXX-XXXX").
- **§7 Review triggers and cadence.** Prompt for the enumerated triggers plus the review cadence per tier tag from `mod-102`.

Every prompt in the template is one or two sentences; the template is not the essay. The template's job is to make the essay easy to write.

### Part 2 — the worked example

Author `mod-105-ex-01-canonical-impact-assessment-mcda.md` — the template populated from the MCDA MAP walk. Populate every field. Use the register entries RR-2026-0212 through -0215 verbatim. Where a MAP subcategory does not have a fact to feed a template prompt, mark the prompt *not applicable* with a one-line reason — do not leave blanks.

The MCDA is internal-only, so no regulator views apply. Populate the cross-reference block with the model card, system card, datasheet, bias-review note, eval report, vendor reviews, incident-response plan, and monitoring dashboard identifiers from chapter 08.

## Requirements

- **The template is regulator-agnostic.** No AIA / FRIA / DPIA / sector fields appear in the canonical template itself. Those extras will layer on top in exercises 02–06.
- **Every 42005 documentary element is a top-level template section.** Do not compress two into one; do not skip one.
- **Every template section names its MAP-subcategory sources.** A section prompt that does not cite the MAP subcategory it sources from is not a prompt — it is a stray heading.
- **The worked example populates every prompt in the template.** No `TBD`. A prompt with no fact gets an explicit `Not applicable — [one-line reason]` answer.
- **Register entries are reused verbatim.** The worked example does not re-word RR-2026-0212 through -0215 from `mod-103`; it cites them by identifier and reproduces only the columns the canonical template asks for.
- **The cross-reference block uses stable identifiers**, not names. `INV-2026-0088`, not "MCDA inventory row".
- **Nothing is fabricated.** ISO 42005 specific-clause quotations are marked `<!-- needs-research: -->` unless the analyst has a licensed copy of the standard open. External incident-database or benchmark citations are not required for this exercise; if introduced anyway, cite primary sources or mark `<!-- needs-research: -->`.

## Starter guidance

- Author the template first, populate it second. The discipline test is whether the template can produce a good worked example without any authoring intelligence in the template itself. If you keep having to add a template prompt while populating, the template is under-specified.
- The load-bearing template design decision: the *enumerated impacts and analysis* section is a table row-per-impact, not free-text. Free-text degrades to prose that a downstream regulator-view generator cannot read mechanically. The row schema lets the AIA / FRIA / DPIA views project the columns they need.
- On the *review triggers and cadence* section, resist the urge to over-enumerate. Chapter 01's MCDA example has six triggers; that is a good default. The list is a working list, not an exhaustive one; the annual review is where new triggers are added if the year surfaced them.
- On the cross-reference block, the ordering matters — inventory row first, register entries second, canonical document third, model card fourth. That is the intake-forward order the walk in chapter 08 relies on. Do not re-order.
- The 42005 abstract does not enumerate the seven documentary elements or nine procedural steps in the same words chapter 01 uses. That is fine — chapter 01 is the analyst-tier paraphrase, and every paraphrased element carries a `<!-- needs-research: verify verbatim wording -->` marker in the template. Reproduce the markers.

## Acceptance criteria

- `mod-105-ex-01-canonical-impact-assessment-template.md` with the header, cross-reference block, and seven 42005 documentary sections; every section prompt cites the MAP subcategory it sources from.
- `mod-105-ex-01-canonical-impact-assessment-mcda.md` with every template prompt populated from the MCDA MAP walk; no `TBD`; every register entry cited by identifier.
- The template is regulator-agnostic — no AIA / FRIA / DPIA / sector fields present.
- The cross-reference block uses stable identifiers throughout.
- The `<!-- needs-research: -->` markers are present on any specific-clause claim not verifiable from public 42005 abstract text.
- No fabricated statutes, incidents, or vendor names.

## Stretch goals

- **A JSON / YAML front-matter version of the template.** Render the template's header and cross-reference block as machine-parseable front-matter, and the seven documentary sections as an ordered list of section objects. This is the shape the GRC platform ingests. Route the design back to `mod-102` chapter 04's GRC-platform-tour framing.
- **A diff-against-a-second-worked-example.** Populate the template a second time against a *different* MAP walk (e.g., a hiring-AI use case from `mod-104` chapter 04's overlays). Diff the two populated documents; the diff shape shows what is system-specific vs template-machinery.
- **A completeness-check script.** Write a short Python or shell script that reads a populated canonical document and reports missing sections or unresolved `TBD` markers. This is the first step towards the mechanical cross-reference-walk automation in chapter 08.
- **A published-abstract citation-check.** For each specific-clause claim marked `<!-- needs-research: -->`, note the exact wording used and where in the ISO abstract or SC 42 committee summary it can be traced. This is the pre-work for an audit-facing revision that removes the markers.
- **A two-page compressed template.** Compress the template to a two-page shape suitable for a Medium-tier system where a full canonical document is disproportionate to the risk. Retain all seven documentary elements; cut prompt verbosity, not sections.

## Deliverables

- `mod-105-ex-01-canonical-impact-assessment-template.md` — the reusable template.
- `mod-105-ex-01-canonical-impact-assessment-mcda.md` — the MCDA-worked example.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference template. Yours will differ in prompt wording and in the specific sub-fields under each documentary element; what should not differ is (a) all seven 42005 elements present as top-level sections, (b) every prompt sourced from a MAP subcategory, (c) the worked example has zero `TBD` and reuses the `mod-103` register entries verbatim, (d) the template is regulator-agnostic — no AIA / FRIA / DPIA / sector fields. A clean 42005-shaped canonical template beats a longer one that has already imported a regulator's fields; the point of the shared template is that the regulator views are cheap to render from it, and that only works if the canonical shape stays neutral.
