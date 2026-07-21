# mod-102 — AI System Intake and Inventory Maintenance

**Estimated effort:** 12 hours

The AI governance program lives or dies on its intake and its inventory. If the intake questionnaire is badly designed, requesters bounce off it and shadow AI grows. If the inventory drifts against the ML team's model registry, the risk assessments, controls, and reviewer packs downstream all cite the wrong version of the world. This module is how you keep both clean.

## Learning objectives

- Design an AI use-case intake questionnaire with the fields employers actually populate — business owner, purpose, autonomy, data sources, model family, deployment surface, third-party dependencies, EU AI Act tier, applicable sector regulator — and know why each field is on the form.
- Triage an incoming intake into in-scope / out-of-scope / needs-follow-up buckets against the enterprise definition and the EU AI Act tier scheme, and route boundary cases correctly.
- Maintain an AI-system inventory row aligned with the ML team's model registry, including material-change re-review triggers and retirement handling.
- Use GRC-for-AI platforms (Credo AI, Holistic AI, ModelOp, ServiceNow AI Control Tower) at analyst level and produce the spreadsheet-shaped equivalent when the enterprise has not yet adopted a platform.
- Reconcile a model-registry export against a governance-inventory export in pandas or Excel, and file the delta as a governance-record row.

## Chapters

| # | Chapter | Focus |
|---|---|---|
| 01 | [The AI Use-Case Intake Questionnaire — Fields Employers Actually Populate](01-intake-questionnaire-design.md) | The canonical intake schema; business / technical / governance field split; definitions that work |
| 02 | [Intake Triage — In-Scope / Out-of-Scope / Needs-Follow-Up](02-triage-and-tier-tagging-workflow.md) | The three-bucket triage; EU AI Act tier decision tree; enterprise-internal tier overlay |
| 03 | [The AI System Inventory — Row Schema and Registry Sync](03-inventory-row-and-registry-sync.md) | Inventory row fields; distinction from model registry / risk register / control matrix; material change |
| 04 | [GRC-for-AI Platforms at Analyst Level — and the Spreadsheet Fallback](04-grc-platforms-for-ai-at-analyst-level.md) | Credo AI, Holistic AI, ModelOp, ServiceNow AI Control Tower; the spreadsheet-fallback discipline |
| 05 | [Reconciling the Model Registry Against the Governance Inventory — pandas / Excel](05-pandas-and-excel-reconciliation.md) | The three-set diff; material-change signals; the reconciliation record row |

## Exercises

Hands-on prompts; solutions live in the paired `ai-governance-analyst-solutions` repository.

| # | Exercise | Estimated |
|---|---|---|
| 01 | [Intake Questionnaire Design](exercises/exercise-01-intake-questionnaire-design.md) | 2 h |
| 02 | [EU AI Act Tier Triage Workflow](exercises/exercise-02-eu-ai-act-tier-triage-workflow.md) | 2 h |
| 03 | [Inventory Row Schema and Example](exercises/exercise-03-inventory-row-schema-and-example.md) | 2 h |
| 04 | [GRC Platform Analyst Tour](exercises/exercise-04-grc-platform-analyst-tour.md) | 2 h |
| 05 | [Pandas Reconciliation Drill](exercises/exercise-05-pandas-reconciliation-drill.md) | 2 h |

## Lab

- `lab-01` — Not yet authored; scheduled for the next content cycle.

## Quiz

- One knowledge check per the curriculum plan. Not yet authored; scheduled for the next content cycle.

## Resources

Curated references are in [`resources.md`](resources.md).

## Prerequisites

Fluency in `mod-101-ai-governance-landscape` — you must be able to walk the EU AI Act tier scheme, cite NIST AI RMF MAP subcategories, and recognise ISO/IEC 42001 Clause 6 language before starting this module.

## Downstream dependencies

- `mod-103-risk-assessment-authoring` walks the risk assessment for a system the intake has already tagged.
- `mod-105-impact-assessments-and-model-cards` uses the intake row as the starting fields for AIA / FRIA / DPIA authoring.
- `mod-108-controls-and-compliance-evidence` reads the inventory row when picking the SoA slice per system.
- `project-101-end-to-end-intake-inventory-and-impact-assessment` chains this module end-to-end for a single use case.
