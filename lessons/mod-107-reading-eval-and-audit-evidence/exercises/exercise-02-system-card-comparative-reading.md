# Exercise 02 — System Card Comparative Reading

**Estimated effort:** 2 hours
**Grounding chapters:** [06 — Reading Public System Cards](../06-reading-public-system-cards.md), [07 — Responsible Scaling Policies and Preparedness Frameworks](../07-responsible-scaling-policies-and-preparedness-frameworks.md), [08 — Benchmarking Internal Artifacts Against Public References](../08-benchmarking-internal-artifacts-against-public-references.md).

## Objective

Read two public vendor system cards from different frontier-lab providers and their paired Responsible Scaling Policy / Preparedness-Framework / Frontier-Safety-Framework disclosures, populate a `EVAL-<year>-<sequence>` row of type *vendor-system-card* and one of type *vendor-rsp-disclosure* for each vendor, and produce a `BENCH-<year>-<sequence>` benchmark row that compares one internal system's evidence base against the vendor artefacts along the four axes chapter 08 fixed. The exercise's point is not to *rank the vendors* — the four axes are deliberately not comparable across vendors — but to make the analyst's benchmark discipline mechanical enough that the same reading applied to a different vendor next quarter produces a row of the same shape.

After this exercise you should be able to sit down with any vendor's published system card and RSP disclosure and, within an hour, produce a benchmark row with a defensible gap list that a release-assurance engineer can act on.

## Prerequisites

