# Exercise 02 — EU AI Act vs US State Crosswalk

**Estimated effort:** 2 hours
**Grounding chapters:** [02 — The EU Stack — AI Act, GDPR, and the Council of Europe Framework Convention](../02-eu-stack-ai-act-gdpr-coe.md) and [04 — The US State Stack — Colorado AI Act, NYC Local Law 144, and Illinois BIPA](../04-us-state-stack.md); tag-and-routing reference in [08 — The IAPP AIGP Body of Knowledge as the Shared Vocabulary](../08-iapp-aigp-shared-vocabulary.md).

## Objective

Author an obligation-level crosswalk between the EU AI Act and the anchor US state instruments — Colorado AI Act (SB24-205), NYC Local Law 144 of 2021, and (as a biometric-adjacent contrast) Illinois BIPA — and pair the crosswalk with a short per-system applicability memo for the MCDA and MCDA-Benefits inventory rows carried across the track. The crosswalk is the analyst-tier artefact that answers *if we already do X for the AI Act, what more does Colorado / NYC / Illinois require of us — and vice versa*, without collapsing the differences into false equivalence.

After this exercise you should be able to sit down in front of a mixed-jurisdiction deployment, tell the reviewer within a page which obligations attach where, which are near-duplicates that can be evidenced together, and which are genuinely divergent so that separate work is required.

## Prerequisites

