# Quiz 01 — Intake, Triage, Inventory, GRC Platforms, and Reconciliation

**Format:** 10 multiple-choice questions, one correct answer each.
**Grounding chapters:** [01](../01-intake-questionnaire-design.md), [02](../02-triage-and-tier-tagging-workflow.md), [03](../03-inventory-row-and-registry-sync.md), [04](../04-grc-platforms-for-ai-at-analyst-level.md), [05](../05-pandas-and-excel-reconciliation.md).
**Rules:** Open-book against the chapters themselves — this quiz tests fluency, not look-up. Closed-book against anything else.

---

## Questions

### 1. The three field groups on the intake questionnaire

Chapter 01's canonical intake schema is built on a *three-way split* of its fields. Which split is it, and who fills each group?

- A. **Public / internal / restricted** — split by data-sensitivity label, with Security filling the restricted group.
- B. **Mandatory / optional / stretch** — split by whether the field blocks intake, with the requester filling mandatory and the analyst filling the rest.
- C. **Business-facing / technical / governance-fill** — the requester fills the business-facing group; the requester fills the technical group with help (or an ML partner completes after routing); the analyst fills the governance-fill group.
- D. **NIST / ISO / EU** — one group per framework anchor, filled by whichever framework owner is on call that week.

### 2. "Unsure" as a first-class answer

Chapter 01 insists that several yes/no fields on the intake carry a third answer: "unsure — please help me confirm". Which failure mode is that rule guarding against?

- A. Requesters padding the form with uncertainty to delay governance review.
- B. Requesters guessing wrong on questions like *personal data involved?* or *automated decision-making about individuals?* so the intake routes incorrectly — "unsure" routes to a joint follow-up instead.
- C. The GRC platform rejecting the form for having blank fields.
- D. Analysts being unable to count "yes" responses if "unsure" is an allowed answer.

### 3. The autonomy-level definition

Chapter 01 pastes in a verbatim plain-English gloss for the four autonomy levels. Which of the four descriptions below matches **"Semi-autonomous"** as the chapter defines it?

- A. The system produces a suggestion that a human always sees and always decides.
- B. The system drafts something a human edits before it goes out.
- C. The system acts by default; a human can override before the action commits.
- D. The system acts and commits without human intervention on the specific instance.

### 4. Walking the EU AI Act decision tree

An analyst is triaging a new intake and wants to apply chapter 02's five-step EU AI Act tagging walk in order. Which sequence matches the chapter?

- A. Article 50 (transparency) → Annex I → Annex III → Article 5 → residual minimal.
- B. Article 5 (prohibited) → Annex I (safety-component) → Annex III (use-case) → Article 50 (transparency) → residual minimal.
- C. Annex III → Article 5 → Article 6(3) derogation → Annex I → Article 50.
- D. Residual minimal → Article 50 → Annex III → Annex I → Article 5 (so the lightest tier is checked first).

### 5. Triaging an under-specified intake

Chapter 02's "Intake C" vignette is a PM asking about "using AI to help our customer support team", with no purpose statement, no business owner, and no deployment surface named. Which bucket does the chapter put it in, and what does the analyst do next?

- A. **Out-of-scope** — the intake does not meet the enterprise definition and is routed to Procurement.
- B. **In-scope** — the analyst tags EU AI Act limited risk by default and starts the risk assessment.
- C. **Needs follow-up** — the analyst returns the intake with specific questions on the missing fields and an SLA (chapter 02 names three business days).
- D. **Rejected** — the intake is closed with no routing.

### 6. What the inventory is *not*

Chapter 03 draws sharp lines between the governance inventory and three peer artefacts. Which statement captures the distinction the chapter makes?

- A. The inventory *is* the model registry — the ML team's registry just adds engineering fields on top.
- B. The inventory is per-*system*; the risk register is per-*risk*; the control matrix is a Statement-of-Applicability slice per system; the model registry carries engineering facts (artefacts, hyperparameters, training runs). A single inventory row points at many risk-register entries.
- C. The inventory is per-*risk*; the risk register is per-*system*; the control matrix is the model registry under a different name.
- D. The inventory, the risk register, and the control matrix are three views on the same underlying table and share a primary key.

### 7. Material change — what fires re-assessment

Chapter 03 enumerates the signals that count as a *material change* and trigger a re-assessment cycle. Which of the following would **not** fire a re-assessment under the chapter's list?

- A. The hosted foundation model is swapped from one vendor to another.
- B. The system is rolled out from an internal user population to external customers.
- C. A bug-fix patch is deployed that leaves the model, data sources, autonomy level, deployment surface, and user population unchanged.
- D. A new tool (an email-sending API) is added to an agentic pipeline's tool list.

### 8. Picking the GRC-for-AI vendor by emphasis

Chapter 04 characterises the four named vendors by their analyst-tier emphasis. Which pairing matches the chapter?

- A. Credo AI → ModelOps lifecycle and continuous monitoring; ServiceNow AI Control Tower → technical audit modules; Holistic AI → workflow and ITSM integration; ModelOp → prebuilt intake templates and policy attach.
- B. Credo AI → prebuilt intake templates and policy-attach; Holistic AI → technical audit and monitoring modules producing per-system risk reports; ModelOp → model lifecycle inventory and continuous-monitoring integration; ServiceNow AI Control Tower → workflow automation layered on the Now Platform / ITSM stack.
- C. All four vendors converge on the same analyst-tier feature set, so the chapter does not distinguish them.
- D. Credo AI → ITSM-integrated workflow; Holistic AI → prebuilt intake templates; ModelOp → policy-attach; ServiceNow AI Control Tower → technical bias audits.

