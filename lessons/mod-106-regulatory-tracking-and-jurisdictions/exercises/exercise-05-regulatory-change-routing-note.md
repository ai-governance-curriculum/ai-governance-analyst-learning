# Exercise 05 — Regulatory-Change Routing Note

**Estimated effort:** 2 hours
**Grounding chapter:** [10 — Filing the Regulatory-Change Note and Routing It to Affected System Owners](../10-regulatory-change-note-routing.md)

## Objective

Author two full regulatory-change notes end-to-end against realistic *the regulation moved* scenarios, plus a small ledger that shows how the notes sit in the enterprise's change-note log over time. The drill exercises every field of the change-note structure from chapter 10 — header, body, routing, counsel flag, next-step tracking date, footer status — and forces the analyst to work through the closure discipline that turns a tracker update into evidence in the impact-assessment corpus. The point is not to produce two beautifully-formatted memos; the point is to produce two notes that a system owner receiving them cold on a Monday morning could act on before lunch.

After this exercise you should be able to open a regulator's newly-published bulletin, update the affected tracker row, draft the change-note against the tracker update, route it to the specific system owners and copy the right counsel and specialist counterparts, set the next-step tracking date, and — two weeks later — close the loop by attaching the evidence artefact and setting the note's status to *Resolved*.

## Prerequisites

- Chapter 10 read; the change-note structure, the primary / secondary / tertiary routing pattern, the closure discipline, and the failure modes the discipline prevents fresh in memory.
- Chapters 02, 04, and 06 skimmed for the specific regulator artefacts the two scenarios reference.
- Chapter 07 skimmed for the counsel / privacy-officer flag pattern that the change-note's tertiary routing invokes.
- The exercise-01 seed tracker open — the change-notes reference the tracker rows you assigned there (`REG-2026-EU-*`, `REG-2026-US-CO-*`, `REG-2026-SEC-INS-*`).
- The MCDA (`INV-2026-0088`) and MCDA-Benefits (`INV-2026-0311` or your equivalent) inventory rows from `mod-105` chapter 03, and the associated canonical-document / register-entry / model-card identifier space from `mod-105` chapters 01–04 and `mod-104` chapter 05.
- The example change-note in chapter 10 (the `CN-2026-0044` MCDA-Benefits Article 27 phase-in note) open as a shape reference — your outputs match that structure.

## Problem statement

The deliverable is two Markdown files.

### Part 1 — the two change-notes

Author `mod-106-ex-05-change-notes.md`. The document contains two full change-notes, one per scenario below, each following the chapter 10 structure verbatim. Both notes reserve their own change-note identifier — `CN-2026-EX05-01` and `CN-2026-EX05-02`.

Between the two notes, insert a short (three-to-five-line) *comparison callout* that names the specific structural difference between the two — different affected-inventory-row sets, different specialist-routing shapes, different next-step tracking cadences, different closure evidence artefacts. The callout is the reader's key to seeing that the change-note structure absorbs a wide range of regulatory events while producing a consistent-shape artefact.

#### Scenario A — an AI Act Article 26 clarification with immediate deployer impact

Suppose it is **2026-09-15**. The European Commission has just published a Q&A document on the AI Office site clarifying that Article 26(6) human-oversight requirements for high-risk AI systems apply to any deployer regardless of the deployer's public / private status — that a public-sector deployer's caseworker workflow does not, on its own, satisfy the Article 26(6) requirement without documented human-oversight training and monitoring. The MCDA-Benefits deployment at `INV-2026-0088` is a public-body deployment of an Annex III point 5(a) high-risk system; the enterprise's operating assumption in the Q2 FRIA-view had been that the caseworker workflow was on its own sufficient evidence of Article 26(6) compliance.

The change-note updates the tracker row for the AI Act Article 26 obligations (from your exercise 01 seed) and routes an action list to the MCDA-Benefits system owner.

Populate every field of the chapter 10 structure. Specifically:

