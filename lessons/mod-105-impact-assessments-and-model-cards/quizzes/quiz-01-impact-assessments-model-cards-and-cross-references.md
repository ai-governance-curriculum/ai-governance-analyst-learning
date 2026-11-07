# Quiz 01 — Impact Assessments, Model Cards, System Cards, Datasheets, and Cross-References

**Format:** 12 multiple-choice questions, one correct answer each.
**Grounding chapters:** [01](../01-iso-42005-scaffold-and-shared-template.md), [02](../02-algorithmic-impact-assessment-canadian-aia.md), [03](../03-fundamental-rights-impact-assessment-eu-article-27.md), [04](../04-data-protection-impact-assessment-gdpr-article-35.md), [05](../05-sector-specific-impact-assessment-fda-gmlp.md), [06](../06-model-cards-mitchell-hf-mct.md), [07](../07-system-cards-and-datasheets.md), [08](../08-cross-referencing-artefacts-and-walk-discipline.md).
**Rules:** Open-book against the chapters themselves — this quiz tests fluency, not look-up. Closed-book against anything else.

---

## Questions

### 1. The standards stack around ISO/IEC 42005

Chapter 01 places ISO/IEC 42005:2025 inside a three-standard SC 42 stack and gives each a distinct job. Which mapping matches the chapter?

- A. 42001 is the risk-management standard; 23894 is the AIMS; 42005 is the impact-assessment standard.
- B. 42001 is the AI management system the enterprise certifies against and requires an impact assessment; 23894 supplies the risk-source lens; 42005 supplies the impact-assessment shape.
- C. 42001, 23894, and 42005 are three competing impact-assessment standards; the enterprise picks one.
- D. 42005 replaces the NIST AI RMF MAP walk; the analyst does not need MAP once 42005 is adopted.

### 2. Why one canonical document plus regulator views

Chapter 01 argues against authoring the AIA, FRIA, DPIA, and sector overlays from scratch. Which statement best captures the load-bearing reason?

- A. The regulator forms share no fields in common, so the only efficiency gain is editorial.
- B. All four draw from the same underlying facts surfaced by the MAP walk; authoring each from scratch guarantees drift between them and is a route to an audit finding.
- C. The AIA is the authoritative shape and the FRIA / DPIA / sector views are strict subsets; only the AIA needs to be authored in full.
- D. ISO/IEC 42005 forbids the generation of regulator-shaped views; views must be authored independently.

### 3. The Canadian AIA — what makes it distinctive

Chapter 02 names two features that distinguish the Canadian AIA from the FRIA and DPIA. Which pair matches the chapter?

- A. The AIA is authored only by legal counsel, and its output is private to the sponsoring institution.
- B. The questionnaire is scored (a deterministic impact level I–IV emerges from the answer-set) and the completed assessment is published on the Open Government Portal by default.
- C. The AIA replaces the DPIA for Canadian federal deployments and requires no separate privacy review.
- D. The AIA is an evaluation report produced by the ML team, not a governance artefact.

### 4. Article 27 FRIA scope — who actually owes one

Chapter 03 warns that a common early-authoring error is to assume *all* high-risk deployment triggers a FRIA. Which set names the four deployer classes Article 27 attaches to?

- A. Any deployer of any Annex III high-risk system in any sector.
- B. Bodies governed by public law; private operators providing public services; deployers of high-risk systems used to evaluate creditworthiness or credit-scoring; deployers of high-risk systems used for risk assessment and pricing in life and health insurance.
- C. Only providers (not deployers) of Annex III systems; deployers are out of scope.
- D. Employers using Annex III point 4 hiring tools; private banks; social-media platforms; any public body.

### 5. The Article 13 dependency

Chapter 03 names an input the FRIA cannot be completed without. Which input is it, and whose artefact is it?

- A. The deployer's Article 26 human-oversight plan — authored by the deployer.
- B. The provider's Article 13 instructions for use, which cover intended purpose, characteristics, capabilities, and limitations — authored by the provider; the deployer references it and escalates if it is missing.
- C. The market-surveillance authority's advance approval — issued by the authority.
- D. The Charter-of-Fundamental-Rights legal memo — authored by counsel.

### 6. The WP 248 nine-criteria filter

Chapter 04 presents the WP 248 criteria as a presumptive-trigger filter. Which rule does the chapter attach to the filter?

- A. All nine criteria must be met before a DPIA is required.
- B. Any single criterion being met forces supervisory-authority prior consultation under Article 36.
- C. Where two or more criteria are met, a DPIA is presumptively required; most enterprise AI systems processing personal data hit at least *evaluation or scoring* plus *innovative use*.
- D. The WP 248 criteria have been formally withdrawn and no longer apply to AI systems.

