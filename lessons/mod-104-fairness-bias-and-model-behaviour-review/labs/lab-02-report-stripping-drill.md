# Lab 02 — Report-Stripping Drill on a Fixed Fairlearn Report

**Duration:** 90 minutes.
**Grounding chapters:** [01](../01-fairness-metric-glossary-and-limits.md) (per-group confusion matrix as the base artefact), [02](../02-reading-fairlearn-and-aif360-reports.md) (the four common omissions; the five-thing reading pass; the five-question non-technical summary).
**Difficulty:** Core — guided walkthrough of one report under four distinct stripping scenarios.

## Objective

Take a **fixed, complete** Fairlearn-style bias report and rewrite the analyst's findings under **four distinct stripping scenarios** — one per common omission from chapter 02 (base rates; confidence intervals; intersectional / sub-group breakdown; per-group confusion matrix as the base artefact). For each scenario, produce the pared-down five-thing reading pass, the honestly-degraded five-question non-technical summary, and the specific analyst-tier follow-up ask the missing element forces. Close with a one-sentence verdict on which omission moved the honest-what-we-can-say line the most.

Exercise 02 produces a bias-review note from a *full* generated report plus one stripped variant. Exercise 03 adds per-datapoint WIT evidence on top of the aggregate report. Neither exercise *stress-tests* the aggregate report across multiple omission patterns on a single fixed input. This lab fills that gap: four stripping scenarios on one report, with the five-thing pass and the five-question summary recomputed each time. It is the muscle an analyst uses when a reviewer asks the sharpest version of the completeness question — *"what would you be able to say if the vendor had not given you this one piece?"*

## Prerequisites

- Chapters 01 and 02 read.
- Lab 01, or exercises 01 and 02, completed or at minimum read — the metric glossary and the five-thing reading pass should not be learned here.
- A markdown editor. No Python or notebook environment required.

## The fixed input

Use *exactly* this report — do not substitute. A fixed report lets this lab's expected moves line up with the chapter-anchored expected shape in the checkpoint section. All numbers are `pedagogic example — numbers illustrative`.

> **System.** LoanRank Underwriting Signal (LRU-2027-03). In-house ML classifier used as a soft-signal input to a human underwriter's decline / approve / escalate decision on unsecured personal-loan applications. Deployer: a US-federally-chartered mid-size bank.
>
> **Automation.** Advisory — underwriter reviews the signal alongside the decisioning model's reason codes.
>
> **Evaluation dataset.** 24,800 historical applications from a 12-month window, labelled by downstream repayment outcome (positive class = "repaid on schedule in the first 12 months").
>
> **Protected attributes reported.** Sex; race/ethnicity (self-disclosed categorical); age band.
>
> **Full Fairlearn-style report (the baseline), pedagogic example — numbers illustrative.**
>
> *Per-group table — single-attribute (race/ethnicity) slice.*
>
> | Group | N | Selection rate | TPR | FPR | Precision | Calibration slope | Base rate (positive class) |
> |---|---|---|---|---|---|---|---|
> | A | 12,400 | 0.61 | 0.82 | 0.18 | 0.72 | 1.01 | 0.58 |
> | B | 7,100 | 0.52 | 0.74 | 0.17 | 0.69 | 0.95 | 0.55 |
> | C | 3,400 | 0.42 | 0.61 | 0.22 | 0.58 | 0.78 | 0.49 |
> | D | 1,900 | 0.47 | 0.66 | 0.19 | 0.63 | 0.88 | 0.51 |
>
> *Per-group confusion matrices.* Provided inline — one per group, with TP / FP / TN / FN counts summing to N.
>
> *Confidence intervals.* 95% CIs reported on selection rate, TPR, FPR, and precision per group, computed via bootstrap on the labelled set. For group C, the CI on TPR is [0.56, 0.66].
>
> *Intersectional breakdown.* A second table (not reproduced here for length) slices race/ethnicity × sex and race/ethnicity × age band. The intersection cell for *race-C × age-18-24* has N = 180 and is flagged `sample-size fragile` by the vendor.
>
> *Disparity metrics.*
>
> - Selection-rate ratio (min / max across race) = 0.42 / 0.61 = 0.69. Vendor flags *below 0.80 four-fifths threshold*.
> - TPR ratio (min / max) = 0.61 / 0.82 = 0.74.
> - Calibration slope for group C = 0.78 (materially below 1.0).
>
> *Out-of-time hold-out.* Not reported. Fairness was measured on a random stratified test split of the same 12-month window as training.
>
> *Primary fairness metric adopted by the enterprise.* Calibration by group — the bank's register records calibration as the primary because the signal is used as an input into a decisioning model that already treats scores as probabilities, and miscalibration compounds downstream. The trade-off is recorded: unequal selection rates and unequal TPR / FPR may persist.

