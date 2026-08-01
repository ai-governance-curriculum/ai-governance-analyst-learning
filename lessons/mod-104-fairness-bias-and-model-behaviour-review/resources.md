# Resources — mod-104 Reading Fairness, Bias, and Model-Behaviour Reports

## Fairness-metric primary literature

- [Hardt, Price, and Srebro (2016) — "Equality of Opportunity in Supervised Learning"](https://arxiv.org/abs/1610.02413) — the original equalised-odds and equal-opportunity paper.
- [Chouldechova (2017) — "Fair Prediction with Disparate Impact"](https://arxiv.org/abs/1703.00056) — one of the two canonical impossibility-result papers, framed around recidivism risk.
- [Kleinberg, Mullainathan, and Raghavan (2016) — "Inherent Trade-offs in the Fair Determination of Risk Scores"](https://arxiv.org/abs/1609.05807) — the other canonical impossibility-result paper.
- [Dwork, Hardt, Pitassi, Reingold, Zemel (2012) — "Fairness Through Awareness"](https://arxiv.org/abs/1104.3913) — the individual-fairness framing.
- [Barocas, Hardt, Narayanan — "Fairness and Machine Learning" (open textbook)](https://fairmlbook.org/) — the standing reference for the definitions used in analyst-facing reports.

## Fairness tooling

- [Fairlearn](https://fairlearn.org/) — Microsoft-led open-source fairness library; the `MetricFrame` API is the analyst's default read shape.
- [Fairlearn user guide — Fairness in Machine Learning](https://fairlearn.org/main/user_guide/fairness_in_machine_learning.html) — definitional cross-reference for the metric families.
- [AI Fairness 360 (AIF360)](https://aif360.readthedocs.io/) — IBM-led open-source library; adds bias-mitigation-algorithm scaffolding.
- [Google What-If Tool (WIT)](https://pair-code.github.io/what-if-tool/) — PAIR's code-free per-group exploration tool; TensorBoard plugin, Jupyter widget, Colab demo.
- [Google PAIR AI Explorables — Measuring Fairness](https://pair.withgoogle.com/explorables/measuring-fairness/) — visual intuition builder for the metric trade-offs.
- [Google PAIR AI Explorables — Hidden Bias](https://pair.withgoogle.com/explorables/hidden-bias/) — proxy-variable intuition builder.
- [Google PAIR People + AI Guidebook](https://pair.withgoogle.com/guidebook/) — human-centered framing for why counterfactuals and per-group behaviour matter to stakeholders.

## US federal statutory and regulatory anchors

- [Title VII of the Civil Rights Act (1964)](https://www.eeoc.gov/statutes/title-vii-civil-rights-act-1964) — protected-classes framing.
- [EEOC Uniform Guidelines on Employee Selection Procedures](https://www.eeoc.gov/uniform-guidelines-employee-selection-procedures) — the four-fifths rule and the burden-shift structure.
- [EEOC — Select Issues: Assessing Adverse Impact in Software, Algorithms, and Artificial Intelligence (May 2023)](https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial) — the 2023 EEOC AI guidance the analyst cites at intake.
- [EEOC — Americans with Disabilities Act and the Use of Software, Algorithms, and Artificial Intelligence to Assess Job Applicants and Employees (2022)](https://www.eeoc.gov/laws/guidance/americans-disabilities-act-and-use-software-algorithms-and-artificial-intelligence) — ADA-flavoured companion to the 2023 adverse-impact guidance.
- [Age Discrimination in Employment Act (ADEA)](https://www.eeoc.gov/statutes/age-discrimination-employment-act-1967) — age-band protected-class framing.

## US state and local overlays for hiring AI

- [NYC Local Law 144 — Automated Employment Decision Tools](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) — the NYC AEDT rule, in force since 5 July 2023.
- [Illinois Artificial Intelligence Video Interview Act](https://www.ilga.gov/legislation/publicacts/101/101-0260.htm) — AI-in-video-interview notification, consent, and retention rules.
- [Maryland HB 1202 (2020)](https://mgaleg.maryland.gov/mgawebsite/Legislation/Details/hb1202?ys=2020rs) — facial-recognition restrictions in job interviews.
- [Colorado SB 24-205 — Consumer Protections for Artificial Intelligence](https://leg.colorado.gov/bills/sb24-205) — first US-state comprehensive AI act with consequential-decision-tool obligations.
- [California legislature bill search](https://leginfo.legislature.ca.gov/) — California's evolving AI-in-employment statutes. <!-- needs-research: track the currently-enacted California AI-in-employment statute and its effective date; AB 2930 / SB 942 / successor bills have moved through the legislature multiple times. -->

## Financial-services and consumer-finance overlays touching fairness

- [ECOA / Regulation B](https://www.consumerfinance.gov/rules-policy/regulations/1002/) — consumer-credit non-discrimination and adverse-action framing.
- [CFPB Circular 2022-03 on adverse action notification](https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/) — reason-code requirements for complex-algorithm decisions.

## EU and UK overlays

- [EU AI Act (Regulation (EU) 2024/1689)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — Annex III item 4 attaches recruitment / selection to high-risk; Articles 26, 27, 50 carry the deployer obligations, FRIA, and transparency requirements.
- [GDPR Article 22 — Automated Decision-Making](https://gdpr-info.eu/art-22-gdpr/) — the right not to be subject to a decision based solely on automated processing.
- [UK Equality Act 2010 — guidance](https://www.gov.uk/guidance/equality-act-2010-guidance) — UK analogue to the Title VII disparate-impact frame.
- [UK ICO — AI and data protection guidance](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/) — regulator guidance on fairness testing in AI systems.

## NIST anchors reused across the module

- [NIST AI RMF 1.0 (AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) — MEASURE function is where fairness metrics land in the RMF.
- [NIST AI RMF Generative AI Profile (AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — GenAI-specific bias framing (Sections 2.4, 2.6).
- [NIST SP 1270 — Towards a Standard for Identifying and Managing Bias in AI](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.1270.pdf) — systemic / statistical / human-cognitive bias framing that sits behind the metric vocabulary.

## Datasets used in the exercises

- [UCI Adult / Census Income dataset](https://archive.ics.uci.edu/dataset/2/adult) — canonical fairness-tutorial dataset.
- [COMPAS recidivism dataset (ProPublica repo)](https://github.com/propublica/compas-analysis) — the ProPublica investigation's dataset and reproducible analysis notebooks.
- [ProPublica "Machine Bias" (2016)](https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing) — original investigation.
- [Northpointe / Equivant response](https://www.equivant.com/response-to-propublica-demonstrating-accuracy-equity-and-predictive-parity/) — the developer rebuttal; reading both together is where the impossibility-result frame lands hardest.
- [UCI Bank Marketing dataset](https://archive.ics.uci.edu/dataset/222/bank+marketing) — lower-stakes alternative for the fairness reading drill.

## Generative-output bias measurement (for the recognition-level analyst)

- [Stanford HELM](https://crfm.stanford.edu/helm/) — holistic evaluation of language models including per-group bias metrics.
- [BOLD — Bias in Open-ended Language Generation Dataset](https://github.com/amazon-research/bold) — sentiment / regard bias probes across demographic axes.
- [StereoSet](https://stereoset.mit.edu/) — stereotype / association bias benchmark for LMs.
- [BBQ — Bias Benchmark for QA](https://github.com/nyu-mll/BBQ) — ambiguous-context stereotype-reliance benchmark.

## Deferred-depth references

Depth-owning tracks the analyst hands off to.

- [ai-risk-engineer](https://github.com/ml-engineering-curriculum/ai-risk-engineer-learning) — bias-audit methodology design, mitigation algorithm selection, red-team data generation.
- [ai-evaluation-engineer](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-learning) — eval methodology for generative-output bias.
- [senior-ai-governance-architect](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) — fairness-metric-choice governance decisions; enterprise threshold-setting.

## What is deliberately not here

- Blog-post summaries of the EEOC guidance, LL 144, or the EU AI Act — read the primary text.
- Vendor marketing whitepapers that present "our tool is unbiased" as evidence — the analyst-tier discipline is to read primary metrics against primary thresholds.
- One-shot fairness "certification" services that produce a green tick without disclosing the metric choice — chapter 01 is explicit that a fairness claim without a named axis is under-specified.
