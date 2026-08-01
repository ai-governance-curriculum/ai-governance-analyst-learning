# System Cards and Datasheets for Datasets

## Why this chapter

The model card in chapter 06 describes a *model*. The two artefacts in this chapter describe the pieces around it:

- The **system card** describes the whole deployed system — model plus prompts plus tools plus guardrails plus operating context — because a modern AI system is more than the underlying model. Public examples from foundation-model providers (OpenAI, Anthropic, Meta) have popularised the shape.
- The **datasheet for a dataset** describes the data — how it was collected, who it represents, what motivated its creation, what limitations it carries — as an independent artefact so a downstream user of the dataset can decide whether to use it.

The analyst needs both. The FRIA cites the system card when the model card alone would under-describe the risk. The DPIA cites the datasheet when the training-data description is load-bearing. The impact assessment is only as evidenced as its downstream artefacts.

This chapter walks the system-card shape (Mitchell et al. re-extended plus what OpenAI / Anthropic publications have converged on), the [Gebru et al. (2018) datasheet](https://arxiv.org/abs/1803.09010), and the analyst / ML team division of labour on each.

## System cards — why the model card is not enough

A system card exists because *the deployed system is not the model*. A modern AI application typically composes:

- A base model (often a hosted foundation model).
- A prompting layer with structured templates and safety instructions.
- Retrieval-augmented context injection.
- Tool-use / function-calling with an enumerated tool inventory.
- Post-generation filters and guardrails.
- An orchestration layer with rate limits, session state, and audit logging.
- A user-facing surface with human-in-the-loop controls.

Any of the seven can shift the residual risk more than a change to the base model would. A well-authored model card cannot describe this composition; the system card is where it goes.

The public exemplars — the [OpenAI GPT-4 System Card (2023)](https://cdn.openai.com/papers/gpt-4-system-card.pdf), the [OpenAI GPT-4V(ision) System Card (2023)](https://cdn.openai.com/papers/GPTV_System_Card.pdf), the [OpenAI o1 System Card (2024)](https://cdn.openai.com/o1-system-card-20241205.pdf), and Anthropic's [Claude 3 Model Card and Evaluations (2024)](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Model_Card_Claude_3.pdf) — are model-*and*-system hybrids. The load-bearing sections common across them:

- **Model overview** and safety training summary.
- **Evaluation coverage** — capability evaluations plus safety evaluations plus red-team findings, with named eval suites.
- **Known limitations and observed harms** — a candid catalogue with cited incidents where relevant.
- **Mitigations applied** — a description of policy training, refusal training, red-team-driven fixes, and system-level guardrails.
- **Deployment considerations** — recommendations for downstream deployers, including gating and human oversight.

<!-- needs-research: verify current published version identifiers and URLs for OpenAI and Anthropic system cards before citing in an audit-facing artefact; system-card URLs change as new model versions are released and older cards are superseded or moved. -->

## System cards at internal scale

The public system cards are hundreds of pages and are the output of large in-house safety programmes. Internal enterprise system cards are much smaller — perhaps 5–15 pages — and pull only what a downstream deployer or reviewer needs.

The internal shape most enterprises settle into extends the Mitchell nine-section model card with three additional sections:

- **10. Composition and Deployment Context.** What sits between the model and the user. Prompt templates and their version; retrieval indices and their scope; tool inventory and permissions; guardrails and their configuration; the deployment surface.
- **11. Safety Evaluation Coverage.** Which safety evals ran; which did not; red-team findings summary; refusal-behaviour findings.
- **12. Change-Management Triggers.** When the system card is regenerated: base-model version change; prompt-template major rev; tool-inventory change; guardrail configuration change; incident-response event.

Section 10 is the load-bearing one. A change to the retrieval index scope or a change to the tool inventory can shift the FRIA-relevant risk without any change to the model. The system card is where that story lives.

## Analyst-tier expectations on the system card

The analyst-tier division of labour extends chapter 06:

- **Section 10 (Composition and Deployment Context).** The *inventory* of prompts, tools, and retrieval indices is authored by the ML / platform team; the *deployment context* narrative is authored by the analyst from MAP 1.1 and MAP 3.3.
- **Section 11 (Safety Evaluation Coverage).** The ML / safety team owns; analyst reads (see `mod-104` and `mod-107`).
- **Section 12 (Change-Management Triggers).** Analyst authors from the enterprise change-management policy plus the register-entry change triggers.

The Mitchell 1–9 sections are extended, not replaced. A system card is not a replacement for the model card; it is a supplement that sits alongside it, with the composition and deployment story.

## Datasheets for datasets

Where the model card describes the model and the system card describes the system, the [Gebru et al. (2018) datasheet](https://arxiv.org/abs/1803.09010) describes the data. The paper enumerates roughly fifty questions grouped into seven sections:

1. **Motivation.** Why was the dataset created; who funded it; who created it.
2. **Composition.** What the instances are; how many; representativeness; sensitive attributes present.
3. **Collection Process.** How data was acquired; who collected; when; consent status; ethical review.
4. **Preprocessing / Cleaning / Labeling.** What preprocessing was done; whether raw data is preserved; software used.
5. **Uses.** What the dataset has been used for; what it should not be used for; whether it has been used for tasks with reported harms.
6. **Distribution.** How the dataset is shared; license; restrictions; whether third-party IP is embedded.
7. **Maintenance.** Who maintains; contact; update cadence; erratum policy; whether the dataset will be updated.

The load-bearing analyst-tier points:

- **Section 3 (Collection Process)** is where consent-status and lawful-basis claims for the training data live. This is a DPIA-relevant field for any personal-data dataset.
- **Section 5 (Uses)** — the *should-not-be-used-for* sub-field — is the datasheet's parallel to the model card's *out-of-scope use cases*. Enterprises are under-populating this field almost universally.
- **Section 7 (Maintenance)** is where re-authoring triggers live. A dataset whose composition changes over time (a customer-interaction log, a scraped-web corpus) needs a datasheet with a live update cadence, not a snapshot.

## Datasheet applicability at deployer scope

Most enterprise governance analysts do not personally author datasheets for foundation-model *training* data — that data belongs to the vendor and is often opaque. But the analyst *does* author datasheets for:

- **Evaluation datasets** the enterprise curates for its own eval pipeline.
- **Retrieval-augmentation indices** — the corpus the RAG system retrieves from.
- **Fine-tuning datasets** where the enterprise fine-tunes a base model.
- **Feature stores** feeding classical-ML systems in the enterprise.

For vendor-supplied datasets or vendor-hosted foundation models, the analyst *reads* the vendor's datasheet (if published) and files it alongside the vendor's model card. Missing vendor datasheets are noted as evidence gaps in the register.

## Analyst-tier expectations on the datasheet

- **Motivation.** Analyst authors from intake and the risk register.
- **Composition.** Data-owning team authors; analyst reviews for affected-population coverage and sensitive-attribute inventory.
- **Collection Process.** Data-owning team authors; analyst reviews for consent status and lawful basis.
- **Preprocessing.** Data-owning team owns; analyst reads.
- **Uses.** Analyst authors from the register — reused with the model card's out-of-scope field.
- **Distribution.** Legal and data-owning team own.
- **Maintenance.** Analyst authors the review cadence; data-owning team commits to it.

## Concrete example — the MCDA datasheet slice

MCDA's retrieval-augmentation index is a curated corpus of past enterprise marketing campaigns. That corpus needs a datasheet.

- **Motivation.** Corpus assembled to ground draft outputs in prior enterprise voice and prior product statements. Assembled by Marketing Data Platform team in early 2026.
- **Composition.** ~4,200 past-campaign records, each with a structured brief and the final approved copy. No personal data; no customer-identifying fields. Contains one class of proprietary business information (product-launch dates prior to public announcement) with an access restriction on the index tier.
- **Collection Process.** Records pulled from enterprise campaign-management system with the Marketing Ops owner's approval. No third-party data acquisition. No individual data-subject consent required as no personal data is processed.
- **Preprocessing.** Free-text campaign notes normalised to a per-record schema; product-launch-date sensitivity tags added; records prior to 2022 excluded on relevance grounds.
- **Uses.** Retrieval grounding for MCDA and no other purpose. Should not be used as a general-purpose training set; should not be redistributed outside the enterprise.
- **Distribution.** Not distributed. Access restricted to MCDA runtime service principal.
- **Maintenance.** Marketing Data Platform team maintains; monthly refresh; any campaign added to the enterprise campaign-management system enters the index within 24 hours; records removed on retention-schedule expiry.

The datasheet lands as a related-artefact reference in the MCDA canonical document and is cross-referenced by the enterprise model card supplement.

## What analyst-tier system-card and datasheet work is *not*

- **Not a red-team report.** Section 11 of the system card *references* the red-team findings; it does not reproduce them. Red-team methodology is `ai-red-team-engineer` scope.
- **Not a data-quality audit.** Section 4 of the datasheet describes preprocessing; a full data-quality audit is out of scope for analyst-tier work.
- **Not the model provenance file.** Enterprises with mature ML platforms maintain a per-model provenance file (training-run identifier, data snapshot IDs, hyperparameter set). That file is ML-platform scope; the model card and datasheet reference it.
- **Not a replacement for the vendor artefact.** For hosted vendor systems, the enterprise supplements the vendor's card; it does not replace it.

## What to memorise

- **The three-artefact family** — model card (chapter 06), system card (this chapter, sections 1–12), datasheet for a dataset (this chapter).
- **The extra system-card sections** — Composition and Deployment Context, Safety Evaluation Coverage, Change-Management Triggers.
- **The seven datasheet sections** — Motivation, Composition, Collection, Preprocessing, Uses, Distribution, Maintenance.
- **The DPIA hook on Collection Process** — datasheet Section 3 is where the training-data lawful basis lives.
- **The should-not-be-used-for discipline** — datasheet Section 5 and model card Section 2, both under-populated.

## Summary

The system card supplements the model card by describing the composition of the deployed system — prompts, retrieval, tools, guardrails, deployment surface — because a change to any of those can shift risk more than a change to the base model. The [Gebru et al. (2018) datasheet](https://arxiv.org/abs/1803.09010) supplements both by describing the data that trained, evaluated, or grounds the model. Analyst-tier work on the system card covers the deployment-context sections and the change-management triggers; on the datasheet, motivation, uses, and maintenance cadence. For vendor-hosted models, the enterprise reads the vendor's system card and datasheet where published, cites them, and files the gaps as evidence gaps in the register.
