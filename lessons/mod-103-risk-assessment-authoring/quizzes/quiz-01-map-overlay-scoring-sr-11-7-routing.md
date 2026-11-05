# Quiz 01 — MAP Walk, 23894 Overlay, Scoring, SR 11-7, and Routing

**Format:** 10 multiple-choice questions, one correct answer each.
**Grounding chapters:** [01](../01-nist-rmf-map-walkthrough.md), [02](../02-iso-23894-risk-sources-overlay.md), [03](../03-genai-profile-scoring-and-register-entry.md), [04](../04-sr-11-7-shape-for-financial-services.md), [05](../05-routing-residuals-and-executive-framing.md).
**Rules:** Open-book against the chapters themselves — this quiz tests fluency, not look-up. Closed-book against anything else.

---

## Questions

### 1. The MAP 5.1 impact-framing shape

Chapter 01 names the four-part shape that every MAP 5.1 impact claim must carry before it is allowed into the register-source narrative. Which four parts?

- A. *Threat actor × attack vector × likelihood × magnitude.*
- B. *Type of harm × affected population × plausible mechanism × likelihood-and-magnitude claim.*
- C. *Regulator × obligation × control × evidence.*
- D. *Confabulation × bias × privacy × security — the four GenAI defaults applied to every impact.*

### 2. The analyst-tier altitude limits on the MAP walk

Chapter 01 draws three explicit lines around what the analyst does *not* do at MAP time. Which trio of hand-offs does the chapter name?

- A. Harm-model design → `ai-risk-engineer`; quantitative risk methodology → `senior-ai-governance-architect`; release sign-off → `ai-evaluation-engineer`.
- B. Intake triage → `mod-102`; impact assessment → `mod-105`; eval design → `mod-107` — each a downstream module, no individual role named.
- C. Risk-tolerance authoring → `CRO`; policy drafting → `General Counsel`; monitoring design → `SRE` — all enterprise-leadership hand-offs.
- D. There are no hand-offs; the analyst owns the MAP walk, the harm model, the eval design, and the release sign-off.

### 3. The two-lens sweep

Chapter 02 insists the analyst runs *two* taxonomies against every MAP 5 impact rather than one. Which pair, and why both?

- A. NIST AI RMF MAP + NIST AI RMF MEASURE — because MAP enumerates and MEASURE scores.
- B. ISO 31000 + ISO 27005 — the general-risk and infosec-risk pair the standard family provides.
- C. NIST GenAI Profile 12 risks (*what can go wrong*) + ISO/IEC 23894 risk-source categories (*where risk enters the system*) — because each lens surfaces entries the other misses.
- D. OWASP Top 10 for LLMs + MITRE ATLAS — the two adversarial taxonomies that cover the attack surface.

### 4. "Does not apply" as an audit-defensible answer

Chapter 02 is explicit that an ISO/IEC 23894 category the analyst marks *not applicable* is not a free skip. What does the chapter require instead?

- A. A full paragraph of reasoning citing the standard's clause numbers verbatim.
- B. A one-line reason recorded for each *not applicable* mark — that is the audit answer to "did you consider it?"
- C. A sign-off from the Model Risk Management group confirming the category is irrelevant.
- D. Nothing — absence on the scan sheet is a valid answer on its own.

### 5. Three columns, not one

Chapter 03 is strict that every scored register entry carries *three* ordinal claims, not one or two. Which trio, and what is each?

- A. *Low / Medium / High* — one column, three possible values.
- B. *Inherent* (before controls), *residual* (after proposed controls fire as designed), and *control-defeated* (if the load-bearing control fails or is bypassed) — three separate columns.
- C. *Likelihood / magnitude / aggregate* — likelihood and magnitude ordinals, combined into a single aggregate score.
- D. *Proposed / accepted / monitored* — three lifecycle stages, not three risk views.

### 6. The five proposed-mitigation categories

Chapter 03's proposed-mitigation field uses five category labels. Which set matches the chapter?

- A. Preventive / detective / corrective / transfer / accept.
- B. Prevent / detect / respond / recover / review.
- C. Mandatory / recommended / optional / stretch / deferred.
- D. Technical / administrative / physical / contractual / cultural.

### 7. Why the analyst does not aggregate ordinals into a single system score

Chapter 03 explicitly prohibits collapsing the register into "overall system risk: Medium" for the executive summary. What is the chapter's reasoning?

- A. Executives prefer long detailed registers and reject aggregate scores on principle.
- B. Ordinal aggregation is arithmetically indefensible and hides the profile — the executive should read the individual claims, especially the highest-residual and highest control-defeated items, not a single collapsed grade.
- C. The GRC platform cannot render aggregate scores, so the register has to stay disaggregated.
- D. Aggregation is fine at analyst tier but prohibited at architect tier — the analyst *is* expected to produce the single aggregate.

### 8. What SR 11-7 adds that the NIST AI RMF does not spell out at the same depth

Chapter 04 names three concrete additions SR 11-7 brings to an AI RMF-only program when the enterprise is a regulated US FSI. Which trio?

- A. Prohibited practices; use-case tiering; transparency disclosures.
- B. A board-approved AI ethics code; a Chief AI Officer role; an AI incident disclosure rule.
- C. Explicit developer/validator independence as a formal role; materiality tiering of models; mandatory ongoing performance monitoring for material models.
- D. A single standardised model-card template; a mandatory third-party audit; a public model registry.

