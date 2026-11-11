# Quiz 01 — The Rolling Tracker, Jurisdictional Branches, Privacy Flagging, Voluntary Codes, and Change-Note Routing

**Format:** 12 multiple-choice questions, one correct answer each.
**Grounding chapters:** [01](../01-rolling-regulatory-tracker-method.md), [02](../02-eu-stack-ai-act-gdpr-coe.md), [03](../03-us-federal-patchwork.md), [04](../04-us-state-stack.md), [05](../05-uk-canada-trajectories.md), [06](../06-sector-regulators.md), [07](../07-privacy-law-flagging-discipline.md), [08](../08-iapp-aigp-shared-vocabulary.md), [09](../09-voluntary-codes-gpai-code-of-practice.md), [10](../10-regulatory-change-note-routing.md).
**Rules:** Open-book against the chapters themselves — this quiz tests fluency, not look-up. Closed-book against anything else.

---

## Questions

### 1. The tracker as a register, not a memo

Chapter 01 opens by naming a specific first-year failure mode and the discipline that prevents it. Which statement captures the chapter's framing?

- A. The tracker is a confidential legal-opinion database maintained by the analyst; its rows record counsel's characterisations of each obligation.
- B. The tracker is a bookmark folder plus the analyst's tacit knowledge; the discipline is to keep the folder organised by jurisdiction.
- C. The tracker is a register — one row per obligation, discoverable, versioned, tied to inventory rows, with a *last-verified* date that turns the row into evidence rather than a claim.
- D. The tracker is a narrative memo the analyst refreshes annually, summarising the state of AI regulation globally.

### 2. The AI Act phase-in schedule

Chapter 02 names four phase-in dates for the EU AI Act under Article 113. Which mapping matches the chapter?

- A. All provisions apply from 2 August 2024; there is no phased schedule.
- B. 2 February 2025 — Article 5 prohibitions and Article 4 AI-literacy; 2 August 2025 — governance and GPAI (Chapter V) and penalties; 2 August 2026 — most other provisions including Annex III high-risk; 2 August 2027 — Annex I harmonisation-legislation overlay.
- C. 2 August 2025 — all provisions, including Annex I and Annex III high-risk; penalties framework in 2027.
- D. The AI Act has not yet entered into force; its phase-in has been suspended by delegated act.

### 3. Provider vs deployer — per-system, not per-enterprise

Chapter 02 is explicit that an enterprise's role under the AI Act is assigned per system, not per enterprise. Which statement matches the chapter?

- A. An enterprise is classified as either a provider or a deployer once at registration with the AI Office; the classification applies to all its AI systems.
- B. The role is per-system — the same enterprise can be a provider for one system (an internally-developed model exposed to a downstream customer) and a deployer for another (a hosted foundation-model API used inside a workflow); the tracker's affected-inventory-rows column pairs each inventory row with the role the enterprise plays for that system.
- C. Only EU-established enterprises can be providers; non-EU enterprises are always deployers.
- D. The provider / deployer distinction was removed in the final AI Act text; only *operator* applies.

### 4. The joint statement — which authorities, and what it establishes

Chapter 03 calls the joint statement the load-bearing artefact for the analyst's rebuttal to *there is no US federal law on AI*. Which description matches the chapter?

- A. A single-authority FTC rulemaking declaring that AI systems are deceptive practices unless certified by NIST.
- B. An EEOC, FTC, HHS OCR, and FDA joint rulemaking creating a new federal AI statute.
- C. A joint statement first issued 25 April 2023 and re-affirmed 12 April 2024 by the CFPB, DOJ Civil Rights Division, EEOC, and FTC — stating that existing federal law (Title VII, ECOA, Section 5 of the FTC Act, Fair Housing Act, and others) prohibits discrimination and other harms in automated systems, and that the signing authorities intend to enforce those laws against AI-driven violations.
- D. A non-US instrument issued by the OECD AI Policy Observatory and endorsed by US agencies as a voluntary code.

### 5. The executive-order overlay is dynamic

Chapter 03 treats the White House EO stack as a distinct kind of tracker row with a specific refresh discipline. Which description matches the chapter?

