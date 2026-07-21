# Overlaying ISO/IEC 23894 Risk Sources on the MAP Walk

## Why this chapter

The MAP walk gives you a narrative. It does not, on its own, tell you whether you have enumerated *all* the plausible risk sources. That is where a taxonomy earns its keep.

[ISO/IEC 23894:2023 — Information technology — Artificial intelligence — Guidance on risk management](https://www.iso.org/standard/77304.html) is the AI-specific companion to [ISO 31000:2018](https://www.iso.org/standard/65694.html), the general risk-management standard. Together they give the analyst a checklist of risk *sources* — where risk enters an AI system — that overlays cleanly onto the MAP output.

You do not memorise 23894. You use it as a scan-list against your MAP 5 to catch what you missed. Combined with the GenAI Profile's 12 risks (mod-101 chapter 02), it gives you a two-lens sweep before you commit the register entries.

## Where ISO 23894 sits

ISO/IEC 42001 Clause 6 requires an AI risk assessment. It references ISO/IEC 23894 as the recommended AI-specific guidance. In practice most enterprise programs that certify against 42001 adopt 23894 as their risk-management method-of-record, and the risk-source categories it lists become the second lens applied to every risk assessment.

The standard is not free — it is behind the ISO paywall — so this chapter cites the categories at the level the ISO/IEC AI JTC 1/SC 42 published in the standard's public abstract and the associated freely-published summaries. For citation in an audit-facing document, retrieve the current published text.

<!-- needs-research: verify the exact category and subcategory titles of ISO/IEC 23894:2023 against the current published text before citing verbatim in an external-facing document; the standard is behind a paywall and the phrasing has been the subject of minor errata. -->

## The risk-source categories

23894 organises AI-specific risk sources into a small number of categories the analyst uses as a scanning list. The paraphrased categories:

- **Complexity of AI systems.** Risk arises from architectural complexity, opaque model behaviour, and emergent behaviours in composed systems.
- **Life-cycle stage.** Risk emerges differently at design, data acquisition, training, deployment, monitoring, and retirement.
- **Level of automation.** Risk correlates with autonomy — a fully autonomous system carries different residual than an assistive one.
- **Machine-learning risks.** Data-set representativeness, overfitting, distribution shift, adversarial robustness.
- **System hardware and software.** Compute infrastructure, dependencies, hardware failure modes.
- **Deployment context.** Environment mismatch between training and deployment; user population differences.
- **Human factors.** Over-reliance, automation bias, unclear handoff, deskilling.
- **Environmental factors.** Physical environment differences, external stressors.

The point of a scan is not to fill every category on every use case. It is to *ask* every category and record which ones apply and which do not. Categories marked *not applicable* are marked with a one-line reason — that is your audit answer to "did you consider it?"

## The two-lens sweep

The GenAI Profile lens (mod-101 chapter 02) is *what can go wrong from a generative-AI perspective* — 12 named risks like Confabulation, Data Privacy, Value Chain and Component Integration. The ISO 23894 lens is *where does risk enter the AI system* — categories like Complexity, Life-cycle stage, Human factors.

They cover different angles. A given register entry might tie to:

- GenAI Profile: **Confabulation** (risk #2)
- 23894: **Complexity of AI systems** (a large hosted model's behaviour is opaque) + **Machine-learning risks** (distribution shift on the topic) + **Human factors** (copywriter over-reliance)

Neither lens alone would surface all of those. Both together give the reviewer a defensible case that the risk enumeration is complete.

## Applying the 23894 lens to MAP 5

Take each MAP 5.1 impact from the previous chapter and ask, for each 23894 category: *does this category surface a risk source you did not catch in the GenAI Profile pass?*

Worked from the MCDA example:

- Impact: **Confabulation of product facts.**
  - Complexity of AI systems: **applies.** The hosted LLM's behaviour on niche product-specific facts is opaque; grounding through retrieval only partly closes the gap.
  - Machine-learning risks: **applies.** Training-time distribution differs from enterprise-specific product taxonomy — that is the mechanism behind the risk.
  - Human factors: **applies.** Copywriter over-reliance materially increases the residual — the analyst notes the human-oversight design as a control.

- Impact: **Brand-voice homogenisation.**
  - Life-cycle stage: **applies.** Risk grows over time as the model and templates settle; caught at monitoring stage, not at deployment.
  - Complexity of AI systems: **applies at a slight tangent.** Convergence across product teams is an emergent behaviour when many teams pull on the same underlying model.

- Impact: **IP contamination.**
  - Machine-learning risks: **applies.** Training-data provenance for the hosted model is opaque.
  - System hardware and software: *does not apply*.

- Impact: **Data leakage in prompts.**
  - Deployment context: **applies.** The training-time assumption ("model trained on internal data") does not match deployment reality ("prompts sent to a vendor SaaS"); the risk is a context-mismatch risk.
  - Human factors: **applies.** Users may paste more into a prompt than they realise.

Every category the analyst marks *does not apply* gets a one-line reason. Every category the analyst marks *applies* gets fed into the risk-register entry as a risk source citation.

## The register-entry shape after the 23894 overlay

The register entry drafts fill out to include both lenses. A minimum-viable field list, one row per identified risk:

- **Risk ID.**
- **System.**
- **Risk title** (one line).
- **GenAI Profile risk(s)** — the taxonomy hook.
- **ISO 23894 risk source(s)** — the source lens.
- **NIST RMF subcategory anchor** — the MAP subcategory that identified it.
- **Owner** (product / ML / security / legal / privacy).
- **Inherent likelihood / magnitude** — ordinal, with a one-line rationale each.
- **Proposed mitigation(s)** — what the analyst suggests; not the last word.
- **Residual likelihood / magnitude** — after mitigation.
- **Status** — proposed / accepted / in-mitigation / closed.
- **Evidence link(s)** — to eval reports, incident evidence, control-testing results.

That row structure is what chapter 03 fills in scoring-wise, and what chapter 05 routes to owners.

## Where 23894 stops for the analyst

- **You do not author the enterprise's risk-management method.** That is architect scope. Whether the enterprise adopts 23894 verbatim or overlays a local taxonomy is a decision above the analyst's pay grade.
- **You do not build risk-source-to-control mappings from scratch.** The control library is the architect's artefact; the analyst *picks* the applicable controls when filling out the register row.
- **You do not do the deep alignment / harm-model surface analysis** that some 23894 categories point at. `ai-risk-engineer` owns that depth.

Analyst-tier work: use 23894 as a scan-list against MAP 5, produce a defensible enumeration, and fill in the register entries with both taxonomy hooks.

## Concrete example — the MCDA register skeleton after both lenses

Before the scoring pass in the next chapter, the MCDA register looks like:

- **RR-2026-0212 — Confabulation of product facts.** GenAI Profile #2 (Confabulation). ISO 23894: Complexity of AI systems, Machine-learning risks, Human factors. NIST MAP 5.1. Owner: Marketing Ops.
- **RR-2026-0213 — Brand-voice homogenisation.** GenAI Profile #6 (Harmful Bias or Homogenization). ISO 23894: Life-cycle stage, Complexity. NIST MAP 5.1. Owner: Marketing Ops.
- **RR-2026-0214 — IP contamination.** GenAI Profile #10 (Intellectual Property). ISO 23894: Machine-learning risks. NIST MAP 4.1. Owner: Legal.
- **RR-2026-0215 — Data leakage in prompts.** GenAI Profile #4 (Data Privacy). ISO 23894: Deployment context, Human factors. NIST MAP 5.1. Owner: Privacy + Security.

Four register entries, each with two taxonomy anchors and one framework anchor. That is the analyst-tier baseline before scoring, mitigation, and residual pass.

## What to memorise

- The **two-lens sweep**: GenAI Profile + ISO 23894.
- The **eight paraphrased 23894 risk-source categories** — Complexity, Life-cycle stage, Automation level, ML risks, System hardware/software, Deployment context, Human factors, Environmental factors.
- The **register-row minimum field list** carrying both taxonomy hooks.
- The rule: **every category is asked; the not-applicable answer is recorded with a one-line reason.**

## Summary

ISO/IEC 23894 is the AI-specific overlay on ISO 31000, referenced by ISO/IEC 42001 Clause 6, that gives the analyst a risk-source scanning list. Combined with the NIST GenAI Profile 12 risks, it produces a two-lens sweep of MAP 5 impacts — the taxonomy lens says *what can go wrong*, the source lens says *where risk enters the system*. The register-entry shape carries both anchors, plus the NIST subcategory citation, plus the owner. That is the analyst-tier baseline before the scoring, routing, and residual pass covered in later chapters.