Treat the report as given. Do not re-author it. If a stripping scenario tempts you to re-derive the missing element from the baseline, resist — the discipline is to rewrite the finding from *what the stripped report contains*, not from what you remember the baseline said.

## The four scenarios

Four stripping perturbations on the *same* baseline report. Scenario A is the baseline — your job is to anchor it, not re-read it. Scenarios B, C, D, and E strip one omission each; the idea is to see how the honest-what-we-can-say line moves as each piece is removed.

| Scenario | Shape |
|---|---|
| **A — baseline** | The full report as presented. Anchor the five-thing pass and the five-question summary once; subsequent scenarios compare against this baseline. |
| **B — base rates stripped** | The *base rate (positive class)* column is removed. Everything else stands. |
| **C — confidence intervals stripped** | All CIs are removed. Everything else stands. |
| **D — intersectional breakdown stripped** | The race/ethnicity × sex and race/ethnicity × age-band tables are removed; the single-attribute slice remains. |
| **E — per-group confusion matrices stripped** | The per-group TP / FP / TN / FN counts are removed; the derived metrics (selection rate, TPR, FPR, precision, calibration slope) remain in the per-group table. |

Each scenario strips exactly one of chapter 02's four common omissions (scenarios B, C, D) plus the chapter 01 base artefact (scenario E). The goal is to see which omission *actually* moves the analyst-tier verdict and the stakeholder-facing summary — not which looks most dramatic on the page.

## Steps

### Step 1 — Scaffold the artefact (5 min)

Create the working folder and file.

```bash
mkdir -p ~/aicg-labs/mod-104-lab-02
cd ~/aicg-labs/mod-104-lab-02
touch stripping-drill.md
```

Open `stripping-drill.md` and lay in the structure up front:

```markdown
# Report-stripping drill — LRU-2027-03 LoanRank Underwriting Signal

## 1. Baseline report (reference)
## 2. Scenario A — baseline five-thing pass and five-question summary
## 3. Scenario B — base rates stripped
## 4. Scenario C — confidence intervals stripped
## 5. Scenario D — intersectional breakdown stripped
## 6. Scenario E — per-group confusion matrices stripped
## 7. Highest-impact omission — a verdict
```

Add a one-line `Analyst / date:` entry at the top.

### Step 2 — Anchor the baseline (10 min)

Section 1 is reference. Copy the fixed-input text above into section 1 verbatim. Do not edit; the point is to have the baseline visible on the page next to each stripped scenario.

Author section 2 as the *reference* five-thing pass plus the *reference* five-question non-technical summary — the full baseline, written once, that subsequent scenarios compare against.

**2.1 Five-thing pass (baseline).** For each of the five things in chapter 02's list, one row: *observation / threshold / verdict*.

| Thing | Observation | Threshold / expected shape | Verdict |
|---|---|---|---|
| 1. Sample sizes per group | A=12,400; B=7,100; C=3,400; D=1,900 | N < 100 is unreliable; intersections flagged separately. | clean on single-attribute; intersection *race-C × age-18-24* flagged fragile by vendor. |
| 2. Selection-rate ratio | 0.42 / 0.61 = 0.69 | < 0.80 → four-fifths breach. | **breach**. |
| 3. TPR / FPR differences | TPR ratio 0.74; FPR max − min = 0.22 − 0.17 = 0.05. | Enterprise's primary metric is calibration; TPR / FPR unequal is tolerated per the recorded trade-off. | **soft-flag** against the enterprise's recorded primary metric; **hard-flag** if the primary metric had been equal-opportunity. |
| 4. Calibration slope per group | A=1.01; B=0.95; C=0.78; D=0.88. | Materially different from 1.0; this is the enterprise's *primary* metric. | **breach** on group C; group D is a soft-flag. |
| 5. Precision differences | 0.72 / 0.69 / 0.58 / 0.63 | Load-bearing when false-positive cost is high. | hard-flag — the C precision is materially below the others. |

