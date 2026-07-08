# Exercise 04 — GenAI Profile Risks Mapped to Use Cases

**Estimated effort:** 2 hours
**Grounding chapters:** [02 — GenAI Profile twelve risks](../02-genai-profile-twelve-risks.md), [01 — NIST AI RMF](../01-nist-ai-rmf-four-functions.md)

## Objective

For each of the **12 generative-AI risks** enumerated in NIST AI 600-1, produce:

1. A one-sentence description of the risk in your own words.
2. A plausible internal use case where that risk is *primary*.
3. Two additional risks that would *also* apply to that use case (real intakes are always multi-risk).
4. The NIST AI RMF subcategory you would file the risk-register entry under.
5. One MEASURE-tier action a downstream engineer would take.
6. One MANAGE-tier action the analyst would file for the risk owner.

This is the mental muscle that turns an intake into a scored register entry in `mod-103`.

## Prerequisites

- Chapter 02 read.
- [NIST AI 600-1 PDF](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) open.
- [NIST AI RMF 1.0 PDF](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) and [Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) open.

## Problem statement

Author `mod-101-ex-04-genai-risk-map.md` containing:

### Section 1 — The twelve rows

A table with these columns, one row per risk:

| Column | Content |
|---|---|
| # | 1–12 |
| Risk | Canonical name (as published in AI 600-1) |
| One-sentence description | Your paraphrase — do not copy the AI 600-1 text |
| Primary use case | A plausible internal enterprise use case where this risk is the *dominant* one |
| Secondary risks | Two other GenAI risks that would also apply to that use case |
| RMF subcategory | The RMF category (e.g., `MEASURE 2.9`) you would file the register entry under; where you know the specific subcategory, cite it |
| MEASURE action | One concrete downstream engineering action to evaluate the risk (do not design it — cite the shape) |
| MANAGE action | One analyst-tier action to file for the risk owner |

### Section 2 — The always-on defaults

A short section identifying the **three risks you would treat as default candidates on almost any generative-AI intake**. Chapter 02 names them (Value Chain and Component Integration, Data Privacy, Information Security). Justify with 2–3 sentences why each is a default.

### Section 3 — A one-intake case study

Pick **one** of the twelve use cases you wrote in Section 1 and expand it into a mini-register entry:

- Business purpose (2 sentences).
- Deployment surface (1 sentence).
- Three risk-register rows, one per risk you identified (primary + two secondaries). Each row has: risk name, RMF subcategory, inherent-risk claim (low / medium / high with a one-line rationale), proposed control, residual-risk claim, and owner (product / ML / security / privacy / legal).

### Section 4 — Reflection

3–5 sentences. Which of the 12 risks was hardest to attach to a concrete internal use case, and why? Which is easiest to accidentally over-apply? (Common answer: Confabulation gets over-applied; Human-AI Configuration gets under-applied; Environmental Impacts is often forgotten because it feels far from the analyst desk.)

## Requirements

- No fabricated risk names. If your recall of the AI 600-1 canonical spelling differs from the PDF, defer to the PDF and note the discrepancy.
- Every RMF subcategory cited must exist in the framework. If unsure, cite the top-level category (e.g., `MEASURE 2`) instead of guessing a subcategory number.
- The mini-register entry in Section 3 must be *reviewable* — a senior architect should be able to read it and identify at least one thing to push back on.
- No hallucinated incidents or real-world case studies. Fictional but plausible enterprise use cases only.

## Starter guidance

- Do not try to be creative with the use cases in Section 1. Boring is fine — an internal résumé-screening pilot, an internal marketing-copy generator, a customer-support agent-facing assistant, a code-generation assistant on internal repos, an internal knowledge-base search assistant, a clinical-note summary tool. Boring maps cleanly.
- For MEASURE actions, use shapes the analyst can *read* even if not *design*: bias evaluation with Fairlearn / AI Fairness 360; red-team pass against the OWASP LLM Top 10; accuracy evaluation against a labelled sample; content-moderation eval; environmental / cost telemetry review.
- For MANAGE actions, use shapes the analyst *does* every week: file a register entry with owner + residual claim; open a follow-up ticket to the risk owner; request the impact-assessment update; escalate to legal for a boundary case.
- The mini-register entry in Section 3 is the artefact you will build a whole module around in `mod-103`. Treat this as your first-pass rehearsal.

## Acceptance criteria

- All 12 GenAI risks covered in Section 1.
- Section 2 justifies three default risks.
- Section 3 has a coherent mini-register entry with three risk-register rows.
- Section 4 reflection is present, honest, and specific.
- Every RMF subcategory cited is real (or is a top-level category if unsure).
- No fabricated incidents, benchmarks, or vendor claims.

## Stretch goals

- Add a **"trustworthy-AI characteristic"** column to Section 1 — for each risk, name the RMF characteristic it primarily bears on (safe / secure and resilient / valid and reliable / privacy-enhanced / fair with harmful bias managed / accountable and transparent / explainable and interpretable).
- Add a **regulator overlay** column — for each risk, note any obviously-attaching regulation (e.g., Harmful Bias → EEOC Title VII for hiring AI; Data Privacy → GDPR; CBRN → export controls). Deep coverage of this lives in `mod-106`; here it is a warm-up.
- Draft a **"defaults-to-scan-for" template** you would drop into your intake questionnaire — a checkbox list of the three default risks (Value Chain, Data Privacy, Information Security) and a prompt asking the submitter to acknowledge them.

## Deliverables

- `mod-101-ex-04-genai-risk-map.md`.

## Notes on evaluation

The reference solution in the paired repo will show one full mapping. The rubric is (a) canonical risk names honestly reflected, (b) plausible use cases, (c) honest handling of RMF subcategory citations (better to cite the top-level category than to fabricate a subcategory number), and (d) a Section 3 mini-register entry that would survive a senior architect's first review with only push-back on details.
