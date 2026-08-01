# The Analyst's Scope on Communication and Council Support

## Why this chapter

Nine modules have produced artefacts — the inventory row (`mod-102`), the risk register entry (`mod-103`), the fairness-review note (`mod-104`), the impact assessment (`mod-105`), the regulator-tracker row (`mod-106`), the eval-evidence row (`mod-107`), the control-status report and vendor-risk-register row (`mod-108`), and the incident record and monitoring-reading note (`mod-109`). Each is written in the vocabulary its module fixed: statute article numbers, standard clause references, metric names, threshold values, control identifiers, `INC-<year>-<sequence>` and its siblings.

The audiences that read those artefacts are not fluent in that vocabulary. Legal counsel reads for liability shape. The privacy office reads for lawful basis and data-subject rights exposure. Security reads for threat class and exploit path. Product reads for roadmap impact and launch-gate risk. The executive committee and the governance council read for portfolio-level decisions they can vote on inside a fifty-minute meeting. This module is the discipline that translates the artefact into the audience's language, walks the packet into the council-meeting pre-read, captures the council's decisions in minutes an internal auditor will still be able to reconstruct three years later, and — for the enterprise's internal-policy work — writes the first-cut draft that `senior-ai-governance-architect` edits and `head-of-ai-governance` ratifies.

The role's stance in this module: the analyst is a *translator, meeting-packet packager, minutes-and-decisions recorder, and first-cut drafter*. The analyst is not the council decision-maker, not the policy ratifier, not the enterprise spokesperson, and not the accountable executive who sits on the record for what the council or the regulator receives. Chapter 09 walks the boundary in full.

## What the analyst does on communication and council support

The analyst-tier verbs, in order:

1. **Translates** a technical eval, risk, audit, incident, or monitoring artefact into the language of the receiving audience — legal, privacy, security, product, executive, or council (chapter 02). For board-level audiences, the translation is bounded by ISO/IEC 38507's governance-body vocabulary (chapter 03).
2. **Assembles** the council pre-read pack — the standing-agenda slide, the portfolio-status one-pager, the decisions-needed slide, the escalation queue, the appended incident and PMS summaries — from the artefacts the earlier modules produced (chapter 04).
3. **Records** council minutes that survive an internal or external audit: decisions taken (yes / no / defer / conditional), the owner assigned per decision, dissent captured verbatim where offered, the action-item list with dates, and the retention path (chapter 05).
4. **Drafts** first-cut internal AI policies and standards — acceptable-use policy (AUP), model-approval standard, third-party AI vendor review standard, generative-AI employee guidance — for `senior-ai-governance-architect` to edit and `head-of-ai-governance` to route into ratification (chapter 06).
5. **Contributes to** external-facing responsible-AI communication — the enterprise trust site, model card publication, regulator-response first drafts — at analyst tier, under legal-review and executive-sign-off boundaries (chapter 07).
6. **Positions** the IAPP AIGP body of knowledge as the shared communication vocabulary the analyst uses across the five audiences; sequences CIPP/US or CIPP/E as the privacy-adjacent add-on and ISO/IEC 42001 lead-implementer / lead-auditor as a rising preferred credential for the analyst's own portfolio (chapter 08).

## What the analyst does not do

The analyst does not:

- **Decide what the council decides.** Council decisions belong to the council members. The analyst produces the pre-read and the minutes; the members vote and the accountable executive signs.
- **Ratify a policy or standard.** First-cut drafts are analyst work. Editing goes to `senior-ai-governance-architect`. Ratification goes to `head-of-ai-governance` or the enterprise's equivalent AI-accountable executive under the enterprise's policy-approval workflow.
- **Speak on behalf of the enterprise externally.** Public statements, media responses, and formal regulator submissions belong to `head-of-ai-governance`, `legal`, `communications`, and the accountable executive named for the specific jurisdiction. The analyst drafts; the executive signs.
- **Author the technical claim from scratch.** The analyst translates and packages the claim `ai-eval-engineer`, `ai-risk-engineer`, `ai-infra-security`, or the assessment's original owner produced. The analyst does not invent the metric, the threshold, or the mitigation.
- **Chair the council meeting.** The chair is named by the council's terms of reference — usually `head-of-ai-governance`, occasionally a rotating senior member. The analyst is the meeting's secretary and packet-owner, not its chair.
- **Take a legal position.** Any question that would require the analyst to interpret a statute, a regulation, a contract, or a case law citation as legal advice goes to `legal counsel`. The analyst summarises the tracker row (`mod-106`); the analyst does not opine on how the article applies to a specific system.

