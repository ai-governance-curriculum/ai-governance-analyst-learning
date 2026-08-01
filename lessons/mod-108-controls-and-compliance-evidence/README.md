# mod-108 — Controls, Compliance Evidence, and Third-Party AI Vendor Review

**Estimated effort:** 12 hours

Every artefact the analyst has authored to this point — the inventory row, the risk register entry, the fairness-review note, the impact assessment, the regulator-tracker row, the eval-evidence row — makes claims about what the enterprise *does*. This module is the discipline that shows the auditor *the enterprise actually did it*. It teaches the analyst to run a periodic control-testing cycle against the enterprise's already-published control library, to pull the evidence artefacts (config exports, log samples, eval-report links, sign-off records) from ML / infra / product owners, to attach them to control records in the GRC platform, to flag the evidence that has gone stale, and to produce a control-status report an internal auditor can pick up cold.

It also teaches the two horizontal disciplines the control cycle assumes as background. First, an *analyst-tier reading knowledge* of the AI/LLM security threat taxonomies — OWASP LLM Top 10, MITRE ATLAS, NIST AI 100-2, and Google's Secure AI Framework — deep enough to open a security-linked control record correctly and route it to `ai-infra-security`, not deep enough to reproduce the attack. Second, a *third-party AI vendor / model / dataset intake* workflow: reading vendor model cards, sub-processor lists, DPAs, ISO/IEC 42001 certification letters, and independent audit reports; producing a vendor-risk-register row that the vendor management office and downstream teams inherit.

The role's stance in this module: the analyst *runs* the cycle, *pulls* the evidence, *tags* the records, and *produces* the report. The analyst does not design the master control library — that is `senior-ai-governance-architect` scope. The analyst does not execute the security exploits, run the pentest, or draft the mitigation code — that is `ai-infra-security` scope. The analyst does not sign the vendor contract or approve the DPA — that is `procurement` / `legal` scope. The row and the report are the analyst's tangible outputs; the delegation boundary is chapter 09.

## Learning objectives

- Run periodic control-testing cycles: pull evidence artefacts (config exports, log samples, eval-report links, sign-off records) from the ML / infra / product teams; attach them to control-record entries in the GRC platform; flag stale evidence.
- Produce a control-status report an internal auditor can review — deferring control-library design to `senior-ai-governance-architect`.
- Recognise the top AI/LLM security threat categories (prompt injection, data exfiltration, model theft, membership inference, adversarial evasion, supply-chain, guardrail bypass) from OWASP LLM Top 10, MITRE ATLAS, NIST AI 100-2, and Google SAIF at a level sufficient to file a security-linked record and route to `ai-infra-security`.
- Run third-party AI vendor / model / dataset intake: review vendor model cards, sub-processor lists, DPAs, ISO/IEC 42001 certification letters, and independent audit reports; produce a vendor-risk-register row.
- Map controls across ISO/IEC 42001 clauses, NIST AI RMF sub-categories, EU AI Act obligations, SR 11-7 pillars, and the internal policy catalogue — building the analyst-tier crosswalk, not the master control library.
- Position ForHumanity and BABL AI as the two most-referenced independent-audit / bias-auditor credential bodies the analyst encounters.

## Chapters

