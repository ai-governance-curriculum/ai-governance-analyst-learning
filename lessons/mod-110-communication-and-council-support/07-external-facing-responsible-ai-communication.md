# External-Facing Responsible AI Communication

## Why this chapter

Nine of the ten modules in this track keep the analyst's writing *internal* — inventory rows, register entries, impact assessments, minutes, first-cut policies. This chapter is the small but consequential exception. Every enterprise with a materially sized AI program produces external-facing responsible-AI content: a trust site or responsible-AI page on the corporate website, model cards published for the AI systems the enterprise has decided to disclose, statements issued in response to regulator inquiries or incident disclosures, and — for organisations with a public-comment posture — occasional public responses to regulator consultations. Analyst-tier contribution to those artefacts exists, is real, and is a discriminating skill on the promotion path into the senior-architect track.

It is also the artefact class where the analyst's delegation boundary matters most. Every external artefact carries the enterprise's name; every mis-statement, over-claim, or premature disclosure is a legal, contractual, or regulator-facing exposure the enterprise cannot easily unwind. The analyst *drafts* and *factual-reviews*. The analyst does not sign, does not publish, does not speak-of-record, and does not decide unilaterally what leaves the enterprise. `legal`, `communications`, `head-of-ai-governance`, and — for named-executive statements — the accountable executive make those calls.

This chapter walks the four external-facing artefact families the analyst is expected to contribute to at analyst tier: the enterprise trust site, published model cards, regulator responses, and public consultation responses. It fixes the review-and-approval chain each moves through, the *do not* patterns, and the class of red flags that requires the analyst to stop and escalate.

## The four external-facing artefact families

### 1. Trust site content

**What it is.** The enterprise's externally-published page (or set of pages) that documents its AI governance posture. Common contents include: a responsible-AI or AI-principles statement, a summary of the enterprise's approach to AI risk management, a plain-language description of the enterprise's AI use, links to published model cards and privacy notices, a statement of applicable jurisdiction and applicable statutes, a contact channel for external inquiries or complaints, and — increasingly — a formal transparency statement complying with EU AI Act Article 50's transparency obligations where the enterprise deploys AI systems that interact with people, generate synthetic content, or perform emotion recognition or biometric categorisation.

**Where the analyst contributes.**

- *Drafts* the plain-language summary of the enterprise's AI governance posture, drawing on the artefacts the earlier modules produced (inventory scale, tiering distribution, control-set posture, incident-disclosure posture).
- *Factual-reviews* trust-site content authored by `communications` or by an external agency, catching claims that overstate the enterprise's posture, mis-state framework compliance, or drift from the underlying internal artefacts.
- *Maintains cross-references* to the underlying internal artefacts by ID (internally-visible; the external site cites categories, not IDs).
- *Flags updates* required when the underlying posture changes — a new jurisdiction, a new framework, a material portfolio change, a new statute in force.

**Where the analyst does not contribute.**

- *Design and copy.* Communications or an agency owns the visual and copy work.
- *Brand voice and marketing tone.* Not the analyst's ground.
- *Publication.* Comms owns the publication workflow.

**Common red flags in trust-site content the analyst catches.**

- *"Our AI is unbiased."* — an eval-and-artefact-unsupported claim; strike or replace with a factually-supportable statement about the enterprise's fairness-review discipline (`mod-104`).
- *"We comply with the EU AI Act."* — an over-broad claim; the EU AI Act has many articles, and *compliance* is per-article and per-system. Fix: name the specific obligations the enterprise addresses (Article 14 human oversight, Article 26 deployer obligations, Article 27 FRIA, Article 50 transparency) and the systems in scope.
- *"Our systems meet ISO/IEC 42001."* — a claim only supportable if the enterprise has an ISO/IEC 42001 *certification* from an accredited certification body (i.e. through an accredited conformity-assessment body). Alignment or implementation are different from certification; the analyst distinguishes.
- *"We do not use AI for consequential decisions."* — a claim easily falsified by an internal audit or a data-scientist's confessional interview. If untrue, strike; if true, cite the AUP prohibition (chapter 06) that makes it true.
- *Model claims that outstrip the underlying model card.* If the internal model card says the model was evaluated on X and Y under conditions Z, the external claim cannot expand to *"our model works on any content in any context"*.

