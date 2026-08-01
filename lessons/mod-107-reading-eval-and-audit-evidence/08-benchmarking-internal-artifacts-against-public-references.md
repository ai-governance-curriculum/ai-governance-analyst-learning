# Benchmarking Internal Artifacts Against Public References

## Why this chapter

Chapters 06 and 07 walked the two public artefact families the analyst should be reading — the vendor system card and the vendor RSP / Preparedness-Framework disclosure. Those artefacts are not just files-in-a-drawer; they are the reference documents against which every regulator, auditor, and governance council will silently or explicitly compare the enterprise's internal artefacts.

The comparison is the *benchmark*. Where the vendor's system card says *the model was evaluated against these safety benchmarks and classified at [tier]*, the analyst's job is to ask *does our internal safety-eval cover the categories the vendor cares about? Do we deploy the model in a way that respects the vendor's stated deployment considerations? Does our residual-risk claim align with, or diverge from, the vendor's? Where it diverges, do we have the evidence to justify the divergence?* The benchmark is not a scorecard — it is a *gap analysis* that produces a follow-up list.

This chapter walks the benchmark method: what to compare, how to record the comparison, how to file a gap, and how to hand the resulting gap report to `ai-evaluation-engineer` and to the internal-policy-refresh owner.

## What the benchmark is (and is not)

The benchmark is:

- A **structured comparison** between the internal `EVAL-<year>-<sequence>` rows for a system and the paired vendor-system-card and vendor-rsp-disclosure rows for the underlying model.
- A **gap-analysis output** — a list of categories the vendor evaluated that the enterprise has not; commitments the vendor made that the enterprise has not internalised; deployment considerations the vendor recommended that the enterprise has not honoured.
- A **written artefact** filed into the governance repository, cross-linked to the underlying rows.

The benchmark is not:

- A **conformance check**. The vendor's framework is not a standard the enterprise is certifying against; the enterprise is checking alignment, not conformance.
- A **cross-vendor comparison**. Chapter 07 named the reason: thresholds across vendors are not directly comparable. A benchmark is per-model-per-vendor.
- A **re-evaluation**. The enterprise is not re-running the vendor's evals; it is reading them and checking scope alignment.
- **Optional** for a system whose base model is a frontier foundation model. If the enterprise inventories a system that uses GPT-4o, Claude 3.5 Sonnet, Gemini 2, Llama 4, or any other frontier model with a published system card and RSP disclosure, the benchmark row is a required deliverable of this module.

## The four benchmark axes

For any internal system whose underlying model has a public system card and RSP disclosure, the analyst benchmarks along four axes:

### Axis 1 — Category coverage

Question: **Do the internal safety-eval categories cover what the vendor's safety-eval categories cover?**

Method: enumerate the categories in the vendor system card's safety-evaluations section (chapter 06 section 5) and the vendor RSP's tracked categories (chapter 07). For each, ask: does the enterprise's internal safety-eval `EVAL-<year>-<sequence>` row for this system cover the category, and how? Categories the vendor covers that the internal eval does not are *coverage gaps*.

Illustrative output: *Vendor covers CBRN-uplift, cyber-offense-uplift, model-autonomy, persuasion, bias, hallucination-under-grounding. Internal safety-eval covers brand-guideline-violation, competitor-disparagement, protected-class-generalisation, unsafe-medical-claim, plus hallucination-under-grounding (RAG-triad row `EVAL-2026-089`). Coverage gap: cyber-offense-uplift is not evaluated internally; the vendor's system card is the sole evidence line. Coverage gap: model-autonomy is not applicable — the deployed system has no tool use enabled.*

### Axis 2 — Threshold alignment

Question: **Does the internal threshold on residual risk align with, exceed, or fall below the vendor's stated threshold classification?**

