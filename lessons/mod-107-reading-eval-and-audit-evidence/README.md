# mod-107 — Reading Eval, Red-Team, and Audit Evidence into Governance Records

**Estimated effort:** 10 hours

Every inventory row, register entry, impact assessment, fairness-review note, and tracker row the analyst has authored to this point in the track was written against a set of *mitigations claimed* — not *evidence that the mitigations worked*. This module is the discipline that closes the loop. It teaches the analyst to read the three most common eval-and-audit report shapes (Inspect-style capability / safety evals, RAG-triad quality evals, red-team engagement reports), to read the two most common public reference artefacts (vendor system cards and Responsible Scaling Policy / Preparedness-Framework disclosures), and to turn each into a per-system evidence row that a governance council, an external auditor, and a release-assurance engineer can trust.

The role's stance in this module is reader-and-summariser, not producer. `ai-evaluation-engineer`, `ai-red-team-engineer`, and `ai-risk-engineer` produce the evidence; the analyst reads it, benchmarks it against public references, packages it into a review packet for release-assurance sign-off, and escalates the gaps.

## Learning objectives

- Read an AISI-style Inspect eval report, an internal RAG-triad eval report, or a red-team engagement report enough to summarise the residual-risk claim, the threshold-decision rationale, and the unresolved findings into a governance-record row.
- Read a public system card (OpenAI GPT-4 / GPT-5 style, Anthropic Claude style) and a Responsible Scaling Policy disclosure enough to benchmark internal artifacts against them.
- Package the analyst-tier summary + source-artefact link + open-follow-up list into a review packet, and hand it to `ai-evaluation-engineer` for release-assurance sign-off.
- Recognise the delegation boundary: this role reads the evidence; `ai-evaluation-engineer` / `model-evaluation-engineer` / `ai-risk-engineer` produce it.
- Escalate an under-evidenced claim, a mis-scoped eval, or a stale eval to the ML / product owner and the governance council.

## Chapters

| # | Chapter | Focus |
|---|---|---|
| 01 | [The Analyst's Scope on Eval, Red-Team, and Audit Evidence](01-analyst-scope-on-eval-and-audit-evidence.md) | Role stance (reader, not producer); the three load-bearing claims (residual-risk / threshold-decision rationale / unresolved findings); the delegation map preview; vocabulary |
| 02 | [Inspect-Style Eval Report Anatomy](02-inspect-style-eval-report-anatomy.md) | UK AISI's Inspect framework as the reference shape; task / dataset / solver / scorer / model / sample / log / metric primitives; the fourteen expected sections; where the three claims live |
| 03 | [RAG-Triad and Retrieval-Quality Eval Reports](03-rag-triad-and-quality-eval-reports.md) | TruLens RAG triad (context relevance, groundedness, answer relevance); RAGAS and DeepEval extensions; the four version dimensions of a RAG system; negative-query subset as load-bearing |
| 04 | [Red-Team Engagement Reports](04-red-team-engagement-reports.md) | Adversarial evaluation vs benchmarks; OWASP LLM Top 10 / MITRE ATLAS / NIST AI 600-1 taxonomy references; finding-record shape; severity rubrics; mitigation-vs-validation distinction |
| 05 | [Summarising Eval Evidence into a Governance-Record Row](05-summarising-eval-evidence-into-a-governance-row.md) | The nineteen-column `EVAL-<year>-<sequence>` row schema across identity, system-under-eval, three claims, cross-artefact references, provenance, cadence, and governance-package fields |
| 06 | [Reading Public System Cards](06-reading-public-system-cards.md) | Public exemplars (OpenAI GPT-4 / GPT-4V / o1 / GPT-4o / GPT-5-series; Anthropic Claude 3 / 3.5 / 4-series; DeepMind Gemini; Meta Llama); twelve common sections; the *vendor-system-card* row |
| 07 | [Responsible Scaling Policies and Preparedness Frameworks](07-responsible-scaling-policies-and-preparedness-frameworks.md) | Anthropic RSP / OpenAI Preparedness Framework / DeepMind Frontier Safety Framework — three vocabularies, one shape; the *vendor-rsp-disclosure* row |
| 08 | [Benchmarking Internal Artifacts Against Public References](08-benchmarking-internal-artifacts-against-public-references.md) | The `BENCH-<year>-<sequence>` row; four axes (category coverage / threshold alignment / deployment-consideration honour / external-evaluator alignment); gap-list output |
| 09 | [Composing and Handing Off the Review Packet](09-composing-and-handing-off-the-review-packet.md) | Per-release-gate packet; eight sections; pre-hand-off completeness check; hand-off protocol with `ai-evaluation-engineer`; multi-system continuity |
| 10 | [Delegation Boundary and Escalation Patterns](10-delegation-boundary-and-escalation-patterns.md) | Full statement of the delegation boundary; four escalation classes (under-evidenced / mis-scoped / stale / packet-cannot-be-handed-off); the escalation register; recurring-pattern policy work |

## Exercises

Hands-on prompts; solutions live in the paired `ai-governance-analyst-solutions` repository.

| # | Exercise | Estimated |
|---|---|---|
| 01 | [Eval Report Reading Drill](exercises/exercise-01-eval-report-reading-drill.md) | 2 h |
| 02 | [System Card Comparative Reading](exercises/exercise-02-system-card-comparative-reading.md) | 2 h |
| 03 | [Review Packet Composition](exercises/exercise-03-review-packet-composition.md) | 2 h |
| 04 | [Delegation Boundary Drill](exercises/exercise-04-delegation-boundary-drill.md) | 2 h |

## Lab

- `lab-01` — Not yet authored; scheduled for the next content cycle.

## Quiz

- Knowledge check per the curriculum plan. Not yet authored; scheduled for the next content cycle.

## Resources

Curated primary references are in [`resources.md`](resources.md).

## Prerequisites

Fluency in `mod-101` (NIST AI RMF, ISO/IEC 42001, EU AI Act tiers, role scope — the delegation boundary this module makes operational), `mod-102` (inventory rows the eval-evidence rows attach to), `mod-103` (register entries the eval-evidence rows update), `mod-104` (fairness-review notes and the fairness-eval reading vocabulary), `mod-105` (impact-assessment corpus and the model-card / system-card / datasheet artefact family), and `mod-106` (regulatory tracker rows that link to RSP disclosures and to vendor-card claims).

## Downstream dependencies

- `mod-108-controls-and-compliance-evidence` — control assertions of the *evaluated-and-below-threshold* type cite eval-evidence rows produced in this module.
- `mod-109-incident-response-and-continuous-monitoring` — incident-response reads eval unresolved-findings for post-market surveillance prioritisation; continuous monitoring reads last-verified dates to catch stale rows.
- `mod-110-communication-and-council-support` — council briefings quote the analyst-tier summary and the benchmark gap list; the escalation-register roll-up feeds the council's policy-work agenda.
- `project-101` — the end-to-end deliverable set uses eval-evidence rows and review packets as the release-assurance backbone.