- Chapter 02 read; the AI Act four-tier structure, the provider / deployer / importer / distributor role distinctions, and the phase-in schedule fresh in memory.
- Chapter 04 read; the Colorado AI Act developer/deployer split, the NYC LL 144 bias-audit / notice / public-summary triad, and the BIPA §15 duties fresh in memory.
- Chapter 08 skimmed; the AIGP domain tags are used to label crosswalk cells for downstream filtering.
- The seed tracker from exercise 01 open — the crosswalk cells link back to the tracker row identifiers you assigned there (`REG-2026-EU-*`, `REG-2026-US-CO-*`, `REG-2026-US-NY-*`, `REG-2026-US-IL-*`).
- The MCDA (`INV-2026-0088`) and MCDA-Benefits (`INV-2026-0311` or your equivalent) inventory rows from `mod-105` chapter 03. If you swapped in a different pair of systems in exercise 01, use the same pair here.
- Primary sources open in adjacent tabs: [Regulation (EU) 2024/1689](https://eur-lex.europa.eu/eli/reg/2024/1689/oj); [Colorado SB24-205](https://leg.colorado.gov/bills/sb24-205); the [NYC LL 144 DCWP rules at 6 RCNY §§ 5-300 to 5-304](https://rules.cityofnewyork.us/wp-content/uploads/2023/04/DCWP-NOA-for-Use-of-Automated-Employment-Decisionmaking-Tools-2.pdf); [Illinois BIPA (740 ILCS 14)](https://www.ilga.gov/legislation/ilcs/ilcs3.asp?ActID=3004).

## Problem statement

The deliverable is two Markdown files.

### Part 1 — the obligation-level crosswalk

Author `mod-106-ex-02-eu-us-state-crosswalk.md`. The document has:

- **Header block.** Version, date, author, cross-reference to the exercise-01 seed tracker file, list of the four instruments in scope, and a one-sentence *what this document is not* disclaimer (it is not a legal opinion; it is an obligation-shape mapping the analyst maintains for internal routing).
- **A canonical-obligations column.** Down the left side of the main crosswalk table, name the analyst-tier obligation categories the two regimes cover. At minimum: risk-tier classification / scoping filter; consequential-decision or high-risk trigger; conformity-assessment or bias-audit obligation; consumer or candidate notice; explanation / meaningful-information right; opt-out or human-review right; impact-assessment obligation; ongoing-monitoring or post-market obligation; public-summary or disclosure obligation; enforcement authority and private right of action; and — as a separate row — the biometric-specific obligations that BIPA raises.
- **Four instrument columns.** *EU AI Act*, *Colorado AI Act*, *NYC LL 144*, *Illinois BIPA*. Each cell carries:
  - The instrument's specific article or section citation.
  - A one-sentence characterisation of the obligation as it lands under that instrument (e.g., for the *consumer notice* row under Colorado AI Act: *deployer must notify the consumer that a consequential decision was made by a high-risk AI system and — if adverse — provide the reason, an opportunity to correct data, and a right to appeal to human review, per SB24-205 §6-1-1703*).
  - A *not applicable — [one-line reason]* explicit value where the instrument does not carry the obligation. Blanks are not permitted.
  - The tracker row identifier from your exercise-01 seed (e.g., `REG-2026-US-CO-002`).
  - An AIGP domain tag per chapter 08's tagging pattern.
- **A same-shape / different-shape / no-analogue narrative** — three short sub-sections underneath the crosswalk table:
  - **Same shape.** Obligations that map cleanly across two or more instruments and can be evidenced with a single shared artefact (e.g., a single impact assessment that can be projected into both an AI Act Article 27 FRIA view and a Colorado risk-management-programme view per `mod-105` chapter 01's shared-template discipline).
  - **Different shape.** Obligations that exist in more than one regime but with materially different scope, threshold, or content — the analyst names the difference, cites both texts, and flags to counsel where the enterprise's practice would need to be adapted per jurisdiction (e.g., the AI Act's bias-and-quality obligations under Article 10 vs the NYC LL 144 bias-audit metric shape).
  - **No analogue.** Obligations that exist in only one instrument — name them explicitly so that a same-shape reader does not silently assume coverage transfers (e.g., BIPA's private right of action with statutory damages has no analogue in the AI Act or the Colorado AI Act; the AI Act's Article 5 prohibitions have no direct US-state analogue).

### Part 2 — the per-system applicability memo

Author `mod-106-ex-02-crosswalk-applicability-mcda.md`. Two sections, one per system:

- **MCDA (`INV-2026-0088`) — marketing copy draft assistant.** For each of the four instruments, one paragraph: which obligations apply, which do not, and — where an obligation applies — which crosswalk row and which tracker row it maps to. Include the *role* the enterprise plays under each instrument (provider, deployer, developer, employer, or *not in scope*).
- **MCDA-Benefits (`INV-2026-0311` or your equivalent) — public-benefits caseworker draft assistant.** Same shape.

Close the memo with a short **hand-off block** — no more than five lines — naming the counsel and privacy-office questions the crosswalk surfaces for each system, plus the change-note ID reservations you would use if any of the underlying obligations moved (referencing chapter 10's shape).

## Requirements

- **The crosswalk covers all four instruments in every canonical-obligation row.** No hidden three-instrument tables with the fourth omitted; a *not applicable — [reason]* cell is the correct value where the instrument does not carry the obligation.
- **Every cell cites the specific article or section.** *AI Act — Article 6 + Annex III* is the correct citation shape; *AI Act* is not.
- **Every non-empty cell cross-references a tracker row from exercise 01.** The crosswalk is a projection of the tracker; the identifiers are the join key.
- **Every cell carries at least one AIGP domain tag.** Multi-domain cells list the primary domain first.
- **The three sub-sections are populated** — same shape, different shape, no analogue — with concrete named obligations, not abstractions. *There are similarities between the two regimes* is not a same-shape entry; *the AI Act's Article 26(6) human-oversight expectation and Colorado's SB24-205 §6-1-1703(3) right of appeal to human review both attach to the deployer of a covered system* is a same-shape entry.
- **The applicability memo names the enterprise's role per instrument, per system.** Do not default to *deployer everywhere*; some rows land the enterprise as *developer* under Colorado for the same system it is *deployer* under the AI Act, and some inventory rows are simply out of scope for one or more instruments (e.g., MCDA is not a hiring tool, so NYC LL 144 is *not applicable — non-employment use case*).
- **Illinois BIPA is treated as a biometric-adjacent instrument, not a general AI statute.** Most obligation rows will read *not applicable — BIPA scope is biometric identifiers / information* for both the MCDA and MCDA-Benefits systems. The biometric-specific row is where BIPA has content; the other rows carry the *not applicable* note. That is the correct answer.
- **No fabricated statutory sections or authorities.** Every citation traces to a primary-source text; where the specific effective date, the specific implementing regulation, or the specific enforcement posture is uncertain, mark the cell `<!-- needs-research: ... -->` with the source to check (Colorado AG office; NYC DCWP; Illinois Attorney General; European Commission AI Office).
- **The hand-off block names roles, not people.** *DPO*, *General Counsel*, *Colorado privacy lead* — not personal names.

## Starter guidance

- Build the canonical-obligations column first, before you start populating cells. If the column set is wrong, every cell across four instruments has to be re-authored. A twelve-to-fifteen-row canonical column set is enough to carry the main obligations; you can extend if your enterprise's shape adds specific rows (e.g., third-party-model due diligence).
- The *scoping filter* row is the most useful and the most dangerous. AI Act Annex III lists eight domains; Colorado's *consequential decision* list is eight domains; NYC LL 144's *employment decision* is a single narrow category; BIPA's biometric-identifier definition is narrower still. Cite each scoping test verbatim; do not compress them into *both cover hiring* or *both cover consumer decisions* — the differences are load-bearing.
- The *provider / deployer / developer* mapping is easy to get wrong. AI Act *provider* ≠ Colorado *developer* exactly, but they overlap heavily; AI Act *deployer* ≠ Colorado *deployer* exactly, but again they overlap. Flag the mismatch in the *different shape* section and — for the enterprise's own systems — cite counsel's characterisation, or mark the row `<!-- needs-research: ... -->` if counsel has not yet opined.
- The *bias audit* obligation is a specific example of different-shape. NYC LL 144's bias audit is a defined *independent auditor* engagement computing specific selection-rate metrics by protected class; the AI Act's Article 10 data-and-data-governance and Article 15 accuracy-and-robustness are provider-side and shaped as ongoing quality obligations rather than an annual auditor-produced report. `mod-104` chapter 04 walked the metric shape; cite that chapter's framing here.
- The *public summary* obligation is another specific example. NYC LL 144 requires the bias-audit summary and the AEDT distribution date to be published on the employer's website; Colorado requires a public summary of the enterprise's use of high-risk AI systems; the AI Act carries no direct public-summary obligation on private-sector deployers (though provider-side Article 13 information-to-deployers obligations shape a different downstream disclosure). The three are related but not the same artefact.
- The Illinois BIPA row is where the *no analogue* section carries most of its weight. BIPA's statutory damages, private right of action, and per-scan accrual (as limited by [Public Act 103-0769](https://www.ilga.gov/legislation/publicacts/103/PDF/103-0769.pdf)) shape enterprise risk in a way that no AI Act provision or Colorado AI Act provision does. Name that explicitly.
- The applicability memo is where the reader tests whether the crosswalk actually helps. Write it as if the reader is the MCDA-Benefits system owner asking *what am I actually on the hook for* — not as if the reader is a Ph.D. examiner.

## Acceptance criteria

- `mod-106-ex-02-eu-us-state-crosswalk.md` with the header, canonical-obligations column, four instrument columns fully populated (no blank cells), and the three sub-sections (same shape / different shape / no analogue).
- Every cell cites a specific article or section from the primary source and cross-references a tracker row from exercise 01.
- Every cell carries at least one AIGP domain tag.
- Every *not applicable* cell has a one-line reason.
- `mod-106-ex-02-crosswalk-applicability-mcda.md` with a paragraph per instrument per system, an explicit *role* assignment per cell, and a five-line-maximum hand-off block naming counsel / privacy-office questions and change-note ID reservations by role.
- Illinois BIPA is treated correctly as biometric-scope; the biometric-specific row has content; the general rows carry *not applicable — BIPA scope is biometric identifiers / information*.
- No fabricated statutes, authorities, or citations. Any uncertain cell is marked `<!-- needs-research: -->` with the specific source to check.
- The crosswalk reads without requiring the reader to know the enterprise; the applicability memo reads with the enterprise in front of them.

## Stretch goals

- **A California-and-Texas extension column set.** Add columns for [California CCPA/CPRA with the CPPA ADMT regulations](https://cppa.ca.gov/regulations/) and — if a bill has passed by the time you complete this exercise — Texas or other comprehensive-state variants. Cite primary sources; mark `<!-- needs-research: -->` for provisions whose enacted text or effective date you have not verified.
- **A visual matrix.** Render the crosswalk as a compact matrix (e.g., a wide Markdown table or an ASCII-art heatmap) using cell markers: ● *same shape*, ◐ *different shape*, ○ *no analogue in this column*, ─ *not applicable*. The visual is a scannable index that sits above the full table for quick reading in an oversight meeting.
- **A change-note trigger list.** For each different-shape row, name the specific regulator publication that would trigger a change-note under chapter 10's discipline (a Colorado AG implementing rule, a DCWP enforcement bulletin, an EU AI Office guidance revision, an EDPB opinion). This produces the watch list the analyst uses on the monthly deep read.
- **A per-audience filtered projection.** Produce a short (one-page) view of the crosswalk filtered by AIGP domain — a domain-3 (*Current Laws Applied to AI Systems*) view for a CIPP-holder DPO, a domain-4 (*Existing and Emerging AI Laws and Standards*) view for a CRO or an internal auditor. This is the chapter-08 per-audience projection applied to the crosswalk product rather than to the raw tracker.
- **A single-system dry run against a real product.** If you have a real internal system you can use in place of MCDA / MCDA-Benefits (with appropriate confidentiality), run the applicability memo against it and compare with counsel's independent read. Any divergence is a note for the flagging discipline in chapter 07.

## Deliverables

- `mod-106-ex-02-eu-us-state-crosswalk.md` — the obligation-level crosswalk with three narrative sub-sections.
- `mod-106-ex-02-crosswalk-applicability-mcda.md` — the per-system applicability memo with the hand-off block.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference crosswalk shaped around MCDA / MCDA-Benefits. Yours will differ in the specific canonical-obligation rows and the exact same-shape / different-shape / no-analogue narrative. What should not differ is (a) all four instruments are covered in every canonical-obligation row, (b) every non-*not applicable* cell cites a specific article or section, (c) BIPA is treated as biometric-scope and not force-fit into general-AI rows, (d) the applicability memo names the enterprise's role per instrument per system, and (e) *not applicable* cells carry a reason. A twelve-row crosswalk with every cell populated honestly and cited to primary sources beats a thirty-row crosswalk with half the cells left as *pending* or paraphrased away from the statutory text.