- **Header.** Change-note ID `CN-2026-EX05-01`; filing date 2026-09-15; filer (your analyst-role name); tracker row updated (cite the exercise-01 identifier for the Article 26 row); related regulator artefacts (the AI Office Q&A page — cite a URL of the form `https://digital-strategy.ec.europa.eu/en/policies/ai-office` and mark `<!-- needs-research: -->` on the specific Q&A page URL if you have not verified a live page for this drill).
- **What changed.** Two sentences, precise. The clarification narrows the *caseworker workflow is sufficient* assumption; documented training and monitoring evidence is now the enforcement expectation.
- **Why it matters here.** Two-to-three sentences on how the clarification affects the MCDA-Benefits deployment specifically. The FRIA-view CDX-2026-0198-FRIA-v2 (or your equivalent) cites the caseworker workflow as the human-oversight safeguard; the model-card MC-2026-0044 (or your equivalent) similarly references caseworker review.
- **Affected inventory rows.** `INV-2026-0088` (MCDA-Benefits). Optionally add the MCDA row (`INV-2026-0088` proper — if you decide the clarification also affects the non-benefits variant, explain briefly).
- **Affected impact-assessment artefacts.** The canonical document, FRIA view, DPIA view, register entries covering human oversight, and model card. Cite each by identifier.
- **Recommended action per owner.** Three concrete actions with target dates — (a) update the FRIA-view's human-oversight section to add training-and-monitoring evidence or to explicitly flag the evidence-gap, (b) coordinate with Benefits Casework Ops training to produce or retrieve the caseworker-training record and the monitoring cadence, (c) revisit the residual-risk column on the affected register entries in light of the clarified expectation.
- **Counsel / privacy-officer flag.** Route to General Counsel and DPO on the interpretation question — *is the current caseworker workflow, evidenced by [X], sufficient under the clarified Article 26(6) expectation, or does the enterprise need to close a specific evidence gap before the FRIA-view is refreshed to a pass state*.
- **Analyst next-step tracking date.** Two weeks — 2026-09-29.
- **Footer.** Status *Open (routed 2026-09-15; awaiting owner action)*; cross-reference to the tracker row and to any prior change-notes on the same row (from the seed tracker or from prior exercises — if none, state *no prior change-notes on this row*).

#### Scenario B — a new US state adopting the NAIC Model Bulletin, and the enterprise deploys the insurance claim-triage engine in that state

Suppose it is **2026-11-04**. The state of *Ohio* insurance department has issued Bulletin 2026-05 adopting the NAIC Model Bulletin on the Use of Artificial Intelligence Systems by Insurers, effective 1 February 2027 (illustrative; mark `<!-- needs-research: -->` on the specific bulletin number and effective date). The enterprise deploys the homeowners-insurance claim-triage engine `INV-2026-EX04-INS` from exercise 04 in Ohio; a small-commercial claim-triage variant at `INV-2026-EX05-INS-COM` (invent as needed) is also deployed in Ohio.

