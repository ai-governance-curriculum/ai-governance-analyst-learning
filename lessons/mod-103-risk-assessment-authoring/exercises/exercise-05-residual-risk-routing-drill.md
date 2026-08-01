# Exercise 05 — Residual Risk Routing Drill

**Estimated effort:** 2 hours
**Grounding chapter:** [05 — Routing Risks, Residual Claims, and the Executive Framing](../05-routing-residuals-and-executive-framing.md)

## Objective

Take the scored register from exercise 03 and run it through a full routing round — draft the routing packets, run the negotiation for each entry against three characteristic owner-response shapes, capture the register updates, and produce the one-page executive framing. The output is the artefact chain a real analyst files at the end of a first-draft risk assessment: acknowledged register + audit-trail negotiation log + executive framing.

After this exercise you should be able to hold three lines under pressure — no aggregated single score, no legal-opinion language, no release-sign-off language — while still giving the executive a decision they can actually make.

## Prerequisites

- Exercise 03 completed. This exercise consumes your `mod-103-ex-03-scored-register.md`. If you have not done exercise 03, do it first.
- Chapter 05 (this module) read.
- The chapter 03 routing table (owners-by-risk-pattern) handy.
- Optional: chapter 06 of `mod-101` — the boundary-holding chapter — as a reminder of what "not a legal opinion" and "not a release sign-off" actually mean in analyst voice.

## Problem statement

You will drive a routing round for the register from exercise 03. The round has four parts.

### Part 1 — the routing packets

For each register entry, produce a routing packet with the minimum field list from chapter 05:

- Register ID and system link.
- Risk title + one-paragraph description.
- Three taxonomy anchors (NIST subcategory + GenAI Profile risk + ISO 23894 risk source).
- Inherent likelihood / magnitude with rationale.
- Proposed controls by category.
- Proposed residual with rationale.
- Control-defeated residual with rationale.
- The specific ask ("accept the residual as claimed" / "propose alternate controls" / "contest the routing" / "accept the risk with rationale" / "escalate").
- SLA (five business days for ack; two more weeks for substantive response is the default).
- Analyst contact.

Every entry ships one packet. The packets are the audit-facing evidence that the entry was formally routed.

### Part 2 — the negotiation round

For each register entry, simulate an owner response and record it. Distribute the responses across the three characteristic shapes from chapter 05 — at least one of each:

- **"You're too high — we have a control you haven't seen."** Owner cites a control the analyst did not know about. The analyst requests evidence, adds the control to the packet, and re-scores. Record the pre-and-post residual claim.
- **"You're too low — this thing scares us more than you realise."** Owner pushes for a tighter residual. The analyst records the owner's mechanism, and either updates the register or leaves the score and notes the disagreement. Record which.
- **"We disagree with the routing — this should belong to X team."** Owner argues the risk belongs to a different team. The analyst checks the routing table and either re-routes or holds. Record the decision and the reason.

Any remaining entries can receive a plain "accepted as proposed" or "accepted with monitoring commitment" — but at least one must land each of the three pushback shapes. If you cannot honestly imagine an owner pushing back on your register, either your entries are too soft (nothing to push back on) or you are role-playing owner responses as too compliant.

Record every negotiation as an entry in a `negotiation-log.md` with:

- Date.
- Register ID.
- Owner name and role (fabricate plausibly).
- Owner response (verbatim in analyst voice).
- Analyst reply.
- Register update (residual re-scored / control added / routing changed / no change).
- Outcome (accepted / accepted with conditions / escalated).

### Part 3 — the updated register

Reissue the register with the results of the negotiation round captured. Each entry now carries:

- Original proposed residual (marked as such — do not silently overwrite).
- Post-negotiation residual (the accepted score).
- Owner + acknowledgement date.
- Any conditions the owner attached (monitoring commitments, revalidation dates, escalation triggers).
- Status (`accepted` / `accepted-with-conditions` / `in-mitigation` / `escalated`).

### Part 4 — the executive framing

Produce a **one-page** executive framing that follows chapter 05's shape:

- The system in a sentence.
- The register profile — how many entries, at what post-negotiation residuals.
- The load-bearing controls (one or two) whose maintenance the profile depends on.
- The control-defeated exposure — the highest control-defeated case, called out explicitly.
- The re-review cadence — specific date and trigger.
- The ask — approve to proceed / approve conditional on X / request re-review / escalate.

The one-page limit is a hard limit. If it does not fit on one page, the register is not doing its job of carrying the detail.

## Requirements

