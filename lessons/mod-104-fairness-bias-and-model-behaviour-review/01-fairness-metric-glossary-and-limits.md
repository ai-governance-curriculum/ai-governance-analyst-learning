# The Fairness Metric Glossary — And What Each One Cannot Tell You

## Why this chapter

Fairness metrics are the vocabulary of the bias-audit report. The analyst does not compute them — the ML or evaluation team does — but the analyst reads them, summarises them, and files remediation tickets when a threshold is breached. Reading a fairness report without a working grasp of the metric definitions is a recipe for silently misrepresenting the finding to a non-technical stakeholder.

The other reason the vocabulary matters: fairness metrics are *not compatible with each other*. A model can satisfy demographic parity and fail equalised odds. It can be well-calibrated within groups and still show a disparate-impact ratio below the four-fifths threshold. There is no single "fair" — there are choices between fairness definitions that carry ethical and legal weight. The analyst needs to know the choices.

This chapter enumerates the metrics you will see in the reports, defines each in plain-English, and — critically — says what each *cannot* tell you.

## The framing

Fairness metrics operate over a classifier's predictions on a labelled dataset with a **protected attribute** — a variable identifying group membership (race, sex, age band, disability status, etc.). Each metric compares some quantity across values of the protected attribute.

Two mental models help:

- **Group fairness.** Compare an aggregate over predictions across groups. Most classical metrics (demographic parity, equalised odds, four-fifths rule) are group-fairness metrics.
- **Individual fairness.** Similar individuals get similar treatment. Much less common in employer reports; usually shows up as *counterfactual* or *causal* fairness.

Analyst-tier work sits almost entirely in the group-fairness world. When an eval report mentions individual fairness or counterfactual fairness, note the definition and route to the ML team for interpretation.

## Demographic parity (statistical parity, independence)

**Definition.** The probability of a positive prediction is the same across groups. If the classifier says *yes* to X% of one group, it should say *yes* to roughly X% of the other.

**What a breach looks like.** A résumé screener that flags 40% of applicants from group A as *promising* but only 25% of applicants from group B.

**What it does not tell you.** Whether the *base rates* of promising candidates differ across groups. If group A genuinely has a higher rate of, say, tenure-qualifying experience for the role (because of upstream structural reasons), demographic parity would require the model to *ignore* real signal to equalise the prediction rate. That is a live debate; the analyst does not resolve it, but does record it.

**When it is the right metric.** When the goal is equal allocation of a resource, regardless of ground truth (e.g., a marketing coupon; a screening pass-through where the downstream review will re-evaluate).

## Equalised odds (Hardt / Price / Srebro 2016)

**Definition.** True positive rate (recall) and false positive rate are the same across groups. The model is equally accurate for the positive class *and* equally wrong for the negative class in each group.

**What a breach looks like.** A hiring model has 80% recall on group A but only 55% recall on group B — the model correctly identifies promising candidates from group A more often than promising candidates from group B, even though both groups have the same underlying rate.

**What it does not tell you.** Whether the *positive predictive value* (precision) is equal. A model can satisfy equalised odds and still have unequal precision — leading to unequal cost of a wrong decision across groups.

**When it is the right metric.** When the ground truth is available and the goal is equal *accuracy* per group (e.g., clinical decision support; loan default prediction).

**Weakening.** *Equal opportunity* is equalised odds relaxed to true positive rate only. Cited when the negative class error is less consequential than the positive class error.

## Calibration by group

**Definition.** For a given predicted probability p, the actual rate of positives is p — and this holds within each group. If the model says 70% chance of a customer defaulting, then across borrowers of each group where the model said 70%, roughly 70% actually default.

**What a breach looks like.** For group A, when the model predicts 70% default risk, 68% actually default. For group B, when the model predicts 70% default risk, 85% actually default. Same score, different real risk — the score means different things across groups.

**What it does not tell you.** Whether the prediction rates or error rates are equal. Well-calibrated models can still exhibit demographic-parity or equalised-odds breaches.

**When it is the right metric.** Whenever probabilities are used as decision inputs (credit scoring, risk scoring, triage). If probabilities are miscalibrated across groups, downstream decisions built on those probabilities inherit the miscalibration.

## The impossibility result

Chouldechova (2017) and Kleinberg / Mullainathan / Raghavan (2016) proved that — except in trivial cases — a classifier cannot simultaneously satisfy:

- Calibration within groups,
- Equal false positive rates across groups,
- Equal false negative rates across groups.

This is the **fairness impossibility result**. Trade-offs are not optional; they are mathematical. The analyst does not resolve the trade-off, but must not report a claim of "fair" without asking *fair on which axis, at what cost on the others*.