**2.2 Five-question non-technical summary (baseline).** Chapter 02's five questions, one to two sentences each, no metric names, no thresholds. Keep it plain English — a bank's board-level reviewer, not an ML engineer.

### Step 3 — Scenario B: base rates stripped (15 min)

Section 3. The base rate column is removed; everything else stands.

**What changes.**

- **Sample sizes, selection-rate ratio, TPR / FPR, calibration slope, precision** — observations and thresholds do not move; the verdicts on each line do not mechanically change.
- **Demographic-parity interpretation becomes materially harder.** Chapter 01's "Demographic parity" section is explicit: without the underlying positive rate per group, the analyst cannot tell whether an equal-selection-rate finding is *achieved by ignoring real signal* or by *equalising real outcomes*. In *this* report, the four-fifths breach is at 0.69 and the baseline showed base rates 0.58 / 0.55 / 0.49 / 0.51 — small but real gaps. The baseline reading *could* say: the four-fifths breach is larger than the base-rate gap, so the model is adding disparity on top of the base-rate gap. The stripped reading cannot say that.
- **The calibration finding is unchanged.** Calibration slope deviation is a within-group property and does not depend on the between-group base rates for its interpretation. The primary-metric breach on group C still fires.

**What the five-thing pass can honestly say.** Rewrite the five rows for scenario B. The three affected changes:

- Row 2 (selection-rate ratio): verdict remains **breach**, but the finding is less load-bearing because the reader cannot tell whether it reflects real signal.
- The non-technical summary's "bottom line" question (chapter 02's Q2) must be rewritten to honour the gap — the baseline *could* say "even accounting for differences in the underlying repayment rate across groups, the tool advances group C materially less often"; the scenario-B stripped version cannot. Rewrite as "the tool advances group C materially less often; whether that reflects underlying repayment differences or an additional disparity the tool is introducing cannot be determined from the data as presented."

**Analyst-tier follow-up ask.** One sentence: request the base-rate column from the ML team or the vendor, naming it as a chapter 02 common-omission gap. SLA: five business days.

### Step 4 — Scenario C: confidence intervals stripped (10 min)

Section 4. All CIs are removed; point estimates remain.

**What changes.**

- **Sample sizes** — the CI on a group-C TPR was [0.56, 0.66]. With the CI removed, the point estimate 0.61 stands naked; the reader cannot tell whether the TPR gap is likely to replicate on another draw of the same data.
- **The three-point calibration finding on group C** — slope 0.78 stands as a point estimate without a width; the reader cannot tell whether it is 0.78 ± 0.05 (a soft-flag) or 0.78 ± 0.20 (so wide the finding is almost unverifiable).
- **The four-fifths-breach verdict is not fundamentally affected** — the Uniform Guidelines are indifferent to CIs; 0.69 < 0.80 is 0.69 < 0.80.

**What the five-thing pass can honestly say.** The breach verdicts do not move mechanically, but the *weight* behind each finding softens. Chapter 02's statement — "a 3-percentage-point difference on N=1000 is different from the same difference on N=100" — is exactly the point the CI would carry. Without CIs, the analyst's reading has to flag that *the robustness of the per-group estimates cannot be assessed from the report as presented*.

**Non-technical summary.** Rewrite Q4 (what could the audit have missed) to name the unknown robustness. One sentence; do not list the CIs the reader does not have.

**Analyst-tier follow-up ask.** One sentence: request 95% CIs on selection rate, TPR, FPR, and calibration slope per group from the ML team — bootstrap on the labelled set is the chapter 02 shape. SLA: five business days.

### Step 5 — Scenario D: intersectional breakdown stripped (15 min)

Section 5. The race × sex and race × age-band tables are removed; single-attribute race slice remains.

**What changes.**

- **The single-attribute race finding is unchanged** — four-fifths breach at 0.69; group-C calibration breach at 0.78; group-C precision at 0.58.
- **The intersection *race-C × age-18-24* with N = 180 is gone from the page.** The baseline flagged it as `sample-size fragile`; its loss means the analyst cannot name whether the single-attribute race-C finding is driven by a specific intersection (younger applicants, for example) or is distributed across intersections.
- **Chapter 02's "missing sub-group breakdown" is the single most load-bearing omission for a hiring / lending disparate-impact review** — intersectional patterns hide behind single-attribute aggregates. The stripped report's four-fifths breach is unchanged, but the diagnosis is weaker.

