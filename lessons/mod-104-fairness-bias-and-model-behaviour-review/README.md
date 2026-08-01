# mod-104 — Reading Fairness, Bias, and Model-Behaviour Reports

**Estimated effort:** 10 hours

Fairness reports are handed to the analyst by the ML team, by vendors, and by independent auditors. The analyst does not run the numbers, but the analyst reads the numbers, summarises them for a non-technical stakeholder, verifies the report is complete, and opens the remediation ticket when a threshold is breached. This module walks the vocabulary (demographic parity, equalised odds, calibration, four-fifths rule), the tooling (Fairlearn, AIF360, the What-If Tool), and the two hiring-AI overlays (NYC LL 144, EEOC Title VII) an analyst is most likely to encounter in the first year.

## Learning objectives

- Read Fairlearn / AIF360 outputs and vendor bias-audit reports — demographic parity, equalised odds, calibration by group, four-fifths rule, disparate-impact ratio — well enough to summarise them for a non-technical stakeholder.
- Use the Google What-If Tool to explore a classifier's per-group behaviour without writing code.
- Explain the NYC Local Law 144 bias audit shape and the EEOC Title VII adverse-impact framing at a level sufficient to intake a hiring-AI use case.
- Open a remediation ticket against the ML team with a concrete finding, a threshold breach, and a proposed follow-up scope — knowing that designing the bias-audit methodology belongs to [ai-risk-engineer](https://github.com/ml-engineering-curriculum/ai-risk-engineer-learning).
- Recognise when a claim of fairness is under-evidenced (metric-single-point, missing base rates, missing sub-group breakdown, missing calibration check) and escalate.

## Chapters

| # | Chapter | Focus |
|---|---|---|
| 01 | [The Fairness Metric Glossary — And What Each One Cannot Tell You](01-fairness-metric-glossary-and-limits.md) | Demographic parity, equalised odds, calibration, four-fifths rule; the impossibility result; generative-output biases |
| 02 | [Reading Fairlearn, AIF360, and Vendor Bias-Audit Reports](02-reading-fairlearn-and-aif360-reports.md) | Report shape; five-thing reading pass; common omissions; the five-question non-technical summary |
| 03 | [The Google What-If Tool — Code-Free Per-Group Exploration](03-what-if-tool-code-free-exploration.md) | 45-minute WIT session; counterfactuals; proxy-variable detection; the WIT note |
| 04 | [Hiring AI — NYC Local Law 144, EEOC Title VII, and the Analyst Overlay](04-hiring-ai-overlays-ll144-eeoc.md) | Title VII disparate impact; the EEOC 2023 AI guidance; LL 144 four obligations; EU AI Act Annex III |

## Exercises

Hands-on prompts; solutions live in the paired `ai-governance-analyst-solutions` repository.

| # | Exercise | Estimated |
|---|---|---|
| 01 | [Fairness Metric Glossary and Limits](exercises/exercise-01-fairness-metric-glossary-and-limits.md) | 2 h |
| 02 | [Fairlearn Report Reading Drill](exercises/exercise-02-fairlearn-report-reading-drill.md) | 2 h |
| 03 | [What-If Tool Exploration](exercises/exercise-03-what-if-tool-exploration.md) | 2 h |
| 04 | [NYC LL 144 and EEOC Hiring Drill](exercises/exercise-04-nyc-ll144-and-eeoc-hiring-drill.md) | 2 h |

## Lab

- `lab-01` — Not yet authored; scheduled for the next content cycle.

## Quiz

- Knowledge check per the curriculum plan. Not yet authored; scheduled for the next content cycle.

## Resources

Curated primary references are in [`resources.md`](resources.md).

## Prerequisites

Fluency in `mod-101` (RMF, GenAI Profile, ISO 42001), `mod-102` (intake, inventory, tier tagging), and `mod-103` (register scoring). The bias-review note is a downstream artefact that sits on top of the register entry authored in `mod-103`.

## Downstream dependencies

- `mod-105-impact-assessments-and-model-cards` — the bias-review note is cited from the FRIA / AIA / model card.
- `mod-107-reading-eval-and-audit-evidence` — deepens eval-report reading, including generative-output evaluation which sits beyond WIT's frame.
- `mod-108-controls-and-compliance-evidence` — maps the "remediation ticket" shape into the enterprise control library.
- `mod-109-incident-response-and-continuous-monitoring` — the residual detective controls proposed here become monitoring hooks.
- `mod-110-communication-and-council-support` — the five-question non-technical summary lands on council slides.