- A. EO rows are static — once an EO is cited in the tracker it does not need to be refreshed because EOs are permanent.
- B. EO rows are not permitted in the tracker because EOs do not create private-sector obligations.
- C. The EO row (or short list of rows) is refreshed on the monthly deep read, cites the EOs currently in force, the EOs rescinded in the current administration, and any Federal Register notices adopting or rescinding EO-derived requirements at specific agencies — acknowledging that EOs flow to private-sector enterprise behaviour through federal procurement and through agency-enforcement priorities.
- D. The EO row is refreshed only after a change in presidential administration; between administrations the row is dormant.

### 6. The Colorado AI Act's consequential-decision scope

Chapter 04 names the eight categories a decision must fall into before it can be a *consequential decision* triggering the Colorado AI Act. Which statement captures the Act's scope trigger?

- A. Any decision made by any AI system about any Colorado consumer.
- B. Only decisions in healthcare and insurance; employment, lending, and housing are out of scope.
- C. A decision that has a material legal or similarly significant effect on the provision or denial of, or the cost or terms of, one of the enumerated services — education enrolment or opportunity, employment or employment opportunity, a financial or lending service, an essential government service, healthcare services, housing, insurance, or a legal service — where the AI system is a *substantial factor* in making the decision.
- D. Any automated decision processing biometric identifiers of Colorado residents.

### 7. BIPA's private right of action

Chapter 04 explains why Illinois BIPA is disproportionately consequential among US state biometric-privacy statutes. Which statement matches the chapter?

- A. BIPA is enforced exclusively by the Illinois Attorney General; there is no private right of action and class actions are prohibited.
- B. BIPA carries a private right of action with statutory damages of the greater of actual damages or $1,000 per negligent violation / $5,000 per intentional or reckless violation, plus attorneys' fees and injunctive relief; per-scan accrual was limited by Public Act 103-0769 in August 2024 after *Cothron v. White Castle*, but the financial exposure remains significant.
- C. BIPA's damages are capped at $100 per claimant and plaintiffs may not recover attorneys' fees.
- D. BIPA has been preempted by federal legislation and is no longer enforceable.

### 8. The AIDA status, honestly

Chapter 05 is strict about how the tracker reflects legislative-trajectory rows. Which statement matches the chapter's reading of Canada's AIDA?

- A. AIDA is in force as federal Canadian private-sector AI legislation and is enforced by the Office of the Privacy Commissioner.
- B. AIDA was proposed as Part 3 of Bill C-27, tabled June 2022; Bill C-27 did not pass before the prorogation of the 44th Parliament on 6 January 2025 and — under Canadian parliamentary procedure — died on the order paper. The tracker's status field is *proposed — died on order paper 6 Jan 2025*; a re-tabled version or successor bill would be monitored in the horizon-scan.
- C. AIDA was enacted as a standalone statute in 2024 after Bill C-27's failure.
- D. AIDA has been merged into the TBS Directive on Automated Decision-Making and now binds the private sector through that instrument.

### 9. Sector overlays are not jurisdiction-nested

Chapter 06 frames the sector-overlays branch of the tracker as structurally different from the jurisdictional branches. Which statement matches the chapter?

- A. A sector overlay row sits inside one jurisdictional branch; an FDA GMLP row lives under *US federal* only.
- B. A sector overlay applies across whichever jurisdictions the enterprise operates in that are covered by that sector regulator — FDA GMLP was developed jointly with UK MHRA and Health Canada and is cited well outside US SaMD submissions, and the tracker holds a single sector-overlay row with the role assignment per inventory row rather than one row per jurisdiction.
- C. Sector overlays are optional; the analyst-tier tracker only carries horizontal jurisdictional rows.
- D. Sector overlays apply only to non-AI software; AI-specific obligations always live under the horizontal AI Act or Colorado AI Act rows.

### 10. The three GDPR Article 22 tests and the flag discipline

Chapter 07 names three tests that decide whether Article 22 is engaged and attaches a specific discipline to how the analyst writes a flag. Which statement matches the chapter?

- A. The three tests are *lawful basis*, *purpose limitation*, and *data minimisation*; the analyst writes a conclusion in the inventory row's counsel-questions field that the system either does or does not comply with Article 22.
- B. The three tests are *solely automated* (with the WP 251 rev.01 meaningful-human-involvement threshold — rubber-stamp review is not meaningful), *legal effects*, and *similarly significant effects*; the flag is written when any two of the three plausibly land yes, phrased as a question (not a conclusion), names the inventory row and cites the trigger, and is recorded in the inventory row's counsel-questions field rather than spoken in a hallway.
- C. The three tests are *special-category data*, *cross-border transfer*, and *data-subject access*; a DPIA must be completed before Article 22 can be flagged.
- D. There are no tests — Article 22 applies to every AI system that processes personal data without exception.