Method: for every category the vendor has classified the model at, check whether the enterprise has an internal threshold that at minimum matches. An enterprise deploying a model at Anthropic's ASL-2 needs its own controls to be at least ASL-2-equivalent; a model classified at OpenAI Medium in Persuasion needs internal Persuasion-tier controls. Where the vendor has classified the model at a higher tier than the enterprise's controls are prepared for, the enterprise has a *threshold gap*.

Illustrative output: *Vendor classifies underlying model at [Tier X in Category Y] per the paired system card. Enterprise internal control library does not have a matching tier-Y control for the [X] category (chapter reference: `mod-108`). Threshold gap: internal control library requires tier-Y-equivalent control for [category] before [system] can be released at the internal risk-acceptance threshold. Owner: [platform team]. Target closure: [date].*

### Axis 3 — Deployment-consideration honour

Question: **Does the enterprise's deployment of the model honour the vendor's stated deployment considerations?**

Method: read the vendor system card's deployment-considerations section (chapter 06 section 10). It usually contains recommendations — human oversight in specific contexts, gating for certain use cases, prohibited use cases, recommended guardrail configurations. For each, check whether the enterprise's deployment does or does not follow the recommendation.

Illustrative output: *Vendor recommends human review of model output in [context]. MCDA is a marketing-copy draft assistant where human review before publication is the intended workflow — recommendation is honoured. Vendor recommends against use for [context]; MCDA does not use the model in that context — no gap. Vendor recommends [specific guardrail configuration]; MCDA's guardrail configuration matches — no gap. No deployment-consideration gaps for MCDA.*

Or, for a gap: *Vendor recommends [specific human-oversight configuration] for [category] of use cases. Enterprise system [X] uses the model in that category but does not currently implement the recommended oversight. Gap filed as [ID]; owner [system product owner]; target closure [date].*

### Axis 4 — External-evaluator alignment

Question: **Where the vendor names an external evaluator (UK AISI, US AISI / NIST, METR, Apollo Research), does the enterprise have a corresponding line of evidence — internal or contracted?**

Method: for each named external evaluator, note whether the enterprise has any equivalent line of evidence for the categories the evaluator worked on. This is usually less about *replicating* the external eval and more about ensuring the enterprise's evidence base is broader than the vendor's own self-report.

Illustrative output: *Vendor's card names UK AISI collaboration on [category]. Enterprise has no independent evaluation of the model in [category]; the AISI collaboration and the vendor's own eval are the sole evidence lines. No gap; the AISI collaboration is a strong third-party evidence line and is recorded verbatim in the row's provenance.*

Or, for a gap: *Vendor's card does not name any external evaluator for [category]. Enterprise has no independent evaluation either. Coverage gap: [category] evidence base rests solely on vendor self-report; recommend enterprise seek an external evaluation or an internal red-team engagement scoped to the category. Owner: `ai-evaluation-engineer`. Target: next release-planning cycle.*

## The benchmark row shape

The benchmark artefact is itself a row in the governance repository, filed under a per-benchmark identifier convention (`BENCH-<year>-<sequence>`) that references — but is separate from — the underlying `EVAL-<year>-<sequence>` rows. Its columns:

