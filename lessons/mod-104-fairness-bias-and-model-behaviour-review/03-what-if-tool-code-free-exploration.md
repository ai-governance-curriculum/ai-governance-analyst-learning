# The Google What-If Tool — Code-Free Per-Group Exploration

## Why this chapter

Fairness reports summarise. They tell you the aggregate story. What they cannot easily tell you is *how the model behaves on the boundary cases* — what happens when you change one input feature and keep everything else constant, or what the pattern of errors looks like for a specific sub-group in a specific region of the feature space.

The [What-If Tool (WIT)](https://pair-code.github.io/what-if-tool/) is an interactive visual interface for exactly that exploration. It ships as a TensorBoard plugin, a Jupyter notebook widget, and a Colab-hosted demo. The analyst does not need to write code to use it. The point of this chapter is to make you comfortable opening a WIT-connected notebook the ML team hands over, exploring the classifier's behaviour on the enterprise's protected attributes, and producing an analyst-tier note that adds evidence to the risk register.

## What WIT gives the analyst

Four capabilities matter at analyst tier.

- **Per-datapoint inspection.** Click a datapoint; see the input features, the label, the prediction, and the model's confidence. Useful for spot-checking odd predictions.
- **Counterfactual exploration.** For any datapoint, WIT surfaces the "nearest counterfactual" — the datapoint most similar to the original but with a different prediction. Useful for asking *what would this person have needed to look like to get a different answer?*
- **Partial-dependence and feature-behaviour plots.** Vary one input feature and see the prediction change. Useful for surfacing features the model over-weighs.
- **Per-group performance breakdown.** Group datapoints by a protected attribute and see per-group confusion matrices, ROC curves, and threshold analyses. This is the fairness-report artefact, made interactive.

The analyst does not train models with WIT. The analyst *inspects* models the ML team has trained.

## The setup the analyst can expect

Typical ML-team hand-off:

- A trained classifier (usually a TensorFlow, XGBoost, or scikit-learn model).
- A labelled evaluation dataset with the protected attribute column present.
- A hosted WIT notebook or a URL to a WIT session.

The analyst does not run the setup. If the notebook does not load, or the model / dataset is missing, that is an ML-team hand-off gap; the analyst flags it and does not proceed.

## The reading pattern — a WIT session in 45 minutes

A structured WIT walk for a bias-review record.

1. **Open the datapoint editor.** Confirm the dataset has the protected attribute you were told it has. If the attribute is missing or is a proxy (e.g., ZIP code standing in for race), flag and stop.
2. **Enable the performance panel.** Select the protected attribute as the *slice-by* variable. Read the per-group confusion matrices. Sanity-check they match the fairness report the ML team already handed over.
3. **Look at the ROC / precision-recall curves per group.** WIT plots the curves overlaid. Overlapping curves suggest similar per-group performance; separated curves suggest the model discriminates differently across groups.
4. **Sample five to ten datapoints per group.** For each: what did the model predict? What did the counterfactual look like? What feature moved the counterfactual across the decision boundary?
5. **Explore feature partial-dependence plots.** Especially for features that legally cannot be direct inputs (protected attributes) but might be present via proxies. If the partial-dependence plot for "ZIP code" shows a shape that suggests strong signal, that is a proxy-variable finding.
6. **Try threshold sweeps.** WIT lets you move the classification threshold and see the effect on per-group metrics. Confirm the enterprise's chosen threshold is defensible — a threshold that produces a materially different profile a small nudge away is fragile.
7. **Record findings.** Screenshot the per-group plots; note the counterfactuals that surprised you; note any partial-dependence plots that suggest proxies.

The WIT session produces the analyst-tier bias-review note: a short document capturing the exploration, the findings, and the ML-team follow-ups.

## Counterfactuals — reading them well

Counterfactuals are the most powerful and most easily-misread WIT feature.

- **A counterfactual says *the model considers these inputs similar enough that a small change flips the prediction*.** It does not say what a *fair* counterfactual would look like.
- **When the nearest counterfactual differs on a feature that is a plausible proxy for a protected attribute**, that is a finding — worth flagging even if the classical fairness metrics did not surface it. Example: on a résumé model, the nearest counterfactual differing in "graduated from a school with high representation of group X" flips the prediction. That is proxy-variable evidence.
- **When the nearest counterfactual differs on the protected attribute itself** and nothing else, and this flips the prediction, that is the strongest possible per-datapoint evidence of individual-level unfairness — modulo confounders. Route to the ML team for interpretation.

## Proxy-variable detection

Partial-dependence plots surface features the model has learned to lean on. When the analyst is aware of the enterprise's legal constraints — Title VII, ECOA, HIPAA, LL 144, EU AI Act Article 10(5) prohibiting certain training-data uses — the partial-dependence view is a first-pass filter for proxies.

Common proxy patterns to look for:

- **ZIP code / postcode** as a proxy for race.
- **Educational institution** as a proxy for socio-economic status or race.
- **Employment gap length** as a proxy for parental status or disability.
- **Language spoken** as a proxy for national origin.
- **Employer name** as a proxy for age (some employers have age-clustered workforces).

None of these findings is a legal determination. All of them are analyst-tier signals to route to the ML team, with a note to Legal for consumer-facing or hiring uses.

## The analyst-tier WIT note

The output is a short structured note attached to the governance record.

- **System reviewed** and **evaluation dataset.**
- **WIT session date** and **analyst.**
- **Confirmation** that the ML team's fairness report matches WIT's per-group output.
- **Findings** — per-group observations that add to or contradict the fairness report.
- **Counterfactual observations** — up to five illustrative counterfactuals with the flipping feature and analyst commentary.
- **Proxy-variable candidates** — features with suspicious partial-dependence patterns.
- **Threshold-fragility check** — does the profile change materially with a small threshold move.
- **Recommended follow-ups** — the specific asks routed to the ML team.

## When WIT is not the right tool

- **Generative-AI systems.** WIT is built for classifiers. Generative-output evaluation is a different tooling category (see chapter 04 of `mod-107` for eval-report reading).
- **Very large feature spaces.** WIT is interactive; hundreds of features become unwieldy. The ML team subsets to the relevant slice before hand-off.
- **Sensitive data.** Some datasets cannot be loaded into a WIT session without additional access controls. Coordinate with the ML team on a de-identified sample.
- **When the analyst has no time.** A 45-minute WIT walk is real work. If the review must be summarised in ten minutes, read the Fairlearn/AIF360 report and defer WIT to a follow-up.

## Concrete example — a résumé-triage WIT walk

Continuing the residual example from chapter 02. The ML team hands over a WIT notebook.

- Sliced by sex → per-group confusion matrices match the Fairlearn report.
- Sliced by intersection of sex × education level → the model's precision differs more within each sex band than across, suggesting an education-related driver. Flagged.
- Counterfactual on a female applicant with a 4-year gap: nearest counterfactual differs on "gap length: 0 years" and flips the prediction. Flagged as a parental-status proxy candidate.
- Partial-dependence plot for "postgraduate institution" shows a bimodal shape suggesting the model has learned prestige signal that overlaps with race. Flagged as a proxy-variable candidate.
- Threshold sweep: at the enterprise's chosen threshold, disparate-impact ratio is 0.67. A small threshold move (0.05 lower) brings the ratio to 0.79 — still below four-fifths, still triggering; but the profile is fragile. Flagged.

WIT note attaches to `RR-2026-0219 — Résumé triage disparate impact.` The ML team follows up on the three flagged areas.

## What to memorise

- The **four analyst-relevant capabilities**: per-datapoint inspection, counterfactuals, partial-dependence, per-group performance.
- The **45-minute WIT session structure** — confirm attribute → slice-by → ROC/PR per group → sample counterfactuals → partial-dependence → threshold sweep → record.
- The **counterfactual reading rules** — small change flipping the prediction is the finding; proxy features surface here.
- The **proxy-candidate list** — ZIP, education, employment gap, language, employer.
- The **WIT-not-suitable list** — generative systems; enormous feature spaces; sensitive data without controls.

## Summary

The What-If Tool is the analyst's code-free window into a classifier's per-group behaviour. A 45-minute WIT session confirms the fairness report is complete, surfaces proxy-variable candidates the aggregate metrics missed, and produces counterfactuals that add per-datapoint evidence to the register. The analyst's WIT note is a short structured record attached to the governance file; the methodology depth belongs to `ai-risk-engineer`, and the legal determinations belong to counsel. When WIT is not suitable — generative systems, huge feature spaces, uncontrolled sensitive data — the analyst defers to eval-report reading and route to the appropriate specialist.
