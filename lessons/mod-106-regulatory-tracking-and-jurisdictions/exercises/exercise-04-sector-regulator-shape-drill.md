# Exercise 04 — Sector Regulator Shape Drill

**Estimated effort:** 2 hours
**Grounding chapter:** [06 — Sector Regulators — FDA GMLP, Banking Model Risk, and Insurance Actuarial Oversight](../06-sector-regulators.md)

## Objective

Author the analyst-tier sector-overlay branch of the tracker for the three anchor overlays — medical device software (FDA GMLP + SaMD + PCCP + MDR/IVDR), banking model risk (SR 11-7 / OCC 2011-12), and insurance actuarial oversight (NAIC Model Bulletin + EIOPA + state analogues) — and pair each overlay with a **specialist-routing note** that names the enterprise-internal counterpart the analyst hands off to. The drill also produces a short **applicability drill** across three deliberately-mixed inventory-row scenarios so that you build the muscle for recognising when an inventory row inherits a sector overlay and when the overlay is out of scope.

After this exercise you should be able to sit down with a new inventory row, identify within a page which of the three overlays attach, name the specialist inside the enterprise who owns the sector-specific depth, and produce a specialist-routing note that hands off cleanly without collapsing the analyst's tracker discipline into the specialist's workflow.

## Prerequisites

