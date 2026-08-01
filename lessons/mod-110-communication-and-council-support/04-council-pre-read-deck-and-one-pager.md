# The Council Pre-Read: Deck, One-Pager, Standing Agenda

## Why this chapter

Most enterprises with a materially sized AI portfolio run an *AI governance council* — sometimes named an AI ethics committee, an AI review board, a responsible-AI council, an AI risk council, or the enterprise's specific variant. Its terms of reference vary; its typical cadence is monthly (with a full quarterly review) and its typical membership crosses `head-of-ai-governance` (usually the chair), `legal`, `privacy` / DPO, `security` (usually a CISO delegate), a business-line owner or two, and — depending on posture — a fairness / responsible-AI SME. Board-tier oversight rolls up out of it (chapter 03); operational tickets flow out to product, security, privacy, and legal (chapter 02).

The council does not investigate systems from scratch inside its meeting. It reads a pre-circulated packet, focuses the meeting time on the items that need discussion or a decision, and leaves with a set of minutes and an assigned action list. The packet is the analyst's tangible output for this artefact family. If the packet is coherent, the meeting is coherent; if the packet is chaotic, the meeting is a first-read exercise and no decisions land.

This chapter fixes the packet shape (the pre-read: deck + one-pager), the standing agenda that structures it, and the on-cycle discipline that makes the whole cadence sustainable. Chapter 05 handles the minutes and action-item output; together the two chapters define the meeting-packaging artefact.

## The standing agenda

Councils that decide things run standing agendas. Standing agendas mean members do not have to re-learn the meeting shape month to month; they can also spot the *missing* agenda item — which is often the most-important signal. A worked default:

1. **Minutes of the previous meeting.** Approve, or note corrections. Two minutes.
2. **Action items from previous meetings.** Status against each open action item — *done*, *in-flight*, *deferred with rationale*, *blocked with owner*. Two to five minutes.
3. **Portfolio status.** Number of AI systems in scope, delta from last meeting, tier / register-scoring distribution, control-status roll-up, vendor-risk-register roll-up. One slide, one minute. The one-pager (below) is the deep dive.
4. **New intakes and tiering decisions.** New AI systems intaked since the last meeting, their tiering decisions (per `mod-102`), and any tiering that requires council sign-off (typically the EU AI Act *high-risk* determinations and the *prohibited* / *not-permitted* determinations). Five to ten minutes.
5. **Impact-assessment sign-offs pending.** IAs, FRIAs, and DPIAs that reached council-attention threshold or where the assessment's original owner requested council review. Five to ten minutes.
6. **Residual-risk acceptances above threshold.** Register entries whose residual-risk score sits above the enterprise's council-attention threshold (per `mod-103`); the risk owner presents; the council either endorses the acceptance, defers with conditions, or rejects and requires further mitigation. Ten to fifteen minutes.
7. **Incident and monitoring roll-up.** The incident record set from `mod-109` (new, in-flight, closed since last meeting) and the monitoring-reading roll-up. Five to ten minutes; longer if a serious incident is in scope.
8. **Policy and standard work in flight.** First-cut drafts (from `mod-110` chapter 06), edits in progress (with `senior-ai-governance-architect`), items pending ratification (with `head-of-ai-governance` or the enterprise's policy-approval workflow). Five to ten minutes.
9. **Regulatory-tracker headlines.** New obligations that landed since the last meeting (from `mod-106`), impact assessment on the portfolio, sequencing decisions the council needs to make. Two to five minutes.
10. **Escalations from the escalation register.** Items escalated in from `mod-108` / `mod-109` that require council attention or decision. Variable.
11. **AOB / open floor.** Named items only — the chair does not accept new escalations from the floor without a written brief.
12. **Decisions needed this meeting.** A reprint of the decisions-needed one-slide (below) with the council's decisions marked live. Two minutes.

The order, timings, and section names are the enterprise's to set. The discipline is: the same shape every month, the same author (the analyst), the same delivery cadence (typically 48 to 72 hours ahead of the meeting), the same length ceiling (typically 15 to 25 slides plus one one-pager).

## The pre-read pack: what is in it

Two artefacts, delivered together:

### The deck

The deck follows the standing agenda one section per slide (or two slides where the section is heavy). It is not a general-purpose slide deck; it is a working document for the meeting. Design principles:

- **One slide per agenda item.** Two only where the item cannot fit — a serious-incident review typically needs a timeline slide and a decision slide.
- **The decision or discussion question is the slide's title.** Not *"Portfolio Status Q3"* — instead *"Approve tier-1 residual for RISK-2026-0104?"* or *"Portfolio: 3 systems now sit above appetite — pattern to note?"* The title tells the member what to be reading for.
- **Cross-references by ID.** Every claim on the slide traces to an artefact ID (per chapter 02's rule).
- **No confidential material that a member cannot legitimately read.** The council reads at a policy / oversight altitude; if a slide contains material a specific member is not cleared for (customer PII, market-sensitive commercial data), it does not belong on the pack. The analyst confirms read-permissions with the chair and the security / privacy delegates before circulating.
- **Speaker notes carry the depth.** The slide surface is short; the notes carry the underlying detail and the analyst-authored talking points for whoever presents the slide (often the risk owner or the assessment's original owner, not the analyst).

Slides that recur every meeting can be templated; the analyst maintains a template deck and updates the deltas each cycle.

### The one-pager

The one-pager is a single-page written summary of the portfolio state and the meeting's asks. It exists because members skim the deck but read the one-pager. Its shape:

```
[Enterprise] — AI Governance Council — Pre-Read
Meeting: [YYYY-MM-DD]  ·  Chair: [name]  ·  Secretary: [analyst]

Portfolio at a glance
   • [N] AI systems in scope (delta from last meeting: [±M])
   • Tier distribution: [x prohibited / y high-risk / z limited-risk / w minimal-risk] (or the enterprise's equivalent)
   • Register entries above council-attention threshold: [count] (from [count] last meeting)
   • Open incidents: [count]  ·  in-flight PMS records: [count]
   • Control-status: [x% of controls tested this cycle, y open findings]
   • Vendor-risk register: [count of high-risk vendor rows]

Since last meeting
   • [Notable change 1 — one line, ID-cited]
   • [Notable change 2]
   • [Notable change 3]
   (Aim for 3–6 bullets; skip if nothing material.)

Decisions the council is asked to take today
   1. [Concise ask — the specific decision requested]  ·  agenda item [#]
   2. [Concise ask]  ·  agenda item [#]
   3. [Concise ask]  ·  agenda item [#]

For information only (no decision requested)
   • [Item 1]
   • [Item 2]

Escalations pending council direction
   • [Item 1 — one line, escalation ID cited]
   • [Item 2]

Cross-references
   • Full deck: [link]  ·  Prior minutes: [link]  ·  Escalation register: [link]
```

The one-pager is what a member who has ten minutes before the meeting actually reads. If a member cannot walk out of that read knowing what the meeting will decide, the pre-read has failed.

## The decisions-needed slide

The single most important slide in the deck is the *decisions needed this meeting* slide. It appears twice — once early in the deck (so members know what they are working toward across the meeting) and once at the end (so the chair can walk the council through the votes at close of business).

A worked shape:

| # | Decision requested | Agenda item | Recommending role | Options |
|---|---|---|---|---|
| D1 | Endorse the residual-risk acceptance on `RISK-2026-0104` | 6 | Risk owner: [name] | Endorse / defer with conditions / reject |
| D2 | Approve first-cut GenAI Employee Guidance for ratification-track routing | 8 | `ai-governance-analyst` | Approve / return for edits / defer |
| D3 | Endorse the Article 73 serious-incident notification draft for `INC-2026-0018` | 7 | `head-of-ai-governance` | Endorse for submission / require edits / escalate to board |

Every decision on the slide has: a one-line description, the agenda item it corresponds to, the role recommending it, and the option set. *Options* — not *approval-or-not* — because most council decisions have three or more legitimate outcomes and reducing them to yes/no obscures the real choice.

The analyst confirms with the chair, ahead of the meeting, that the decisions listed are the decisions the chair is prepared to take that day. Surprise decisions do not appear on the decisions-needed slide; they belong on the *for information* list, escalated to the *decisions* list at the *next* meeting.

## Delivery cadence and workflow

Typical monthly cadence, with day counts anchored to the meeting date M.

| Day | Task | Owner |
|---|---|---|
| M − 14 | Standing-agenda draft circulated to chair for adjustments | analyst |
| M − 10 | Content owners (risk owners, assessment owners, incident post-mortem writers) notified of expected pre-read contributions and deadlines | analyst |
| M − 7 | Content contributions due to the analyst | contributors |
| M − 5 | First-draft deck and one-pager to `head-of-ai-governance` and the chair for review | analyst |
| M − 3 | Chair-approved deck and one-pager circulated to council members with the invitation | analyst |
| M | Meeting | chair; analyst as secretary |
| M + 1 | Draft minutes to chair for approval | analyst |
| M + 3 | Chair-approved minutes circulated to council members and appended to the minute record | analyst |
| M + 5 | Action-item register updated in the GRC platform and delivered to action owners | analyst |

The cadence is what makes the cycle sustainable. Slip any of the pre-meeting dates and the pack lands cold; slip any of the post-meeting dates and the action items evaporate.

## Where the pre-read gets its content

The analyst does not compose the pre-read from scratch each cycle. Each section maps to an artefact set the earlier modules produced.

| Pre-read section | Source artefacts |
|---|---|
| Portfolio at a glance | `mod-102` inventory row roll-up |
| Tier distribution | `mod-102` inventory row tier field roll-up |
| Register entries above threshold | `mod-103` register roll-up (with `mod-103` chapter 05's *council-attention threshold* filter) |
| Open incidents | `mod-109` incident register |
| PMS records in flight | `mod-109` chapter 07 |
| Control-status | `mod-108` control-status report |
| Vendor-risk roll-up | `mod-108` chapter 06 |
| Impact-assessment sign-offs pending | `mod-105` corpus |
| Regulatory-tracker headlines | `mod-106` tracker |
| Escalations pending | `mod-108` / `mod-109` escalation register |
| Policy and standard work in flight | chapter 06 of this module |
| Decisions needed today | Composed by the analyst from all the above, in agreement with the chair |

The analyst's per-cycle work is the roll-up, the delta computation, and the packaging — not fresh authoring. If the analyst finds that the pre-read content is not derivable from the existing artefacts, that is itself a finding: the underlying artefact is missing a field or a cadence, and the analyst files back to the appropriate earlier-module owner rather than filling the gap by hand.

## Handling the *sensitive item* pattern

Some items that would ordinarily belong in the pre-read cannot be circulated ahead of time — an in-flight legal-privileged item, a serious-incident notification pending regulator submission, a personnel matter, market-sensitive commercial information. The pattern:

- The pre-read *names the item* in one line — *"Item 6b: sensitive matter, briefed verbally by [role]"* — so members know a discussion is coming and can allocate time.
- The substantive brief is delivered verbally in the meeting.
- The minutes (chapter 05) record what the council decided, in a form that survives audit while respecting the sensitivity — usually by decision-only entry and a reference to the underlying legal-privileged or sealed record, not by verbatim substance.

The analyst does not decide unilaterally that an item is sensitive; the chair, `legal`, and the security / privacy delegates do. The analyst asks.

## Common failure modes on the pre-read

- **Too long.** Fifty-slide decks that no member has read by meeting time. Fix: the length ceiling is a hard target; overflow goes into appendix slides that are *not* on the meeting agenda but are cited in the speaker notes.
- **No decisions-needed slide.** The meeting drifts because no member (including the chair) is clear on what they are being asked to decide. Fix: chapter 05's minute template requires a decision-list section; work backwards from that — the decisions-needed slide is the sibling of the minutes.
- **Slides written for the analyst's confidence, not the member's read.** *"Chapter 02 of the Enterprise Control Library maps clause 9.1.2 of ISO/IEC 42001 to the following..."* — the analyst is proving they read the library. The member is trying to decide whether to endorse a residual. Fix: the slide title is the decision or the read-for question, always.
- **The one-pager duplicates the deck instead of summarising it.** Every bullet in the one-pager should be a synthesis, not a copy from a slide. If a member reads the one-pager and gets a different picture from the deck, either the one-pager or the deck is wrong.
- **The pre-read circulates late (M − 1, M − 0).** Members skim it in the meeting. Discussions become first-read exercises. Fix: the cadence is a management-review commitment, not a soft target. The analyst escalates late-source-artefact problems (a missing risk-owner brief, an incomplete incident post-mortem) to the chair rather than delaying the pack.
- **Sensitive items on the circulated pre-read that should have stayed verbal.** Fix: the analyst confirms with the chair and the security / privacy delegates whenever a candidate item touches privilege, market-sensitivity, personnel, or in-flight regulator submission.
- **Standing agenda drift.** New sections added ad-hoc, old sections dropped without a decision. Members lose the shape. Fix: agenda changes are a chair decision, minuted, and applied to the standing-agenda template from that meeting forward.

## What to memorise

- **The council reads a pre-read; the meeting decides.** If the pre-read is not landed 48–72 hours ahead, decisions do not land.
- **Standing agenda + delta = the pre-read.** Same shape each cycle; only the content changes.
- **Deck + one-pager, together.** The one-pager is what the member with ten minutes reads. Both trace every claim to an artefact ID.
- **Decisions-needed slide is the meeting's spine.** Confirm the list with the chair before circulating.
- **Cadence is the discipline.** M − 14 to M + 5; slip a step and the whole cycle slips.
- **The analyst's job is roll-up, packaging, and cadence — not fresh authoring.** Content lives in the earlier-module artefacts; the analyst aggregates.

## Summary

The council pre-read is the analyst-tier tangible output for this artefact family. It is a two-piece package — a deck ordered to the standing agenda and a single one-pager — assembled from artefacts the earlier modules produced, circulated 48 to 72 hours ahead of the meeting on a fixed monthly cadence, and structured around a *decisions needed this meeting* spine. Every claim traces to an artefact ID; sensitive items are named but briefed verbally; the analyst is the meeting's secretary and packet-owner, not its chair. Chapter 05 handles the other half of the meeting-packaging artefact: the minutes, the decision records, and the action items that make the pre-read's work stick.