Chapter 09 walks the full boundary. The point at this stage: the analyst's altitude is one of packaging and translating and drafting — not one of deciding, ratifying, or speaking-of-record.

## The three tangible outputs

Everything in this module reduces to three artefact families:

1. **The audience-adapted briefing.** A written translation of an underlying technical artefact into the vocabulary and depth of a named audience. Shape varies by audience: a two-page memo for legal, a controls-mapping annex for privacy, an OWASP-anchored risk read for security, a launch-gate note for product, a one-page portfolio slide for the executive committee, a governance-body-vocabulary briefing (per ISO/IEC 38507) for the board. Chapter 02 fixes the shape per audience; chapter 03 fixes the board-level vocabulary constraint.
2. **The council packet.** A named-cadence deliverable for each governance council meeting — pre-read pack (deck + one-pager) circulated before the meeting, minutes circulated after, action-item register updated at meeting-close. Chapter 04 fixes the pre-read; chapter 05 fixes the minutes.
3. **The first-cut policy / standard draft.** A markdown or GRC-platform draft of an enterprise-internal AI policy or standard, versioned, with the routing chain (analyst → senior architect → head of governance → policy-approval workflow) captured on the document itself. Chapter 06 walks the four canonical drafts the analyst is expected to originate.

External-facing communication (chapter 07) and the certifications portfolio (chapter 08) are *disciplines* rather than tangible outputs — they modulate how the three artefact families above are written and by whom the analyst is understood.

## Where this module sits in the arc

- **Inputs.** Every artefact the analyst has authored in `mod-102`–`mod-109` — inventory, register, fairness note, impact assessment, tracker row, eval-evidence row, control-status report, vendor row, incident record, monitoring-reading note, PMS summary. Plus the enterprise's council terms of reference, the enterprise's policy-approval workflow, the enterprise's press-and-regulator-communication protocol, and the enterprise's public trust-site.
- **Outputs.** Audience-adapted briefings on demand; a council packet per meeting cycle (typically monthly for the AI governance council, quarterly for board-level updates); first-cut drafts of the AUP, model-approval standard, third-party AI vendor review standard, and generative-AI employee guidance; on-demand external-communication first drafts under legal and executive review.
- **Downstream consumers.** The council itself (pre-read and minutes); the enterprise's policy library (ratified policies land in the library after `head-of-ai-governance` ratification); the trust site, model card publication site, and regulator response record; the analyst's own promotion / role-progression story (the demonstrated ability to translate, draft, and package is what promotes an analyst into the senior-architect track).

## The vocabulary the analyst needs

- **Audience.** The named party the analyst is writing for. In this module the analyst writes for six audiences distinctively: legal, privacy, security, product, executive committee, and board / governance council. Chapter 02 fixes the per-audience translation rules; chapter 03 adds the ISO/IEC 38507 constraint on board-level language.
- **Translation.** The analyst-tier verb for restating a technical claim in an audience's language without changing the claim's substance. Translation is not summarisation (which loses information) and not rewriting (which changes claims). Chapter 02 walks the translation moves per audience.
- **Governance body.** In ISO/IEC 38507 language, the person or group of people accountable for the performance and conformance of the organisation. Boards, board committees (audit, risk, technology), and — for legal entities that do not have a board — the equivalent accountable body. Chapter 03 walks the vocabulary the standard uses to distinguish the governance body from the management team the body oversees.
- **Council pre-read.** The document set circulated to council members ahead of the meeting so members arrive prepared. Typically a slide deck plus a one-pager, with the appended incident, PMS, and escalation summaries. Chapter 04 fixes the shape.
- **Minutes.** The formal record of what the council discussed, decided, and assigned. Distinct from meeting notes (which are informal and personal) and from a transcript (which is a full verbatim record and usually is not what governance councils produce). Chapter 05 walks the shape and the audit-survival criteria.
- **Decision.** In this module, a discrete governance-body action of the form *approve / reject / defer / approve-with-conditions*, taken against a specific artefact (a policy, a standard, an escalation, a residual-risk acceptance, an incident-response plan, an external-communication draft) at a specific meeting on a specific date, with an owner named for the follow-through action. Chapter 05 fixes the decision-record fields.
- **Policy vs standard vs guidance.** *Policy* is a high-level enterprise statement of intent, ratified at the top of the policy hierarchy (typically by an executive or the board), and short. *Standard* is a specific normative requirement that operationalises a policy — usually mid-hierarchy, longer, and more testable. *Guidance* is non-normative recommendation for a named audience (employees using generative-AI tools, for example) that helps them act consistently with policy without imposing enforceable requirements. Chapter 06 walks all three with worked examples.
- **AIGP.** The IAPP's Artificial Intelligence Governance Professional certification. In this module, treated as the *shared communication vocabulary* the analyst uses across the five audiences — the AIGP body of knowledge is the common denominator most cross-functional AI-governance participants recognise. Chapter 08 walks the credential and its two most-common privacy-adjacent add-ons (CIPP/US, CIPP/E) plus the ISO/IEC 42001 lead-implementer / lead-auditor path.
- **Trust site.** The enterprise's externally-published page (or set of pages) that documents its AI governance posture — usually including model cards, policy summaries, an incident-disclosure statement, and (where regulated) a public copy of the applicable impact assessment or algorithmic-decision-tool notice. Chapter 07 walks the analyst-tier contribution shape.

