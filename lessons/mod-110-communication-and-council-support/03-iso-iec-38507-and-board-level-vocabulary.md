# ISO/IEC 38507 and Board-Level Governance-Body Vocabulary

## Why this chapter

Chapter 02 walked the five day-to-day audiences the analyst writes for. The sixth audience — the board, a board committee (audit, risk, technology, or the equivalent), or the enterprise's non-board equivalent accountable body — is different in kind. Boards do not read to *act*; boards read to *oversee*. A board reads the briefing to satisfy itself that management has the AI use of the organisation under control, that the risks are named and inside the enterprise's stated appetite, and that the direction management is heading is consistent with the strategy the board has endorsed. The board's decision is almost never *do this specific thing on this specific system*; it is *approve the policy / approve the risk-appetite statement / accept the assurance report / require management to come back with X*.

ISO/IEC 38507:2022 — *Information technology — Governance of IT — Governance implications of the use of artificial intelligence by organizations* — is the standard that fixes the vocabulary the analyst uses when writing for that audience. It is short (a few dozen pages), high-altitude, and specifically about the governance body's relationship to AI. It sits inside the broader ISO/IEC 38500 family (IT governance), reuses that family's *evaluate / direct / monitor* triad, and layers AI-specific considerations on top. Knowing it well enough to speak its vocabulary is the discriminating skill between an analyst who can hand a briefing to `head-of-ai-governance` for the board pack and an analyst who cannot.

The analyst does not deliver the briefing to the board — `head-of-ai-governance`, the accountable executive, or a named C-level does. The analyst drafts it. Getting the vocabulary right is what makes the draft usable without a full rewrite.

## What ISO/IEC 38507 is (and is not)

ISO/IEC 38507:2022 is a *guidance* standard, not a certifiable one. It does not have a *shall / should / may* clause structure the way an ISO management-system standard (like ISO/IEC 42001) does; it does not have an accompanying audit standard the way ISO/IEC 27001 has ISO/IEC 27006. It is written for the governance body and the executive management team who advise the governance body, and its central claim is that the governance body must be able to *evaluate, direct, and monitor* the organisation's use of AI just as it does for any other significant organisational capability.

It sits alongside — not inside — ISO/IEC 42001:2023 (the certifiable AI management system standard) and ISO/IEC 23894:2023 (AI risk management guidance). The analyst uses 42001 in the control-library work (`mod-108`), 23894 in the risk-authoring work (`mod-103`), and 38507 in the *board-facing briefing* work. All three share vocabulary, but 38507 is the one whose vocabulary the governance body itself is likely to recognise.

**What 38507 gives the analyst.**

- A distinction between the *governance body* (accountable for performance and conformance) and *management* (responsible for planning and executing). This is the distinction the board-level briefing must respect.
- A set of *considerations for the governance body* — governance-body actions grouped under *evaluate*, *direct*, and *monitor* — the analyst can use as the briefing's structural spine.
- A vocabulary of *AI-specific* governance concerns — autonomy of AI systems, opacity, use of data, cultural and behavioural change, dependence on third parties — that the analyst can lift verbatim into the briefing without introducing enterprise-specific jargon the board may not track.

**What 38507 does not give the analyst.**

- A management-system control set (that is `mod-108` and ISO/IEC 42001).
- A risk-scoring methodology (that is `mod-103` and ISO/IEC 23894 / NIST AI RMF).
- A conformity-assessment or certification path.
- Statute-specific mappings (those live in the tracker rows in `mod-106`).

The analyst does not cite 38507 as an obligation the enterprise has to comply with. The analyst cites 38507 as the *vocabulary source* for the board-facing briefing.

## The governance-body / management distinction

The single most-common failure in a board-facing draft is collapsing this distinction. Two examples of the failure:

- *"The AI governance council decided to update the acceptable-use policy this quarter."* — this reads the council's decision *as if* it were the board's decision. The council may report *to* the board, but the council is a management-tier body. A board-facing briefing distinguishes: *"Management (via the AI governance council) is updating the acceptable-use policy this quarter and will bring the revised policy to the board for ratification on [date]."*
- *"The enterprise operates 47 AI systems across three regulated jurisdictions."* — this is a management fact. A board-facing briefing frames it as an oversight fact: *"Management reports 47 AI systems operating across three regulated jurisdictions; the risk-appetite statement the board endorsed in Q2 currently accepts this scope, subject to the quarterly portfolio-status report management is required to bring."*

