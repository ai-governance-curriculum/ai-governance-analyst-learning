# Exercise 02 — Fairlearn Report Reading Drill

**Estimated effort:** 2 hours
**Grounding chapter:** [02 — Reading Fairlearn, AIF360, and Vendor Bias-Audit Reports](../02-reading-fairlearn-and-aif360-reports.md)

## Objective

Generate a Fairlearn (or AIF360-equivalent) report for a public tabular classifier, run the analyst-tier **five-thing reading pass** against it, produce the analyst-tier bias-review note including a remediation-ticket draft, and translate the finding into the **five-question non-technical summary** an executive stakeholder can act on.

After this exercise you should be able to open a Fairlearn or vendor bias-audit report a hiring manager or vendor forwards to you, read it end-to-end in twenty minutes, identify what is missing, and file a defensible one-page bias-review note.

## Prerequisites

- Chapter 02 read; the five-thing reading pass and the five-question non-technical summary fresh in memory.
- Exercise 01 completed — you need the glossary in reach.
- Python 3.10+ with [pandas](https://pandas.pydata.org/), [scikit-learn](https://scikit-learn.org/), and [Fairlearn](https://fairlearn.org/) installed. AIF360 is acceptable if you prefer; the reading pass is the same.
- The [Fairlearn quickstart / user guide](https://fairlearn.org/main/quickstart.html) and the [`MetricFrame` API reference](https://fairlearn.org/main/api_reference/generated/fairlearn.metrics.MetricFrame.html) open.
- Optional: the [AIF360 quickstart](https://aif360.readthedocs.io/en/stable/getting_started.html) if you take that path.

## Problem statement

You are the AI governance analyst on a hosted-model review. The ML team hands you a Fairlearn report on a classifier trained against a public benchmark dataset. Your job is to read it, verify it is complete, translate it, and file the bias-review note.

The exercise has four parts.

### Part A — pick a dataset and train a classifier

You need a Fairlearn report to read. If the ML team is not going to produce one for you at learner tier, produce one yourself using a well-known open dataset. Pick **one**:

- **[UCI Adult / Census Income](https://archive.ics.uci.edu/dataset/2/adult)** — predict income > $50K. Protected attributes: sex, race. The canonical fairness-tutorial dataset; Fairlearn's own tutorials use it.
- **[COMPAS recidivism dataset](https://github.com/propublica/compas-analysis)** — predict two-year recidivism. Protected attributes: race, sex, age. The dataset behind the [ProPublica "Machine Bias" investigation (2016)](https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing). Read the ProPublica investigation and the [Northpointe rebuttal](https://www.equivant.com/response-to-propublica-demonstrating-accuracy-equity-and-predictive-parity/) before touching this dataset — the reading pass is the exercise, but the ethical framing of *why* this dataset exists is part of what you are learning to hold.
- **[Bank Marketing dataset](https://archive.ics.uci.edu/dataset/222/bank+marketing)** — predict subscription to a term deposit. Protected attributes: age band. A lower-stakes, less-loaded dataset if COMPAS feels too heavy for a training exercise.

Train a straightforward classifier (logistic regression or gradient-boosted trees; the model is not the exercise) on your chosen dataset. Split train / test with a fixed random seed so the report is reproducible.

### Part B — generate the Fairlearn report

Author a notebook (`fairlearn_report.ipynb`) or script (`fairlearn_report.py`) that:

1. Loads the dataset and the trained model.
2. Uses Fairlearn's `MetricFrame` to compute per-group values for **at minimum**:
   - Sample size per group.
   - Selection rate per group.
   - True positive rate (recall) per group.
   - False positive rate per group.
   - Precision per group.
   - Accuracy per group.
3. Computes disparity metrics:
   - `selection_rate_difference` and `selection_rate_ratio` (this is the four-fifths shape).
   - `true_positive_rate_difference` and `true_positive_rate_ratio` (equalised-odds shape).
   - `false_positive_rate_difference`.
4. Produces a per-group calibration plot — either using Fairlearn's `calibration_curve` helper or scikit-learn's [`sklearn.calibration.calibration_curve`](https://scikit-learn.org/stable/modules/generated/sklearn.calibration.calibration_curve.html) sliced per group.
5. Writes the per-group table and the disparity metrics to a `report.md` file with the shape chapter 02 illustrates.

For at least one protected attribute, use the **intersection** of two attributes (e.g., sex × race for Adult) — Fairlearn accepts a `sensitive_features` DataFrame with multiple columns. The intersection is where chapter 02's "missing sub-group breakdown" ask often lands, and running it yourself is the fastest way to internalise the shape.

### Part C — apply the five-thing reading pass and author the bias-review note

Take *your own* generated report and read it as though the ML team handed it to you. Author `bias-review-note.md` with these sections, in order:

1. **Header.** System name (fabricate one — e.g., `INT-2026-0417 — CensusIncome income classifier`), analyst (you), date, evaluation dataset, model family, and the metric the enterprise has (hypothetically) adopted as its primary fairness metric. Pick and cite the pick.
2. **The five-thing reading pass.** For each of the five things (sample sizes per group; selection-rate ratio; TPR / FPR differences; calibration slope per group; precision differences), one to two sentences with the specific numbers from *your* report and a verdict — clean / soft-flag / hard-flag / breach.
3. **Coverage gaps.** Which of the four common omissions from chapter 02 (base rates, confidence intervals, sub-group breakdown, out-of-time hold-out) apply to your report. Name each explicitly; do not silently pass on any.
4. **Findings.** A short (150–300 word) findings section. Each finding is one paragraph with the shape *metric × per-group values × threshold × verdict × downstream implication*.
5. **The five-question non-technical summary.** The council-facing translation from chapter 02: was a fairness audit done? what is the bottom line? what are we doing about breaches? what could the audit have missed? when is the next audit? One or two sentences per question — no more.
6. **Remediation-ticket draft.** A single ticket ready to open with the ML team. Chapter 02's shape: concrete finding, threshold breached, proposed follow-up scope, and the explicit boundary that the *methodology* belongs to `ai-risk-engineer` and the *legal determination* belongs to Legal.
7. **Sign-off block.** Analyst name, date, review status (`draft` / `pending peer review` / `filed`).

### Part D — a "report is missing" pass

The report you generated in Part B is deliberately more complete than most vendor reports the analyst will see in the field. To practise the harder read, deliberately **strip** something from your report and re-run Part C on the stripped version:

- Remove the calibration plot entirely.
- OR remove the per-group table for the smallest group.
- OR remove the disparity-ratio metrics and leave only the per-group values.
- OR remove the intersectional breakdown.

Author `bias-review-note-stripped.md` — a shortened variant of the bias-review note that reflects what you *can* say from the stripped report, and what the analyst-tier follow-up ask becomes when the missing element is critical. The point is to feel the drop-off between a full report and a real-world vendor report.

## Requirements

- **The notebook / script runs end-to-end.** A reviewer can clone the workspace, run `jupyter nbconvert --to notebook --execute fairlearn_report.ipynb` or `python fairlearn_report.py`, and get `report.md` and the plots.
- **The generated Fairlearn report matches the chapter 02 shape** — per-group table, disparity metrics, calibration slope per group, intersectional breakdown on at least one attribute pair.
- **The bias-review note runs the full five-thing pass** with the specific numbers from your report, not the numbers from chapter 02's example.
- **Every finding names the metric, the threshold, and the verdict.** No "there is a problem here" without the maths behind it.
- **The five-question non-technical summary is genuinely non-technical.** No metric names, no thresholds — plain English. If the finance director cannot skim it and know what to do, rewrite.
- **The remediation-ticket draft is one ticket, not a project charter.** Concrete finding, threshold breached, proposed follow-up scope — see chapter 02 for the shape.
- **The stripped-report note reflects a real drop-off in what the analyst can say.** If the stripped note reads the same as the full note, you have not honoured the removal.
- **No fabricated statute references, incident citations, or vendor names.** Uncertain claims marked `<!-- needs-research: -->`.
- **Ethical framing on COMPAS.** If you choose COMPAS, the bias-review note explicitly frames the classifier as a *learner-tier reproduction* and cites the ProPublica investigation and Northpointe rebuttal. Do not present a COMPAS classifier as a live enterprise system.

## Starter guidance

- On dataset choice: Adult is the fastest path if you have not used Fairlearn before — the Fairlearn tutorials use it, so the setup friction is minimal. COMPAS is the sharpest for internalising *why* the impossibility result matters (Northpointe optimised for calibration; ProPublica critiqued for FPR disparity; both were technically correct, and the exercise is to hold both). Bank Marketing is the lowest-stakes if the ethical weight of the criminal-justice framing is not what you want to be practising against this week.
- Fairlearn's [`MetricFrame` walkthrough](https://fairlearn.org/main/user_guide/assessment/index.html) is the reference. Copy the pattern; adapt column names.
- For the intersectional breakdown, be honest about sample-size fragility. Adult has enough rows that most intersections work; Bank Marketing intersections thin fast. If an intersection cell has N < 30, note it in the report as `sample-size fragile` rather than reporting a metric that will not survive review.
- On calibration slope per group, the analyst does not need to fit a full calibration model. Bucket the predicted probabilities into (say) 10 bins per group, compare the mean predicted probability to the mean actual outcome per bin, and report the slope of the line through the buckets. Chapter 01 defines what "slope materially different from 1.0" means; the report gives the number and lets the reader judge.
- On the primary-fairness-metric pick, the trap is to pick "all of them". The analyst-tier discipline is to name one and record the trade. Pick equalised odds for Adult (income classification with reasonably meaningful ground truth); pick demographic parity or equal opportunity for COMPAS (recidivism ground truth is contested); pick precision-parity for Bank Marketing (the cost of a false positive — an unnecessary marketing contact — is small; the cost of a false negative is opportunity cost). Whatever you pick, write out the *trade* — what the enterprise is *not* optimising for.
- On the remediation ticket, do not draft the fix. Draft the *ask*. "Please investigate the group-C precision disparity and propose either a threshold adjustment or a data-collection review; scope of investigation to be sized by the ML team; owner: <ML team lead>; SLA: 15 business days for a scoped response."

## Acceptance criteria

- `mod-104-ex-02/fairlearn_report.ipynb` (or `.py`) that runs end-to-end and produces `report.md` and the per-group / calibration plots.
- `mod-104-ex-02/report.md` — the generated Fairlearn report with per-group table, disparity metrics, and calibration slope per group, including at least one intersectional breakdown.
- `mod-104-ex-02/bias-review-note.md` — the analyst-tier note with the seven sections above, in order.
- `mod-104-ex-02/bias-review-note-stripped.md` — the shortened variant reflecting a stripped report.
- The primary fairness metric is picked and defended; the trade-off is written down.
- Every finding cites the specific number, threshold, and verdict; the five-question non-technical summary is genuinely non-technical.
- Every uncertain claim marked `<!-- needs-research: -->`. No fabricated statutes, incidents, or vendor names.
- If COMPAS is used, ProPublica and Northpointe citations are present in the bias-review note.

## Stretch goals

- **AIF360 parallel report.** Re-run Part B using AIF360 instead of Fairlearn. Compare the reports; write a short (200-word) note on which library made the analyst's job easier and where each has a rough edge.
- **A "before mitigation vs. after mitigation" pass.** Apply one of AIF360's or Fairlearn's mitigation algorithms (Fairlearn's [`ExponentiatedGradient`](https://fairlearn.org/main/user_guide/mitigation/reductions.html) is a reasonable pick), regenerate the report on the mitigated model, and write a paragraph on what improved, what regressed, and what the analyst-tier trade-off record would look like — chapter 02's AIF360 discussion is your reference.
- **A vendor-report shadow read.** Find a publicly-published vendor bias-audit report (LL 144 employers publish these; some Credo AI / Holistic AI case studies are public). Read it end-to-end using your five-thing pass and write a 500-word analyst note. Compare the vendor's presentation choices to yours — where did the vendor hide something you would have surfaced?
- **A one-page executive slide.** Take the five-question non-technical summary and turn it into a single slide (5–6 bullets, no charts) for a council meeting. Preview work for `mod-110`.
- **A ticket-to-JIRA harness.** Wrap the remediation ticket in a Jira-ready or ServiceNow-ready template that the analyst can copy-paste. Add fields for the ML team lead, SLA, and dependency-ticket ID.

## Deliverables

- `mod-104-ex-02/fairlearn_report.ipynb` (or `.py`).
- `mod-104-ex-02/report.md` — the generated Fairlearn report.
- `mod-104-ex-02/bias-review-note.md` — the analyst-tier bias-review note.
- `mod-104-ex-02/bias-review-note-stripped.md` — the stripped variant.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works UCI Adult as the reference dataset and adopts equalised odds as the primary metric. A strong deliverable against COMPAS or Bank Marketing is not penalised — the point is running the five-thing pass with real numbers, naming what is missing, and translating for a non-technical stakeholder. The commonest failure modes are (a) reporting the Fairlearn output as-is without the analyst-tier reading pass on top; (b) skipping the calibration slope because it is fiddly to compute; (c) letting the five-question non-technical summary sneak metric names back in. A five-thing reading pass on a clean report that is honest about coverage gaps beats a technically dazzling report the stakeholder cannot read.
