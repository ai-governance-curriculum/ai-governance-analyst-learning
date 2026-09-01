# Exercise 02 — Council Pre-Read and Minutes

**Estimated effort:** 2 hours
**Grounding chapters:** [01 — The Analyst's Scope on Communication and Council Support](../01-analyst-scope-on-communication-and-council-support.md), [04 — The Council Pre-Read: Deck, One-Pager, Standing Agenda](../04-council-pre-read-deck-and-one-pager.md), [05 — Council Minutes That Survive Audit](../05-council-minutes-that-survive-audit.md), [09 — Delegation Boundary and Escalation Patterns](../09-delegation-boundary-and-escalation-patterns.md).

## Objective

Compose one complete meeting cycle's worth of council-packaging artefacts — the pre-read one-pager, the decisions-needed slide (as a Markdown table), and the ratified minutes with the action-item register. The drill is anchored on a single AI governance council meeting composed from artefacts you have carried through the earlier modules (or their placeholders) so that the pre-read is *derivable* from the underlying artefacts, per chapter 04's *the analyst's per-cycle work is the roll-up, not fresh authoring* rule.

The drill's point is that the pre-read, the decisions-needed slide, and the minutes are three tightly-coupled artefacts. Every decision-needed on the slide traces back to an agenda item on the pre-read and forward to a decision-record entry on the minutes. Every action-item on the minutes has an owner and a due date and traces back to a decision. If any of the three artefacts drift from the other two, the cycle fails. The exercise is a check that the analyst can hold all three artefacts in the required alignment through one meeting cycle.

After this exercise you should be able to run a single monthly council-meeting cycle end-to-end from a set of underlying-module artefacts: assemble the pre-read (deck + one-pager), confirm the decisions-needed list with the chair, take minutes live during the meeting in the standard shape, produce the ratified minutes and the action-item-register updates, and identify at least one class-4 recurring-pattern promotion candidate per chapter 09.

## Prerequisites

- Chapter 01 read; the three tangible outputs (audience-adapted briefing, council packet, first-cut policy / standard draft) and the analyst's role (translator, packager, recorder, first-cut drafter) fresh in memory.
- Chapter 04 read; the standing-agenda spine (12 items), the deck-plus-one-pager pack, the decisions-needed slide, the M − 14 to M + 5 cadence, the per-section-artefact-set mapping, and the sensitive-item pattern.
- Chapter 05 read; the minutes template, the five-field decision-record pattern (ID, artefact scope, decision text, vote outcome, conditions and dissent), the action-item register fields, and the audit-survival test.
- Chapter 09 read; the delegation-boundary rows for council packaging (analyst is secretary; chair sets agenda; chair approves minutes; council decides; analyst records but does not chair) and the four escalation classes (particularly class 1 — content-owner delay — and class 4 — recurring pattern → policy-work).
- Your worked artefacts from `mod-102` through `mod-109`, or the placeholder set from those modules. Specifically you need: the inventory row roll-up, the register with residuals above the council-attention threshold, the FRIA / DPIA / IA corpus with any pending sign-offs, the control-status report roll-up, the vendor-risk register roll-up, the incident register, the monitoring-reading note, the PMS-summary set, the escalation register, and the regulator-tracker roll-up.

## Problem statement

The deliverable is a **folder `mod-110-ex-02-council-cycle/`** containing five files:

- `00-source-artefacts-index.md` — the analyst's index of which underlying-module artefacts feed which pre-read section, and how the delta since the last meeting was computed. Chapter 04 was explicit that the per-cycle work is the roll-up and delta computation.
- `01-pre-read-one-pager.md` — the one-page written summary per chapter 04's shape.
- `02-decisions-needed-slide.md` — the decisions-needed slide as a Markdown table.
- `03-meeting-minutes.md` — the minutes for the meeting, in chapter 05's template.
- `04-action-item-register-updates.md` — the actions assigned this meeting, in the register row shape from chapter 05.

The council meeting is a monthly cadence for the enterprise's AI governance council. Set the meeting date to a plausible near-future date (e.g., three weeks from your drafting date) so the M − 14 to M + 5 cadence you cite in `00-` is coherent. Set the meeting attendees consistent with a realistic council (chair = `head-of-ai-governance`; members drawn from `legal`, `privacy` / DPO, `security` / CISO delegate, a business-line owner, a fairness / responsible-AI SME; secretary = the analyst).

### The meeting substance

The meeting must include, at minimum, the following substantive items so the minutes exercise the five-field decision-record pattern and the action-item register:

1. **A residual-risk acceptance decision above council-attention threshold.** Use `RISK-2026-0104` on MCDA-Benefits — the fairness-finding-driven re-score from exercise 01 (or an equivalent from your `mod-103` work). The council decides: endorse the re-scored acceptance, defer with conditions, or reject and require further mitigation. The decision-record should carry the five fields.
2. **A first-cut policy or standard for approval to route into architect edits.** Use a first-cut standard (a good candidate is a *generative-AI employee guidance* placeholder, or the *third-party AI vendor review standard* first cut) from your future exercise-03 work — or a placeholder if you have not drafted one yet. The council decides: approve for routing to `senior-ai-governance-architect`, return for named revisions, or defer pending additional input from named contributors.
3. **An impact-assessment sign-off pending.** Use `FRIA-2026-0044` re-open outcome (following exercise 01), or an equivalent from your `mod-105` work. The council decides: sign off, sign off with conditions, return for edits, or defer pending named artefact.
4. **A serious-incident review that requires council awareness.** Use an `INC-2026-<sequence>` from your `mod-109` work (e.g., a class-4 biased-outcome-escalation incident on MCDA-Benefits, or a class-2 jailbreak on a chat assistant). The council decides: note taken, require post-mortem re-review, escalate to board at the next quarterly touch-point, or require Article 73 draft review at the next meeting.
5. **A regulatory-tracker item requiring sequencing decision.** Use a new EU AI Act guidance publication (an implementing act, a Commission notice) from your `mod-106` work. The council decides: sequence into policy-work at cadence, escalate to a special session, or note-taken.
6. **An escalation-register item requiring council direction.** Use an `ESC-2026-<sequence>` from your `mod-108` / `mod-109` work — a cross-role finding that has been sitting on the escalation register and requires a governance-level decision.
7. **A member dissent recorded on at least one decision.** Chapter 05's dissent-capture discipline is exercised. Attribute by named role, verbatim or paraphrased with the member's permission.
8. **At least one recurring-pattern signal that the analyst promotes as a class-4 escalation** per chapter 09. The escalation goes on the pre-read one-pager for information and on the minutes as an action-item to compose the class-4 memo for the next council.

### The five files, in detail

#### 00-source-artefacts-index.md

- Chapter 04's per-section-to-artefact-set mapping, applied to your specific artefacts. For each of the 12 standing-agenda items in the pre-read, name the source artefacts that feed the item (by ID) and the delta since the last meeting (what changed, computed how, from what source-of-truth).
- A short *cadence log* naming the M − 14, M − 10, M − 7, M − 5, and M − 3 handoffs and who owns each. Chapter 04 was explicit that slippage on any of the pre-meeting dates lands the pack cold.
- A short *sensitivity-check log* listing any items that touch privilege, market-sensitivity, personnel, or in-flight regulator submission, and whether the item is going on the circulated pre-read or being handled per the sensitive-item verbal pattern.
- A short *content-owner acknowledgement log* — for each risk owner, assessment owner, or contributor whose input the pre-read depends on, the requested-by / due-by / received-by state per chapter 04's contributor-notification cadence.

#### 01-pre-read-one-pager.md

- Chapter 04's one-pager template, populated with your specific numbers, deltas, decisions-needed list, for-information items, and escalations pending.
- The one-pager is a *single page*. Chapter 04 was explicit that longer one-pagers are read by nobody. Enforce the length.
- All cross-references cite artefact IDs.
- No sensitive substance (per your `00-` sensitivity-check log); sensitive items are named but not detailed.

#### 02-decisions-needed-slide.md

- The Markdown-table shape from chapter 04: number (D1, D2, ...), decision requested, agenda item, recommending role, options.
- At least four decisions on the slide, corresponding to items 1 through 6 of the meeting substance above (items 1, 2, 3 are always decision-needed; items 4, 5, 6 may be for-information or may need a decision depending on how you framed them).
- Every decision has an option set (not a yes/no reduction) per chapter 04's *options — not approval-or-not* discipline.
- The recommending role is named for every decision — the risk owner for the residual, the analyst for the first-cut policy routing, the assessment owner for the FRIA sign-off, etc.

#### 03-meeting-minutes.md

- Chapter 05's template, populated with your specific attendees, decisions, dissent, and actions.
- Attendance and quorum stated explicitly.
- Prior-minutes approval line present.
- Every substantive minute entry cites its underlying artefact ID.
- Every decision has the five fields: decision ID, artefact scope, decision text (from the pre-read's option set), vote outcome, conditions and dissent.
- At least one dissent recorded, attributed by named role.
- At least one *approved with conditions* decision with numbered conditions, each with a named owner and a due date and an action-item ID.
- The *decisions taken this meeting* recap section is populated with every decision keyed to agenda item and artefact ID.
- The *actions assigned this meeting* section is populated with every action-item, each carrying `ACT-<year>-<sequence>` ID, description, owner, and due date.
- Language discipline per chapter 05 — third person, past tense, active voice; no personal-opinion language; no un-attributed dissent; no half-attribution.

#### 04-action-item-register-updates.md

- Chapter 05's action-item register row shape (Action ID, Source meeting, Source minute entry, Description, Owner, Due date, Status, Evidence of completion, Rationale for deferral, History).
- One row per action assigned in the meeting.
- Every row cites the minute-entry that created it and the underlying artefact ID(s) it operates on.
- Status set to *open* for every new row.
- Include at least one *carried-forward* row from a hypothetical prior meeting to exercise the register's cross-meeting-continuity discipline — one action-item that was assigned at a prior meeting, with a status update recorded at this meeting (e.g., *in-flight — pending contributor review*, or *complete — evidence [artefact ID]*).
- Include the class-4 recurring-pattern escalation as an action-item (compose the class-4 memo for the next council).

## Requirements

- **All five files filed in `mod-110-ex-02-council-cycle/`.**
- **The one-pager fits on one page.** A one-pager that runs beyond a page is a chapter-04 discipline failure.
- **Every substantive claim on the one-pager, on the decisions-needed slide, and in the minutes traces to an artefact ID.**
- **The decisions-needed slide is a subset of the decisions taken in the minutes.** No decision appears in the minutes that was not on the slide (chapter 04 was explicit that surprise decisions belong on the *for information* list, escalated to the *decisions* list at the *next* meeting). If your meeting invents a decision the pre-read did not surface, name it in the minutes as *unplanned decision surfaced during meeting, added to next-meeting agenda for formal decision-record* — do not silently promote it.
- **Every decision in the minutes has all five fields.** Decision ID, artefact scope, decision text, vote outcome, conditions and dissent. Missing any of the five is a chapter-05 audit-survival failure.
- **At least one *approved with conditions* decision with numbered conditions, each with an owner and a due date and an action-item ID.**
- **At least one dissent recorded, attributed by named role, verbatim or paraphrased.** Un-attributed dissent (*"there was some concern"*) is a chapter-05 failure mode.
- **Every action-item has a named owner (role, or role plus named delegate) and a due date.** *"Legal to review"* without a delegate or a date is a chapter-05 failure.
- **The class-4 recurring-pattern escalation is identified in the one-pager (for information) and captured as an action-item (compose the memo for the next council).** Chapter 09's promotion rule applies: second recurrence notes; third promotes.
- **The sensitive-item pattern is exercised.** At least one candidate sensitive item is noted in the `00-` sensitivity-check log with the disposition (on-circulated-pre-read / verbal-only / sealed-record-reference).
- **Prior-minutes approval line is present** in the minutes; if this is a hypothetical first meeting for the exercise, note that explicitly.
- **Quorum is stated explicitly** (met / not-met per your enterprise's terms of reference).
- **No decision recorded that the council did not take.** Chapter 09's boundary: the analyst records; the council decides.
- **The analyst is named as *Secretary* in the minutes and pre-read header, not as *Chair*.** Chair is `head-of-ai-governance` or the enterprise's terms-of-reference-named chair (chapter 09 boundary).

## Starter guidance

- Draft `00-source-artefacts-index.md` first. It is the accounting exercise that makes the rest of the pack coherent. Chapter 04's per-section-to-artefact-set mapping is the scaffold; each row is *pre-read section → source-of-truth artefact(s) → delta computation → source-of-truth link*.
- Draft `01-pre-read-one-pager.md` next. It is the deliverable the council actually reads before the meeting; getting it right shapes the whole pack. Use chapter 04's one-pager template verbatim.
- Draft `02-decisions-needed-slide.md` after the one-pager. The decisions-needed list is the sibling of the *actions assigned this meeting* section of the minutes; the slide is what the chair walks the council through at close-of-business.
- Draft `03-meeting-minutes.md` after the pre-read and the decisions-needed slide. The minutes ratify (or amend) the decisions on the slide. Use chapter 05's template verbatim. Write the minutes as if you were live in the meeting — chapter 05 was explicit that post-meeting rewriting loses decisions the note-taker did not recognise at the time.
- Draft `04-action-item-register-updates.md` last. It captures the actions assigned this meeting plus the carried-forward status of at least one prior action. Use chapter 05's register field shape.
- For the dissent, pick a plausible member to dissent on a plausible decision. A common pattern: the DPO dissents on a residual-risk acceptance where the fairness finding has data-protection implications the DPO believes are under-weighted; or the legal delegate dissents on a first-cut policy that the delegate believes needs more consultation. Attribute the dissent by named role and either verbatim or paraphrased with the member's permission-in-record.
- For the *approved with conditions* decision, pick the FRIA sign-off (item 3) or the residual acceptance (item 1). Conditions should be numbered (Condition 1: [X, owner Y, due Z]; Condition 2: [X, owner Y, due Z]) with the action-item register carrying the follow-through.
- For the class-4 recurring-pattern promotion, pick a pattern the underlying artefacts plausibly show. Candidates chapter 09 named: content owners repeatedly miss pre-read deadlines → policy work on the pre-read commitment; council meetings repeatedly overrun because decisions are being made without pre-reads → *no decisions without pre-read* discipline; policy-exception requests recur for the same section → the section is misspecified. The class-4 memo is not part of the deliverable (it belongs at the next council); the action-item to compose it is.
- The sensitive-item pattern: a plausible candidate for this exercise is item 4 (the serious-incident review) or item 5 (the regulatory-tracker item) if either touches an in-flight legal-privileged matter, a personnel matter, or an in-flight regulator submission. Name the item on the pre-read in the sensitive-item shape (*"Item [n]: sensitive matter, briefed verbally by [role]"*) rather than detail it.
- Chapter 04's cadence discipline is real. The M − 14 to M + 5 cadence in `00-source-artefacts-index.md` should be a realistic set of dates keyed to your meeting date, not aspirational placeholders.
- Chapter 05's language discipline is exacting. Third person, past tense, active voice, named attribution. *"The council endorsed the residual acceptance"* — not *"we endorsed"* and not *"it was endorsed."* Verbatim quotation is for dissent-on-record and specific-conditions text only.
- Use `TBD-<name>` and `TBD-<date>` where a specific piece of the drill needs a name or date you do not have — but do not leave every field TBD. The exercise is a check that you can compose the pack coherently; the specific names and dates should be plausible and consistent across the five files.

## Acceptance criteria

- Five files filed in `mod-110-ex-02-council-cycle/`: `00-source-artefacts-index.md`, `01-pre-read-one-pager.md`, `02-decisions-needed-slide.md`, `03-meeting-minutes.md`, `04-action-item-register-updates.md`.
- The source-artefacts index maps every pre-read section to its underlying-module artefact(s) with the delta computation.
- The pre-read one-pager fits on one page, uses chapter 04's template, cites artefact IDs, names the meeting date and chair and secretary.
- The decisions-needed slide is a table with at least four decisions, each with an option set (not yes/no), a recommending role, and an agenda-item pointer.
- The minutes are written in chapter 05's template with attendance, quorum, prior-minutes approval, agenda items 1 through 12 as applicable, decisions taken (five fields per decision), at least one *approved with conditions* decision with numbered conditions and action-item IDs, at least one dissent recorded with named attribution, actions assigned recap with `ACT-` IDs and due dates.
- The action-item register updates are in the field shape from chapter 05 with at least one carried-forward row from a prior meeting and one row for the class-4 recurring-pattern memo composition.
- The class-4 recurring-pattern signal is identified on the one-pager (for information) and captured as an action-item (compose the memo).
- The sensitive-item pattern is exercised in the `00-` log with disposition.
- The analyst is Secretary in all headers, not Chair.
- No decision recorded that the council did not take.
- No un-attributed dissent, no actions without owners or dates, no silent conditions.
- Cadence dates on `00-` are realistic and keyed to the meeting date.

## Stretch goals

- **The full deck.** Draft a 15-slide `05-deck.md` file (Markdown as slide content) following chapter 04's *one slide per agenda item* rule, with speaker notes carrying the analyst-authored talking points. The deck is what the chair walks the council through in the meeting; the one-pager is the pre-read. Both are the analyst's tangible outputs.
- **The retention-and-versioning appendix.** Draft a `06-retention-and-access.md` file per chapter 05 covering the enterprise's records-retention position on the minutes (typically at least 10 years for high-risk-adjacent AI governance minutes under EU AI Act post-market documentation retention — chapter 05 flagged this as `<!-- needs-research: -->`; carry the note through) and the access control (council + chair + internal-audit on request + external-audit and regulators under disclosure protocol). Cite the enterprise records-retention policy by ID (or `TBD-<policy-name>` if not available).
- **The corrections log for a hypothetical prior-minutes error.** Draft a `07-corrections-log.md` file with an example prior-minutes-correction under the enterprise's records-correction process (chair-signed correction appendix; never silent edit-in-place per chapter 05). The corrections log demonstrates the *frozen after ratification* discipline.
- **The decision log.** Draft an `08-decision-log.md` file — the union of decision-record fields across all decisions taken in this meeting plus at least three plausible decisions from prior meetings, in the *answer "has the council ever decided X?" in one query* shape chapter 05 named. This is the artefact the auditor most often asks for.
- **The class-4 memo.** Draft the memo the analyst composes to promote the recurring pattern per chapter 09 — a `09-class-4-memo.md` file naming the pattern, the recurring incidents, the common cause, the operational cost of continuing to handle them one-at-a-time, and the proposed policy-work item with rough scope. Chapter 09 was explicit that this memo may itself land as a standing-agenda item at the next council.

## Deliverables

- `mod-110-ex-02-council-cycle/` folder containing:
  - `00-source-artefacts-index.md`
  - `01-pre-read-one-pager.md`
  - `02-decisions-needed-slide.md`
  - `03-meeting-minutes.md`
  - `04-action-item-register-updates.md`
- Optional stretch files (`05-` through `09-`) named clearly.

## Notes on evaluation

The paired solutions repo works one reference pack. The load-bearing calls your draft is expected to match: (a) the pre-read fits on one page and every claim traces to an artefact ID; (b) the decisions-needed slide is a subset of the decisions-taken in the minutes; (c) every decision in the minutes has all five fields (ID, artefact scope, decision text, vote outcome, conditions and dissent); (d) at least one dissent recorded with named attribution; (e) at least one *approved with conditions* decision with numbered conditions and action-item IDs; (f) every action-item has a named owner and a due date; (g) the class-4 recurring-pattern signal is identified and captured; (h) the sensitive-item pattern is exercised; (i) the analyst is Secretary, not Chair. The narrower calls — the specific decisions taken, the specific conditions attached, the specific dissenting member, the specific class-4 pattern — will differ per your worked-artefacts base. What should not differ is the coupling between the three artefacts (one-pager, decisions-needed, minutes) and the audit-survival criteria on the minutes. A tight pack that gets the coupling right beats a longer pack whose one-pager and decisions-needed slide and minutes read as if they were composed by three different analysts.
