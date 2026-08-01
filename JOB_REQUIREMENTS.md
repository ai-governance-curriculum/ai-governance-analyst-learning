# Job Requirements — AI Governance Analyst

**Role level:** 15 (entry / early-career — Governance family)
**Track:** `ai-governance-analyst-learning`
**Research window:** 2026-05-01 → 2026-08-01 (last 90 days)
**Today:** 2026-08-01
**Cycle:** 2026-08 (backfill pass; 25 live in-window postings)

This file documents the requirements catalog used to seed and maintain the AI Governance Analyst curriculum. Raw normalized data lives in [`.aicg/job-requirements.json`](.aicg/job-requirements.json); the planned curriculum lives in [`.aicg/curriculum-plan.json`](.aicg/curriculum-plan.json); this cycle's *proposed additions* live in [`.aicg/curriculum-plan-delta.json`](.aicg/curriculum-plan-delta.json) (intentionally empty — see the rationale in that file).

## Cycle 2026-08 summary

Backfilled 25 in-window postings across `AI Governance Analyst`, `AI Policy Analyst`, `Responsible AI Analyst`, `AI Compliance Analyst`, `AI Risk & Compliance Analyst`, `AI Governance & Compliance Analyst`, and adjacent variants. Every requirement theme with `≥ 30%` observed frequency in the sample is already covered by `mod-101..mod-110`. Three emerging themes (agentic AI governance, shadow-AI remediation, governance-dashboarding) came in below threshold; they are documented for the next cycle to re-evaluate under [`.aicg/job-requirements.json` → `market_signal_notes.themes_below_addition_threshold_but_worth_watching`](.aicg/job-requirements.json). Per the continuity-bias rule, this cycle proposes **zero new modules, zero new exercises, and zero new projects**.

## Methodology

1. Fanned out title-variant searches across ATS aggregators (Workday, Greenhouse, Lever, Ashby), curated boards (`ai-governance-jobs.com`, Built In, TheMuse, Prosple, Ladders, ALPFA, privacy.jobs), and general aggregators (Indeed, LinkedIn, ZipRecruiter, Dice). Workday-hosted pages 403 on direct fetch; verbatim requirement bullets for those were pulled from authoritative mirrors and flagged in each posting's `source_note` in the JSON.
2. Filtered per the ownership rule: excluded `Senior`, `Manager`, `Lead`, `Head`, `Director`, `Architect`, `VP`, `Chief` modifiers (those inherit upward to `senior-ai-governance-architect` / `head-of-ai-governance` / `chief-ai-officer`); excluded engineering-shaped titles (`AI Risk Engineer` → `ai-risk-engineer`; `AI Evaluation Engineer` → `ai-eval-engineer` / `ai-evaluation-engineer`); excluded generic `Privacy Analyst` / `GRC Analyst` / `Compliance Analyst` postings with no AI/ML reference; excluded frontier-lab safety-research PhD roles and think-tank policy-analyst roles with no AI-technical exposure.
3. Recomputed per-requirement frequencies against the 25-posting sample.
4. Applied the continuity-bias decision rule: propose net-new content only when (a) ≥ 3 distinct in-window postings cite a requirement the curriculum does NOT cover, (b) frequency ≥ 0.30, and (c) no existing module or exercise can be extended incrementally.

## Requirement themes → curriculum ownership

