# Council Minutes That Survive Audit

## Why this chapter

The council pre-read (chapter 04) is the input to the meeting. The minutes are the output — and the minutes are what the internal auditor, the external auditor, the regulator, and (three years hence) the next generation of council members will read to reconstruct what the enterprise decided about its AI portfolio and *why*. A pre-read badly written wastes the members' meeting hour. Minutes badly written waste the enterprise's audit posture.

*Minutes that survive audit* has a specific meaning. It means the minutes are complete enough that a reader with no other context can walk from the minutes back to the underlying artefacts, understand what was decided, understand who took the decision, understand what conditions or dissent were recorded, and understand what happened next. Missing that standard has real-world cost: a regulator asking *why did you deploy this high-risk system?* answered by a minute entry that reads *"Item 6b: discussed"* is a regulator finding. A residual-risk acceptance recorded as *"the council agreed"* without an owner name is an internal-audit finding. A dissent that a member offered and the minute omitted is an integrity finding.

The analyst is the meeting's *secretary* — the drafter and steward of the minute record. The chair *approves* the minutes; the council *ratifies* them at the next meeting. Chapter 04 fixed the pre-read; this chapter fixes the minutes and the action-item register that walks out with them.

## The two artefacts

Every meeting produces two related artefacts:

1. **The minutes.** The formal record of the meeting — attendance, agenda items discussed, decisions taken (with the vote outcome), dissent captured, actions assigned. Circulated within a few business days of the meeting; approved by the chair; ratified by the council at the next meeting.
2. **The action-item register.** The rolling list of every open action item across meetings — action ID, source-meeting date, description, owner, due date, status. Updated at meeting-close (with actions added) and at each subsequent meeting (with statuses updated). Lives in the GRC platform or the enterprise's project-tracker, not in the minute document itself.

The two are cross-referenced. Every action item in the register cites the minute-entry that created it; every minute-entry that assigns an action cites the action-item ID.

## The minutes template

Boring on purpose, consistent from meeting to meeting.

```
[Enterprise] — AI Governance Council — Meeting Minutes
Meeting: [YYYY-MM-DD]  ·  Start: [HH:MM tz]  ·  End: [HH:MM tz]
Chair: [name, role]  ·  Secretary: [analyst name]
Attendees: [list, one per line, with role]
Apologies: [list, with role]
Quorum met: [yes / no per terms of reference]
Prior minutes reference: [meeting date, link]

1. Minutes of the previous meeting
   Approved as circulated. / Approved with corrections [describe].
   (If any member proposed corrections, name the member and the correction.)

2. Action items from previous meetings
   Reviewed. See action-item register [link] for current state.
   Notable updates:
   • [ACT-YYYY-NNNN] — [one-line update]
   • [ACT-YYYY-NNNN] — [one-line update]

3. Portfolio status
   Presented by [analyst]. Discussion:
   • [Substantive point 1 — one sentence, member attributed]
   • [Substantive point 2]
   No decisions taken.

4. New intakes and tiering decisions
   • [INV-YYYY-NNNN, system name] — tiering: [tier]. Presented by [role].
     Discussion: [one to two sentences]. Decision: [approved as presented /
     re-tiered to [tier] / deferred pending [artefact]].
   (Repeat per intake.)

5. Impact-assessment sign-offs
   [IA-YYYY-NNNN / FRIA-YYYY-NNNN / DPIA-YYYY-NNNN] — [system name].
   Presented by [role]. Discussion: [one to two sentences].
   Decision: [signed off / signed off with conditions / returned for edits /
   deferred pending [artefact]].
   Conditions (if any): [list].
   Dissent (if any): [member name] — [verbatim or paraphrased statement].

6. Residual-risk acceptances
   [RISK-YYYY-NNNN] — residual score [score], owner [role].
   Presented by [risk owner]. Discussion: [one to two sentences].
   Decision: [endorsed / endorsed with conditions / rejected — require
   further mitigation / escalated to board (chapter 03)].
   Conditions (if any): [list].
   Dissent (if any): [member name] — [statement].
   Actions: [ACT-YYYY-NNNN] — [description], owner [role], due [YYYY-MM-DD].

7. Incident and monitoring roll-up
   Presented by [analyst]. Substantive items:
   • [INC-YYYY-NNNN] — [one-line summary]. Discussion: [if any].
     Decision: [note taken / require post-mortem re-review / escalate /
     require Article 73 draft review at next meeting / etc.].
   PMS records in flight: [count]. Notable: [item].

8. Policy and standard work in flight
   [Draft name, version, phase — first-cut / edits / ratification-track].
   Owner: [role]. Discussion: [if any]. Decision: [approved for
   next-phase routing / returned for [named] revisions / etc.].

9. Regulatory-tracker headlines
   New obligations since last meeting:
   • [Obligation name, jurisdiction, effective date, tracker-row ID].
     Discussion: [one line]. Portfolio implication: [one line].
   No decisions taken (or: decision to sequence [item] into policy work
   as [ACT-YYYY-NNNN]).

10. Escalations from the escalation register
    • [ESC-YYYY-NNNN] — [description]. Discussion: [one to two sentences].
      Decision: [assigned to [role] with [ACT-YYYY-NNNN] / re-classified /
      returned to originating role / etc.].

11. AOB
    [Named items discussed; decisions if any.]

12. Decisions taken this meeting (recap)
    D1  [Item 4, INV-...]: [decision text]
    D2  [Item 6, RISK-...]: [decision text]
    D3  [Item 8, Draft-X]: [decision text]
    (Full list, keyed to agenda item and artefact ID.)

Actions assigned this meeting
    [ACT-YYYY-NNNN] — [description] — owner [role] — due [YYYY-MM-DD]
    [ACT-YYYY-NNNN] — [description] — owner [role] — due [YYYY-MM-DD]

Next meeting: [YYYY-MM-DD]
```

