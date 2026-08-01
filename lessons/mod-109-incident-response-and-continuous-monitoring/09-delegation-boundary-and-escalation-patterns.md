# Delegation Boundary and Escalation Patterns

## Why this chapter

Chapters 01–08 defined the analyst's outputs (the incident record, the monitoring-reading note, the post-market surveillance summary with its serious-incident-notification draft, and the evidence pack) and the operating discipline around each. This closing chapter states the full delegation-boundary map operationalised across those outputs and defines the four escalation classes the analyst uses when monitoring or incident work outgrows the analyst's scope.

The stakes for boundary discipline in this module are higher than in `mod-108`. Cross the line silently on a control-testing finding and the enterprise's assurance posture takes a controlled hit; cross the line silently on an incident and the enterprise may miss a serious-incident notification, mis-time a customer disclosure, contaminate a legal position, or take a residual-risk-acceptance decision that was not the analyst's to take. The four escalation classes are the mechanism that makes those cross-line moments auditable. The pattern-recognition rules that close the chapter are the mechanism that turns recurring incidents into policy work the enterprise can act on.

## The full delegation-boundary map

The preview from chapter 01, stated in full and cross-referenced to the chapters where each row was operationalised.

| Artefact / action | Owner | Analyst's role | Chapter reference |
|---|---|---|---|
| Recognition of AI-specific-vs-software-incident class at intake | `ai-governance-analyst` | Owns | 02 |
| Technical containment (rollback, guardrail retune, gating, kill-switch) | ML / infra / product on-call | Records the actions and their timestamps | 02, 03 |
| Enterprise-level incident command (public statement, customer notification, regulator engagement, board briefing) | `head-of-ai-governance` / enterprise crisis-management function | Supplies the evidence pack; drafts communication where explicitly delegated | 03, 08 |
| Incident record — `INC-<year>-<sequence>` composition, cross-references, status through closure | `ai-governance-analyst` | Owns | 03 |
| Severity assignment | Primary-route specialist per their taxonomy | Records the specialist's assignment | 03 |
| Post-mortem — technical root cause, mitigation code, engineering follow-through | ML / infra / product engineering | Reads the post-mortem; translates the root cause into governance vocabulary | 03, 08 |
| Impact-assessment (IA / FRIA / DPIA) update on incident trigger — the drafting | Assessment's original owner (per `mod-105` corpus) | Coordinates the trigger, timeline, and sign-off routing | 04 |
| DPIA Article 36 supervisory-authority consultation on residual high risk | `data-protection-officer` and `legal` | Records the consultation identifier | 04 |
| Residual-risk re-acceptance on register entry the incident called into question | Risk owner named on the `mod-103` register entry | Coordinates the re-scoring; records the acceptance | 03 |
| Monitoring dashboard design — metric choice, threshold, sampling rule, alerting rule | `ai-eval-engineer`, `ai-infra-mlops` | Reads what those roles have built; flags un-readable or missing panels | 05 |
| Monitoring-reading note composition | `ai-governance-analyst` | Owns | 05 |
| Monitoring signal escalation — model behaviour | `ai-risk-engineer` (on receipt) | Files (Class A) | 06 |
| Monitoring signal escalation — security | `ai-infra-security` (on receipt) | Files (Class B) | 06 |
| Monitoring signal escalation — monitoring redesign | `ai-infra-mlops` (on receipt) | Files (Class C) | 06 |
| Monitoring signal escalation — enterprise-level | `head-of-ai-governance` (on receipt) | Files (Class D) | 06 |
| Post-market monitoring plan (EU AI Act Article 72) | EU AI Act compliance function | Composes the periodic PMS summary against the plan | 07 |
| Serious-incident notification (EU AI Act Article 73) drafting | `ai-governance-analyst` | Owns the draft; drives the deadline | 07 |
| Serious-incident notification signature and submission | Accountable executive per enterprise's EU AI Act compliance function | Records the sign-off and submission identifiers | 07 |
| Determination that an incident is a serious incident (Article 3(49) evaluation) | `legal` and EU AI Act compliance function | Flags the possible-serious-incident case at intake and triage; supplies the evidence for the determination | 07 |
| Parallel notifications under GDPR (Article 33 personal-data breach), MDR/IVDR, other Union harmonisation legislation | `data-protection-officer`, regulatory-affairs, `legal` | Cross-references the parallel notifications on the AI Act record | 07 |
| Post-incident evidence pack for council and internal audit | `ai-governance-analyst` | Owns | 08 |
| Post-incident control re-test (out-of-cycle, feeds `mod-108`) | `ai-governance-analyst` (test), control owner (evidence) | Owns the test; supplies the evidence-artefact request | 03, 08; `mod-108` |
| Council decision on any escalated incident matter | Governance council, convened by `head-of-ai-governance` | Supplies the evidence pack and the recommendation | 08 |
| Internal audit engagement scoping on AI incidents | `internal-audit` | Supplies the evidence pack | 08 |

