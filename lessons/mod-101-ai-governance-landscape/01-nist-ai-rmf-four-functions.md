# NIST AI RMF 1.0 — The Four Functions and the Playbook

## Why this chapter

The [NIST AI Risk Management Framework 1.0 (AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) is the most-cited AI governance framework in North American job postings. In enterprise programs it is the *scaffold* on which the risk register, the intake questionnaire, the impact-assessment template, and the control library are all hung. If the risk-owner asks "what did MAP-1.1 say for this system?", you should know which document to open, which function it lives in, and roughly what evidence answers the question.

The framework is voluntary. It is not a certification standard, it is not law, and it does not prescribe controls. What it does give you is a *shared vocabulary* — the same four verbs, the same subcategory numbers — so that a Google, a JPMorgan, a Kaiser Permanente, and a mid-market vendor can all talk about the same risk without needing to translate.

Your job as an analyst is to be fluent in that vocabulary and to know where in the [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) to look when a specific subcategory needs concrete implementation actions.

## The four functions at a glance

The framework organises AI risk management into four functions. GOVERN sits alongside the other three as a *continuous* function — it never stops running. MAP, MEASURE, and MANAGE cycle through the AI lifecycle, with the outputs of each feeding the next.

| Function | One-line intent | When it fires |
|---|---|---|
| **GOVERN** | Cultivate an organisational culture, policies, and roles that make risk management possible in the first place | Continuous; predates any single system and outlives it |
| **MAP** | Establish the context of the AI system and identify the risks associated with it | At intake, at any material change, and at re-review |
| **MEASURE** | Analyse, assess, benchmark, and monitor AI risks with quantitative and qualitative methods | Before deployment; on a schedule after deployment |
| **MANAGE** | Allocate resources to the mapped and measured risks, and act on them (accept, mitigate, transfer, avoid) | Continuous once the system is live |

A useful mental picture: **GOVERN** is the org chart and the policy binder. **MAP** is intake and risk identification. **MEASURE** is the eval / red-team / bias-audit stack. **MANAGE** is the register, the mitigations, and the escalation path.

## GOVERN — six categories

GOVERN has six categories (GOVERN 1 through GOVERN 6). These are the cross-cutting ones — they touch every system in the inventory rather than any single one.

- **GOVERN 1** — Policies, processes, procedures, and practices for managing AI risks are in place, transparent, and implemented effectively.
- **GOVERN 2** — Accountability structures are in place so appropriate teams and individuals are empowered, responsible, and trained for AI-risk-management decisions.
- **GOVERN 3** — Workforce diversity, equity, inclusion, and accessibility processes are prioritised in the mapping, measuring, and managing of AI risks.
- **GOVERN 4** — Organisational teams are committed to a culture that considers and communicates AI risk.
- **GOVERN 5** — Processes are in place for robust engagement with relevant AI actors.
- **GOVERN 6** — Policies and procedures are in place to address AI risks and benefits arising from third-party software and data, and other supply-chain issues.

Every analyst-owned artefact in the enterprise usually traces back to a GOVERN category: an intake questionnaire → GOVERN 1; a RACI on the AI governance council → GOVERN 2; a supplier due-diligence questionnaire → GOVERN 6.

## MAP — five categories

MAP is where you meet the individual system. This is the function most of your day-to-day intake and inventory work sits under.

- **MAP 1** — Context is established and understood (business purpose, stakeholders, expected benefits, deployment surface).
- **MAP 2** — Categorisation of the AI system is performed (task, model family, autonomy level, data provenance).
- **MAP 3** — AI capabilities, targeted usage, goals, and expected benefits and costs are understood.
- **MAP 4** — Risks and benefits are mapped for all components of the AI system, including third-party software and data.
- **MAP 5** — Impacts to individuals, groups, communities, organisations, and society are characterised.

A first-draft risk assessment for a new use case (see `mod-103-risk-assessment-authoring`) is essentially a narrative pass through MAP 1 → MAP 5.

## MEASURE — four categories

MEASURE covers the evidence side. As an analyst you rarely *author* the evaluations, but you must be able to *read* their outputs into a governance record.

- **MEASURE 1** — Appropriate methods and metrics are identified and applied.
- **MEASURE 2** — AI systems are evaluated for trustworthy characteristics (validity, reliability, safety, security, resilience, accountability, transparency, explainability, privacy, and fairness with harmful-bias managed).
- **MEASURE 3** — Mechanisms for tracking identified AI risks over time are in place.
- **MEASURE 4** — Feedback about the efficacy of measurement is gathered and assessed.

The `mod-107-reading-eval-and-audit-evidence` module lives almost entirely inside MEASURE 2.

## MANAGE — four categories

MANAGE is where a mapped and measured risk becomes an action — accept, mitigate, transfer, or avoid.

- **MANAGE 1** — AI risks based on assessments and other analytical output are prioritised, responded to, and managed.
- **MANAGE 2** — Strategies to maximise AI benefits and minimise negative impacts are planned, prepared, implemented, documented, and informed by input from relevant AI actors.
- **MANAGE 3** — AI risks and benefits from third-party entities are regularly monitored and risk controls are applied and documented.
- **MANAGE 4** — Risk treatments, including response and recovery, and communication plans, for the identified and measured AI risks are documented and monitored regularly.

Incident response (`mod-109-incident-response-and-continuous-monitoring`) traces back to MANAGE 4.

## Trustworthy AI characteristics

The RMF anchors MEASURE (and the framework as a whole) in seven characteristics of *trustworthy AI*. Memorise them — they are the language you will use when writing impact assessments and model cards.

1. Valid and reliable
2. Safe
3. Secure and resilient
4. Accountable and transparent
5. Explainable and interpretable
6. Privacy-enhanced
7. Fair — with harmful bias managed

These are not weighted or ordered; they are properties you check the system against. Different domains put different ones first: a hiring model foregrounds fairness; a medical device foregrounds safety and reliability; an internal RAG assistant foregrounds accuracy (valid and reliable) and privacy.

## The Playbook — your day-to-day companion

The [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) is a companion document that expands each subcategory into:

- **Suggested actions** — concrete implementation steps.
- **Transparency and documentation** — questions the org should be able to answer.
- **References** — related standards, papers, and guidance.

You do not memorise the Playbook. You *use* it. Typical analyst pattern:

1. A new use case arrives in intake.
2. You open the Playbook to MAP 1 (context) and MAP 5 (impacts).
3. You use the Playbook's suggested actions and transparency questions as the *skeleton* of your first-draft assessment.
4. You cite the specific subcategory in the assessment so a reviewer can trace your reasoning back to the framework.

The Playbook is a living document — NIST updates it as guidance matures. Bookmark the [AI Resource Center Knowledge Base](https://airc.nist.gov/AI_RMF_Knowledge_Base) rather than a specific URL you scraped once.

## Concrete example — a customer-support LLM assistant

Suppose an internal team wants to deploy a retrieval-augmented LLM assistant that answers agent-facing questions from a support knowledge base. Walking it through the framework:

- **GOVERN 1** — Does the enterprise's Acceptable Use Policy already cover LLM-generated content served to employees? If not, this intake reveals a policy gap.
- **GOVERN 6** — Which model provider? Which vector database vendor? Have they been through third-party review?
- **MAP 1** — Business purpose is "reduce agent handle time by 15%". Stakeholders are Contact Center Ops, the Data Platform team, and the Customer Trust group.
- **MAP 2** — Task: retrieval-augmented generation. Model family: hosted frontier LLM. Autonomy: assistive (agent still owns the answer sent to the customer).
- **MAP 5** — Downstream impact if the assistant confabulates: incorrect billing or eligibility information passed to a customer. Impact severity is medium if the human agent reviews; escalates to high if the org later automates the send step.
- **MEASURE 2** — Fairness evaluation across customer segments; accuracy evaluation against a labelled knowledge-base sample; red-team pass against prompt injection.
- **MANAGE 1** — Register entry for "hallucination on billing-eligibility questions" with owner (Contact Center Ops), residual claim ("agent-in-the-loop reduces to Low"), and mitigation ("mandatory answer-confidence-below-threshold hides the AI response").

This is the analyst's daily flow: an intake becomes a MAP walk, which produces register entries, which acquire MEASURE evidence, which get triaged in MANAGE.

## What to memorise

- The four function names, in order: **GOVERN, MAP, MEASURE, MANAGE**.
- The count of categories under each: **6, 5, 4, 4**.
- The seven **trustworthy AI characteristics**.
- Where to find the **Playbook** and how to cite a subcategory (e.g., "per NIST AI RMF MAP 5.1").

You do not need to memorise every subcategory number. You need to be able to open the framework, find the right function, scan the categories, and quote the applicable subcategory into a governance record.

## Summary

NIST AI RMF 1.0 gives the enterprise a shared vocabulary — four functions, seven trustworthy-AI characteristics, and a Playbook that translates them into day-to-day actions. Analyst work maps cleanly onto the framework: intake sits under MAP, evidence sits under MEASURE, register-and-route sits under MANAGE, and the org chart, policies, and third-party review sit under GOVERN. Keep the Playbook open in a second tab.
