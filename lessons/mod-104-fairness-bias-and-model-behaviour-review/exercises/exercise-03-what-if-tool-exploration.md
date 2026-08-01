# Exercise 03 — What-If Tool Exploration

**Estimated effort:** 2 hours
**Grounding chapter:** [03 — The Google What-If Tool — Code-Free Per-Group Exploration](../03-what-if-tool-code-free-exploration.md)

## Objective

Run the **45-minute structured WIT walk** from chapter 03 against a classifier and evaluation dataset, produce the analyst-tier WIT note, and identify at least one finding (counterfactual, proxy-variable candidate, or threshold-fragility observation) that the aggregate fairness metrics from exercise 02 did *not* surface.

After this exercise you should be comfortable opening a What-If Tool session the ML team hands over, running a structured walk in under an hour, and producing a note that adds per-datapoint evidence to a bias-review record already anchored on aggregate metrics.

## Prerequisites

- Chapter 03 read; the four analyst-relevant capabilities and the 45-minute walk sequence fresh in memory.
- Exercise 02 completed — the classifier and evaluation dataset from exercise 02 is your target system here. If you did not do exercise 02, use one of its recommended datasets (UCI Adult, COMPAS, Bank Marketing).
- A working [What-If Tool](https://pair-code.github.io/what-if-tool/) environment. Three options:
  - **Colab.** The [WIT Colab demo](https://colab.research.google.com/github/PAIR-code/what-if-tool/blob/master/WIT_Smile_Detector.ipynb) is the quickest path — you can adapt it to point at your own model and dataset.
  - **Jupyter widget.** `pip install witwidget`, then follow the [WIT Jupyter setup](https://github.com/PAIR-code/what-if-tool#how-do-i-use-it).
  - **TensorBoard plugin.** Requires a served TensorFlow model; slower to set up but the reference environment for enterprise use.
- The [PAIR AI Explorables — Measuring Fairness](https://pair.withgoogle.com/explorables/measuring-fairness/) and [Hidden Bias](https://pair.withgoogle.com/explorables/hidden-bias/) as intuition-builders — 15 minutes each.
- Optional: [Google PAIR "People + AI Guidebook"](https://pair.withgoogle.com/guidebook/) for the human-centered framing on why counterfactuals matter to stakeholders.

## Problem statement

The exercise has three parts: run the walk, author the WIT note, and produce a comparison memo between the aggregate-metric bias-review note (from exercise 02) and the per-datapoint WIT note (from this exercise).

### Part A — set up the WIT session

Choose one of the three environments (Colab is fastest) and load:

- The classifier you trained in exercise 02.
- The evaluation dataset with the protected attribute(s) present as columns.

If the WIT setup does not load in 20 minutes of effort, that is a real analyst-tier signal — chapter 03 says the analyst does not run the setup and treats a broken hand-off as a stop-and-flag. For this exercise, however, you *are* also the ML team; keep going, but write down in the WIT note what you would have flagged if the hand-off had come from someone else.

Record:

- The environment (Colab / Jupyter / TensorBoard) and the WIT version.
- The dataset row count and the protected attribute(s).
- The link to the notebook or a screenshot of the WIT interface loaded on your data.

### Part B — run the structured walk and take screenshots

Chapter 03's 45-minute walk sequence, executed step by step. For each step, take one screenshot (or copy the relevant numbers into the note) and write one to three sentences on what you observed.

1. **Open the datapoint editor.** Confirm the protected attribute column is present. Note the count of unique values. Flag any missing or clearly proxy attribute (ZIP for race, etc.).
2. **Enable the performance panel; slice by the protected attribute.** Compare the per-group confusion matrices to the Fairlearn report from exercise 02. Confirm they match (they should — if they do not, one of the two is wrong; investigate).
3. **View ROC / precision-recall curves per group.** Note whether the curves overlap or separate. Separated curves are an equalised-odds visualisation; write down the direction of the disparity.
4. **Sample five to ten datapoints per group.** For each, note: the predicted class, the confidence, the nearest counterfactual, and what feature the counterfactual differs on. Flag any counterfactual whose flipping feature is a plausible protected-attribute proxy.
5. **Explore feature partial-dependence plots** for at least three features. Prioritise features chapter 03 flags as classic proxies (ZIP / postcode, educational institution, employment-gap length, employer name, language spoken) if your dataset has any. Note the shape of each plot and whether the model appears to lean strongly on that feature.
6. **Threshold sweep.** Move the classification threshold across at least three points (default, +0.05, −0.05). For each, note the effect on the disparate-impact ratio and TPR difference. Flag if the profile is *fragile* — meaning a small threshold move changes the verdict from breach to clean or vice versa.
7. **Record findings.** Assemble the observations into the WIT note (Part C).

Screenshot naming convention: `wit-step-01-datapoint-editor.png` through `wit-step-06-threshold-sweep.png`. If screenshotting is impractical (Colab file management, private data), transcribe the numbers into the note instead — the intermediate step of *looking* is what the exercise is testing.

### Part C — author the WIT note

Author `wit-note.md` with the chapter 03 shape. Every section is filled; no `TBD`.

- **System reviewed** and **evaluation dataset** — the same header as the exercise-02 bias-review note.
- **WIT session date** and **analyst** (you).
- **Environment** — Colab / Jupyter / TensorBoard, WIT version.
- **Confirmation** that the WIT per-group output matches the exercise-02 Fairlearn per-group output — or, if it does not, the reconciliation note.
- **Findings** — a numbered list. Each finding is one paragraph in the shape *observation × where in the WIT session it was surfaced × verdict × downstream implication*. Include per-group observations that add to or contradict the exercise-02 report.
- **Counterfactual observations** — up to five illustrative counterfactuals, each with the flipping feature and one to two sentences of analyst commentary. Distinguish counterfactuals where the flipping feature is a plausible proxy from counterfactuals where it is a legitimate signal.
- **Proxy-variable candidates** — a short list of features whose partial-dependence plot suggests the model has learned proxy signal. For each, name the protected attribute it may be proxying for and note the ask that would go to the ML team.
- **Threshold-fragility check** — one paragraph on whether the enterprise's chosen threshold is defensible or fragile.
- **Recommended follow-ups** — a short list of asks routed to the ML team, each with a proposed scope and a note that the *methodology* belongs to `ai-risk-engineer` and the *legal determination* belongs to Legal.
- **Sign-off block** — analyst name, date, review status.

Target length: 800–1,500 words. Longer than that and you are re-writing chapter 03 rather than reporting a session; shorter than that and the session was not deep enough.

### Part D — the aggregate-vs-per-datapoint comparison memo

Author a short (300–500 word) `wit-vs-fairlearn-comparison.md` that answers three questions:

- **What did WIT surface that Fairlearn did not?** Name at least one finding — a counterfactual pattern, a proxy-variable candidate, a threshold-fragility observation.
- **What did Fairlearn surface that WIT did not?** Aggregate metrics with confidence framing; sample-size caveats; the intersectional table. Name at least one.
- **How do the two artefacts sit together in the governance record?** The aggregate report is the *anchor*; the WIT note is the *per-datapoint evidence*. Both are cited from the register entry. Write out how you would file both.

The comparison memo is short on purpose — it is a reflection artefact for the analyst, not a stakeholder-facing document.

## Requirements

- **The WIT session loaded on the exercise-02 classifier.** Screenshots or transcribed numbers show the session actually ran; the note is not authored from chapter-03 examples.
- **All seven walk steps executed and reported.** Every step has one to three sentences on what was observed; no step is silently skipped.
- **At least one finding is genuinely from WIT** and not derivable from the exercise-02 Fairlearn report. This is the point of the exercise — WIT earns its 45 minutes by surfacing something the aggregate metrics did not.
- **Counterfactual observations distinguish proxy candidates from legitimate signals.** No counterfactual is reported as *the model is unfair* on the strength of one datapoint — chapter 03 is explicit that per-datapoint evidence is a *route to the ML team*, not a determination.
- **Proxy-variable candidates use the chapter 03 checklist** (ZIP, education, employment gap, language, employer) as a starting-point filter. If your dataset has none of these, name the closest analogue.
- **Threshold-fragility check produces a verdict, not just a table.** Name whether the profile is fragile at the enterprise's chosen threshold and whether that changes the analyst's remediation ask.
- **The comparison memo is honest.** If WIT surfaced nothing the aggregate metrics did not, say so — that is a finding in itself, and it is the honest answer if the classifier and dataset are simple.
- **No fabricated statute references, incident citations, or vendor names.** Uncertain claims marked `<!-- needs-research: -->`.
- **The sign-off block treats the exercise as a draft**, not a filed governance artefact — this is a learner-tier reproduction.

## Starter guidance

- Do not try to master the entire WIT interface before starting. Load the demo notebook, get *your* data into it, and start walking. WIT is designed to be explored — the walk sequence is the scaffolding.
- The performance panel is the most valuable early step. If your per-group confusion matrices in WIT do not match the Fairlearn per-group output from exercise 02, one of them has a bug — usually a mismatch in how the protected attribute is encoded. Fix it before continuing.
- For counterfactuals, WIT surfaces the nearest neighbour under an L1 or L2 distance. That is not the same as the *nearest fair counterfactual* — it is the nearest counterfactual in *feature space*. Chapter 03's caveat holds: a counterfactual on a plausible proxy is a finding, not a determination.
- Partial-dependence plots are the fastest proxy-variable filter. For each feature, look for a monotonic-and-steep shape or a step-function shape — those suggest the model has learned a hard boundary the analyst can ask about.
- For the threshold sweep, small moves (+/-0.05 or +/-0.10) are usually enough. If the enterprise threshold sits at the *knee* of the disparate-impact-ratio-vs-threshold curve, the choice is fragile; that is the fragility finding.
- On environment friction: if you spend more than 30 minutes fighting WIT setup, switch to a different environment (Colab is the fallback) and write down the friction in the WIT note. That friction is realistic — vendors and ML teams sometimes hand over a WIT link that does not load, and the analyst-tier response is to flag rather than to spend the review budget on setup.

## Acceptance criteria

- `mod-104-ex-03/wit-note.md` — the analyst-tier WIT note with all sections filled, 800–1,500 words.
- `mod-104-ex-03/wit-vs-fairlearn-comparison.md` — the 300–500 word comparison memo.
- Screenshots or transcribed numbers for each of the seven walk steps in a `mod-104-ex-03/session-artefacts/` directory (or referenced inline in the WIT note).
- At least one finding surfaced by WIT that is not present in the exercise-02 Fairlearn report.
- Counterfactual observations distinguish proxy candidates from legitimate signals, with the flipping feature and analyst commentary for each.
- Threshold-fragility check produces a verdict.
- Every uncertain claim marked `<!-- needs-research: -->`. No fabricated statutes, incidents, or vendor names.

## Stretch goals

- **A second WIT session on the mitigated model.** If you completed the exercise-02 stretch mitigation pass, run WIT against the mitigated model and write a paragraph on how the per-datapoint behaviour changed. Sometimes the aggregate metrics improve while the per-datapoint proxy signal stays put; sometimes both improve; sometimes proxy signal shifts to a different feature. This is where fairness intuition matures.
- **A "WIT is not the right tool" note.** Take one of the chapter 03 not-suitable cases (generative-AI system; very large feature space; sensitive data without controls) and write a one-page note on the shape of the alternative artefact the analyst would file instead. Preview work for `mod-107`.
- **A proxy-variable evidence pack.** For each proxy-variable candidate in your WIT note, write a short (100-word) evidence paragraph citing the literature or a regulator's guidance on why that feature is a proxy. Examples: ZIP code as a race proxy is cited in [HUD housing-discrimination case law](https://www.hud.gov/); educational institution as a socio-economic proxy is cited in [OECD education research](https://www.oecd.org/education/). Do not fabricate case citations.
- **A stakeholder walk-through slide.** Take one counterfactual from your WIT note and turn it into a single slide that explains it to a non-technical stakeholder. Preview work for `mod-110`.
- **A WIT-notebook template.** Extract a reusable WIT session template from your notebook — headers, placeholders, and a checklist per walk step — that a peer analyst could adapt to a different system. Publish it as `mod-104-ex-03-wit-template.ipynb`.

## Deliverables

- `mod-104-ex-03/wit-note.md`.
- `mod-104-ex-03/wit-vs-fairlearn-comparison.md`.
- `mod-104-ex-03/session-artefacts/` — screenshots or transcribed numbers per walk step.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo runs WIT against the UCI Adult classifier from the exercise-02 reference solution and produces a WIT note with a proxy-variable candidate (education level) and a threshold-fragility finding. Your findings will differ; what should not differ is that the seven walk steps were actually executed, that at least one finding is genuinely WIT-surfaced, and that per-datapoint observations are treated as routes to the ML team rather than as determinations. A short honest WIT note that says "WIT confirmed the aggregate findings and surfaced no new proxy candidates" is a passing deliverable if the seven steps are all evidenced. A dazzling WIT note whose findings turn out to be re-statements of the Fairlearn output is not.
