# Delegation Boundary and Escalation Patterns

## Why this chapter

Chapters 01–08 walked what the analyst *does* on communication and council support. This chapter closes the module by walking what the analyst *does not do* in full — the delegation boundary — and by naming the four escalation classes that route work out of the analyst's desk when the analyst hits them. Every prior chapter previewed pieces of this map; this chapter is the consolidated version an analyst can pin to a desk and read once a quarter.

The pattern is the same as `mod-108` chapter 09 and `mod-109` chapter 09: the boundary is stated as a table, the escalation classes are stated with triggers and target roles, and the recurring-pattern rules — the ones that promote a repeated escalation from an individual escalation into a policy-work item — are stated explicitly.

## The full delegation-boundary statement

The table below is the union of the delegation rows from chapters 01, 02, 03, 04, 05, 06, 07, and 08 — with the additions this chapter contributes for cases the earlier chapters did not name.

### Translation and briefing (chapters 02 and 03)

| Artefact / action | Role that owns | Role that supports | The analyst *never* |
|---|---|---|---|
| Audience-adapted briefing to legal, privacy, security, product | `ai-governance-analyst` | Original artefact author; the receiving-audience role | Interprets the statute for legal; takes a lawful-basis position for privacy; specifies the mitigation for security; makes the launch-gate call in place of product |
| Board / governance-body briefing (ISO/IEC 38507 vocabulary) | `ai-governance-analyst` (drafts) | `senior-ai-governance-architect` (reviews), `legal` (reviews for external liability) | Delivers the briefing to the board; the delivery is by `head-of-ai-governance` or the named accountable executive |
| Executive-committee briefing | `ai-governance-analyst` (drafts) | `head-of-ai-governance` (delivers) | Delivers the briefing to the executive committee directly, or bypasses `head-of-ai-governance` in escalating to the executive |

### Council packaging (chapters 04 and 05)

| Artefact / action | Role that owns | Role that supports | The analyst *never* |
|---|---|---|---|
| Council standing agenda | Council chair (typically `head-of-ai-governance`) | `ai-governance-analyst` | Sets the agenda unilaterally |
| Council pre-read pack (deck + one-pager) | `ai-governance-analyst` | Content-owning contributors (risk owners, assessment owners) | Publishes without chair approval |
| Council chair and vote-management in-meeting | Council chair | `ai-governance-analyst` (as secretary) | Chairs the meeting or calls the vote |
| Council decisions | Council (voting members) | `ai-governance-analyst` (records) | Records a decision the council did not take |
| Council minutes | `ai-governance-analyst` | Council chair (approves for the record) | Edits ratified minutes silently; omits recorded dissent |
| Action-item register maintenance | `ai-governance-analyst` | Action-item owners | Closes an action item without evidence of completion |

### Policy and standard drafting (chapter 06)

