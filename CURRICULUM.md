# AI Governance Analyst Curriculum

**Role level:** 15 (entry / early-career — AI Governance family)
**Family:** AI Governance
**Status:** planned — modules and projects below are the planned scope authored from [`.aicg/curriculum-plan.json`](.aicg/curriculum-plan.json). Lessons and projects will be drafted by subsequent autonomous content cycles.

## Overview

This track teaches the day-to-day operational analyst work that keeps an enterprise AI governance program running: AI use-case intake and triage → model / AI-system inventory maintenance → framework crosswalks across NIST AI RMF, ISO/IEC 42001, and the EU AI Act → first-draft AI risk assessments → reading fairness / bias reports → algorithmic / fundamental-rights / data-protection impact assessment authoring → model / system / dataset card authoring → cross-jurisdiction regulatory tracking → reading eval / red-team / audit evidence into governance records → control-tracking and evidence-collection cycles → third-party AI vendor review → AI incident response at the analyst tier → continuous monitoring interpretation → stakeholder communication and council support → drafting internal AI policies under senior guidance.

It is an **entry / early-career track at level 15**, positioned in the **AI Governance family**. The differentiator against higher-level Governance tracks is *operational analyst altitude*: this curriculum owns the day-to-day intake, inventory, documentation, and control-tracking work that supports — but does not architect — the governance program. Framework architecture, control-library design, cross-jurisdiction reconciliation, program leadership, board reporting, and regulator interface are owned by [`senior-ai-governance-architect`](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning), [`head-of-ai-governance`](https://github.com/ai-governance-curriculum/head-of-ai-governance-learning), and [`chief-ai-officer`](https://github.com/ai-governance-curriculum/chief-ai-officer-learning) and are *consumed here, not re-implemented*.

Total planned commitment: **114 hours across 10 modules** + **85 hours across 3 projects** = **~199 hours**.

## Ownership rule

Following the project-wide ownership rule, this curriculum:

- **Owns** the operational analyst work end-to-end — AI system intake and use-case triage; model / AI-system inventory maintenance; NIST AI RMF / ISO/IEC 42001 / EU AI Act framework crosswalks; first-draft AI risk assessments; fairness / bias report reading and remediation coordination; algorithmic / fundamental-rights / data-protection / sector-specific impact assessment authoring; model / system / dataset card authoring; cross-jurisdiction regulatory tracking; reading eval / red-team / audit evidence into governance records; control-tracking and evidence-collection cycles; third-party AI vendor / model / dataset review; AI incident response at the analyst tier; continuous-monitoring interpretation and post-market surveillance filing; council-support communication; and drafting internal AI policies and standards under senior guidance.
- **Defers up** to [`senior-ai-governance-architect-learning`](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) for framework architecture (control-library design, policy taxonomy, cross-jurisdiction reconciliation); to [`head-of-ai-governance-learning`](https://github.com/ai-governance-curriculum/head-of-ai-governance-learning) for program leadership (board reporting, budget, external / regulator engagement); to [`chief-ai-officer-learning`](https://github.com/ai-governance-curriculum/chief-ai-officer-learning) for executive scope.
- **Defers sideways** to [`ai-evaluation-engineer-learning`](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-learning) (peer, Governance family) for release-assurance / audit-trail methodology; to [`ai-risk-engineer-learning`](https://github.com/ml-engineering-curriculum/ai-risk-engineer-learning) for harm-model design and red-team data generation; to [`ai-eval-engineer-learning`](https://github.com/ai-engineering-curriculum/ai-eval-engineer-learning) for AI-application eval methodology depth; to [`model-evaluation-engineer-learning`](https://github.com/ml-engineering-curriculum/model-evaluation-engineer-learning) for benchmark and statistical methodology depth; to [`ai-infra-security-learning`](https://github.com/ai-infra-curriculum/ai-infra-security-learning) for deep ML/AI security depth.
- **Links out** for general privacy / GDPR / CCPA / HIPAA depth beyond AI-specific overlays (privacy engineering track) and for legal opinion (legal counsel — analysts do paralegal-level reading of statutes and standards, not statutory interpretation).

See [`JOB_REQUIREMENTS.md`](JOB_REQUIREMENTS.md) for the requirements-to-coverage map and the cited public references the catalog is grounded in.

## Module Plan

| Module | Title | Hours | Status |
|---|---|---|---|
| mod-101-ai-governance-landscape | AI Governance Landscape: Frameworks, Standards, and Values Baselines | 12 | planned |
| mod-102-ai-system-inventory-and-intake | AI System Intake and Inventory Maintenance | 12 | planned |
| mod-103-risk-assessment-authoring | First-Draft AI Risk Assessment Authoring | 12 | planned |
| mod-104-fairness-bias-and-model-behaviour-review | Reading Fairness, Bias, and Model-Behaviour Reports | 10 | planned |
| mod-105-impact-assessments-and-model-cards | Impact Assessments, Model Cards, System Cards, and Datasheets | 14 | planned |
| mod-106-regulatory-tracking-and-jurisdictions | Cross-Jurisdiction Regulatory Tracking | 12 | planned |
| mod-107-reading-eval-and-audit-evidence | Reading Eval, Red-Team, and Audit Evidence into Governance Records | 10 | planned |
| mod-108-controls-and-compliance-evidence | Controls, Compliance Evidence, and Third-Party AI Vendor Review | 12 | planned |
| mod-109-incident-response-and-continuous-monitoring | AI Incident Response and Continuous Monitoring at the Analyst Tier | 10 | planned |
| mod-110-communication-and-council-support | Stakeholder Communication, Council Support, and Policy Drafting | 10 | planned |

## Project Plan

| Project | Title | Hours | Status |
|---|---|---|---|
| project-101-end-to-end-intake-inventory-and-impact-assessment | End-to-End Intake → Inventory → Impact Assessment for a New AI Use Case | 25 | planned |
| project-102-regulatory-tracker-and-control-crosswalk-slice | Rolling Regulatory Tracker + Control Crosswalk for One Enterprise Slice | 25 | planned |
| project-103-review-packet-and-council-support-package | Eval Review Packet + Council Support Package for a Live AI System | 35 | planned |

## Module summaries

### mod-101 — AI Governance Landscape
Paraphrase NIST AI RMF's four functions (GOVERN, MAP, MEASURE, MANAGE) using the Playbook as a day-to-day reference; recite the 12 generative-AI risks from the NIST AI RMF Generative AI Profile (AI 600-1); walk the ISO/IEC 42001 clause structure and its correspondence to ISO/IEC 27001; read the EU AI Act risk-tier scheme and Annex III high-risk domain list; position OECD, CoE, and UNESCO instruments as the international values baseline; commit the analyst-role deferral rules to memory so the next-up architect / head-of-governance responsibilities stay off this desk.

### mod-102 — AI System Intake and Inventory Maintenance
Design an intake questionnaire employers actually populate (owner, purpose, autonomy, data sources, model family, deployment surface, third-party dependencies, EU AI Act tier, applicable sector regulator); triage into in-scope / out-of-scope / needs-follow-up buckets; build and maintain an AI-system inventory row synced with the ML team's model registry; use Credo AI / Holistic AI / ModelOp / ServiceNow AI Control Tower at an analyst level, with a spreadsheet fallback; use pandas / Excel to reconcile a registry export against the governance inventory.

### mod-103 — First-Draft AI Risk Assessment Authoring
Walk a new use case through NIST AI RMF MAP; overlay ISO/IEC 23894 risk sources and the GenAI-Profile risks to produce a scored register entry; apply SR 11-7 shape for regulated financial institutions; route risks to product / ML / security / legal / privacy owners with proposed mitigations — deferring harm-model methodology up to `ai-risk-engineer` and quantitative methodology up to `senior-ai-governance-architect`; distinguish inherent / residual / control-defeated risk for an executive audience.

### mod-104 — Reading Fairness, Bias, and Model-Behaviour Reports
Read Fairlearn / AIF360 outputs and vendor bias-audit reports (demographic parity, equalised odds, calibration by group, four-fifths rule, disparate-impact ratio) well enough to summarise them for a non-technical stakeholder; use the Google What-If Tool without writing code; apply the NYC LL 144 bias-audit shape and the EEOC Title VII adverse-impact framing for hiring AI; open remediation tickets with a concrete finding and threshold breach; recognise under-evidenced fairness claims and escalate.

### mod-105 — Impact Assessments, Model Cards, System Cards, and Datasheets
Author drafts of the four canonical AI impact assessments — algorithmic (Canadian AIA shape), fundamental-rights (EU AI Act Article 27), data-protection (GDPR Article 35), and sector-specific — from a shared template that reuses NIST MAP output; use ISO/IEC 42005 as the AI-specific IA standard scaffold; author a model card (Mitchell et al.), a system card (OpenAI / Anthropic style at internal scale), and a datasheet for a dataset (Gebru et al.); publish through Hugging Face / Google Model Card Toolkit or an internal template; cross-reference model card, impact assessment, and inventory row so a reader can walk between them.

### mod-106 — Cross-Jurisdiction Regulatory Tracking
Maintain a rolling AI regulatory tracker across EU, US federal, US state, UK, Canada, and sector regulators; read GDPR Article 22, Article 35, CCPA / CPRA, HIPAA at a paralegal level; use the IAPP AIGP body of knowledge as the shared vocabulary and know where CIPP/US / CIPP/E and ISO/IEC 42001 lead-implementer / lead-auditor fit as add-on credentials; read the EU AI Office GPAI Code of Practice; file regulatory-change notes and route them to affected system owners.

### mod-107 — Reading Eval, Red-Team, and Audit Evidence
Read an AISI-style Inspect eval report, an internal RAG-triad eval report, or a red-team engagement report enough to summarise residual-risk claims, threshold-decision rationale, and unresolved findings into a governance-record row; read public system cards and responsible-scaling policy disclosures as benchmarks; compose an analyst-tier review packet and hand it to `ai-evaluation-engineer` for release-assurance sign-off; hold the delegation boundary — this role reads the evidence, peer engineering tracks produce it.

### mod-108 — Controls, Compliance Evidence, and Third-Party AI Vendor Review
Run periodic control-testing cycles; pull evidence artifacts and attach them to control records in the GRC platform; produce a control-status report an internal auditor can review; recognise the top AI/LLM security threat categories from OWASP LLM Top 10, MITRE ATLAS, NIST AI 100-2, Google SAIF at a level sufficient to file a record and route to `ai-infra-security`; run third-party AI vendor intake with an AI-specific due-diligence questionnaire; build the analyst-tier control crosswalk across ISO 42001, NIST AI RMF, EU AI Act, SR 11-7, and internal policy — deferring master-library design upward.

### mod-109 — AI Incident Response and Continuous Monitoring
Log an AI incident against the risk register; cross-reference the affected inventory row; coordinate impact-assessment updates; package post-incident evidence for the council or auditor; distinguish AI-specific incidents (model regression, jailbreak, prompt injection, biased outcome escalation, hallucination harm, unauthorised model use) from general software incidents; read continuous-monitoring dashboards for governance sign-off and file post-market-surveillance summaries under the EU AI Act.

### mod-110 — Stakeholder Communication, Council Support, and Policy Drafting
Translate technical eval / risk / audit outputs into business-facing language; use ISO/IEC 38507 governance-body vocabulary for board audiences; prepare pre-read decks, one-pagers, decision logs, and audit-surviving meeting minutes for the AI governance council; draft first-cut internal AI policies (acceptable-use policy, model-approval standard, third-party AI vendor review standard, generative-AI employee guidance) — routing for senior architect edits and head-of-governance ratification; plan a certifications portfolio (IAPP AIGP, CIPP/US or CIPP/E, ISO/IEC 42001 LI/LA).

## Assessment

Each module ships **1 quiz** plus the exercises and lab listed in [`.aicg/curriculum-plan.json`](.aicg/curriculum-plan.json). Each project ships a portfolio-grade README, a governance-record folder with cross-linked artifacts (inventory row, impact assessment, model card, control matrix, review packet, meeting minutes as applicable), and an explicit rubric covering framework-mapping accuracy, artifact completeness, delegation-boundary discipline, and communication quality.

## Where to go after this curriculum

- **`senior-ai-governance-architect-learning`** — the direct next step on the Governance ladder for framework architecture and cross-jurisdiction reconciliation.
- **`ai-evaluation-engineer-learning`** — peer specialist in the Governance family for release-assurance / audit-trail methodology.
- **`head-of-ai-governance-learning`** — governance-program leadership scope.
- **`ai-risk-engineer-learning`** — peer specialist for harm-model design and red-team data generation on the ML Engineering ladder.
- **`ai-eval-engineer-learning`** / **`model-evaluation-engineer-learning`** — peer specialists for AI-application and model evaluation methodology depth.
- **`ai-infra-security-learning`** — for deep ML/AI security.
- **`chief-ai-officer-learning`** — executive scope.

<!-- needs-research: backfill industry-frequency evidence into JOB_REQUIREMENTS.md once the autonomous research loop runs with WebSearch / WebFetch exercised against live job boards; demote any module or exercise whose underlying requirement does not show up in ≥3 in-window postings. -->