The vocabulary shift is small — *management reports*, *the risk-appetite statement the board endorsed*, *management is required to bring* — and it does the whole job. The board is being told what management is doing; the board is not being told what to do. That respects the accountability model 38507 assumes.

**A rule of thumb.** In the body of the board-facing briefing, every material claim should be attributable to either *the board* (past decisions, endorsed appetite, ratified policies) or *management* (current operations, ongoing work, upcoming asks). If the briefing has claims attributable to neither, the analyst has left ambiguity the board will read as *someone else made this decision without the board's knowledge* — which is exactly the failure mode 38507 exists to prevent.

## The *evaluate / direct / monitor* spine

ISO/IEC 38507 (inheriting from ISO/IEC 38500) organises the governance body's role around three verbs:

- **Evaluate** — the governance body assesses current and future use of AI, considering pressures acting on the organisation, and the organisation's ability to respond.
- **Direct** — the governance body assigns responsibility and directs the preparation and implementation of plans and policies. This is where the board *ratifies* an AI policy or *endorses* a risk-appetite statement.
- **Monitor** — the governance body monitors, via measurement systems, the performance of AI-related activities. This is where the board *receives* the portfolio-status pack, the assurance report, the incident summary.

A well-structured board-facing briefing walks the three verbs explicitly. A worked skeleton:

> **1. What management is asking the board to evaluate.** *One or two sentences naming the item — a new policy, a revised risk appetite, an expansion of scope into a new jurisdiction, an assurance report — and the specific evaluation the board is being asked to make.*
>
> **2. What management is asking the board to direct.** *Named actions the board would take if it approved — ratify the policy, endorse the appetite, require management to return with X. Written as options, not as recommendations, so the board can choose.*
>
> **3. What management is asking the board to monitor.** *The measurement cadence and content management is committing to — quarterly portfolio-status pack, monthly incident summary, on-trigger regulator-notification report. Named artefacts, named cadence, named owner.*
>
> **4. AI-specific considerations flagged for the board.** *Lifted from 38507's own vocabulary — autonomy, opacity, data use, cultural and behavioural change, third-party dependence — as they apply to the item in front of the board today.*
>
> **5. Prior-record cross-references.** *Prior board decisions (date and minute reference) this item builds on or amends. Prior council decisions (date and minute reference) that fed this item.*

The spine is repeatable across board packs — the board learns the shape and reads faster over time. The analyst does not restructure it meeting to meeting.

## The AI-specific considerations vocabulary

ISO/IEC 38507 names a set of AI-specific considerations the governance body should attend to. The exact set varies with the reader's edition of the standard, but the analyst's briefing should use the standard's language where it applies:

- **Autonomy.** The extent to which the AI system makes decisions without human intervention. In board vocabulary: *"the system makes a decision that reaches a customer without a human in the loop"* — usually the specific claim the board is being asked to endorse or push back on.
- **Opacity.** The extent to which the reasoning of the AI system is inspectable and explainable to affected parties, to auditors, and to the governance body itself. In board vocabulary: *"the system's outputs cannot be explained in the way a rule-based system's outputs can; management's assurance is based on evaluation evidence, not on inspection of the model's internals."*
- **Data use.** The extent and provenance of the data the AI system was trained on, is currently retrieved from, and is fine-tuned on. In board vocabulary: *"the model was trained on data with the following provenance; the retrieval index draws from the following sources; the model was fine-tuned on the following internal corpus."*
- **Cultural and behavioural change.** How the AI system changes the way people inside the organisation work — task shift, skill shift, delegation-of-judgement patterns, over-reliance risk. In board vocabulary: *"the deployment shifts the following tasks from human judgement to model output; management is monitoring the workforce impact via [named process]."*
- **Third-party dependence.** The extent to which the AI system depends on third-party foundation models, hosting providers, retrieval sources, or governance certifications outside the enterprise's direct control. In board vocabulary: *"the enterprise's assurance depends on Vendor X's model, Vendor Y's ISO/IEC 42001 certification, and Vendor Z's independent audit report; if Vendor X changes the model version, management's assurance for [affected systems] resets."*

