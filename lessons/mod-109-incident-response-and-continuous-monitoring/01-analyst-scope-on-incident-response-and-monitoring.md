# The Analyst's Scope on Incident Response and Continuous Monitoring

## Why this chapter

The analyst has by now populated the inventory (`mod-102`), the risk register (`mod-103`), the fairness-review notes (`mod-104`), the impact-assessment corpus (`mod-105`), the regulator tracker (`mod-106`), the eval-evidence row set (`mod-107`), and the control-status report and vendor-risk-register row set (`mod-108`). All of those artefacts describe the enterprise's AI estate *as it stood at the time each artefact was authored*.

Two facts about AI systems in operation make that snapshot insufficient:

1. **AI systems drift.** The model that passed the release-assurance eval two quarters ago is not the model on production today — retraining, prompt updates, base-model provider upgrades, retrieval-index refreshes, and traffic-mix changes all move the operating behaviour away from the evaluated behaviour.
2. **AI systems fail in AI-specific ways.** Model regressions, jailbreak success, prompt-injection exploitation, biased-outcome escalations, hallucination-driven harm, and unauthorised model use are not the incident types that classical software-incident response was designed around. Somebody in the governance function has to be the person who *recognises* the AI-specific failure mode, *records* it against the register and the inventory row, *coordinates* the impact-assessment update, and *packages* the evidence for governance and audit consumption. In the analyst role stack, that person is the analyst.

This chapter fixes the scope: what the analyst *does* on incidents and continuous monitoring, what the analyst *does not do*, the three tangible outputs the module reduces to, the vocabulary that recurs in chapters 02–09, and the delegation-map preview that chapter 09 states in full.

## What the analyst does on incidents and continuous monitoring

The analyst-tier verbs, in order:

