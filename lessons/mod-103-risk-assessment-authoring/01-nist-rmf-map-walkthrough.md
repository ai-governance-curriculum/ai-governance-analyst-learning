# Walking a Use Case Through NIST AI RMF MAP

## Why this chapter

The first-draft AI risk assessment is the analyst's most consequential technical deliverable. It is the document the risk owner reads, the reviewer signs off on, and — years later — the auditor pulls when reconstructing "what did the enterprise know when it deployed this system?" A well-authored MAP walk answers that question directly.

NIST AI RMF MAP is not a form. It is a *function* with five categories and roughly twenty subcategories, each phrased as a governance question. The analyst's job is to translate each subcategory question into a specific answer for a specific use case, cite the subcategory, and produce a narrative a downstream reader can act on.

## MAP as a narrative, not a checklist

The single most common failure mode of first-draft risk assessments is the checklist voice — "MAP 1.1: yes; MAP 1.2: yes; MAP 1.3: yes". This is worse than useless. It gives no evidence, no reasoning, and no artefact a reviewer can challenge.

Good MAP output reads like a short case study: *this is the system, this is who it affects, this is what it does, this is where it can fail, and this is what we think the residual harm looks like*. The MAP subcategory numbers cite the reasoning; the reasoning is what the reviewer reads.

## MAP 1 — Context is established and understood

MAP 1 is the *setup*. It answers: what is this system, what is it for, who runs it, who is affected, and what does the enterprise gain by running it.

Subcategories at analyst-tier depth:

- **MAP 1.1** — The intended purpose and specific application (task, deployment scope, and setting) is understood.
- **MAP 1.2** — Interdisciplinary AI actors and stakeholders are identified.
- **MAP 1.3** — The organisation's mission and relevant goals for the AI system are understood.
- **MAP 1.4** — Business value or context of business use is clearly defined.
- **MAP 1.5** — Organisational risk tolerances are determined and documented.
- **MAP 1.6** — System requirements are elicited from and understood by relevant AI actors.

What analyst-tier MAP 1 output looks like: two or three paragraphs of narrative that name the system, the purpose statement (recycled from intake), the stakeholders (owner, users, affected populations), and the mission tie-out. Cite MAP 1.5 by pointing at the enterprise's risk tolerance statement — you do not author risk tolerance at analyst tier.

## MAP 2 — Categorisation of the AI system is performed

MAP 2 is the *technical framing*. It answers: what type of AI is this, on what data, from what provider.

- **MAP 2.1** — The specific tasks and methods used to implement the tasks the AI system will support are defined.
- **MAP 2.2** — Information about the AI system's knowledge limits and how system output may be utilised is documented.
- **MAP 2.3** — Scientific integrity and TEVV (test, evaluation, verification, and validation) considerations are identified and documented.

Analyst-tier MAP 2 output ties directly to the intake's technical fields: model family, model provider, data sources, tools / APIs. The scientific-integrity subcategory (MAP 2.3) is where you name the evaluation team owning TEVV — you do not *design* the eval methodology; that is `mod-107` and, ultimately, `ai-evaluation-engineer` scope. You *record* what team owns it.

## MAP 3 — AI capabilities, targeted usage, goals, and expected benefits and costs are understood

MAP 3 is the *value question*. It answers: what is the enterprise expecting to get out of running this, and at what cost.

- **MAP 3.1** — Potential benefits of intended AI system functionality and performance are examined and documented.
- **MAP 3.2** — Potential costs, including non-monetary costs, of intended AI system functionality and performance are examined and documented.
- **MAP 3.3** — Targeted application scope is specified and documented.
- **MAP 3.4** — Processes for operator and practitioner proficiency with AI system performance and trustworthiness are defined and communicated.
- **MAP 3.5** — Processes for human oversight are defined, assessed, and documented in accordance with organisational policies.

MAP 3 is where the analyst distinguishes what the system is *supposed* to do from what it *could* do — the difference between intended purpose (MAP 3.3) and reasonably foreseeable misuse. The oversight subcategory (MAP 3.5) ties back to [EU AI Act Article 14](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) for high-risk systems.

## MAP 4 — Risks and benefits are mapped for all components

MAP 4 is the *supply-chain question*. It answers: what components does the system depend on, and what risks do they bring.

- **MAP 4.1** — Approaches for mapping AI technology and legal risks of its components — including the use of third-party data or software — are in place, followed, and documented, as are risks of infringement of a third-party's intellectual property or other rights.
- **MAP 4.2** — Internal risk controls for components of the AI system, including third-party AI technologies, are identified and documented.

MAP 4 output enumerates the third-party dependencies (from intake and inventory), calls out where each has been through vendor review, and flags gaps. This is where the GenAI Profile risk #12 (Value Chain and Component Integration) formally lands.

## MAP 5 — Impacts to individuals, groups, communities, organisations, and society are characterised

MAP 5 is the *harm question*. This is the heaviest section — often the longest — and the section a reviewer will scrutinise hardest.

- **MAP 5.1** — Likelihood and magnitude of each identified impact (both potentially beneficial and harmful) based on expected use, past uses of AI systems in similar contexts, public incident reports, feedback from those external to the team that developed or deployed the AI system, or other data are identified and documented.
- **MAP 5.2** — Practices and personnel for supporting regular engagement with relevant AI actors and integrating feedback about positive, negative, and unanticipated impacts are in place and documented.

MAP 5 draws on:

- **The NIST GenAI Profile 12 risks** for the taxonomy of what can go wrong (chapter 02 of `mod-101`).
- **ISO/IEC 23894 risk sources** for the risk-source lens (see chapter 02 of this module).
- **Public incident reports** — the [AI Incident Database](https://incidentdatabase.ai/) and the [OECD AI Incidents Monitor](https://oecd.ai/en/incidents) — for prior-art evidence.
- **Affected-population representation** where accessible.

The analyst frames each identified impact as *type of harm × affected population × plausible mechanism × likelihood-and-magnitude claim*. That framing is what the risk-register entries will draw from.

## Sequence — MAP 1 → MAP 5

The MAP walk is sequential, but not strictly linear — you often go back to MAP 1 to re-fix scope after MAP 5 surfaces an impact you had not framed. The pattern most analysts settle into:

1. MAP 1 pass (context and stakeholders).
2. MAP 2 pass (technical framing).
3. MAP 3 pass (value and oversight design).
4. MAP 4 pass (third-party components).
5. MAP 5 pass (impacts) — heaviest, longest.
6. Re-pass MAP 1 and MAP 3 to check anything MAP 5 surfaced does not invalidate the earlier framing.

Two hours for a Medium-tier system, four to six hours for a High-tier system is the typical shape — you are not writing an academic paper, you are writing an operational artefact.

## Concrete example — the MCDA MAP walk

Returning to the Marketing Copy Draft Assistant (MCDA) — internal, hosted foundation model, assistive marketing-copy drafting.

- **MAP 1.1** — Purpose: reduce time to first-draft marketing copy from 3 days to 4 hours. Deployment scope: internal copywriters; internal review workflow before customer-facing release.
- **MAP 1.2** — Actors: Marketing Ops (owner), Marketing Data Platform team (technical), Legal (review), Governance (this analyst), Vendor V (model provider).
- **MAP 1.4** — Business value: measurable throughput uplift; anecdotal quality uplift. Not a compliance-driven system.
- **MAP 2.1** — Task: conditional text generation from structured brief + prior-campaign retrieval. Method: prompt-engineered use of hosted LLM v2024-06 with prompt template maintained by Marketing Data Platform team.
- **MAP 2.2** — Knowledge limits: model has training cut-off ~2023; not authoritative for the enterprise's own past campaigns without retrieval grounding. Outputs are drafts — never sent externally as-is.
- **MAP 2.3** — TEVV: Marketing Data Platform team runs an accuracy eval per template rev; AI Evaluation Engineer will sign off on release rev v1.4.
- **MAP 3.1** — Benefit: throughput, plus a lower barrier for smaller product teams that could not previously get marketing capacity.
- **MAP 3.2** — Costs: vendor licence; occasional legal-review overhead for edge outputs; small brand-voice-homogenisation risk (see MAP 5).
- **MAP 3.3** — Scope: internal only; sending an unreviewed draft externally is out of scope.
- **MAP 3.4** — Copywriter proficiency: prompt-guidance doc + monthly Q&A with the platform team.
- **MAP 3.5** — Human oversight: every draft is edited by a copywriter and passes review workflow before external release.
- **MAP 4.1** — Third-party: Vendor V (LLM), Vendor P (prompt-management SaaS). Both under vendor review VR-2026-0044 and VR-2026-0031.
- **MAP 4.2** — Internal controls: prompt-injection filtering; PII-scanning on prompts; rate-limiting; audit log.
- **MAP 5.1** — Identified impacts:
  - *Confabulation of product facts* → copywriter propagates false claim → customer-facing brand or compliance incident. Likelihood: medium (in absence of review; low with review). Magnitude: high per instance if it lands (regulatory ad exposure).
  - *Brand-voice homogenisation* → outputs converge across product teams → weakened brand differentiation. Likelihood: medium. Magnitude: medium over time.
  - *IP contamination* → training data reproduces copyrighted phrasing. Likelihood: low. Magnitude: medium.
  - *Data leakage in prompts* → sensitive briefs sent to vendor SaaS unprotected. Likelihood: low (controls in place); Magnitude: high if realised.
- **MAP 5.2** — Feedback: monthly copywriter user-forum + incident-report channel; Legal escalation on any suspected copyright collision.

That narrative *is* the first-draft risk assessment for MAP. It becomes register entries in the next chapter's overlay pass, and it becomes source material for the impact assessment (`mod-105`) and the model card.

## What analyst-tier MAP is *not*

- **Not a harm-model design.** The frame — type × population × mechanism × likelihood-and-magnitude — is enough for a first-draft register entry. Deep harm-modelling is [ai-risk-engineer](https://github.com/ml-engineering-curriculum/ai-risk-engineer-learning) scope.
- **Not quantitative risk methodology.** Likelihood and magnitude are stated as ordinal claims with reasoning. Monetised, probability-weighted, or portfolio-aggregated risk claims are `senior-ai-governance-architect` scope.
- **Not release sign-off.** The MAP walk *informs* release sign-off; it does not *provide* it. `ai-evaluation-engineer` owns the sign-off.

## What to memorise

- The **five MAP categories** and one-line intent of each.
- The **standard MAP walk sequence**: MAP 1 → MAP 2 → MAP 3 → MAP 4 → MAP 5 → re-check MAP 1 and MAP 3.
- The **impact-framing shape**: type × population × mechanism × likelihood-and-magnitude.
- The **three altitude limits**: no harm-model design; no quantitative methodology; no release sign-off.

## Summary

MAP is where the analyst turns an intake row into a first-draft narrative risk assessment — context, technical framing, value and oversight, third-party components, and impacts. It is written as a case study, not a checklist. The heaviest work is MAP 5, framed as type × population × mechanism × likelihood-and-magnitude, drawing on the GenAI Profile risks, ISO/IEC 23894 risk sources, and public incident evidence. Analyst-tier MAP produces the narrative and the register-source; it does not design harm models, produce quantitative scores, or authorise release.