Length depends on the council's volume, but the *decisions taken this meeting* section is the audit-load-bearing block. If it is missing or vague, nothing else the minutes contain rescues them.

## What "survives audit" means, field by field

- **Attendance and quorum.** Named individuals with roles, distinguishing attendees from apologies. Quorum is a terms-of-reference determination — the analyst confirms with the chair whether the meeting's decisions carry weight if quorum was not met. Un-quorate decisions are recorded as *un-quorate; ratification at next meeting required*.
- **Prior-minutes approval.** The council either approves the previous minutes as circulated or approves with corrections. Silent absence of this line breaks the chain of ratification.
- **Decisions.** Every decision names: the artefact by ID, the decision text (from the option set on the pre-read's decisions-needed slide), the vote outcome (unanimous, majority, dissent), the conditions where the decision is *approved with conditions*, and any dissent captured verbatim (or paraphrased with the member's approval).
- **Dissent.** If a member dissented and asked for it to be recorded, the minute records the dissent by name and either verbatim or by faithful paraphrase. Silent omission is an integrity failure. The chair may not remove recorded dissent; that removal would be a corrections item at the next meeting, with the dissenting member's agreement.
- **Conditions.** Where a decision is *approved with conditions* (or *signed off with conditions*), the conditions are numbered and each has a follow-through owner and — where the condition is time-bound — a due date and an action-item ID.
- **Actions.** Every action item is written to be executable — a named owner, a named artefact or output, a named due date. *"Legal to look into it"* is not an action; *"Legal [named delegate] to draft a two-paragraph note on GDPR Article 22 applicability to [INV-YYYY-NNNN] by [YYYY-MM-DD]"* is.
- **Cross-references.** Every substantive minute-entry cites the underlying artefact ID (`INV-`, `RISK-`, `IA-`, `INC-`, `PMS-`, `EVAL-`, `CTL-`, `VND-`, `ESC-`, or the enterprise's equivalent).

The audit-survival test the analyst runs on the draft before circulating: *if an auditor reads only these minutes, can they reconstruct what was decided, by whom, on what basis, and what happened next?* If not, the analyst fixes the draft before it goes to the chair.

## Language discipline in the minutes body

Minutes are a formal record, not a transcript and not a narrative. Language conventions:

- **Third person, past tense, active voice where possible.** *"The council endorsed the residual acceptance on RISK-2026-0104."* Not *"We approved..."* and not *"It was approved..."* (which loses attribution).
- **Verbatim only where the member requested it.** Discussion is paraphrased in one to two sentences per substantive point, with member attribution (*"Legal noted that..."* / *"The privacy delegate observed that..."*). Verbatim quotation is reserved for dissent-on-record and for the specific-conditions text the council approved.
- **No personal-opinion language.** Not *"the presenter did a good job"*, not *"this discussion was heated"*. Minutes record what was decided; tone-of-meeting notes belong in the analyst's separate operating record, not on the audit-visible minute.
- **No side-of-mouth attribution.** *"A member noted that legal risk was overstated"* — which member? Attribute or omit; do not half-attribute. Members who spoke on the record are named on the record.
- **No content the enterprise cannot legitimately record.** Personnel matters, legal-privileged discussions, market-sensitive commercial information — the minute records the *fact* of the discussion and the decision, referenced to the underlying (sealed or privileged) record, not the substance. Chapter 04's *sensitive item* pattern applies here.

## The action-item register

The register sits alongside the minutes and is where action items actually get tracked. Its rows:

| Field | Content |
|---|---|
| Action ID | `ACT-<year>-<sequence>` |
| Source meeting | Date (YYYY-MM-DD) |
| Source minute entry | Agenda item # and (typically) the item's underlying artefact ID |
| Description | One sentence, executable |
| Owner | Named role or individual |
| Due date | YYYY-MM-DD |
| Status | *open* / *in-flight* / *complete* / *deferred with rationale* / *blocked with named blocker* |
| Evidence of completion | Link or artefact ID when *complete* |
| Rationale for deferral | Text when *deferred* |
| History | Timestamped log of status changes and updates |

The register is a live artefact — the analyst updates it at meeting-close (adding new items), at each subsequent meeting (statuses reviewed in agenda item 2), and continuously between meetings (as owners report completion or blockers).

Items that stall for two consecutive meetings without progress are escalated to the chair — as *"either move this or defer it explicitly; we do not carry stalled items indefinitely"*. Silently-carried items are the failure mode; the escalation is what prevents them.

## Retention, access, and versioning

- **Retention period.** Set by the enterprise's records-retention policy. For AI governance council minutes, the analyst assumes at minimum the retention required for the longest-running applicable regulatory obligation — for the EU AI Act's high-risk regime this is typically 10 years from the AI system's placing-on-the-market (per the technical-documentation retention requirements the analyst confirms with legal, since specific-article obligations differ). <!-- needs-research: specific EU AI Act article and duration for post-market documentation retention; last-authored based on general 10-year assumption. Confirm current text against Regulation (EU) 2024/1689. -->
- **Access.** Council members and the chair by default. `internal-audit` on request. `external-audit` and regulators under the enterprise's disclosure protocols. The analyst confirms access rules with the chair and `legal` at the start of the analyst's tenure and again whenever the enterprise's disclosure posture changes.
- **Versioning.** Once ratified at the next meeting, a minute record is *frozen*. Corrections thereafter follow the enterprise's records-correction process (typically a chair-signed correction appendix, not an edit-in-place). The analyst never edits a ratified minute silently.

## The decision-record pattern in detail

Because the decision record is the audit-load-bearing block, it is worth pulling out. Every council decision reduces to five fields the minute must carry.

| Field | Content | Failure mode if missing |
|---|---|---|
| Decision ID | `DEC-<year>-<sequence>` (or agenda-item-plus-meeting-date if the enterprise's system does not assign) | Cannot cross-reference later |
| Artefact scope | The specific artefact ID(s) the decision is *about* | Decision floats — cannot tie to what it decided on |
| Decision text | The exact option chosen from the pre-read's option set | Reader cannot tell what was decided |
| Vote outcome | *unanimous* / *majority with N in favour, M against, K abstaining* / *chair's decision (where terms of reference permit)* | Cannot tell whether the decision carries |
| Conditions and dissent | Named conditions with owners and due dates; named dissent verbatim or paraphrased with permission | Silent conditions and silent dissent are integrity failures |

A good analyst maintains a *decision log* — a spreadsheet or GRC-platform view — that is the union of the decision-record fields across every meeting. It answers *"has the council ever decided X?"* in one query, which is the question the auditor most often asks.

## Common failure modes on the minutes

- **Silent quorum.** The minute does not say whether quorum was met. If it was not, the decisions taken may not carry — the analyst has to force this determination on the draft.
- **Un-attributed dissent.** *"There was some concern about the residual score"* — from whom? Attributed dissent is a member-of-record's on-the-record view; un-attributed dissent is meeting-room chatter and does not belong in the minutes.
- **Silent conditions.** *"Approved with conditions."* — which conditions? Every condition is written out, numbered, and given an owner and (where applicable) a due date and action-item ID.
- **Actions without owners or dates.** *"Legal to review."* — by when? *"Someone to draft the update."* — who? Every action has both.
- **Post-meeting rewrite.** The analyst attends the meeting, writes verbatim-shaped notes, then reshapes them into the minute style days later — losing decisions the note-taker did not recognise as decisions at the time. Fix: the analyst writes the minute in the standard shape *during* the meeting, treating the pre-read as a scaffold that fills in with decisions and paraphrase live. Post-meeting cleanup is minor edits, not fresh drafting.
- **Silent overwrites of a ratified minute.** A member spots an error two meetings later; the analyst edits the minute file directly. This is a version-control failure. Fix: corrections go through the enterprise's records-correction process, never silent edits.
- **Sensitive substance leaked into the minute.** A member asked for a privileged legal opinion during discussion and the minute paraphrased the opinion. Fix: the fact of the discussion and the decision go on the minute; the substance goes on the sealed / privileged record referenced from the minute. `legal` and the chair own this call.
- **The minute reads like a chat transcript.** Long, discursive, unattributed, un-decisional. Fix: the minute records decisions and substantive points, not the flow of the conversation.

## The interaction with the escalation register

Decisions the council takes may create escalations to other roles — a residual-risk rejection that requires additional mitigation from the risk owner, a policy-work item routed to `senior-ai-governance-architect`, an incident item requiring a board briefing at the next quarterly touch-point. The interaction:

- The minute records the decision and the action-item ID assigned.
- The action-item register carries the action.
- Where the action rises to *escalation* — meaning it belongs on the enterprise's cross-role escalation register (`mod-108` chapter 09) — the analyst files an `ESC-<year>-<sequence>` and links it from the action-item register row.

The council does not adjudicate every escalation itself; the escalation register is the shared workflow across `head-of-ai-governance`, `senior-ai-governance-architect`, and the analyst.

## What to memorise

- **Two artefacts: the minutes and the action-item register.** The minutes are the formal record; the register is the live workflow.
- **Every decision has five fields: ID, artefact scope, decision text, vote outcome, conditions and dissent.** Missing any of them breaks audit survival.
- **Attribution is on-the-record.** Named members, named roles, named artefacts. No un-attributed dissent, no un-attributed action.
- **Verbatim only where a member requested it or where the specific-conditions text was voted on.** Otherwise, paraphrase.
- **The minutes are frozen once ratified.** Corrections follow the enterprise's records-correction process, never silent edits.
- **The audit-survival test.** A reader with no other context can reconstruct what was decided, by whom, on what basis, and what happened next.

## Summary

Council minutes are the audit-load-bearing artefact of the entire meeting cycle. They record attendance, decisions taken (with vote outcome, conditions, and dissent), and actions assigned — in a standard shape, in formal language, with every substantive claim cross-referenced to an artefact ID and every decision keyed to the pre-read's option set. The action-item register carries the actions forward as a live workflow. The chair approves; the council ratifies at the next meeting; once ratified, the minutes are frozen and corrections follow the enterprise's records-correction process. The analyst is the secretary — drafter and steward of the record. Chapter 06 turns to the first-cut policy and standard drafts the analyst originates to route into the ratification chain.