1. **Recognises** whether a surfaced issue is AI-specific or a general software incident, and applies the routing rule per class (chapter 02). The recognition step is the analyst's — the analyst does not defer the classification to the on-call ML engineer, because the routing decision depends on governance vocabulary the on-call is not usually fluent in.
2. **Logs** the incident against the risk register with an `INC-<year>-<sequence>` identifier, cross-references the affected `INV-<year>-<sequence>` inventory row, and links the `RISK-<year>-<sequence>` register entries whose residual claims the incident calls into question (chapter 03).
3. **Coordinates** the impact-assessment (IA), fundamental-rights impact-assessment (FRIA), and data-protection impact-assessment (DPIA) re-open with the assessments' named owners, when the incident materially changes the assessment's factual basis (chapter 04). The analyst does not draft the update — the assessment's original owner does — but the analyst tracks it to completion.
4. **Reads** the continuous-monitoring dashboards for the affected system, and for the enterprise's live AI systems as a standing cadence, at a level sufficient to interpret them for governance sign-off (chapter 05). *Reading* here is the analyst-tier verb; *designing* the dashboard, the metrics, the thresholds, and the alerting is `ai-eval-engineer` / `ai-infra-mlops` scope.
5. **Escalates** the monitoring signals that warrant it — to `ai-risk-engineer` on model-behaviour degradation, to `ai-infra-security` on security-adjacent signals, to `head-of-ai-governance` on enterprise-level or council-decision-worthy signals (chapter 06).
6. **Composes** the periodic post-market surveillance (PMS) summary and drafts the serious-incident notification for any AI system in the EU AI Act's high-risk scope (chapter 07). The analyst drafts; the accountable executive named by the enterprise's EU AI Act compliance function signs and submits.
7. **Packages** the post-incident evidence pack — timeline, root-cause narrative in analyst voice, register / inventory / IA / control cross-references, evidence artefact links — for the governance council or the internal auditor (chapter 08).
8. **Re-tests** the controls the incident calls into question, out-of-cycle, feeding the finding back into the `mod-108` control-status report and the escalation register (chapter 08; the trigger for `mod-108`'s post-incident control re-test row).

None of these verbs *commands the incident*. None *designs the monitoring stack*. None *submits the regulator filing directly*. That distinction is the module's spine.

## What the analyst does not do

The analyst does not:

- **Take incident command for the technical containment.** The ML / infra / product on-call runs the containment — rollback, guardrail retuning, traffic gating, model version pin, kill-switch. The analyst records what the on-call did and when; the analyst does not decide what the on-call should do.
- **Take enterprise-level incident command for the cross-functional decisions.** Enterprise-level decisions — public statement, customer notification, regulator engagement, board briefing, extended service degradation — sit with `head-of-ai-governance` on the governance track and with the appropriate crisis-management function on the enterprise track. The analyst supplies the evidence pack; the executive decides.
- **Design the monitoring dashboards, metrics, thresholds, or alerting.** The analyst reads what `ai-eval-engineer` and `ai-infra-mlops` have built. The analyst flags panels that are unreadable, ambiguous, or missing entirely — but the redesign is the specialists' work, not the analyst's.
- **Author the post-mortem's technical root cause or the mitigation code.** The technical root cause and mitigation are ML / infra / product scope. The analyst reads the post-mortem, records it against the incident record, and translates the technical claims into governance vocabulary in the evidence pack.
- **Sign or submit the serious-incident notification to a market surveillance authority.** Under the EU AI Act the provider (or, in some cases, the deployer) has the reporting obligation; the enterprise designates the accountable executive who signs and submits. The analyst *drafts* the notification and drives the deadline discipline; the executive owns the submission.
- **Draft the impact-assessment update itself.** The IA / FRIA / DPIA's original owner drafts the update. The analyst coordinates the trigger, the timeline, and the sign-off routing.
- **Take a residual-risk-acceptance decision on behalf of the risk owner.** If an incident forces a residual-risk re-open on a register entry (per `mod-103` chapter 05), the risk owner re-accepts the residual; the analyst re-scores the entry with the risk owner and records the acceptance. The analyst does not accept residual risk on the owner's behalf.

Chapter 09 walks the full boundary. The point at this stage: the analyst is a *recorder, coordinator, and packager*, not an incident commander, monitoring designer, or regulator-facing signer.

## The three tangible outputs

Everything in this module reduces to three artefacts:

1. **The incident record.** A row per AI incident with the `INC-<year>-<sequence>` identifier, cross-referenced to the inventory, register, IA corpus, eval-evidence, and control-status rows the incident touches. The record is the connective tissue that lets any downstream reader — internal auditor, external auditor, regulator, governance-council member — walk from the incident to every artefact affected. Chapter 03 fixes the shape.
2. **The monitoring-reading note.** A periodic (typically monthly, plus on-trigger) analyst-authored note per live AI system that reports what the four panel families (drift, quality, safety, cost — chapter 05) show, what the analyst read from them, whether the state is consistent with the current governance sign-off, and what — if anything — escalated. Chapter 05 fixes the shape.
3. **The post-market surveillance summary.** For any AI system in the EU AI Act's high-risk scope, a periodic summary of the system's post-deployment behaviour that maps to Article 72's post-market monitoring plan requirements, plus — on trigger — the Article 73 serious-incident notification draft. Chapter 07 fixes both.

The post-incident evidence pack (chapter 08) is a *format* for delivering the incident record and its cross-referenced artefacts to a specific audience (council or internal audit); it does not add a new tangible output on top of the incident record itself.

## Where this module sits in the arc

- **Inputs.** The inventory row set (`mod-102`), the risk register (`mod-103`), the fairness-review notes (`mod-104`), the impact-assessment corpus (`mod-105`), the regulator tracker (`mod-106`), the eval-evidence rows (`mod-107`), the control-status report and the vendor-risk-register (`mod-108`); the live monitoring dashboards designed and operated by `ai-eval-engineer` / `ai-infra-mlops`; the ML / infra / product on-call's technical incident record; each affected system's release-assurance and eval-evidence history.
- **Outputs.** An incident record per AI incident; a monitoring-reading note per live AI system per cadence period, plus on-trigger; a periodic PMS summary per high-risk system with the standing serious-incident-notification draft template ready; a post-incident evidence pack per incident where the council or internal audit asks for one; an escalation register roll-up (feeding into `mod-108`'s register and into `mod-110`'s council briefings) of the monitoring and incident escalations that occurred in the period.
- **Downstream consumers.** `mod-110` reads the incident records and PMS summaries into council briefings; the escalation register feeds the council's standing policy-work agenda. `mod-108`'s control-status report picks up post-incident control re-tests as trigger-driven test rows. `internal-audit` reads the evidence packs when scoping an internal-audit engagement. The provider's or deployer's designated executive reads the serious-incident-notification draft when the deadline lands.

## The vocabulary the analyst needs

- **AI incident.** Any event where an AI system produces an unsafe, unauthorised, incorrect, biased, or unexpected outcome that reaches a person, a downstream system, or an operating decision — or where an AI system was successfully attacked, exploited, or used outside its approved envelope. Chapter 02 walks the six AI-specific classes. The AI Incident Database (AIID) and the OECD AI Incidents Monitor use overlapping-but-distinct definitions; chapter 02 fixes the enterprise-internal definition and cites both external corpora.
- **AI-specific incident vs general software incident.** A general software incident (an outage, a data-corruption bug, a deployment failure, a security incident that would exist without the AI component) can affect an AI system without being an *AI* incident. Chapter 02 walks the boundary and the *both-at-once* pattern where a single event has both a general-software root cause and an AI-specific effect.
- **Incident record.** The analyst's tangible output per incident. `INC-<year>-<sequence>` identifier; row shape in chapter 03.
- **Incident commander.** The role that runs the technical containment. On the ML / infra / product side, the on-call engineer per the enterprise's on-call rotation; on the enterprise-level side, `head-of-ai-governance` (or the enterprise's crisis-management function) for cross-functional decisions. Not the analyst.
- **Continuous monitoring.** The standing observation of a deployed AI system's operating behaviour along multiple dimensions — drift, quality, safety, cost — with alerting on threshold breach. Chapter 05 walks the four panel families and the analyst-tier reading depth.
- **Drift.** A change in the statistical distribution of the model's inputs, outputs, or the ground-truth signal the model is evaluated against. *Data drift* (input distribution shifts), *concept drift* (the input-to-label relationship shifts), *label drift* (the target distribution shifts), and *prediction drift* (the output distribution shifts) are the analyst-tier subclasses. `ai-eval-engineer` selects the metric; the analyst reads whether the metric is inside or outside the threshold.
- **Quality.** The composite of task-appropriate accuracy signals — RAG groundedness, refusal-rate on the internal jailbreak-attempt corpus, factuality on a reference set, task-completion rate, hallucination rate as measured by a specific benchmark. The metric is task-specific; the reading is analyst-tier.
- **Safety.** The composite of guardrail-related signals — jailbreak-classifier fire rate, output-filter hit rate, unsafe-content classification rate, agent-tool-call authorisation-failure rate, refusal-rate on prohibited-use prompts. The metric is task-specific and threat-model-specific; chapter 06 walks the escalation triggers.
- **Cost.** The composite of run-cost signals — inference cost per request, tokens per response, cache hit rate, tool-call cost, cost per business outcome. Not usually a governance signal in itself, but a *governance-adjacent* signal — an unexplained cost spike frequently precedes a quality or safety regression, so the analyst reads cost alongside the other panels.
- **Post-market surveillance (PMS).** Under the EU AI Act, the provider's obligation to systematically monitor a placed-on-the-market AI system's performance and to record and report performance issues. Article 72 sets the post-market monitoring plan requirement; Article 73 sets the serious-incident reporting obligation. Chapter 07 walks the analyst-tier reading depth.
- **Serious incident.** As defined in the EU AI Act, an incident causing (among other outcomes) death, serious harm to health, serious and irreversible disruption of critical infrastructure, breach of fundamental rights, or serious harm to property or the environment — attributable to an AI system. Chapter 07 walks the analyst-tier reading and the notification timelines.
- **Post-mortem.** The technical write-up produced after an incident by the responding engineering team. In this module, the analyst reads the post-mortem, records it against the incident record, and translates its technical claims into governance vocabulary. The analyst does not author the technical section.
- **Root cause.** The engineering team's determination of what upstream condition caused the incident. In classical (non-AI) incident practice, root causes are usually a single-actor deterministic condition. In AI incidents, root causes are more often *systemic* — a data-drift condition that was not monitored for, an evaluation gap, a deployment-process bypass — and the analyst's evidence pack is where that systemic framing is captured.