| # | Theme | Freq | Owner role | Coverage |
|---|---|---|---|---|
| 1 | Fluency with AI governance frameworks (NIST AI RMF, ISO/IEC 42001, EU AI Act, OECD) | 0.48 | `ai-governance-analyst` (this) | [`mod-101-ai-governance-landscape`](lessons/mod-101-ai-governance-landscape) |
| 2 | AI use-case intake, triage, and prioritisation | 0.36 | `ai-governance-analyst` | [`mod-102-ai-system-inventory-and-intake`](lessons/mod-102-ai-system-inventory-and-intake) |
| 3 | Model / AI system inventory maintenance | 0.40 | `ai-governance-analyst` | [`mod-102-ai-system-inventory-and-intake`](lessons/mod-102-ai-system-inventory-and-intake) |
| 4 | Framework crosswalks (NIST AI RMF ↔ ISO 42001 ↔ EU AI Act ↔ internal policy) | 0.20 | `ai-governance-analyst` | [`mod-101-ai-governance-landscape`](lessons/mod-101-ai-governance-landscape) + [`mod-108-controls-and-compliance-evidence`](lessons/mod-108-controls-and-compliance-evidence) |
| 5 | AI risk assessment authoring (first-draft) | 0.36 | `ai-governance-analyst` | [`mod-103-risk-assessment-authoring`](lessons/mod-103-risk-assessment-authoring) |
| 6 | Fairness / bias report reading and remediation coordination | 0.16 | `ai-governance-analyst` | [`mod-104-fairness-bias-and-model-behaviour-review`](lessons/mod-104-fairness-bias-and-model-behaviour-review) |
| 7 | Impact assessment authoring (AIA, DPIA, FRIA, sector-specific) | 0.24 | `ai-governance-analyst` | [`mod-105-impact-assessments-and-model-cards`](lessons/mod-105-impact-assessments-and-model-cards) |
| 8 | Model card / system card / datasheet authoring | 0.12 | `ai-governance-analyst` | [`mod-105-impact-assessments-and-model-cards`](lessons/mod-105-impact-assessments-and-model-cards) |
| 9 | Cross-jurisdiction regulatory tracking | 0.32 | `ai-governance-analyst` | [`mod-106-regulatory-tracking-and-jurisdictions`](lessons/mod-106-regulatory-tracking-and-jurisdictions) |
| 10 | Reading eval / red-team / audit evidence into governance records | 0.12 | `ai-governance-analyst` | [`mod-107-reading-eval-and-audit-evidence`](lessons/mod-107-reading-eval-and-audit-evidence) |
| 11 | Control-tracking and evidence-collection cycles | 0.20 | `ai-governance-analyst` | [`mod-108-controls-and-compliance-evidence`](lessons/mod-108-controls-and-compliance-evidence) |
| 12 | AI security threat taxonomy awareness (OWASP LLM Top 10, MITRE ATLAS, NIST AML) | 0.24 | `ai-governance-analyst` | [`mod-108-controls-and-compliance-evidence`](lessons/mod-108-controls-and-compliance-evidence) |
| 13 | AI incident response participation (analyst tier) | 0.08 | `ai-governance-analyst` | [`mod-109-incident-response-and-continuous-monitoring`](lessons/mod-109-incident-response-and-continuous-monitoring) |
| 14 | Continuous monitoring / post-market surveillance (reading and filing) | 0.16 | `ai-governance-analyst` | [`mod-109-incident-response-and-continuous-monitoring`](lessons/mod-109-incident-response-and-continuous-monitoring) |
| 15 | Stakeholder communication and council coordination | 0.36 | `ai-governance-analyst` | [`mod-110-communication-and-council-support`](lessons/mod-110-communication-and-council-support) |
| 16 | Privacy law adjacency (GDPR Article 22, DPIA overlap, personal-data flags) | 0.36 | `ai-governance-analyst` | [`mod-106-regulatory-tracking-and-jurisdictions`](lessons/mod-106-regulatory-tracking-and-jurisdictions) |
| 17 | Drafting internal AI policies / standards under senior guidance | 0.24 | `ai-governance-analyst` | [`mod-110-communication-and-council-support`](lessons/mod-110-communication-and-council-support) |
| 18 | Third-party AI vendor / model / dataset review (incl. shadow-AI discovery) | 0.20 | `ai-governance-analyst` | [`mod-108-controls-and-compliance-evidence`](lessons/mod-108-controls-and-compliance-evidence) |
| 19 | Basic Python + spreadsheet fluency for governance analytics | 0.16 | `ai-governance-analyst` | [`mod-102-ai-system-inventory-and-intake`](lessons/mod-102-ai-system-inventory-and-intake) |
| 20 | Certifications portfolio (IAPP AIGP v2.1 / CIPP / ISO 42001 LI/LA / CISA / CRISC / CISM) | 0.12 | `ai-governance-analyst` | Threaded through [`mod-101`](lessons/mod-101-ai-governance-landscape) + [`mod-106`](lessons/mod-106-regulatory-tracking-and-jurisdictions) + [`mod-110`](lessons/mod-110-communication-and-council-support) |
| 21 | AI evaluation methodology / red-team data / statistical methodology | n/a — peer specialist | `ai-eval-engineer` / `model-evaluation-engineer` / `ai-risk-engineer` | Linked out; analyst reads outputs and files them |
| 22 | Release-assurance / audit-trail methodology | n/a — peer specialist | `ai-evaluation-engineer` (level 25) | Linked out; analyst produces analyst-tier inputs |
| 23 | Deep ML/AI security | n/a — higher-level peer | `ai-infra-security` (level 35) | Awareness in mod-108; depth linked out |
| 24 | Control-library architecture / policy taxonomy / cross-jurisdiction reconciliation | n/a — next-up | `senior-ai-governance-architect` | Linked out |
| 25 | Program leadership, board reporting, regulator interface | n/a — next-up | `head-of-ai-governance` (level 40) / `chief-ai-officer` | Linked out |