### 2. Published model cards

**What it is.** The externally-published version of the internal model card `mod-105` produced. Not every internal model card is published externally — most are internal-only. When an enterprise elects to publish a model card (increasingly common for foundation-model providers, for enterprises with high public-transparency posture, and for high-risk deployments under emerging regulation), the external version is a distinct artefact from the internal one.

**Where the analyst contributes.**

- *Drafts the external version* from the internal model card, translating internal-only detail (specific system identifiers, internal team names, internal metric thresholds) into external-appropriate language (system category, published metric summary, external-appropriate scope-of-use description).
- *Reconciles the external version against the internal model card* — the external version cannot claim what the internal card does not support.
- *Feeds edit cycles* with `senior-ai-governance-architect` (who owns the published shape), `legal`, and `communications`.
- *Tracks publication cadence* — the external card is versioned alongside the internal one and re-published when the internal one changes materially.

**Standard references the analyst leans on.**

- The *model card* format originated with Mitchell et al. (2019) at Google — the framework the analyst usually cites when explaining what a model card is to a non-technical audience.
- The Hugging Face model-card standard is the most-adopted community version and is what most public-facing model cards on model-hosting platforms use.
- ISO/IEC 12792 (AI system transparency taxonomy of information elements) sits in the standards space around this artefact; where the enterprise's model card format includes 12792-aligned elements, the analyst names it explicitly. <!-- needs-research: confirm ISO/IEC 12792 (or a related transparency-standard document) status and publication as it moves through the ISO/IEC JTC 1/SC 42 pipeline; the analyst should cite the current published state at time of writing. -->

**Common red flags on the analyst's factual-review.**

- *External model card describes a use case the internal card excludes.* Fix: strike from the external card or re-scope the internal card (which is a `mod-105` question, not a `mod-110` question — route back).
- *External model card omits limitations the internal card names.* Fix: the analyst inserts the limitation. External model cards are worse than internal ones when they omit the limitations the internal one names — they read as marketing.
- *Metrics on the external card do not match the eval-evidence rows in `mod-107`.* Fix: reconcile before publication; the two must match by number, threshold, and evaluation date.

### 3. Regulator responses

**What it is.** The enterprise's formal, on-record response to an inquiry, request-for-information, notice, or investigation from a regulator with jurisdiction over the enterprise. Regulator responses may be routine (a scheduled reporting requirement, a periodic post-market surveillance summary — `mod-109` chapter 07 walked the Article 72 case) or non-routine (a specific inquiry, an incident-notification, a request for supplemental information following a filed notification).

**Where the analyst contributes.**

- *Drafts the first version* of the response, drawing on the artefacts the earlier modules produced (the underlying incident record, the impact assessment, the eval-evidence rows, the control-status report).
- *Fact-checks against the underlying artefacts* — a regulator response's factual claims must trace to the artefacts.
- *Tracks the response's deadline discipline* — regulator responses typically have hard due dates the analyst enforces on the internal review chain.

**Where the analyst does not contribute.**

