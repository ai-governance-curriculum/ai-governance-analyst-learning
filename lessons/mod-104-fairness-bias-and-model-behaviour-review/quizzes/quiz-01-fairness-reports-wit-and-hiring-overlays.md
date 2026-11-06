# Quiz 01 — Fairness Metrics, Report Reading, WIT, and the Hiring Overlay

**Format:** 11 multiple-choice questions, one correct answer each.
**Grounding chapters:** [01](../01-fairness-metric-glossary-and-limits.md), [02](../02-reading-fairlearn-and-aif360-reports.md), [03](../03-what-if-tool-code-free-exploration.md), [04](../04-hiring-ai-overlays-ll144-eeoc.md).
**Rules:** Open-book against the chapters themselves — this quiz tests fluency, not look-up. Closed-book against anything else.

---

## Questions

### 1. What demographic parity cannot tell you

Chapter 01 insists that even when a report shows demographic parity is satisfied, the analyst still records what the metric *cannot* speak to. Which claim is it most important to hold open?

- A. Whether the model is well-calibrated across groups — equal selection rates can hide very different score-to-outcome mappings.
- B. Whether *base rates* of the positive class differ across groups — equal selection rates can only be achieved by ignoring real signal if the underlying rates differ.
- C. Whether the training-test split was stratified — demographic parity assumes a stratified split.
- D. Whether the vendor bias-audit report is independent — demographic parity presumes an independent auditor.

### 2. The fairness impossibility result

Chapter 01 cites Chouldechova (2017) and Kleinberg / Mullainathan / Raghavan (2016) for the impossibility result. Which trio of properties does the result say cannot simultaneously hold except in trivial cases?

- A. Demographic parity; equalised odds; four-fifths rule.
- B. Calibration within groups; equal false positive rates across groups; equal false negative rates across groups.
- C. Group fairness; individual fairness; counterfactual fairness.
- D. Selection-rate parity; precision parity; recall parity.

### 3. The four-fifths rule, framed correctly

Chapter 01 is careful about *what* the four-fifths rule is evidence of. Which statement matches the chapter?

- A. A disparate-impact ratio below 0.80 is a legal finding that Title VII has been violated.
- B. A disparate-impact ratio below 0.80 is treated as presumptive evidence of adverse impact under the EEOC Uniform Guidelines, which then triggers the business-necessity analysis — not a legality determination by itself.
- C. The four-fifths rule applies only to credit scoring and loan underwriting, not to hiring selection procedures.
- D. The four-fifths rule is an industry best practice with no regulator recognition; the analyst files it as an advisory finding.

### 4. Generative-AI biases that classical metrics do not cover

Chapter 01 names four bias shapes that appear in generative-AI outputs and do *not* fit the binary-classifier framing of demographic parity, equalised odds, or calibration. Which set matches the chapter?

- A. Confabulation; refusal; toxicity; copyright leakage.
- B. Representation; association; refusal; quality.
- C. Privacy; security; transparency; accountability.
- D. Pre-processing; in-processing; post-processing; adversarial debiasing.

### 5. The five-thing reading pass

Chapter 02's "what to look for first" list is a specific ordered sequence the analyst runs against a Fairlearn report. Which trio *correctly* names three of the five things (in the chapter's framing)?

- A. Sample sizes per group; selection-rate ratio against the four-fifths threshold; calibration slope per group.
- B. Confidence intervals; p-values on statistical-parity tests; a multiple-comparisons correction.
- C. Choice of mitigation algorithm; before-vs-after-mitigation deltas; accuracy on the training distribution.
- D. The vendor's branding; the auditor's independence statement; the publication URL.

### 6. The common omissions in a Fairlearn report

Chapter 02 names four omissions the analyst routinely has to ask for before a bias-audit report can be considered complete. Which set matches the chapter?

- A. Base rates per group; confidence intervals; sub-group (intersectional) breakdown; fairness on an out-of-time hold-out.
- B. The mitigation algorithm used; the primary fairness metric adopted; the business-necessity argument; the auditor's name.
- C. Training-data provenance; red-team findings; copyright clearance; data-retention schedule.
- D. The EU AI Act tier tag; the NIST MAP subcategory; the SR 11-7 pillar; the ISO 42001 clause.

