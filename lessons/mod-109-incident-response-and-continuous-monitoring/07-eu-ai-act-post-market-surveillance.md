# EU AI Act Post-Market Surveillance and Serious-Incident Reporting

## Why this chapter

The EU AI Act (Regulation (EU) 2024/1689) sets two operational obligations on providers of high-risk AI systems (as defined by Article 6 and Annex III) that this module operationalises directly. Article 72 requires the provider to establish and operate a *post-market monitoring system* under a documented *post-market monitoring plan*; the periodic summary of what that system observed is a governance artefact the enterprise composes on cadence. Article 73 requires the provider to *report serious incidents* — as defined in Article 3(49) — to the market surveillance authority of the Member State where the incident occurred, on tightly-bound timelines. Deployers of high-risk systems have parallel monitoring obligations under Article 26 and — for the specified categories — the fundamental-rights impact assessment obligation under Article 27 the analyst has already met in `mod-105` and re-opens per chapter 04.

The analyst-tier work sits in two artefacts:

1. **The post-market surveillance (PMS) summary.** A periodic report per high-risk AI system that summarises what the monitoring plan (owned by the provider's EU AI Act compliance function, not the analyst) observed in the period, cross-references incidents and monitoring escalations, and documents the residual-risk position that the accountable executive uses to confirm continued conformity.
2. **The Article 73 serious-incident notification.** An on-trigger draft the analyst produces when an incident meets the Article 3(49) threshold, so the accountable executive can review and submit within the Article 73 timelines.

The analyst *drafts* both artefacts. The enterprise's EU AI Act compliance function *owns the post-market monitoring plan itself* (the design, the scope, the methodology). The accountable executive named by the enterprise *signs and submits* the serious-incident notification. This chapter fixes the analyst-tier reading depth on Articles 72 and 73, the PMS summary shape, and the Article 73 notification draft shape.

## What Article 72 requires — analyst-tier reading

Article 72 of Regulation (EU) 2024/1689 obliges providers of high-risk AI systems (per Article 6) to:

- Establish and document a *post-market monitoring system* proportionate to the nature of the AI technologies and the risks of the high-risk AI system.
- Actively and systematically collect, document, and analyse relevant data — provided by deployers or collected through other sources — on the performance of the high-risk AI system throughout its lifetime.
- Allow the provider to evaluate continuous compliance with the requirements set out in Chapter III Section 2 of the Regulation (the requirements for high-risk AI systems).
- Follow a *post-market monitoring plan* that is part of the technical documentation referred to in Annex IV.

The Commission is empowered to adopt an implementing act specifying a template for the post-market monitoring plan and the list of elements to be included in the plan.

**What this means for the analyst.** The analyst does not author the *plan* — the plan is authored by the enterprise's EU AI Act compliance function (or the equivalent — commonly a joint effort of `head-of-ai-governance`, `legal`, and `senior-ai-governance-architect`). The analyst reads the plan and understands, per high-risk system, what data the plan requires the enterprise to collect, at what cadence, and against what continued-compliance criteria. The periodic PMS summary the analyst composes is the artefact that reports whether the plan's data collection ran, what it observed, and what the analyst reads from it.

The plan will typically require the enterprise to record and analyse:

- Performance data from continuous monitoring (chapter 05's four panel families).
- Feedback from deployers where the enterprise is a provider but not the deployer (per Article 72's *data provided by deployers* clause).
- Every incident logged against the system in the period (chapter 03's incident records).
- Every escalation from monitoring signals (chapter 06's escalation register).
- Every material change to the system (model version, retrieval index, prompt, guardrail configuration) and its effect on continued-compliance claims.
- Every finding from post-market surveillance authority engagement, if any.

Article 72(3) provides that for high-risk AI systems covered by the Union harmonisation legislation listed in Section A of Annex I, where the applicable legislation already provides for a post-market monitoring system, the provider may integrate the elements required by the Regulation into the existing system. In practice this affects providers whose systems are already regulated as medical devices, in vitro diagnostic devices, machinery, or the other Annex-I-Section-A categories.

<!-- needs-research: verify current Commission implementing-act status on the Article 72 post-market monitoring plan template — as of the drafting cycle, the Commission had been empowered to adopt but publication timing should be checked against the AI Office's page before the enterprise finalises its own template. -->

## What Article 73 requires — analyst-tier reading

Article 73 of Regulation (EU) 2024/1689 obliges providers of high-risk AI systems placed on the Union market to report *serious incidents* to the market surveillance authority of the Member State where the incident occurred.

The definition of *serious incident* is in Article 3(49): an incident or malfunctioning of an AI system that directly or indirectly leads to any of the following —

- (a) the death of a person, or serious harm to a person's health;
- (b) a serious and irreversible disruption of the management or operation of critical infrastructure;
- (c) infringement of obligations under Union law intended to protect fundamental rights;
- (d) serious harm to property or the environment.

Article 73 sets specific notification deadlines. The general rule: the report is made *immediately* after the provider has established a causal link — or the reasonable likelihood of such a link — between the AI system and the serious incident, and in any event no later than 15 days after the provider or, where applicable, the deployer becomes aware of the serious incident.

Two shorter deadlines apply to specific outcome classes:

- In the case of a widespread infringement or a serious and irreversible disruption of critical infrastructure (Article 3(49)(b)), the report is made **immediately, and no later than 2 days** after the provider or deployer becomes aware of the incident.
- In the case of the death of a person, the report is made **immediately after the provider has established, or as soon as it suspects,** a causal relationship between the AI system and the serious incident, and no later than **10 days** after the date on which the provider or deployer becomes aware of the serious incident.

Where necessary to ensure timely reporting, providers may submit an *initial, incomplete report* followed by a complete report.

Providers also cooperate with the competent authorities and — for AI systems that are safety components of products covered by other Union harmonisation legislation — apply the corresponding reporting obligations under that legislation, subject to specific carve-outs in Article 73.

**What this means for the analyst.** The analyst does not decide whether an incident is a *serious incident* — that determination is a legal one that the enterprise's EU AI Act compliance function and `legal` make on the analyst's evidence. The analyst *reads for the Article 3(49) criteria* at incident intake and at triage; if any of the four outcome classes appears plausibly implicated, the analyst flags the incident for Article 73 evaluation immediately, opens the notification draft in parallel with the incident record's other follow-through, and ensures the accountable executive is in the loop within the same day. The 2-day and 10-day deadlines are not amenable to normal working-hours cadence; the analyst's job is to make sure the clock does not silently start without the executive knowing.

<!-- needs-research: verify the current text of Article 73 timelines against the final published version in OJ (2024/1689) — the 15-day / 10-day / 2-day structure is as adopted, but any subsequent corrigendum or Commission delegated act should be checked. -->

## The PMS summary shape

The periodic summary the analyst composes per high-risk AI system.

### Header

| Field | Content |
|---|---|
| PMS record ID | `PMS-<year>-<inv-id>` for the standing record; `PMS-<year>-<inv-id>-<period>` for the per-period summary |
| Reporting period | Start and end dates |
| Inventory row | `INV-<year>-<sequence>` |
| High-risk classification basis | Which Annex III use case (or Section A of Annex I mapping) qualifies the system as high-risk |
| Provider vs deployer role | The enterprise's role for this system under the Act |
| Post-market monitoring plan reference | The plan version this summary reports against |
| Accountable executive | Named per the enterprise's EU AI Act compliance function |
| Composed by | Analyst identifier |
| Composed on | Date |

### Section 1 — Data collection completeness

Was the plan-required data collected in the period, at the required cadence, from the required sources? One paragraph per data source (continuous monitoring per chapter 05, deployer feedback per Article 72, incident records per chapter 03, escalations per chapter 06, material-change records, third-party findings). Gaps are named explicitly and cross-referenced to any `mod-108` control-testing finding that captures the gap.

### Section 2 — Performance findings

What did the collected data show about the system's performance against the continued-compliance criteria? One paragraph per continued-compliance criterion (e.g., accuracy claims from the technical documentation, fairness commitments from the FRIA, safety claims from the risk-management system per Article 9). Reference the monitoring-reading notes (`MON-<year>-<month>-<inv-id>`) for the underlying data.

### Section 3 — Incidents in the period

Every `INC-<year>-<sequence>` on the affected inventory row for the period, listed with:

- Incident ID and class (chapter 02).
- Article 3(49) evaluation — was the incident a *serious incident* under any of the four outcome classes? Yes / no / evaluated-and-deferred, with rationale.
- Article 73 notification status — *not-applicable* / *drafted* / *submitted*, with the notification identifier.
- Cross-references to any control-status changes triggered.
- IA / FRIA / DPIA re-open status.

### Section 4 — Escalations in the period

Every `ESC-<year>-<sequence>` from the monitoring escalation register (chapter 06) filed against the system in the period, listed with class, owner, current status, and resolution artefact identifier.

### Section 5 — Material changes in the period

Every change to the system that affects a claim in the technical documentation — model-version updates, retrieval-index changes, prompt-template edits, guardrail-configuration changes, tool-authorisation-scope changes. Each named with date, actor, and cross-reference to the change-management record.

### Section 6 — Assessment of continued conformity

The accountable executive's determination — for signature — of whether the system remains in conformity with the requirements of Chapter III Section 2 of the Regulation. The analyst's draft carries the evidence; the executive signs. Options: *conformity maintained*, *conformity maintained with named observations*, *conformity in question — corrective action open*, *non-conformity identified — corrective action complete before period close*, *non-conformity identified — corrective action in flight past period close*.

### Section 7 — Actions and follow-through

The corrective and preventive actions from Sections 3, 4, 5, and 6 with owners and target dates; explicit hand-off to the next-period summary for any action carrying over.

### Attachments

- The monitoring-reading notes for the period.
- The incident records referenced in Section 3.
- The escalation records referenced in Section 4.
- The change-management records referenced in Section 5.
- Any deployer-supplied feedback records (for provider-only-not-deployer relationships).

### Cadence

The plan sets the cadence; the analyst applies it. A reasonable default in the absence of a plan-specified cadence is quarterly for High-tier systems, semi-annually for medium-risk systems within Annex III scope, and immediately-on-serious-incident regardless.

## The Article 73 serious-incident notification draft shape

The on-trigger draft the analyst opens when the Article 3(49) evaluation crosses the threshold. The final notification's fields, format, and submission channel are set by the Commission (an implementing act specifies the reporting template) and by each Member State's designated market surveillance authority; the analyst's draft carries the substantive content the executive reviews and submits through whichever channel the enterprise's EU AI Act compliance function has established.

<!-- needs-research: verify the current status of the Commission's implementing act on the Article 73 notification format, and check with the enterprise's EU AI Act compliance function for the Member-State-specific submission channel. Different Member States are designating different market surveillance authorities. -->

### Header

| Field | Content |
|---|---|
| Notification ID | `A73-<year>-<sequence>` (internal) |
| Related incident record | `INC-<year>-<sequence>` |
| Related inventory row | `INV-<year>-<sequence>` |
| Provider identifier | Legal name, address, EU representative if applicable |
| Deployer identifier | If the deployer initiated the report; the Regulation places specific obligations on deployers where the provider is not established in the Union |
| AI system identifier | Trade name, version, unique reference from the technical documentation |
| Member State | Where the incident occurred |
| Market surveillance authority | The authority the notification is submitted to |
| Analyst drafting | Named actor |
| Executive reviewing | Named accountable executive |
| Draft opened | Date and time |
| Draft submitted for review | Date and time |
| Executive sign-off | Date and time |
| Submitted | Date and time |
| Acknowledgement received | Date and time; authority reference number |

### Substantive content

The draft covers, in analyst voice, at a minimum:

- **The serious incident.** What happened, when, where, and against which AI system. One paragraph in factual voice.
- **The Article 3(49) outcome class(es) implicated.** (a) death or serious harm to health / (b) critical-infrastructure disruption / (c) fundamental-rights infringement / (d) serious harm to property or environment — with the rationale for each class named.
- **The causal link status.** Established / reasonable likelihood / suspected — matching the specific deadline that applies.
- **The scope of impact.** Number of persons affected, systems affected, geographic scope, temporal scope. Estimates permitted with the estimation basis named.
- **The AI system.** Trade name, version(s) involved, deployment context, deployer relationship (if the provider is not the deployer).
- **Immediate containment actions.** What the enterprise has done to prevent further occurrence in the period since awareness — rollback, gating, kill-switch, guardrail retune, disable of feature, deployer notification.
- **Corrective actions planned.** Root-cause investigation status, mitigation strategy, expected timeline.
- **Coordination with other authorities.** If the incident triggers reporting under other Union legislation (medical device, product safety, data protection) — the parallel reports filed.
- **Attachments.** The incident record, the monitoring-reading note that surfaced the signal (if applicable), the technical-documentation reference for the affected system, the post-mortem (if landed by draft time).

### The deadline discipline

The analyst tracks the deadline against three clock-start events, whichever is earliest applicable:

- **Awareness.** The provider (or deployer) became aware of the incident — the moment a person acting for the provider first learned of the incident, not the moment the incident occurred.
- **Causal-link establishment.** The provider established the causal link (for the general 15-day path).
- **Suspicion of causal link.** The provider first suspects a causal link (for the 10-day death-of-a-person path).

The clock is measured in calendar days, not working days. The analyst opens a timer on the notification record at intake and pings the accountable executive daily until the notification is submitted. The 2-day critical-infrastructure / widespread-infringement clock is short enough that same-day executive engagement is required; the analyst does not wait for the next scheduled meeting.

## The provider-deployer role split

The enterprise may be a provider (having placed the system on the market or put it into service under its own name or trademark), a deployer (using the system under its own authority), or both (in-house use of a system the enterprise itself provides). The obligations differ:

- **Provider obligations** are more extensive: technical documentation, post-market monitoring plan (Article 72), serious-incident reporting (Article 73), quality management system, and continuous compliance with Chapter III Section 2.
- **Deployer obligations** under Article 26 include monitoring the operation of the high-risk system according to the instructions for use, immediately informing the provider (and, where applicable, the deployer's own market surveillance authority) of any serious incident, and — for the categories in Article 27 — completing a FRIA.

The analyst records the enterprise's role per system on the inventory row and on the PMS record. Systems where the enterprise is both provider and deployer carry both obligation sets. Systems where the enterprise is a deployer of a third-party high-risk AI system trigger vendor-intake work under `mod-108` chapter 06 in addition to the PMS record.

## Interaction with GDPR, medical device, and product safety reporting

An AI system's serious incident may trigger parallel reporting under other regimes. The analyst does not run those regimes but does record the parallel notifications on the AI Act notification record so the enterprise can demonstrate coordinated handling.

- **GDPR personal-data breach.** If the serious incident includes a personal-data breach, GDPR Article 33 requires notification to the supervisory authority within 72 hours. The `data-protection-officer` runs this notification; the analyst cross-references it on the AI Act notification record.
- **Medical device.** If the AI system is a medical device or in vitro diagnostic device, the Medical Device Regulation and IVDR incident-reporting obligations apply; the enterprise's regulatory-affairs function runs those; the analyst cross-references.
- **Product safety.** If the AI system is a component of a product covered by other Union harmonisation legislation, that legislation's post-market surveillance and incident-reporting obligations apply, with the Article 73 carve-out (per Article 73(9)-(11) as adopted) reducing duplicative reporting.

## Common failure modes

- **Silent Article 3(49) evaluation.** The analyst files *not-triggered* on Article 73 for every incident without walking the four outcome classes. Fix: the incident record's *Article 73 evaluation* field records the class-by-class walk with rationale.
- **The clock starts before anyone tells the executive.** The analyst becomes aware of the incident on Friday afternoon; the executive is not looped in until Monday morning; the clock has consumed three of fifteen days. Fix: the intake question *do you have an executive in the loop* is a same-day question; the notification draft opens in parallel with the incident record.
- **The PMS summary is not composed until year-end.** The plan requires periodic reporting and the analyst treats it as an annual exercise. Fix: the plan's cadence is respected; a plan that does not name a cadence is a `mod-108` control-testing finding against the plan.
- **Provider vs deployer role confusion.** The analyst records the enterprise as provider for a system it only deploys, or vice versa, and the wrong obligation set applies. Fix: the inventory row's *EU AI Act role* field is set at intake per `mod-102`; the PMS record inherits it.
- **The notification is drafted in isolation.** The analyst composes the notification without `legal` or the EU AI Act compliance function's review; substantive-content errors reach the authority. Fix: the accountable executive review is mandatory; `legal` review is standard practice.
- **The notification's clock is measured in working days.** The deadlines in Article 73 are calendar days. Fix: the deadline timer is calendar-day-based.

## What to memorise

- **Article 72 obliges a post-market monitoring plan and system;** the analyst reads the plan, and composes the periodic PMS summary per system.
- **Article 73 obliges serious-incident reporting** on 15-day (general), 10-day (death), and 2-day (critical infrastructure / widespread infringement) deadlines in calendar days.
- **Article 3(49) defines *serious incident*** across four outcome classes: death or serious harm to health, critical-infrastructure disruption, fundamental-rights infringement, serious harm to property or the environment.
- **The analyst drafts, the accountable executive signs and submits.**
- **The provider-deployer role split determines which obligations apply.**
- **The PMS summary shape is seven sections** — data collection, performance findings, incidents, escalations, material changes, continued-conformity assessment, and actions.
- **Parallel reporting** under GDPR, MDR/IVDR, or other Union harmonisation legislation is cross-referenced but not run by the analyst.

## Summary

For each AI system in the EU AI Act's high-risk scope, the analyst composes a periodic post-market surveillance summary against the plan owned by the enterprise's EU AI Act compliance function, and drafts an Article 73 serious-incident notification when the Article 3(49) threshold is crossed. Article 72 sets the standing PMS-plan-and-system obligation; Article 73 sets the serious-incident reporting obligation with 15-day general / 10-day death / 2-day critical-infrastructure or widespread-infringement calendar-day deadlines. The analyst does not decide whether an incident is a *serious incident* — that is a legal determination — but reads for the four Article 3(49) outcome classes at intake and triage, opens the notification draft in parallel with the incident record's other follow-through, and drives the deadline discipline so the accountable executive is never surprised by a clock they did not know was running. Chapter 08 turns to the post-incident evidence pack — the artefact that packages the incident record and its cross-referenced artefacts for the governance council and internal audit.