### 11. The AIGP body-of-knowledge as the shared vocabulary

Chapter 08 positions the IAPP AIGP BoK as the analyst's shared vocabulary with the DPO, CISO, CRO, and internal auditor. Which statement matches the chapter?

- A. The AIGP certification is required for every AI governance analyst; without it, the tracker is not usable.
- B. The AIGP BoK replaces primary regulatory citations in the tracker; the BoK tag is the source of authority for each row.
- C. The AIGP BoK is organised into five current domains (foundations; impacts and responsible-AI principles; how current laws apply to AI; existing and emerging AI laws and standards; AI development life cycle); every tracker row carries at least one AIGP domain tag as a discoverability index so a DPO reading domain 3 or a CRO reading domain 4 can filter the tracker without paraphrasing; the certification decision is individual, the vocabulary discipline is not; and the primary regulatory citation remains the source of authority.
- D. The AIGP BoK applies only to EU jurisdictions; US-state obligations are tagged against the CIPP/US BoK instead.

### 12. The regulatory-change-note — what it is for

Chapter 10 defines the change-note as the artefact that converts a tracker update into routed action across affected inventory rows. Which statement matches the chapter?

- A. The change-note is an internal memo filed by counsel after a tracker update; the analyst does not author it.
- B. The change-note is a mass-distribution email sent to all system owners whenever any tracker row's last-verified date changes.
- C. The change-note is a short, structured artefact (header with change-note ID, date, filer, tracker row updated, related regulator artefacts; body with what changed, why it matters here, affected inventory rows, affected impact-assessment artefacts, recommended action per owner, counsel / privacy-officer flag, analyst next-step tracking date; footer with status and cross-reference); it routes primary to the system owner, secondary to the governance and risk-register owners, tertiary to counsel or privacy officer — no mass distribution — and is closed only when the owner has updated the review-triggers list, revisited the register entries, regenerated affected regulator views, and attached the evidence artefact.
- D. The change-note replaces the tracker row; once the change-note is filed, the tracker row is deleted.

---

## Answer key

