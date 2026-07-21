# Scoring the Register Entry — GenAI Profile Risks and the Likelihood-Magnitude Pass

## Why this chapter

An unscored register entry is a comment, not a governance artefact. The scoring pass turns each identified risk into an actionable decision: is this something the enterprise accepts, mitigates, transfers, or avoids? Which owner does the routing land on? Does the residual claim make the system OK to run?

At analyst tier you score with *ordinal* claims (Low / Medium / High) grounded in reasoning a reviewer can challenge — not quantitative probability distributions. Quantitative methodology (frequency-and-severity models, portfolio-level aggregation, monetised loss estimates) is [senior AI governance architect](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) scope. This chapter walks the ordinal shape.

## The scoring grid

Most enterprise programs run on a 3×3 or 5×5 grid.

For an entry-level analyst, the 3×3 is more forgiving and — for a first-draft register — usually sufficient. The 5×5 gets more precision at the cost of more argument over category boundaries.

| Likelihood | Definition (rough guidance) |
|---|---|
| **Low** | Not expected in normal operation; would require a rare combination of failures |
| **Medium** | Plausible under normal operation; expected occasionally within the enterprise's use of the system |
| **High** | Expected in normal operation; the system will exhibit this regularly unless mitigated |

| Magnitude | Definition (rough guidance) |
|---|---|
| **Low** | Contained blast radius; recoverable at low cost; no material regulatory, reputational, or user-harm exposure |
| **Medium** | Material internal cost; recoverable but with visible effort; contained regulatory or reputational exposure |
| **High** | Broad blast radius; user harm, regulatory-reportable event, or headline-grade reputational damage |

Every ordinal claim is paired with **a one-line rationale** the reviewer can push on. "Medium likelihood: hosted LLMs confabulate on niche facts multiple times per user session in observed evaluation."

## Inherent vs residual vs control-defeated

Three distinct scores exist per register entry. The analyst is careful to keep them apart.

- **Inherent risk.** Before any controls fire. What the risk would be if the system ran with no protection.
- **Residual risk.** After the controls the analyst *believes will be in place* fire. This is the analyst's operational-risk claim.
- **Control-defeated risk.** What happens if a control fails, is bypassed, or has been silently misconfigured. Sometimes called *residual-if-defeated* or *worst-case residual*.

The reviewer often asks: *"what does the residual look like if control X fails?"* An analyst who has already thought about control-defeated risk answers immediately; an analyst who has only computed residual has to redo the pass.

The Basel-style shape (used implicitly by [SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) and other financial-services frames) treats the three as separate columns on the risk register. Adopt the same shape for AI risk registers.

## The routing decision

Every register entry routes to an owner. The routing is a formal decision, not a "we'll figure it out later" — the register entry is not complete until the owner is named and has acknowledged.

Analyst-tier routing table:

| Risk pattern | Default owner | Framework anchor |
|---|---|---|
| Confabulation, groundedness, factual accuracy | Product owner (with ML support) | NIST MAP 5, MEASURE 2 |
| Bias, fairness, disparate impact | Product owner (fairness lens); Legal (EEOC / LL 144 / disparate-impact overlays) | NIST MAP 5, MEASURE 2.11 |
| Data privacy, personal data leakage, memorisation | Privacy team | GDPR Art. 35; NIST MAP 5 |
| Information security, prompt injection, adversarial | Security team | OWASP LLM Top 10; NIST MAP 4 |
| IP contamination, copyright | Legal | NIST MAP 4.1 |
| Environmental impact | Sustainability / Operations owner | GenAI Profile #5 |
| Human-AI configuration, over-reliance | Product / UX owner | GenAI Profile #7 |
| Value chain / third-party component | Governance (analyst) with vendor owner | GenAI Profile #12; NIST GOVERN 6 |

The analyst files the entry, names the owner, and CC's the governance record. The owner acknowledges within an SLA (typically five business days). Non-acknowledged entries go on the governance council agenda.

## The proposed-mitigation field

Analyst-tier mitigations are *proposed* — the owner is the one who accepts or edits. The analyst-tier framing:

- **Preventive** — a control that reduces likelihood (e.g., a system prompt template that constrains topic; a PII scanner on prompts before they reach the LLM).
- **Detective** — a control that surfaces the risk when it happens (e.g., an anomaly monitor; a fairness metric on a fixed monitoring dataset).
- **Corrective** — a control that mitigates the impact when it fires (e.g., a rollback plan; a customer-facing correction procedure).
- **Transfer** — the risk moves to a third party (e.g., contractual indemnification from the vendor; insurance).
- **Accept** — the risk is knowingly retained; documented with rationale.

Proposed-mitigation entries name the control category and one plausible instance. The owner picks the actual control.

## Scoring the MCDA register

