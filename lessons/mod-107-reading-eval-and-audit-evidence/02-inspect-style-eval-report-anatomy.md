# Inspect-Style Eval Report Anatomy

## Why this chapter

The [UK AI Security Institute's Inspect framework](https://inspect.aisi.org.uk/) is the closest thing the field has to a standardised open-source eval harness. It was published by AISI (originally the AI Safety Institute; the organisation was renamed to AI Security Institute in early 2025) as [`inspect_ai`](https://github.com/UKGovernmentBEIS/inspect_ai) and is used by AISI's own safety teams, by frontier-lab evaluators, and by an increasing number of enterprise safety-eval functions to author capability and safety evaluations.

Even where an enterprise's internal eval pipeline is not literally Inspect, the *shape* of a modern eval report has converged around the Inspect vocabulary — a task, a dataset, a solver, one or more scorers, per-sample records, and an aggregated result. Learning to read an Inspect report reliably transfers to any enterprise-safety-eval report an analyst is likely to encounter.

This chapter walks the load-bearing sections of an Inspect-style report — what each section says, where the residual-risk claim lives, where the threshold-decision rationale lives, and where the unresolved findings live. The point is not to teach the analyst to *build* an Inspect eval — that is `ai-evaluation-engineer` scope — but to teach the analyst to read one and pull out the three claims chapter 01 named.

## Inspect's core vocabulary

Inspect standardises around a small set of primitives. Every eval report the analyst reads will name most of these:

- **Task.** The named evaluation, described in a Python module. A task pairs a dataset with a solver and one or more scorers. Example task names in the public [Inspect Evals repository](https://github.com/UKGovernmentBEIS/inspect_evals) include `mmlu`, `arc`, `gpqa`, `humaneval`, and safety-oriented tasks under sub-directories for cyber, biology, and behaviour.
- **Dataset.** The samples the task runs on. Each sample carries an *input* (the prompt or scenario) and one or more *targets* (the correct answer, the disallowed answer, or a rubric).
- **Solver.** The pipeline that takes each sample's input and produces the model output. Solvers may include tool-use loops, multi-turn dialogues, chain-of-thought elicitation, self-critique steps, and other structures the eval owner chose.
- **Scorer.** The function that converts each sample's output-plus-target into a numeric or categorical score. Scorers may be exact-match, rubric-based, LLM-as-judge, or programmatic.
- **Model.** The specific model version and provider being evaluated. The report cites the model identifier — for example `openai/gpt-4o-2024-11-20` or `anthropic/claude-3-5-sonnet-20241022`.
- **Sample.** One row of the dataset, evaluated end-to-end.
- **Log.** The complete per-sample transcript — input, model messages, tool calls, tool outputs, final answer, scorer output, and metadata. Inspect stores logs in `.eval` files that can be replayed with the Inspect log viewer.
- **Metric.** The aggregation of scorer output — accuracy, mean score, pass-rate, refusal-rate. A task can produce multiple metrics.

If any of these primitives is missing from a report the analyst is reading, the report is under-specified — the analyst notes the gap and files it as a follow-up (chapter 10).

## The report's expected sections

A well-authored Inspect-style eval report has roughly these sections. The analyst reads them in order:

1. **Header.** Report identifier, author, date, model(s) evaluated, task(s) run, and a one-paragraph purpose statement. The purpose statement is the analyst's first indicator of the eval's *scope* — a capability eval, a safety eval, a fairness eval, or a mixed suite.
2. **Scope and out-of-scope.** What this eval measured and — critically — what it did *not* measure. A safety eval that measures refusal rate on CBRN prompts but does not measure jailbreak-robustness under an adversarial rewrite says so explicitly here. Analysts should treat any report that does not state its out-of-scope as under-specified.
3. **Model(s) evaluated.** Exact model identifier and version. If the eval was run on a fine-tune or a system-prompted deployment, the fine-tune identifier and the system prompt version. This section is often terser than it should be; the analyst asks for the missing detail.
4. **Task and dataset.** The tasks that ran and the datasets under each. Each dataset is cited — either by public reference (a HuggingFace dataset URL, a paper) or by internal identifier for enterprise-curated datasets.
5. **Solver configuration.** The prompting scaffold, tool inventory, temperature settings, number of trials per sample, and any other solver-level configuration. A residual-risk claim that reports refusal-rate at *temperature=0, single-trial, no tools* is a different claim than one at *temperature=0.7, five-trial best-of-N, with browsing and code execution*.
6. **Scorer configuration.** How each scorer works, and — for LLM-as-judge scorers — the judge model and judge prompt. LLM-as-judge scoring is the fastest-growing source of eval error in enterprise safety evals; the analyst flags any judge configuration that is under-documented.
7. **Aggregate metrics.** The headline numbers. Accuracy, refusal rate, harm-elicitation rate, or a bespoke metric name with a defined denominator.
8. **Per-sample breakdown.** Distribution of scores across samples; disaggregation by dataset slice, by category, by difficulty tier. This is often where a safe-looking aggregate hides an unsafe subset.
9. **Comparison to prior runs.** How this run compares to the last one — a deterioration is a much stronger governance signal than an absolute number in isolation.
10. **Residual-risk narrative.** The eval owner's plain-language interpretation: *given the numbers above, what is the residual risk this system is being deployed with?*
11. **Threshold-decision rationale.** The named internal or external threshold the residual risk is being measured against, and the yes-or-no call.
12. **Unresolved findings and follow-ups.** Coverage gaps the eval owner is not closing in this run; findings that require follow-up work; open questions.
13. **Change log.** Version history of the report itself — when it was refreshed, what changed since the last version, when it should be refreshed next.
14. **Appendix / log links.** Links to the underlying Inspect log files (`.eval` files or equivalent) so a downstream reader can inspect specific samples.

Not every enterprise report has all fourteen sections named this way. But if the report cannot answer *what did you measure*, *on which model*, *with which solver and scorer*, *what did you find*, *what is the residual-risk claim*, *what is the threshold decision*, and *what did you not close* — six load-bearing questions — the analyst treats it as under-specified.

## Where the three claims live

Chapter 01 named the three claims. Here is where each one typically lives in an Inspect-style report:

- **Residual-risk claim** → sections 10 and 11. Section 10 states the risk in words; section 11 (or the closing paragraph of section 10) states the threshold-decision rationale.
- **Threshold-decision rationale** → section 11. If the report has no section 11 — no named threshold, no yes-or-no call — the analyst files this as a gap. The analyst does not manufacture a threshold from the metric alone.
- **Unresolved findings** → section 12. Explicit, itemised, with (ideally) severity, reproducibility, and follow-up owner. If unresolved findings are scattered across the report rather than itemised in one place, the analyst assembles the list and cross-checks with the eval owner before summarising.

The analyst's row is populated from these three sections. Sections 3–9 populate the *provenance* fields (model version, dataset, solver, scorer, metric, aggregate values). Section 13 populates the row's *last-verified-date* and *refresh-cadence* fields. Section 14 populates the row's *source-log-link* field.

## Common failure modes when reading Inspect-style reports

- **Aggregate-only reading.** The analyst reads section 7 (aggregate metrics), sees a 92% refusal rate, and files that as the residual-risk claim. Section 8 (per-sample breakdown) may show that all 8% of non-refusals cluster in a specific harm category the enterprise cares most about. The row must reflect the disaggregation, not just the headline.
- **Ignoring the solver.** A refusal rate reported at temperature=0 does not generalise to the deployed configuration at temperature=0.7 with tool use enabled. The analyst records the exact solver configuration in the row's provenance field so a downstream reader knows what regime the number came from.
- **Ignoring the scorer.** LLM-as-judge scorers can be biased in ways that are not obvious from the aggregate. If section 6 does not name the judge model and does not link to the judge prompt, the analyst files a follow-up before quoting the aggregate as evidence.
- **Silently promoting a capability metric into a safety claim.** A high MMLU score is a capability signal, not a safety signal. If the report is a capability eval, the residual-risk claim is a capability claim (e.g., *the model performs at [level] on [task] — the risk of deploying it without additional safety mitigations is [X]*), not a general safety claim.
- **Reading a stale report.** Inspect logs and reports carry timestamps. If the model version or the solver configuration has changed since the report ran, the report is stale. Chapter 10 covers the stale-eval escalation.

## A concrete illustrative walkthrough

Consider an enterprise-safety eval report on the MCDA (marketing-copy draft assistant) inventory row from prior modules. The report might look like this (illustrative — not a real report):

- **Header.** *MCDA safety eval, run 2026-07-14, author Safety Eval Team, model `anthropic/claude-3-5-sonnet-20241022` via internal API gateway.*
- **Scope.** *Measures refusal on the internal harm suite v3.2 (four categories: brand-guideline-violation, competitor-disparagement, protected-class-generalisation, unsafe-medical-claim). Does not measure jailbreak-robustness under adversarial rewrite; that is scheduled for red-team engagement RT-2026-014.*
- **Model.** `anthropic/claude-3-5-sonnet-20241022`, with the MCDA system prompt v1.7 and no tool use.
- **Task and dataset.** `mcda_harm_suite_v3_2`, 1,200 samples, 300 per category, prompts curated from prior red-team engagements RT-2026-001 through RT-2026-011.
- **Solver.** Single-turn, temperature=0.7, three-trial majority vote (a *pass* requires refusal in ≥ 2/3 trials).
- **Scorer.** LLM-as-judge with `anthropic/claude-3-opus-20240229` as judge, judge prompt v2.1 (linked). Categorical: `refused` / `answered-safely` / `answered-unsafely`.
- **Aggregate.** Refusal-or-safe-answer rate: 96.4% overall. `unsafely-answered` rate: 3.6%.
- **Per-sample breakdown.** Category breakdown: brand-guideline-violation 99.3% safe; competitor-disparagement 98.7% safe; protected-class-generalisation 89.0% safe; unsafe-medical-claim 98.7% safe.
- **Comparison.** Improvement of +4.1pp overall vs the prior run (2026-05-02); protected-class-generalisation moved from 82.3% to 89.0%.
- **Residual-risk narrative.** *Overall safe-answer rate is above the internal MCDA-safety-threshold of 95%. Protected-class-generalisation remains the weakest category at 89.0%, below its category-specific threshold of 92%; this is characterised as a partial-failure requiring follow-up.*
- **Threshold-decision rationale.** *The overall threshold is met; the category-specific threshold on protected-class-generalisation is not. Per internal safety-eval-policy v2.4, a category-specific miss with an aggregate pass is graded amber and requires a follow-up eval within 60 days.*
- **Unresolved findings.** *Finding SE-2026-114: protected-class-generalisation at 89.0% (threshold 92%). Owner: MCDA product owner. Follow-up eval scheduled RT-2026-014 (red-team) and re-eval by 2026-09-14. Finding SE-2026-115: judge-prompt v2.1 was measured against a small human-labelled calibration set of 50 samples; inter-annotator agreement was 0.83; recommend a 200-sample re-calibration in the next quarter.*

The analyst's row for MCDA populates from those sections in a mechanical way. Chapter 05 walks the extraction.

## What the analyst does *not* second-guess

- **The scorer's calibration.** If the report claims inter-annotator agreement is 0.83 on a 50-sample calibration set, the analyst records that number. The analyst does not re-run the calibration or dispute it.
- **The threshold value itself.** If the internal MCDA-safety-threshold is 95%, the analyst records 95% as the threshold. If the analyst believes the threshold should be higher, that is a *governance-council* observation for the internal-policy-review agenda, not a decision the analyst makes in the row.
- **The eval owner's methodological choices.** Choice of single-turn vs multi-turn, temperature setting, best-of-N configuration, judge model, and scorer prompt are the eval owner's. The analyst records the choices as provenance and — if a choice looks materially inconsistent with the residual-risk claim — asks the eval owner to characterise the choice. The analyst does not silently override it.

## What to memorise

- **Inspect standardises task / dataset / solver / scorer / model / sample / log / metric.** Reports that don't name these primitives are under-specified.
- **The fourteen expected sections** — header, scope, model, task, solver, scorer, aggregate, per-sample, comparison, residual-risk narrative, threshold-decision rationale, unresolved findings, change log, appendix.
- **Sections 10, 11, and 12 carry the three load-bearing claims.**
- **Read aggregate *and* per-sample.** A safe aggregate can hide an unsafe subset.
- **Record the solver and scorer configuration in the provenance fields.** A number without its regime is a number, not evidence.

## Summary

An Inspect-style eval report is the analyst's most common evidence artefact. Its sections converge around Inspect's core vocabulary — task, dataset, solver, scorer, model, sample, log, metric — and its residual-risk claim, threshold-decision rationale, and unresolved-findings list live in the closing sections. The analyst reads the report end-to-end, records the aggregate *and* the per-sample breakdown, captures the exact solver and scorer configuration as provenance, and populates the governance-record row from the three load-bearing sections. Chapter 03 walks a specialised report shape — the RAG-triad eval — and chapter 04 walks red-team engagement reports before chapter 05 defines the row itself.
