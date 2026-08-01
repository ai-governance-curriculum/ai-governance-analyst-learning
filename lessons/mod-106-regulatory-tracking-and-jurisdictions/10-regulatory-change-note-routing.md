# Filing the Regulatory-Change Note and Routing It to Affected System Owners

## Why this chapter

The tracker (chapter 01) records the current state. But a static record does not, on its own, change what happens downstream in the enterprise. When a new obligation lands — a phased-in AI Act provision that is now enforceable, a Colorado AG implementing regulation that has clarified the *substantial factor* test, a NAIC bulletin that a new state has adopted, a Section 1557 rule injunction that has been lifted, an FDA guidance revision on PCCP scope — the analyst must convert the tracker update into a **regulatory-change note** and route it to the owners of the affected inventory rows so that they can revisit the impact-assessment corpus, update the register, and adjust the controls.

This chapter defines the change-note shape, the routing pattern, the review-trigger update that closes the loop into the impact-assessment corpus, and the failure modes the discipline is designed to prevent. It is the operational output of the whole module — the point at which the tracker's situational awareness becomes routed action.

## The failure mode this discipline prevents

Without the change-note discipline, three failure modes recur:

- **The regulation moves and the impact assessment does not.** The AI Act phase-in date passes; the affected system's FRIA-view is still dated *pre-phase-in*; the reviewer at the annual review or the auditor at the internal-audit walk finds an impact assessment that references a state of the regulation that is no longer current. This is the analyst's single most-common finding.
- **The regulation moves and the wrong owner is notified.** The analyst updates the tracker but sends the change-note to the general counsel's mailbox instead of to the specific system owner whose deployment is materially affected. Counsel does not act on operational routing; the affected system owner is unaware; the deployment continues on stale evidence.
- **The regulation moves and no one is notified.** The analyst updates the tracker's *last-verified* date and marks the row *in force* without generating a change-note. The tracker is up-to-date; the downstream artefacts have no signal that anything has changed. This is a documentation-only update that is worse than no update — it creates the appearance of coverage without the substance.

The change-note is the artefact that closes the loop. It is short, structured, addressed to the affected owners by name, and referenced from the inventory row and the impact-assessment corpus.

## The change-note shape

A regulatory-change note is a single Markdown document (or a single GRC-platform record) with the following structure. It is short — one page maximum — and terse.

### Header

- **Change-note identifier.** `CN-<year>-<sequence>`. Stable; never re-used.
- **Date.** Absolute date the note is filed. If the tracker source references a relative date (*last month*, *this quarter*), the change-note resolves it to an absolute date.
- **Filed by.** Analyst who filed the note.
- **Tracker row updated.** `REG-<year>-<sequence>` — the tracker row whose update triggered this note.
- **Related regulator artefacts.** Primary-source URL to the regulator's publication that occasioned the update (Federal Register notice, EUR-Lex citation, state-legislature bill page, regulator's guidance page, adopter-list update).

### Body

- **What changed.** One or two sentences, precise. *The Colorado Attorney General's implementing regulations for the Colorado AI Act SB24-205 [1 CCR 904-3](https://coag.gov/) were finalised on [date] and take effect [date]. Rule 6 clarifies the substantial-factor test for consequential decisions.* Not — *the Colorado rules landed*.
- **Why it matters here.** Two or three sentences on how the change affects the enterprise's operational surface. *Rule 6's clarification narrows the substantial-factor test relative to the enterprise's prior working interpretation. Inventory rows that were previously borderline on the substantial-factor test may now clearly qualify (or clearly not).*
- **Affected inventory rows.** Explicit list — `INV-XXXX-XXXX` (`[system name]`), one per line. This is the field that turns the change-note from an alert into a routed action. Empty list is a valid answer — *no inventory rows currently affected; retained as tracker update only*.
- **Affected impact-assessment artefacts.** For each affected inventory row, the specific canonical document (`CDX-XXXX-XXXX`), FRIA / AIA / DPIA / sector view IDs, model-card and register-entry IDs that must be reviewed against the change. This is the reading-and-action list for the affected owner.
- **Recommended action per owner.** One or two lines per affected inventory row: what the analyst is asking the owner to do (revisit the canonical document, refresh the residual-risk column of specific register entries, re-check the review-trigger field, flag to counsel for opinion on a specific question). No open-ended *please review* — a specific action.
- **Counsel / privacy-officer flag.** *Flagged to* — the counsel or privacy officer (chapter 07) who owns the legal characterisation of the change. Names or roles, dated. Where the change is a voluntary-code adherence-decision change (chapter 09), *flagged to governance owner and general counsel*.
- **Analyst next-step tracking date.** The date by which the analyst will re-check that the affected owners have actioned the note. Typically 14 to 30 days depending on the change's urgency.