These considerations are not risks per se; they are the axes along which risks arise. A board briefing that names them explicitly gives the board members a vocabulary to ask the right follow-up questions, which is the whole point of 38507.

## Board vs board committee vs council

Different meeting audiences within the enterprise are governed by different terms of reference. The analyst matches the vocabulary to the audience.

- **Full board.** Highest-altitude audience. Reads for strategy-level alignment, appetite endorsement, policy ratification. Terms of reference usually set by the enterprise's corporate governance policy. Meets less frequently. The briefing is short, uses full ISO/IEC 38507 vocabulary, and asks for a small number of well-scoped decisions.
- **Board committee (audit, risk, technology, ethics, or the enterprise's specific AI committee).** Mid-altitude audience. Reads at slightly higher technical depth than the full board and may go into methodology (control set, assurance framework, third-party audit posture). Vocabulary still governance-body-flavoured; may reference ISO/IEC 42001 or the enterprise's control library by clause where the committee is comfortable with it.
- **AI governance council (management-tier, sometimes called an AI ethics committee, an AI review board, or a responsible-AI council).** Not a governance-body audience under 38507. Reads at management-tier depth — chapter 04's territory. The council makes management-tier decisions and reports to the board or board committee.
- **Executive committee.** Also management-tier. Reads at portfolio-executive depth per chapter 02.

Confusing the four is a common failure. A briefing written for the AI governance council is almost never appropriate for the full board without a rewrite; the technical detail is too deep and the decision is at the wrong altitude. The analyst opens a briefing draft with the *named audience* at the top of the document so the audience-decision-vocabulary triad is fixed before the first sentence.

## Where 38507 sits vs 42001 vs 23894

For quick reference:

| Standard | What it is for | Vocabulary the analyst borrows for the board briefing |
|---|---|---|
| ISO/IEC 38507:2022 | Governance-body-facing guidance on AI governance implications | *governance body*, *evaluate / direct / monitor*, *autonomy / opacity / data use / cultural change / third-party dependence*, *risk appetite* |
| ISO/IEC 42001:2023 | Certifiable AI management system standard | *AI management system*, *AI policy*, *AI risk assessment*, *AI system impact assessment*, *management review*, *internal audit* — cited as evidence management is operating a certifiable system |
| ISO/IEC 23894:2023 | AI risk management guidance | *risk sources*, *risk analysis*, *risk evaluation*, *risk treatment* — used inside the risk-appetite-and-risk-portfolio parts of the board briefing |
| ISO/IEC 42005 | AI system impact assessment | Not usually cited by name in the board briefing; the impact assessment corpus (`mod-105`) is cited as an aggregate |

A board-facing briefing usually mentions all four indirectly. The analyst does not usually cite each by number in the body — that is footnote / annex work — but the vocabulary the body uses should be recognisable to someone who has read them.

## What a board-facing briefing looks like in practice

A worked one-page shape.

```
[Enterprise] — AI Governance — Board Briefing
Meeting: [YYYY-MM-DD] — Item: [numbered agenda entry] — Author: [analyst] — Approver: [head-of-ai-governance]

1. Ask
   The board is asked to [evaluate / direct / monitor] the following item:
   [one sentence].

2. Context
   [Two-to-four sentences of context in management-attributed language.
    Prior board actions cited by minute reference; prior council actions cited
    by minute reference. Any deltas from the last board pack named explicitly.]

3. AI-specific considerations (ISO/IEC 38507)
   - Autonomy: [one line]
   - Opacity: [one line]
   - Data use: [one line]
   - Cultural / behavioural change: [one line]
   - Third-party dependence: [one line]
   (Omit lines that do not apply; do not add lines outside the 38507 vocabulary.)

4. Options for board decision
   Option A — [name and one-sentence description]. Implications: [one line].
   Option B — [name and one-sentence description]. Implications: [one line].
   (Options C, D as needed; management's recommended option is marked
    explicitly and its rationale given in one line.)

5. What management will monitor and report back on
   Artefact: [named], cadence: [named], owner: [named], next arrival at
   the board: [YYYY-MM-DD].

Cross-references
   - Underlying artefacts: [IDs, e.g., IA-2026-0022, RISK-2026-0104]
   - Prior council decisions: [minute reference]
   - Prior board decisions: [minute reference]
```

The shape is boring on purpose. Board members read many such packets across many oversight domains; consistency is a feature.

## Common failure modes on board-facing drafts

- **Deep-in-the-weeds technical detail.** The board does not read for methodology. Metric tables, per-group breakdowns, and evidence-artefact excerpts go in the annex or the referenced underlying artefact, not the body.
- **Ambiguity about which body decided what.** *"It was decided that..."* — decided by whom? The board reads this as *someone made this decision on the enterprise's behalf and I do not know who they were accountable to*. Fix: attribute every claim to either the board or management, explicitly.
- **Recommendations disguised as decisions.** *"Management recommends that the board approve..."* is a legitimate framing. *"The board approves..."* — before the board has voted — is not. Draft options; the board decides.
- **Missing prior-record cross-references.** The board pack lands in front of members who have not seen the prior council minutes. If this item builds on a prior decision (theirs or management's), name the decision with its minute reference so members can find it. Uncited history disorients.
- **Enterprise jargon.** Internal system names (*Falcon-3, Prism-Retail-Copilot, THEIA-Signals*) without a one-line gloss. Board members do not track the enterprise's system-naming convention. Fix: gloss on first use.
- **Framework alphabet soup.** *"Per NIST AI RMF Measure 2.11 and ISO/IEC 42001 clause 9.1.2 the demonstration is..."* — the board does not read the framework citations; the analyst is proving they read the frameworks. Fix: put the citations in a footnote or an annex; write the body in plain governance-body language.
- **Answering a management question at the board altitude.** *"Should we upgrade to model version 4.1?"* is a management question; it does not belong on a board pack unless the upgrade materially changes the risk appetite or the strategy. Fix: escalate only the items that require oversight, not the items that require operational decisions.

## What the analyst does if the enterprise does not have a *board* per se

Not every enterprise the analyst works at has a formal board (private companies below certain thresholds, non-profits, subsidiaries, public-sector entities all vary). ISO/IEC 38507 uses *governing body* precisely so it can apply anywhere accountability sits at the top of the organisation. The analyst's job is to find the accountable body — an executive committee that also serves the accountability role, a partnership, a public-sector accounting-officer role, a trustee board — and adapt the briefing shape. The vocabulary discipline (governance-body-vs-management, evaluate / direct / monitor, AI-specific considerations) still applies.

## What to memorise

- **ISO/IEC 38507:2022 is the analyst's board-vocabulary anchor.** It is guidance, not certifiable, and not a source of compliance obligations — but it is the standard the governance body's advisers are likely to have read.
- **Governance body ≠ management.** Every material claim in a board-facing briefing is attributable to one or the other, explicitly.
- **Evaluate / direct / monitor is the spine.** Structure the ask around what the board is being asked to *evaluate*, *direct*, or *monitor*.
- **The AI-specific considerations vocabulary — autonomy, opacity, data use, cultural / behavioural change, third-party dependence — is lifted from the standard.** Use its words; do not paraphrase them into enterprise jargon.
- **The board's decision is at the appetite / policy / portfolio altitude, not the system-launch altitude.** System-launch decisions belong at the management-tier council or at product — chapter 04's audience.
- **The analyst drafts; `head-of-ai-governance` delivers.** The analyst does not present to the board directly unless explicitly invited.

## Summary

ISO/IEC 38507:2022 gives the analyst the vocabulary a board-facing briefing needs so the governance body can *evaluate, direct, and monitor* the enterprise's use of AI at its own altitude, without collapsing the governance-body-vs-management distinction and without drowning the board in framework citations or enterprise jargon. Every claim in the briefing is attributable to either the board or management. Every decision the briefing asks for is at the appetite / policy / portfolio altitude. The AI-specific considerations — autonomy, opacity, data use, cultural and behavioural change, third-party dependence — are named in the standard's own words. Chapter 04 opens the AI governance council (a management-tier audience) and the shape of the pre-read the council actually meets on.