**What the five-thing pass can honestly say.** The five rows do not move mechanically — the chapter 02 five-thing pass is anchored on the single-attribute slice. But the *coverage gap* line in section 2's Part B becomes louder: the intersectional gap is now not a *flag*, it is a *hole in the report's coverage*. Rewrite the coverage-gap framing to reflect that distinction.

**Non-technical summary.** Rewrite Q2 (the bottom line) and Q4 (what the audit could have missed). The baseline's Q4 would already name the intersectional sample-size fragility; the stripped Q4 names a wider ignorance — the report does not slice by intersection at all.

**Analyst-tier follow-up ask.** One sentence: request the intersectional breakdowns (race × sex, race × age band, sex × age band) from the ML team, with sample-size disclosure per intersection cell per chapter 02. SLA: 10 business days.

### Step 6 — Scenario E: per-group confusion matrices stripped (15 min)

Section 6. The per-group TP / FP / TN / FN counts are removed; the derived metrics stand.

**What changes.**

- **Chapter 01's base artefact is gone.** The chapter is explicit: "almost every fairness metric derives from a per-group confusion matrix … When a fairness report exists but does not include the per-group confusion matrices, it is an incomplete report. The analyst-tier response: request the per-group matrices; without them the specific metric definitions cannot be verified."
- **The derived metrics in the per-group table are *claimed* but not verifiable from the page.** If the vendor computed TPR = TP / (TP + FN) using a different convention (for example, treating the "escalate" class as a soft positive), the analyst cannot re-derive from the stripped report. The report still *reads* as if the metrics are present, but the chapter 01 discipline is that without the base artefact, the derivation cannot be audited.

**What the five-thing pass can honestly say.** The rows are not mechanically different, but the *verdict strength* collapses. The chapter 01 rule bites: the five-thing pass can no longer independently verify any derived metric; everything on the page is a vendor-asserted number rather than an analyst-audited one.

**Non-technical summary.** Rewrite Q1 (was a fairness audit done — and when) to name that the audit's *claims* exist but the *base evidence* is missing. The stakeholder-facing framing: the audit's *results* are on the page, but the *working* is not.

**Analyst-tier follow-up ask.** One sentence: request per-group confusion matrices from the ML team, citing chapter 01's "base artefact" framing. SLA: five business days. Note that this is the *highest-priority* of the five asks — without the base matrices, the other derived metrics cannot be audited.

### Step 7 — Highest-impact omission verdict (10 min)

Open section 7. In three to five sentences, name the stripping scenario that moved the honest-what-we-can-say line the most.

The expected finding (write it in your own voice, not copy):

- **Scenario E (per-group confusion matrices)** moves the line most heavily for the *integrity* of the report — chapter 01 says without the base artefact, the derived metrics cannot be audited at all, so every finding downstream is vendor-asserted rather than analyst-verifiable.
- **Scenario D (intersectional breakdown)** moves the line most heavily for the *diagnostic depth* — the four-fifths breach is unchanged, but the ability to name *which sub-group is driving the breach* is lost.
- **Scenario B (base rates)** moves the line most heavily for the *interpretation* of demographic parity — the chapter 01 point that equal selection rates can only be achieved by ignoring real signal if base rates differ.
- **Scenario C (confidence intervals)** moves the line least on the breach verdict (the Uniform Guidelines are indifferent to CIs) but softens the weight of every point estimate.

Which single stripping is the highest impact depends on the question being asked: *"is the report auditable at all?"* → scenario E; *"what is the diagnosis?"* → scenario D; *"is the demographic-parity line interpretable?"* → scenario B. Name the question the enterprise's register entry is anchored on — for *this* system, it is the calibration primary metric with the four-fifths breach layered on top — and pick the scenario accordingly. The expected single-sentence verdict: scenario E is the highest-impact omission against *this* register anchor, because the calibration-primary-metric finding depends on a derived metric that cannot be verified without the per-group confusion matrix.

If your verdict differs, write out *why*. The drill's value is in the reasoning, not in matching a prescribed answer.