- Chapters 06, 07, 08 read; the twelve common system-card sections and the six RSP-family shape elements (named risk categories / thresholds / commitments / evaluation methodology / governance mechanism / change process) fresh in memory.
- The exercise-01 row set open — the vendor rows produced here will cross-link to the internal `EVAL-<year>-<sequence>` rows filed there.
- The MCDA (`INV-2026-0088`) or MCDA-Benefits (`INV-2026-0311` or your equivalent) inventory row identified as the *system under benchmark* (pick whichever one uses a frontier vendor model with a public card and RSP disclosure).
- Two vendor system cards and their paired RSPs / Preparedness Frameworks / FSFs open in adjacent tabs. Two acceptable combinations (pick one):
  - **OpenAI + Anthropic.** [GPT-4 System Card](https://cdn.openai.com/papers/gpt-4-system-card.pdf) or a more recent OpenAI card verified against the [OpenAI research index](https://openai.com/research/), plus the [OpenAI Preparedness Framework](https://openai.com/preparedness/); and the [Anthropic Claude 3 Model Card](https://www-cdn.anthropic.com/de8ba9b01c9ab7cbabf5c33b80b7bbc618857627/Model_Card_Claude_3.pdf) or a more recent Claude card verified against the [Anthropic news page](https://www.anthropic.com/news), plus the [Anthropic Responsible Scaling Policy](https://www.anthropic.com/rsp).
  - **Google DeepMind + Meta.** A [Gemini technical report](https://arxiv.org/abs/2403.05530) or more recent verified against the [DeepMind publications page](https://deepmind.google/research/), plus the [DeepMind Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/); and a [Llama model card](https://github.com/meta-llama/llama-models) verified against the current Llama-models repository. Note that Meta does not publish an RSP-shaped document in the same form — the *vendor-rsp-disclosure* row for Meta is populated as `Not applicable — Meta does not publish an RSP-family framework of the [Anthropic / OpenAI / DeepMind] shape as of [date]; the analyst records this in the row's residual-risk-claim field and flags to the [FMF](https://www.frontiermodelforum.org/) landscape for changes` and the benchmark's Axis-2 for the Meta system compares against best-practice-industry-baseline rather than a vendor-specific RSP.
- The [UK AI Security Institute page](https://www.aisi.gov.uk/) and the [US AI Safety Institute (NIST) page](https://www.nist.gov/aisi) open for reference on the named external evaluators the cards will cite.

## Problem statement

The deliverable is a **single Markdown file, `mod-107-ex-02-vendor-benchmark.md`**, containing four rows and one benchmark artefact.

### Part 1 — Two vendor-system-card rows

For each of the two vendors you chose, populate a `EVAL-<year>-<sequence>` row of type *vendor-system-card* against the chapter-05 schema. Row identifiers `EVAL-2026-EX02-CARD-<vendor>` (e.g., `EVAL-2026-EX02-CARD-ANTHROPIC`).

Chapter 06's mapping table is the mechanical guide — twelve card sections into row columns. Load-bearing fields:

- The *system version(s) evaluated* column records the exact vendor model identifier (e.g., `anthropic/claude-3-5-sonnet-20241022`, `openai/gpt-4o-2024-11-20`). Model-identifier version drift is a specific trap chapter 06 called out.
- The *inventory row(s)* column is a **list** — every internal `INV-<year>-<sequence>` row that uses this base model links to this card row. For the exercise, populate at least the MCDA / MCDA-Benefits row you chose as the system under benchmark; if the same vendor model appears elsewhere in your enterprise's inventory, list those too.
- The *residual-risk claim* is synthesised from the card's *known limitations* (section 8) and — for frontier evaluations — the *frontier-eval outcome* (section 6). Quote both parts.
- The *threshold-decision rationale* cites the vendor's own RSP / Preparedness-Framework / FSF tier for the model (e.g., *classified at ASL-2 per Anthropic RSP v[X]*, *classified at Medium in Persuasion per OpenAI Preparedness Framework Beta v[Y]*).
- The *deployment configuration snapshot* is `Not applicable — vendor evaluation is at base-model level; internal deployment configuration is captured in the internal-eval row` per chapter 06.
- Named external evaluators (UK AISI, US AISI / NIST, METR, Apollo Research, academic groups) are recorded as separate lines of provenance — the presence of a named external is load-bearing.

### Part 2 — Two vendor-rsp-disclosure rows

For each vendor, populate a `EVAL-<year>-<sequence>` row of type *vendor-rsp-disclosure* against the chapter-05 schema. Row identifiers `EVAL-2026-EX02-RSP-<vendor>`.

Chapter 07's mapping table is the mechanical guide. Load-bearing fields:

- The *report version* column records the exact framework version identifier (RSPs revise; the RSP version cited in a card released in 2024 may not be the RSP version currently in force).
- The *inventory row(s)* column is again a list — every internal system that uses a model the framework covers.
- The *residual-risk claim* summarises the framework's own commitments at the tier the model has been classified at.
- The *threshold-decision rationale* records the framework's named thresholds and the classification calls made against them.
- The *unresolved-findings list* is populated from the framework's own change log and any acknowledged limitations of the framework itself — the developer's own statement of what the framework does not yet cover.
- Task / dataset / solver / scorer / aggregate columns are `Not applicable — RSP disclosure describes the framework, not a single eval` per chapter 07.

For the Meta case, the *vendor-rsp-disclosure* row records the absence of an RSP-family framework and links to the [Frontier Model Forum](https://www.frontiermodelforum.org/) and the [G7 Hiroshima Process International Code of Conduct for Organizations Developing Advanced AI Systems](https://digital-strategy.ec.europa.eu/en/library/hiroshima-process-international-code-conduct-advanced-ai-systems) as adjacent commitments where they exist.

### Part 3 — One benchmark row

Pick **one** of your internal systems (MCDA or MCDA-Benefits) as the system under benchmark. Choose the vendor whose model the system actually runs on. Populate a `BENCH-<year>-<sequence>` row (identifier `BENCH-2026-EX02-01`) against the chapter-08 schema, comparing the internal `EVAL-<year>-<sequence>` rows from exercise 01 against the paired vendor-system-card and vendor-rsp-disclosure rows from Parts 1 and 2 above.

The benchmark row's four axes (chapter 08):

- **Axis 1 — Category coverage.** Enumerate the vendor's safety-eval categories and RSP tracked categories. For each, mark: covered by an internal eval, partially covered, not covered (with reason). *Not applicable — [reason]* is a valid answer per chapter 08's *silent-not-applicable trap* discipline, but every *not applicable* carries a one-line justification.
- **Axis 2 — Threshold alignment.** For every category the vendor has classified the model at, mark: internal control library at least at vendor tier, at vendor tier with notes, or below vendor tier (which is a *threshold gap*). Reference `mod-108` for the internal control library where an internal control exists.
- **Axis 3 — Deployment-consideration honour.** For each recommendation in the vendor card's deployment-considerations section, mark: honoured, partially honoured, not honoured (with reason).
- **Axis 4 — External-evaluator alignment.** For each named external evaluator (UK AISI, US AISI / NIST, METR, Apollo Research), mark: matched by internal eval, matched by third-party engagement, unmatched (with recommendation).

Each axis produces zero or more gap entries. The benchmark row's *gap list* column aggregates them under `BENCH-GAP-<year>-<sequence>` identifiers with severity, owner, target closure date.

Close the benchmark with the one-paragraph *analyst summary* the release-assurance packet (exercise 03) will quote.

## Requirements

- **All four rows populate every column of the chapter-05 schema.** Where a column genuinely does not apply, the value is `Not applicable — [one-line reason]`.
- **Exact model identifiers.** `anthropic/claude-3-5-sonnet-20241022` is the correct citation shape; `Claude 3.5 Sonnet` is not. Version identifiers are load-bearing (chapter 06's *version-drift trap*).
- **Exact framework versions.** The RSP row records the version identifier of the framework as published, not a paraphrase like *current RSP*. Framework revisions land on their own schedule; the analyst records both what the paired card cites and what is currently in force, and flags divergence per chapter 07's *version-in-flight trap*.
- **Named external evaluators are recorded verbatim.** UK AISI, US AISI / NIST, METR, Apollo Research, and named academic groups each appear on their own line of provenance where the card lists them. Chapter 06 called out the *self-published-metric trap* — the analyst does not collapse vendor self-report and external-collaborator evidence into a single line.
- **The benchmark row cites the four axes explicitly.** A benchmark that presents a summary table without walking Axis 1 / 2 / 3 / 4 is chapter-08's *scorecard trap*. Each axis carries its own structured output.
- **The benchmark's output is a gap list, not a scorecard.** Every gap has an ID, a one-line description, a severity (Critical / High / Medium / Low), an owner, and a target closure date. Zero gaps is a valid answer *if* every axis has been honestly walked; a suspiciously-clean benchmark should be re-read.
- **No cross-vendor arithmetic.** Chapter 07's *threshold-arithmetic trap* — the benchmark is per-model-per-vendor. Do not build a comparison table that plots Anthropic ASL against OpenAI Preparedness Levels on the same axis.
- **Vendor-artefact snapshot references are recorded.** Chapter 09 will require these for the packet; capture them here. For each vendor artefact cited, the row's *source-artefact link* carries both the live URL and (where possible) an [archive.org](https://web.archive.org/) snapshot or a repository-controlled local mirror per chapter 06's *deprecated-card trap*.
- **The Meta / no-RSP case is handled honestly.** If you chose the Google DeepMind + Meta combination, the Meta *vendor-rsp-disclosure* row records the absence of an RSP-shaped framework and links to the FMF and Hiroshima Code as adjacent commitments — it is not skipped and it is not backfilled with a *would-be* framework.
- **Cited vendor artefacts are current as of the date of the exercise.** Any URL that has moved is chased; the row records both the live URL and the snapshot. Where a specific published version is unavailable, mark the row `<!-- needs-research: verify current published version of [artefact] at [vendor page URL] -->`.
- **No fabricated tier classifications.** If the vendor's card does not explicitly classify the model at a tier under a specific framework category, the row's *threshold-decision rationale* field records the absence explicitly. Do not manufacture a classification from the analyst's own reading of the numbers.

## Starter guidance

- Read each vendor's card and RSP together as a pair. The card carries the classification; the RSP carries the framework the classification is against. Reading either without the other loses context. Chapter 07 called this out as *vendor rows come in pairs*.
- The twelve common sections (chapter 06) are not headings — they are content shapes. Different vendors label the same content differently. The analyst reads for content, not for section titles.
- The card's *external evaluations* content is often thin — one sentence naming the collaboration, occasionally a paragraph. Record what is present. If the collaboration produced its own published artefact (e.g., [UK AISI's Advanced AI Evaluations updates](https://www.aisi.gov.uk/work/advanced-ai-evaluations-may-update), a METR autonomy report, an Apollo Research deception-eval paper), link to it from the row's *log / raw-evidence link* field.
- The RSP's evaluation methodology is often the most useful section to read closely — it tells the analyst what the vendor thinks a load-bearing eval looks like, which is a strong signal for what the enterprise's own internal safety-eval discipline should aspire to. Anthropic's RSP methodology, OpenAI's Preparedness Framework Safety Scorecard shape, and DeepMind's FSF early-warning-evaluations discipline are all worth reading closely.
- For Axis 1 in the benchmark row, the *category coverage* mapping is not always obvious. The vendor's *CBRN* category may not map neatly to any internal category the enterprise's safety eval covers, either because the enterprise's use case does not surface CBRN risk (in which case the axis entry is *Not applicable — MCDA does not generate scientific content; CBRN category is not applicable to this deployment*) or because the enterprise's eval has categories that no vendor names (e.g., *brand-guideline-violation*, *competitor-disparagement*). The gap list is where the *no vendor category maps* case surfaces as a *vendor evaluation does not cover this deployment-specific category — internal-eval-only evidence line* note.
- For Axis 2, the *threshold alignment* is less about matching numbers than about matching the *tier of control*. If the vendor deploys at Anthropic's ASL-2, the enterprise's internal control library needs at least ASL-2-equivalent controls (access, monitoring, refresh cadence). If the vendor's classification would trigger ASL-3 controls the vendor commits to, the enterprise's internal controls need to be updated in tandem — the row's gap list carries the update expectation.
- For Axis 3, the *deployment considerations* are usually the easiest to walk mechanically. The card recommends X for use case Y; does the enterprise's use of the model in that shape honour the recommendation? If yes, honoured; if no, gap. Chapter 08's illustrative MCDA example (customer-visible AI-disclosure marker) is the shape most gaps will take.
- For Axis 4, the *external-evaluator alignment* is the most nuanced. The point is not to replicate the external eval — it is to ensure the enterprise's evidence base is broader than the vendor's self-report. If the vendor's only line of external evidence is a single named collaboration on a specific category, and the enterprise has no independent line of evidence on that category, the gap is *category [X] evidence base rests solely on vendor self-report plus one external collaboration; recommend enterprise seek an independent line of evidence for category [X]*.
- Snapshot the vendor artefacts to a local mirror or [archive.org](https://web.archive.org/) at the time of the exercise. Vendor URLs move; the row's *source-artefact link* is only usable in six months if the snapshot is captured now.

## Acceptance criteria

- `mod-107-ex-02-vendor-benchmark.md` with two *vendor-system-card* rows (one per vendor), two *vendor-rsp-disclosure* rows (one per vendor; the Meta / no-RSP case is handled explicitly), and one `BENCH-<year>-<sequence>` benchmark row for one internal system against one vendor's paired artefacts.
- Every row populates every column of the chapter-05 schema; `Not applicable — [reason]` is a valid value; blank is not.
- Exact model identifiers with version suffixes; exact framework version identifiers.
- Named external evaluators recorded as separate lines of provenance where the card lists them.
- The benchmark row walks all four axes explicitly with per-category structured output.
- The benchmark's gap list is populated with per-gap ID, severity, owner, target closure date.
- No cross-vendor arithmetic in the benchmark or elsewhere.
- Vendor artefact snapshots are captured; the row records both the live URL and the snapshot reference.
- No fabricated tier classifications, category names, or evaluator claims. Uncertain fields marked `<!-- needs-research: -->` with the specific vendor page to check.
- The benchmark's *analyst summary* paragraph is written; exercise 03 will quote it into the review packet.

## Stretch goals

- **A third vendor row set.** Add a third vendor (Mistral, Cohere, Amazon Bedrock foundation-model providers, or an open-model provider whose safety-and-eval documentation is public). This exercises the row schema against a card whose shape may diverge more sharply from the OpenAI / Anthropic template.
- **A benchmark of the second internal system too.** Run the benchmark against the *other* system (MCDA or MCDA-Benefits — whichever you did not use in Part 3). This surfaces where the same underlying vendor model produces different gap lists on different deployments and prepares ground for the multi-system packet-composition case in exercise 03.
- **A benchmark across two models on the same system.** If your enterprise runs a system with a primary and a fallback model, produce two benchmark rows — one per model — and note where the gap lists differ. Multi-model applications need per-model transfer testing (chapter 04's *single-vendor-model transfer trap*); the benchmark surface exposes this.
- **A framework-diff mini-artefact.** Produce a short (one-page) side-by-side of the six RSP-family shape elements (chapter 07) across the two vendors you chose. Named risk categories / thresholds / commitments / evaluation methodology / governance mechanism / change process. This is chapter 07's *three exemplars share a shape* rendered as a working reference; the artefact is useful for onboarding the next analyst.
- **A regulator-tracker cross-link update.** Update the tracker rows from `mod-106` for the [EU AI Office General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/library/final-general-purpose-ai-code-practice) to cross-reference the RSP-disclosure rows produced here, per chapter 07's *connection to internal governance artefacts* section. This closes the loop between the module and the tracker discipline `mod-106` established.

## Deliverables

- `mod-107-ex-02-vendor-benchmark.md` — four vendor rows (two *vendor-system-card*, two *vendor-rsp-disclosure*) and one benchmark row with a gap list and an analyst summary.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference row set shaped around the OpenAI + Anthropic combination benchmarking MCDA against Anthropic's Claude 3.5 Sonnet card and RSP. Yours will differ in the vendors chosen, the specific model versions read, and the specific gaps surfaced. What should not differ is (a) both vendors are covered with both a card row and an RSP row (with the Meta / no-RSP case handled honestly if you chose that combination), (b) exact model and framework version identifiers are recorded, (c) named external evaluators appear on their own lines of provenance, (d) the benchmark walks all four axes with per-category structured output, and (e) the gap list has IDs, severities, owners, and target closure dates. A four-row-plus-benchmark set with every column populated honestly and every claim traceable to the vendor artefacts beats a broader review that collapses cards and RSPs together or that presents a scorecard in place of a gap list.