| # | Answer | Why |
|---|---|---|
| 1 | **C** | Chapter 01's "The tracker is a register, not a memo" is explicit: the tracker is one row per obligation, columns filled in, updated on a cadence, discoverable in the same governance repository as the inventory; the *last-verified* date is called out as *the single most important field* because it is what turns the row into evidence. Options A, B, and D are precisely the failure modes the chapter names. |
| 2 | **B** | Chapter 02's "The AI Act — tier structure and phase-in" table lists the four dates verbatim: 2 Feb 2025 (Article 5 prohibitions and Article 4), 2 Aug 2025 (governance and GPAI Chapter V and penalties Chapter XII), 2 Aug 2026 (most other provisions including Annex III high-risk and Article 50 transparency), and 2 Aug 2027 (Annex I harmonisation-legislation overlay). The chapter's needs-research marker asks the analyst to verify against current consolidated text before citing to audit. |
| 3 | **B** | Chapter 02's "Deployer vs provider — the load-bearing role distinction" says the role is per-system, not per-enterprise, and uses the exact example of an internally-developed model exposed to a downstream customer vs a hosted foundation-model API used inside a workflow. The chapter calls this the load-bearing role distinction for tracker authoring. |
| 4 | **C** | Chapter 03's "The joint statement — five authorities agreeing they already have authority" names the four signing authorities (CFPB, DOJ Civil Rights Division, EEOC, FTC), the first-issue and re-affirmation dates (25 April 2023; 12 April 2024), and the plain reading — existing federal law prohibits discrimination and other harms in automated systems, and the signing authorities intend to enforce those laws against AI-driven violations. The chapter explicitly notes it is the analyst's rebuttal to *there is no US federal law on AI*. |
| 5 | **C** | Chapter 03's "White House executive orders — the shifting overlay" says the EO stack changes with the presidential administration, flows to private-sector behaviour indirectly through federal procurement and through agency enforcement priorities, and names the monthly-deep-read cadence that keeps the row current. The row cites EOs currently in force, EOs rescinded in the current administration, and Federal Register notices adopting or rescinding EO-derived requirements at specific agencies. |
| 6 | **C** | Chapter 04's "The scope trigger" sub-section under the Colorado AI Act names the eight categories verbatim and attaches the *substantial factor in making a consequential decision* test. The chapter notes the definition draws on the EU AI Act Annex III shape but adds the substantial-factor test as a US-litigation-friendly formulation. |
| 7 | **B** | Chapter 04's "The private right of action" sub-section states the statutory-damages amounts, cites *Cothron v. White Castle* (2023 IL 128004) on per-scan accrual, and notes that Public Act 103-0769 in August 2024 limited per-scan accrual so that repeated collections from the same person in the same manner produce a single claim — but that the financial exposure remains significant. The private right of action is why the chapter calls BIPA disproportionately consequential among US state biometric-privacy laws. |
| 8 | **B** | Chapter 05's "The AIDA trajectory" sub-section states that Bill C-27 did not pass before the prorogation of the 44th Parliament on 6 January 2025, that under Canadian parliamentary procedure the bill died on the order paper, and that the tracker's status field is *proposed — died on order paper 6 Jan 2025*. The chapter's needs-research marker asks the analyst to monitor for any successor legislation. |
| 9 | **B** | Chapter 06's opening section is explicit that the sector-overlays branch is *not jurisdiction-nested* — a sector overlay applies across whichever jurisdictions the enterprise operates in that are covered by that sector regulator, and the FDA GMLP example is cited specifically because it was co-authored with UK MHRA and Health Canada. The chapter's "What to memorise" bullet repeats this framing. |
| 10 | **B** | Chapter 07's "GDPR Article 22 — solely-automated decisions with legal or similar significant effect" names the three tests verbatim, attaches the WP 251 rev.01 meaningful-human-involvement standard (rubber-stamp review is not meaningful), and specifies the two-of-three-plausibly-yes flag threshold. The "The flagging discipline — three rules" section lists the question-not-conclusion rule, the name-the-row-and-cite-the-trigger rule, and the recorded-not-spoken rule. |
| 11 | **C** | Chapter 08's "What the AIGP is" and "How to tag tracker rows with AIGP domains" sections name the five current domains, the one-tag-per-row discipline, the discoverability-index framing (filtering by domain produces the per-audience reading list), and the explicit note that the primary regulatory citation remains the source of authority — the AIGP tag is discoverability, not evidence. The "The AIGP certification decision" section frames the certification as individual, the vocabulary as a tracker-hygiene rule. |
| 12 | **C** | Chapter 10's "The change-note shape" names the header / body / footer field set verbatim; its "The routing pattern" section names the primary / secondary / tertiary routing and the no-mass-distribution rule; its "Closing the loop into the impact-assessment corpus" section names the four closure steps (review-triggers list update, register-entry revisit, regulator-view regeneration, evidence-artefact attachment); and the chapter's framing of the three failure modes the discipline prevents — the regulation moves and the IA does not, the regulation moves and the wrong owner is notified, the regulation moves and no one is notified — is what makes options A, B, and D the exact failure modes rather than the discipline. |

## Scoring

- **11–12 correct:** Fluent — ready to maintain the rolling tracker across all six jurisdictional branches, flag privacy-law questions to counsel without crossing into legal conclusions, treat the GPAI Code of Practice as anticipatory intelligence, and route change-notes that close the loop into the impact-assessment corpus.
- **9–10 correct:** Solid. Re-read the chapters anchoring any missed questions before `mod-107` (eval and audit evidence reads the tracker's affected-inventory-row list to scope its walks) or `mod-110` (council briefings read from the tracker and from the change-note log) start leaning on this fluency.
- **7–8 correct:** Partial. Re-read chapters 01 (the register-not-memo framing and the cadence), 07 (the three Article 22 tests and the question-not-conclusion flagging discipline), and 10 (the change-note structure and the closure discipline) end-to-end; those are the three chapters that carry the module's integration muscle.
- **≤6 correct:** Re-read the module. The downstream modules (eval evidence, controls, incident response, communication, and `project-101`) assume this material at recall speed, not look-up speed.
