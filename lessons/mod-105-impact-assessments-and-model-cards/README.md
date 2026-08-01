# mod-105 — Impact Assessments, Model Cards, System Cards, and Datasheets

**Estimated effort:** 14 hours

The impact assessment is the artefact the analyst delivers to counsel, to the regulator, and — years later — to the auditor reconstructing what the enterprise knew when the system was deployed. The model card, system card, and datasheets are the evidence corpus the impact assessment reads from. This module walks the shape of each artefact, the ISO/IEC 42005 scaffold that unifies them, and the cross-referencing discipline that keeps the corpus consistent as it grows across a portfolio of systems.

## Learning objectives

- Author drafts of the four canonical AI impact assessments — algorithmic impact assessment (Canadian AIA shape), fundamental-rights impact assessment (EU AI Act Article 27), data-protection impact assessment (GDPR Article 35), and sector-specific impact assessment (e.g., FDA good-ML-practice pre-market submission slice) — from a shared template that reuses NIST MAP output.
- Apply ISO/IEC 42005 as the AI-specific impact-assessment standard scaffold.
- Author a model card following Mitchell et al. (2019), a system card following public OpenAI / Anthropic examples at internal scale, and a datasheet for a dataset following Gebru et al. (2018).
- Publish through the Hugging Face model-card format or the Google Model Card Toolkit and know when an internal template supersedes both.
- Cross-reference model card, impact assessment, and inventory row so a reader can walk from any one to the others.
- Populate the analyst-tier sections yourself and coordinate with the ML team on the model-behaviour and evaluation-evidence sections.

## Chapters

| # | Chapter | Focus |
|---|---|---|
| 01 | [ISO/IEC 42005 as the Impact-Assessment Scaffold and the Shared-Template Idea](01-iso-42005-scaffold-and-shared-template.md) | Standards stack; documentary and procedural elements; MAP-to-42005 mapping; canonical document + regulator views pattern |
| 02 | [The Algorithmic Impact Assessment — Canadian AIA Shape](02-algorithmic-impact-assessment-canadian-aia.md) | Directive on Automated Decision-Making; four impact levels; scored, publish-by-default questionnaire; canonical-to-AIA mapping |
| 03 | [The Fundamental-Rights Impact Assessment — EU AI Act Article 27](03-fundamental-rights-impact-assessment-eu-article-27.md) | Article 27 scoping filter; six required elements; Article 13 provider-info dependency; market-surveillance notification |
| 04 | [The Data-Protection Impact Assessment — GDPR Article 35 and Its Overlap With the FRIA](04-data-protection-impact-assessment-gdpr-article-35.md) | Article 35 trigger; WP 248 nine-criteria filter; four required elements; DPO and Article 36 prior consultation; DPIA / FRIA overlap |
| 05 | [Sector-Specific Impact Assessments — The FDA Good ML Practice Slice](05-sector-specific-impact-assessment-fda-gmlp.md) | Horizontal-plus-vertical model; ten GMLP guiding principles; pre-market-submission evidence shape; analyst / regulatory-affairs boundary |
| 06 | [Model Cards — Mitchell et al. (2019), Hugging Face, and the Google Model Card Toolkit](06-model-cards-mitchell-hf-mct.md) | Nine Mitchell sections; intersectional evaluation; HF and MCT publication surfaces; internal template supersession; vendor supplement pattern |
| 07 | [System Cards and Datasheets for Datasets](07-system-cards-and-datasheets.md) | System-card extra sections (composition, safety-eval coverage, change-management triggers); seven Gebru datasheet sections; DPIA hook on Collection Process |
| 08 | [Cross-Referencing the Impact Assessment, Model Card, and Inventory Row](08-cross-referencing-artefacts-and-walk-discipline.md) | Cross-reference block; provenance chain; six walks; six failure modes; walk cadence |

## Exercises

Hands-on prompts; solutions live in the paired `ai-governance-analyst-solutions` repository.

| # | Exercise | Estimated |
|---|---|---|
| 01 | [ISO 42005 Scaffold and Template](exercises/exercise-01-iso-42005-scaffold-and-template.md) | 2 h |
| 02 | [AIA First Draft Drill](exercises/exercise-02-aia-first-draft-drill.md) | 2 h |
| 03 | [FRIA First Draft Drill](exercises/exercise-03-fria-first-draft-drill.md) | 2 h |
| 04 | [DPIA Overlap With FRIA](exercises/exercise-04-dpia-overlap-with-fria.md) | 2 h |
| 05 | [Model Card Authoring From ML Inputs](exercises/exercise-05-model-card-authoring-from-ml-inputs.md) | 2 h |
| 06 | [Datasheet for a Dataset](exercises/exercise-06-datasheet-for-a-dataset.md) | 2 h |

## Lab

- `lab-01` — Not yet authored; scheduled for the next content cycle.

## Quiz

- Knowledge check per the curriculum plan. Not yet authored; scheduled for the next content cycle.

## Resources

Curated primary references are in [`resources.md`](resources.md).

## Prerequisites

Fluency in `mod-101` (RMF, GenAI Profile, ISO 42001), `mod-102` (intake, inventory, tier tagging), `mod-103` (risk register authoring — the MAP walk and register entries this module reuses), and `mod-104` (bias-review note, the ethical-considerations input to model cards).

## Downstream dependencies

- `mod-106-regulatory-tracking-and-jurisdictions` — the regulator-view generation in chapters 02–05 is refreshed as jurisdictions change; that tracking is `mod-106`.
- `mod-107-reading-eval-and-audit-evidence` — eval reports referenced from model card Sections 4–7 and system card Section 11 are read at depth in `mod-107`.
- `mod-108-controls-and-compliance-evidence` — the *measures* sections of the AIA / FRIA / DPIA feed the enterprise control library maintained in `mod-108`.
- `mod-109-incident-response-and-continuous-monitoring` — the review triggers and cross-reference walk on incident come from `mod-109`.
- `mod-110-communication-and-council-support` — the impact assessment is a source document for council briefings authored in `mod-110`.
- `project-101` — chains `mod-102`, `mod-103`, and this module end-to-end into a full first-year deliverable set.