The line pattern is consistent: the analyst recognises, records, coordinates, drafts, packages, files, tests, and hands off. The analyst does not command incidents, take clinical or product decisions, tune monitoring instruments, sign regulator submissions, determine legal characterisations, or take residual-risk-acceptance decisions on behalf of a risk owner.

## The four escalation classes

Every artefact this module produces can generate an escalation. Four classes cover the field; the analyst files under whichever fits, with the same rationale-plus-requested-action-plus-target-date shape `mod-108` chapter 09 established.

### Class 1 — Incident-command handoff

- **Trigger.** An incident that grows past the analyst's coordinating scope — a customer-facing disclosure is needed; a regulator has directly contacted the enterprise; a technical containment action requires a decision the on-call cannot take alone; the incident's blast radius crosses multiple business units.
- **Owner of the escalation.** `head-of-ai-governance`, with the enterprise's crisis-management function copied for cross-cutting incidents.
- **What the analyst supplies.** The incident record identifier, the current status, the timeline to date, the outstanding decisions, and the evidence pack (either the current draft or a hand-authored *interim brief* if the pack is not yet composed).
- **What the analyst does not do.** Take the customer-disclosure decision. Take the regulator-engagement decision. Take the containment-decision that requires executive sign-off. Speak to media or external parties without explicit delegation.
- **Example.** *INC-2026-0044 (hallucination-driven-harm on the clinical-decision-support prototype) has been open 72 hours; two additional user reports of similar-shape harm have surfaced overnight; the technical team recommends a full pause of the prototype and the product owner does not have unilateral authority to pause a deployment with ongoing clinical use. Escalating to `head-of-ai-governance` for pause decision; interim brief attached; full evidence pack in draft with target compose date 2026-08-16.*

### Class 2 — Monitoring redesign

- **Trigger.** A monitoring gap that recurs across incidents or across periods — the same panel is repeatedly un-readable; the same signal is repeatedly missed; the same threshold is repeatedly poorly-calibrated; a category of signal the enterprise needs to observe is not observable given the current dashboard set.
- **Owner of the escalation.** `ai-infra-mlops` for the platform-and-instrumentation side; `ai-eval-engineer` for the metric-and-threshold side. `senior-ai-governance-architect` for the library-level implication (the control statement the missing panel maps to).
- **What the analyst supplies.** The pattern (which panel, which signal, across which periods or incidents), the specific gap (un-readable / missing / poorly-calibrated), the affected inventory rows, the requested redesign at the outcome level (not the specification level — the analyst does not draft the panel), and the evidence (screenshots, panel URLs, incident records that surfaced the gap).
- **What the analyst does not do.** Design the new panel. Choose the metric. Set the threshold. Write the alerting rule. Author the platform ticket.
- **Example.** *Three separate INC records (INC-2026-0018, INC-2026-0031, INC-2026-0044) surfaced through customer reports rather than through dashboard alerts. Reviewing the monitoring-reading notes for those systems, the current dashboards do not include a user-feedback-signal panel that would have surfaced the pattern earlier. Escalating to `ai-infra-mlops` for a platform-level user-feedback-panel addition; escalating to `senior-ai-governance-architect` for library-level review of the *user-feedback signal is monitored* control statement.*