The change-note updates the sector-overlay row for the NAIC state-adoption map (from your exercise 04 tracker extension) and routes an action list to the insurance-compliance / chief-actuary specialist (the specialist role from exercise 04's routing notes) alongside the two inventory-row owners.

Populate every field of the chapter 10 structure. Specifically:

- **Header.** Change-note ID `CN-2026-EX05-02`; filing date 2026-11-04; filer; tracker row updated (the exercise-04 NAIC-state-adoption row); related regulator artefacts (Ohio insurance department bulletin page — mark URL `<!-- needs-research: -->` for the drill).
- **What changed.** Ohio insurance department has adopted the NAIC Model Bulletin, effective 1 February 2027. Note that this is the state-adoption row moving; the underlying NAIC Model Bulletin has not changed.
- **Why it matters here.** The two Ohio-deployed inventory rows now inherit AISP obligations under Ohio insurance regulator jurisdiction, in addition to the AISP obligations they already inherit in other adopting states. Chief-actuary and insurance-compliance teams will need to add Ohio to the AISP state-scope schedule.
- **Affected inventory rows.** `INV-2026-EX04-INS` and `INV-2026-EX05-INS-COM`. State the specific Ohio-deployment fact per row (approximate policy count is not required — the fact of Ohio deployment is).
- **Affected impact-assessment artefacts.** For each inventory row: the canonical document, sector view, model card, register entries touching AI governance, and — critically — the enterprise's AISP documentation (which is a specialist-owned artefact per exercise 04's boundaries; the change-note requests that the specialist add Ohio to the AISP scope rather than the analyst rewriting the AISP).
- **Recommended action per owner.** Three concrete actions with target dates — (a) chief actuary / insurance compliance to add Ohio to the AISP state-scope schedule by [target], (b) system owners to confirm that the sector-view section of each canonical document is annotated with Ohio inheritance by [target], (c) analyst to schedule a monthly re-check until AISP-Ohio-scope evidence is attached to the change-note.
- **Counsel / privacy-officer flag.** Route to insurance-compliance counsel on the interpretation of Ohio's specific bulletin language — Ohio may have adopted the Model Bulletin with modifications rather than verbatim (mark `<!-- needs-research: -->` since the actual Ohio bulletin is illustrative in the scenario); counsel confirms whether the enterprise's existing AISP posture already satisfies Ohio's specific formulation.
- **Analyst next-step tracking date.** Six weeks — 2026-12-16 — reflecting that the effective date is not until 1 February 2027 and the AISP-scope-add work is more coordination than acute.
- **Footer.** Status *Open (routed 2026-11-04; awaiting specialist and owner action)*; cross-reference to the NAIC-state-adoption row and to any prior change-notes on that row.

### Part 2 — the change-note ledger

Author `mod-106-ex-05-change-note-ledger.md` — the analyst's change-note log. Structure:

- **Header block.** Version, date, author, cross-reference to the tracker file, and a one-sentence note that the ledger is the enterprise's audit-log of regulatory-change response (chapter 10's *cumulatively form an audit-log* framing).
- **Ledger table.** Columns: change-note ID; filing date; tracker row updated; affected inventory rows; status (with dated status changes as they land); next-step tracking date; closure evidence artefact reference (populated when the note is resolved).
- **Two ledger rows** — one per change-note. Populate every column for both.
- **A dated closure simulation for scenario A.** As a demonstration of the closure discipline, add a *closure note* underneath the ledger for `CN-2026-EX05-01` that says (illustratively): *2026-09-27 — Benefits Casework Ops attached caseworker-training-record `TR-BENEFITS-CASE-2026-Q3` and monitoring-cadence memo `MEMO-OVR-2026-09` to the change-note; FRIA-view CDX-2026-0198-FRIA-v3 regenerated with the added evidence; register entries `RR-2026-0311` and `RR-2026-0313` re-scored; status updated to Resolved — evidence attached.* This is the analyst-side demonstration that the change-note discipline includes closing the loop, not just filing.
- **A pending-status simulation for scenario B.** Leave `CN-2026-EX05-02` at *Open (routed)* with the six-week tracking date reserved. Add a one-line note that on the next-step tracking date the analyst re-checks — if the AISP-scope-add work is in progress, status moves to *In progress*; if it has not started, the analyst escalates via the routing pattern from `mod-103` chapter 05.

## Requirements