## The delegation map — preview

Chapter 09 states this in full; here is the preview.

| Artefact / action | Role that owns | Role that supports |
|---|---|---|
| Recognition of AI-specific-vs-software-incident class | `ai-governance-analyst` | ML / infra / product on-call (technical detail) |
| Technical containment (rollback, gating, guardrail retune, kill-switch) | ML / infra / product on-call | `ai-governance-analyst` (records) |
| Enterprise-level incident command (public statement, customer notification, regulator engagement) | `head-of-ai-governance` / crisis-management | `ai-governance-analyst` (evidence pack) |
| Incident record — `INC-<year>-<sequence>` composition and cross-references | `ai-governance-analyst` | ML / infra / product on-call (technical detail) |
| Impact-assessment (IA / FRIA / DPIA) update on incident trigger | Assessment's original owner | `ai-governance-analyst` (coordinates), `data-protection-officer` (DPIA sign-off) |
| Continuous-monitoring dashboard design, metric choice, threshold setting, alerting rules | `ai-eval-engineer` / `ai-infra-mlops` | `ai-governance-analyst` (reads; flags un-readable panels) |
| Monitoring-reading note for governance sign-off | `ai-governance-analyst` | `ai-eval-engineer` (technical Q&A) |
| Monitoring-signal escalation — model behaviour | `ai-risk-engineer` (on receipt) | `ai-governance-analyst` (files) |
| Monitoring-signal escalation — security | `ai-infra-security` (on receipt) | `ai-governance-analyst` (files) |
| Monitoring-signal escalation — enterprise-level | `head-of-ai-governance` (on receipt) | `ai-governance-analyst` (files) |
| Post-market surveillance summary composition (EU AI Act Article 72) | `ai-governance-analyst` | EU AI Act compliance function (owns the plan) |
| Serious-incident notification (EU AI Act Article 73) drafting | `ai-governance-analyst` | Accountable executive (signs and submits) |
| Post-incident evidence pack for council / internal audit | `ai-governance-analyst` | `head-of-ai-governance` (reviews), `internal-audit` (consumes) |
| Post-incident control re-test (out-of-cycle, feeds `mod-108`) | `ai-governance-analyst` | Control owner (supplies evidence) |
| Residual-risk re-acceptance on register entry the incident calls into question | Risk owner named on the register entry | `ai-governance-analyst` (re-scores) |

