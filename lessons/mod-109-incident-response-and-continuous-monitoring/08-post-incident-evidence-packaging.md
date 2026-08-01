# Post-Incident Evidence Packaging for Council and Internal Audit

## Why this chapter

Chapters 03, 04, 06, and 07 fixed the records the analyst maintains as an incident moves from intake to closure. This chapter fixes the *packaging* — the specific artefact the analyst produces when a governance council member or an internal auditor asks *what happened, what did we do, and what changed as a result*.

The record itself (chapter 03) is a system-of-record row. The evidence pack is a *reading* — a self-contained artefact composed of the record and its cross-references, arranged and narrated so a reader with governance vocabulary but no incident context can pick it up cold. Two audiences need this reading:

- **The governance council.** When an incident is placed on a council agenda — as a briefing item, as an escalation, or as the trigger for a policy discussion — the pack is the pre-read the council members work from.
- **The internal auditor.** When internal audit scopes an engagement that touches an AI system with an open or recently-closed incident, the pack is the input the auditor reads before requesting evidence artefacts.

Both audiences read the pack against the same criteria: was the enterprise's assurance model operating; where did it fail or succeed; what changed as a result. The pack answers those three questions in analyst voice, cross-referencing the underlying records rather than repeating their content, and stopping at the boundaries chapter 09 fixes.

## The pack shape

The pack has seven sections. The order matters — the audiences read top-to-bottom.

### Section 1 — The one-page summary

The audience opens here. The section covers, in one page (~500 words):

- **What happened.** One sentence in factual voice — no root-cause claim, no responsibility assignment.
- **When.** Awareness date, containment date, closure date (or *ongoing*).
- **What system.** The `INV-<year>-<sequence>` name plus a one-line description ("*customer-facing product recommendation assistant, RAG-based, in production since 2025-Q2*").
- **How it was surfaced.** The surface-of-report from the incident record.
- **Immediate impact.** Estimated users / systems affected; harm class if applicable per chapter 07's Article 3(49) evaluation.
- **What the enterprise did.** Containment actions (one-line summary), the incident-record status, and the fact-pattern of the governance follow-through (IA re-open triggered or not, register re-open triggered or not, PMS notification filed or not).
- **What changed as a result.** The corrective and preventive actions completed, with the artefact identifiers.
- **What remains open.** Any follow-through items still in flight, with owners and target dates.
- **What decision the reader is being asked to make.** Council-agenda item / internal-audit briefing / information-only.

The one-page summary is a hard limit. If it does not fit, the pack has the wrong altitude — either the incident is more than one incident (split), or the analyst is including detail that belongs in the deeper sections.

### Section 2 — The timeline

A chronological table from awareness through closure, with each row carrying:

| Time | Event | Actor | Artefact |
|---|---|---|---|
| T0 | Awareness — how the enterprise first learned | Reporting party | Source-of-report link |
| T0+15m | Incident record opened at intake | Analyst | `INC-<year>-<sequence>` |
| ... | Every containment action, every notification, every re-open trigger, every escalation, every sign-off | Named | Artefact ID |
| T-close | Incident record closed | Analyst | Closure rationale reference |

The timeline is factual, not narrative. Every row cites the underlying artefact so a reader can walk from the row to the evidence. Silent gaps (an hour or a day where nothing appears to have happened) are called out — silence in an incident timeline is either the enterprise waiting on a signal or the enterprise's record-keeping missing an event, and the reader deserves the honest characterisation.

### Section 3 — The root-cause narrative in analyst voice

The technical post-mortem's root cause, translated into governance vocabulary. The analyst does not author the technical root cause — the engineering team did that. The analyst *reads* the post-mortem and produces a paragraph or two that answers, for a governance reader:

- **What condition made the incident possible?** (The upstream condition — a distribution shift the monitoring did not capture, an evaluation gap, a deployment-process bypass, a third-party model update, a guardrail configuration that had drifted.)
- **What made it happen at the time it did?** (The triggering event — a specific traffic pattern, a specific user action, a specific external change.)
- **What allowed it to reach a user or downstream system?** (The gap in the mitigation stack — a control that failed, a signal that was missed, a threshold that was too loose, an escalation that did not fire.)
- **What did the enterprise assume that turned out to be false?** (The specific claim in the IA, FRIA, DPIA, register entry, or system card that the incident falsified. Chapter 04's Q1–Q4 walk lands here.)

The three-question shape is deliberately un-technical. A reader who does not know what the guardrail-classifier's ROC curve looks like can still read *the enterprise assumed the guardrail would refuse this class of prompt at the trained threshold, and the incident showed that on the current traffic mix the refusal rate is lower than the training baseline* and understand what changed.

### Section 4 — The cross-reference walk

Not a duplicate of the incident record's cross-reference block — a *reading* of it. Section 4 walks the reader from the incident to every affected artefact in the order a governance reader would think about them:

- **The system.** `INV-<year>-<sequence>` — one paragraph on the system's governance status (High-tier per `mod-102`, current IA version, current release-assurance eval-evidence baseline).
- **The register.** `RISK-<year>-<sequence>` entries the incident called into question — one paragraph per entry on the residual-risk claim, the incident's implication, and the re-scoring outcome.
- **The assessments.** `IA` / `FRIA` / `DPIA` entries the incident triggered a re-open on — one paragraph per assessment on the trigger (which of chapter 04's Q1–Q4), the update timeline, and the sign-off status.
- **The evaluations.** `EVAL-<year>-<sequence>` rows the incident indicates missed the failure mode — one paragraph on the evaluation the release-assurance sign-off cited and how the incident relates.
- **The controls.** `CTL-<year>-<sequence>` records the incident triggered a re-test on — one paragraph on the control statement, the re-test outcome, and any `mod-108` finding filed.
- **The vendors.** `VND-<year>-<sequence>` rows implicated — one paragraph per vendor on the vendor's role in the incident, the vendor-communication history, and any renegotiation triggered.
- **The PMS record.** For high-risk EU AI Act systems, `PMS-<year>-<inv-id>` — one paragraph on how the incident lands on the current period's summary and whether an Article 73 notification was drafted / submitted.

Section 4 is where a reader can most efficiently see the *blast radius* of the incident across the enterprise's governance record. Every paragraph cites the underlying artefact ID.

### Section 5 — The monitoring context

A short section — usually one page — that answers *what did the monitoring show, before and during and after*.

- **Before.** The three monitoring-reading notes (`MON-<year>-<month>-<inv-id>`) preceding the incident. What did they show; did any of them contain an unheeded escalation trigger; did they reveal a pattern in retrospect that the analyst missed at the time.
- **During.** The panel state at the moment of awareness. Screenshots of the relevant panels with URL and timestamp; the metric values; the threshold state.
- **After.** The two monitoring-reading notes following the incident. Did the containment restore the metric to baseline; are new panels or metrics in scope as a result of the incident.

Section 5 is where the *reading was done but the escalation was not* pattern is either confirmed or contradicted. If the pattern is confirmed, chapter 06's escalation-record discipline receives a `mod-108` control-testing finding for the missed escalation; the finding lands on the pack.

### Section 6 — Corrective and preventive actions

The table from the incident record's *corrective actions* and *preventive actions* fields, rendered with a status column:

| Action | Type (corrective / preventive) | Owner | Target date | Status | Resolving artefact |
|---|---|---|---|---|---|
| ... | ... | ... | ... | *complete* / *in-flight* / *deferred with rationale* | Artefact ID |

Corrective actions are what fix the specific instance; preventive actions are what stop the class of failure from recurring. The pack surfaces both. Preventive actions that were named but not completed by pack-publication are called out — the audience wants to know what the enterprise learned versus what the enterprise merely committed to.

### Section 7 — What the analyst recommends

The analyst is not the decision-maker, but the analyst is often the person best-positioned to name what the enterprise should decide next. Section 7 is a short (paragraph-length) recommendation, phrased as:

- **What the analyst thinks the enterprise should consider.** Not a decision — a recommendation. "*The analyst recommends the council consider whether the enterprise's current guardrail-classifier retune cadence is adequate for the observed rate of attack innovation.*"
- **What the analyst recommends against.** Where a plausible response would be worse than no action. "*The analyst recommends against a blanket-refuse policy on the affected content class; the FRIA cites protected expressive uses that would be affected.*"
- **What the analyst commits to doing next.** Follow-through inside the analyst's own scope. "*The analyst will re-open the FRIA at the next scheduled cycle regardless of whether the current re-open completes on target, per chapter 04's discipline.*"

The recommendation is analyst voice — it does not pre-empt the council's or the auditor's judgement, but it does say honestly what the analyst thinks and why. The audience can accept, modify, or reject.

## Composition discipline

The pack is composed after the incident record has closed, or after a natural mid-flight milestone (30 days post-awareness, at a natural governance-cadence boundary, on demand for an audit engagement). Composition is not open-ended — the following rules keep the pack usable.

- **The pack is self-contained but not duplicative.** Every claim cites the underlying artefact ID. The pack does not reproduce the artefact's content in full; the reader who wants full content clicks through. The pack's job is to give the reader the *reading* they cannot produce themselves.
- **The pack is dated and versioned.** *Composed 2026-08-15 against the state of the incident record on 2026-08-14 17:00 UTC.* If the underlying record changes after the pack ships, the pack is re-versioned; the prior version is retained.
- **The pack cites its own limits.** *Post-mortem landed on 2026-08-12; contributing-factors analysis by `ai-eval-engineer` is due 2026-08-25 and not reflected in this pack; a v2 pack will incorporate.* Silent omissions are a fail.
- **The pack respects read-permission boundaries.** Sensitive fields (personal-data-adjacent details, security-response internals, in-flight legal exposure) are redacted or replaced with a governance-appropriate abstraction. Chapter 03's read-permission notes apply.
- **The pack does not translate technical error into governance blame.** The engineering team's post-mortem may name specific individuals or specific errors; the analyst's voice in the pack stays at the *systemic condition* level. Blame belongs in the technical post-mortem, if anywhere; the governance pack asks what the assurance model missed, not who to fire.

## The council pack vs the internal-audit pack

The two audiences read the same pack, mostly, with two shape-differences.

### Council pack

- Section 1 is written for a reader who has not touched the system, may not remember the enterprise's specific IA / FRIA / DPIA position, and needs the *what changed at the enterprise level* answered efficiently.
- Section 7 addresses a decision the council might be asked to take — a policy question, an escalation-register roll-up read, a resource-allocation implication.
- Section 4 emphasises the register interaction and the assessment interaction over the control-record interaction, because the register and assessments are the council's usual reading vocabulary.
- The pack is short — 8 to 12 pages typical, with the one-page Section 1 as the read-first artefact and Sections 2–7 as the walk-through the interested member can go deeper on.

### Internal-audit pack

- Section 1 is written for a reader who has technical vocabulary but needs the incident's *governance* framing.
- Section 4 emphasises the control-record interaction (the `CTL-<year>-<sequence>` re-tests, the `mod-108` findings) because internal audit reads the controls.
- Section 5 is more detailed because internal audit will read the monitoring-reading notes as evidence of the enterprise's continuous-monitoring assurance operation.
- Section 6 carries the audit-visible confirmation of the corrective / preventive action outcomes; internal audit will re-test the completeness claim.
- The pack is medium-length — 10 to 20 pages typical — and the internal auditor will read every section.

Both packs share Sections 2, 3, and 5–6 content substantially. Sections 1 and 7 are audience-tailored; Section 4 has different emphasis. The analyst composes one *master* pack per incident and produces the audience-tailored versions from the master.

## The pack as evidence of the module's operation

An unstated benefit of the pack: it is the artefact `mod-108` reads to demonstrate that this module operated. The presence of a well-composed pack for each material incident is itself a `mod-108` control statement — *the enterprise produces a governance-consumption evidence pack for each material AI incident*. The absence of a pack for an incident that meets the *material* threshold (defined by the enterprise; typically any incident that triggered an IA re-open, an Article 73 notification, or a council briefing) is a finding.

The pack also lands in `mod-110` as an input to any council briefing that references the incident, and as an input to any communication artefact — customer letter, blog post, statement to regulator — that the enterprise composes about the incident.

## Common failure modes

- **The pack reads like the incident record.** The analyst reproduces the record's fields in the pack rather than composing a reading of them. Fix: the pack cites the record; the reader who wants the record clicks through.
- **The pack claims a root cause the post-mortem does not support.** The analyst's Section 3 narrative goes beyond what the engineering team wrote. Fix: the narrative reads the post-mortem; if the post-mortem is thin, the narrative acknowledges the limits.
- **The pack is composed before the post-mortem lands.** The analyst ships a pack with a *root cause TBD* section 3. Fix: pack composition is scheduled after post-mortem landing or after a natural mid-flight milestone with the milestone's limits called out.
- **Section 7 pre-empts the council's decision.** The analyst recommends a specific action the council might take, phrased as a decision. Fix: recommendations are recommendations, not decisions; the council decides.
- **The pack survives changes to the incident record without re-versioning.** The underlying record moves after pack composition, and the pack is not updated. Fix: pack versioning is explicit; if the underlying state changes materially, a v2 pack ships.
- **The council pack and the internal-audit pack are the same document.** The analyst delivers one pack to both audiences; the internal-audit pack lacks the depth the auditor needs; the council pack has depth the council does not need. Fix: audience-tailor Section 1, Section 4 emphasis, and Section 7.

## What to memorise

- **Seven sections:** one-page summary, timeline, root-cause narrative in analyst voice, cross-reference walk, monitoring context, corrective and preventive actions, analyst recommendation.
- **The pack is a *reading*, not a duplicate.** Every claim cites the underlying artefact.
- **The pack is dated, versioned, and self-limits.** Silent omissions and un-versioned updates are fails.
- **The council pack and the internal-audit pack share substantive content and differ in Section 1, Section 4 emphasis, and Section 7.**
- **The pack is composed after post-mortem landing or a natural mid-flight milestone, with the milestone's limits called out.**
- **The pack's presence — or absence — is itself a `mod-108` control-testing signal.**

## Summary

The post-incident evidence pack is the analyst's translation of the incident record into a reading a governance council or an internal auditor can consume cold. Seven sections — one-page summary, timeline, root-cause narrative in analyst voice, cross-reference walk across every affected artefact, monitoring context before / during / after, corrective and preventive actions with status, and analyst recommendation — with the audience-tailored council and internal-audit shapes sharing substantive content. The pack cites rather than duplicates; it is dated, versioned, and calls out its own limits; it stops at recommendation rather than decision; it stays at the systemic-condition altitude, not the individual-blame altitude. The pack's presence is itself a signal of the module's operation. Chapter 09 closes the module by stating the full delegation-boundary map and the four escalation classes the analyst uses when work outgrows the analyst's scope.