## The delegation map — preview

Chapter 09 states this in full; here is the preview.

| Artefact / action | Role that owns | Role that supports |
|---|---|---|
| Audience-adapted briefing (legal, privacy, security, product) | `ai-governance-analyst` | Original artefact author (technical Q&A) |
| Executive-committee / board briefing (governance-body vocabulary) | `ai-governance-analyst` (drafts), `head-of-ai-governance` (delivers) | `senior-ai-governance-architect` (reviews); `legal` (reviews for external liability) |
| Council pre-read pack composition | `ai-governance-analyst` | `head-of-ai-governance` (chairs, sets agenda) |
| Council chair / agenda-setting | `head-of-ai-governance` (or the terms-of-reference-named chair) | `ai-governance-analyst` |
| Council minutes | `ai-governance-analyst` | Council chair (approves the minutes for record) |
| Council decision itself | Council (voting members) | `ai-governance-analyst` (records) |
| First-cut policy / standard draft | `ai-governance-analyst` | Subject-matter contributors (privacy, security, legal, HR) |
| Policy / standard edits | `senior-ai-governance-architect` | `ai-governance-analyst` (incorporates edits) |
| Policy / standard ratification | `head-of-ai-governance` (or enterprise policy-approval workflow authority) | Both above |
| Trust-site content | Enterprise `communications` + `legal` | `ai-governance-analyst` (drafts and factual review) |
| Model card publication (external) | `senior-ai-governance-architect` (owns the published shape) | `ai-governance-analyst` (drafts from internal card per `mod-105`) |
| Regulator response first draft | `ai-governance-analyst` | `legal` (edits), `head-of-ai-governance` (approves), accountable executive (signs) |
| Public statement / media response | `head-of-ai-governance` + `communications` | `ai-governance-analyst` (factual-review only) |

The middle rows — briefing, packet, minutes, first-cut drafts — are the analyst's day-to-day. The top and bottom rows are what the analyst hands off to.

## What to memorise

- **The analyst translates, packages, records, and drafts. The analyst does not decide, ratify, or speak-of-record.**
- **The three tangible outputs are the audience-adapted briefing, the council packet, and the first-cut policy / standard draft.**
- **Board-level briefings use ISO/IEC 38507's governance-body vocabulary.** Chapter 03 walks the standard.
- **Council minutes survive audit or they are not minutes.** Chapter 05 walks the survival criteria.
- **Policies are ratified by `head-of-ai-governance`, not by the analyst.** The analyst's draft is a first cut; the routing chain is analyst → senior architect → head of governance → policy-approval workflow.
- **AIGP is the shared vocabulary** — chapter 08 walks why the analyst pursues it early and what add-ons follow it.

## Summary

This module is the discipline that lets the artefacts the earlier modules produced actually be *acted on* — by legal, by privacy, by security, by product, by the executive committee, and by the board. The analyst is a translator (technical evidence → audience language), a meeting-packet packager (artefacts → council pre-read and minutes), a first-cut drafter (policy and standard drafts), and — under legal and executive review — a contributor to the enterprise's external-facing responsible-AI communication. The role stops at council decisions, policy ratification, and enterprise-of-record speech; the members, the accountable executives, and the communications function take it from there. Chapter 02 opens by fixing the audience-translation matrix the module's other artefacts assume.
