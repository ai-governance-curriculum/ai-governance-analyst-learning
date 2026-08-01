# Model Cards — Mitchell et al. (2019), Hugging Face, and the Google Model Card Toolkit

## Why this chapter

The model card is the analyst's second most-cited artefact after the impact assessment itself. It sits at the boundary between the ML team and everyone else — governance, procurement, legal, downstream deployers, external auditors — and its job is to give a non-model-developing reader enough information to decide whether the model is fit for a specific purpose.

Model cards do not automate governance. A well-authored card *makes an argument* about intended use, in-distribution performance, out-of-distribution behaviour, evaluation coverage, and known limitations, and cites the evidence for each claim. A badly-authored card is a marketing page.

This chapter walks the [Mitchell et al. (2019) — "Model Cards for Model Reporting"](https://arxiv.org/abs/1810.03677) sections, the two dominant publication surfaces (Hugging Face format and Google Model Card Toolkit), when an internal template supersedes both, and the analyst / ML team division of labour.

## The Mitchell et al. sections

The [original paper](https://arxiv.org/abs/1810.03677) enumerates nine sections. Every model card the analyst produces or reviews should have all nine — filled or explicitly marked *not applicable* with a reason.

1. **Model Details.** Person or organisation developing the model, model date, model version, model type, information about training algorithms/parameters, paper or resource for more information, citation details, license, where to send questions.
2. **Intended Use.** Primary intended uses; primary intended users; out-of-scope use cases.
3. **Factors.** Relevant factors (groups, instrumentation, environments); evaluation factors.
4. **Metrics.** Model performance measures; decision thresholds; variation approaches.
5. **Evaluation Data.** Datasets used; motivation for choosing; preprocessing.
6. **Training Data.** Same three fields as Evaluation Data.
7. **Quantitative Analyses.** Unitary results (per-metric); intersectional results (per-metric per-factor-combination).
8. **Ethical Considerations.** Data reflects any sensitive attributes; risks and harms; use cases the model should not be used for; mitigation strategies.
9. **Caveats and Recommendations.** Additional context not previously covered.

The paper's load-bearing framing is that **intersectional evaluation is not optional**. Section 7 explicitly requires per-factor-combination performance — not just per-group. A model with 95% accuracy overall may have 60% accuracy on group A × environment X; the intersectional table is where that surfaces. Chapters 01–02 of `mod-104` are the analyst's grounding on reading these tables.

## Analyst-tier expectations per section

The analyst does not author every section. The rough division of labour:

- **Model Details.** Analyst can populate from intake and vendor documentation. The load-bearing analyst check is that the *version* is unambiguous — a card citing "GPT-4" without a version pin is under-specified.
- **Intended Use.** Analyst authors from the MAP 1.1, MAP 3.3 narrative. The *out-of-scope use cases* sub-field is the one under-populated in first drafts; force it.
- **Factors.** Analyst identifies relevant factors from the affected-population inventory; ML team confirms which are technically available in the data.
- **Metrics.** ML team owns.
- **Evaluation Data / Training Data.** ML team owns; analyst reads.
- **Quantitative Analyses.** ML team runs; analyst reads (see `mod-104`).
- **Ethical Considerations.** Analyst authors from the register entries and the FRIA / DPIA. This is the section where the *impact assessment* and the *model card* most closely converge.
- **Caveats and Recommendations.** Both — analyst adds governance-side caveats; ML team adds technical ones.

The rule of thumb: **analyst-tier sections are 1, 2, 3, 8, 9 (partially). ML-team-tier sections are 4, 5, 6, 7. Section 3 is co-owned.**

## Hugging Face model-card format

[Hugging Face](https://huggingface.co) — the largest public model-hosting platform — has adopted the Mitchell framing and standardised a [model-card format](https://huggingface.co/docs/hub/model-cards) implemented as a YAML metadata block plus Markdown body. The [model-card creator tool](https://huggingface.co/spaces/huggingface/Model_Cards_Writing_Tool) generates skeletons from a form; the [Hub Python library](https://huggingface.co/docs/huggingface_hub/how-to-manage#create-a-model-card) has a `ModelCard` class for programmatic authoring.

The YAML metadata front-matter fields relevant to governance-side reading:

- `license` — SPDX identifier plus optional custom clauses.
- `datasets` — datasets used in training / evaluation, each linkable to its own dataset card (chapter 07).
- `language` — languages supported.
- `pipeline_tag` — task category (text-generation, image-classification, etc.).
- `tags` — free-form labels.
- `model-index` — structured evaluation-result claims: dataset, metric, value. Read this as a claim under evidence; the model card must link the eval report that backs each entry.

The Markdown body follows the Mitchell sections. The Hugging Face default template is loose about section names; a governance-facing card should adopt the Mitchell section headings verbatim so a reviewer can find each section by scanning.

**When the Hugging Face format is the right publication surface.** External open-weight release; academic release; internal release where the enterprise already uses a Hugging Face-compatible model store (e.g., an internal Hugging Face Enterprise hub); vendor-supplied models that the enterprise pulls from Hugging Face.

**When it is not.** A hosted-API model with no downloadable weights (Vendor V's foundation model in the MCDA example — there is nothing to publish on Hugging Face); a proprietary model with contract terms that forbid publication.

## Google Model Card Toolkit

The [Google Model Card Toolkit (MCT)](https://github.com/tensorflow/model-card-toolkit) is a Python-and-JSON tooling stack for authoring model cards programmatically. Its shape:

- A **schema** (`ModelCard` proto) that mirrors the Mitchell sections with an added structured-graphic representation for quantitative analyses.
- A **library** that populates the schema from TensorFlow Model Analysis (TFMA) evaluation output, TFX pipelines, and manual entry.
- A **template** that renders the populated card to HTML.

The programmatic authoring is the point. Where the ML team's evaluation pipeline produces TFMA output, the quantitative-analyses section populates automatically — the analyst's read is against a schema-conformant artefact, not a hand-typed page that may drift from the underlying eval results.

**When MCT is the right surface.** TensorFlow / TFX shop; regulated environment where the ML team needs the evaluation-to-card link auditable and reproducible; enterprise where a per-model card is generated on every training run.

**When it is not.** Non-TF stacks (PyTorch, JAX) — the MCT works with the schema but the auto-population from TFMA does not apply; hand-authored cards for hosted vendor models; large-language-model shops that have converged on either the Hugging Face format or an internal template.

<!-- needs-research: verify current maintenance status of the Model Card Toolkit; the repository at tensorflow/model-card-toolkit was under active development in 2020–2022 and the analyst should confirm current cadence before recommending it for a new pipeline. -->

## When an internal template supersedes both

Neither the Hugging Face format nor the MCT covers everything a well-run enterprise governance function needs on the artefact. Common enterprise additions that push the enterprise to an internal template:

- **Cross-reference block.** Explicit fields for the inventory row ID, the FRIA / DPIA / AIA IDs, the risk register entries, the vendor review ID, the eval reports, the incident-response plan. Chapter 08 develops the cross-reference discipline in depth.
- **Governance sign-off block.** Named sign-off from the risk owner, the DPO, the AI governance owner, the ML team lead. Dates.
- **Enterprise-specific fields.** Tier tag from `mod-102`; SR 11-7 tier where financial-services; FDA product code where a medical device.
- **Structured update triggers.** *This card is regenerated on: model version change, prompt template major rev, incident logged, eval report re-run, expiration date reached.*
- **Restricted-fields separation.** Some enterprise cards separate public-facing content from internal-only content in a way the Hugging Face format does not natively support.

The pattern most enterprises settle into: **an internal Markdown or JSON template that is a superset of the Hugging Face / Mitchell shape, plus a rendering step that produces the Hugging Face-shaped external card when publication is warranted.** The analyst-tier discipline: never produce an external card that has fields the internal card does not; never allow the two to drift.

## Concrete example — the MCDA model card

The MCDA (chapter 01) does not have downloadable weights — Vendor V hosts the foundation model. So the *model card* the analyst produces is an *enterprise-supplement* to the vendor-supplied card. Two artefacts:

- **Vendor V's model card** — provided by the vendor; pinned to the vendor's version identifier. Filed as MC-2026-0044-Vendor at intake.
- **Enterprise supplement MC-2026-0044-Enterprise** — the enterprise's model card that adds intended-use in the enterprise's context, factors relevant to the enterprise's use, an enterprise-specific ethical-considerations section that reuses the FRIA / DPIA content, and the cross-reference block.

The enterprise supplement's nine Mitchell sections:

- **Model Details.** Vendor V hosted model, version 2024-06, called through Vendor V API; enterprise integration owned by Marketing Data Platform team; cite the vendor's card by URL and pin the version.
- **Intended Use.** Draft marketing copy for internal copywriter review. Not intended for external release without copywriter review. Not intended for regulated-domain content (financial disclosures, clinical claims, legal notices).
- **Factors.** Product-team factor (across enterprise business units); template-version factor (v1.4 as of card date); customer-language factor (English only currently supported).
- **Metrics.** Reference to the eval report EV-2026-0091; metric definitions kept out of the card body to avoid drift.
- **Evaluation Data.** Reference to the eval-set description in EV-2026-0091.
- **Training Data.** Vendor-controlled; enterprise does not have visibility below the vendor card level.
- **Quantitative Analyses.** Reference to EV-2026-0091 tables.
- **Ethical Considerations.** Confabulation risk RR-2026-0212 with the mitigation summary; brand-voice-homogenisation risk RR-2026-0213; IP contamination risk RR-2026-0214; data-leakage risk RR-2026-0215. Cross-reference to bias-review note BR-2026-0117 (per `mod-104`).
- **Caveats and Recommendations.** Card regenerated on vendor version change, on prompt-template major rev, on incident logged. Card review annually. Enterprise consumers of the card must not extrapolate performance claims to use cases outside the intended-use section.

The card body is short — under 1500 words. The evidence lives in the cross-referenced artefacts.

## What analyst-tier model-card work is *not*

- **Not the eval report.** Sections 4, 5, 6, 7 are ML-team output. The analyst references, does not restate.
- **Not the training-data audit.** Training-data provenance is `mod-107` and `ai-evaluation-engineer` scope for internally-trained models; for vendor-hosted models, the vendor card is the source and the analyst cites it.
- **Not fitness-for-purpose approval.** The card is evidence; the fitness-for-purpose call is the risk-owner's, informed by the register and the card.
- **Not a marketing document.** A card that reads as promotional copy is not a card. Push back and rewrite.

## What to memorise

- **The nine Mitchell sections** by name and by which are analyst-tier vs ML-team tier.
- **The intersectional-evaluation requirement** in section 7 — per-factor-combination, not just per-group.
- **The two publication surfaces**: Hugging Face format for open-weight-shaped releases; MCT for TF-native pipelines.
- **The internal-supersedes rule** — an enterprise card is a superset; the external card is a rendering.
- **The vendor-supplement pattern** for hosted-API models — vendor card plus enterprise supplement, both cited in the inventory.

## Summary

The Mitchell et al. (2019) model card is the standing analyst-facing shape — nine sections covering model details, intended use, factors, metrics, evaluation and training data, quantitative analyses, ethical considerations, and caveats. Hugging Face and the Google Model Card Toolkit are the two dominant publication surfaces; an internal enterprise template usually supersedes both by adding cross-references, sign-offs, and enterprise-specific fields. Analyst-tier authoring covers intended use, factors, ethical considerations, and cross-references; the ML team owns metrics, data, and quantitative-analyses sections. For vendor-hosted models, the enterprise produces a *supplement* to the vendor card and cites both.
