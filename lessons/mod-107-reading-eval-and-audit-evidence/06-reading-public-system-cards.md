# Reading Public System Cards

## Why this chapter

`mod-105` chapter 07 introduced the system card as an artefact family and named its shape. This chapter is the reading discipline: given a specific published system card from a frontier-model vendor — an OpenAI GPT-4 or GPT-5 system card, an Anthropic Claude system card, a Google DeepMind Gemini technical report, a Meta Llama model card — what does the analyst extract, how does the analyst summarise it into a `EVAL-<year>-<sequence>` row of type *vendor-system-card*, and how does that row participate in the internal-artefact benchmark chapter 08 works?

The public cards are hundreds of pages, are the output of large in-house safety programmes, and are the closest thing in the field to a *canonical* eval-and-safety disclosure per model release. They are also the reference document a regulator, an auditor, or a governance council will cite when asking *how does our internal MCDA safety-eval compare to what the model vendor themselves published?* The analyst who has not read the card for the underlying model is not in a position to answer that question.

## The public exemplars the analyst should be able to name

Foundation-model providers have converged (loosely) on a system-card shape. The exemplars an analyst should have read at least once:

- **OpenAI GPT-4 System Card** ([2023 release, PDF](https://cdn.openai.com/papers/gpt-4-system-card.pdf)) — the first widely-cited system card; introduced the public shape of a lab-published eval-and-safety disclosure paired with a base-model release.
- **OpenAI GPT-4V(ision) System Card** ([2023, PDF](https://cdn.openai.com/papers/GPTV_System_Card.pdf)) — the modality-extended shape (multimodal capability + safety evaluation).
- **OpenAI o1 System Card** ([2024, PDF](https://cdn.openai.com/o1-system-card-20241205.pdf)) — the reasoning-model-shape, notable for its explicit chain-of-thought safety analysis and Preparedness-Framework scoring.
- **OpenAI GPT-4o System Card** ([2024, published on the OpenAI site](https://openai.com/index/gpt-4o-system-card/)) — the omnimodal-shape (text + vision + audio).
- **OpenAI o3 / GPT-4.5 / GPT-5 series system cards** — <!-- needs-research: verify the current published system-card URLs for the o3, GPT-4.5, and GPT-5 releases against the OpenAI research index (https://openai.com/research/) as system-card URLs change per release and older cards are moved or superseded. -->
- **Anthropic Claude 3 Model Card and Addendum** ([Claude 3 Model Card, PDF](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Model_Card_Claude_3.pdf)) — Anthropic's model card is the paired document to the RSP disclosure and covers evaluations, refusal behaviour, and Anthropic's Acceptable Use Policy considerations.
- **Anthropic Claude 3.5 / Claude 4 series model cards and addenda** — <!-- needs-research: verify current published model-card URLs for the Claude 3.5, Claude 4, and later Claude releases against the Anthropic model overview page (https://www.anthropic.com/claude) and Anthropic's news page (https://www.anthropic.com/news) at the date of use. -->
- **Google DeepMind Gemini technical reports** — the [Gemini 1.5 technical report (arXiv 2403.05530)](https://arxiv.org/abs/2403.05530) established a public technical-report shape for Google's model family; subsequent releases (Gemini 2.x, Gemini 3.x) follow with published technical reports. <!-- needs-research: verify current Gemini technical-report URLs (arXiv identifiers and the DeepMind publications page) at time of use. -->
- **Meta Llama model cards** — Meta publishes model cards alongside Llama releases; the shape has extended across [Llama 2](https://github.com/meta-llama/llama-models/blob/main/models/llama2/MODEL_CARD.md), [Llama 3](https://github.com/meta-llama/llama-models/blob/main/models/llama3/MODEL_CARD.md), and successor releases. <!-- needs-research: verify current Llama model-card URLs for the Llama 4 and later releases against the [Meta Llama models repository](https://github.com/meta-llama/llama-models) at time of use. -->
- **Mistral, Cohere, and other frontier providers** — model cards vary in shape and depth. The analyst identifies which cards apply to models the enterprise uses.

The analyst does not need to memorise every card. The analyst needs to be able to (a) find the card for a model the enterprise has inventoried, (b) recognise the load-bearing sections, and (c) extract the fields chapter 05's row schema requires.

## The load-bearing sections common across public system cards

Across the public exemplars, the following section shape recurs. Not every card has every section under the same heading, but the *content* is present in some form:

1. **Model overview.** The model family, capabilities, intended use cases, and any modality extensions (vision, audio, code, tool use).
2. **Training data summary.** A high-level description of the training data provenance. Rarely detailed; the analyst does not expect a datasheet-level disclosure.
3. **Safety-training methodology.** RLHF / RLAIF / constitutional AI / DPO or the vendor's proprietary alignment approach; refusal-training corpus notes; red-team-driven fixes.
4. **Capability evaluations.** A catalogue of capability benchmarks (MMLU, GPQA, MATH, HumanEval, SWE-bench, and specialised suites) with scores.
5. **Safety evaluations.** A catalogue of safety-relevant evaluations — refusal-on-disallowed-content, bias assessments, hallucination benchmarks, jailbreak-robustness, and vendor-specific suites.
6. **Frontier / catastrophic-risk evaluations.** For frontier models, evaluations against the vendor's own Responsible Scaling Policy or Preparedness Framework capability thresholds — CBRN uplift, cyber-offense uplift, autonomous replication and adaptation, deceptive alignment, and other frontier-risk categories. Chapter 07 walks the RSP / Preparedness Framework shape that these evaluations are scored against.
7. **Red-team engagement summary.** Findings from internal and external red-teams; number of engagements, categories tested, most notable findings. Public disclosures are almost always summaries — the full findings stay with the vendor.
8. **Known limitations and observed harms.** A candid catalogue where the shape and depth vary by vendor. OpenAI's and Anthropic's cards have historically been more detailed here than average.
9. **Mitigations applied.** What the vendor did in response to red-team and safety-eval findings — policy training, refusal training, system-level guardrails, deployment-tier gating.
10. **Deployment considerations.** Recommendations for downstream deployers, including where the vendor recommends the model *not* be used, gating recommendations, and human-oversight recommendations.
11. **External evaluation collaborations.** Named collaborations — with the [UK AI Security Institute](https://www.aisi.gov.uk/), the [US AI Safety Institute (NIST)](https://www.nist.gov/aisi), METR, Apollo Research, and academic groups. The analyst records the named external evaluator alongside the vendor's own eval numbers.
12. **Change log and version.** When the card was last updated and against which model version.

## Where the three claims live in a public system card

- **Residual-risk claim.** Sections 5 (safety evaluations) and 6 (frontier evaluations), synthesised in section 8 (known limitations). For frontier evaluations, the residual-risk claim is often a *pre-mitigation* score plus a *post-mitigation* score with the delta attributed to specific interventions. The analyst records both.
- **Threshold-decision rationale.** Section 6 for frontier evaluations — the vendor cites their own RSP / Preparedness-Framework threshold and the yes-or-no call (e.g., *the model evaluated below the CBRN Medium threshold and above the CBRN Low threshold; classified at CBRN Medium; deployed with associated Medium-tier mitigations*). Chapter 07 covers the vendor threshold schemas the card references.
- **Unresolved findings.** Section 8 (known limitations) and section 10 (deployment considerations that constrain use). The vendor is publishing what they have not fully solved; the analyst records these as the vendor's own open list.

## What the analyst *reads for* in a vendor card

The analyst has three concrete questions when reading a vendor system card:

- **Does the internal system's use case fall inside or outside the vendor's stated intended use and known limitations?** If MCDA uses `anthropic/claude-3-5-sonnet-20241022` for marketing-copy drafting, does the card address marketing-adjacent use? Does the card's known-limitations catalogue include any behaviour that would show up in the MCDA use case? A card that limits *unsafe medical claim generation* is directly relevant to MCDA's `unsafe-medical-claim` category; a card that limits *long-context coherence beyond N tokens* is relevant if MCDA passes long context.
- **What frontier-risk classification did the model receive?** The vendor's own RSP / Preparedness-Framework score is a lower bound on what the enterprise must consider. A model classified at CBRN Medium by the vendor cannot be treated as CBRN Low by the enterprise's internal risk assessment without novel evidence.
- **What external evaluations did the vendor commission or accept?** An engagement with UK AISI or US AISI (NIST) is a load-bearing third-party validation. An engagement with METR or Apollo Research on autonomy or deception evals is likewise load-bearing. The analyst records the named collaborators.

## Populating a *vendor-system-card* row

Chapter 05's schema accommodates vendor cards under report-type = *vendor-system-card*. The mapping:

| Row field | Source in a vendor system card |
|---|---|
| Report title / date / author | Card header — vendor, card title, card version |
| Report type | *vendor-system-card* |
| Inventory row(s) | Foreign key to every internal `INV-<year>-<sequence>` row that uses this base model |
| System version(s) | Vendor's model identifier and version (e.g., `openai/gpt-4o-2024-11-20`) |
| Deployment configuration snapshot | *N/A — vendor evaluation is at base-model level; internal deployment configuration is captured in the internal-eval row for the internal system* |
| Task / dataset | Vendor's named capability and safety suites (sections 4 and 5); frontier-eval suites (section 6) |
| Solver / scorer | *As disclosed in card — often at a lower level of detail than an internal Inspect-style eval; recorded verbatim from the card* |
| Aggregate result | Section 4/5/6 scores, verbatim |
| Per-slice breakdown | Section 5/6 disaggregation where the card provides it |
| Residual-risk claim | Section 8 (known limitations), synthesised with section 6's frontier-eval outcome |
| Threshold-decision rationale | Section 6 — the vendor's own RSP / Preparedness-Framework threshold call |
| Unresolved findings | Section 8 (known limitations) and section 10 (deployment constraints), itemised |
| Cross-artefact links | Every internal `EVAL-<year>-<sequence>` row on a system using this model, and the paired *vendor-rsp-disclosure* row (chapter 07) |
| Row status | *evidence-current* while the model version is deployed; *evidence-stale* when the vendor releases a new version and the internal deployment has not caught up |
| Refresh cadence | Per vendor card revision or per model-version change |

The vendor card row is often *one-to-many* against internal inventory rows — one card per model version, referenced by every internal system using that model. The row's *inventory row(s)* field carries the full foreign-key list.

## Reading traps specific to public system cards

- **The self-published-metric trap.** A vendor card is the vendor's own account of their model's safety. It is evidence, but it is not independent evidence. Where an external collaborator (AISI, NIST, METR, Apollo) is named, the analyst records the external assessment as a separate line of the row's provenance.
- **The scope-of-evaluation trap.** A safety eval that measured refusal on a specific benchmark does not automatically transfer to the enterprise's harm categories. MCDA's *brand-guideline-violation* category is not going to be in any vendor's public safety suite; the vendor card is *supporting* evidence for the model's baseline safety, not *substitute* evidence for the internal safety eval.
- **The version-drift trap.** Vendor model identifiers move — `claude-3-5-sonnet-20240620` and `claude-3-5-sonnet-20241022` are different models; `gpt-4o-2024-05-13` and `gpt-4o-2024-11-20` are different models. A card for one is not evidence for the other. The row's *system version* field records the exact identifier.
- **The deprecated-card trap.** Older cards are sometimes replaced or moved as vendors publish successor documents. A URL that returned the intended card six months ago may now redirect or 404. The analyst prefers repository-controlled snapshots of vendor cards (either via [archive.org](https://web.archive.org/) or via a local mirror) alongside the current live URL.
- **The composition-not-in-card trap.** A vendor card describes the model, not the enterprise's *system* that composes the model with prompts, retrieval, tools, and guardrails. The card cannot substitute for the internal system card or the internal eval; it supplements them (per `mod-105` chapter 07).
- **The favourable-framing trap.** Vendor cards are marketing-adjacent documents. Where a card presents a favourable framing (*safe deployment in the vast majority of cases*, *the model refuses correctly in nearly all tested scenarios*), the analyst records the underlying number, not the framing.

## What the analyst does *not* second-guess

- **The vendor's own frontier-risk classification.** If the vendor classifies a model at CBRN Medium against their own RSP, the row records CBRN Medium. The analyst does not silently re-classify.
- **The named external evaluators' credibility.** An engagement with UK AISI, US AISI (NIST), METR, or Apollo Research is recorded as such. If the enterprise's counsel or council wants a view on the evaluator's independence, that is escalation-tier work (chapter 10), not a row-level override.
- **The vendor's methodology choices in the eval.** As with internal reports, the analyst records the methodology as provenance and asks about anything materially inconsistent with the residual-risk claim. The analyst does not silently re-run the vendor's calculation.

## What to memorise

- **Every foundation model the enterprise inventories has a vendor card that populates one `EVAL-<year>-<sequence>` row.** Every internal system using that model links to the card row.
- **The twelve common sections** — overview, training data, safety-training methodology, capability evals, safety evals, frontier evals, red-team summary, known limitations, mitigations, deployment considerations, external collaborations, change log.
- **Section 6 (frontier evals) is where the vendor's threshold-decision rationale lives**, scored against their own RSP / Preparedness Framework.
- **Named external evaluators are recorded as separate provenance.** UK AISI, US AISI (NIST), METR, Apollo Research — the presence of a named external is load-bearing.
- **A vendor card is *supplement*, not *substitute*.** Internal system-card and internal-eval rows still populate; the vendor row rides alongside.
- **Model-identifier version matters.** `claude-3-5-sonnet-20240620` ≠ `claude-3-5-sonnet-20241022`. Record the exact identifier.

## Summary

Public system cards from OpenAI, Anthropic, Google DeepMind, Meta, and other frontier providers converge on a twelve-section shape covering overview, training-data summary, safety-training methodology, capability and safety evaluations, frontier-risk evaluations against the vendor's own RSP / Preparedness Framework, red-team summary, known limitations, mitigations, deployment considerations, external collaborations, and a change log. The analyst extracts the three load-bearing claims into a `EVAL-<year>-<sequence>` row of type *vendor-system-card*, links it to every internal inventory row using that model, and records external-collaborator names (AISI, NIST, METR, Apollo Research) as separate provenance. Chapter 07 walks the RSP and Preparedness-Framework disclosures that the frontier-eval section of the card references, and chapter 08 covers how the internal artefacts benchmark against the vendor card and the RSP disclosure together.