| # | Chapter | Focus |
|---|---|---|
| 01 | [The Analyst's Scope on Controls and Compliance Evidence](01-analyst-scope-on-controls-and-compliance-evidence.md) | Role stance (cycle runner, not library designer); the two tangible outputs (control-status report + vendor row); delegation preview; vocabulary |
| 02 | [The Control-Testing Cycle and Evidence-Artefact Shape](02-control-testing-cycle-and-evidence-artefacts.md) | Cycle cadence per control class; six evidence-artefact classes (config export, log sample, eval-report link, sign-off record, screenshot, interview note); the pull protocol; the stale-evidence flag rules |
| 03 | [The Control-Status Report for Internal Audit](03-control-status-report-for-internal-audit.md) | The `CTL-<year>-<sequence>-<test-N>` row; the report shape internal audit expects; the analyst-tier "operating effectiveness" language; the hand-off to `senior-ai-governance-architect` for library-level fixes |
| 04 | [OWASP LLM Top 10 and the Analyst-Tier Taxonomy](04-owasp-llm-top-10-and-analyst-tier-taxonomy.md) | The 2025 list item-by-item; how each maps to an evidence-artefact class; the analyst's tagging rule; the file-and-route pattern to `ai-infra-security` |
| 05 | [MITRE ATLAS, NIST AI 100-2, and Google SAIF](05-mitre-atlas-nist-ai-100-2-and-google-saif.md) | Three complementary threat-taxonomy references; the seven top categories the analyst must recognise; recognition depth vs exploitation depth; when to cite which |
| 06 | [Third-Party AI Vendor, Model, and Dataset Intake](06-third-party-ai-vendor-and-model-intake.md) | Six vendor-evidence artefacts (model card, sub-processor list, DPA, ISO/IEC 42001 certification letter, independent audit report, security questionnaire response); the `VND-<year>-<sequence>` vendor-risk-register row schema |
| 07 | [The Controls Crosswalk — ISO/IEC 42001, NIST AI RMF, EU AI Act, SR 11-7, and the Internal Catalogue](07-controls-crosswalk-across-42001-rmf-eu-ai-act-sr-11-7.md) | The analyst-tier crosswalk (not the master control library); five column sources; the walk discipline; the hand-off boundary with `senior-ai-governance-architect` |
| 08 | [Independent-Audit and Bias-Auditor Credentialing — ForHumanity and BABL AI](08-independent-audit-and-bias-auditor-credentialing-forhumanity-and-babl-ai.md) | The two credential bodies the analyst encounters most; what a ForHumanity-independent audit report looks like; what a BABL-trained auditor typically produces; the NYC Local Law 144 through-line |
| 09 | [Delegation Boundary and Escalation Patterns](09-delegation-boundary-and-escalation-patterns.md) | Full delegation-boundary statement across `senior-ai-governance-architect`, `ai-infra-security`, `procurement` / `legal`, `internal-audit`; four escalation classes; the escalation register roll-up |

## Exercises

Hands-on prompts; solutions live in the paired `ai-governance-analyst-solutions` repository.

| # | Exercise | Estimated |
|---|---|---|
| 01 | [Control Cycle Analyst Runbook](exercises/exercise-01-control-cycle-analyst-runbook.md) | 2 h |
| 02 | [OWASP LLM Top 10 Tagging Drill](exercises/exercise-02-owasp-llm-top10-tagging-drill.md) | 2 h |
| 03 | [MITRE ATLAS and NIST AML Awareness](exercises/exercise-03-mitre-atlas-and-nist-aml-awareness.md) | 2 h |
| 04 | [Third-Party Vendor Questionnaire](exercises/exercise-04-third-party-vendor-questionnaire.md) | 2 h |
| 05 | [Control Crosswalk Matrix Drill](exercises/exercise-05-control-crosswalk-matrix-drill.md) | 2 h |

## Lab

- `lab-01` — Not yet authored; scheduled for the next content cycle.

## Quiz

- Knowledge check per the curriculum plan. Not yet authored; scheduled for the next content cycle.

## Resources

Curated primary references are in [`resources.md`](resources.md).

## Prerequisites

Fluency in `mod-101` (NIST AI RMF, ISO/IEC 42001, EU AI Act tiers, and the role scope this module operationalises against the control library), `mod-102` (inventory rows the control tests reference), `mod-103` (register entries the mitigations map to controls in), `mod-104` (fairness-review notes the bias-audit controls read from), `mod-105` (impact-assessment corpus that names the *measures* — an early source of control statements), `mod-106` (regulatory tracker rows that mark when a new obligation lands and a new control is needed), and `mod-107` (eval-evidence rows the *evaluated-and-below-threshold* controls cite).

## Downstream dependencies

- `mod-109-incident-response-and-continuous-monitoring` — post-market surveillance re-tests controls on incident; monitoring dashboards trip control-status changes; the control-status report is the first artefact incident-response reads to reconstruct what was in place.
- `mod-110-communication-and-council-support` — council briefings quote the control-status report's summary; the escalation register from this module feeds the council's policy-work agenda; the vendor-risk-register roll-up is a standing council item.
- `project-101` — the end-to-end deliverable set uses the control-status report and vendor row set as the compliance evidence backbone.
