# Routing Risks, Residual Claims, and the Executive Framing

## Why this chapter

The register entries from chapters 02 and 03 exist. The next step is turning them into decisions — routing each entry to the correct owner, negotiating the residual claim, and producing a summary an executive audience can act on. This is where a lot of first-draft risk assessments quietly go wrong: the analyst hands off a register but never gets acknowledgement, or the residual claims are self-negotiated ("Medium seems right"), or the executive summary is either alarmist or reassuring in ways the register does not support.

At analyst tier the discipline is: **route with a proposed action, not a question**; **make residual claims that name the control they depend on**; **frame executive summaries around the profile of residuals, not a single score**.

## The routing packet

Every routed register entry ships as a *routing packet* — enough context for the owner to accept the entry without reading the full risk assessment.

Minimum routing packet:

- **Register ID and system link.**
- **Risk title** and **one-paragraph description.**
- **NIST subcategory + GenAI Profile risk + ISO 23894 risk source** — the three taxonomy anchors.
- **Inherent likelihood / magnitude** with rationale.
- **Proposed controls** by category (preventive / detective / corrective / transfer / accept).
- **Proposed residual** with rationale.
- **Control-defeated residual** with rationale.
- **What the analyst is asking the owner to do** — a specific ask: *accept the residual as claimed; propose alternate controls; contest the routing; accept the risk with rationale; escalate.*
- **SLA** — typically five business days for acknowledgement, further two weeks for the owner's substantive response.
- **Analyst contact** — you.

The point of the packet is to make the owner's response mechanical when the analyst has done the work well.

## The residual-claim negotiation

The proposed residual is the analyst's *starting position*. Owners will push back in three characteristic shapes.

**"You're too high — we have a control you haven't seen."** Response: request the control-evidence, add it to the packet, and re-score. Update the register. This is a good failure mode — you learn about a control.

**"You're too low — this thing scares us more than you realise."** Response: understand the owner's mental model, cite the specific mechanism, and either update the register (if the owner's frame is defensible) or leave it and note the disagreement (owner is signalling appetite tighter than the analyst's frame).

**"We disagree with the routing — this should belong to X team."** Response: check the routing table (chapter 03), check the enterprise's RACI, and if the owner's argument is defensible, re-route. Do not silently accept a routing challenge that lands nowhere — orphan risk items are a program-level failure.

Every negotiation outcome is recorded on the register entry. The register is the audit-facing evidence of who owned what, and when.

## Inherent, residual, control-defeated in the executive framing

The three-column residual carries into the executive framing. The analyst reports the profile, not a single score.

Executive-audience shape:

- **The register in a sentence.** *N entries against system X; M require ongoing controls; K depend on a specific human-in-the-loop process; residual profile is acceptable-to-run.*
- **The one or two entries that dominate the profile.** By highest residual magnitude or by highest control-defeated residual.
- **The control dependencies.** The residual profile is *conditional* on specific controls being in place. If a control lapses, this is what the residual becomes.
- **The proposed re-review cadence.** Not a monthly promise; a specific date and trigger.
- **What the analyst is asking the executive to do.** Approve to proceed; approve conditional on control-X; request a re-review; escalate.

The failure mode is a single aggregated risk score. Ordinal aggregation is arithmetically indefensible and hides the profile. Report the profile.

## What the executive should not see

- **The full register.** They will read one page, not twenty. The register lives in the governance record; the executive sees the summary.
- **Language that reads as a legal opinion.** "Compliant with GDPR Art. 35" is a legal claim; use "DPIA completed; findings closed" instead.
- **Language that reads as a release sign-off.** "Safe to release" is [ai-evaluation-engineer](https://github.com/ai-governance-curriculum/ai-evaluation-engineer-learning) scope; use "acceptable-to-proceed pending evaluation-engineer sign-off" instead.
- **Quantitative risk claims the analyst did not derive.** If the enterprise wants a monetised or probabilistic claim, that is [senior-ai-governance-architect](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) scope.

Holding these lines matters — it is the same boundary-holding discipline covered in `mod-101 chapter 06`.

## Concrete example — the MCDA routing round

The four MCDA register entries from chapters 02–03 route out:

- **RR-2026-0212 (Confabulation) — Marketing Ops (Priya Nair).** Packet ships Monday. Priya acknowledges Tuesday, accepts the residual, agrees the copywriter-review workflow is the load-bearing control, requests that the analyst schedule quarterly monitoring review. Analyst updates the register: accepted with quarterly monitoring commitment.
- **RR-2026-0213 (Homogenisation) — Marketing Ops.** Priya accepts, notes the per-brand template rollout addresses the residual. Register updated.
- **RR-2026-0214 (IP contamination) — Legal.** Legal contests routing partway ("this should also carry a Marketing Ops accept"). Analyst adds Marketing Ops as secondary owner. Legal confirms vendor terms cover training-data indemnification; register carries the residual with the citation.
- **RR-2026-0215 (Data leakage) — Privacy + Security.** Both acknowledge. Privacy team confirms the PII scanner covers customer-identifier patterns; Security team commits to a monthly audit-log review. Register updated.

By Friday the routing round is closed. The analyst now writes the executive framing.

### Executive framing — MCDA (one page)

**System.** Marketing Copy Draft Assistant (MCDA), v1.3.2. Internal, assistive, hosted foundation model.

**Register profile.** Four risks identified. Two Medium-Medium residuals (Confabulation, Data-leakage-in-prompts), two Low-Medium residuals (Homogenisation, IP contamination). All routed; all acknowledged.

**Control dependencies.** The residual profile depends on: (a) copywriter-review workflow catching factual errors before external release; (b) PII / confidentiality scanner catching leakage in prompts; (c) per-brand prompt templates maintained by Marketing Ops. Any of these lapsing changes the profile.

**Control-defeated exposure.** If the copywriter-review workflow lapses, Confabulation goes to Medium × High. This is the most-exposed control-defeated case.

**Next review.** Quarterly monitoring beginning 2027-Q1; full re-assessment on next material change or 2027-09-15 (annual), whichever is sooner.

**Ask.** Approve to proceed under the acknowledged control set. No escalation to the governance council needed at this cadence; regular quarterly monitoring will surface any drift.

That is a one-page executive framing derived cleanly from the register, with no single aggregated score and clear control-dependency framing.

## What analyst-tier routing is *not*

- **Not a negotiation shortcut.** If an owner refuses to accept an entry, the analyst does not lower the residual to make it more palatable. The disagreement gets recorded and escalated.
- **Not a hand-off.** The analyst owns the register through routing, negotiation, acknowledgement, and monitoring. Owners *accept* the risk; they do not take the register itself.
- **Not the executive decision.** The analyst frames; the executive decides. The register carries the decision.

## What to memorise

- The **routing packet field list** — enough for the owner to respond without reading the full assessment.
- The **three pushback shapes**: control-you-missed; appetite-tighter-than-yours; wrong-team-routing.
- The **executive framing shape** — one paragraph, the entries that dominate, the control dependencies, the control-defeated exposure, the review cadence, the ask.
- The **three do-nots**: aggregated single score; legal-opinion language; release-sign-off language.

## Summary

Routing turns register entries into acknowledged decisions with named owners. Every entry ships as a routing packet with a specific ask and an SLA; every owner response is captured on the register. Residual claims are negotiated, not self-declared, and the register surfaces the negotiation. The executive framing reports the profile — one paragraph, the load-bearing controls, the control-defeated exposure, the ask — not a single aggregated score. When the round is complete the register is the audit-facing artefact and the executive has a one-page answer to "is this system OK to run?"