### 7. The five-question non-technical summary

Chapter 02 says the stakeholder does not want the metric table — they want to know five specific things. Which set matches the five questions?

- A. What is the inherent risk? What is the residual? What is the control-defeated? Who is the owner? When is the next review?
- B. Which GenAI Profile risks apply? Which ISO 23894 sources apply? Which NIST MAP subcategory? Which EU AI Act Annex? Which ISO 42001 clause?
- C. Was a fairness audit done (and when)? What is the bottom line per group? What are we doing about any breaches? What could the audit have missed? When is the next audit?
- D. Is the model compliant with Title VII? Compliant with LL 144? Compliant with the EU AI Act? Compliant with ECOA? Safe to release?

### 8. The analyst-tier response when the per-group confusion matrix is missing

Chapter 01 names the per-group confusion matrix as the *base artefact* from which almost every fairness metric is derived. What does the chapter say the analyst does when the report cites metrics but omits the per-group confusion matrices?

- A. Recompute the matrix from the raw dataset so the review can proceed.
- B. Treat the report as complete — the derived metrics stand on their own and the matrix is auditor-tier detail.
- C. Treat the report as *incomplete* and request the per-group matrices from the ML team; without them, the specific metric definitions cannot be verified.
- D. Escalate to Legal for a statutory opinion before any further reading.

### 9. Reading a WIT counterfactual well

Chapter 03 is explicit about what a nearest-counterfactual observation in the What-If Tool *does* and *does not* say. Which reading matches the chapter?

- A. A counterfactual whose flipping feature is a plausible proxy for a protected attribute is a *determination* that the model is unfair; the analyst files it as a confirmed finding.
- B. WIT's nearest counterfactual is the nearest in *feature space* (an L1/L2 neighbour) — a small change that flips the prediction is a *route to the ML team*, not a determination, and proxy-looking flipping features are the specific shape worth flagging.
- C. Counterfactuals only matter for generative-AI systems; for classifiers they are decorative.
- D. A counterfactual that differs on the protected attribute itself and flips the prediction can be ignored because WIT's distance metric is unreliable at group boundaries.

### 10. The four NYC Local Law 144 employer obligations

Chapter 04 names four distinct obligations an employer takes on when deploying an automated employment decision tool for a candidate for an NYC-based role. Which set matches the chapter?

- A. Annual independent bias audit; publicly posted audit summary; candidate notification at least 10 business days before use; published data-protection information (categories collected and retention period, where applicable).
- B. Annual red-team exercise; quarterly model-card update; monthly drift report; weekly incident review.
- C. EU AI Act FRIA; Article 26 deployer plan; Article 50 transparency notice; Article 27 impact assessment.
- D. SR 11-7 validation; MRM sign-off; CFPB disclosure; OCC 2023-17 third-party review.

### 11. The EEOC 2023 AI-adverse-impact guidance — the two load-bearing claims

Chapter 04 highlights two specific claims from the EEOC's May 2023 guidance on "Assessing Adverse Impact in Software, Algorithms, and AI." Which pair matches the chapter?

- A. The four-fifths rule does *not* apply to AI selection tools; vendors are solely responsible for any disparate-impact analysis.
- B. The four-fifths rule *does* apply to AI selection procedures (vendor claims to the contrary are wrong), and the *employer* using the tool — not the vendor — is responsible for the disparate-impact assessment.
- C. The four-fifths rule is superseded by a new 0.90 threshold for AI, and the employer is responsible for computing it.
- D. The guidance mandates that AI selection tools obtain prior EEOC approval before deployment, and the vendor is the responsible party.

---

## Answer key

