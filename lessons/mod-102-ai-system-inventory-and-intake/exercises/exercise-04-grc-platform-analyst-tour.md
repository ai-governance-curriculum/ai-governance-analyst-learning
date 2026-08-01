# Exercise 04 — GRC Platform Analyst Tour

**Estimated effort:** 2 hours
**Grounding chapter:** [04 — GRC-for-AI Platforms at Analyst Level — and the Spreadsheet Fallback](../04-grc-platforms-for-ai-at-analyst-level.md)

## Objective

Get hands-on-adjacent familiarity with the GRC-for-AI vendor landscape at analyst tier — enough to sit in front of any of the platforms named in chapter 04 and *use* it without needing a two-week onboarding. Where the vendor does not offer a self-serve demo, you will substitute a documentation-driven tour and produce the same comparison memo. The deliverable is a memo you could hand to a hiring manager as "yes, I have driven these tools" evidence.

You should finish this exercise able to sketch, on a whiteboard, the intake-and-inventory workflow inside at least two of the four vendors covered in chapter 04, name the strengths of each, and produce a spreadsheet fallback that mirrors the same workflow.

## Prerequisites

- Chapter 04 read.
- Access to the internet, a professional email address (some vendors gate demo access behind corporate-email screening), and a note-taking surface.
- The vendor pages open in tabs: [Credo AI](https://www.credo.ai/), [Holistic AI](https://www.holisticai.com/), [ModelOp](https://www.modelop.com/), [ServiceNow AI Control Tower](https://www.servicenow.com/products/ai-control-tower.html). Read the product-page content; do NOT rely on third-party summaries.
- Optional: any of [IBM watsonx.governance](https://www.ibm.com/products/watsonx-governance), [Fairly AI](https://fairly.ai/), or the AI-governance module of your current employer's GRC tool.

## Problem statement

Produce a **comparison memo** and a **spreadsheet-fallback template**. The memo is written for an imagined governance-program lead who is choosing whether to adopt one of these platforms or stay on spreadsheets for another quarter.

### Part A — the platform tour (four vendors, ~20 minutes each)

For **each of the four vendors** listed in chapter 04 (Credo AI, Holistic AI, ModelOp, ServiceNow AI Control Tower), document:

1. **How the intake flow works.** What does the requester see? What conditional logic is prebuilt? What fields are required by default? Where does the tier tag get assigned — by the requester, by the analyst, or by the tool automatically from other fields?
2. **How the inventory / system-of-record view is shaped.** What is the primary key? What artefacts hang off a system record? Can an analyst see all open risk items, all controls, and all incidents for one system on one screen?
3. **How the control library is shaped.** Which framework crosswalks are prebuilt (ISO/IEC 42001 Annex A? NIST AI RMF subcategories? EU AI Act obligations? sector-specific overlays)? Is the Statement of Applicability a native view?
4. **How reporting / export works.** Can you export a reviewer pack for a single system? A regulator-shaped report? A council deck? What formats?
5. **What is *not* in the tool.** Every platform has gaps. Name at least two per vendor (e.g., "no native SR 11-7 crosswalk", "no built-in FRIA template", "workflow requires ServiceNow Now Platform license").

You do not need a paid subscription. Acceptable evidence sources, in priority order:

- **A hands-on demo.** If a vendor offers a self-serve trial or interactive product tour, use it and screenshot the intake and inventory screens.
- **A vendor-led walkthrough.** Many vendors offer "book a demo" calls that are within reach for a learner; if you take one, note the date and the sales-engineer contact for the record.
- **Published product documentation.** Every vendor has some — customer help centre, developer docs, or a public trust-centre page.
- **Public case studies and webinars.** Vendor-published, but with named enterprise customers who verified their use.

If the *only* evidence you can gather is marketing pages, say so explicitly in the memo — that is a real finding about the vendor.

### Part B — the spreadsheet fallback

Produce the spreadsheet-shape fallback described in chapter 04. The deliverable is a set of six files (or six sheets of one workbook) matching the chapter's file list:

- `inventory.xlsx` (or `.csv`, `.md`) — one row per system, using the schema you built in exercise-03.
- `risk_register.xlsx` — one row per risk item; columns for system link, risk type, owner, likelihood, impact, residual, evidence-attach, status.
- `control_matrix.xlsx` — one row per (system, control) pair; columns for status (implemented / not applicable with justification / gap), evidence link, last tested date, next test due.
- `vendor_review.xlsx` — one row per third-party AI-relevant vendor; due-diligence status and re-review date.
- `incidents.xlsx` — one row per incident (empty is acceptable; put a header row).
- `change_log.md` — one entry per material change.

Populate the inventory with the three rows from exercise-03. Populate the risk register with at least two entries per in-production system. Populate the control matrix with the top ten most-relevant controls for the in-production system (choose from ISO/IEC 42001 Annex A or NIST AI RMF subcategories — cite the exact identifier). Populate the vendor-review file with the third-party dependencies from your inventory rows.

## Requirements

- **The comparison memo is 800–1500 words**, structured as: one-paragraph executive summary; a per-vendor section following the five-question shape above; a comparison table with the vendors as columns and the five question areas as rows; a "which would you pick for the imagined program and why" paragraph; a "which would you pick against for the same program" paragraph; a "what the spreadsheet fallback gets you at zero platform spend" paragraph.
- **Every vendor claim is sourced.** Cite the vendor page, documentation page, case study, or demo screenshot. Any claim you cannot source is either dropped or marked `<!-- needs-research: -->`.
- **The comparison table is analyst-usable.** It should let a hiring manager see, in one glance, which vendor emphasises which capability. Use "yes / no / partial" or a 1-3 scoring scale with a legend, not free text.
- **The spreadsheet fallback is complete and internally consistent.** The system IDs on the inventory rows appear on the risk-register rows and the control-matrix rows; the vendor names on the third-party dependency column of the inventory appear on the vendor-review file.
- **Version-control discipline is demonstrated.** Every file has a header row (or frontmatter) capturing the last-edited date and the initials of the analyst; the change log has at least two entries for the exercise itself (an "initial draft" and one revision).
- **No fabricated vendor features.** If Credo AI publishes a "risk-report export" module and Holistic AI does not, do not claim Holistic AI does. If you are not sure, say so.
- **A one-paragraph reflection** at the end of the memo: which vendor's workflow felt closest to how you would actually work, which felt farthest, and what you would want to demo before a hiring-manager conversation.

## Starter guidance

- Give each vendor a fixed timebox — 20 minutes of tour, 5 minutes of note-taking. If you slip into "I have to understand every feature", you will not finish. The analyst-tier read is what an analyst does in the first month.
- ServiceNow AI Control Tower is deeply intertwined with the rest of the ServiceNow install; if you have never used ServiceNow ITSM, expect it to feel foreign. Note that as a finding.
- ModelOp's ModelOps lineage means the inventory view is closer to a model-registry-plus-governance-overlay than a standalone governance register. Say so.
- Holistic AI's technical-audit modules are more of a "what a data scientist runs" surface than a "what an analyst runs" surface. That is not a criticism, but it changes how the platform fits an analyst-tier workflow.
- Credo AI leans toward policy-as-code and templates. The strength is the prebuilt library; the risk is that the templates dictate the shape of your program.
- On the spreadsheet fallback, do not try to reinvent columns you already picked in exercise-03. Reuse the schema; the whole point is that the same schema works whether the tool is a spreadsheet or a platform.

## Acceptance criteria

- `mod-102-ex-04-memo.md` — the 800–1500 word comparison memo with the executive summary, per-vendor sections, comparison table, pick-for / pick-against paragraphs, and reflection.
- `mod-102-ex-04-spreadsheet-fallback/` (directory) — the six files (`inventory`, `risk_register`, `control_matrix`, `vendor_review`, `incidents`, `change_log`) in your preferred formats.
- Every vendor claim in the memo is sourced (footnote, hyperlink, or a note on the demo call).
- Spreadsheet-fallback rows are internally consistent — system IDs match across files, vendor names match across files, control IDs cite the ISO/IEC 42001 Annex A or NIST AI RMF identifiers.
- No fabricated vendor features; every uncertain claim is marked `<!-- needs-research: -->`.

## Stretch goals

- **A fifth-vendor comparison.** Add IBM watsonx.governance, Fairly AI, or the AI module of your enterprise's incumbent GRC platform (Archer / MetricStream / ServiceNow non-AI-Control-Tower configuration). Same five-question shape.
- **A tool-migration checklist.** Draft the runbook a governance program would follow to move from the spreadsheet fallback to a chosen platform without losing artefacts or history. Ten to fifteen steps.
- **A hiring-interview one-pager.** Take the memo and compress it into a 300-word one-pager that would answer the interview question "walk me through the GRC-for-AI vendor landscape and what you would pick for our environment".
- **A live-tool screenshot pack.** If you obtained demo access, capture and annotate five screens per vendor (intake, inventory, control library, reporting, admin) as a supplementary appendix. Redact any customer or PII data from screenshots.
- **A "spreadsheet-to-platform" data-migration script sketch.** Given your six-file spreadsheet fallback, sketch (in pandas or SQL) the transformation that would load each row into the corresponding platform table. Include the field-name mapping table.

## Deliverables

- `mod-102-ex-04-memo.md` — the comparison memo.
- `mod-102-ex-04-spreadsheet-fallback/` — the six-file spreadsheet-shape register.
- Optional stretch artefacts named clearly.

## Notes on evaluation

There is no "correct" vendor to pick. The reference solution in the paired solutions repo picks one vendor for the imagined program and defends the choice with sourced evidence; a memo that picks a *different* vendor with an equally-defensible defence is an equally-strong deliverable. The exercise's teeth are in the sourcing discipline (every claim tied to a page / doc / demo), the internal consistency of the spreadsheet fallback, and the analyst-tier framing of the memo.
