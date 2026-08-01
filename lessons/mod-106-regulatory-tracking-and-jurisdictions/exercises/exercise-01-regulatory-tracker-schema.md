# Exercise 01 — Regulatory Tracker Schema

**Estimated effort:** 2 hours
**Grounding chapter:** [01 — The Rolling AI Regulatory Tracker — Method, Schema, and Cadence](../01-rolling-regulatory-tracker-method.md)

## Objective

Author the enterprise's regulatory-tracker template and populate it with a seed row set covering at least one obligation from each of the six jurisdictional branches — EU, US federal, US state, UK, Canada, sector overlay. The template is the reusable schema every future tracker row will conform to; the seed populated rows are the day-one working tracker that subsequent exercises (02, 03, 04, 05) will extend.

After this exercise you should be able to sit down with a new obligation you have just noticed in the trade press, write a tracker row for it in five minutes, and know exactly which affected inventory rows and which counsel or specialist your row routes to.

## Prerequisites

- Chapter 01 read; the tracker's fifteen-column field shape, the jurisdiction taxonomy, and the refresh cadence fresh in memory.
- Chapters 02–06 skimmed for the specific instruments you will populate as seed rows.
- The MCDA and MCDA-Benefits worked examples from `mod-103` and `mod-105` open — the tracker's *affected inventory rows* column populates against inventory rows those examples already have.
- Any GRC-platform documentation your enterprise uses (from `mod-102` chapter 04's tour); the template you author here should be renderable into that platform's row shape as well as into Markdown.

## Problem statement

The deliverable is two Markdown files.

### Part 1 — the reusable tracker template

Author `mod-106-ex-01-regulatory-tracker-template.md` as an empty template a colleague could fill in for a new obligation. The template covers the full column set from chapter 01, plus a template-header block. Structure:

- **Header.**
  - Tracker version and date.
  - Author (analyst).
  - Refresh cadence adopted (weekly light touch, monthly deep read, quarterly cross-check, on-demand — cite the cadence and target session length).
  - Governance-artefact repository location and identifier convention.
  - Cross-reference to the inventory (`mod-102`) and the impact-assessment corpus (`mod-105`) — the primary consumers of tracker output.
- **Column schema table.** One row per tracker column, with:
  - Column name (exactly as it will appear in the row).
  - Field type (identifier, free-text, controlled vocabulary, date, URL, foreign-key list, tag list).
  - Controlled-vocabulary values if applicable (e.g., *status* takes one of *in force* / *phased — [date]* / *proposed* / *guidance — non-binding* / *voluntary code* / *rescinded*).
  - Required vs optional.
  - A one-sentence description of what populates the field.
- **Row template.** A blank instance of the tracker row with every column present and a one-sentence prompt explaining what to write. The template row is what the analyst copies-and-populates for a new obligation.
- **Cadence-and-review protocol.** A short section that documents the weekly / monthly / quarterly / on-demand cadence and the exact list of source checks per cadence tier (which regulator pages, which practitioner briefings, which state-legislative-tracking pages).

### Part 2 — the seed row set

Author `mod-106-ex-01-regulatory-tracker-seed.md` — the template populated with at least one row per jurisdictional branch, using the identifier convention `REG-<year>-<branch>-<sequence>`. Minimum viable seed set:

- **EU** — at least three rows: one AI Act (choose Article 5, Article 6+Annex III, Article 27, or Article 50), one GDPR (Article 22 or Article 35), and one CoE Framework Convention row.
- **US federal** — at least three rows: one civil-rights row (EEOC on Title VII/ADA), one consumer-protection row (FTC Section 5), and either an HHS or FDA row (Section 1557, HIPAA, SaMD, or PCCP).
- **US state** — at least three rows: Colorado AI Act (developer or deployer duties), NYC LL 144, and Illinois BIPA.
- **UK** — at least two rows: UK GDPR / DPA 2018 (with the Data (Use and Access) Act 2025 ADM provisions where applicable) and the UK principles-based cross-regulator row.
- **Canada** — at least two rows: TBS Directive on Automated Decision-Making and PIPEDA + OPC generative-AI principles. Include an AIDA horizon-scan row with the current status of any successor legislation.
- **Sector overlays** — at least two rows: one banking (SR 11-7 / OCC 2011-12) and one insurance (NAIC Model Bulletin), plus a medical-device row (FDA GMLP + PCCP) if the enterprise's use case supports it.

Every row populates every column of the template. Where a field does not apply, use `Not applicable — [one-line reason]`; do not leave blanks.

Every row's *affected inventory rows* column is populated. Use the MCDA (`INV-2026-0088`) and MCDA-Benefits (`INV-2026-0311` or the identifier used in your `mod-105` chapter 03 work) inventory rows from the earlier modules; extend to additional inventory rows if your enterprise's shape supports them. Empty (no affected inventory rows) is a valid answer for horizon-scan rows and for jurisdictional-branch rows the enterprise's operational footprint does not currently engage — say so explicitly.

Every row's *AIGP body-of-knowledge tag* column is populated per chapter 08's tagging pattern. Rows are often multi-domain; primary first.

## Requirements

- **The template's column schema names every column from chapter 01.** Do not compress; do not skip. The fifteen columns are the analyst-tier minimum; add columns if your enterprise's tracker shape needs them, but do not remove.
- **Controlled vocabularies are enumerated in the schema.** *Status* is not a free-text field; it takes one of the six enumerated values. The template names each and — where applicable — the shape they take (e.g., *phased — [date]* is a status pattern; the date is populated per row).
- **The row template is a blank copy of the row structure.** Not filled in; just the empty prompts.
- **The seed set covers every jurisdictional branch.** No branch is empty. A branch with no operational engagement is still represented by at least one row with a *no in-scope systems; retained for horizon-scan* note.
- **Every seed row cites a primary source.** The *primary-source URLs* column carries the regulation itself, not a practitioner-briefing summary. If a stable archived URL is available, prefer it.
- **Every seed row's *last-verified date* is populated with the date of your authoring session.** No stale dates on the day the seed set is delivered.
- **Every seed row's *affected inventory rows* column is populated** with either at least one inventory-row identifier or an explicit *no in-scope systems* note. Unpopulated (unwritten) is not an acceptable answer.
- **Every seed row's *AIGP body-of-knowledge tag* is populated.** Primary domain first. Verify current AIGP BoK domains against the IAPP page before quoting (chapter 08 needs-research marker).
- **Nothing is fabricated.** No invented statutes, no invented enforcement authorities, no invented supervisory-authority names. Every citation traces to a primary source; where you cannot verify a specific claim (e.g., the current AIDA-successor legislative status, the current EO stack), mark the field with `<!-- needs-research: -->` and note the specific source to check.

## Starter guidance

- Author the template first, then populate. If you find yourself adding a column while populating a seed row, the template is under-specified — go back and add the column to the template with a proper schema definition.
- The *scope trigger* field is where first-draft trackers are shallowest. A trigger that says *AI system processing personal data* is under-specified; a trigger that says *AI system processing personal data of EU-resident data subjects, deployed by a controller established in the EU or offering goods or services to EU-resident data subjects* is a working trigger. Aim for the second style.
- The *role* field is per-row and per-system. Do not assume the enterprise is always the *deployer* or always the *controller* — the MCDA (marketing copy draft assistant) may have the enterprise as *deployer* under the AI Act and *controller* under GDPR; the MCDA-Benefits variant may add *public-body-deployer* under Article 27's scoping filter. Populate the field per row honestly.
- On the executive-order row: date-stamp the row and cite the currently-in-force EOs by number and Federal Register document URL. If the EO stack has changed since you last checked, note the change and the source date. Do not cite an EO from an earlier administration as *in force* without verifying.
- On the AIDA horizon-scan row: mark the status as *proposed — [current parliamentary state as of session date]* with a `<!-- needs-research: -->` marker pointing at the current Parliament of Canada page. Do not cite the 2022 Bill C-27 as current unless you have verified it was re-tabled and is at a specific stage.
- On the UK Data (Use and Access) Act 2025 row: verify the enacted text's ADM provisions before quoting. The Bill's shape shifted through Parliament and the enacted text is the authoritative source, not any earlier committee-stage version.

## Acceptance criteria

- `mod-106-ex-01-regulatory-tracker-template.md` with header, column-schema table, blank row template, and cadence-and-review protocol. Every column named; every controlled vocabulary enumerated; every field's population prompt written.
- `mod-106-ex-01-regulatory-tracker-seed.md` with at least the minimum-viable seed set (three EU, three US federal, three US state, two UK, two Canada, two sector-overlay). Every row's every column populated (or explicit *not applicable* with reason). Every row's primary-source URL, last-verified date, affected-inventory-rows, and AIGP tag populated.
- The template and seed use the same identifier convention throughout.
- The cadence-and-review protocol section names the specific source checks per cadence tier.
- No fabricated statutes, authorities, or citations. Any specific-claim uncertainty is marked `<!-- needs-research: -->` with the source to verify.
- Nothing fabricated in the sense of invented inventory rows — use the MCDA/MCDA-Benefits identifiers from prior modules, or explicitly-mock identifiers you note as *illustrative — not a real inventory row*.

## Stretch goals

- **A GRC-platform-shaped export.** Render the template's row structure as a JSON or YAML schema suitable for import into a GRC platform. This is the shape `mod-102` chapter 04's platform tour framing anticipates. Route the design decisions back to the platform's row-schema documentation.
- **A completeness-check script.** Write a short Python script that reads a tracker Markdown or YAML file and reports rows with empty required columns, stale last-verified dates (older than the cadence-appropriate threshold), or missing AIGP tags. This is the first mechanical step toward automated tracker-hygiene monitoring.
- **A horizon-scan tab.** Author a separate section (or file) for bills-in-progress or newly-published-but-not-yet-effective instruments. Include the promotion rule that moves a row from horizon-scan to main tracker (effective-date-within-window; inventory-row-affected). Populate with at least three horizon-scan rows for the current state legislative session or Union-legislative-agenda.
- **An IAPP-tracker cross-check.** For each seed row, verify against the [IAPP Global AI Legislation Tracker](https://iapp.org/resources/article/global-ai-legislation-tracker/) or the [IAPP US State Privacy Legislation Tracker](https://iapp.org/resources/article/us-state-privacy-legislation-tracker/). Where IAPP's entry cites the same instrument, cross-reference; where IAPP's entry does not appear, note that the row is analyst-authored rather than IAPP-confirmed. IAPP is a secondary reference (chapter 08); use it as verification, not as evidence.
- **A per-audience filtered view.** Render three additional short documents — a DPO-filtered view (rows tagged AIGP D3), a CRO-filtered view (rows tagged AIGP D2 and D4), and an internal-auditor-filtered view (rows tagged AIGP D4 and D5). Each view is a subset of the tracker with the same schema, oriented around a specific audience's reading list.

## Deliverables

- `mod-106-ex-01-regulatory-tracker-template.md` — the reusable schema.
- `mod-106-ex-01-regulatory-tracker-seed.md` — the seed row set covering all six jurisdictional branches.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference template and one MCDA-shaped seed set. Yours will differ in the specific rows chosen and the exact controlled-vocabulary shapes; what should not differ is (a) the fifteen-column schema is present in the template, (b) the seed set covers every jurisdictional branch with primary-source URLs and current last-verified dates, (c) affected-inventory-rows is populated on every row, and (d) AIGP tags are populated on every row. A ten-row seed set with every column populated honestly beats a fifty-row set with half the columns empty; the point is to prove the template works, not to enumerate every obligation.