### 7. The Article 36 prior-consultation flag

Chapter 04 is specific about when the analyst *raises* an Article 36 flag. Which statement matches the chapter?

- A. Any DPIA that is required under Article 35 must be submitted to the supervisory authority before processing begins.
- B. Article 36 prior consultation is triggered only when the enterprise voluntarily chooses to seek guidance.
- C. If the DPIA indicates the processing would result in a high risk *in the absence of measures taken by the controller to mitigate the risk* — in practice, residuals that stay High after mitigation — the analyst raises the flag; the DPO or Head of Privacy decides whether to consult.
- D. Article 36 applies only to processing of special-category data under Article 9; standard personal data is out of scope.

### 8. Horizontal plus vertical — what a sector overlay adds

Chapter 05 frames sector-specific impact assessments as adding to, not replacing, the horizontal AIA / FRIA / DPIA. For an FDA ML-enabled medical device, which statement captures the analyst / regulatory-affairs boundary?

- A. The analyst files the 510(k) and owns the ISO 14971 risk-management file.
- B. The analyst's 42005 canonical document *is* the pre-market submission; regulatory affairs only reviews it.
- C. The analyst produces a governance-side *contribution packet* (intended-use, stakeholder, sub-group framing, post-market monitoring intent, change-control intent, transparency references); regulatory affairs assembles the submission and owns the ISO 14971 file, clinical performance analysis, predetermined-change-control-plan mechanics, and labelling regulatory language.
- D. The GMLP guiding principles are legally binding on the deployer and must be cited as rulemaking in the DPIA.

### 9. Mitchell section 7 — intersectional evaluation

Chapter 06 flags one aspect of the Mitchell paper's shape as not optional. Which statement matches the chapter?

- A. Section 7 requires only overall-model accuracy; per-group breakdowns are a stretch goal.
- B. Section 7 requires both unitary results (per-metric) and intersectional results (per-metric per-factor-combination); a 95% overall accuracy may hide 60% accuracy on group A × environment X, which is where the intersectional table surfaces.
- C. Section 7 is analyst-authored and does not require ML-team involvement.
- D. Section 7 was removed from the paper and replaced by a reference to the Hugging Face evaluation suite.

### 10. When the model card is not enough — the system card's extra sections

Chapter 07 says internal enterprise system cards extend the Mitchell nine-section model card with three additional sections. Which set matches the chapter?

- A. Composition and Deployment Context; Safety Evaluation Coverage; Change-Management Triggers.
- B. Model Details; Intended Use; Metrics.
- C. Motivation; Composition; Collection Process.
- D. Training Data; Evaluation Data; Ethical Considerations.

### 11. The datasheet's DPIA hook

Chapter 07 names the datasheet section where the training-data lawful-basis claim lives and the section where the *should-not-be-used-for* discipline runs. Which pair matches the chapter?

- A. Section 1 Motivation (lawful basis) and Section 7 Maintenance (should-not-be-used-for).
- B. Section 3 Collection Process (consent / lawful-basis claims; DPIA-relevant for any personal-data dataset) and Section 5 Uses (should-not-be-used-for sub-field — the datasheet's parallel to the model card's out-of-scope use cases).
- C. Section 4 Preprocessing (lawful basis) and Section 6 Distribution (should-not-be-used-for).
- D. Section 2 Composition (lawful basis) and Section 4 Preprocessing (should-not-be-used-for).

### 12. The six cross-reference failure modes

Chapter 08 enumerates six recurring failure modes the analyst pre-empts with the cross-reference discipline. Which set matches the chapter?

- A. Renaming drift; version drift; forked-artefact drift; dangling reference; one-way reference; verbal-only reference.
- B. Confabulation; brand-voice homogenisation; IP contamination; data leakage; over-reliance; drift.
- C. Demographic parity; equalised odds; calibration; precision; recall; selection-rate ratio.
- D. Peer review; notice; monitoring; training-data quality; human-in-the-loop; senior-official approval.

---

## Answer key