- *Legal position taking.* Interpreting how the statute or article applies to the enterprise's facts is `legal`'s ground.
- *Signature and submission.* An accountable executive (or a specifically-named regulator-facing person, sometimes `head-of-ai-governance`, sometimes the enterprise's data-protection officer, sometimes the general counsel — varies by jurisdiction and by regulator) signs and submits.
- *Any communication with the regulator that is not through the reviewed-and-approved response.* No calls, no side-channel emails, no clarification-in-passing with the regulator's contact from the analyst desk. If the regulator's contact reaches out directly, the analyst routes them to `legal` and `head-of-ai-governance` before responding.

**Standard references the analyst leans on.**

- The applicable statute, article, and any regulator-issued guidance on the specific response type. `mod-106`'s tracker row for the obligation is the analyst's entry point.
- The regulator's own published response templates or forms, where they exist.
- Prior enterprise responses to the same regulator, if any — cited so the response is consistent with the enterprise's prior positions.

**Common red flags.**

- *Response makes claims the underlying artefacts do not support.* Fix: strike or route back to the underlying-artefact owner for a supplemental artefact.
- *Response takes a legal position without legal review.* Fix: never submit without a documented legal sign-off.
- *Response is drafted in a tone appropriate to internal communication but not to a regulator.* Fix: the tone is formal, third-person, factually-conservative, and legally-reviewed. `communications` and `legal` typically edit for tone before submission.
- *Response drifts past the deadline.* Fix: the analyst tracks the deadline explicitly and escalates at pre-agreed intervals if internal review is not converging.

### 4. Public consultation responses

**What it is.** Some enterprises take public-comment positions in response to regulator consultations — draft standards, draft rules, requests for information from bodies like the EU Commission's AI Office, NIST (during RMF or profile development), the UK ICO, state attorneys general, and standard-development bodies. These are voluntary in a way regulator responses are not — the enterprise chooses to comment or not.

**Where the analyst contributes.**

- *Drafts factual content* — the parts of the response describing the enterprise's own AI use, its interpretation of terms in the draft rule, and its experience with the practical operation of relevant standards.
- *Tracks the consultation calendar* — public-comment windows are typically finite; the analyst maintains a calendar and flags the internal decision *"do we comment?"* well before the deadline.
- *Coordinates cross-functional review* — legal, government-affairs, communications, senior-architect all contribute.

**Where the analyst does not contribute.**

- *Position-taking on the enterprise's behalf.* Positions belong to `head-of-ai-governance` and, for material positions, an executive. The analyst drafts factual content, not positions.

## The review-and-approval chain

Every external-facing artefact moves through a review-and-approval chain the analyst maps explicitly. A minimal shape:

| Artefact | Analyst's role | Required reviewers | Signer / publisher |
|---|---|---|---|
| Trust-site update | Drafts / factual-reviews | `senior-ai-governance-architect`, `legal`, `communications`, `head-of-ai-governance` | Publisher: `communications` |
| External model card | Drafts / factual-reviews | Internal model card owner (`mod-105`), `senior-ai-governance-architect`, `legal` (for high-risk deployments), `communications` (for tone) | Publisher: `senior-ai-governance-architect` or the enterprise's model-card publication authority |
| Regulator response | Drafts / factual-checks | `legal`, `head-of-ai-governance`, subject-matter contributors (privacy, security, business line) | Signer: accountable executive named for the specific regulator and jurisdiction |
| Public consultation response | Drafts factual content | `government-affairs` (where it exists), `legal`, `senior-ai-governance-architect`, `head-of-ai-governance`, `communications` | Signer: `head-of-ai-governance` or an executive on the material-position path |

The analyst never sends an external artefact from the analyst's own account. Sending is always through the reviewer / signer chain.

## The escalation red flags

Certain findings in the course of external-facing drafting are *stop and escalate* signals — the analyst pauses drafting and routes to legal and head of governance before continuing.

- **A material mis-statement in an already-published external artefact.** A trust-site claim that turns out to be unsupported; a model card that overclaimed; a prior regulator response whose factual basis has since shifted. This is a legal-and-comms decision, not an analyst-desk fix.
- **A regulator inquiry that the analyst has been asked to answer without a legal review path.** Even if the analyst's response would be factually correct, submitting without a legal review is a boundary breach. The analyst says *"I can draft; I need legal review before submission"* and does not proceed without it.
- **A press or media inquiry directed to the analyst.** Not the analyst's desk. Route to `communications` immediately; do not respond.
- **A social-media post that misrepresents the enterprise's AI posture and is gaining traction.** Route to `communications`; the analyst may be asked to draft factual clarification content, but the response is not launched from the analyst desk.
- **A whistleblower or worker report received externally.** Route to the enterprise's whistleblower channel — usually a legal-owned intake — and to `head-of-ai-governance` as a governance-council matter for a subsequent meeting.
- **Any request to publish something before the review chain is complete.** *"Can we just get this up on the site today?"* — no. The chain exists to catch precisely the failure modes the shortcut invites.

## The public-facing vocabulary discipline

External-facing content sits under a stricter vocabulary discipline than internal briefings. Rules the analyst applies to every external draft:

- **Names of frameworks and standards are precise.** *"ISO/IEC 42001:2023"* (with the year), not *"ISO 42001"*. *"NIST AI Risk Management Framework 1.0"*, not *"the NIST framework"*. *"Regulation (EU) 2024/1689 (the EU AI Act)"* on first use, then *"the EU AI Act"* thereafter.
- **Verbs of adherence are distinguished.** *Certified* (an accredited certification body has issued a certificate) ≠ *aligned* (the enterprise's practice tracks the framework but has no third-party attestation) ≠ *implementing* (the enterprise is in progress but not yet aligned) ≠ *compliant* (a statute-flavoured word usually best avoided outside legal review). The analyst does not use *certified* unless a certificate exists.
- **Metrics are cited with their measurement basis.** *"Accuracy 87 % on the [named] evaluation set as of [date]"* rather than *"highly accurate"*.
- **Limitations are named.** External model cards, external transparency notices, and trust-site descriptions all name the limitations the internal artefacts name.
- **No comparative claims about competitors.** *"Better than [competitor's] approach"* invites competitive-marketing scrutiny and does not add substance.
- **No speculation about future capability.** *"Our system will soon..."* creates forward-looking-statement exposure and is not analyst-desk speech.

## Interaction with EU AI Act Article 50 (transparency)

The EU AI Act's Article 50 imposes specific transparency obligations on providers and deployers of certain AI system categories — systems that interact with people, systems that generate synthetic content, and systems performing emotion recognition or biometric categorisation, among others. For enterprises in the EU AI Act's territorial scope, some Article 50 obligations translate directly into external-facing content the analyst helps compose:

- Informing individuals that they are interacting with an AI system (where the interaction is with an AI system that is not obviously such).
- Labelling AI-generated or AI-manipulated content (deepfakes, synthetic media) as artificially generated.
- Informing individuals that they are the subject of emotion recognition or biometric categorisation (subject to the article's exceptions).

The transparency notice is a compliance artefact, not marketing content. It is short, factual, in the language of the affected individual's jurisdiction, and readily accessible. `legal` and (where personal data is in scope) `privacy` own the article's interpretation; the analyst drafts the notice and coordinates the placement across the enterprise's user-facing surfaces. Chapter 06's routing chain applies. <!-- needs-research: Article 50 obligations vary across sub-provisions and are being clarified in secondary legislation and Commission guidance; confirm current state before drafting Article-50 notices. -->

## What to memorise

- **The analyst drafts and factual-reviews. The analyst does not sign, publish, or speak-of-record externally.**
- **Four external artefact families: trust site, published model cards, regulator responses, public consultation responses.**
- **Every external artefact has a review-and-approval chain — legal, communications, head of governance, and (for regulator responses) an accountable executive.**
- **External vocabulary is strict.** Named frameworks with versions, verbs of adherence distinguished (*certified* ≠ *aligned* ≠ *compliant*), metrics cited with their basis, limitations named.
- **A published mis-statement is a stop-and-escalate signal.** Route to legal and head of governance; do not silently fix.
- **A press or media inquiry is not the analyst's desk.** Route to communications immediately.
- **EU AI Act Article 50 transparency notices are compliance artefacts.** Draft to the article; do not marketing-ise.

## Summary

External-facing responsible-AI communication is where the analyst's writing intersects with the enterprise's public-facing risk surface. The analyst drafts and factual-reviews trust-site content, published model cards, regulator responses, and public consultation responses — but does not sign, does not publish, and does not speak of record. Every artefact moves through a mapped review-and-approval chain; every artefact respects the external-vocabulary discipline (precise framework names, distinguished verbs of adherence, cited metrics, named limitations); every red flag (published mis-statement, unreviewed regulator submission, press inquiry, whistleblower report, shortcut publication request) is a stop-and-escalate signal. The analyst's contribution to external speech is bounded and consequential — done well, it is how the enterprise's internal governance posture becomes legible to the outside world. Chapter 08 turns to the analyst's own professional-development vocabulary — the AIGP body of knowledge and the certifications the analyst sequences into their portfolio.