- Chapter 06 read; the three overlays (medical / banking / insurance), the specialist-routing table, and the *not jurisdiction-nested* framing fresh in memory.
- Chapter 07 read; the *question, not conclusion* discipline that applies to sector-specialist routing as much as to counsel routing.
- Chapter 10 skimmed; specialist-routing notes are a close cousin of change-notes and use the same *primary / secondary / tertiary* routing pattern.
- The seed tracker from exercise 01 open — the sector-overlay rows you populate here extend the `REG-2026-SEC-*` branch you already seeded.
- Primary sources open in adjacent tabs: [FDA Good Machine Learning Practice guiding principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles); [SR 11-7 (Federal Reserve)](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) and [OCC Bulletin 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html); [NAIC Model Bulletin on the Use of Artificial Intelligence Systems by Insurers](https://content.naic.org/sites/default/files/inline-files/2023-12-4%20Model%20Bulletin_Adopted_0.pdf); [EIOPA opinion on the use of AI in insurance](https://www.eiopa.europa.eu/publications/opinion-artificial-intelligence-governance_en).

## Problem statement

The deliverable is three Markdown files.

### Part 1 — the sector-overlays tracker extension

Author `mod-106-ex-04-sector-overlays-tracker.md` — the sector-overlays branch of the tracker, extending the exercise-01 seed. Structure:

- **Header block.** Version, date, author, cross-reference to the exercise-01 seed file, and a one-sentence note that this branch is not jurisdiction-nested — a single overlay applies across whichever jurisdictions the enterprise operates in that are covered by that sector regulator.
- **Three overlay sub-sections** — medical, banking, insurance — each containing at minimum:
  - **Medical (`REG-2026-SEC-MED-*`).** Five rows minimum, per chapter 06's minimum-viable list:
    - FDA SaMD framework + 21 CFR Parts 807 / 814 / 820 transitioning to QMSR (with the [2 February 2026 QMSR compliance date](https://www.federalregister.gov/documents/2024/02/02/2024-01709/medical-devices-quality-system-regulation-amendments) noted).
    - FDA PCCP guidance for AI/ML-enabled devices.
    - FDA GMLP guiding principles.
    - UK MHRA and Health Canada analogues (co-authored on GMLP; local implementation).
    - EU MDR ([Regulation (EU) 2017/745](https://eur-lex.europa.eu/eli/reg/2017/745/oj)) and IVDR ([Regulation (EU) 2017/746](https://eur-lex.europa.eu/eli/reg/2017/746/oj)) where the enterprise's software qualifies as a medical device or IVD.
  - **Banking (`REG-2026-SEC-BANK-*`).** Five rows minimum:
    - SR 11-7 / OCC 2011-12 supervisory guidance on model risk management (with the three components — development / validation / governance — noted in the row body).
    - Model-inventory requirement (implicit in SR 11-7; explicit in internal-audit expectations).
    - [Interagency Statement on the Use of Alternative Data in Credit Underwriting](https://www.federalreserve.gov/newsevents/pressreleases/files/bcreg20191203a1.pdf) (December 2019, five-agency).
    - [FRB SR 21-14 / OCC 2021-52 — third-party risk management](https://www.federalreserve.gov/supervisionreg/srletters/sr2114.htm), where the AI/ML model is sourced from a third party.
    - Non-US bank analogues — the [European Central Bank guide to internal models](https://www.bankingsupervision.europa.eu/ecb/pub/pdf/ssm.guidetointernalmodels_consolidated_202310~b0f210cbb0.en.pdf) and any [Basel Committee](https://www.bis.org/bcbs/) principles on AI/ML in the banking supervisory context that are current at the date of authoring. Mark `<!-- needs-research: -->` for any Basel document whose current status you have not verified.
  - **Insurance (`REG-2026-SEC-INS-*`).** Five rows minimum:
    - NAIC Model Bulletin — AISP requirement.
    - State-by-state adoption of the NAIC Model Bulletin. Row body carries the state-adoption map; the analyst may cite the [IAPP US State AI Governance Legislation Tracker](https://iapp.org/resources/article/us-state-ai-governance-legislation-tracker/) or the NAIC's own status page as the secondary reading list, but the primary source cited per state is the state insurance department's adopting bulletin. Mark rows `<!-- needs-research: -->` for states whose current adoption status you have not confirmed on the day of authoring.
    - [Colorado Insurance Regulation 10-1-1](https://drive.google.com/file/d/16LZY-e9CyoxSpvsAmwjXfjKb9ITw2DEO/view) — testing and reporting of external-consumer-data-and-information-source-driven and algorithm-and-predictive-model-driven insurance practices.
    - EIOPA opinion + EU AI Act Annex III point 5(c) — life and health insurance risk assessment and pricing.
    - [NY DFS Circular Letter on the Use of AI and External Consumer Data and Information Sources in Insurance Underwriting and Pricing](https://www.dfs.ny.gov/industry_guidance/circular_letters/cl2024_07).

Each row populates the full tracker column set from exercise 01. Rows carry:

- The specific primary-source citation and URL.
- The scope trigger (what makes an inventory row in-scope for the overlay — *manufacturer of an AI/ML-enabled Class II or Class III medical device*, *institution supervised by the Federal Reserve or OCC that uses AI/ML models within the model-risk-management perimeter*, *insurer authorised in a state that has adopted the NAIC Model Bulletin*).
- The role assignment (*manufacturer / user facility*, *supervised institution / third-party service provider*, *insurer / MGA / vendor-of-external-consumer-data*).
- The status (*in force* / *phased — [date]* / *guidance — non-binding* / *voluntary code*).
- The enforcement authority (FDA / MHRA / Health Canada; Federal Reserve / OCC / FDIC / NCUA; state insurance department per state of licensure / EIOPA / NY DFS).
- The affected inventory rows (populate against the systems in exercise 01's seed; empty is valid where no in-scope system exists, in which case the row is retained as horizon-scan and the row body says so explicitly).
- The AIGP body-of-knowledge tag per chapter 08's tagging pattern.
- The *notes for counsel* column carries the specialist name in addition to (not in place of) counsel — this is the chapter-06 discipline.

### Part 2 — the specialist-routing notes

Author `mod-106-ex-04-specialist-routing-notes.md` — three routing notes, one per overlay. Each note:

- **Overlay header.** Overlay name, tracker-row identifier prefix (e.g., `REG-2026-SEC-MED-*`), analyst author, date.
- **The specialist role inside the enterprise.** Named by role, not by person (*Regulatory Affairs / Quality Assurance lead*, *Head of Model Risk Management*, *Chief Actuary / Insurance Compliance lead*). Where the enterprise does not carry the role — because it is not in the sector — say so explicitly and mark the routing note *no in-scope specialist; overlay retained as horizon-scan*.
- **The routing shape.** How the specialist receives sector-overlay change-notes (chapter 10 pattern), how the analyst receives sector-specialist findings that need to land in the tracker (the reverse flow), and the meeting or forum where the joint reading happens (a monthly sector-review, a quarterly council briefing, a submission-window pre-read).
- **The boundary of the analyst's role.** From chapter 06 — *not the medical-device submission*, *not the model-validation report*, *not the actuarial pricing memo*, *not the specialist opinion*. State each boundary explicitly for this overlay so that a new specialist joining the enterprise reads the analyst's note and understands the hand-off.
- **The specialist's escalation path back to counsel.** Sector overlays often engage counsel indirectly (through the specialist's work); the routing note names the pattern (*specialist raises legal characterisation questions through their own counsel counterpart; analyst adds a note on the tracker row when the question is raised and updates the row when the answer lands*).

### Part 3 — the applicability drill

Author `mod-106-ex-04-sector-overlay-applicability.md` — three short (paragraph-per-overlay) applicability paragraphs for each of three deliberately-mixed inventory rows. Use these illustrative rows (not real deployments):

1. **`INV-2026-EX04-MED` — an AI-enabled digital pathology triage tool.** Deployed as a Class II software-as-a-medical-device in the US and CE-marked under EU MDR. Uses image classification on histopathology slides to flag likely-positive cases for priority review by a pathologist.
2. **`INV-2026-EX04-BANK` — an AI-enabled small-business-credit underwriting model.** Deployed by a state-chartered commercial bank supervised by the Federal Reserve; underwrites loans up to $500,000; incorporates alternative data from a third-party vendor.
3. **`INV-2026-EX04-INS` — an AI-enabled homeowners-insurance claim-triage engine.** Deployed by an insurer authorised in twelve US states (varying NAIC adoption status) and in three EU member states; classifies incoming claims by severity and routes them to fast-track or full-investigation queues.

For each inventory row, produce three overlay paragraphs — one per overlay — that resolve to *in scope, overlay applies, cite tracker rows and specialist routing* or *not in scope, one-line reason*. The point of the mixed scenarios is that some inventory rows attach to more than one overlay (the pathology tool engages medical directly and does not engage banking or insurance; the small-business-credit model engages banking directly and does not engage medical or insurance; the homeowners claim-triage engine engages insurance directly and — through the third-party-vendor alternative-data path — a reduced-shape banking-adjacent third-party-risk overlay if the enterprise is part of a bank-holding group).

## Requirements

- **The sector-overlays tracker extension is a projection of the exercise-01 seed schema, not a rewrite.** Same column set, same identifier convention, same *not applicable — [reason]* convention on cells that do not populate.
- **Every overlay sub-section has at least five rows.** Fewer means either the analyst's authoring session was cut short or the overlay-specific primary-source landscape was not walked; either way, expand.
- **Every row cites a primary source.** IAPP tracker pages, law-firm client alerts, and NAIC secondary summaries are useful reading; the *primary-source URLs* column carries the regulator's or supervisor's own published document.
- **Every row's affected-inventory-rows column is populated** with either an inventory-row identifier (from exercise 01 or from the applicability-drill inventory) or an explicit *no in-scope systems; retained as horizon-scan*.
- **Every specialist-routing note names the enterprise-internal specialist by role**, not by personal name.
- **Every specialist-routing note states the four boundaries explicitly** — the analyst does not draft the medical-device submission, the model-validation report, the actuarial pricing memo, or the specialist opinion. These are the four *do not cross this line* statements from chapter 06.
- **Every applicability paragraph resolves to a specific outcome.** *Might apply* is not an outcome; *in scope — deployer / manufacturer / insurer role; tracker rows `REG-2026-SEC-*-<n>`, `<n>`; specialist route to [role]* is. *Not in scope — [one-line reason]* is also an outcome.
- **The `INV-2026-EX04-INS` applicability paragraphs resolve the mixed-overlay case honestly.** The homeowners claim-triage engine primarily engages the insurance overlay, but the third-party-vendor alternative-data path may — depending on the enterprise's group structure — also engage the FFIEC / SR 21-14 third-party-risk shape from the banking overlay. State the read, cite the trigger, and route to counsel and to the specialist for the boundary determination. Do not force the mixed case into a single-overlay answer for neatness.
- **Nothing fabricated.** No invented state insurance department bulletins, no invented FDA guidance IDs, no invented supervisory letters. Mark `<!-- needs-research: -->` on any factual claim whose current status you have not verified against the primary source at the date of authoring.
- **No legal-conclusion language.** The tracker names the obligation and the scope trigger; the applicability paragraphs and the specialist-routing notes ask the sector specialist (and, where warranted, counsel) the right questions. Analyst-tier flags stay questions.

## Starter guidance

- Populate the medical overlay first. FDA GMLP is the most extensively-documented anchor overlay in the module and its shape is the cleanest to build against. Once you have five rows with full-column populations, the banking and insurance rows fall into a similar pattern.
- The banking model-inventory row is easy to skip because it is *implicit* in SR 11-7 rather than a separately-labelled requirement. Do not skip it — the model inventory is the load-bearing evidence artefact for internal-audit walks in `mod-108`, and the analyst is who cites it. Put it in the tracker as its own row so it is discoverable.
- The insurance state-adoption row body is where the tracker's discipline earns its keep. A row body that says *most states have adopted the NAIC Model Bulletin* is not evidence; a row body that lists the states with adoption dates and primary-source citations is. If you cannot verify every state, mark the unverified states `<!-- needs-research: -->` and cite the source you would check.
- The specialist-routing notes are what the enterprise reads to decide whether it needs to hire the specialist. If the analyst's note reads *specialist role X owns the depth in this overlay, and specifically these four artefacts I do not touch*, the note doubles as a job description for hiring the specialist when the enterprise's exposure to the overlay grows. Write it that way.
- The `INV-2026-EX04-INS` mixed-overlay case is the hardest of the three applicability scenarios. The insurance overlay is direct; the banking-adjacent third-party-risk shape depends on whether the enterprise is part of a bank-holding group (in which case FFIEC third-party risk and SR 21-14 attach through the group affiliation) or a standalone insurer (in which case the third-party risk lives inside the NAIC AISP third-party-AI-systems section and does not travel to the banking overlay). State the enterprise-shape assumption and follow the corresponding fork.
- The chapter's *no in-scope systems; retained as horizon-scan* framing is not a workaround for lazy tracking — it is the honest status for a row where the overlay would attach if the enterprise ever entered the sector. Author the row honestly with the horizon-scan note; the point is that the row exists so a future intake into that sector inherits the obligation rather than starting from scratch.

## Acceptance criteria

- `mod-106-ex-04-sector-overlays-tracker.md` with a header block, three overlay sub-sections (medical / banking / insurance), and at least five rows per overlay with the full exercise-01 column set populated.
- Every row cites a primary source in the *primary-source URLs* column; every row's affected-inventory-rows column is populated or explicitly marked as horizon-scan.
- `mod-106-ex-04-specialist-routing-notes.md` with three routing notes, each naming the specialist role, the routing shape (both directions), the four boundaries from chapter 06, and the specialist's escalation path back to counsel.
- `mod-106-ex-04-sector-overlay-applicability.md` with three inventory rows (`INV-2026-EX04-MED`, `INV-2026-EX04-BANK`, `INV-2026-EX04-INS`), a paragraph per overlay per row, each resolving to a specific in-scope / not-in-scope outcome with tracker-row citations and specialist-routing notes.
- The `INV-2026-EX04-INS` case handles the mixed-overlay situation honestly, stating the enterprise-shape assumption and following the corresponding fork rather than forcing a single-overlay answer.
- No fabricated regulator documents, no fabricated adopted-state list entries, no fabricated Basel Committee outputs. `<!-- needs-research: -->` markers are permitted and expected for verification points; unmarked fabrication is not.
- No legal-conclusion language; the applicability paragraphs and routing notes ask the specialist (and counsel where applicable) the right questions.

## Stretch goals

- **A fourth overlay — payments and consumer credit.** Extend the tracker to add `REG-2026-SEC-CONSFIN-*` rows for the [Consumer Financial Protection Bureau (CFPB)](https://www.consumerfinance.gov/) enforcement of ECOA / Regulation B and the [CFPB Circular 2022-03 on adverse-action notification for decisions based on complex algorithms](https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/). The small-business-credit inventory row from the applicability drill picks this overlay up as well as the banking one.
- **A cross-jurisdictional analogue map.** For the medical overlay, produce a small companion table showing how FDA GMLP maps onto UK MHRA, Health Canada, EU MDR/IVDR, and the [IMDRF SaMD framework](https://www.imdrf.org/documents/software-medical-device-samd-key-definitions). One row per overlay principle or artefact; one column per jurisdiction; each cell cites the local instrument or notes *no direct analogue*.
- **A specialist-hiring signal document.** For an overlay where the enterprise's exposure is growing but the specialist role does not yet exist internally, extract the routing note into a short (one-page) *why we need this specialist* memo. The memo is the input the analyst hands to the head of governance or the CFO when arguing that the enterprise's sector exposure has crossed the threshold where the analyst-tier tracker + external counsel model is no longer sufficient.
- **A specialist-review artefact index.** For each overlay, list the specialist-owned artefacts the impact-assessment corpus (`mod-105`) cites but does not author — the 510(k) submission, the independent model-validation report, the actuarial pricing memo, the AISP documentation. Group them by overlay and add a column for *where the analyst finds the current version* (the specialist's team folder, the GRC platform, the enterprise's regulated-artefact repository). This is the evidence discoverability layer for `mod-107` and `mod-108`.
- **A single-page overlay-inheritance visualisation.** Render the applicability drill's outcomes as a compact matrix — inventory rows across the top, overlays down the side, cells marked ● *in scope, direct*, ◐ *in scope, adjacent (routes through group affiliation or third-party path)*, ─ *not in scope*. Attach it to the front of the applicability document for reader-scannability.

## Deliverables

- `mod-106-ex-04-sector-overlays-tracker.md` — the sector-overlays tracker extension.
- `mod-106-ex-04-specialist-routing-notes.md` — the three routing notes.
- `mod-106-ex-04-sector-overlay-applicability.md` — the applicability drill across three mixed inventory rows.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference set of rows and routing notes shaped around a mid-size insurance-and-fintech enterprise. Yours will differ in the specific rows, the state-adoption details, and the routing-note phrasing. What should not differ is (a) every overlay has at least five rows with full-column populations, (b) every row cites a primary source and populates affected-inventory-rows or explicitly marks the row as horizon-scan, (c) every routing note names the specialist role and the four boundaries from chapter 06, (d) the applicability paragraphs resolve to specific outcomes with tracker-row citations, and (e) the mixed-overlay `INV-2026-EX04-INS` case is handled honestly rather than force-fit. A five-row-per-overlay tracker extension with disciplined citations and honest horizon-scan rows beats a twenty-row extension with speculative row bodies and unmarked fabrication.
