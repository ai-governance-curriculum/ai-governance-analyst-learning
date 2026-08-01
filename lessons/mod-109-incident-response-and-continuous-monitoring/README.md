# mod-109 — AI Incident Response and Continuous Monitoring at the Analyst Tier

**Estimated effort:** 10 hours

Every artefact the analyst has produced through `mod-102`–`mod-108` describes the enterprise as it was *at the time the artefact was authored*. AI systems drift, degrade, get jailbroken, produce biased outputs, hallucinate, and are put to use in ways nobody wrote down. This module is the discipline that keeps the governance record honest about that: when something goes wrong, the analyst logs it against the register and the affected inventory row, coordinates the impact-assessment re-open, and packages the evidence for the governance council or internal auditor; when nothing has gone wrong yet, the analyst reads the continuous-monitoring dashboards well enough to sign off on the *operating* record and to spot the signal that needs to escalate before it becomes an incident. For systems inside the EU AI Act's high-risk scope, the analyst also files the periodic post-market surveillance summary and drafts the Article 73 serious-incident notification.

The role's stance in this module: the analyst is a *recorder, coordinator, and packager* — not the incident commander, not the monitoring designer, not the regulator's contact-of-record. Incident command sits with the ML / infra / product on-call for the technical containment work and with `head-of-ai-governance` for the enterprise-level decisions. Monitoring design sits with `ai-eval-engineer` and `ai-infra-mlops`. Signing and submitting a serious-incident notification to a market surveillance authority sits with the accountable executive named by the enterprise's EU AI Act compliance function. The analyst produces the artefacts these roles rely on, in a shape they can pick up cold; chapter 09 states the delegation boundary and the four escalation classes in full.

## Learning objectives

- Log an AI incident against the risk register, cross-reference the affected AI-system inventory row, coordinate an impact-assessment update, and package post-incident evidence for the governance council or internal auditor.
- Distinguish an AI-specific incident (model regression, jailbreak, prompt-injection exploitation, biased-outcome escalation, hallucination-driven harm, unauthorised model use) from a general software incident and route accordingly.
- Read continuous-monitoring dashboards (drift, quality, safety, cost) for a live AI system at a level sufficient to interpret them for governance sign-off — deferring monitoring design to `ai-eval-engineer` / `ai-infra-mlops`.
- File a post-market surveillance summary as required for high-risk systems under the EU AI Act (Articles 72 and 73).
- Recognise when a monitoring signal warrants escalation to `ai-risk-engineer`, `ai-infra-security`, or `head-of-ai-governance`.

## Chapters

| # | Chapter | Focus |
|---|---|---|
| 01 | [The Analyst's Scope on Incident Response and Continuous Monitoring](01-analyst-scope-on-incident-response-and-monitoring.md) | Role stance (recorder, coordinator, packager); the three tangible outputs (incident record, monitoring-reading note, PMS summary); delegation preview; vocabulary |
| 02 | [Distinguishing AI-Specific Incidents from General Software Incidents](02-ai-specific-incident-taxonomy.md) | The six AI-specific incident classes; the software-incident boundary; the routing rule per class; the *both-at-once* pattern |
| 03 | [Logging the Incident Against the Risk Register](03-incident-record-and-register-linkage.md) | The `INC-<year>-<sequence>` row schema; cross-refs to `INV`, `RISK`, `EV`, `CTL`, `IA`/`FRIA`/`DPIA`; intake, triage, post-mortem cadence |
| 04 | [Coordinating the Impact-Assessment Update](04-coordinating-impact-assessment-update.md) | When an incident triggers an IA / FRIA / DPIA re-open; the walk protocol; sign-off routing; the analyst's coordinating verb — not the drafter of the update |
| 05 | [Reading Continuous-Monitoring Dashboards for Governance Sign-off](05-monitoring-dashboards-for-governance-signoff.md) | The four panel families — drift, quality, safety, cost; analyst-tier reading depth; the monitoring-reading note; the deferral to `ai-eval-engineer` / `ai-infra-mlops` on design |
| 06 | [Monitoring-Signal Escalation Patterns](06-monitoring-signal-escalation-patterns.md) | When a signal warrants escalation to `ai-risk-engineer`, `ai-infra-security`, or `head-of-ai-governance`; escalation-trigger tables per panel family; the escalation record |
| 07 | [EU AI Act Post-Market Surveillance and Serious-Incident Reporting](07-eu-ai-act-post-market-surveillance.md) | Articles 72 and 73 at analyst-tier reading depth; the PMS summary shape; the serious-incident notification draft and its 15 / 10 / 2-day deadlines |
| 08 | [Post-Incident Evidence Packaging for Council and Internal Audit](08-post-incident-evidence-packaging.md) | The evidence-pack shape; the timeline reconstruction; the root-cause narrative in analyst voice; the hand-off protocol |
| 09 | [Delegation Boundary and Escalation Patterns](09-delegation-boundary-and-escalation-patterns.md) | Full delegation map; four escalation classes (incident-command handoff, monitoring redesign, regulator filing, council decision); pattern-recognition rules for recurring incidents |

## Exercises

Hands-on prompts; solutions live in the paired `ai-governance-analyst-solutions` repository.

| # | Exercise | Estimated |
|---|---|---|
| 01 | [AI Incident Taxonomy Drill](exercises/exercise-01-ai-incident-taxonomy-drill.md) | 2 h |
| 02 | [Incident Record Composition](exercises/exercise-02-incident-record-composition.md) | 2 h |
| 03 | [Monitoring Dashboard Reading Drill](exercises/exercise-03-monitoring-dashboard-reading-drill.md) | 2 h |
| 04 | [Post-Market Surveillance Summary](exercises/exercise-04-post-market-surveillance-summary.md) | 2 h |

## Lab

- `lab-01` — Not yet authored; scheduled for the next content cycle.

## Quiz

- Knowledge check per the curriculum plan. Not yet authored; scheduled for the next content cycle.

## Resources

Curated primary references are in [`resources.md`](resources.md).

## Prerequisites

Fluency in `mod-102` (the inventory rows the incident record cross-references), `mod-103` (the risk register the incident logs against and whose residuals may need re-opening), `mod-105` (the IA / FRIA / DPIA corpus whose re-open the incident may trigger), `mod-107` (the eval-evidence rows the post-mortem may cite as *evaluated but the signal missed the failure mode*), and `mod-108` (the control-status report the incident re-tests and the escalation register the incident's cross-role findings flow into). `mod-104` (fairness) is prerequisite specifically for reading a biased-outcome-escalation incident correctly. `mod-106` (regulator tracker) is prerequisite for the Article 72 / 73 chapter — the EU AI Act obligation must be tracked before the summary can be filed.

## Downstream dependencies

- `mod-110-communication-and-council-support` — the post-incident evidence pack is the primary input to any council briefing on the incident; the PMS summary and the escalation register roll up into council standing agenda items.
- `project-101` — the end-to-end deliverable set uses one worked incident record and one PMS-summary draft as the *system in operation* backbone.