| Artefact / action | Role that owns | Role that supports | The analyst *never* |
|---|---|---|---|
| First-cut policy / standard / guidance draft | `ai-governance-analyst` | Subject-matter contributors (privacy, security, legal, HR) | Publishes the draft outside the routing chain |
| Draft editing (post-first-cut) | `senior-ai-governance-architect` | `ai-governance-analyst` (incorporates edits) | Edits after the architect has taken editing ownership without the architect's request |
| Cross-functional consultation running | `senior-ai-governance-architect` | Named contributors from legal, privacy, security, HR, procurement, business lines | Runs the consultation on the architect's behalf without the architect's request |
| Ratification | `head-of-ai-governance` (or the enterprise's policy-approval workflow authority) | Both above | Ratifies |
| Policy exception approval (standard-level) | `senior-ai-governance-architect` | `ai-governance-analyst` (files the exception in the register) | Approves an exception |
| Policy exception approval (policy-level) | `head-of-ai-governance` | `ai-governance-analyst` (files the exception in the register) | Approves an exception |

### External communication (chapter 07)

| Artefact / action | Role that owns | Role that supports | The analyst *never* |
|---|---|---|---|
| Trust-site content | `communications` + `legal` | `ai-governance-analyst` (drafts / factual-reviews) | Publishes to the trust site |
| External model card publication | `senior-ai-governance-architect` (owns the published shape) | `ai-governance-analyst` (drafts from the internal card); `legal` (for high-risk) | Publishes an external card without architect approval; changes an internal card's scope to match the external one |
| Regulator response first draft | `ai-governance-analyst` | `legal`, `head-of-ai-governance`, subject-matter contributors | Signs or submits |
| Regulator submission | Accountable executive named for the regulator and jurisdiction | Everyone above | Signs or submits |
| Public-consultation response (factual content) | `ai-governance-analyst` (drafts factual content) | `government-affairs`, `legal`, `senior-ai-governance-architect`, `head-of-ai-governance` | Takes a position on the enterprise's behalf; signs |
| Press or media response | `communications` + `head-of-ai-governance` | `ai-governance-analyst` (factual-review only, on request) | Responds directly to a media inquiry |
| Public statement of record | Named accountable executive | Everyone above | Speaks of record |
| Whistleblower / worker complaint received externally | Enterprise whistleblower channel (legal-owned) + `head-of-ai-governance` | `ai-governance-analyst` (routes; contributes evidence on request) | Investigates independently; retains without routing |

### Certifications and professional development (chapter 08)

| Artefact / action | Role that owns | Role that supports | The analyst *never* |
|---|---|---|---|
| Analyst's own credential portfolio plan | `ai-governance-analyst` (with their manager) | `head-of-ai-governance` (approves training budget within enterprise-set limits) | Enrols in an out-of-plan credential using enterprise budget without manager approval |
| Peer-role credential-pursuit (CISSP, CISM, ML practitioner credentials) | Peer role | — | Competes on peer-role credentials as a substitute for the analyst's own portfolio |
| Enterprise ISO/IEC 42001 certification | `head-of-ai-governance` + `senior-ai-governance-architect` | `ai-governance-analyst` (operational contribution to the AIMS) | Represents the enterprise as the certification-project accountable executive |

### Cross-module rows (from `mod-101`–`mod-109`, restated where they intersect this module)

| Artefact / action | Owning module | The analyst's role in this module's context |
|---|---|---|
| Register-entry residual-risk acceptance | `mod-103` | Recorded in council minutes (chapter 05); briefed in the pre-read (chapter 04); packaged in the audience-adapted briefing (chapter 02) — but the acceptance decision belongs to the risk owner and, above the council-attention threshold, the council |
| Incident record composition | `mod-109` | Packaged in the incident-and-monitoring roll-up on the pre-read (chapter 04); the record itself is `mod-109` |
| Impact-assessment update on incident | `mod-109` chapter 04 + `mod-105` | Presented in the council pre-read; the update itself is the assessment owner's work |
| Control-status report roll-up on the pre-read | `mod-108` chapter 03 | Analyst summarises the report roll-up in the pre-read; the report itself is `mod-108` |
| Regulator-tracker headlines on the pre-read | `mod-106` | Analyst summarises; the tracker itself is `mod-106` |
| Serious-incident notification (EU AI Act Article 73) | `mod-109` chapter 07 | Reviewed at council as a decision item; drafting and submission are `mod-109`'s |

The union of these tables is what the analyst's role card actually looks like on the communication-and-council-support arc. The rows the analyst *owns* (the middle groups — drafting, packaging, recording, first-cut authoring) are the day-to-day. The rows above them (chairing, signing, ratifying, delivering, speaking of record) are the accountable roles the analyst hands to. The rows below them (peer credentials, peer roles' methodology) are the peers the analyst borrows vocabulary from without pursuing on the analyst's own name.

## The four escalation classes

Escalations from this module route in one of four ways. The classes match `mod-108` / `mod-109`'s four-class shape so an analyst who has learned the pattern once uses it everywhere.

