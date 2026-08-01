# Exercise 06 — Datasheet for a Dataset

**Estimated effort:** 2 hours
**Grounding chapter:** [07 — System Cards and Datasheets for Datasets](../07-system-cards-and-datasheets.md)

## Objective

Author a Gebru et al. (2018)-shaped datasheet for an enterprise-controlled dataset — an evaluation set, a retrieval-augmentation index, a fine-tuning corpus, or a feature store — that is legible to a downstream user deciding whether to use the dataset for a specific purpose. The drill covers all seven Gebru sections, the analyst / data-owning-team division of labour, the DPIA hook on the Collection Process section, and the should-not-be-used-for discipline on the Uses section.

After this exercise you should be able to author a datasheet in an afternoon for any enterprise-controlled dataset, correctly refuse to author one for vendor-controlled training data (you cite the vendor's datasheet, if any, or file the gap), and defend the datasheet as an audit-facing artefact when the DPIA cites it in Article 35(7)(a).

## Prerequisites

- Chapter 07 read; the seven Gebru sections, the DPIA hook on Section 3, and the should-not-be-used-for framing on Section 5 fresh in memory.
- Chapter 06 read — the model card cites the datasheet in Sections 5 and 6, so you know where the datasheet is consumed.
- The [Gebru et al. (2018) "Datasheets for Datasets"](https://arxiv.org/abs/1803.09010) paper open — the paper's appendix lists roughly fifty questions grouped into the seven sections; you follow that structure.
- Optional: the [Hugging Face dataset-cards documentation](https://huggingface.co/docs/hub/datasets-cards) as a publication-surface reference; the Hugging Face format is loosely aligned with Gebru.
- Optional: the [Google Data Cards Playbook](https://sites.research.google/datacardsplaybook/) as an alternative shape reference (the Data Card is broader than the Gebru datasheet; the analyst chooses per use case).
- Optional: a published datasheet as a shape reference — for example, the [PhysioNet MIMIC-IV datasheet](https://physionet.org/content/mimiciv/2.2/) style, or any datasheet published under Hugging Face's data-cards format for a well-known dataset.

## Problem statement

The deliverable is two Markdown files.

### Part 1 — the datasheet

Author `mod-105-ex-06-datasheet-<dataset>.md` for a dataset of your choice.

Pick the dataset:

- **Default.** The MCDA retrieval-augmentation index described in chapter 07 — a curated corpus of past enterprise marketing campaigns used for RAG grounding.
- **Alternatives.** An evaluation set the enterprise curated (a labelled test set with the ML team's ground truth); a fine-tuning corpus (if your enterprise fine-tunes a base model); a classical-ML feature store; a synthetic-data-augmented training slice.

Constraints: the dataset must be *enterprise-controlled*. Datasets belonging to a vendor or third party are out of scope for this exercise — for those you would cite the vendor's datasheet (or file the missing-vendor-datasheet gap in the register) rather than author one.

Cover all seven Gebru sections, in order, populated:

- **1. Motivation.** Why was the dataset created; who funded / commissioned it; who created it; any specific gap it fills.
- **2. Composition.** What the instances are; how many; representativeness; sensitive attributes present or excluded; label taxonomy if labelled.
- **3. Collection Process.** How data was acquired; who collected; when; consent status (or the reason personal-data consent is not applicable); ethical-review status if relevant.
- **4. Preprocessing / Cleaning / Labeling.** What preprocessing was done; whether raw data is preserved; software used; label-conflict resolution process if labelled.
- **5. Uses.** What the dataset has been used for; what it should not be used for; whether it has been used for tasks with reported harms; the intended-use constraint.
- **6. Distribution.** How the dataset is shared (internally-only, restricted-tier, licensed-external); license or access terms; restrictions; third-party IP embedded, if any.
- **7. Maintenance.** Who maintains; contact; update cadence; erratum policy; whether the dataset will be updated; retention and end-of-life plan.

At the head, place the cross-reference block from chapter 08. Add the datasheet's own identifier and version. Cite the model card(s) and the impact assessment(s) that consume the dataset.

### Part 2 — the DPIA-hook and register-hook note

Author `mod-105-ex-06-datasheet-consumption-notes-<dataset>.md` — one page — that walks:

- **The DPIA hook on Section 3.** If the dataset contains personal data, state the Article 6 (and Article 9 if applicable) lawful basis for the collection, cite the DPIA that carries the necessity-and-proportionality argument, and note the datasheet's role as evidence for Article 35(7)(a). If the dataset contains no personal data, state that explicitly with the reason.
- **The should-not-be-used-for stance on Section 5.** Enumerate at least three uses the dataset should not be put to and one line each on why. Route this to the register — if a colleague on a future project tries to use the dataset for one of the enumerated should-not uses, is there a mechanism (access restriction, review gate, register entry) that catches them?
- **The Section 7 update-cadence hook.** Name the maintenance cadence (monthly, per-training-cycle, event-triggered) and the review trigger that forces a datasheet revision (data-source added, retention policy changed, sensitive-attribute newly detected, etc.).
- **The vendor-datasheet gap-filing pattern.** For each vendor-controlled dataset your system depends on that lacks a published vendor datasheet, name the dataset, the vendor, and the register entry ID (or `TBD-<placeholder>`) that files the gap.

## Requirements

- **All seven Gebru sections are present**, in order, labelled, and populated. No section is *TBD*; a section legitimately not-applicable is populated with an explicit *Not applicable — [one-line reason]*.
- **Section 3 (Collection Process) resolves consent and lawful-basis status.** For personal-data datasets, cite the Article 6 (and Article 9 if applicable) basis. For non-personal-data datasets, state that fact with the reason.
- **Section 5 (Uses) includes at least three should-not-be-used-for entries.** *Should not be used for X* is a first-class deliverable, not a footnote.
- **Section 7 (Maintenance) carries a specific update cadence and a maintainer contact.** No *ad hoc* cadence and no *TBD* contact.
- **The cross-reference block resolves.** Every artefact cited by identifier is real (in the enterprise) or marked `TBD-<placeholder>` with a note.
- **The consumption-notes file names DPIA hooks explicitly.** If the dataset feeds a system with a DPIA, the datasheet's role in Article 35(7)(a) evidence is stated.
- **Nothing is fabricated.** No invented dataset instance counts; no invented collection-consent statements; no invented vendor names or datasheet URLs. Where a fact is unknown (e.g., the exact retrieval-index size at a given date), note *pending data-owning-team confirmation* and file the follow-up.

## Starter guidance

- Section 3 (Collection Process) is the section where most first-draft datasheets are shallowest, especially for datasets assembled from internal enterprise data. The failure mode: writing *collected from internal systems* and stopping. Push harder — which internal systems, whose approval, what consent-status inheritance from those systems, what happens on data-subject deletion requests to the source systems.
- Section 5 (Uses) is the section most cited by future project owners. Author the *should not be used for* sub-field as if a future colleague will hit it in six months when they try to reuse the dataset. The specifics matter — *should not be used as a general-purpose training set*, *should not be used across product lines*, *should not be used for regulated-domain content generation* are all distinct constraints.
- On Section 2 (Composition), the *sensitive attributes present* sub-field is where datasheets over-promise or under-promise. Under-promising ("no sensitive attributes") is the more common failure — the analyst asks: is `postal code` present? `job title`? `product-purchase pattern`? Many fields that are not directly sensitive are proxies for sensitive attributes. Note them.
- On Section 6 (Distribution), if the dataset is internal-only, state that explicitly. If access is tiered, describe the tiers. If the dataset is licensed out, state the license.
- Section 7 (Maintenance) is where datasheets go stale. The maintenance cadence commits the data-owning team to a review moment; the analyst does not commit the ML team to something the team has not agreed to. If the data-owning team has not committed to a cadence, note the gap and file it — do not invent a cadence.
- For vendor-controlled training data on hosted foundation models, do not author a datasheet — cite the vendor's, if published. If none is published, file the gap. The register-entry pattern from `mod-103` is where the gap lives.

## Acceptance criteria

- `mod-105-ex-06-datasheet-<dataset>.md` with the cross-reference block and all seven Gebru sections populated.
- Section 3 resolves consent and lawful-basis status.
- Section 5 includes at least three should-not-be-used-for entries.
- Section 7 carries a specific update cadence and maintainer contact.
- `mod-105-ex-06-datasheet-consumption-notes-<dataset>.md` walks the DPIA hook, the should-not-be-used-for register mechanism, the update-cadence hook, and the vendor-datasheet gap pattern.
- No fabricated instance counts, consent statements, vendor URLs, or maintainer names.

## Stretch goals

- **A Hugging Face dataset-card front-matter.** Render the datasheet's header as a Hugging Face dataset-card YAML front-matter block, so the same underlying content can be published on a Hugging Face dataset page if warranted. The `annotations_creators`, `language_creators`, `language`, `license`, `size_categories`, and `task_categories` fields are the load-bearing ones.
- **A programmatic datasheet-generation approach.** Sketch (in pseudocode) how a datasheet could be auto-populated from a data-catalog entry. Which fields are safely auto-populatable (instance count, schema, last-updated timestamp) and which require human authorship (motivation, should-not-be-used-for, ethical considerations).
- **A cross-dataset lineage note.** For a dataset derived from another dataset (e.g., a fine-tuning corpus filtered from a raw corpus), author the lineage — parent dataset ID, derivation transformation, differences from the parent's Section 2 composition. Route to `mod-107` where eval-and-audit lineage lives.
- **A retention-schedule-and-erratum-policy sub-artefact.** Author the shape of the erratum policy Section 7 references — how the data-owning team publishes an erratum, how downstream consumers of the dataset are notified, how the datasheet version bumps.
- **A dataset-lint script.** Write a short Python or shell script that reads a datasheet Markdown file and reports missing sections, `TBD` markers, and empty *should not be used for* entries. This is the mechanical enforcement of the datasheet discipline.

## Deliverables

- `mod-105-ex-06-datasheet-<dataset>.md` — the datasheet.
- `mod-105-ex-06-datasheet-consumption-notes-<dataset>.md` — the DPIA-hook and register-hook note.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference datasheet against the MCDA retrieval-augmentation index. Yours will differ in the specific composition and use-case content; what should not differ is (a) all seven Gebru sections are populated, (b) Section 3 resolves consent and lawful-basis status honestly, (c) Section 5 carries at least three should-not-be-used-for entries, (d) Section 7 carries a real cadence and a real contact, (e) the DPIA hook is stated explicitly. A short datasheet that honestly names three *should not be used for* constraints and files a maintainer contact beats a longer one that hand-waves *see internal data catalog* on Section 3 or leaves Section 7 undated.
