# RAG-Triad and Retrieval-Quality Eval Reports

## Why this chapter

Retrieval-augmented generation systems — RAG chatbots, RAG-grounded knowledge assistants, RAG-backed customer-support tools — are a large and growing share of the enterprise AI inventory. They fail differently than standalone LLM systems: a RAG system that retrieves the wrong context can produce a fluent, plausible, and wrong answer even when the underlying model is well-aligned. Standard capability and safety evals do not catch these failure modes because the failure is in the *retrieval step*, not the generation step.

The industry-standard eval shape for RAG quality is the **RAG triad**: three complementary metrics that jointly characterise whether the retrieved context was relevant, whether the answer was grounded in it, and whether the answer addressed the question. The triad was popularised by [TruEra's TruLens project](https://www.trulens.org/) and has since been adopted (with variations) by other RAG evaluation tooling — [RAGAS](https://docs.ragas.io/), [DeepEval](https://docs.confident-ai.com/), and vendor-specific RAG-eval suites in enterprise AI platforms.

This chapter walks the RAG-triad shape and the load-bearing sections of a RAG-triad eval report, so the analyst can read a report, locate the three claims chapter 01 named, and populate a governance-record row for a RAG system without help.

## The three metrics of the RAG triad

The three metrics, per the TruLens formulation:

- **Context relevance.** Is the *retrieved context* relevant to the user's query? Scored per retrieved chunk, aggregated per query. Low context relevance means the retrieval step failed — the model is being handed material it should not be trying to use.
- **Groundedness.** Is the *generated answer* supported by the retrieved context? Scored by decomposing the answer into claims and checking each claim against the context. Low groundedness means the model hallucinated — it added claims the retrieved context did not support.
- **Answer relevance.** Does the *generated answer* address the user's original question? Scored by comparing the answer to the question independent of the context. Low answer relevance means the model wandered — it produced text that may be grounded and coherent but does not answer what was asked.

All three are typically scored on a 0-to-1 scale using LLM-as-judge scorers. A single-number *RAG-triad score* (e.g., a geometric or arithmetic mean of the three) may be reported for convenience, but the analyst reads all three components — a system with 0.98 groundedness, 0.98 answer relevance, and 0.3 context relevance is retrieving noise the model is politely ignoring, and that is a very different governance story than 0.98 across all three.

## Variants and extensions the analyst may encounter

The RAG triad is the base shape; enterprise RAG-eval reports often extend it. Common extensions:

- **Faithfulness.** A synonym or subtype of groundedness in some tools (RAGAS uses *faithfulness* where TruLens uses *groundedness*; the underlying idea is the same).
- **Context precision and context recall.** From RAGAS. Precision measures whether the top-*k* retrieved chunks are relevant *in ranking order*; recall measures whether the retrieval retrieved *all* relevant chunks that existed. Both extend the single *context relevance* score.
- **Answer correctness.** Compares the generated answer to a ground-truth answer where one exists. Requires a labelled dataset with reference answers.
- **Answer semantic similarity.** Cosine similarity or LLM-judged similarity between the generated answer and a reference answer. Sensitive to phrasing differences.
- **Noise sensitivity / adversarial robustness.** How the system responds when retrieval returns partially-irrelevant or intentionally misleading chunks. A robustness variant popularised by more recent RAG-eval work.
- **Retrieval latency and token cost.** Operational metrics that belong in the report but are not part of the safety claim.

The analyst does not need to memorise every extension. The analyst needs to (a) identify which metric family the report is using, (b) locate the residual-risk claim inside that family, and (c) note in the row's provenance which specific metrics were reported.

## The expected sections of a RAG-triad eval report

A well-authored RAG-triad eval report generally has these sections. Compare with the Inspect-style anatomy in chapter 02 — the overlap is deliberate:

1. **Header and scope.** What system, what version, what retrieval index version, what generation-model version, what date. RAG systems have four version dimensions (application code, retrieval index, retrieval-model / embedding-model, generation model); the analyst records all four in the row's provenance.
2. **Corpus and index description.** The retrieval corpus — what it contains, what its access controls are, how many chunks, when it was last refreshed, whether a datasheet exists (`mod-105` chapter 07). If the corpus contains personal or regulated data, this section should say so.
3. **Query dataset.** The queries the eval ran against. Typically a curated set of representative queries (with categories for common query types, adversarial-looking queries, out-of-distribution queries, and negative queries where the correct answer is *the corpus does not contain this information*). The negative-query subset is what catches over-confident hallucination.
4. **Retrieval configuration.** Embedding model, chunk size, chunk overlap, top-*k*, re-ranking model (if any), filtering rules.
5. **Generation configuration.** Base model, system prompt version, temperature, tool inventory, guardrails.
6. **Scorer configuration.** LLM-as-judge model and judge-prompt version for each of the triad metrics; any human-labelled calibration set and inter-annotator agreement.
7. **Aggregate metrics.** Mean and (better) distribution of each triad metric. The analyst prefers reports that show distributions over reports that show only means — a mean of 0.85 groundedness with a long left tail of 0.2s is a very different story than a mean of 0.85 with a tight distribution around 0.83–0.87.
8. **Per-slice breakdown.** Scores disaggregated by query category, corpus source, retrieved-chunk provenance, and any user-population slice the system serves. The parallel to the Inspect per-sample section from chapter 02.
9. **Failure-mode catalogue.** Where the system failed — over-confident hallucination on negative queries, wrong-index retrieval on cross-domain queries, groundedness collapse under long-context stuffing, retrieval-precision collapse on paraphrased queries. Each named failure mode should carry a per-mode incidence rate and (ideally) a sample of representative failures.
10. **Residual-risk narrative.** The eval owner's plain-language interpretation.
11. **Threshold-decision rationale.** The named triad-metric thresholds (per metric — a single-number RAG-triad threshold is under-specified) and the yes-or-no call.
12. **Unresolved findings and follow-ups.** Coverage gaps, planned mitigations, next re-eval date.
13. **Change log.** Version history of the report.
14. **Appendix / raw logs.** Per-query traces the analyst can spot-check.

## Where the three claims live in a RAG-triad report

- **Residual-risk claim** → sections 9, 10, and 11. Section 9 (failure-mode catalogue) is often more concrete than the narrative in section 10 — the analyst prefers the catalogue's wording where the narrative and catalogue diverge.
- **Threshold-decision rationale** → section 11. Load-bearing question: are the thresholds *per-metric* (a floor on context relevance *and* a floor on groundedness *and* a floor on answer relevance) or is there only a composite threshold? A composite-only threshold hides a metric that failed; the analyst notes this if the report is under-specified.
- **Unresolved findings** → section 12, cross-referenced with section 9. The failure-mode catalogue often contains items the report has not committed to mitigating; those flow into the row's *unresolved findings* field alongside section 12's list.

## Failure modes specific to RAG-triad reading

- **Reading the composite RAG-triad score.** A single number that averages the three is not evidence — the three metrics are complementary and can compensate for each other in the aggregate while a specific failure mode dominates a category. The analyst records all three separately in the row.
- **Ignoring the negative-query subset.** If the report does not include negative queries (*the corpus does not contain this information; the correct answer is a refusal or an explicit uncertainty*), the eval cannot measure over-confident hallucination. The analyst files this as a scope gap.
- **Ignoring index freshness.** A RAG system evaluated against an index that has since been refreshed has a stale eval. The analyst records the eval-time index version and cross-checks against the deployed index version. Chapter 10 covers the stale-eval escalation.
- **Ignoring the corpus's sensitivity classification.** If the corpus contains personal, regulated, or trade-secret material, the RAG-triad eval's scope should include an access-control check (does the system return chunks a user shouldn't see?). If that check is absent, the analyst notes it as a scope gap and flags to counsel / DPO.
- **Treating groundedness as safety.** A system with high groundedness can still generate unsafe or harmful content that the retrieved context happens to support. Groundedness is a *quality* metric, not a *safety* metric. Safety evals (chapter 02) are separate; a mature RAG governance record cites both.

## The RAG-triad row provenance columns

Because a RAG system has four version dimensions and the eval reports typically depend on a specific fixture of all four, the analyst records these provenance fields in the row for a RAG-triad eval:

- Application version (git tag or release identifier).
- Retrieval-index version and refresh timestamp.
- Embedding model identifier.
- Retrieval configuration snapshot (chunk size, top-*k*, re-ranker if any).
- Generation model identifier.
- System prompt version.
- Scorer / judge model identifier and judge-prompt version.
- Query-dataset identifier and version.
- Eval-run timestamp.

Chapter 05 folds these into the standardised row template.

## A concrete illustrative walkthrough

Consider a RAG chatbot answering internal policy questions from the enterprise's HR policy corpus (illustrative — not a real system). The RAG-triad eval report might look like:

- **Header.** *HR-Policy-Bot RAG-triad eval, run 2026-06-30, application v2.4, retrieval index v2026-06-15, embedding model `text-embedding-3-large`, generation model `openai/gpt-4o-2024-11-20`, system prompt v3.1.*
- **Corpus.** *HR policy corpus, 8,900 chunks (400-token chunks with 50-token overlap), last refresh 2026-06-15. Contains no personal data; contains one class of restricted material (draft policy revisions) tagged and access-controlled at retrieval time.*
- **Query dataset.** *900 queries — 600 in-scope (six categories, 100 each), 200 negative (policies that do not exist or questions the bot should redirect), 100 adversarial (paraphrase, injection, out-of-domain).*
- **Retrieval.** Top-5 chunks, cosine similarity, no re-ranker.
- **Generation.** Temperature 0.2, no tool use, guardrails on personally-identifying-information leakage in outputs.
- **Scorer.** LLM-as-judge with `openai/gpt-4o-2024-11-20` as judge (documented judge-prompt v1.2, calibrated on 120 human-labelled samples, inter-annotator agreement 0.86).
- **Aggregate.** Context relevance mean 0.87 (25th percentile 0.71); groundedness mean 0.94 (25th percentile 0.85); answer relevance mean 0.92 (25th percentile 0.82).
- **Per-slice.** In-scope queries: all three metrics ≥ 0.90 mean. Negative queries: groundedness 0.71 mean, answer relevance 0.58 mean — the system over-answers on negative queries. Adversarial queries: context relevance drops to 0.62 mean.
- **Failure modes.** *(a) Over-confident answer on negative queries — 34% of negative-query answers assert a policy exists when the retrieved chunks do not support the assertion. (b) Groundedness collapse on paraphrased queries — for the top 10% of paraphrase-heavy adversarial queries, groundedness drops below 0.7. (c) One instance of restricted-tier chunk leakage in retrieved context (finding SE-2026-141).*
- **Residual-risk narrative.** *In-scope quality meets thresholds. Negative-query handling is materially below threshold and represents the highest-severity residual risk. Restricted-tier chunk leakage is a single-instance finding requiring immediate access-control review.*
- **Threshold-decision rationale.** *Per-metric thresholds: context relevance ≥ 0.80, groundedness ≥ 0.90, answer relevance ≥ 0.85. In-scope: met. Negative queries: groundedness 0.71 (fail) and answer relevance 0.58 (fail). System is graded red for the negative-query subset pending mitigation.*
- **Unresolved findings.** *Finding SE-2026-141: restricted-tier chunk leakage — owner Retrieval Platform team, target closure 2026-07-15. Finding SE-2026-142: negative-query over-answering — owner HR-Policy-Bot product owner, mitigation plan (system-prompt guardrail v3.2 draft) due 2026-07-14; re-eval scheduled 2026-08-01.*

The analyst's row for HR-Policy-Bot populates from these sections. The threshold-decision rationale is complex enough to warrant a per-slice breakdown in the row itself — chapter 05 accommodates this.

## What the analyst does *not* second-guess

- **The threshold values.** As with capability / safety evals, the specific per-metric thresholds are owned by the eval owner and the product owner; the analyst records them.
- **The corpus quality.** Whether the underlying policy documents are current or well-authored is an HR / knowledge-management concern, not a RAG-eval concern. The analyst notes the last-refresh date and moves on.
- **The judge model's choice.** If the eval used GPT-4o as judge on outputs from GPT-4o, that is a same-model-family judge — a known bias direction. The analyst records the choice and can note it as a follow-up question for the eval owner, but does not veto it.

## What to memorise

- **The three triad metrics** — context relevance, groundedness, answer relevance — must all be recorded separately in the row.
- **A composite RAG-triad score is not evidence.** Record the three components.
- **Negative queries are the load-bearing subset.** A RAG eval without negative queries cannot measure over-confident hallucination.
- **RAG systems have four version dimensions** — application, retrieval index, embedding model, generation model — and the row's provenance records all four.
- **Groundedness is a quality metric, not a safety metric.** Cite the safety eval separately.

## Summary

RAG-triad eval reports are the analyst's most common evidence artefact for retrieval-augmented systems. The three metrics — context relevance, groundedness, answer relevance — are complementary and are recorded separately in the row. Per-slice breakdowns often expose failure modes (over-confident hallucination on negative queries, groundedness collapse under paraphrase) the aggregate hides. RAG systems have four version dimensions, and the row's provenance records all four. Chapter 04 walks the third and most narrative-heavy report shape the analyst will encounter — the red-team engagement report — before chapter 05 fixes the governance-record row schema itself.