### Class 1 — Content-owner delay or non-response

**Trigger.** A content owner (a risk owner, an assessment owner, a policy contributor, a control owner) has not delivered a pre-read contribution or a consultation input by the required date, and the analyst's follow-ups have not moved the item.

**Target role.** `senior-ai-governance-architect` (for policy-and-standard consultation delays) or `head-of-ai-governance` (for council-pre-read contribution delays).

**Escalation shape.** A brief note naming the item, the owner, the requested content, the requested date, the follow-ups the analyst has already made, and the impact on the downstream artefact (the pre-read will land without the item; the standard will consult without the contributor's sign-off).

**When the escalation triggers a policy-work item.** Repeated delays from the same content owner across multiple cycles are not an operational escalation; they are a role-clarity or resourcing question. After two consecutive cycles the analyst escalates as a class-4 (policy-work) item rather than a class-1 operational one.

### Class 2 — Chair or ratifier boundary-holding request

**Trigger.** The analyst is being pushed (usually by a well-meaning contributor, sometimes by a business-line owner) to publish a draft outside the routing chain, to record a decision the council did not take, to omit dissent from a minute, to bypass consultation, to short-circuit ratification, or to speak externally before legal review. The analyst declines and needs the chair's or the ratifier's backing to make the decline stick.

**Target role.** Council chair (typically `head-of-ai-governance`) or the applicable ratifier.

**Escalation shape.** A brief note naming the ask, the discipline the ask breaches, the analyst's decline, and the request for the chair's or the ratifier's confirmation of the boundary.

**When the escalation reveals a systemic issue.** If the ask pattern is recurring across multiple askers — the enterprise is not treating the routing chain as authoritative — the analyst raises the pattern to `head-of-ai-governance` as a policy-work item (class 4), often producing a *communication about the communication policy* to remind the enterprise of the routing chain.

### Class 3 — Regulator / external audit / material public exposure

**Trigger.** An external event has raised the stakes on an artefact currently in the analyst's queue — a regulator has opened an inquiry; an external audit has scoped an engagement; a public statement, media report, or third-party publication has raised material exposure. The artefact needs immediate senior-and-legal attention.

**Target roles.** `legal` and `head-of-ai-governance` simultaneously; `communications` where the exposure is public-facing.

**Escalation shape.** A brief with the external trigger, the affected artefact(s), the deadline (regulator responses have hard due dates; media cycles have soft ones), and the analyst's proposed next step (typically *pause current drafting, convene the review chain, re-plan the artefact under the new constraint*).

**Escalation must not go through the analyst first.** If the regulator or the external auditor reaches out directly to the analyst — a call, an email, a request-for-information — the analyst routes the contact to `legal` and `head-of-ai-governance` *before* responding substantively. The analyst does not become the regulator's or auditor's contact-of-record for the enterprise.

### Class 4 — Recurring pattern requires policy-work

**Trigger.** The analyst has seen the same class of problem across multiple meetings, multiple systems, or multiple content owners — and the fix is not another instance of the same operational action but a change to a policy, a standard, a training material, a tooling configuration, or a role-clarity statement.

**Target role.** `senior-ai-governance-architect` and `head-of-ai-governance`.

**Escalation shape.** A pattern-recognition memo: the recurring incidents, their common cause, the operational cost of continuing to handle them one-at-a-time, and the proposed policy-work item (a policy revision, a new standard section, a training update, a tooling configuration, a role-clarity statement) with the analyst's rough scope estimate. The class-4 escalation is where the analyst's *first-cut drafting* voice (chapter 06) meets the analyst's *council packaging* voice (chapter 04) — the memo may itself land as a standing-agenda item on the next council.

**Common class-4 patterns from this module.**

- Content owners repeatedly miss pre-read deadlines → policy work on the pre-read commitment.
- Content owners repeatedly deliver draft contributions in inconsistent shape → tooling / template work on the pre-read scaffolding.
- Council meetings repeatedly overrun because decisions are being made without pre-reads → policy work on the *no decisions without pre-read* discipline the chair enforces.
- External-facing drafting requests repeatedly come to the analyst without a review chain → policy work on the external-communication routing chain.
- Policy-exception requests recur for the same section → the section is misspecified in the policy and needs re-drafting rather than repeated exception-granting.
- Regulator responses recur on the same statute or article → sequencing the tracker row into the standing-agenda regulator-headlines section and a dedicated council touch-point.

## The recurring-pattern promotion rule

An operational escalation happens; a second one of the same class-and-shape happens; a third one is a pattern. The analyst does not wait for a fourth. The rule:

- **Second recurrence** — the analyst notes the pattern in the pre-read *for information*.
- **Third recurrence** — the analyst promotes the pattern to a class-4 escalation with a proposed policy-work item.
- **After promotion** — the pattern's individual instances continue to route as normal, but a running instance-count is maintained on the escalation register so the council can see whether the policy-work item is closing the pattern.

The promotion rule is what prevents the analyst from becoming a permanent operational hand-cranker of the same problem. If the analyst is doing the same operational escalation every month, the analyst has missed the promotion moment.

## Where the analyst's own role ends

Two final rows the boundary tables do not quite capture explicitly.

- **The analyst's own promotion.** Progression from `ai-governance-analyst` (level 15) toward the senior-architect track is a manager-and-analyst decision inside the enterprise's career-path structure. The analyst does not self-promote or unilaterally take architect-tier work; the promotion follows a formal path. The credentials the analyst pursues (chapter 08) support the promotion; they do not substitute for the manager's decision.
- **The analyst's own decision to leave the role.** Departure decisions are personal. When departure is planned, the analyst's transition responsibility is to leave the artefact set — the inventory, the register, the impact-assessment corpus, the tracker, the eval-evidence rows, the control-status report, the incident register, the monitoring-reading roll-up, the council pre-read and minutes archive, the policy and standard drafts in flight — in a shape the successor can pick up cold, per the disciplines the modules have walked. The three tangible outputs of this module (audience-adapted briefing, council packet, first-cut policy / standard draft) go in that hand-over.

## What to memorise

- **The delegation boundary is not a preference. It is a load-bearing part of the role's design.** Every audit engagement, every regulator inquiry, every incident post-mortem asks *who owned this?* The boundary answers the question.
- **The four escalation classes.** Class 1 = content-owner delay; Class 2 = boundary-holding request; Class 3 = regulator / external audit / public exposure; Class 4 = recurring pattern → policy-work.
- **The recurring-pattern promotion rule.** Second recurrence notes it; third promotes to class 4; instance-count on the register after promotion tracks whether the policy-work item closes the pattern.
- **Regulator, media, and whistleblower contacts do not become the analyst's private correspondence.** They route immediately to `legal`, `head-of-ai-governance`, or the enterprise's whistleblower channel.
- **The analyst does not chair the council, ratify a policy, sign a regulator submission, or speak of record.** The chair, the ratifier, the accountable executive, and communications hold those roles.
- **The analyst does not compete on peer-role credentials.** AIGP-plus-CIPP-or-42001; peer credentials belong to peer roles.

## Summary

This chapter closes the module by consolidating the delegation boundary walked across chapters 01–08 into a single table and stating the four escalation classes (content-owner delay; boundary-holding request; regulator / external audit / material public exposure; recurring pattern → policy-work) that route work out of the analyst's desk when the pattern demands. The recurring-pattern promotion rule (note on second recurrence, promote on third, instance-count after promotion) is what prevents the analyst from becoming a permanent operational hand-cranker of the same problem. The analyst is a translator, packager, recorder, and first-cut drafter; the analyst is not a decider, ratifier, signer, or speaker-of-record. The boundary is the role's load-bearing architecture, and this module — like `mod-108` and `mod-109` before it — closes on the same principle: the analyst's altitude is fixed and the hand-off directions are named.