- **Every register entry has a routing packet.** Any entry without a packet is a fail.
- **The negotiation round lands all three pushback shapes.** At least one control-you-missed, one appetite-tighter-than-yours, one wrong-team-routing.
- **The negotiation log is complete.** One entry per negotiation, with the six fields above. Absent negotiations (entries that just accepted as proposed) still appear as a one-line log entry.
- **The updated register preserves the original scores.** The audit trail requires that the analyst's *proposed* residual is visible alongside the *accepted* residual. Silent overwrites are a fail.
- **The executive framing is one page.** ≤500 words. Reports the profile, not a score. No single aggregated system rating. No legal-opinion language. No release-sign-off language.
- **Three do-nots respected.** No aggregated single score anywhere in the framing. No "compliant with X" language — use "assessment complete; findings closed" or equivalent. No "safe to release" or "cleared for launch" — use "acceptable-to-proceed pending evaluation-engineer sign-off" or equivalent.
- **The ask is specific.** "Approve to proceed under the acknowledged control set" is a specific ask. "Please review" is not.
- **No fabricated owners, meetings, or dates without acknowledgement.** If you are inventing an owner name, mark them as fabricated in a note at the bottom of the log — the fabrication is fine for the exercise, but the reviewer must know which parts are simulated.

## Starter guidance

- Do the packets first, in one sitting. They are largely mechanical; the value is in getting them uniform. Uniformity is what makes the negotiation round fast.
- For the negotiation round, do not over-play the pushback. Owners in a functioning enterprise mostly ack the proposal or push once — long-form disputes are rare and go to the governance council, not to the analyst's inbox. Keep the negotiations realistic.
- The "you're too high" pushback is the one that most improves the analyst's register — the owner is telling you about a control you did not know about. Treat it as free information.
- The "you're too low" pushback is the one that most improves the analyst's *judgment* — the owner is signalling an appetite the analyst has not calibrated to. Even if you leave the score, log the disagreement — the governance-council pattern is that these become known items.
- The "wrong-team" pushback is the one that most tests the analyst's routing-table discipline. If the pushback is defensible, re-route. If not, hold the routing and log the reason. Do not orphan the risk.
- For the executive framing, write the ask first and work backward. The ask forces you to be honest about whether the register actually supports the framing. If the ask reads as "please approve" but the register carries a control-defeated High × High case, rewrite the ask to reflect the boundary condition.
- The one-page limit is real. Cut. The register carries the detail; the executive framing carries the decision.

## Acceptance criteria

- A `mod-103-ex-05-routing-packets.md` (or a folder of one file per entry) with a routing packet for every register entry.
- A `mod-103-ex-05-negotiation-log.md` with a log entry per register entry, distributed across the three pushback shapes (at least one of each), with all six log fields per entry.
- A `mod-103-ex-05-updated-register.md` with proposed-vs-accepted residual columns, owner + ack date, conditions, status.
- A `mod-103-ex-05-executive-framing.md` of ≤500 words, on one page, following the six-part shape.
- Three do-nots respected: no aggregated single score, no legal-opinion language, no release-sign-off language.
- Any simulated owner names are flagged in the log.
- Every ordinal claim (proposed or accepted) carries a rationale. Every uncertain claim is marked `<!-- needs-research: -->`.

## Stretch goals

- **The governance-council slide.** Take the executive framing and rewrite it as a single slide (title + three bullets + the ask) for the governance council. This is preview work for `mod-110`.
- **The audit rehearsal.** Pick your most-negotiated register entry and imagine an auditor asking, three years later, *"why did you accept a Medium × Medium residual on this?"* Write the one-paragraph answer citing the negotiation log, the load-bearing control, the owner acknowledgement, and the monitoring commitment. This is preview work for `mod-107` and `mod-108`.
- **The re-assessment trigger note.** Chapter 05 mentions the re-review cadence. Extend it: author a short (~300 word) note listing the specific events (model version change, vendor change, new regulatory obligation, incident) that would force a re-assessment before the calendar cadence. This is preview work for `mod-109`.
- **The escalation memo.** If any of your entries escalated to the governance council in the negotiation round, write the escalation memo — one page, chair-of-council audience, with the specific disagreement, the analyst's frame, the owner's frame, and the decision the council is being asked to take.
- **The peer-review pass.** Swap deliverables with a peer (or an LLM playing a skeptical head of governance). Have them (a) find any aggregated-score language, legal-opinion language, or release-sign-off language you did not catch, and (b) push back on any residual whose rationale reads as thin. Log which of their findings you accepted.

## Deliverables

- `mod-103-ex-05-routing-packets.md` (or folder).
- `mod-103-ex-05-negotiation-log.md`.
- `mod-103-ex-05-updated-register.md`.
- `mod-103-ex-05-executive-framing.md`.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The solutions repo works the reference register (from exercise 03 on the CareTriage case) through a full routing round with three simulated pushbacks and a one-page executive framing. What is graded is (a) whether the audit trail is intact — proposed residual preserved alongside accepted residual, owner acknowledgement dated, conditions captured; (b) whether the three pushback shapes actually landed with real-sounding owner responses; (c) whether the executive framing respects the three do-nots; (d) whether the ask is specific and defensible. A framing that reads well but hides a control-defeated High × High case behind an aggregate-sounding sentence is worse than a rougher framing that surfaces the exposure honestly.
