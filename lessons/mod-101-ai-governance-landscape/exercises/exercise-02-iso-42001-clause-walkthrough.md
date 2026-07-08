# Exercise 02 — ISO/IEC 42001 Clause Walkthrough

**Estimated effort:** 2 hours
**Grounding chapter:** [03 — ISO/IEC 42001 clause walkthrough](../03-iso-iec-42001-clause-walkthrough.md)

## Objective

Produce a one-page **clause map** for ISO/IEC 42001:2023 that (a) shows every top-level clause with its intent, (b) shows the parallel ISO/IEC 27001 clause, and (c) shows which analyst-tier artefact (intake questionnaire, impact assessment, risk register, model card, incident log, control-status report, etc.) provides evidence against each clause.

This is the map you will keep at your desk during an ISO 42001 program roll-out. Auditors will not ask you to recite Clause 6.1.3.2 verbatim; they will ask "show me the evidence for Clause 6." Your map is what tells you which folder to open.

## Prerequisites

- Chapter 03 read.
- Access to the ISO/IEC 42001:2023 standard. If your employer or study cohort does not have a purchased copy, you can work from (a) the ISO published table-of-contents / preview, (b) the Annex L / Harmonised Structure clause skeleton that ISO publishes openly, and (c) chapter 03 of this module. Do not paraphrase clause *content* you have not read; describe clause *intent* only.
- A markdown editor.

## Problem statement

Author a single markdown file, `mod-101-ex-02-clause-map.md`, containing:

### Section 1 — Clause map table

A table with columns:

| Column | Content |
|---|---|
| ISO/IEC 42001 clause | e.g., `4.1`, `4.2`, `4.3`, `4.4`, `5.1`, ..., `10.2` — top-level and second-level clauses within 4–10 |
| Intent | One sentence — plain language, not a copy of the ISO text |
| ISO/IEC 27001 parallel | The corresponding 27001 clause (should be structurally identical for 4–10) |
| Analyst-tier evidence | Which artefact from the analyst desk covers this clause — pick from {intake questionnaire, risk register row, impact assessment, model / system / dataset card, control-status report, SoA row, management-review pack, incident log, vendor review record, policy document, meeting minutes, other} |
| Owner | Who signs off (analyst / architect / head of governance / risk owner / legal / CISO / etc.) |

Fill in **every second-level clause under 4–10** (roughly 20–30 rows depending on how you break down the standard).

### Section 2 — Annex table

A short table covering **Annexes A, B, C, D**: name, one-line intent, analyst-tier interaction.

### Section 3 — Statement of Applicability (SoA) skeleton

A ten-row SoA skeleton showing *how* you would present Annex A controls to an auditor. Columns:

| Control ID (Annex A reference) | Control name (paraphrased intent — do not copy) | Applicable? (Y/N) | Implemented? (Y/N) | Justification | Evidence pointer |

Populate ten rows with **placeholder** control references and clear `TODO` markers where a real Annex A control reference is required. Do not fabricate control IDs from memory. Where you would normally pull the control name and identifier from the standard, write `<!-- needs-research: Annex A A.X.Y control reference from ISO/IEC 42001:2023 -->` so a reviewer can fill it in with the licensed copy.

### Section 4 — Reflection

3–5 sentences answering: **where does the AIMS create work an existing ISMS does not already do?** Point at the specific clauses where the ISO 42001 delta actually bites (hint: Clause 6 planning and Clause 8 operation, with the AI *impact* assessment being the biggest single addition).

## Requirements

- No fabricated clause content. If you cannot verify a clause's phrasing, describe *intent* only and cite chapter 03 or the ISO table-of-contents.
- The 27001 parallel column must match. Any clause 4.x maps to 27001 4.x; any clause 5.x maps to 27001 5.x; etc.
- Every analyst-tier evidence pointer must be an artefact taught somewhere in this curriculum (this module or a later one).
- The SoA skeleton must clearly signal placeholders vs real content — use `<!-- needs-research: ... -->` markers.

## Starter guidance

- Do not try to cover Clauses 1, 2, 3 — they are housekeeping.
- Do not try to cover every fourth-level subclause. Second-level (e.g., 6.1, 6.2, 6.3) is enough for the map to be useful without being enormous.
- Consider the shape of your target enterprise. A pure-SaaS shop puts different evidence under Clause 8 than a regulated bank. Pick one shape and be consistent.
- The Annex table (Section 2) is where you show you know the difference between Annex A (controls to consider), Annex B (implementation guidance), Annex C (objectives and risk sources), and Annex D (sector tailoring). Interviewers ask this.
- The SoA skeleton (Section 3) is a *skeleton*. You are not authoring a real SoA in this exercise — that is `mod-108` work.

## Acceptance criteria

- File `mod-101-ex-02-clause-map.md` present in your workspace.
- Section 1 covers all second-level clauses under 4–10.
- Section 2 covers all four Annexes.
- Section 3 has ten rows with visible placeholder markers where Annex A references would go.
- Section 4 reflection is present and non-generic — it should point at *which specific clauses* create AI-specific work.
- No fabricated clause phrasing; no fabricated Annex A control IDs.

## Stretch goals

- Extend Section 1 with a "**NIST AI RMF touchpoint**" column — for each 42001 clause, name the RMF function or category most closely aligned. This is the beginning of the framework crosswalk you will do properly in `mod-108-controls-and-compliance-evidence`.
- Add a "**GDPR Article 35 DPIA touchpoint**" column for clauses where the AIMS impact assessment overlaps the DPIA — analyst-tier work in `mod-105`.
- Add a short paragraph on where **ISO/IEC 42005:2025** slots into Clause 6.1 (AI impact assessment) — the AI-specific IA standard is expanded in `mod-105`.
- Publish your clause map as an internal wiki page at your employer (with permission) — this is a legitimately reusable analyst-tier artefact.

## Deliverables

- `mod-101-ex-02-clause-map.md`.

## Notes on evaluation

The reference deck in the paired solutions repo will show one defensible clause map. Yours should differ in evidence choices — that reflects *your* enterprise's evidence stack, not the reference implementation. The rubric is: (a) structural correctness of the clause map, (b) honest Annex A treatment (no fabricated IDs), (c) reflection actually names the AI-specific delta.
