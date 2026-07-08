# Job Requirements — AI Governance Analyst

**Role level:** 15 (entry / early-career — Governance family)
**Track:** `ai-governance-analyst-learning`
**Research window:** 2026-04-09 → 2026-07-08 (last 90 days)
**Today:** 2026-07-08

This file documents the requirements catalog used to seed the AI Governance Analyst curriculum. Raw normalized data lives in [`.aicg/job-requirements.json`](.aicg/job-requirements.json); the planned curriculum lives in [`.aicg/curriculum-plan.json`](.aicg/curriculum-plan.json).

## Status — bootstrap session, live postings deferred

<!-- needs-research: collect ≥25 distinct in-window postings titled "AI Governance Analyst" / "Responsible AI Analyst" / "AI Risk & Compliance Analyst" / "AI Ethics Analyst" / "AI Policy Analyst" / "Trustworthy AI Analyst" / "AI Governance Specialist" / "AI Compliance Analyst" / "GRC Analyst — AI" / "AI Assurance Analyst" / "Model Risk Analyst — AI/ML" / "AI Program Analyst" / "AI Regulatory Analyst" / "Responsible AI Coordinator" / "AI Trust Analyst". Filter OUT "Senior", "Manager", "Lead", "Head", "Director", "Architect" modifiers (those inherit this packet upward toward `senior-ai-governance-architect` / `head-of-ai-governance` / `chief-ai-officer`), OUT engineering-shaped titles that own methodology depth (`AI Risk Engineer` → `ai-risk-engineer`; `AI Evaluation Engineer` → `ai-eval-engineer` / `ai-evaluation-engineer`), and OUT generic "Privacy Analyst" / "GRC Analyst" / "Compliance Analyst" postings that make no reference to AI/ML/model risk (those belong to a general privacy/compliance track). Re-validate every requirement against the live evidence and demote any theme whose evidence stays empty. -->

This packet was authored in a bootstrap session **without an exercised WebSearch / WebFetch pass against live job boards** (WebSearch / WebFetch permissions were not granted in-session). Per the project rules (*"Do not invent facts, incidents, or salary figures. Cite sources."*), the `postings` array in [`.aicg/job-requirements.json`](.aicg/job-requirements.json) is intentionally empty — the curriculum will not claim to have analysed 25 live postings when none were fetched.

The autonomous research loop is expected to fill that gap on its next cycle. To keep the loop deterministic and to give the curriculum a defensible baseline in the meantime, this document grounds the requirements catalog in **authoritative public references** that publish what the role is hired against:

- **International standards** — [NIST AI RMF 1.0 (AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf), the [NIST AI RMF Generative AI Profile (AI 600-1)](https://airc.nist.gov/AI_RMF_Knowledge_Base/AI_RMF/Uses/GenAI-Profile), the [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook), [ISO/IEC 42001:2023](https://www.iso.org/standard/81230.html), [ISO/IEC 23894:2023](https://www.iso.org/standard/77304.html), [ISO/IEC 23053:2022](https://www.iso.org/standard/74438.html), [ISO/IEC 22989:2022](https://www.iso.org/standard/74296.html), [ISO/IEC 42005:2025](https://www.iso.org/standard/44545.html), [ISO/IEC 38507:2022](https://www.iso.org/standard/56641.html).
- **Regulation and public policy** — [EU AI Act (Regulation 2024/1689)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) including [Annex III](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32024R1689), the [EU AI Office General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice), the [OECD AI Principles](https://oecd.ai/en/ai-principles), the [Council of Europe Framework Convention on AI](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence), the [UNESCO Recommendation on the Ethics of AI](https://www.unesco.org/en/artificial-intelligence/recommendation-ethics), the [Colorado AI Act (SB 24-205)](https://leg.colorado.gov/bills/sb24-205), [NYC Local Law 144](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page), [EEOC guidance on AI in employment](https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial), the [FDA / Health Canada / MHRA Good ML Practice guiding principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles), [US Federal Reserve SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) + [OCC Bulletin 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html), [Canada's Directive on Automated Decision-Making + AIA tool](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/responsible-use-ai/algorithmic-impact-assessment.html), the [UK Algorithmic Transparency Recording Standard](https://www.gov.uk/government/publications/algorithmic-transparency-recording-standard-hub), [GDPR Article 22](https://gdpr-info.eu/art-22-gdpr/), and the [NIST Privacy Framework](https://www.nist.gov/privacy-framework).
- **Documentation practice** — [Model Cards for Model Reporting (Mitchell et al. 2019)](https://arxiv.org/abs/1810.03993), [Datasheets for Datasets (Gebru et al. 2018)](https://arxiv.org/abs/1803.09010), the [Hugging Face Model Cards guide](https://huggingface.co/docs/hub/model-cards), the [Google Model Card Toolkit](https://github.com/tensorflow/model-card-toolkit), the [Partnership on AI ABOUT ML documentation guidance](https://partnershiponai.org/paper/about-ml/), and public examples: [OpenAI system cards](https://openai.com/safety/), [Anthropic's Responsible Scaling Policy](https://www.anthropic.com/rsp).
- **Fairness and bias tooling** — [Fairlearn](https://fairlearn.org/), [IBM AI Fairness 360](https://aif360.res.ibm.com/), [Google What-If Tool](https://pair-code.github.io/what-if-tool/).
- **AI security threat taxonomies** — [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/), [MITRE ATLAS](https://atlas.mitre.org/), [Google SAIF](https://safety.google/cybersecurity-advancements/saif/), [NIST AI 100-2 Adversarial ML Taxonomy](https://csrc.nist.gov/publications/detail/nistir/8269/draft), [AIRO — AI Risk Ontology](https://w3id.org/AIRO).
- **Vendor governance / GRC-for-AI platforms** — [Credo AI](https://www.credo.ai/product), [Holistic AI](https://www.holisticai.com/), [Fiddler AI](https://docs.fiddler.ai/), [ModelOp](https://www.modelop.com/), [ServiceNow AI Control Tower](https://www.servicenow.com/products/ai-control-tower.html).
- **AISI-adjacent evaluation evidence the analyst reads (does not author)** — [UK AISI Inspect harness](https://inspect.aisi.org.uk/), [US AI Safety Institute Consortium](https://www.nist.gov/aisi).
- **Certifications** — [IAPP AIGP](https://iapp.org/certify/aigp/) (most cited), [IAPP CIPP/US · CIPP/E](https://iapp.org/certify/), plus emerging ISO/IEC 42001 lead-implementer / lead-auditor programs, and independent-auditor credentials from [ForHumanity](https://forhumanity.center/independent-audit-of-ai-systems/) and [BABL AI](https://babl.ai/).

Every requirement below cites at least one such reference, and every requirement is shaped so posting-frequency evidence can be added underneath it without restructure.

## Methodology

1. Sourced the canonical task domains for an entry-level AI governance analyst from the public references catalogued in `.aicg/job-requirements.json → authoritative_references`.
2. Mapped each task domain to (a) the role on our level ladder that should own it primarily and (b) the curriculum module that will cover it.
3. Applied the **ownership rule** — assign coverage to the lowest-level role that genuinely requires the skill; higher-level tracks link back rather than duplicate. In particular, deferred:
   - *Up* to `senior-ai-governance-architect` for framework architecture (control library design, policy taxonomy, cross-jurisdiction reconciliation) and to `head-of-ai-governance` for program leadership (board reporting, budget, external / regulator engagement).
   - *Sideways* to `ai-evaluation-engineer` (peer, level 25, Governance family) for release-assurance / audit-trail methodology.
   - *Sideways* to `ai-risk-engineer` (peer, level 30) for harm-model design and red-team data generation.
   - *Sideways* to `ai-eval-engineer` (peer, level 30, AI Engineering family) for AI-application eval methodology depth.
   - *Sideways* to `model-evaluation-engineer` (peer, level 30, ML Engineering family) for benchmark construction and statistical methodology depth.
   - *Sideways* to `ai-infra-security` (level 35) for deep ML/AI security depth.
   - *Out of scope* to general privacy engineering and legal counsel — the analyst reads GDPR / CCPA / HIPAA text at a paralegal level but does not deliver a legal opinion.
4. Flagged everything that has not yet been validated against in-window postings so the next cycle can demote any requirement whose evidence stays empty.

## Requirement themes → curriculum ownership

The table below lists each requirement theme, its planned owner per the level hierarchy, and the curriculum coverage path. **Freq** is intentionally blank for this cycle — it will be backfilled by the next research pass.

| # | Theme | Freq | Owner role | Coverage |
|---|---|---|---|---|
| 1 | Fluency with AI governance frameworks (NIST AI RMF, ISO/IEC 42001, EU AI Act, OECD) | <!-- needs-research --> | `ai-governance-analyst` (this) | [`mod-101-ai-governance-landscape`](lessons/mod-101-ai-governance-landscape) |
| 2 | AI use-case intake, triage, and prioritisation | <!-- needs-research --> | `ai-governance-analyst` | [`mod-102-ai-system-inventory-and-intake`](lessons/mod-102-ai-system-inventory-and-intake) |
| 3 | Model / AI system inventory maintenance | <!-- needs-research --> | `ai-governance-analyst` | [`mod-102-ai-system-inventory-and-intake`](lessons/mod-102-ai-system-inventory-and-intake) |
| 4 | Framework crosswalks (NIST AI RMF ↔ ISO 42001 ↔ EU AI Act ↔ internal policy) | <!-- needs-research --> | `ai-governance-analyst` | [`mod-101-ai-governance-landscape`](lessons/mod-101-ai-governance-landscape) + [`mod-108-controls-and-compliance-evidence`](lessons/mod-108-controls-and-compliance-evidence) |
| 5 | AI risk assessment authoring (first-draft) | <!-- needs-research --> | `ai-governance-analyst` | [`mod-103-risk-assessment-authoring`](lessons/mod-103-risk-assessment-authoring) |
| 6 | Fairness / bias report reading and remediation coordination | <!-- needs-research --> | `ai-governance-analyst` | [`mod-104-fairness-bias-and-model-behaviour-review`](lessons/mod-104-fairness-bias-and-model-behaviour-review) |
| 7 | Impact assessment authoring (AIA, DPIA, FRIA, sector-specific) | <!-- needs-research --> | `ai-governance-analyst` | [`mod-105-impact-assessments-and-model-cards`](lessons/mod-105-impact-assessments-and-model-cards) |
| 8 | Model card / system card / datasheet authoring | <!-- needs-research --> | `ai-governance-analyst` | [`mod-105-impact-assessments-and-model-cards`](lessons/mod-105-impact-assessments-and-model-cards) |
| 9 | Cross-jurisdiction regulatory tracking | <!-- needs-research --> | `ai-governance-analyst` | [`mod-106-regulatory-tracking-and-jurisdictions`](lessons/mod-106-regulatory-tracking-and-jurisdictions) |
| 10 | Reading eval / red-team / audit evidence into governance records | <!-- needs-research --> | `ai-governance-analyst` | [`mod-107-reading-eval-and-audit-evidence`](lessons/mod-107-reading-eval-and-audit-evidence) |
| 11 | Control-tracking and evidence-collection cycles | <!-- needs-research --> | `ai-governance-analyst` | [`mod-108-controls-and-compliance-evidence`](lessons/mod-108-controls-and-compliance-evidence) |
| 12 | AI security threat taxonomy awareness (OWASP LLM Top 10, MITRE ATLAS, NIST AML) | <!-- needs-research --> | `ai-governance-analyst` | [`mod-108-controls-and-compliance-evidence`](lessons/mod-108-controls-and-compliance-evidence) |
| 13 | AI incident response participation (analyst tier) | <!-- needs-research --> | `ai-governance-analyst` | [`mod-109-incident-response-and-continuous-monitoring`](lessons/mod-109-incident-response-and-continuous-monitoring) |
| 14 | Continuous monitoring / post-market surveillance (reading and filing) | <!-- needs-research --> | `ai-governance-analyst` | [`mod-109-incident-response-and-continuous-monitoring`](lessons/mod-109-incident-response-and-continuous-monitoring) |
| 15 | Stakeholder communication and council coordination | <!-- needs-research --> | `ai-governance-analyst` | [`mod-110-communication-and-council-support`](lessons/mod-110-communication-and-council-support) |
| 16 | Privacy law adjacency (GDPR Article 22, DPIA overlap, personal-data flags) | <!-- needs-research --> | `ai-governance-analyst` | [`mod-106-regulatory-tracking-and-jurisdictions`](lessons/mod-106-regulatory-tracking-and-jurisdictions) |
| 17 | Drafting internal AI policies / standards under senior guidance | <!-- needs-research --> | `ai-governance-analyst` | [`mod-110-communication-and-council-support`](lessons/mod-110-communication-and-council-support) |
| 18 | Third-party AI vendor / model / dataset review | <!-- needs-research --> | `ai-governance-analyst` | [`mod-108-controls-and-compliance-evidence`](lessons/mod-108-controls-and-compliance-evidence) |
| 19 | Basic Python + spreadsheet fluency for governance analytics | <!-- needs-research --> | `ai-governance-analyst` | [`mod-102-ai-system-inventory-and-intake`](lessons/mod-102-ai-system-inventory-and-intake) |
| 20 | Certifications portfolio (IAPP AIGP / CIPP / ISO 42001 LI/LA) | <!-- needs-research --> | `ai-governance-analyst` | Threaded through [`mod-101`](lessons/mod-101-ai-governance-landscape) + [`mod-106`](lessons/mod-106-regulatory-tracking-and-jurisdictions) |
| 21 | AI evaluation methodology / red-team data / statistical methodology | n/a — peer specialist | `ai-eval-engineer` / `model-evaluation-engineer` / `ai-risk-engineer` | Linked out; analyst reads outputs and files them |
| 22 | Release-assurance / audit-trail methodology | n/a — peer specialist | `ai-evaluation-engineer` (level 25) | Linked out; analyst produces analyst-tier inputs |
| 23 | Deep ML/AI security | n/a — higher-level peer | `ai-infra-security` (level 35) | Awareness in mod-108; depth linked out |
| 24 | Control-library architecture / policy taxonomy / cross-jurisdiction reconciliation | n/a — next-up | `senior-ai-governance-architect` | Linked out |
| 25 | Program leadership, board reporting, regulator interface | n/a — next-up | `head-of-ai-governance` (level 40) / `chief-ai-officer` | Linked out |

## Posting evidence

<!-- needs-research: populate with the ≥25 in-window postings sampled next cycle. Use the same table shape as `agentic-ai-engineer-learning/JOB_REQUIREMENTS.md`. -->

No postings were sampled this cycle. See the **Status** section above for the reason. The next autonomous research cycle should fan out across:

- **ATS aggregators** — `boards.greenhouse.io`, `jobs.lever.co`, `jobs.ashbyhq.com`, `app.workable.com`, `myworkdayjobs.com`, `smartrecruiters.com`.
- **Frontier-lab governance / trust teams** — OpenAI (Safety Systems / Trust), Anthropic (Responsible Scaling, Trust & Safety), Google DeepMind (Responsibility & Safety), Meta (Responsible AI), Microsoft (AETHER / ORA / Office of Responsible AI), Apple (ML Privacy), Amazon (Responsible AI), xAI, Character.AI. Reject research-scientist safety roles that require an ML PhD — those belong to safety-research tracks.
- **Hyperscaler cloud AI trust teams** — Google Cloud (Vertex AI trust), Azure AI (Responsible AI), AWS (Bedrock Responsible AI).
- **Enterprise regulated-industry AI teams** — Financial: JPMorgan, Goldman, Bank of America, Wells Fargo, Citi, Morgan Stanley (model risk); Bloomberg AI trust. Health: UnitedHealth, CVS, Humana, Cigna, Kaiser (clinical AI governance). Pharma: Pfizer, Novartis, Merck, Roche (pharma AI governance). Insurance: Allstate, Progressive, Nationwide, Liberty Mutual. Insurance model-risk governance often surfaces this role.
- **Governance-tooling employers** — Credo AI, Holistic AI, Fairly AI, Fiddler AI, Arthur AI, ModelOp, WhyLabs, Robust Intelligence, Trustible, Enzai, Monitaur, Verify AI, BABL AI, ForHumanity.
- **Public sector and civil society** — NIST, UK AI Safety Institute, US AI Safety Institute, EU AI Office, OECD.AI, GPAI, Partnership on AI, MITRE, RAND.
- **Audit / assurance firms building AI practice** — Deloitte / EY / PwC / KPMG responsible AI practices, plus Accenture, BCG (X), McKinsey (QuantumBlack).

For each posting, capture employer, exact title, URL, `date_observed`, `date_posted` (or `estimated:2026-MM`), location, 5–10 verbatim requirement bullets, 2–6 preferred-qualification bullets, salary range when published, and one short representative quote. Filter out:

- **Senior / Manager / Lead / Head / Director / Architect modifiers** — those inherit this packet upward.
- **AI Risk Engineer** postings — those belong to `ai-risk-engineer` (peer specialist, level 30) which owns harm-model methodology.
- **AI Evaluation Engineer** postings — those belong to `ai-eval-engineer` (AI Engineering family, level 30) or `ai-evaluation-engineer` (Governance family, level 25) depending on the shape.
- **Generic Privacy Analyst / GRC Analyst / Compliance Analyst** postings that make no reference to AI/ML/model risk — those belong to a general privacy/compliance track.
- **Frontier-lab safety-research** postings that require ML PhD — those belong to safety-research tracks.
- **Think-tank policy-analyst** postings that require zero AI-technical exposure — those belong to a policy-analyst track.

## Ownership map — quick reference for next cycle

When backfilling postings, use this ownership decision to keep the curriculum from drifting into peer territory:

- **AI Governance Analyst** (this track, level 15, Governance family) — owns operational analyst work: AI system intake and use-case triage, model / AI-system inventory maintenance, framework-mapping legwork, impact-assessment authoring, model-card / system-card / datasheet authoring, control-tracking and evidence-collection cycles, jurisdictional regulatory tracking, reading eval / red-team evidence enough to summarise it into a governance record, drafting policies and standards under senior guidance, and cross-functional council coordination.
- **AI Evaluation Engineer** (peer, level 25, Governance family, `ai-evaluation-engineer-learning`) — owns release-assurance / audit trail / regulator-facing methodology. **This analyst hands ready-to-review packets to that peer and receives review verdicts back.**
- **AI Risk Engineer** (peer, level 30, `ai-risk-engineer-learning`) — owns harm-model design, alignment-risk methodology, red-team data generation. **This analyst consumes harm-model outputs and files them into the risk register.**
- **AI Eval Engineer** (peer, level 30, AI Engineering family) — owns AI-application eval methodology depth.
- **Model Evaluation Engineer** (peer, level 30, ML Engineering family) — owns benchmark and statistical methodology depth.
- **AI Infra Security** (peer, level 35) — owns deep ML/AI security depth.
- **Senior AI Governance Architect** — next-up. Owns control-library architecture, policy taxonomy, cross-jurisdiction reconciliation. **Inherits this packet and adds architectural scope.**
- **Head of AI Governance** (level 40) — next-up leadership. Owns program leadership, board reporting, regulator engagement.
- **Chief AI Officer** (level 50) — executive scope.

## Salary evidence

<!-- needs-research: aggregate salary from live in-window postings across US / EU / UK / Canada / APAC and report per-geography ranges with sample size and posting-title distribution. -->

No compensation claims are made in this bootstrap packet. The next research cycle should populate a `salary_range` field per posting (verbatim from the source). Only after ≥5 in-window observations should an aggregated range be reported, with sample size and geography attached.