Applying the shape to the MCDA register skeleton from the previous chapter.

### RR-2026-0212 — Confabulation of product facts
- **Inherent.** Likelihood: High (hosted LLM confabulates on niche product facts under observed prompts). Magnitude: Medium (contained by review workflow; escalates to High if a confabulated fact reaches customer-facing copy).
- **Proposed controls.** *Preventive:* retrieval grounding against internal product datasheets; system-prompt guardrails against fact-generation about unreleased products. *Detective:* accuracy eval per release. *Corrective:* copywriter review workflow is a soft-corrective; incident-response runbook for a customer-facing confabulation.
- **Residual.** Likelihood: Medium. Magnitude: Medium.
- **Control-defeated.** If review workflow fails (copywriter accepts an output verbatim): Likelihood remains Medium. Magnitude: High.
- **Owner.** Marketing Ops (Priya Nair).

### RR-2026-0213 — Brand-voice homogenisation
- **Inherent.** Likelihood: Medium. Magnitude: Medium.
- **Proposed controls.** *Preventive:* per-brand prompt templates; style-guide grounding. *Detective:* periodic brand-voice audit by Marketing Ops.
- **Residual.** Likelihood: Low. Magnitude: Medium.
- **Control-defeated.** If per-brand templates are not maintained: Likelihood: Medium. Magnitude: Medium.
- **Owner.** Marketing Ops.

### RR-2026-0214 — IP contamination
- **Inherent.** Likelihood: Low. Magnitude: Medium.
- **Proposed controls.** *Preventive:* vendor terms explicitly cover training-data indemnification; internal legal review on any copyright-adjacent template. *Detective:* copywriter review is a soft-detective for near-verbatim phrases.
- **Residual.** Likelihood: Low. Magnitude: Medium.
- **Control-defeated.** If vendor indemnification does not cover the failure mode: Likelihood: Low. Magnitude: High.
- **Owner.** Legal.

### RR-2026-0215 — Data leakage in prompts
- **Inherent.** Likelihood: Medium (users paste unreleased brief content). Magnitude: High (vendor sees pre-release strategy).
- **Proposed controls.** *Preventive:* PII / confidentiality scanner on prompts pre-flight; user-facing prompt hygiene guidance. *Detective:* prompt audit-log review.
- **Residual.** Likelihood: Low. Magnitude: High.
- **Control-defeated.** If the scanner is bypassed or misses a novel confidentiality pattern: Likelihood: Medium. Magnitude: High.
- **Owner.** Privacy + Security.

Each entry now carries an owner, an inherent claim, a proposed control shape, a residual claim, and a control-defeated claim. That is the analyst-tier scoring pass complete for the system.

## Executive-audience translation

The register carries the reasoning. The executive audience sees a shorter form:

- **Overall residual profile.** For MCDA, three Medium-magnitude items and one High-magnitude item, all with Low or Medium residual likelihood. Verdict: the system is *acceptable to run* with the proposed control set in place; monitoring will re-check quarterly.
- **Highest-residual concern.** Data leakage in prompts (residual Low × High) — the executive is aware because the control-defeated case is High-High.
- **Boundary condition.** Confabulation control-defeated is Medium × High — the executive is aware that if the review workflow lapses, this system is materially riskier than the register otherwise suggests.

The analyst is careful not to *aggregate* the ordinal claims into a single "system risk score". Ordinal aggregation is lossy and misleading; report the individual claims, and let the executive read the profile.

## What analyst-tier scoring is *not*

- **Not a quantitative model.** Frequency × severity × time is architect scope. Analyst uses ordinal claims with reasoning.
- **Not a portfolio view.** Aggregating risk across many systems is architect / head-of-governance scope.
- **Not the release decision.** The scored register informs release; the AI Evaluation Engineer signs off.
- **Not a legal opinion.** "Residual: Low" does not mean "compliant with obligation X" — the analyst does not opine on obligations. Legal owns that.

## What to memorise

- The **3×3 grid** definitions of Low / Medium / High.
- **Inherent vs residual vs control-defeated** — three separate columns.
- The **routing table** — which owner defaults for which risk pattern.
- The **five mitigation categories**: preventive, detective, corrective, transfer, accept.
- The rule: **do not aggregate ordinal claims into a system score**; report the profile.

## Summary

The scoring pass turns the enumerated register entries into ordinal claims a reviewer can challenge and an owner can act on. Every entry carries an inherent, residual, and control-defeated claim, each with a one-line rationale, and every entry names an owner from the routing table. Mitigations are proposed by category (preventive / detective / corrective / transfer / accept) — the owner picks the actual control. The executive translation reports the profile, not an aggregate score, and calls out the highest control-defeated case as a boundary condition. Analyst-tier scoring is defensible without being quantitative.