| # | Answer | Why |
|---|---|---|
| 1 | **B** | Chapter 01's "Demographic parity" section names base rates explicitly: if the underlying positive rate differs across groups, demographic parity can only be achieved by ignoring real signal, which is a live debate the analyst records rather than resolves. A, while true as a general property (the chapter also notes calibration can be violated when demographic parity holds), is secondary to the base-rate point that the chapter uses to anchor what the metric does not tell you. |
| 2 | **B** | Chapter 01's "The impossibility result" section states the trio verbatim: calibration within groups, equal false positive rates across groups, and equal false negative rates across groups cannot simultaneously hold except in trivial cases. The chapter cites Chouldechova (2017) and Kleinberg / Mullainathan / Raghavan (2016). |
| 3 | **B** | Chapter 01's "Disparate-impact ratio" section and the "Analyst-tier framing" bullet both say the four-fifths breach gets a remediation ticket but does *not* conclude the model is illegal — it triggers the business-necessity / adverse-impact analysis under the Uniform Guidelines. Chapter 04 restates the same frame around burden-shift. |
| 4 | **B** | Chapter 01's "Calibration in generative outputs — beyond classification" section enumerates representation bias, association bias, refusal bias, and quality bias as the four generative shapes the classical metrics do not directly cover. |
| 5 | **A** | Chapter 02's "What to look for first" names the five in order: sample sizes per group; selection-rate ratio against the four-fifths threshold; TPR/FPR differences; calibration slope per group; precision differences. Option A picks three of the five from that list verbatim. B names things the chapter explicitly says are *not* analyst scope (confidence intervals and p-values are model-evaluation-engineer territory); C is AIF360 content, not the Fairlearn reading pass; D is the vendor-report wrapper, not the reading pass. |
| 6 | **A** | Chapter 02's "What the report often omits" section lists the four verbatim: base rates per group, confidence intervals, sub-group (intersectional) breakdown, and fairness on an out-of-time hold-out. Each omission is an analyst-tier follow-up ask. |
| 7 | **C** | Chapter 02's "Reading a report for a non-technical stakeholder" section lists the five questions: was a fairness audit done (and when); what is the bottom line (named metric, breach per group); what are we doing about breaches; what could the audit have missed (coverage gaps); when is the next audit. Options A and B are from `mod-103`'s register discipline; D is a legal-opinion shape the chapter 02 summary explicitly avoids. |
| 8 | **C** | Chapter 01's "Confusion matrix per group — the base artefact" section says the per-group confusion matrix is the base from which almost every fairness metric is derived; when it is missing, the analyst-tier response is to request it from the ML team because the specific metric definitions cannot otherwise be verified. Recomputing the matrix (A) is ML-team scope; treating the report as complete (B) is the mistake the chapter is warning against. |
| 9 | **B** | Chapter 03's "Counterfactuals — reading them well" section is explicit that WIT surfaces the nearest neighbour in *feature space* (not the nearest *fair* counterfactual), that a small change flipping the prediction is a *finding* routed to the ML team rather than a determination, and that a plausible proxy as the flipping feature is the specific shape worth flagging. Option A overstates the certainty of per-datapoint evidence, which the chapter warns against. |
| 10 | **A** | Chapter 04's "NYC Local Law 144 — the AEDT rule" section lists the four employer obligations verbatim: annual independent bias audit within one year of use; publicly posted audit summary; candidate notification at least 10 business days before use with the required content; published data-protection information (categories collected and, if applicable, retention period). |
| 11 | **B** | Chapter 04's "Title VII framing" section quotes the two key claims from the EEOC's May 2023 guidance on "Assessing Adverse Impact in Software, Algorithms, and Artificial Intelligence": (1) the four-fifths rule applies to AI selection procedures and vendors who claim otherwise are wrong, and (2) the employer using the AI selection tool is responsible for the disparate-impact assessment, not the vendor. |

## Scoring

- **10–11 correct:** Fluent — ready to read a Fairlearn / AIF360 / vendor bias-audit report, run a WIT walk, and attach the hiring-overlay pack at intake with the correct statutory anchors.
- **8–9 correct:** Solid. Re-read any chapter anchoring a missed question before `mod-105` (impact assessments and model cards) or `mod-107` (eval / audit evidence) start leaning on this fluency.
- **6–7 correct:** Partial. Re-read chapters 01 and 04 end-to-end — the metric vocabulary and the Title VII / LL 144 overlay are the two most commonly fumbled under review pressure.
- **≤5 correct:** Re-read the module. The downstream modules (impact assessments, eval evidence, controls, incident response, communication) assume this material at recall speed, not look-up speed.