### 9. Spreadsheet-fallback discipline

Chapter 04 lists the spreadsheet-fallback discipline rules that keep the fallback as auditable as a tool-hosted equivalent. Which of the following is **not** one of them?

- A. Version-control the files (shared drive with revision history at minimum; git repo if the enterprise allows).
- B. Log every change with a timestamp and initials — in a tool this is automatic, in a spreadsheet you do it manually.
- C. Freeze exports on any decision date (council meeting, regulator response, audit) — the frozen exports are the evidence, not the live spreadsheet.
- D. Scatter the master files across each analyst's local laptop so that an outage at the shared drive cannot take the program down.

### 10. The three sets the weekly reconciliation produces

Chapter 05's pandas walk builds its reconciliation output as a three-set diff between the model registry and the governance inventory. Which three sets, and what does each shape mean?

- A. **Registry-only** (likely shadow AI — ML team deployed without governance intake), **Inventory-only** (often a retired system or a stale entry), and **Both-with-drift** (present in both but with a material-change signal since the last review).
- B. **High-risk / Limited-risk / Minimal** — the output partitions systems into EU AI Act tiers.
- C. **To-do / In-progress / Done** — the output is a Kanban of open governance tasks.
- D. **Owned / Unowned / Orphan** — the output partitions rows by who the business owner is.

---

## Answer key

| # | Answer | Why |
|---|---|---|
| 1 | **C** | Chapter 01's "Field-by-field — the canonical intake row" section organises the whole schema under **Business-facing (requester fills)**, **Technical (requester fills with help, or ML partner completes after routing)**, and **Governance-fill (analyst / governance owner completes)** tables, and the "Why the field split matters" section names the pattern explicitly as business-then-technical-then-governance. |
| 2 | **B** | Chapter 01's "Field patterns that fail in production" section calls out the "Yes/no where 'unsure' is the correct third option" anti-pattern on personal data, automated decision-making, and jurisdiction, and the "What to memorise" bullet names the rule: *capture 'unsure' as a first-class answer; it routes correctly, guessing does not*. |
| 3 | **C** | Chapter 01's "Field definitions matter more than field count" section pastes the four autonomy-level definitions verbatim; *Semi-autonomous* is "the system acts by default; a human can override before the action commits". A is Advisory, B is Assistive, D is Autonomous. |
| 4 | **B** | Chapter 02's "The EU AI Act tier — the primary hook" section lists the walk as 1) Article 5 prohibited → Unacceptable; 2) Annex I safety-component → High-risk (Annex I); 3) Annex III use-case → High-risk (Annex III); 4) Article 50 interaction / synthetic content / biometric categorisation → Limited-risk; 5) None of the above → Minimal risk. Walking out of order is the common failure. |
| 5 | **C** | Chapter 02's "Intake C" vignette in "Concrete example — three intakes on a Monday morning" explicitly lands on **needs-follow-up** because purpose statement is missing, business owner is unnamed, and deployment surface is not specified — the analyst returns the intake with three specific questions and an SLA of three business days. |
| 6 | **B** | Chapter 03's "What the inventory is *not*" section draws the lines: the model registry carries engineering facts; the risk register is per-risk (one row per identified risk item); the control matrix is a Statement-of-Applicability slice per system. The inventory is per-system and points at many risk-register entries. Option A conflates inventory with registry — the specific failure the chapter warns against. |
| 7 | **C** | Chapter 03's "The material-change definition" section lists the triggering changes (model family / provider, data sources / fine-tune, autonomy level, deployment surface, user population, new tools in an agentic pipeline, jurisdictions, material incidents) and then names "a bug-fix patch, a prompt-template tweak that does not change intent, a monitoring-tool swap" as examples of **non-material** changes that get logged but do not fire re-assessment. |
| 8 | **B** | Chapter 04's per-vendor sections characterise Credo AI around prebuilt templates and policy-attach, Holistic AI around technical audit and monitoring modules producing per-system risk reports, ModelOp around the ModelOps / lifecycle-and-monitoring surface, and ServiceNow AI Control Tower as workflow automation on the Now Platform / ITSM install. |
| 9 | **D** | Chapter 04's "Spreadsheet-fallback discipline" bullets list version-control, timestamp-and-initials change logging, freezing exports on decision dates — and explicitly end with *"Do not scatter across multiple owners' local copies. One authoritative version, one edit at a time."* D is the exact anti-pattern the chapter prohibits. |
| 10 | **A** | Chapter 05's "The reconciliation shape" section defines the three sets as **Registry-only** (almost always a *shadow AI* row — ML team deployed without governance intake), **Inventory-only** (often benign retirement; sometimes a stale entry), and **Both, but material-change drift** (present in both with a new version / provider / owner / data source signal since the last review). |

## Scoring

- **9–10 correct:** Fluent — ready to sit intake, triage, and weekly reconciliation on day one.
- **7–8 correct:** Solid. Re-read the chapters anchoring any missed questions before `mod-103` leans on this fluency.
- **5–6 correct:** Partial. Re-read chapters 01, 02, and 03 end-to-end — these three carry the most downstream weight for every subsequent module.
- **≤4 correct:** Re-read the module. Downstream modules (risk assessment authoring, impact assessments, controls-and-evidence) assume this material at recall speed, not look-up speed.