### Class 3 — Regulatory filing

- **Trigger.** An incident that meets the Article 3(49) threshold (or the equivalent under GDPR, MDR/IVDR, or other Union harmonisation legislation) and requires the accountable executive to sign a notification the analyst has drafted; a market surveillance authority contact; a request from a regulator for information about an AI system, an incident, or the enterprise's post-market monitoring.
- **Owner of the escalation.** The accountable executive per the enterprise's EU AI Act compliance function; `legal` copied on every filing; `data-protection-officer` copied where a personal-data dimension exists.
- **What the analyst supplies.** The notification draft per chapter 07, the incident record, the Article 3(49) evaluation with the four-outcome-class walk, the calendar-day countdown against the applicable Article 73 deadline, any parallel notifications open under other regimes.
- **What the analyst does not do.** Determine that the incident is a serious incident (the determination is `legal` and the EU AI Act compliance function's). Sign the notification. Submit the notification. Negotiate the wording of the enterprise's regulator communication.
- **Example.** *INC-2026-0044 has been evaluated by legal to meet the Article 3(49)(a) serious-harm-to-health outcome class; the 10-day death-of-a-person calendar clock is not applicable but the general 15-day clock started at awareness on 2026-08-13; day 6 of 15. Serious-incident notification draft attached; requesting executive review by 2026-08-25 and submission to the Member-State market surveillance authority by 2026-08-28.*

### Class 4 — Governance-council decision

- **Trigger.** An incident whose resolution requires a decision the analyst, the specialist roles, or the accountable executives cannot take alone — an enterprise-wide policy change (e.g., a moratorium on a specific model family, a change to the enterprise's deployment approval process), a residual-risk acceptance beyond a named threshold, a decision on whether to continue an incident-affected system in operation, a decision on public disclosure.
- **Owner of the escalation.** The governance council, with `head-of-ai-governance` as convener.
- **What the analyst supplies.** The full evidence pack (chapter 08), the recommendation from `head-of-ai-governance` obtained during the pack review, the specific decision the council is being asked to take, and the timing constraints on the decision.
- **What the analyst does not do.** Take the decision. Withdraw the escalation because a downstream role has promised remediation. Downgrade the class to a lower one to avoid the council slot.
- **Example.** *Three separate INC records across INC-2026-0018, INC-2026-0031, and INC-2026-0044 in the current quarter map to a shared root cause in the enterprise's guardrail-classifier release cadence — the current cadence lags observed attack innovation by an average of six weeks. Escalating to the governance council for decision at the next meeting on whether the enterprise should adopt a shorter cadence or a different classifier architecture; `head-of-ai-governance` recommends option B (shorter cadence with rollback discipline). Full evidence pack attached.*

## The escalation register — additions to `mod-108`'s shape

Monitoring and incident escalations share the `ESC-<year>-<sequence>` register introduced in `mod-108` chapter 09; three fields on the row are specific to this module's classes.

| Field | Content |
|---|---|
| Trigger source | The `INC-<year>-<sequence>` incident record, the `MON-<year>-<month>-<inv-id>` monitoring-reading note, or the `PMS-<year>-<inv-id>-<period>` PMS summary that surfaced the pattern |
| Module | *mod-109* — distinguishes this module's escalations from mod-108's on the roll-up view |
| Class | 1 (incident-command handoff) / 2 (monitoring redesign) / 3 (regulatory filing) / 4 (governance-council decision) |

The register's roll-up (open escalations per class per period) feeds the control-status report (`mod-108` §5), the council briefings (`mod-110`), and the enterprise's EU AI Act compliance function's dashboard.

## Pattern-recognition rules for recurring incidents

Repeated incidents of the same shape are not a set of individual incidents — they are policy work in slow-motion form. The analyst does not do the policy work but does surface the pattern.

- **Three incidents of the same class against the same inventory row within a rolling quarter.** Pattern: the system in question has a specific failure mode the assurance model is not enveloping. Recommend to `head-of-ai-governance` and the assessment's original owner a targeted re-assessment.
- **Three incidents of the same class across different inventory rows within a rolling quarter.** Pattern: the enterprise has a *class-of-system* problem, not a *specific-system* problem. Recommend to `senior-ai-governance-architect` and `head-of-ai-governance` a library-level review and a possible policy-work agenda item.
- **Repeated Class B monitoring escalations on jailbreak or prompt-injection signals across multiple systems.** Pattern: the enterprise's guardrail architecture is not keeping pace with attack innovation. Recommend to `ai-infra-security` and `senior-ai-governance-architect` an evaluation of platform-level guardrail solutions (echoing `mod-108` chapter 09's parallel pattern).
- **Repeated Class 3 (regulatory filing) escalations concentrated in one system.** Pattern: the system may not be safely operable at its current scope; the accountable executive should consider a scope reduction, a re-authorisation review, or a sunset.
- **Class 4 (council-decision) escalations resolving with *no decision*.** Pattern: the council is under-resourced or under-informed for the volume of AI decisions. Recommend to `head-of-ai-governance` that decision-rights be delegated or that the council cadence increase (echoing `mod-108` chapter 09).

These are pattern-recognitions, not policy proposals. The analyst raises the pattern; the roles that own the underlying artefact set the policy.

## When to file up rather than across

Not every difficulty is an escalation. A first-instance incident with a clear owner, an active on-call, and a normal recovery trajectory is a *record*, not an escalation. The threshold for opening an escalation register entry is one of:

- The issue has crossed into another role's scope and requires their action.
- The issue exposes an assurance-model gap (a monitoring gap, an assessment gap, a control gap).
- The issue's follow-through requires a decision the analyst or the primary-route specialist cannot make.
- The issue recurs across incidents or across periods.
- The issue exposes a boundary the enterprise's current process does not clearly resolve (a first-of-kind scenario).

Otherwise the incident record itself carries the follow-through and the escalation register stays clean.

## When to escalate around a blocked resolution

The escalation owner may not act. The analyst does not silently absorb the block. `mod-108` chapter 09's blocked-resolution discipline applies directly:

- **Escalation owner does not respond by the target date.** Re-issue with the date restated; copy the owner's manager. Second non-response escalates the block itself as a Class 4 (governance-council decision) entry with the original attached.
- **Escalation owner declines with rationale.** Record the declination on the register entry (*status: withdrawn — declined by owner: rationale*) and, where the finding still merits action, consider whether the case belongs at a higher class or a different owner.
- **Escalation owner declines without rationale.** Ask for the rationale; failing that, raise to the owner's manager. Silent decline without rationale is a governance failure the analyst does not accept.

## Cross-module escalation flow

Escalations that arise from this module's incidents and monitoring flow across the earlier and later modules the analyst has already touched:

- **`mod-102` — inventory.** An incident may reveal that the affected system's inventory row is out of date (owner has changed, tier is wrong, dependency set is incomplete). The analyst opens a reconciliation request.
- **`mod-103` — risk register.** An incident that falsifies a residual-risk claim opens a `mod-103` residual re-open with the risk owner (chapter 03).
- **`mod-104` — fairness.** A biased-outcome-escalation incident (class 4) may open a fairness-review-note re-open per `mod-104`.
- **`mod-105` — impact-assessment corpus.** Chapter 04's IA / FRIA / DPIA update coordination is the standing cross-module flow.
- **`mod-106` — regulatory tracker.** A regulatory filing under Article 73 or under a parallel regime may reveal a tracker gap (a Member-State-specific market surveillance authority not yet on the tracker; a personal-data supervisory authority not yet linked to the DPIA).
- **`mod-107` — eval-evidence.** An incident that indicates an eval missed a failure mode opens a re-run request to `ai-evaluation-engineer`.
- **`mod-108` — controls and vendor register.** An incident triggers post-incident control re-tests; recurring incidents against the same vendor trigger a vendor-row re-review.
- **`mod-110` — communication and council support.** The evidence pack and the escalation register roll-up are standing inputs to council briefings and to enterprise-level communication artefacts.

The `ESC-<year>-<sequence>` and `INC-<year>-<sequence>` identifiers are the walking path.

## Common failure modes

- **The analyst takes the decision.** The escalation owner is unavailable and the analyst — under pressure — makes the call. Fix: unavailability is itself the escalation trigger; the analyst re-escalates to the owner's manager or to Class 4, never to their own judgement on out-of-scope decisions.
- **Blame in the pack.** Section 3 of the evidence pack names an engineer or a specific team as the cause. Fix: chapter 08's *systemic condition* altitude; the pack asks what the assurance model missed.
- **The Article 73 clock is missed because the analyst waited for triage.** The analyst does not open the notification draft until the specialist confirms the class. Fix: the notification draft opens in parallel with the incident record; the accountable executive is looped in at intake for possible-Article-3(49) cases.
- **Class 4 escalations that never reach the council.** The analyst files a Class 4 but the roll-up view lists it as Class 1. Fix: the class at filing is the analyst's determination; downgrades require a co-sign from `head-of-ai-governance`.
- **Silent module-boundary crossings.** The analyst updates a `mod-103` register entry, a `mod-105` assessment, or a `mod-108` control without opening the cross-module request. Fix: cross-module changes require the request; the analyst's changes are within the incident record only.
- **The evidence pack is composed once and never re-versioned.** Follow-through completes over the weeks after the initial pack ships; the pack is not updated. Fix: chapter 08's versioning discipline; material changes to the incident record produce a re-versioned pack.

## What to memorise

- **The delegation map is twenty-plus rows.** The analyst recognises, records, coordinates, drafts, packages, files, tests, and hands off — nothing more, nothing less.
- **Four escalation classes** — incident-command handoff, monitoring redesign, regulatory filing, governance-council decision.
- **Escalations share the `ESC-<year>-<sequence>` register with `mod-108`**, with a *module* field to distinguish and a `mod-109`-specific class taxonomy.
- **Pattern-recognition rules turn recurring incidents into policy-work signals** to `head-of-ai-governance`, `senior-ai-governance-architect`, and `ai-infra-security`.
- **The Article 73 clock starts on awareness**, not on triage — the notification draft opens in parallel with the incident record; the accountable executive is looped in same-day for possible-serious-incident cases.
- **The pack stays at the systemic-condition altitude.** Blame belongs — if anywhere — in the technical post-mortem.
- **Cross-module escalation flow** goes through the `ESC-*` and `INC-*` identifiers; the analyst's changes stay within the incident record unless a cross-module request is opened.

## Summary

This chapter closes the module by stating the full delegation-boundary map operationalised across every earlier chapter and defining the four escalation classes — incident-command handoff, monitoring redesign, regulatory filing, governance-council decision — the analyst uses when work outgrows the analyst's scope. The escalation register is shared with `mod-108`'s and distinguished by module and class. Pattern-recognition rules turn recurring incidents into policy-work signals. The Article 73 clock starts on awareness, not on triage. The evidence pack stays at the systemic-condition altitude; blame belongs elsewhere. The analyst recognises, records, coordinates, drafts, packages, files, tests, and hands off; the specialists — `ai-eval-engineer`, `ai-risk-engineer`, `ai-infra-security`, `ai-infra-mlops`, `data-protection-officer`, `legal`, the EU AI Act compliance function, the accountable executive, `head-of-ai-governance`, and the governance council — own the artefacts they own. The module ends where the enterprise's live AI systems rest: on the incident record, the monitoring-reading note, and the post-market surveillance summary the analyst produces, and on the register of escalations that connects this module's cycle to every other role's work.
