# Reading Fairlearn, AIF360, and Vendor Bias-Audit Reports

## Why this chapter

Enterprises rarely author fairness reports from scratch. They use libraries — [Fairlearn](https://fairlearn.org/) (Microsoft-led open source), [AI Fairness 360 (AIF360)](https://aif360.readthedocs.io/) (IBM-led open source) — or vendor tools like [Credo AI](https://www.credo.ai/), [Holistic AI](https://www.holisticai.com/), or [Fiddler AI](https://www.fiddler.ai/). Each produces a structured report against a labelled evaluation dataset.

The analyst's job is to read those reports well enough to (a) confirm the report is complete, (b) recognise threshold breaches, (c) summarise findings for a non-technical stakeholder, and (d) open remediation tickets when required. This chapter walks the shape of the reports and the reading pattern.

## The canonical Fairlearn output

A Fairlearn report typically produces a table with rows per group and columns per metric. Common shape:

| Group | N | Selection rate | TPR | FPR | Precision | Calibration slope |
|---|---|---|---|---|---|---|
| A | 4,200 | 0.42 | 0.78 | 0.14 | 0.68 | 1.02 |
| B | 3,800 | 0.35 | 0.66 | 0.11 | 0.71 | 0.94 |
| C | 1,900 | 0.28 | 0.55 | 0.18 | 0.55 | 0.81 |

Alongside the table, Fairlearn reports **disparity metrics** — differences and ratios across groups:

- **Selection-rate difference:** max − min = 0.42 − 0.28 = 0.14
- **Selection-rate ratio (four-fifths shape):** min / max = 0.28 / 0.42 = 0.67 → below 0.80
- **True-positive-rate difference:** max − min = 0.78 − 0.55 = 0.23
- **True-positive-rate ratio:** 0.55 / 0.78 = 0.71

Fairlearn also plots these visually — the analyst reads the numbers first, glances at the plots second.

### What to look for first

1. **Sample sizes per group.** A group with N < 100 is often statistically unreliable. The analyst calls it out — a metric on 30 examples is not defensible.
2. **The selection-rate ratio.** Below 0.80 → EEOC four-fifths breach; automatic remediation ticket for a hiring/selection use case.
3. **The TPR / FPR differences.** Substantial gaps here are equalised-odds breaches; interpretation depends on the metric the enterprise adopted.
4. **The calibration slope per group.** A slope materially different from 1.0 indicates miscalibration; especially consequential when the model output is a probability used downstream.
5. **The precision differences.** Under-reported by most vendors but load-bearing when the cost of a false positive is high.

### What the report often omits

- **Base rates per group.** Without knowing the underlying positive rate in each group, some metrics are hard to interpret.
- **Confidence intervals.** A 3-percentage-point difference on N=1000 is different from the same difference on N=100.
- **Sub-group breakdown.** A single "race" axis hides intersectional patterns.
- **Fairness on an out-of-time hold-out.** Fairness on the training distribution is not fairness in production.

Any of these gaps is analyst-tier follow-up: request the missing element from the ML team before closing the review.

## AIF360 shape

[AIF360](https://aif360.readthedocs.io/) produces the same family of metrics with additional emphasis on *bias mitigation algorithms* (pre-processing, in-processing, post-processing) — approaches that transform data or predictions to satisfy a target fairness metric. The report typically includes *before-mitigation* and *after-mitigation* rows so the reviewer can see the effect of a chosen algorithm.

Analyst-tier reading of an AIF360 report:

- **Which mitigation algorithm** was applied. The names carry technical meaning the analyst records rather than judges: *Reweighing*, *Adversarial Debiasing*, *Reject Option Classification*, *Equalized Odds Post-processing*.
- **Which metric** was the mitigation optimising. If the enterprise adopted equalised odds, an *Adversarial Debiasing* run optimising demographic parity does not answer the enterprise's question.
- **The trade-off.** Almost every mitigation trades off overall accuracy for group-metric parity. Record the trade.

The analyst does not opine on which mitigation is correct; that is `ai-risk-engineer` / `ml-fairness` scope. The analyst records that a mitigation was applied and what the resulting metric profile looks like.

## Vendor bias-audit reports

Vendor reports (Credo AI, Holistic AI, Fiddler, and the "compliance-audit" reports [NYC LL 144](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) mandates for hiring tools) generally follow one of two shapes.

- **Structured metric report.** Same shape as Fairlearn/AIF360 output, sometimes with vendor-specific branding.
- **Narrative audit report.** Text-heavy, framed around methodology and findings. The metric tables are appended.

Analyst-tier reading pattern for a narrative report:

1. **Read the methodology first.** What dataset? What time window? What protected attributes? What metrics? What thresholds? If any of these is missing, the report is incomplete.
2. **Find the metric table** and treat it as a Fairlearn output — same five-thing reading pass.
3. **Read the finding statements.** Vendor reports often use hedge phrasing ("no material disparities identified"). Read past the hedge to the numbers.
4. **Check the sign-off.** Who signed off on the audit? What is their independence from the model developer? For an LL 144 audit, independence is required.

## NYC Local Law 144 specifics

For hiring tools deployed in New York City, [Local Law 144](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) requires a bias audit within one year of use, published summaries of the audit results, and candidate notifications. The audit shape is prescribed:

- **Selection rate by category** — the four-fifths comparison across sex, race/ethnicity, and intersection categories.
- **Impact ratio** — reported per category.
- **Candidate categories** — grouped as sex, race/ethnicity, and intersections.
- **Independent auditor** — a person or entity not directly involved in developing or using the tool.

Analyst-tier reading: verify the audit covers the required categories, that the impact ratio is reported per category, and that the auditor's independence is stated. Cross-check the enterprise's disclosure page has the required candidate notification text.

<!-- needs-research: verify the current NYC LL 144 audit-scope requirements and required notification text against the DCA implementation rules — the rulemaking history has produced multiple published updates. -->

## Reading a report for a non-technical stakeholder

The stakeholder does not want the metric table. They want to know:

- **Was a fairness audit done?** Yes / no. When?
- **What is the bottom line?** Named metric, threshold breached / not breached, per group.
- **What are we doing about breaches?** Named remediation, named owner, named date.
- **What could go wrong that the audit did not catch?** The analyst names the coverage gaps (small groups; missing intersectional axis; training-distribution-only; single point in time).
- **When is the next audit?** Date.

That five-question summary is what the analyst produces as a one-page bias-review note attached to the governance record.

## Concrete example — reading an MCDA-adjacent bias report

Imagine a peer system: an internal résumé-triage tool. The Fairlearn report shows selection rates 0.42 (male), 0.35 (female), 0.28 (non-binary), 0.30 (undisclosed). The disparate-impact ratio is 0.67 vs male reference; below the four-fifths threshold.

Analyst-tier reading and note:

- **Coverage.** Fairlearn output covers sex-at-birth but not race/ethnicity, not age, not disability status. Gap flagged.
- **Sample sizes.** Male N=4,200; female N=3,800; non-binary N=380; undisclosed N=610. Non-binary N is small; metric is fragile. Flagged.
- **Selection-rate breach.** 0.28 / 0.42 = 0.67 < 0.80. Automatic remediation ticket.
- **TPR breach.** 0.55 / 0.78 = 0.71. Equalised-odds breach in addition to the demographic-parity/four-fifths breach.
- **Calibration.** Group C calibration slope 0.81 — miscalibrated. Downstream use of the model score is questionable for this group.

Remediation ticket lands with the ML team. Bias-audit methodology depth (how to design a debiasing intervention; whether to re-collect data; whether to change the outcome variable) is `ai-risk-engineer` scope. The analyst files, tracks, and re-reviews when the ML team returns with a post-mitigation report.

## What to memorise

- The **Fairlearn/AIF360 output shape** — per-group table + disparity metrics.
- The **five-thing reading pass** — sample sizes; selection-rate ratio; TPR/FPR differences; calibration slope; precision.
- The **common omissions** to check for — base rates, confidence intervals, intersectional axes, out-of-time hold-out.
- The **NYC LL 144 audit requirements** — categories, impact ratio, independent auditor.
- The **five-question non-technical summary** — audit done? bottom line? remediation? gaps? next audit?

## Summary

The analyst reads bias-audit reports as a specific ritual: check sample sizes, read the disparity ratios against the four-fifths threshold and enterprise thresholds, verify calibration, flag missing elements, and produce a five-question summary a non-technical stakeholder can act on. Fairlearn and AIF360 produce structured reports on similar shapes; vendor reports vary but the reading pattern is the same. Any breach — especially the four-fifths threshold on a hiring or selection use case — fires an automatic remediation ticket. The methodology depth and legal determination defer to specialists.
