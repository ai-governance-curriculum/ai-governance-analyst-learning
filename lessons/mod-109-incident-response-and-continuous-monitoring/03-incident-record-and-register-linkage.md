# Logging the Incident Against the Risk Register

## Why this chapter

Chapter 02 fixed the class field the analyst assigns at intake. This chapter fixes the row the analyst composes around that field: the `INC-<year>-<sequence>` incident record, the cross-references to every affected artefact the earlier modules have produced, and the intake–triage–post-mortem cadence the record fills in across.

The record is the analyst's single most-cited artefact in this module. `mod-108`'s post-incident control re-test cites the record; `mod-110`'s council briefing cites the record; the post-market surveillance summary (chapter 07) cites the record; the internal auditor reads the record when scoping an engagement; the risk-register entry the incident called into question links back to the record. Silent gaps in the record (a missing cross-reference to the inventory row, an unset owner-ack, a post-mortem that never landed on the record even though it was written) are the failure mode the module's downstream artefacts inherit — and cannot recover from without re-opening the incident.

## The intake → triage → post-mortem cadence

The record's fields fill in across three temporally distinct events. The analyst's job at each event is different.

- **Intake (T0 → T0+hours).** The event has surfaced — through a customer complaint, a monitoring alert, an on-call escalation, a red-team report, a regulator query, a `mod-102` inventory reconciliation, a `mod-108` control test finding. The analyst opens the record with the minimum viable field set (identifier, opened date, class per chapter 02, affected inventory row(s), the surface-of-report, the primary route). Severity is unset. Root cause is unset. Post-mortem status is *pending*.
- **Triage (T0+hours → T0+days).** The primary-route specialist has picked up the record, confirmed the class (or reclassified it), set severity per their taxonomy, and started containment. The analyst updates the record with the specialist's confirmation, the containment actions taken (rollback, guardrail retune, kill-switch, gating, version pin) and their timestamps, the current status of the affected system (available / degraded / offline / gated), and the IA / FRIA / DPIA re-open status.
- **Post-mortem (T0+days → T0+weeks).** The engineering team has written the post-mortem. The analyst reads the post-mortem, records its identifier and location on the record, extracts the root cause in analyst-voice governance vocabulary (chapter 08's translation practice), files the register-entry residual-risk re-open request with the risk owner, opens the control re-test rows into the `mod-108` cycle, and — for high-risk EU AI Act systems — updates the post-market surveillance record and evaluates the Article 73 threshold (chapter 07).

Some records close within a week (the containment worked, the post-mortem was a paragraph, no register or IA re-open triggered); some remain open for a quarter or more (a hallucination-driven-harm case with legal follow-through, a biased-outcome-escalation case with a fairness re-audit dependency). The analyst reviews the open-incident roll-up weekly and moves stalled records to the escalation register (chapter 09).

## The `INC-<year>-<sequence>` record shape

Every AI incident record carries the fields below. The shape follows the analyst-tier row discipline the track uses elsewhere: mandatory identifier, mandatory cross-references, mandatory rationale, mandatory ownership, and an audit-trail history of changes.

### Identifier and provenance

| Field | Content | Notes |
|---|---|---|
| Incident ID | `INC-<year>-<sequence>` | GRC-platform assigned; monotonic within year |
| Opened date | Analyst action date | T0 in the cadence |
| Opened by | Analyst identifier | Named actor |
| Surface of report | *customer complaint* / *monitoring alert* / *on-call escalation* / *red-team* / *regulator query* / *inventory reconciliation* / *control-test finding* / *vendor notice* / *internal audit* | One value |
| Source-of-report link | Ticket URL, alert URL, complaint identifier, red-team report ID, regulator correspondence ID | Whatever the surface was |

### Classification

| Field | Content | Notes |
|---|---|---|
| AI-specific class | One of chapter 02's six classes, or *both-at-once* (with the second class named), or *general software* (in which case the record exists only as a cross-reference stub against a classical incident record) | Set at intake by the analyst; may be reclassified at triage by the specialist |
| Reclassification history | `class-was → class-is` with actor and date | Every reclassification is logged; silent overwrites are a fail |
| Classical incident cross-reference | Classical incident record ID (`SEC-...`, `CHG-...`, `INF-...` per the enterprise's classical incident-response schema) if *both-at-once* | Cross-reference is mandatory when *both-at-once* is set |
| External-corpus reference | `AIID Incident nnn` / `OECD AI Incidents Monitor` entry / vendor CVE / other public reference | Optional; recorded when the enterprise's incident mirrors or reports to a public corpus |

### Affected artefacts (the cross-reference block)

| Field | Content | Notes |
|---|---|---|
| Affected `INV-<year>-<sequence>` inventory row(s) | One or more | Empty is a fail; the incident touches at least one inventoried system |
| Affected `RISK-<year>-<sequence>` register entries | Zero or more | Named when the incident's occurrence falsifies or weakens a residual claim per `mod-103` |
| Affected `IA-<year>-<sequence>` / `FRIA-<year>-<sequence>` / `DPIA-<year>-<sequence>` corpus entries | Zero or more | Named when the incident triggers a re-open (chapter 04) |
| Affected `EVAL-<year>-<sequence>` eval-evidence rows | Zero or more | Named when the incident indicates the eval missed the failure mode (`mod-107`) |
| Affected `CTL-<year>-<sequence>` control records | Zero or more | Named when a control failed or when the incident triggers a post-incident control re-test (`mod-108`) |
| Affected `VND-<year>-<sequence>` vendor rows | Zero or more | Named when a vendor is implicated (chapter 02 class 6; `mod-108` chapter 06) |
| Affected `PMS-<year>-<system>` post-market surveillance record | Zero or one | Present when the affected system is in the EU AI Act's high-risk scope (chapter 07) |
| Cross-module escalation IDs | Zero or more `ESC-<year>-<sequence>` | Filed under `mod-108` chapter 09's classes when the incident's follow-through requires |

The cross-reference block is what makes the record navigable. A downstream reader (auditor, regulator, council member) must be able to walk from the `INC-<year>-<sequence>` identifier to every affected artefact by ID alone, without asking the analyst for context.

### Containment and technical detail

| Field | Content | Notes |
|---|---|---|
| Severity | Per the receiving specialist's taxonomy | *unset* at intake; set at triage |
| Availability state | *available* / *degraded* / *offline* / *gated* / *rolled-back* | Current, updated as containment progresses |
| Containment actions | Timestamped list — *rolled back to model v3.1.4 at T+00:47*, *guardrail-classifier threshold raised to 0.90 at T+01:20*, *kill-switch activated at T+00:12* | Actions and their actor; empty for stub-only records |
| Duration of impact | Start and end (or *ongoing*) of the state where the incident's AI-specific effect was reaching users | Distinct from the total record-open duration |
| Users / systems affected estimate | Count and characterisation | Estimate; rationale for the estimate lives in the analyst note |

### Governance follow-through

| Field | Content | Notes |
|---|---|---|
| IA / FRIA / DPIA re-open status | *not-triggered* / *triggered-in-flight* / *update-completed* / *deferred-with-rationale* | Chapter 04 |
| Register-entry residual re-open status | *not-triggered* / *re-scored* / *risk-owner-re-accepted* / *escalated* | `mod-103` chapter 05 |
| System-card / model-card update status | *not-triggered* / *updated* / *deferred-with-rationale* | `mod-105` chapter 05's model card |
| Customer / user notification status | *not-triggered* / *drafted* / *sent* — with legal review reference where applicable | Owned by product / legal; the analyst records the outcome |
| Regulator notification status | *not-triggered* / *drafted* / *submitted* — with the notification identifier and jurisdiction | Chapter 07 for the EU AI Act path |
| Control re-test status | List of `CTL-<year>-<sequence>` re-tested and their `EV-<year>-<sequence>` identifiers | `mod-108` |
| Escalation register entries | `ESC-<year>-<sequence>` filed | `mod-108` chapter 09 |

### Root cause and post-mortem

| Field | Content | Notes |
|---|---|---|
| Post-mortem identifier | The engineering team's write-up ID | Empty until the post-mortem lands |
| Post-mortem link | Stable URL, versioned | Repository or wiki with a content pin |
| Root cause (analyst voice) | One-paragraph translation of the post-mortem's root cause into governance vocabulary | Chapter 08 |
| Contributing factors | Bullet list — data drift, evaluation gap, deployment-process bypass, guardrail-flag drift, third-party update, operator error | Named per post-mortem |
| Corrective actions | Timestamped list with owner and target date | Owned by engineering; the analyst records status |
| Preventive actions | Timestamped list with owner and target date | Distinct from corrective — preventive is what stops the class of failure recurring |

### Closure

| Field | Content | Notes |
|---|---|---|
| Status | *open* / *contained* / *post-mortem-complete* / *closed* / *closed-with-open-follow-through* | Distinct states; *closed* requires every follow-through item to be *complete* or explicitly *deferred with rationale* |
| Closed date | Analyst action date | Only set when *closed* |
| Closed by | Analyst identifier | Named actor |
| Closure rationale | One paragraph — what was resolved, what was deferred, why closure is appropriate | Silent closure is a fail |
| Post-closure re-open history | `re-opened on <date> by <actor> because <reason>` | Re-opens are logged; every re-open re-emits the post-incident evidence pack (chapter 08) |

## The intake questionnaire

The analyst does not compose the record from scratch under time pressure. The intake questionnaire is a fixed set of prompts the analyst walks the reporting party through at T0, in whichever channel the report surfaced on. The questionnaire produces the intake-time subset of the record fields.

- **What did you observe?** (Free text; captured verbatim.)
- **When did you observe it?** (Timestamp; the analyst records the observer's time zone and converts.)
- **Where did you observe it?** (System name; the analyst maps to `INV-<year>-<sequence>`.)
- **Who else has seen this?** (For estimating exposure and identifying the primary and secondary route recipients.)
- **What did the system do that surprised you?** (For extracting the AI-specific class candidate per chapter 02.)
- **Is anyone or anything harmed?** (For evaluating the EU AI Act Article 73 threshold at intake — chapter 07 walks the criteria.)
- **Do you have a screenshot / prompt / log excerpt / transcript?** (For attaching to the record as intake evidence.)
- **Have you notified anyone else?** (For deduplication against any parallel classical-incident record already open.)
- **Are you comfortable being contacted for follow-up?** (For the reporting-party relationship, especially on complaint-driven surfaces.)

The questionnaire is short by design. The reporting party is not always the on-call engineer; frequently it is a customer, a support agent, an internal user, a red-team member, or a regulator. The analyst is fluent enough in the technical detail to file the record correctly; the analyst does not ask the reporting party to be fluent.

## The cross-reference discipline in practice

Two operational rules that make the cross-reference block trustworthy.

- **Cross-references are IDs, not descriptions.** *Affected `INV-2026-0091`* is a cross-reference. *Affected the support copilot* is not. Descriptions rot when systems get renamed; IDs do not. The GRC platform's search-by-ID is what the auditor uses.
- **Cross-references are bidirectional.** When the analyst adds `INC-2026-0018` to an inventory row's *incident history* field, the inventory row's ID also lands on the incident record's *affected inventory row* field, and vice versa. The GRC platform's link tables enforce this if configured; if not, the analyst writes both.

Both rules are easy to break silently. The `mod-108` control-cycle discipline catches silent breaks by testing the *cross-reference-integrity* control: sample a set of `INC-*` records and confirm every ID they name resolves to a live artefact.

## Where the record lives and who can read it

The record lives in the GRC platform (`mod-102` chapter 04 walked the analyst-tier tour). Read permissions differ by field:

- **Identifier, class, opened date, affected inventory row(s), status:** readable by every role that reads the AI inventory. Governance council members, internal audit, product owners, and — depending on enterprise policy — external audit and market surveillance authorities on request.
- **Containment actions, technical detail, post-mortem, root cause:** readable by the analyst, the primary-route specialist, `head-of-ai-governance`, and internal audit.
- **User-affected estimate, notification history, regulator submissions:** readable by the analyst, `legal`, `head-of-ai-governance`, and — for the regulator submissions — the accountable executive who signed.
- **Reporting-party personal data (if collected):** readable by the analyst and — per the enterprise's data-minimisation policy — should not be attached to the record where the report can be de-identified.

Read-permission questions are enterprise-policy questions and are answered by the enterprise's information-security and privacy functions, not by the analyst. The point at the analyst tier: not every field is universally readable; the analyst does not attach fields to the record that violate the read-permission model.

## Weekly roll-up and the escalation register interaction

The analyst runs a weekly roll-up of the incident record set — open, contained, post-mortem-in-flight, closed-with-open-follow-through — and reads it against the escalation register the enterprise runs under `mod-108` chapter 09. The interaction rules:

- Any AI incident that remains *open* for two weeks without primary-route acknowledgement escalates as a class-2 (security route) or class-4 (council decision) entry, depending on class.
- Any AI incident that closes with *deferred* follow-through items escalates the deferred items to the escalation register per the class the deferred item belongs to.
- Repeated AI incidents of the same class against the same inventory row within a rolling quarter is a pattern that the analyst raises to `head-of-ai-governance` — the pattern is policy work, not a fresh incident.
- Post-mortems that fail to land within four weeks of containment complete are a `mod-108` control finding — the control is *every AI incident has a post-mortem landing on the record within X weeks* and the analyst tests it as part of the control cycle.

## Common failure modes

- **The record is opened at triage, not intake.** The analyst waits until the specialist has confirmed the class to open the record, losing the T0 timestamp and the intake-questionnaire content. Fix: open at intake with severity and class candidate unset, and let triage update.
- **Cross-references drift.** The affected inventory row was renamed after the record was opened; the record's cross-reference still points to the old name. Fix: cross-references are IDs; renames on the target artefact don't invalidate the ID; if the GRC platform's link table is intact, the drift does not occur.
- **Post-mortem never lands on the record.** The engineering team writes the post-mortem, publishes it in the team wiki, and moves on; the incident record's post-mortem field stays empty. Fix: the four-week landing control tests this; the analyst opens a finding when it fires.
- **IA re-open is *not-triggered* by default, without evaluation.** The analyst files *not-triggered* on every record because the evaluation is deferred. Fix: chapter 04's evaluation is done at triage, with the rationale recorded on the record. *Not-triggered with rationale* is acceptable; *not-triggered by default* is not.
- **Severity is guessed at intake and never updated.** The analyst writes a severity at intake to satisfy the GRC platform's required field; the specialist's triage severity never overwrites it. Fix: intake severity is *unset*, and the platform is configured to permit *unset* as an initial value. If not, the platform is a `mod-108` library-design-fix escalation.
- **Silent closure.** The record is closed with no rationale field and no evidence that follow-through items completed. Fix: the closure rationale field is mandatory; closure without it is a workflow error.

## Interaction with the risk register

The incident record and the risk register (`mod-103`) interact in three specific patterns.

- **The incident falsifies a residual claim.** A register entry's residual-risk claim rested on an assumption the incident just falsified (a control that the entry counted on that turned out to have been disabled, an evaluation that missed the failure mode, an environmental assumption that changed). The analyst opens a *residual re-open* against the register entry, cites the incident, and drives the re-scoring with the risk owner. `mod-103` chapter 05's negotiation cadence applies.
- **The incident reveals an un-registered risk.** The incident's failure mode was never on the register. The analyst opens a fresh register entry (per `mod-103`'s intake), cites the incident as the surfacing event, and drives the initial scoring and routing. This is the more common case for classes 5 (hallucination-driven harm) and 6 (unauthorised model use).
- **The incident is envelope-confirming.** The incident is exactly what the register entry predicted and its residual-risk claim envelops the outcome. The record still opens; the register entry cites the record; the residual is *not* re-opened. This case is quiet: the enterprise's assurance model worked.

The record's *affected register entries* field is the audit-visible piece of these interactions.

## What to memorise

- **The record is opened at intake, updated at triage, and completed at post-mortem.** Three temporally distinct events; three sets of fields.
- **The cross-reference block is mandatory.** Every affected inventory row, register entry, IA / FRIA / DPIA corpus entry, eval-evidence row, control record, vendor row, and PMS record is named by ID.
- **Cross-references are IDs, not descriptions, and are bidirectional.**
- **Severity is unset at intake.** The primary-route specialist sets it at triage.
- **Silent closure is a fail.** Closure requires a rationale and completion (or explicit deferral with rationale) of every follow-through item.
- **The register interaction has three patterns** — falsification, un-registered risk, envelope-confirming — and the record makes each visible.

## Summary

The incident record is the analyst's single most-cited artefact in this module. Its shape is fixed: identifier and provenance; classification with reclassification history; a cross-reference block linking every affected `INV`, `RISK`, `IA`/`FRIA`/`DPIA`, `EVAL`, `CTL`, `VND`, and `PMS` artefact; containment and technical detail; governance follow-through fields; root cause in analyst voice and the engineering team's post-mortem; and a closure block with rationale. It is populated across intake, triage, and post-mortem — three temporally distinct events, each with a different set of fields — and rolled up weekly against the escalation register. Its cross-references are IDs, its severity is unset at intake, and its closure is never silent. Chapter 04 walks the impact-assessment-update coordination the record's *governance follow-through* block triggers.