### Step 8 — Self-check (5 min)

Walk the file top-to-bottom and verify:

- Each scenario's five-thing pass is honestly *written anew*, not copy-pasted from the baseline with a note "unchanged except for X". Chapter 02's discipline: an honest stripped read is thinner than the baseline; if yours is the same length, you have silently re-imported the missing evidence.
- Each scenario's analyst-tier follow-up ask names (a) the missing element, (b) the chapter 02 common-omission label, and (c) an SLA. No ask is left as "ask the ML team for the missing piece"; the ask is specific.
- The non-technical summary in each scenario reflects what the stakeholder can act on *from the stripped report*. If the summary says the same thing in all four scenarios, the discipline has collapsed.
- The section-7 verdict names a *specific* scenario and a *specific* reason tied to the enterprise's register anchor — calibration primary, four-fifths breach layered — not a generic "scenario E is most important because it is the base artefact."
- No second report has crept into the file. One baseline, four stripping perturbations — anything more and the lab has drifted into exercise 02 scope.

## Expected output

One markdown file in `~/aicg-labs/mod-104-lab-02/`:

- `stripping-drill.md` — seven populated sections, one timestamp, one named analyst.

Total length: roughly 1,200–2,000 words. Most of the content is short-form — the lab is a drill, not an essay. The scenario-B through scenario-E sections should each be shorter than the baseline scenario A; shrinking content in each stripped scenario is part of what the discipline forces.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did the four-fifths breach verdict stay fixed across scenarios A, B, C, D, and E?** Chapter 01 and chapter 02 agree: the four-fifths threshold is 0.80, the report number is 0.69, and no omission from among base rates, CIs, intersectional slice, or per-group confusion matrix mechanically moves that verdict. If the verdict changed between scenarios, re-read chapter 01's "Disparate-impact ratio" section — the ratio is descriptive, and the omissions change *interpretation* and *auditability*, not the arithmetic itself.
2. **Did the calibration-primary-metric breach move materially in scenario E?** Yes — chapter 01's base-artefact rule says the calibration slope derivation cannot be audited without the per-group confusion matrices. The verdict in the five-thing row is the same; the *weight* behind the verdict drops to vendor-asserted. If scenario E's write-up does not reflect that drop, revise.
3. **Did you keep the non-technical summary non-technical across all four stripped scenarios?** Chapter 02's discipline is unchanged: no metric names, no thresholds in the stakeholder translation. If a scenario-B or scenario-D rewrite silently re-admitted a metric name because it was the easiest way to carry the diminished finding, revise.
4. **Does each follow-up ask name the chapter 02 common-omission label?** The four labels are *base rates per group*, *confidence intervals*, *sub-group (intersectional) breakdown*, and *fairness on an out-of-time hold-out*. Chapter 01 adds the *per-group confusion matrix* as the base artefact; scenario E's ask should cite chapter 01's framing explicitly rather than a chapter-02 label. If any ask lacks the label, it reads as improvised rather than anchored.
5. **Does the section-7 verdict pick one scenario on the strength of the enterprise's register anchor — calibration primary, four-fifths breach layered — and say so?** Chapter 02 is explicit that the register anchor determines which omission hurts most for *this* system. A generic "scenario E is the base artefact, so it is the most important" is not anchored; a specific "scenario E breaks calibration-primary auditability, which is this enterprise's recorded metric choice" is. If your verdict is generic, revise.

If any of the five is "no", revise *that section* before considering the lab done.

## Why this is a lab, not an exercise

Exercise 02 asks you to generate one full Fairlearn report and one stripped variant. Exercise 03 adds per-datapoint WIT evidence on top of the aggregate. Neither exercise walks *four* distinct stripping perturbations on the same fixed input.

This lab is the gap between those two. It takes *one* report — pre-written and fixed — and strips the four chapter 02 common omissions plus the chapter 01 base artefact *one at a time*, rewriting the five-thing pass and the five-question summary each time. It surfaces the question a sharp reviewer always asks: *"what would you be able to say if this one piece were missing?"* The muscle is in rewriting the honest finding from the stripped evidence, naming the specific chapter-anchored ask, and picking which omission actually moves the register anchor the most — which is where chapter 01's base-artefact discipline and chapter 02's common-omissions discipline actually meet.