- **Benchmark ID.** `BENCH-<year>-<sequence>`. Stable; never re-used.
- **System benchmarked.** Foreign key to `INV-<year>-<sequence>`.
- **Model benchmarked.** Vendor + identifier + version.
- **Vendor artefacts benchmarked against.** Foreign key list to the paired `EVAL-<year>-<sequence>` rows of type *vendor-system-card* and *vendor-rsp-disclosure* (chapters 06 and 07).
- **Internal artefacts benchmarked from.** Foreign key list to the internal `EVAL-<year>-<sequence>` rows for the system.
- **Axis 1 — category-coverage output.** Structured list per category: covered, partially covered, not covered (with reason).
- **Axis 2 — threshold-alignment output.** Structured list per category: aligned, aligned-with-notes, below-vendor-classification (with reason and gap-ID).
- **Axis 3 — deployment-consideration output.** Structured list per vendor recommendation: honoured, partially honoured, not honoured (with reason and gap-ID).
- **Axis 4 — external-evaluator output.** Structured list per named external: matched-by-internal, matched-by-third-party, unmatched (with recommendation).
- **Gap list.** Itemised, each gap with an ID (`BENCH-GAP-<year>-<sequence>`), one-line description, severity (analyst's tier — Critical / High / Medium / Low), owner, target closure date.
- **Analyst summary.** One paragraph the council briefing (`mod-110`) or the release-assurance packet (chapter 09) can quote.
- **Benchmark date.** The date the benchmark was performed.
- **Next-benchmark-due date.** When the benchmark should be re-run (per vendor-card revision, per RSP revision, per internal-system material change, or per quarterly cadence — whichever is soonest).
- **Row status.** *evidence-current* / *evidence-stale* (a vendor artefact has been superseded) / *escalated* (a gap requires escalation per chapter 10) / *retired*.
- **Last-verified / verified-by.** Same as chapter 05's rows.

## A worked benchmark — the MCDA example

Bringing forward the illustrative MCDA rows from chapter 05 (all illustrative — not real reports or a real system), the benchmark against the paired Claude 3.5 Sonnet system card and Anthropic RSP disclosure (both hypothetically summarised as *vendor rows are `EVAL-2026-102` and `EVAL-2026-103`*):

- **Benchmark ID.** `BENCH-2026-014`.
- **System.** MCDA (`INV-2026-0088`).
- **Model.** `anthropic/claude-3-5-sonnet-20241022`.
- **Vendor artefacts.** `EVAL-2026-102` (vendor-system-card) + `EVAL-2026-103` (vendor-rsp-disclosure).
- **Internal artefacts.** `EVAL-2026-088` (chapter 05's safety eval) + `EVAL-2026-091` (chapter 05's red-team engagement).
- **Axis 1 — category coverage.** Vendor covers CBRN, cyber-offense, model-autonomy, persuasion, bias, hallucination. Internal covers brand-guideline-violation, competitor-disparagement, protected-class-generalisation, unsafe-medical-claim. Overlap: bias (protected-class-generalisation is a bias sub-category); hallucination (partially covered — MCDA does not have a RAG-triad row; noted as a coverage gap `BENCH-GAP-2026-014-01`). Non-overlap: CBRN, cyber-offense, model-autonomy, persuasion — *not applicable to the MCDA use case* (justification recorded per category: MCDA does not generate scientific content, does not generate cyber-relevant content, has no tool use, is human-reviewed before publication).
- **Axis 2 — threshold alignment.** Vendor classifies the model at [ASL-tier X] per the paired RSP row. Enterprise controls for MCDA are graded at least tier-X-equivalent per the control library (`mod-108` reference `CTRL-2026-042`). Aligned.
- **Axis 3 — deployment consideration.** Vendor recommends human review before publication for marketing-adjacent generation. MCDA workflow enforces human review before publication — honoured. Vendor recommends explicit disclosure of AI-generated content to the customer where the enterprise's context requires; MCDA output ships with an internal *AI-assisted-draft* watermark on the review step but does not currently include a customer-visible AI-disclosure marker — gap `BENCH-GAP-2026-014-02`. Owner: MCDA product owner. Target closure: 2026-09-30.
- **Axis 4 — external evaluator.** Vendor card names [external evaluator] on [category]. Enterprise has no matching evaluation on that category, but the category is *not applicable to the MCDA use case* per Axis 1. No gap.
- **Gap list.** `BENCH-GAP-2026-014-01` (hallucination coverage — Med severity, owner: `ai-evaluation-engineer`, target: 2026-Q4 to schedule a RAG-triad or grounded-generation eval for MCDA). `BENCH-GAP-2026-014-02` (customer-visible AI-disclosure marker — Med severity, owner: MCDA product owner, target closure 2026-09-30).
- **Analyst summary.** *MCDA is deployed on `claude-3-5-sonnet-20241022`. Internal safety-eval and red-team coverage covers all MCDA-relevant categories except hallucination-under-grounding, which is scheduled. Vendor threshold classification is honoured by the internal control library. Two deployment-consideration gaps — hallucination coverage and customer-visible AI-disclosure — have owners and target closure dates. No axis 4 gap because the categories the vendor's external evaluator covered are not applicable to MCDA.*
- **Next-benchmark-due.** 2026-11-01 or upon vendor RSP revision, whichever is sooner.

The benchmark row is filed alongside the two internal `EVAL-<year>-<sequence>` rows. It is a first-class input to the review packet chapter 09 works.

## Failure modes when benchmarking

- **The scorecard trap.** The analyst produces a summary table with green ticks and red crosses and no gap list. A benchmark's *output* is the gap list, not the table. A benchmark with no gap list is a status page, not evidence.
- **The identical-comparison trap.** The analyst treats an internal eval that shares a name with a vendor eval as a match without checking scope, dataset, or scorer. A model card's *bias evaluation* may be measured on a different benchmark, at a different granularity, than the enterprise's internal fairness eval; the categories nominally match but the evidence does not. The analyst records both categories and notes the divergence.
- **The vendor-classification-imported trap.** The analyst copies the vendor's classification into the internal risk register without a *why*. A vendor's classification is an input to the internal risk assessment, not a substitute for it. `mod-103` and `mod-105` still own the internal risk decision; the benchmark row is a piece of evidence that feeds them.
- **The one-off-benchmark trap.** The analyst files the benchmark once and never returns. Vendor cards revise, RSPs revise, and internal systems change. The next-benchmark-due date is a first-class field.
- **The silent-not-applicable trap.** The analyst writes *not applicable* against a category without justifying why. An auditor cannot re-verify *not applicable* without the reasoning. Every *not applicable* carries a one-line justification.

## The output of the benchmark — where it goes

- **Into the review packet** (chapter 09) — the benchmark row and gap list ride alongside the internal `EVAL-<year>-<sequence>` rows for `ai-evaluation-engineer` release-assurance sign-off.
- **Into the impact-assessment corpus** (`mod-105`) — a gap that materially changes the residual-risk claim on a system triggers an impact-assessment refresh.
- **Into the control library** (`mod-108`) — a threshold gap or a deployment-consideration gap that requires a new or strengthened control routes to the control library.
- **Into the regulatory tracker** (`mod-106`) — where the vendor's own external-oversight collaboration (UK AISI, US AISI / NIST) links to a regulator-recognised programme, the tracker row for the corresponding regulatory obligation cross-references the benchmark row.
- **Into the council briefing** (`mod-110`) — a gap graded High or Critical is a council-relevant finding.
- **Into the escalation channel** (chapter 10) — an unclosed gap that crosses its target closure date triggers escalation.

## What to memorise

- **The benchmark is required for every system whose base model has a public system card and RSP disclosure.** Not optional.
- **Four axes** — category coverage, threshold alignment, deployment-consideration honour, external-evaluator alignment.
- **The output is a gap list**, not a scorecard.
- **A benchmark is per-model-per-vendor.** No cross-vendor arithmetic.
- **Every *not applicable* carries a one-line justification.**
- **Benchmarks revise** with vendor artefacts and with internal system changes; next-benchmark-due is a first-class field.

## Summary

Benchmarking is the discipline that turns the vendor's public artefacts into a working piece of internal evidence. For every internal system whose base model has a public system card (chapter 06) and RSP disclosure (chapter 07), the analyst files a `BENCH-<year>-<sequence>` row that compares the internal `EVAL-<year>-<sequence>` rows against the vendor's along four axes — category coverage, threshold alignment, deployment-consideration honour, external-evaluator alignment. The output is a gap list with named owners and target closure dates that rides into the review packet chapter 09 builds, into the impact-assessment corpus, into the control library, into the regulatory tracker, and (for the high-severity gaps) into the council briefing.