- **Every change-note populates every field of the chapter 10 structure.** No skipping the *related regulator artefacts* field because the drill URL is illustrative; the field is populated with the URL the analyst would use in a real change-note and marked `<!-- needs-research: -->` where the specific artefact is illustrative for the drill.
- **The *what changed* and *why it matters here* fields are precise.** *A new rule dropped* is not *what changed*; *the Commission published a Q&A document on 2026-09-15 clarifying that Article 26(6) requires documented training and monitoring evidence beyond the workflow itself* is. Similarly for *why it matters here* — the affected inventory row is named and the specific impact is stated.
- **The *recommended action per owner* section is action-shaped, not open-ended.** Each action is a specific task with a target date and an owner role.
- **The *counsel / privacy-officer flag* is a specific question, not *please review*.** The question is the same shape as chapter 07's flagging pattern — analyst asks; counsel or specialist opines.
- **The next-step tracking date is calibrated.** Two weeks for an acute in-force clarification; six weeks for a phased-in state adoption with a February effective date. State the reasoning in a one-line note attached to the tracking date.
- **The ledger row for `CN-2026-EX05-01` shows a full closure cycle**, with an illustrative closure-note and updated status. The reader sees that the change-note lifecycle ends in a resolved state, not in an open ticket that grows stale.
- **The ledger row for `CN-2026-EX05-02` shows the *open with tracking* state**, so that the reader sees the discipline handles change-notes that take weeks-to-months to close.
- **No fabricated regulator actions or bulletin IDs presented as fact.** The scenarios are illustrative; the change-notes reference illustrative regulator artefacts and mark them `<!-- needs-research: -->` where a real-world citation would be verified. Fabricating a real-looking Federal Register citation or a real-looking AI Office guidance ID is not permitted even in a drill; use clearly-illustrative placeholders with the research marker.
- **No mass-distribution routing.** Chapter 10 is explicit: a change-note that goes to a large mailing list has spectators, not owners. Each change-note routes to the specific system owner(s), the specific governance / risk-register owner(s), and the specific counsel / specialist counterpart. Name the roles.
- **The comparison callout between the two notes is written last, not first.** It reads better as the *what did I learn by authoring both* observation than as the *what am I about to show you* preamble.

## Starter guidance

- Draft the two notes in the order given (A then B). Scenario A is closer to the chapter 10 exemplar and is the shorter of the two; scenario B extends the pattern to a specialist-plus-owner routing shape and is a more taxing draft.
- The most common first-draft failure on scenario A is to write the *recommended action per owner* as *revisit human-oversight evidence*. That is not an action; it is an aspiration. Convert to *(a) update FRIA-view section 3 to add caseworker-training record `TR-BENEFITS-CASE-2026-Q3` if the record exists, or (b) if the record does not exist, produce it in coordination with Benefits Casework Ops training lead, target date 2026-09-25.* Owner, specific artefact, specific date.
- The most common first-draft failure on scenario B is to route only to the two system owners and forget the insurance-compliance / chief-actuary specialist. The specialist is the primary actor here — the AISP is a specialist-owned artefact — and the two system owners are secondary. Get the routing hierarchy right on the first pass.
- Use identifier prefixes that will not collide with real artefacts. `CN-2026-EX05-01` and `CN-2026-EX05-02` are drill IDs; `INV-2026-EX05-INS-COM` is a drill inventory ID. The MCDA-Benefits row and the exercise-04 insurance row can carry their existing IDs (`INV-2026-0088`, `INV-2026-EX04-INS`) because those are already deliberately-illustrative.
- The ledger's closure simulation for scenario A is deliberately dated to fall inside the next-step tracking window (2026-09-27 sits before the 2026-09-29 tracking date). This demonstrates the closure discipline is *the analyst re-checks and finds evidence attached* rather than *the analyst re-checks and files an escalation*. Both outcomes are valid; the drill simulates the healthy path.
- The comparison callout is at its most useful when it names the shape differences that the drill reveals — acute vs phased regulator action, single-owner-plus-DPO vs specialist-plus-two-owners routing, in-scope-inventory-changes-in-two-weeks vs runway-through-February, and evidence artefact of a caseworker training record vs an AISP scope update. Keep it to three-to-five lines.

## Acceptance criteria