The rows in the middle three groups — record, coordinate, package — are the analyst's day-to-day. The rows at the top and bottom are what the analyst hands off from and back to.

## What to memorise

- **The analyst records, coordinates, and packages. The analyst does not command the incident, design the monitoring, or submit the regulator filing.**
- **The three tangible outputs are the incident record, the monitoring-reading note, and the post-market surveillance summary (with the standing serious-incident-notification draft).**
- **Reading is the analyst-tier verb on dashboards; designing is not.** Metrics, thresholds, and alerting rules are `ai-eval-engineer` / `ai-infra-mlops` scope; the analyst reads what those roles have built.
- **The incident record is the connective tissue.** A downstream reader must be able to walk from the `INC-<year>-<sequence>` identifier to every affected inventory row, register entry, impact assessment, eval-evidence row, and control-status row.
- **The EU AI Act's Article 72 (post-market monitoring) and Article 73 (serious-incident reporting) obligations sit inside this module.** The analyst drafts; the accountable executive signs.

## Summary

This module makes the enterprise's governance record honest about what its AI systems are doing *in operation* rather than what they were doing when they were assessed. The analyst is a recorder (of the incident and of what the monitoring shows), a coordinator (of the IA update and of the escalation to the specialist role), and a packager (of the evidence for council and internal audit). The three tangible outputs are the incident record (chapter 03), the monitoring-reading note (chapter 05), and the post-market surveillance summary with its serious-incident notification draft (chapter 07). The role stops at incident command, monitoring design, and regulator-facing signature — the specialists and the accountable executives take it from there. Chapter 02 opens by fixing the taxonomy the recognition step depends on.