## Disparate-impact ratio (the four-fifths rule)

**Definition.** The ratio of the positive-selection rate for the group with the lowest rate divided by the rate for the group with the highest rate. Under the [EEOC Uniform Guidelines on Employee Selection Procedures](https://www.eeoc.gov/uniform-guidelines-employee-selection-procedures), a ratio below 0.80 (the "four-fifths rule") is treated as evidence of adverse impact.

**Formula.** disparate impact = P(positive | protected group) / P(positive | reference group).

**What a breach looks like.** In a hiring screening tool, the pass-through rate for one group is 25% and for the reference group is 40%. Disparate-impact ratio = 25/40 = 0.625 < 0.80. This is presumptive evidence of adverse impact under Title VII.

**What it does not tell you.** Whether the model is *actually* causing the disparity — the ratio is descriptive, not causal. The Uniform Guidelines' response to a below-0.80 finding is to move to a *business necessity* analysis: is the selection procedure job-related and consistent with business necessity? That analysis is not analyst scope.

**Analyst-tier framing.** A disparate-impact ratio below 0.80 gets a remediation ticket every time. The ticket does not conclude the model is illegal; it says *four-fifths threshold breached; adverse-impact analysis required per Uniform Guidelines*.

## Calibration in generative outputs — beyond classification

Generative-AI systems complicate the picture. The metrics above assume a binary classifier with a labelled dataset. LLMs and image generators do not fit that shape directly. Bias in generative outputs shows up as:

- **Representation bias.** Sampled outputs over-represent or under-represent groups (e.g., "generate an image of a CEO" defaulting to a demographic pattern).
- **Association bias.** The model links groups to attributes in ways that reproduce stereotypes.
- **Refusal bias.** The model refuses requests differently across groups or topics.
- **Quality bias.** The model produces higher-quality outputs for some groups than others (worse translation for low-resource languages; worse image fidelity for underrepresented skin tones).

Enterprise evaluation reports on generative systems typically report a mix of quantitative aggregate metrics (e.g., per-group win rates in pairwise judgments) and qualitative red-team findings. The analyst reads both.

## Confusion matrix per group — the base artefact

Almost every fairness metric derives from a per-group confusion matrix — true positives, false positives, true negatives, false negatives per group. When a fairness report exists but does not include the per-group confusion matrices, it is an incomplete report. The analyst-tier response: request the per-group matrices; without them the specific metric definitions cannot be verified.

## Metric-choice implications the analyst records

When the ML team says "we chose equalised odds as our fairness metric":

- Record that it explicitly means the enterprise accepts unequal *prediction rates* across groups when ground truth differs.
- Record that it means the enterprise accepts potentially unequal *precision* (positive predictive value) across groups.
- Note the trade-off in the register entry so the reviewer knows what the enterprise is *not* optimising for.

Metric choice is a governance decision, not an ML decision. The [senior AI governance architect](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) or head of governance signs off; the analyst records.

## What analyst-tier fairness reading is *not*

- **Not a fairness-methodology design.** The bias-audit methodology, the choice of metric, the choice of thresholds, is [ai-risk-engineer](https://github.com/ml-engineering-curriculum/ai-risk-engineer-learning) and senior-architect scope.
- **Not a statistical rigor review.** The analyst does not check confidence intervals on group metrics or interpret p-values on statistical parity tests; that is `model-evaluation-engineer` scope.
- **Not a legal determination.** The four-fifths breach flag is not a finding that Title VII is violated; it triggers legal review.

## What to memorise

- The **five metric families**: demographic parity, equalised odds (+ equal opportunity), calibration by group, disparate-impact ratio (four-fifths), generative-output biases.
- The **impossibility result** — cannot simultaneously satisfy calibration, equal FPR, equal FNR.
- The **four-fifths rule** as the EEOC-recognised threshold.
- The **base artefact** — per-group confusion matrix — and the analyst-tier ask when it is missing.
- The rule: **when a report says "fair", ask *fair on which axis, at what cost on the others*.**

## Summary

Fairness metrics are a small vocabulary but a decision-consequential one. Demographic parity, equalised odds, calibration by group, and the disparate-impact ratio measure different things and are mathematically incompatible in most cases. Generative-AI systems add representation, association, refusal, and quality biases the classical metrics do not directly cover. The analyst reads reports, records the metric choice, verifies the per-group confusion matrix is on file, and files remediation tickets when thresholds — especially the EEOC four-fifths — are breached. The bias-audit methodology itself, and the legal determination, defer to specialists.