- `mod-106-ex-05-change-notes.md` with two full change-notes (`CN-2026-EX05-01` and `CN-2026-EX05-02`) matching the chapter 10 structure field-by-field, and a three-to-five-line comparison callout between them.
- Every change-note field is populated, with `<!-- needs-research: -->` markers on illustrative regulator artefact URLs and bulletin IDs.
- Every *recommended action per owner* entry is action-shaped (specific task, specific artefact, specific target date, named owner role).
- Every *counsel / privacy-officer flag* is a specific question routed to a named role.
- Every *analyst next-step tracking date* is calibrated with a one-line reasoning note.
- `mod-106-ex-05-change-note-ledger.md` with a header block, a two-row ledger table, a dated closure simulation for `CN-2026-EX05-01`, and a pending-status note for `CN-2026-EX05-02`.
- The ledger reflects the *cumulatively form an audit-log* framing from chapter 10; a reader can pick up the ledger and see the two notes' full lifecycles.
- No fabricated regulator actions presented as fact; illustrative artefacts are marked as such.
- No mass-distribution routing; every note routes to specific roles.

## Stretch goals

- **A third change-note for a rescinded voluntary code adherence.** Suppose the enterprise had voluntarily adopted a specific voluntary-code commitment (chapter 09) and has just decided — with governance-owner sign-off — to withdraw from the commitment. Draft `CN-2026-EX05-03` following the chapter 10 structure, with the *what changed* field describing the enterprise's decision, the *why it matters here* field naming the specific affected artefacts (the voluntary-code adherence citation in the impact-assessment corpus and in the public communications channel), and the routing block including governance owner, general counsel, and the communications team. This exercises the chapter 09 / chapter 10 interface.
- **A joint change-note per multi-jurisdictional refresh.** Where a single regulator event affects more than one jurisdictional row (a rare-but-real case — an EU Commission implementing regulation on medical AI can shift MDR / AI Act sector-overlay boundaries simultaneously), draft a change-note that updates two tracker rows in a single note and routes to the specialist and to counsel for both. Note the risk of readability loss when a change-note absorbs too many rows; chapter 10 caps the cluster size implicitly by requiring per-owner routing.
- **A change-note escalation memo.** Simulate that the six-week tracking date for `CN-2026-EX05-02` has passed with no specialist or owner action. Draft the escalation memo the analyst would file under the `mod-103` chapter 05 escalation pattern, name the specific escalation recipient (a role above the specialist and the two system owners), and describe the escalated ask (a re-scoped and re-owned change-note, or an explicit acceptance of stale evidence with sign-off by the escalation recipient).
- **A change-note metrics dashboard.** Extract two or three simple metrics from the ledger — open notes older than the tracking date, resolved notes with the evidence artefact attached vs resolved notes without, average time from filing to resolution by affected-owner cluster. Sketch (in narrative form; no code required) how these metrics would surface in the `mod-110` council briefing.
- **A cross-reference to the annual review.** Chapter 10 notes that the annual review (`mod-105` chapter 08's walk cadence) is the systemic backstop for drift the change-notes missed. Write a short (one-page) note on how your two change-notes' closure evidence would flow into the next annual review — what the annual-review reader looks for in the ledger to confirm the analyst's change-note discipline is healthy.

## Deliverables

- `mod-106-ex-05-change-notes.md` — the two change-notes with the comparison callout.
- `mod-106-ex-05-change-note-ledger.md` — the ledger with the closure simulation and the pending-status note.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference change-note per scenario against the MCDA-Benefits and insurance-claim-triage inventory rows. Yours will differ in the specific action wording, the specific target dates, and the specific closure evidence artefact identifiers. What should not differ is (a) every chapter 10 field is populated in both notes, (b) *recommended action per owner* is action-shaped with owner-role-and-date specificity, (c) the *counsel / privacy-officer flag* is a specific question, (d) the ledger reflects a full closure cycle on scenario A and a pending-with-tracking state on scenario B, and (e) illustrative regulator artefacts are marked with `<!-- needs-research: -->` rather than presented as verified fact. A short, disciplined change-note that a system owner can action in 20 minutes beats a memo that reads like a policy brief; the drill measures the former.
