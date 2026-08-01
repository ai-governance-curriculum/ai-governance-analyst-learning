# Coordinating the Impact-Assessment Update

## Why this chapter

The incident record's *governance follow-through* block (chapter 03) carries three named re-open fields: the impact assessment (IA), the fundamental-rights impact assessment (FRIA) under the EU AI Act Article 27, and the data-protection impact assessment (DPIA) under GDPR Article 35. The three assessments were authored during pre-deployment; they made claims about likely benefits, likely harms, the affected populations, the *measures* that reduce residual harm, and the residual risk the enterprise accepts. An incident is the moment those claims are tested against reality — and, sometimes, falsified.

The analyst *coordinates* the re-open. The analyst does not *draft* the update — the assessment's original owner does that, because the drafting requires the substantive fluency (fairness methodology on a FRIA, personal-data purpose analysis on a DPIA, benefit-and-harm framing on an IA) the analyst does not have at library-authoring depth. What the analyst owns is:

- deciding whether the incident materially crosses the assessment's re-open threshold (the *trigger* evaluation);
- convening the update round with the original owner and the accountable executive;
- driving the timeline to completion against the assessment's own re-review cadence and any regulatory deadlines;
- routing the completed update for sign-off and recording the outcome on the incident record and on the assessment corpus (`mod-105`).

This chapter fixes the trigger evaluation, the coordination protocol, the sign-off routing per assessment type, and the failure modes.

## The trigger evaluation

Not every incident triggers a re-open. The analyst evaluates the trigger at triage, records the decision on the incident record's *IA / FRIA / DPIA re-open status* field, and cites the rationale.

The evaluation asks four questions per assessment attached to the affected inventory row.

- **Q1. Did the incident falsify a claim the assessment relied on?** *Load-bearing claim* = a claim the assessment cited as evidence of adequate mitigation, adequate benefit-vs-harm balance, or acceptable residual risk. Examples: an IA that claimed the model's hallucination rate on the reference set was below 2% and the incident is a hallucination-driven-harm case that shows the rate is above 2%; a FRIA that claimed the model refuses to produce protected-class content and the jailbreak just falsified that; a DPIA that claimed the deployment does not process a specific personal-data category and the incident showed it does.
- **Q2. Did the incident affect a population the assessment did not enumerate?** *Un-enumerated population* = a group of affected persons or an affected system class that the assessment did not consider. Examples: an assessment that scoped affected persons to the enterprise's customer base and the incident affected a customer's downstream client; an assessment that scoped an internal-use tool and the incident showed external users accessed it via a bypass.
- **Q3. Did the incident introduce a harm class the assessment did not consider?** *Un-considered harm class* = a category of harm (fundamental right affected, financial loss shape, safety class, dignitary harm) the assessment did not enumerate. Examples: an IA that considered financial-loss and inconvenience but did not consider dignitary-harm and the biased-outcome escalation is a dignitary-harm case; a FRIA that considered non-discrimination and privacy but did not consider freedom of expression.
- **Q4. Did the incident render a *measure* section commitment inoperative?** *Inoperative measure* = a measure the assessment committed the enterprise to (a guardrail configuration, a human-review handoff, an audit cadence, a monitoring threshold) that the incident demonstrated was not operating as described. Examples: the assessment committed to *the model routes to human review when confidence drops below 0.6* and the incident shows the router was mis-configured and never routed; the assessment committed to *quarterly fairness re-audit* and the audit has not run for two quarters.

**A *yes* on any question triggers the re-open** of the assessment the question was evaluated against. The analyst records which questions triggered and against which assessment, per the record's *IA / FRIA / DPIA re-open status* field's rationale.

A *no* on all four questions is a legitimate outcome: the incident occurred within the envelope the assessment considered, and the enterprise's follow-through is technical containment plus register-entry residual review — no assessment update needed. The analyst records *not-triggered with rationale* citing the four-question walk.

## The coordination protocol

Once the re-open is triggered, the analyst runs the coordination protocol per assessment type.

### The convening ask

The analyst opens the update round by writing to the assessment's original owner (per the `mod-105` corpus entry's *owner* field) and copying the accountable executive named on the assessment. The ask carries:

- The incident record identifier and one-paragraph description in analyst voice.
- Which of Q1–Q4 triggered, with the specific claim / population / harm / measure named.
- The requested timeline (default: 15 working days for the update to complete, longer for FRIA / DPIA when the assessment's original round took longer than 15 days).
- The named sign-off routing (per §"Sign-off routing per assessment type").
- The confirmation ask: the original owner acknowledges the update round by a named date and either accepts the coordination or proposes an alternative timeline with rationale.

### The timeline discipline

The 15-working-day default is calibrated to two constraints. First, most register-entry and system-card downstream artefacts also update on incident and cannot land cleanly until the assessment update completes. Second, for high-risk EU AI Act systems the post-market surveillance record (chapter 07) has its own periodicity, and an in-flight assessment update should not leave the PMS record open past a reporting cycle. If the original owner proposes a longer timeline, the analyst records the extended target on the incident record's follow-through block, notes any downstream artefacts held pending, and — if the extension pushes past a regulatory deadline — escalates per chapter 09.

### The update session

The analyst does not chair the update session but does attend to record what changed. The record kept during the session includes:

- Which sections of the assessment were re-opened (typically the *affected populations*, the *harms considered*, the *measures*, and the *residual risk* sections; other sections are usually stable).
- The delta per section — additions, removals, re-worded claims.
- The evidence attached to each delta (the incident record cross-reference is one source; a fresh eval from `ai-eval-engineer`, a fresh fairness re-analysis, an updated privacy-impact analysis are additional sources depending on the assessment type).
- The residual-risk claim's new value (if changed) and rationale.

The analyst's session-record lives on the incident record, cross-referenced to the assessment corpus entry.

### The sign-off round

Chapter §"Sign-off routing per assessment type" walks the roles. The analyst tracks the round to completion, records the sign-off identifier on the assessment corpus entry, updates the incident record's *IA / FRIA / DPIA re-open status* to *update-completed*, and closes the follow-through line.

## Sign-off routing per assessment type

The three assessment types route differently.

### IA update

- **Original owner.** The IA's `mod-105` owner — typically the product owner in coordination with `ai-risk-engineer` and `ai-governance-analyst`. The update draft owner is unchanged.
- **Reviewers before sign-off.** `ai-risk-engineer` (residual-risk claim), `ai-evaluation-engineer` (any fresh eval cited), `head-of-ai-governance` (for High-tier systems).
- **Sign-off.** The IA's accountable executive per the corpus entry — commonly the product's accountable executive or the business-unit head, per enterprise policy.
- **Post-sign-off.** The updated IA replaces the incumbent version in the corpus; the incumbent is retained as a versioned prior. The system-card / model-card (if published) is checked for consistency and updated per `mod-105` chapter 05.

### FRIA update

- **Original owner.** The FRIA's `mod-105` owner — typically the impact-assessment lead with `legal` and, for public-sector deployers, the *fundamental rights authority* liaison. The EU AI Act Article 27 fixes the FRIA obligation for deployers of high-risk AI systems in specified categories; the update draft owner is unchanged from the original round.
- **Reviewers before sign-off.** `legal` (fundamental-rights framing), `ai-risk-engineer` (residual-risk claim), `head-of-ai-governance`, and — where the enterprise has established the practice — the enterprise's ethics or human-rights advisor.
- **Sign-off.** The accountable executive per Article 27, which the enterprise's EU AI Act compliance function will have designated at the FRIA's original round.
- **Post-sign-off.** The updated FRIA is filed in the corpus with the incumbent retained; the enterprise's regulator interaction (if any) updates the fundamental-rights authority per the enterprise's registration-and-notification policy. The PMS record (chapter 07) is updated to reflect the completed re-open.

### DPIA update

- **Original owner.** The DPIA's owner is the *data controller* per GDPR — typically the business-unit owner with the `data-protection-officer` (DPO) as consulted expert. The update draft is written by the same owner in consultation with the DPO.
- **Reviewers before sign-off.** The DPO, `legal`, `information-security` if the incident touched a security surface, `ai-risk-engineer` if a residual-risk claim on the register is affected.
- **Sign-off.** The controller's accountable executive; the DPO opines but does not sign the controller's decision (per GDPR's DPO role definition).
- **Post-sign-off.** The updated DPIA replaces the incumbent; if the update reveals a residual high risk that mitigation cannot reduce (GDPR Article 36), the enterprise's supervisory authority must be consulted before the processing can continue — that consultation is `legal` and `DPO` scope, and the analyst records the consultation identifier on the DPIA corpus entry.

The three routes share a shape (original owner drafts, reviewers review, accountable executive signs, corpus updates with versioned prior) and differ in which reviewer roles are load-bearing.

## When the incident forces a new assessment rather than an update

The re-open evaluation may return a *new-assessment-required* outcome rather than an *update* outcome. The distinction:

- **Update.** The assessment's scope is unchanged; specific claims, populations, harms, or measures within scope need revision. The corpus entry version increments.
- **New assessment.** The affected inventory row's use case, deployment context, or affected-population set has expanded outside the assessment's original scope, and re-scoping the incumbent assessment would exceed the assessment framework's re-open discipline. A new assessment is authored (per `mod-105`'s intake); the incumbent is closed with a cross-reference to the new one.

The unauthorised-model-use class (chapter 02 class 6) frequently forces the new-assessment path: the use case was never in scope. Biased-outcome escalations that reveal an affected population never considered may also force it. The analyst's judgement call here should be made in consultation with the assessment's original owner and `head-of-ai-governance`; the default when uncertain is *update* (lower ceremony), with the option to escalate to *new-assessment* if the update process demonstrates the scope is too different.

## Coordinating a stacked update

Some incidents trigger updates to two or three of the assessments simultaneously — a hallucination-driven-harm case in a healthcare context may trigger the IA (task-appropriate residual claim), the FRIA (fundamental right to health), and the DPIA (personal-data implications of the harm's downstream handling). Coordination gets denser but the protocol is the same, run in parallel.

Two operational rules for stacked updates:

- **Convene once.** The analyst opens the update round with a single note that lists all three assessments and all triggering Q1–Q4 findings, copies all three sets of reviewers, and proposes a single joint timeline. Separate notes fragment the coordination.
- **Sign off in the right order.** The DPIA update completes first when GDPR Article 36 consultation is a possibility, because the outcome affects whether the processing can continue at all. The FRIA completes next when Article 27 registration is affected. The IA completes last, because it reads the outputs of the other two into its *residual risk* section.

If the stacked timeline slips beyond the incident record's *contained* → *closed* window, the analyst records the slip on the incident record, opens the appropriate escalation register entry, and reports the delay to `head-of-ai-governance`.

## Recording the update outcome

The completed update carries a set of artefacts the analyst files on the incident record and on the assessment corpus.

- **Incident record.** The *IA / FRIA / DPIA re-open status* field flips to *update-completed* with the corpus entry's new version identifier, the sign-off identifier, and the sign-off date.
- **Assessment corpus.** The updated assessment replaces the incumbent; the incumbent is retained as versioned prior; the corpus entry's *last incident triggering an update* field records the `INC-<year>-<sequence>` identifier.
- **Register.** Any register entry whose residual claim was affected is re-scored per the `mod-103` cadence; the register entry's *last incident falsifying a claim* field records the `INC-<year>-<sequence>` identifier.
- **System-card / model-card.** If a system card or model card is published externally and any of its claims changed, the analyst opens a card-update request against `mod-105` chapter 05's owner; the card update completes on its own cadence (external cards may need legal review before republication).
- **PMS record (high-risk systems).** Chapter 07's PMS record is updated to reflect the completed re-open.

The analyst does not silently move on from a completed update without filing these four (or five) artefact updates. The audit trail depends on every downstream artefact reflecting the update.

## Common failure modes

- **The re-open trigger is evaluated as *no* by default.** The analyst files *not-triggered* on every record because the trigger evaluation is deferred. Fix: the four-question walk (Q1–Q4) is done at triage, with named findings.
- **The update never lands.** The re-open is triggered, the analyst files the convening ask, and the original owner never acknowledges. Fix: the 15-day default and the escalation-on-non-response rule from chapter 03.
- **The update lands but the corpus version is not incremented.** The original owner amends the assessment in place without a versioned prior. Fix: the corpus discipline requires versioning; the analyst catches this at the sign-off recording step.
- **The stacked update completes out of order.** The IA signs off before the DPIA, and the IA's residual-risk section references DPIA claims that then change. Fix: the sign-off order rule in §"Coordinating a stacked update".
- **The system-card / model-card is never updated.** The assessment update lands but the external card's claims still reflect the incumbent. Fix: the recording step includes the card-update request; the request may take longer than the update but must be opened at update-completion.
- **The DPIA update reveals a residual high risk without triggering Article 36 consultation.** The DPO reads the updated DPIA, flags residual high risk, and the *consultation-required* trigger is not filed with the supervisory authority. Fix: the DPO's opinion is recorded and — when it names *residual high risk that cannot be reduced by proposed measures* — the consultation is a legal / DPO obligation, not an analyst preference.

## What to memorise

- **The trigger evaluation is a four-question walk (Q1–Q4).** *Yes* on any one triggers the re-open. *No* on all four is *not-triggered with rationale*.
- **The analyst coordinates; the original owner drafts.** The assessment's substantive fluency lives with the original owner and the reviewer roles.
- **Sign-off routing differs by assessment type.** IA → business/product accountable executive; FRIA → Article 27 accountable executive; DPIA → controller's accountable executive with DPO consulted and Article 36 consultation on residual high risk.
- **Stacked updates convene once and sign off in DPIA → FRIA → IA order.**
- **The corpus versions.** Every completed update replaces the incumbent with a new version and retains the prior.
- **Recording the outcome touches five artefacts:** the incident record, the assessment corpus entry, the register entry, the system/model card (if published), and the PMS record for high-risk systems.

## Summary

The analyst coordinates the impact-assessment (IA), fundamental-rights impact-assessment (FRIA), and data-protection impact-assessment (DPIA) updates the incident triggers. The trigger evaluation is a four-question walk asking whether the incident falsified a load-bearing claim, affected an un-enumerated population, introduced an un-considered harm class, or rendered a *measure* commitment inoperative. The analyst does not draft the update — the assessment's original owner does — but drives the timeline, convenes the reviewer set, tracks the sign-off, and records the outcome across the incident record, the assessment corpus, the register, the system/model card, and (for high-risk EU AI Act systems) the PMS record. Sign-off routing differs by assessment type; stacked updates convene once and sign off in DPIA → FRIA → IA order. Chapter 05 turns to the continuous-monitoring dashboards the enterprise runs in the periods between incidents, which are frequently the surface on which the next incident is first observed.