| # | Answer | Why |
|---|---|---|
| 1 | **B** | Chapter 01's "Where ISO 42005 sits in the standard stack" names the three interlocking roles: 42001 is the AIMS that *requires* an AI risk assessment and an impact assessment in Clause 6; 23894 is the AI-specific risk-management guidance (the risk-source scan-list from `mod-103`); 42005 is the AI-specific impact-assessment guidance, both procedural and documentary. |
| 2 | **B** | Chapter 01's "The shared-template idea" says the AIA, FRIA, DPIA, and sector overlays all draw from the same underlying facts, so writing each from scratch is "a fast route to inconsistent artefacts and an audit finding". The analyst-tier pattern is one canonical 42005-shaped document per system, with regulator-shaped views layered on top. |
| 3 | **B** | Chapter 02's "The questionnaire — what it asks" calls out the two distinguishing features: the questionnaire is *scored* (impact level I–IV is deterministic from the answer-set and drives the directive's process obligations) and the completed AIA is *published* on the Open Government Portal, which constrains writing style and forbids internal-only shorthand. |
| 4 | **B** | Chapter 03's "Who owes a FRIA" names exactly those four deployer classes and warns that deployers of *other* Annex III high-risk systems (e.g., Annex III point 4 employment-decision systems in the private sector) are outside Article 27 even though they carry other Article 26 deployer obligations. |
| 5 | **B** | Chapter 03's "The six required elements" and its "Mechanical points" are explicit: element (4) is to be developed *taking into account information provided by the provider under Article 13*, the provider must supply instructions for use that cover intended purpose, characteristics, capabilities, and limitations, and if that document is missing the analyst flags the gap and escalates. |
| 6 | **C** | Chapter 04's "When a DPIA is required" lists the nine WP 248 criteria and states the two-or-more rule verbatim: where two or more are met, a DPIA is presumptively required; most enterprise AI systems processing personal data hit at least criteria 1 (evaluation or scoring) and 8 (innovative use or new technological solutions), so they are in scope. |
| 7 | **C** | Chapter 04's "The DPO and Article 36 prior consultation" quotes Article 36's residual-high trigger and explains that enterprises typically use the DPIA's residual-risk column as the indicator; the analyst *raises* the flag when residuals stay High after mitigation, and legal / privacy decides whether to consult. |
| 8 | **C** | Chapter 05's "Where the pre-market submission needs impact-assessment-shaped evidence" and its "Where the sector-specific IA stops for the analyst" together draw the boundary: the analyst produces a contribution packet (intended-use, stakeholder, sub-group framing, post-market monitoring intent, change-control intent, transparency references); regulatory affairs owns the submission, the ISO 14971 file, clinical-performance analysis, the predetermined-change-control-plan mechanics, and the labelling regulatory language. |
| 9 | **B** | Chapter 06's "The Mitchell et al. sections" explicitly names intersectional evaluation as not optional: Section 7 requires both unitary and intersectional results, and the chapter uses the 95%-overall / 60%-on-group-A-×-environment-X framing to make the point. |
| 10 | **A** | Chapter 07's "System cards at internal scale" names the three extra sections verbatim: Section 10 Composition and Deployment Context (prompt templates, retrieval indices, tool inventory, guardrails, deployment surface); Section 11 Safety Evaluation Coverage; Section 12 Change-Management Triggers. Section 10 is called out as the load-bearing one. |
| 11 | **B** | Chapter 07's "Datasheets for datasets" load-bearing-analyst-tier-points list says Section 3 Collection Process is where consent-status and lawful-basis claims live and is DPIA-relevant for any personal-data dataset; Section 5 Uses holds the *should-not-be-used-for* sub-field, the datasheet's parallel to the model card's out-of-scope use cases, which is "under-populated almost universally". |
| 12 | **A** | Chapter 08's "Cross-referencing failure modes" names the six verbatim: renaming drift, version drift, forked-artefact drift, dangling reference, one-way reference, verbal-only reference. The other options cite material from other modules (GenAI risk shapes, fairness metrics, AIA process obligations). |

## Scoring

- **11–12 correct:** Fluent — ready to author a 42005-shaped canonical document, derive AIA / FRIA / DPIA / sector views from it, author an enterprise model-card supplement with a datasheet and a system card, and keep the cross-reference walk clean across the portfolio.
- **9–10 correct:** Solid. Re-read any chapter anchoring a missed question before `mod-106` (regulatory tracking — the regulator-view refresh cadence) or `mod-108` (controls — the *measures* sections feed the control library) start leaning on this fluency.
- **7–8 correct:** Partial. Re-read chapters 01 (the shared-template idea), 03 (the FRIA scope filter), and 08 (the cross-reference walk) end-to-end; those are the three most commonly fumbled under review pressure.
- **≤6 correct:** Re-read the module. The downstream modules (regulatory tracking, eval evidence, controls, incident response, communication, and `project-101`) assume this material at recall speed, not look-up speed.
