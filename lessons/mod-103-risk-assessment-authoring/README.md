# mod-103 — First-Draft AI Risk Assessment Authoring

**Estimated effort:** 12 hours

The first-draft risk assessment is the analyst's most consequential technical artefact. It is what the reviewer signs off on, what the owner accepts, and what the auditor pulls three years later. This module walks the whole authoring cycle: NIST AI RMF MAP walkthrough → ISO/IEC 23894 risk-source overlay → GenAI Profile scoring → SR 11-7 shape for FSI → routing, residuals, executive framing.

## Learning objectives

- Walk a new AI use case through NIST AI RMF MAP 1–5 and produce a narrative first-draft context / stakeholder / risk-source case study — not a checklist.
- Overlay ISO/IEC 23894 risk-source categories and the NIST AI RMF Generative AI Profile 12 risks as a two-lens sweep to produce a defensible register-entry set.
- Score each register entry with ordinal (Low / Medium / High) inherent, residual, and control-defeated claims, each paired with a one-line rationale, and propose mitigations by category (preventive / detective / corrective / transfer / accept).
- Apply the [SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) model-risk-management shape when the enterprise is a regulated financial institution.
- Route each risk to the correct owner (product / ML / security / legal / privacy) with a proposed action and an SLA, negotiate the residual, and translate the register into a one-page executive framing that reports the profile rather than an aggregate score.

## Chapters

| # | Chapter | Focus |
|---|---|---|
| 01 | [Walking a Use Case Through NIST AI RMF MAP](01-nist-rmf-map-walkthrough.md) | MAP 1 through MAP 5 as narrative; MAP walk sequence; impact-framing shape |
| 02 | [Overlaying ISO/IEC 23894 Risk Sources on the MAP Walk](02-iso-23894-risk-sources-overlay.md) | Risk-source categories; two-lens sweep against the GenAI Profile |
| 03 | [Scoring the Register Entry — GenAI Profile Risks and the Likelihood-Magnitude Pass](03-genai-profile-scoring-and-register-entry.md) | 3×3 grid; inherent vs residual vs control-defeated; mitigation categories |
| 04 | [SR 11-7 Shape — Model Risk for Regulated Financial Institutions](04-sr-11-7-shape-for-financial-services.md) | Three-pillar shape; developer/validator independence; materiality tiering |
| 05 | [Routing Risks, Residual Claims, and the Executive Framing](05-routing-residuals-and-executive-framing.md) | Routing packet; residual negotiation; one-page executive summary |

## Exercises

Hands-on prompts; solutions live in the paired `ai-governance-analyst-solutions` repository.

| # | Exercise | Estimated |
|---|---|---|
| 01 | [NIST RMF MAP Walkthrough](exercises/exercise-01-nist-rmf-map-walkthrough.md) | 2 h |
| 02 | [ISO 23894 Risk Sources Overlay](exercises/exercise-02-iso-23894-risk-sources-overlay.md) | 2 h |
| 03 | [GenAI Profile Risk Scoring](exercises/exercise-03-genai-profile-risk-scoring.md) | 2 h |
| 04 | [SR 11-7 Mapping for FS Use Case](exercises/exercise-04-sr-11-7-mapping-for-fs-use-case.md) | 2 h |
| 05 | [Residual Risk Routing Drill](exercises/exercise-05-residual-risk-routing-drill.md) | 2 h |

## Lab

- `lab-01` — Not yet authored; scheduled for the next content cycle.

## Quiz

- One knowledge check per the curriculum plan. Not yet authored; scheduled for the next content cycle.

## Resources

Curated references are in [`resources.md`](resources.md).

## Prerequisites

Fluency in `mod-101` (RMF, GenAI Profile, ISO 42001) and `mod-102` (intake, inventory, tier tagging) — the risk assessment starts from an already-triaged intake row.

## Downstream dependencies

- `mod-105-impact-assessments-and-model-cards` reuses the MAP narrative for AIA / FRIA / DPIA authoring.
- `mod-107-reading-eval-and-audit-evidence` reads eval evidence into the register to close out residuals.
- `mod-108-controls-and-compliance-evidence` maps proposed controls to the enterprise control library.
- `mod-109-incident-response-and-continuous-monitoring` uses the control-defeated column to interpret monitoring alerts.
- `project-101` chains this module with `mod-102` and `mod-105` end-to-end.
