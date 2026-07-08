# Prerequisites — AI Governance Analyst

**Role level:** 15 (entry / early-career — AI Governance family)

This is an early-career track. It assumes a working professional posture but not deep engineering, statistical, or legal specialisation. The prerequisites below are the shape a learner should show up with; the curriculum itself teaches the AI-governance-specific overlays.

## Assumed background

- **General literacy in software and data systems.** Comfortable reading a system-architecture diagram, distinguishing an API from a database from a model artifact, and understanding what "deployed to production" means without needing an engineer to translate. No coding fluency required; see the Python note below for the light hands-on component.
- **Comfort with policy / compliance / risk language.** Prior exposure to a compliance regime (SOC 2, ISO 27001, HIPAA, GDPR, PCI-DSS, SOX, banking model-risk under SR 11-7) or a governance function (risk, audit, legal, privacy) at any tier. If none, expect to spend an extra ~10 hours on the ISO/IEC 42001 clause walkthrough (mod-101) to catch up on management-system vocabulary.
- **Reading discipline for technical / regulatory documents.** Ability to read a 40–80 page standards document (NIST AI RMF, ISO/IEC 42001, EU AI Act preamble + Annexes) and produce a paraphrase without hallucinating clauses that are not present.
- **Spreadsheet fluency.** Comfortable with pivot tables, filters, cross-sheet references, and basic formulas. mod-102 assumes this level.
- **Written and verbal communication skills.** Ability to write a two-page executive brief that survives review by legal / privacy / product / ML stakeholders. mod-110 builds AI-specific structure on top of an already-decent baseline.

## Nice-to-have background

- **A basic Python + pandas capability** (read a CSV / JSON, join two tables, produce a summary). Not required to start; the curriculum will point you at the [`ai-infra-junior-engineer-learning`](https://github.com/ai-infra-curriculum/ai-infra-junior-engineer-learning) prerequisite track if you want to pick this up. mod-102 includes a low-stakes pandas reconciliation drill.
- **A prior privacy or GRC certification.** IAPP CIPP/US or CIPP/E, ISACA CRISC, ISO/IEC 27001 lead-implementer, or comparable. Not required; the curriculum treats these as add-on credentials in mod-110's certifications planner.
- **Some exposure to ML / AI concepts at a lay-reader level** (what a model is, what training vs. inference means, roughly what an LLM does). No math required.

## What this curriculum does *not* teach — link out to the owner instead

- **Building or fine-tuning models.** Owned by [`ml-engineer-learning`](https://github.com/ml-engineering-curriculum/ml-engineer-learning) (level 20) and [`fine-tuning-engineer-learning`](https://github.com/ml-engineering-curriculum/fine-tuning-engineer-learning).
- **Designing AI evaluations, harm models, or red-team datasets.** Owned by [`ai-eval-engineer-learning`](https://github.com/ai-engineering-curriculum/ai-eval-engineer-learning), [`model-evaluation-engineer-learning`](https://github.com/ml-engineering-curriculum/model-evaluation-engineer-learning), and [`ai-risk-engineer-learning`](https://github.com/ml-engineering-curriculum/ai-risk-engineer-learning).
- **Owning the release-assurance / audit-trail / regulator-facing methodology.** Owned by the peer specialist track [`ai-evaluation-engineer-learning`](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-learning) (level 25, Governance family) — this analyst hands ready-to-review packets to that peer.
- **Designing the enterprise AI control library or the policy taxonomy.** Owned by [`senior-ai-governance-architect-learning`](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning).
- **Program leadership, board reporting, budget, regulator engagement.** Owned by [`head-of-ai-governance-learning`](https://github.com/ai-governance-curriculum/head-of-ai-governance-learning) and [`chief-ai-officer-learning`](https://github.com/ai-governance-curriculum/chief-ai-officer-learning).
- **Deep ML / AI security.** Owned by [`ai-infra-security-learning`](https://github.com/ai-infra-curriculum/ai-infra-security-learning) (level 35). This track teaches only the taxonomy awareness needed to file a security-linked record and route it.
- **Legal opinion on statutes and regulations.** Owned by legal counsel. This track teaches paralegal-level reading — recognising an obligation, filing a note, and routing to counsel.

## What you should be able to do on day one after finishing this curriculum

- Take a new AI use case through intake, tier it against the EU AI Act, populate the inventory row, and hand a first-draft risk assessment to the risk owner.
- Author a fundamental-rights or algorithmic impact assessment, a model card, and a datasheet from ML-team inputs, and cross-link them from the inventory row.
- Read a fairness / bias report, a red-team engagement summary, and an internal eval report enough to write the governance-record summary and file the follow-ups.
- Run a control-testing cycle, pull evidence, and produce the analyst-tier control-status report.
- Track a rolling set of AI regulations across two to three jurisdictions and produce a monthly council digest.
- Prepare a pre-read deck and a decision log for an AI governance council meeting, and draft a first-cut acceptable-use policy for senior review.
- Recognise which items belong on your desk and which belong upstairs (architect, head of governance) or sideways (evaluation, risk, security, legal) — and route accordingly.
