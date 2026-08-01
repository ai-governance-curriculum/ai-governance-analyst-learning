# Exercise 05 — Model Card Authoring From ML Inputs

**Estimated effort:** 2 hours
**Grounding chapter:** [06 — Model Cards — Mitchell et al. (2019), Hugging Face, and the Google Model Card Toolkit](../06-model-cards-mitchell-hf-mct.md)

## Objective

Author a first-draft enterprise model card following the Mitchell et al. (2019) nine sections, populating the analyst-tier sections yourself and coordinating with the ML team on the model-behaviour and evaluation-evidence sections through a structured input request. The drill covers the nine sections, the analyst / ML division of labour, the Hugging Face vs Google Model Card Toolkit publication choice, and the internal-supersedes rule for enterprise-supplement cards over vendor-hosted models.

After this exercise you should be able to author a model card in an afternoon, hand a specific and answerable input request to the ML team, and produce an enterprise supplement to a vendor-supplied card that is legible to a downstream deployer without duplicating vendor content.

## Prerequisites

- Chapter 06 read; the nine Mitchell sections, the analyst / ML split, the two publication surfaces, and the internal-supersedes rule fresh in memory.
- Chapter 07 skimmed — the system-card extension and the datasheet reference are useful context but not the deliverable here (exercise 06 covers the datasheet).
- Exercise 01 completed — you have a canonical document for the same system.
- The [Mitchell et al. (2019) "Model Cards for Model Reporting"](https://arxiv.org/abs/1810.03677) paper open — you will cite the nine sections by name and follow the paper's intersectional-evaluation framing in section 7.
- The [Hugging Face model-cards documentation](https://huggingface.co/docs/hub/model-cards) open — the YAML metadata block and the standard body headings are the shape reference for a Hugging Face-published card.
- Optional: the [Google Model Card Toolkit](https://github.com/tensorflow/model-card-toolkit) if you have a TF pipeline; otherwise skip.
- Reference: a small set of published vendor and enterprise model cards. The [Meta Llama 3.1 model card](https://github.com/meta-llama/llama-models/blob/main/models/llama3_1/MODEL_CARD.md), the [Google Gemma model card](https://ai.google.dev/gemma/docs/model_card), and the [Anthropic Claude 3 model card](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Model_Card_Claude_3.pdf) are useful shape exemplars.

## Problem statement

The deliverable is three Markdown files.

### Part 1 — the enterprise model card

Author `mod-105-ex-05-model-card-<system>.md` for a system of your choice.

Pick the use case:

- **Default.** The MCDA enterprise supplement described in chapter 06 — a supplement to Vendor V's hosted-model card, covering the enterprise's specific deployment.
- **Alternative.** A card for an internally-trained model (e.g., a classical-ML classifier the enterprise trains against enterprise data). The nine-section shape and the analyst / ML split still apply; you will populate more of the Section 4–7 content yourself because there is no vendor to defer to.

Cover all nine Mitchell sections, in order, labelled and populated:

- **1. Model Details.** Analyst-tier. Populate from canonical document header + intake row.
- **2. Intended Use.** Analyst-tier. From MAP 1.1 and MAP 3.3. Include *out-of-scope use cases* explicitly.
- **3. Factors.** Co-owned. Analyst identifies factors relevant from the affected-population inventory; ML team confirms technical availability.
- **4. Metrics.** ML-tier. In the enterprise-supplement pattern, cite by reference to the eval report; do not restate.
- **5. Evaluation Data.** ML-tier. Cite by reference.
- **6. Training Data.** ML-tier. For vendor-hosted models, cite the vendor card and note the deployer-scope opacity.
- **7. Quantitative Analyses.** ML-tier. Cite by reference. Note the intersectional-analysis requirement — a card that lacks per-factor-combination results is under-evidenced.
- **8. Ethical Considerations.** Analyst-tier. From the register entries and the FRIA / DPIA / AIA where applicable.
- **9. Caveats and Recommendations.** Co-owned.

At the head, place the cross-reference block from chapter 08 and add the model card's own identifier and version. If the card is a supplement, cite the vendor card explicitly as MC-XXX-XXXX-Vendor and this document as MC-XXX-XXXX-Enterprise.

At the tail, add:

- The Hugging Face YAML metadata block that would front-matter the same card if published on Hugging Face. Include at minimum `license`, `datasets` (by identifier), `language`, `pipeline_tag`, `tags`, and one `model-index` entry per cited eval-report metric.
- A short *publication-surface note* — three or four sentences — that names whether this card would be published on Hugging Face, rendered via the MCT, kept internal, or all three, with the reason.

### Part 2 — the input-request memo to the ML team

Author `mod-105-ex-05-ml-input-request-<system>.md` — a structured request to the ML team for the Section 4–7 content the analyst does not author. Shape:

- **Cross-reference block** — the canonical document, register entries, the model card ID.
- **Section 4 (Metrics) request.** Enumerate the metrics the analyst wants captured on the eval report, the decision thresholds, and the variation approach (confidence intervals, bootstrap, etc. — name what you want, do not accept "we'll do what we normally do").
- **Section 5 (Evaluation Data) request.** The eval-set description the analyst needs, including sampling method and any factor-based stratification.
- **Section 6 (Training Data) request.** For internally-trained models, the training-data-provenance request. For vendor-hosted models, note that this section is populated from the vendor card.
- **Section 7 (Quantitative Analyses) request.** The intersectional-analysis requirement made specific — which factor-combinations the analyst needs surfaced (per-language, per-product-line, per-tenure-band, whatever applies) and why.
- **A response-deadline and a hand-back format** — the analyst asks for a specific artefact (a Markdown fragment, a JSON payload conforming to the MCT schema, a TFMA output link) with a specific timeline.
- **A sign-off request.** The ML team lead signs off on the Section 4–7 content when it lands in the card.

### Part 3 — the internal-vs-external rendering note

Author `mod-105-ex-05-rendering-note-<system>.md` — one page — that walks:

- What is in the *internal* card but not the *external* card. Enterprise fields — inventory row IDs, register entry IDs, vendor review IDs, DPIA / FRIA / AIA IDs, sign-off block — do not travel to the external card.
- What is in the *external* card but not the *internal* card. Nothing should be — the internal is a superset per chapter 06. Assert this rule and check your card against it.
- The rendering step — literal or conceptual — that produces the external card from the internal one. If the enterprise has a `render-card` script, name the fields it drops; if not, name the manual redactions.
- The publication decision — whether this card is being externally published this cycle, and if so, on which surface (Hugging Face public / private, MCT-rendered internal only, enterprise governance portal, etc.).

## Requirements

- **All nine Mitchell sections are present**, in order, labelled, and populated. No section is *TBD*; a section legitimately owned by the ML team is populated *by reference* to the eval report or vendor card, not left blank.
- **Section 2 (Intended Use) includes an explicit *out-of-scope use cases* sub-field.** A card without this sub-field is a marketing page.
- **Section 3 (Factors) is real.** *No relevant factors* is only a valid answer if the enterprise has demonstrably established there are none; the affected-population inventory should have given you at least one factor to name.
- **Section 7 (Quantitative Analyses) cites intersectional results, not just per-group.** The input-request memo asks for intersectional results specifically.
- **Section 8 (Ethical Considerations) cross-references the impact assessment.** Register entries are named by identifier; the FRIA / DPIA / AIA IDs are cited.
- **The Hugging Face YAML block is syntactically valid** — even if the card is not published there, the block should parse.
- **The input-request memo is answerable.** The ML team should be able to read it, produce the requested content, and hand it back without a follow-up meeting. Requirement: each Section 4–7 request specifies (a) the metric or artefact, (b) the format expected, (c) the deadline, (d) the sign-off contact.
- **The internal card is a superset of the external card.** No external field is absent from the internal card. Assert this explicitly in the rendering note.
- **Nothing is fabricated.** No invented eval numbers; no invented vendor card URLs; no invented sign-off names. Where a Section 4–7 field cannot be populated because the eval has not been run, cite `pending EV-XXX-XXXX` — the eval report identifier and status.

## Starter guidance

- Author Section 8 (Ethical Considerations) first if you have the register entries in front of you. It is the section most analysts leave until last; authoring it first forces you to notice which register entries need model-card-facing framing they do not currently have.
- On Section 2, the trap is to author intended use as a marketing statement. The Mitchell paper's framing is closer to a legal warranty: what the model was built for, what users, what deployment settings — and, explicitly, what it was *not* built for. Follow that framing.
- The input-request memo should read like a spec, not like a request for effort. Tell the ML team what you need in the format you need it. *We usually just chat about it* is how model cards drift; a written request is how they do not.
- On the Hugging Face YAML block, the `model-index` array is the load-bearing field for governance-side reading. Each entry is a claim under evidence — dataset, metric, value. If your ML team cannot yet populate a `model-index` entry, the eval report is not yet in a shape a model card can honestly cite.
- On the internal-vs-external rendering, resist the urge to make the external card richer than the internal. That is a common failure mode when the analyst writes the external card first for a publication deadline and back-fills the internal one. Reverse the order: internal is source; external is derived.
- If the system is vendor-hosted, keep the enterprise supplement short — 1000 to 1500 words. Longer supplements are usually retreading vendor content. Cite the vendor card and stop.

## Acceptance criteria

- `mod-105-ex-05-model-card-<system>.md` with cross-reference block, all nine Mitchell sections, Hugging Face YAML block, and publication-surface note.
- Section 2 includes out-of-scope use cases; Section 3 includes at least one factor; Section 7 cites intersectional results (or names the gap).
- Section 8 cross-references the impact assessment and register entries by identifier.
- `mod-105-ex-05-ml-input-request-<system>.md` with cross-reference block and per-section Section 4–7 requests specifying artefact, format, deadline, sign-off contact.
- `mod-105-ex-05-rendering-note-<system>.md` walking internal-vs-external content, the rendering step, and the publication decision.
- The internal card is asserted as a superset of the external card.
- No fabricated eval numbers, vendor URLs, or sign-off names; unpopulated fields cite pending artefacts by identifier.

## Stretch goals

- **A programmatic MCT skeleton.** Populate the [Google Model Card Toolkit](https://github.com/tensorflow/model-card-toolkit) `ModelCard` proto for the same system in Python. The auto-populated sections are Sections 4–7 from a TFMA output; the manually-authored sections are the analyst-tier ones. Note where the schema is under-expressive for the enterprise-specific fields — that is the case for the internal-supersedes rule.
- **A vendor-card diff artefact.** For a hosted vendor model, take the vendor card verbatim and produce a diff showing what the enterprise supplement adds. The diff is the analyst's justification for the supplement's existence.
- **A model-card update-trigger checklist.** From chapter 06's *change-management triggers* framing, list the triggers that would force a re-render of the model card (base-model version change, prompt-template major rev, tool-inventory change, eval-report re-run, incident logged, etc.). Route the checklist to `mod-109` where incident-triggered updates live.
- **A downstream-deployer-facing FAQ.** If the enterprise's model is consumed by other internal teams as a service, author a short FAQ that surfaces the model card's Section 2 (intended use) and Section 8 (ethical considerations) content in a form a consuming team can actually read. This is preview work for `mod-110` communication scope.
- **A card-drift lint script.** Write a short Python or shell script that reads the internal and external cards and reports fields present in the external but absent from the internal. This is the mechanical enforcement of the internal-supersedes rule.

## Deliverables

- `mod-105-ex-05-model-card-<system>.md` — the enterprise model card.
- `mod-105-ex-05-ml-input-request-<system>.md` — the ML team input request memo.
- `mod-105-ex-05-rendering-note-<system>.md` — the internal-vs-external rendering note.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference card against the MCDA enterprise supplement. Yours will differ in the specific intended-use narrative and ethical-considerations content; what should not differ is (a) all nine Mitchell sections are populated, (b) Section 2 has out-of-scope use cases, (c) Section 7 addresses intersectional analysis, (d) Section 8 cross-references the impact assessment, (e) the ML input-request memo is answerable, (f) the internal card is a superset of any external rendering. A clean 1200-word supplement that cites the vendor card and defers gracefully to the eval report beats a longer one that quietly restates vendor content or invents metrics.
