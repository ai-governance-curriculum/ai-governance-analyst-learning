# Exercise 01 — Fairness Metric Glossary and Limits

**Estimated effort:** 2 hours
**Grounding chapter:** [01 — The Fairness Metric Glossary — And What Each One Cannot Tell You](../01-fairness-metric-glossary-and-limits.md)

## Objective

Author a working analyst-tier glossary of the five fairness-metric families in chapter 01, in a shape that lets you (a) explain each metric to a non-technical stakeholder in two sentences, (b) name what the metric *cannot* tell you, (c) name a plausible use case where the metric is the right choice, and (d) walk three worked scenarios where two metrics disagree on the same classifier.

After this exercise you should be able to sit down with a Fairlearn or vendor bias-audit report, name every metric on the page from memory, and challenge a "the model is fair" claim in the review meeting by asking *fair on which axis, at what cost on the others*.

## Prerequisites

- Chapter 01 read; the five metric families and the fairness impossibility result fresh in memory.
- The [EEOC Uniform Guidelines on Employee Selection Procedures](https://www.eeoc.gov/uniform-guidelines-employee-selection-procedures) open — you will cite the four-fifths rule to the source.
- The [Fairlearn "Fairness in Machine Learning" user guide](https://fairlearn.org/main/user_guide/fairness_in_machine_learning.html) as a definitional cross-reference.
- Skimmed: [Hardt, Price, and Srebro (2016) "Equality of Opportunity in Supervised Learning"](https://arxiv.org/abs/1610.02413) and [Chouldechova (2017) "Fair Prediction with Disparate Impact"](https://arxiv.org/abs/1703.00056) — you do not have to master the maths; you do have to know what the impossibility result actually says.
- Optional: the [NIST SP 1270 "Towards a Standard for Identifying and Managing Bias in AI"](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.1270.pdf) for the systemic/statistical/human-cognitive bias framing.

## Problem statement

The deliverable is a single Markdown file — the analyst's personal fairness-metric glossary — plus a short worked-scenarios section that shows the metrics disagree on the same classifier. Structure below.

### Part 1 — the glossary rows

One row per metric. Cover **at minimum** these five families:

- Demographic parity (statistical parity, independence).
- Equalised odds (and its equal-opportunity relaxation).
- Calibration by group.
- Disparate-impact ratio / the four-fifths rule.
- Generative-output biases — representation, association, refusal, quality.

For each metric, fill these six fields:

1. **Plain-English definition** — two sentences a non-technical stakeholder can read and repeat back.
2. **Formal definition** — the actual mathematical statement (may be one line; you can reproduce chapter 01's phrasing or the Fairlearn user-guide phrasing verbatim; cite either).
3. **What a breach looks like** — a one-paragraph concrete example from a plausible enterprise use case (résumé triage, credit scoring, clinical triage, marketing coupon allocation, generative image output). Include the numbers.
4. **What the metric does *not* tell you** — the load-bearing field. Name at least one other fairness property this metric can silently violate.
5. **When it is the right choice** — the use-case shape where this metric is defensible. Cite the property of the use case that makes it defensible (equal allocation, equal accuracy, equal downstream-decision quality, etc.).
6. **Analyst-tier follow-up when it is missing** — the ask you file at the ML team when the report omits this metric.

Every field carries a citation to the source you are pulling from (chapter 01, the Fairlearn user guide, the primary paper, the EEOC guidelines). No naked assertions.

### Part 2 — the impossibility-result note

Write a short (5–10 sentences) note in your own words on the fairness impossibility result. Cover:

- The three properties that cannot simultaneously hold in non-trivial cases (calibration within groups; equal FPR across groups; equal FNR across groups).
- The consequence for reporting — a claim of "fair" is under-specified without naming the axis.
- The analyst-tier ask when the report claims full fairness on all axes — because that claim is either wrong or the enterprise's use case is a trivial edge case.

Cite Chouldechova (2017) and/or Kleinberg / Mullainathan / Raghavan (2016). Do not attempt to reproduce the proof.

### Part 3 — three worked-disagreement scenarios

Author three short (150–250 word) scenarios where the same classifier scores **satisfy one metric and breach another**. Each scenario:

- Names the use case (résumé triage, credit scoring, clinical triage — one per scenario, differ).
- Presents a small per-group table (2 or 3 groups × selection rate + TPR + FPR + calibration slope). Numbers can be fabricated *for pedagogic purposes* — mark the table `pedagogic example — numbers illustrative` so no reader mistakes it for a real report.
- Names the metric that is *satisfied* and the metric that is *breached*, with a one-line explanation of why the maths says so.
- Names which metric the enterprise would defensibly optimise for in that use case, with a one-sentence rationale.
- Names the analyst-tier remediation ticket that would fire — the specific ask, the specific owner, and the specific evidence the ticket requests.

Recommended (but not required) pairings, one per scenario:

- Demographic parity satisfied; equalised odds breached (résumé triage with genuinely different base rates).
- Equalised odds satisfied; calibration by group breached (credit scoring — same TPR/FPR, different score-to-outcome mapping).
- Calibration by group satisfied; disparate-impact ratio breached (clinical triage — well-calibrated scores, still under 0.80 selection ratio).

### Part 4 — a five-question non-technical translation

Take one of the three worked scenarios and write the five-question non-technical summary from chapter 02 — five bullets a council-level stakeholder can act on. This is preview work for exercise 02 and for `mod-110`; do it in miniature here.

## Requirements

- **The glossary covers all five metric families**, each with all six fields filled. No "TBD"; no field omitted because it "did not seem relevant".
- **Every field carries a citation** to a primary source (chapter 01 as an internal citation is fine, but the underlying primary reference — Fairlearn docs, EEOC guidelines, the original paper — should appear at least once per metric).
- **The formal-definition field is the actual definition**, not a paraphrase that loses precision. Copy from the Fairlearn user guide or from chapter 01 if in doubt, and quote.
- **The "what it does not tell you" field is not empty** for any metric. If you cannot name a fairness property the metric silently violates, you have not internalised the metric — return to chapter 01.
- **Every worked-disagreement scenario shows the maths.** The reader can verify the "satisfied" and "breached" claims against the per-group table without extra work.
- **The pedagogic-numbers disclaimer is present** on every fabricated table. No fake numbers presented as real audit outputs.
- **No fabricated statute references, incident citations, or vendor names.** If uncertain about a claim, write `<!-- needs-research: verify X --> `.
- **The five-question translation is one page or less** — the discipline is compressing, not expanding.

## Starter guidance

- The glossary is a reference artefact you will return to. Author it in a shape that lets you skim to the row you need — sub-headings per metric family, not a giant table that gets unwieldy at N=5.
- On the "when it is the right choice" field, the trap is to write "when the enterprise cares about fairness". That is not an answer. The answer names the property of the use case that lets you pick this metric over the others — e.g., demographic parity is the right choice *when the enterprise's policy commits to equal allocation regardless of ground truth*. Force the specificity.
- On generative-output biases, chapter 01 lists four (representation, association, refusal, quality). Do not compress these into a single "generative bias" row; each has a distinct measurement and a distinct kind of remediation ticket. Give each a mini-row with at least the plain-English definition and the analyst-tier follow-up.
- For the worked-disagreement scenarios, keep the tables small (2 or 3 groups). The point is not statistical realism; the point is the two-metric disagreement is visible in the numbers.
- Do the worked-disagreement scenarios *first* and let them reveal which glossary fields are thin. If your résumé-triage scenario reads flat when you try to explain why equalised odds breaches while demographic parity holds, the glossary row for equalised odds needs more work.
- On the impossibility-result note, resist the urge to reproduce the proof. The reader-facing job is to name the property so a stakeholder can act on it, not to teach the theorem.

## Acceptance criteria

- A `mod-104-ex-01-fairness-glossary.md` file with the four parts above, in order.
- All five metric families present with all six fields filled, each carrying at least one primary-source citation.
- Impossibility-result note of 5–10 sentences citing Chouldechova (2017) and/or Kleinberg-Mullainathan-Raghavan (2016).
- Three worked-disagreement scenarios, each with a small per-group table clearly marked as a pedagogic example, showing which metric is satisfied and which is breached with the maths visible.
- One five-question non-technical translation of one of the three scenarios, ≤500 words.
- Every uncertain claim marked `<!-- needs-research: -->`. No fabricated statutes, incidents, or vendor tools.

## Stretch goals

- **Extend the glossary to individual fairness.** Add a sixth family — individual / counterfactual fairness — with the same six fields. Note the difference from group fairness and why analyst-tier work rarely touches it directly.
- **A metric-choice governance decision worksheet.** Distill the "when it is the right choice" fields into a short decision worksheet a governance council could apply to a new use case ("if the use case is X, the enterprise-preferred metric is Y, and the trade-off recorded in the register is Z"). Route this back to `mod-101` for the governance-decision framing.
- **A generative-bias measurement map.** For each of the four generative-bias subtypes (representation, association, refusal, quality), name one publicly-documented measurement approach (e.g., [HELM's bias metrics](https://crfm.stanford.edu/helm/), [BOLD](https://github.com/amazon-research/bold), [StereoSet](https://stereoset.mit.edu/), [BBQ](https://github.com/nyu-mll/BBQ)). Cite each; do not extrapolate.
- **A vendor-report red-team pass.** Take a real public vendor bias-audit report — several are published under NYC LL 144 employer obligations — and audit it against your glossary. Which fields are populated? Which are silently omitted? Do not name the vendor if the exercise is not being sanctioned by them.
- **A two-page cheat sheet.** Compress the glossary to a printable two-page cheat sheet for review meetings. If a metric row does not fit, decide what to cut — that is the discipline test.

## Deliverables

- `mod-104-ex-01-fairness-glossary.md` — the four-part glossary and worked-disagreement file.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference glossary. Yours will differ in tone and in the specific worked-disagreement numbers; what should not differ is that (a) every metric has all six fields filled, (b) the "does not tell you" field is load-bearing rather than filler, (c) the three worked scenarios *show* the disagreement in the numbers rather than *assert* it. A cleanly-argued glossary of the five required families beats an eight-family glossary where half the "does not tell you" fields say "nothing". This is a reference artefact — the test is whether you would actually use it in a review meeting six months from now.