### 9. The three characteristic owner pushbacks in a routing round

Chapter 05 shapes the negotiation round around three owner-response patterns the analyst should expect. Which trio, and what does each imply for the register?

- A. "Approve" / "deny" / "escalate" — a three-way decision with no re-scoring.
- B. "You're too high — we have a control you haven't seen" (add the control and re-score); "you're too low — this thing scares us more than you realise" (update or leave with disagreement logged); "we disagree with the routing — this should belong to X team" (re-route if defensible, otherwise hold and log).
- C. "Not my risk" / "not my team" / "not my problem" — three forms of refusal routed to the governance council.
- D. "Accept with monitoring" / "accept with transfer" / "accept with escalation" — three acceptance flavours, no contested paths.

### 10. The three do-nots in the executive framing

Chapter 05 lists three pieces of language that must *not* appear in the one-page executive framing, even when the underlying claim might be defensible elsewhere. Which three?

- A. Named owner / named date / named control — the executive summary is anonymised.
- B. A single aggregated system risk score; legal-opinion language ("compliant with GDPR Art. 35"); release-sign-off language ("safe to release" / "cleared for launch").
- C. Low-materiality claims; Transfer-category mitigations; Accept-category mitigations — all three signal under-rigour.
- D. The incident citation; the residual claim; the control-defeated claim — three facts the executive cannot act on.

---

## Answer key

| # | Answer | Why |
|---|---|---|
| 1 | **B** | Chapter 01's MAP 5 section and the "what to memorise" bullets both name the impact-framing shape as *type of harm × affected population × plausible mechanism × likelihood-and-magnitude claim*. That framing is what the register entries draw from. |
| 2 | **A** | Chapter 01's "What analyst-tier MAP is *not*" section explicitly defers harm-model design to `ai-risk-engineer`, quantitative risk methodology to `senior-ai-governance-architect`, and release sign-off to `ai-evaluation-engineer`. These are three named individual-role hand-offs, not module hand-offs. |
| 3 | **C** | Chapter 02's "The two-lens sweep" section describes the GenAI Profile as the *what can go wrong* lens and ISO 23894 as the *where does risk enter the AI system* lens, and states that neither lens alone would surface the full enumeration — both together give the reviewer a defensible completeness case. |
| 4 | **B** | Chapter 02 states explicitly: "Categories marked *not applicable* are marked with a one-line reason — that is your audit answer to 'did you consider it?'" The scan is not about filling every category, it is about *asking* every category and recording the reason either way. |
| 5 | **B** | Chapter 03's "Inherent vs residual vs control-defeated" section defines the three as separate columns: inherent (before any control fires), residual (after the controls the analyst believes will be in place fire as designed), and control-defeated (if a control fails, is bypassed, or is silently misconfigured). The chapter notes the reviewer will ask the control-defeated question and the analyst who has pre-computed it answers immediately. |
| 6 | **A** | Chapter 03's "The proposed-mitigation field" section lists the five categories verbatim: preventive (reduces likelihood), detective (surfaces the risk), corrective (mitigates the impact when it fires), transfer (moves the risk to a third party), and accept (knowingly retained with rationale). |
| 7 | **B** | Chapter 03's "Executive-audience translation" and "What to memorise" sections both state the rule: *do not aggregate ordinal claims into a system score; report the profile.* The chapter calls ordinal aggregation "lossy and misleading" and asks the analyst to report individual claims so the executive can read the profile — in particular the highest residual and the highest control-defeated items. |
| 8 | **C** | Chapter 04's "What SR 11-7 adds that AI RMF alone does not" section names the three additions: explicit developer/validator independence as a formal role (MRM is a separate reporting line); model tiering by materiality (decision-materiality and potential loss, peer of the EU AI Act tier but monetary-framed); and mandatory ongoing monitoring for material models (outcomes analysis, back-testing, benchmarking) — where AI-specific drift and fairness monitors plug in. |
| 9 | **B** | Chapter 05's "The residual-claim negotiation" section names the three pushback shapes verbatim and the correct analyst response for each — request evidence and re-score for the "too high" case; capture the mechanism and either update or log disagreement for the "too low" case; check the routing table and the enterprise RACI and re-route only if defensible for the "wrong team" case, never silently accept an orphan. |
| 10 | **B** | Chapter 05's "What the executive should not see" section lists the three: no aggregated single score (ordinal aggregation is prohibited — see question 7); no legal-opinion language ("Compliant with GDPR Art. 35" is a legal claim — use "DPIA completed; findings closed"); no release-sign-off language ("Safe to release" is `ai-evaluation-engineer` scope — use "acceptable-to-proceed pending evaluation-engineer sign-off"). The "What to memorise" bullets at the end of the chapter restate the three as the *three do-nots*. |

## Scoring

- **9–10 correct:** Fluent — ready to author a first-draft risk assessment end-to-end: MAP walk, 23894 overlay, scored register, routing packets, and one-page executive framing.
- **7–8 correct:** Solid. Re-read any chapter anchoring a missed question before `mod-105` (impact assessments) and `mod-108` (controls and evidence) lean on this fluency.
- **5–6 correct:** Partial. Re-read chapters 03 and 05 end-to-end — the scoring discipline and the routing/executive-framing discipline are the two most commonly fumbled under review pressure.
- **≤4 correct:** Re-read the module. Downstream modules (impact assessments, eval evidence, controls, incident response) assume this material at recall speed, not look-up speed.