**Frequency reading.** All frequencies are computed against the n=25 in-window sample. Some themes score low in the raw count because the postings tend to bullet only 3–8 requirements and route the rest through boilerplate — for example, model-card authoring (theme 8, freq 0.12) is nearly always assumed under the broader "AI governance documentation" bullet and is therefore under-counted; the theme remains high-value curriculum coverage even at low observed frequency.

## Emerging themes below the addition threshold (watch list)

These crossed the 3-posting count floor but not the 30% frequency floor. Per the continuity-bias rule they do NOT get new modules / exercises / projects this cycle. Documented so the next cycle can re-evaluate.

- **Agentic AI governance (freq 0.20)** — OpenAI ("Agentic Risk Analyst"), TransUnion ("deploying and monitoring AI agent workloads"), GM, Adobe, Aptiv. Concept-covered today via `mod-108` (OWASP LLM Top 10 2025 includes agentic entries) and `mod-109` (continuous monitoring). If the frequency crosses ~0.30 in the next cycle, propose a dedicated exercise in `mod-108` or `mod-109` rather than a new module — the agent-safety depth belongs to peer `agentic-safety-engineer-learning` (level 40) and should not migrate down here.
- **"Shadow AI" remediation / SaaS-embedded-AI discovery (freq 0.12)** — Pure Storage explicit; Aptiv and Experis implicit via third-party review. Mechanically covered by `mod-102` `exercise-05-pandas-reconciliation-drill` and `mod-108` third-party AI vendor review. If the "shadow AI" framing crystallises, a specific `mod-108` exercise (SaaS-embedded-AI discovery) is the incremental step.
- **Named GRC-tool breadth beyond the current vendor list (freq 0.24)** — OneTrust (Aptiv, Experis), Onspring (TransUnion), Archer + MetricStream (Experis). `mod-102` `exercise-04-grc-platform-analyst-tour` already covers Credo AI / Holistic AI / ModelOp / ServiceNow at the same conceptual depth; the OneTrust reference has been added to `authoritative_references` in this cycle. No exercise change needed — the tour concept scales.
- **Governance / compliance dashboards as an analyst deliverable (freq 0.16)** — Adobe intern, Lincoln Financial, TransUnion, Salesforce intern (Google Suite fluency). Reporting shape covered by `mod-108` `lab-01-produce-a-quarterly-control-status-report`; the dashboarding-tools angle is thinner. Watch for growth.
- **COPPA / children's-AI product safety (freq 0.04)** — single posting (Experis / toy company). Not a signal; noted as an example of the sector-specific overlay work `mod-106` covers.

## Posting evidence