### Footer

- **Change-note status.** *Open* (routed, awaiting owner action), *In progress* (owner is actioning), *Resolved — evidence attached* (owner has updated the impact-assessment corpus; the specific evidence artefact is cited), *Superseded by CN-YYYY-XXXX* (a subsequent change-note has replaced this one).
- **Cross-reference.** The tracker row this note updates, plus any prior change-notes on the same tracker row.

That is the shape. A five-sentence change-note with the eight fields populated is more actionable than a five-page memo with the same underlying facts.

## The routing pattern

The affected inventory rows in the change-note carry an implicit owner list — every inventory row has a system owner, a technical lead, a governance owner where the enterprise's structure separates the two, and a risk-register owner from `mod-102` chapter 03. The routing pattern the analyst uses:

- **Primary routing — the system owner.** The system owner is the person accountable for the deployment. They receive the change-note by direct notification (email, GRC-platform notification, or the enterprise's documented channel) and confirm receipt.
- **Secondary routing — the governance owner and risk-register owner.** These roles maintain the impact assessment and the register entries respectively. They receive the change-note in copy.
- **Tertiary routing — counsel or privacy officer.** For any change-note where a legal characterisation is engaged (chapter 07's flagging discipline; chapter 06's sector-specialist routing; chapter 09's voluntary-code adherence question), counsel or the privacy officer is copied and the *counsel / privacy-officer flag* field records the specific question.
- **No mass distribution.** A change-note that goes to a large mailing list does not have owners; it has spectators. If more than ten inventory rows are affected, the analyst files a summary change-note with the aggregate impact and files individual change-notes per system-owner cluster.

The routing channel is enterprise-specific — some enterprises route through the GRC platform's workflow engine, some through a governance-artefact repository with automated notification, some through a documented email path with the counsel and privacy office in copy. The channel matters less than the discipline: the routing is documented, the receipt is confirmed, and the analyst's next-step tracking date is honoured.

## Closing the loop into the impact-assessment corpus

A change-note is not closed until the affected owner has taken the action and the impact-assessment corpus reflects the change. The analyst-tier closure pattern:

- **Owner updates the canonical document's *review triggers and cadence* section.** The canonical document (`mod-105` chapter 01) carries an enumerated triggers list; the change-note-induced review is added to that list with the change-note ID as the trigger.
- **Owner updates the affected register entries.** The register entries (`mod-103` chapter 02) may need residual-risk revision if the change alters the enterprise's compliance posture. The analyst is not the register-entry updater — the risk-register owner is — but the change-note requests the review.
- **Owner regenerates the affected regulator views.** Where the change alters an AIA / FRIA / DPIA / sector view (`mod-105` chapters 02–05), the view is regenerated from the (possibly-updated) canonical document. Regeneration is cheap when the shared-template discipline from `mod-105` chapter 01 is honoured.
- **Owner attaches the evidence artefact to the change-note.** *Register entries RR-XXXX-XXXX and RR-XXXX-XXXX residuals reviewed on [date]; FRIA view regenerated as CDX-XXXX-XXXX-v3.* The change-note's *Resolved — evidence attached* status is set with the citation.
- **Analyst re-checks on the next-step tracking date.** If the change-note is still *Open* on the tracking date, the analyst escalates via the routing pattern from `mod-103` chapter 05.

The closure discipline is what turns the tracker from an evidence artefact into an operational-hygiene tool. Without closure, the tracker is a list; with closure, the tracker is a system.

## Concrete example — the MCDA-Benefits phase-in change-note

Suppose it is 3 August 2026 — the day after the AI Act's Article 27 FRIA obligations became enforceable for Annex III high-risk deployers. The analyst files:

```
Change-note identifier: CN-2026-0044
Date:                    2026-08-03
Filed by:                Analyst
Tracker row updated:     REG-2026-EU-003 (EU AI Act — Article 27 FRIA)
Related regulator artefacts:
                         Article 27 of Regulation (EU) 2024/1689 —
                           enforceable from 2 August 2026 per Article 113
                         AI Office FRIA notification template
                           (verify current URL and template revision)

What changed:
  The EU AI Act Article 27 FRIA obligation on in-scope high-risk-system
  deployers became enforceable on 2 August 2026. In-scope deployers must
  now have a completed FRIA on file and — per Article 27(3) — notify the
  national market-surveillance authority of the FRIA results using the AI
  Office template.

Why it matters here:
  The MCDA-Benefits deployment at INV-2026-0088 is a public-body deployment
  of a high-risk (Annex III point 5(a) — essential public benefits) AI
  system. Article 27 attaches directly. The FRIA view CDX-2026-0198-v2 was
  drafted in Q2 and is on file but has not been notified to the national
  market-surveillance authority.

Affected inventory rows:
  INV-2026-0088 (MCDA-Benefits)

Affected impact-assessment artefacts:
  INV-2026-0088 →
    Canonical document CDX-2026-0198-v2
    FRIA view          CDX-2026-0198-FRIA-v2
    DPIA view          CDX-2026-0198-DPIA-v2
    Register entries   RR-2026-0311, RR-2026-0312, RR-2026-0313, RR-2026-0314
    Model card         MC-2026-0044-v3

Recommended action per owner:
  INV-2026-0088 (system owner: Benefits Casework Ops, governance owner:
  Public-Sector AI Council chair, risk-register owner: Enterprise Risk):
    (a) Notify the national market-surveillance authority of the FRIA
        results using the AI Office template. Target date: 2026-08-10.
    (b) Add change-note CN-2026-0044 to the CDX-2026-0198-v2 review-triggers
        list.
    (c) Confirm the FRIA view CDX-2026-0198-FRIA-v2 remains current given
        Article 27(1) elements — no known change in the underlying facts
        since drafting. If a review flags a fact change, regenerate the
        FRIA view.

Counsel / privacy-officer flag:
  Flagged to General Counsel and Data Protection Officer (Public-Sector
  Practice) for opinion on the notification content and on the interaction
  with the DPIA view CDX-2026-0198-DPIA-v2 residuals.

Analyst next-step tracking date:
  2026-08-17 (two weeks).

Change-note status:
  Open (routed 2026-08-03; awaiting owner action).

Cross-reference:
  Updates REG-2026-EU-003; supersedes no prior change-notes on this row.
```

That is the shape. The note is short enough to read at the top of a Monday-morning inbox, and specific enough that a system owner can start the work without a follow-up call.

## Where the change-note discipline stops for the analyst

- **Not the owner's action itself.** The analyst files the note; the owner executes the action. The analyst does not draft the market-surveillance-authority notification content, does not rewrite the FRIA, does not opine on the DPO's read.
- **Not the enterprise's change-management process.** The change-note routes into whatever change-management or governance-workflow process the enterprise runs. The analyst uses the process; the analyst does not reinvent it.
- **Not the audit-log artefact.** The change-notes cumulatively form an audit-log of regulatory-change response; the analyst files each note in the enterprise's governance-artefact repository so that the log is discoverable. Whether the log is the *primary* audit-evidence artefact — as opposed to being one of several evidence sources — is `mod-108`'s question.
- **Not the substitute for annual review.** Change-notes are the response to specific triggers; the annual review (`mod-105` chapter 08's walk cadence) is the systemic review that catches drift the change-notes missed.

## What to memorise

- **The change-note is the artefact that turns a tracker update into routed action.** Without the note, the tracker is a list; with the note, the tracker is a system.
- **The change-note structure — header (identifier, date, filer, tracker row, related regulator artefacts), body (what changed, why it matters, affected inventory rows, affected impact-assessment artefacts, recommended action per owner, counsel flag, next-step tracking date), footer (status, cross-reference).**
- **The routing pattern — primary to system owner, secondary to governance / risk-register owners, tertiary to counsel / privacy officer. No mass distribution.**
- **The closure discipline — the change-note is closed when the owner has updated the review-triggers list, revisited the register entries, regenerated affected regulator views, and attached the evidence artefact.**
- **The failure modes the discipline prevents — the regulation moves and the impact assessment does not; the regulation moves and the wrong owner is notified; the regulation moves and no one is notified.**

## Summary

The regulatory-change note is the operational output of the module. It is a short, structured artefact that converts a tracker update into routed action across the affected inventory rows, addresses specific system owners with specific requested actions, flags counsel or the privacy officer where legal characterisation is engaged, and is closed only when the impact-assessment corpus reflects the change and the evidence artefact is attached. The routing is direct — primary to the system owner, secondary to the governance and risk-register owners, tertiary to counsel — and the closure discipline is what keeps the tracker's situational awareness aligned with the impact-assessment corpus over time. The change-note pattern is what makes the tracker's cadence honest, the flagging discipline actionable, and the impact-assessment corpus current as the regulatory landscape moves.