| # | Employer | Title | Location | Date posted | URL |
|---|---|---|---|---|---|
| post-001 | TransUnion | AI Governance Analyst | Chicago, IL (Hybrid) | 2026-07-20 | [Workday](https://transunion.wd5.myworkdayjobs.com/en-US/TransUnion/job/AI-Governance-Analyst_19040360) |
| post-002 | Analog Devices | AI Governance Analyst | Austin, TX (On-site) | 2026-07-01 | [Workday](https://analogdevices.wd1.myworkdayjobs.com/en-US/External/job/AI-Governance-Analyst_R262486) |
| post-003 | Q2 Holdings | AI Governance & Compliance Analyst | Austin, TX (Hybrid) | 2026-07-20 | [Workday](https://q2ebanking.wd5.myworkdayjobs.com/en-US/Q2/job/AI-Governance---Compliance-Analyst_REQ-12635) |
| post-004 | Pure Storage | AI Governance Analyst | Lehi, UT | 2026-06-15 | [Greenhouse](https://job-boards.greenhouse.io/purestorage/jobs/7746667) |
| post-005 | Aptiv | AI Governance Analyst | Krakow, Poland | 2026-06-25 | [Workday](https://aptiv.wd5.myworkdayjobs.com/APTIV_CAREERS/job/AI-Governance-Analyst_J000682148) |
| post-006 | AIG | AI Governance Analyst | US | 2026-06-15 | [Workday](https://aig.wd1.myworkdayjobs.com/en-US/aig/job/AI-Governance-Analyst_JR2502341) |
| post-007 | Howden Group | AI Governance Analyst | Krakow, Poland | 2026-06-15 | [Workday](https://hyperiongrp.wd3.myworkdayjobs.com/en-US/Hyperion_External/job/Ai-Governance-Analyst_R0017471-1) |
| post-008 | Adobe | 2026 Intern - AI Governance | San Jose, CA (Hybrid) | 2026-06-01 | [Workday](https://adobe.wd5.myworkdayjobs.com/external_experienced/job/San-Jose/XMLNAME-2026-Intern---AI-Governance_R161481) |
| post-009 | Whoop | AI Risk & Compliance Analyst | Boston, MA (Hybrid) | 2026-06-01 | [Lever](https://jobs.lever.co/whoop/9f9d3b85-639a-41cf-a612-cee48c3d1bdf) |
| post-010 | Lincoln Financial | Analyst, AI Risk Management | Radnor, PA (multi) | 2026-07-10 | [Careers](https://jobs.lincolnfinancial.com/job/Radnor-Analyst,-AI-Risk-Management-PA/1398844800/) |
| post-011 | Experis USA | AI Risk & Compliance Analyst | NYC / Charlotte NC | 2026-07-09 | [Experis](https://www.experis.com/en/job/400989/ai-risk-compliance-analyst) |
| post-012 | Experis USA | AI Digital Safety, Regulatory and Compliance Analyst | El Segundo, CA | 2026-05-08 | [Experis](https://www.experis.com/en/job/397155/ai-digital-regulatory-and-compliance-analyst) |
| post-013 | Robert Half | AI Risk & Compliance Analyst | New York, NY | 2026-06-16 | [Robert Half](https://www.roberthalf.com/us/en/job/new-york-ny/ai-risk-compliance-analyst/02942-0013453698-usen) |
| post-014 | Carrington Mortgage Services | Analyst, IT AI Compliance | Remote / multi | 2026-05-15 | [Built In](https://builtin.com/job/analyst-it-artificial-intelligence-ai-compliance/9352475) |
| post-015 | Cisco | AI Governance Analyst | Austin, TX | 2026-06-15 | [LinkedIn](https://www.linkedin.com/jobs/view/ai-governance-analyst-at-cisco-3822473280) |
| post-016 | SAIC | AI Analyst - ServiceNow Now Assist | Remote (DC) | 2026-06-10 | [SAIC](https://jobs.saic.com/jobs/17946237-ai-analyst-servicenow-now-assist) |
| post-017 | Salesforce | Summer 2026 Intern - Responsible AI & Technology Product Analyst | Seattle, WA | 2026-05-15 | [The Muse](https://www.themuse.com/jobs/salesforce/summer-2026-intern-responsible-ai-technology-product-analyst) |
| post-018 | Stratacuity | AI Governance Operations Analyst | Richmond, VA (Hybrid) | 2026-07-01 | [beBee](https://bebee.com/us/jobs/ai-governance-analyst-stratacuity-richmond-va-united-states--appcast-7428_d840b4707ee9bb003865b952cae5d820e45d76170b28fb8ad2a6e047dabd55d9) |
| post-019 | General Motors | Sr Analyst - Data & AI Governance Transformation | Warren, MI | 2026-06-01 | [Workday](https://generalmotors.wd5.myworkdayjobs.com/Careers_GM/job/Warren-Michigan-United-States-of-America/Sr-Analyst---Data---AI-Governance-Transformation_JR-202606914) |
| post-020 | OpenAI | Agentic Risk Analyst | San Francisco, CA | 2026-06-20 | [GRC Careers](https://www.ai-governance-jobs.com/ai-grc-jobs/) |
| post-021 | Ethos Life | AI Compliance Analyst | Remote (US) | 2026-06-15 | [GRC Careers](https://www.ai-governance-jobs.com/) |
| post-022 | Babel Street | AI Governance Analyst | Reston, VA (Hybrid) | 2026-06-15 | [GRC Careers](https://www.ai-governance-jobs.com/) |
| post-023 | Simpson Thacher & Bartlett | AI Enablement + Adoption Analyst | New York, NY (Hybrid) | 2026-05-15 | [Indeed](https://www.indeed.com/viewjob?jk=9c774c09bd56aab5) |
| post-024 | Accelyst, LLC | Governance Analyst (Data, Information & AI) | Atlanta, GA (Hybrid) | 2026-06-15 | [Dice](https://www.dice.com/job-detail/c012dd47-be3e-4eea-b964-00789cb842cd) |
| post-025 | TransUnion | AI Governance Analyst | Los Angeles, CA (Hybrid) | 2026-07-20 | [GRC Careers](https://www.ai-governance-jobs.com/jobs/ai-governance-analyst-transunion-los-angeles-ca/) |

Full verbatim requirement bullets, preferred qualifications, salary bands, and source notes for each posting are in [`.aicg/job-requirements.json` → `postings`](.aicg/job-requirements.json). Postings 006, 007, 009, 013, 016, 018, 019, 020, 021, 022, 024, and 025 rely on snippet-level evidence pulled from search results or curated aggregators — the underlying ATS pages 403 to direct fetch — and are marked with `source_note` accordingly. Next cycle should verify them against authenticated ATS proxies.

## Ownership map — decision rules

- **AI Governance Analyst** (this track, level 15, Governance family) — owns operational analyst work: AI system intake and use-case triage, model / AI-system inventory maintenance, framework-mapping legwork, impact-assessment authoring, model-card / system-card / datasheet authoring, control-tracking and evidence-collection cycles, jurisdictional regulatory tracking, reading eval / red-team evidence enough to summarise it into a governance record, drafting policies and standards under senior guidance, and cross-functional council coordination.
- **AI Evaluation Engineer** (peer, level 25, Governance family, `ai-evaluation-engineer-learning`) — owns release-assurance / audit trail / regulator-facing methodology. This analyst hands ready-to-review packets to that peer and receives review verdicts back.
- **AI Risk Engineer** (peer, level 30, `ai-risk-engineer-learning`) — owns harm-model design, alignment-risk methodology, red-team data generation. This analyst consumes harm-model outputs and files them into the risk register.
- **AI Eval Engineer** (peer, level 30, AI Engineering family) — owns AI-application eval methodology depth.
- **Model Evaluation Engineer** (peer, level 30, ML Engineering family) — owns benchmark and statistical methodology depth.
- **Agentic Safety & Red-Team Engineer** (peer, level 40, `agentic-safety-engineer-learning`) — owns agent-specific safety and red-teaming depth. Emerging analyst-tier signal (freq 0.20) stays here at concept-awareness level (`mod-108` OWASP LLM Top 10, `mod-109` monitoring) unless the analyst-side frequency crosses the threshold.
- **AI Infra Security** (peer, level 35) — owns deep ML/AI security depth.
- **Senior AI Governance Architect** — next-up. Owns control-library architecture, policy taxonomy, cross-jurisdiction reconciliation. Inherits this packet and adds architectural scope.
- **Head of AI Governance** (level 40) — next-up leadership. Owns program leadership, board reporting, regulator engagement.
- **Chief AI Officer** (level 50) — executive scope.

## Salary evidence

Sampled from the eight postings in the corpus that published a salary band:

| Employer | Title | Location | Range (USD annual, unless noted) |
|---|---|---|---|
| TransUnion | AI Governance Analyst | Chicago / LA (Hybrid) | $78,750 – $131,250 |
| Pure Storage | AI Governance Analyst | Lehi, UT | $131,000 – $197,000 |
| Lincoln Financial | Analyst, AI Risk Management | Radnor, PA (multi) | $72,900 – $131,600 |
| Carrington Mortgage | Analyst, IT AI Compliance | Remote / multi | $95,000 – $105,000 |
| Ethos Life | AI Compliance Analyst | Remote (US) | $165,000 – $225,000 |
| Babel Street | AI Governance Analyst | Reston, VA (Hybrid) | $140,000 – $180,000 |
| Experis (toy co.) | AI Digital Safety, Regulatory and Compliance Analyst | El Segundo, CA | $35 – $45 / hr (contract) |
| Robert Half | AI Risk & Compliance Analyst | NYC | $80.75 – $93.50 / hr (contract) |

- **Aggregate US full-time band (n=6):** $72,900 low → $225,000 high; ~$105k median floor / ~$165k median ceiling.
- **Regulated-industry premium** is visible: insurtech (Ethos), defense-adjacent (Babel Street), and BigTech-security-org (Pure Storage) all clear $130k on the floor. Financial-services and consumer-product analyst roles cluster $73k – $132k.
- **Aggregator context:** `ai-governance-jobs.com` reports a July 2026 US-wide range of $40.62 – $67.07 / hour for the title "AI Governance Analyst" — consistent with the mid-band above.
- **Non-US postings** (Krakow, Ireland, Toronto, Doha, Europe) did not publish salary in the sampled window. Next cycle should sample 5+ non-US postings with salary bands to build a defensible geography breakdown.
