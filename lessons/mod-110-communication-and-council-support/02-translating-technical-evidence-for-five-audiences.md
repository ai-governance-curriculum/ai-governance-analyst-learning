# Translating Technical Evidence for Five Audiences

## Why this chapter

The analyst's inbox is dense with technical artefacts: an eval report with a per-group accuracy table, an OWASP LLM Top 10 finding on a RAG pipeline, an incident post-mortem citing a data-drift metric, a residual-risk claim scored 4×3 on the enterprise's risk matrix, a control-status report row that reads *not-yet-tested*, an FRIA update that references EU AI Act Article 27. Each of these artefacts is legible to its author's function. None of them is legible to the five downstream audiences that will *act* on them: legal, privacy, security, product, and the executive committee.

*Translation* is the analyst-tier verb for restating what the artefact claims in the receiving audience's language, without changing the claim. It is distinct from *summarisation* (which drops information) and *rewriting* (which changes claims). Get this move right and legal opens a case file, privacy opens a lawful-basis review, security opens a mitigation ticket, product moves the launch gate, and the executive committee books the decision on next month's agenda. Get it wrong — write the legal audience an eval-metric table, write product an SR 11-7 clause reference — and the artefact stalls in the reader's inbox.

Chapter 03 handles the sixth audience (the board, in ISO/IEC 38507 vocabulary) separately, because governance-body speech has stricter conventions than executive-committee speech. This chapter walks the five day-to-day audiences.

## The translation-not-summarisation rule

Two rules bound every translation the analyst produces.

- **The audience-adapted briefing must be able to point to the underlying artefact for every claim it makes.** No claim without a citation to the eval report, the incident record, the register entry, the control-status row, the tracker row, or the impact assessment it came from. A briefing that reads well but cannot be traced back to the source is a rewrite, not a translation. Chapter 05's *decision-record survivability* rule inherits this.
- **The briefing does not add claims the underlying artefact does not support.** If the eval report says *demographic-parity difference is 0.08 with a 95 % CI of [0.05, 0.11]*, the briefing says the same thing in the audience's words — it does not say *the model is unbiased*, does not say *the model is materially biased*, and does not extend the finding to failure modes the eval did not measure. Where the audience's decision requires a claim the artefact does not support, the analyst names the gap explicitly and routes it (typically to `ai-eval-engineer` or `ai-risk-engineer`) rather than filling it in.

These two rules are what separate an analyst-tier briefing from a marketing document.

## The five audiences and what each is trying to decide

Before writing, name what the audience is deciding. The audience is not reading for pleasure; they are reading to decide something.

| Audience | The decision they are trying to make |
|---|---|
| Legal | Does this artefact create legal exposure (statutory, regulatory, contractual, tort) that legal needs to open a case file on, mitigate, or disclose? Which statute, which article, which contract clause? |
| Privacy | Does this artefact trigger a lawful-basis issue, a data-subject-rights obligation (access, rectification, erasure, objection, Article 22 automated-decision), a DPIA re-open, a cross-border-transfer question, or a data-minimisation finding? |
| Security | Does this artefact indicate a threat (per OWASP LLM Top 10, MITRE ATLAS, NIST AI 100-2, or Google SAIF) that needs a mitigation ticket, a control retest, a red-team engagement, or an escalation to the SOC? |
| Product | Does this artefact change the launch gate — is the feature approved for the announced launch, does it need a scoped mitigation before launch, does the launch slip, or does the feature ship in a degraded / gated mode? |
| Executive committee | Does this artefact require a portfolio-level decision — resource allocation, priority re-ordering, strategic pivot, external-communication trigger, or council-agenda escalation? |

The briefing's structure follows the decision. If the decision is *does this create legal exposure and if so what kind*, the briefing's headline is the exposure characterisation, not the eval-metric table.

## The audience-adapted briefing matrix

For each audience: the length, the vocabulary anchor, the depth of technical detail, the required cross-references, and the delivery channel.

### Legal

- **Length.** One to three pages. Legal reads for exposure characterisation, not for methodology.
- **Vocabulary anchor.** Statute / regulation / contract-clause names. EU AI Act Article number, GDPR Article number, US-state statute name, Title VII of the Civil Rights Act, ECOA / Regulation B, HIPAA, contract-clause identifier. If the artefact cannot be tied to a specific legal anchor, the briefing names *no known legal anchor* — silence is a fail.
- **Depth of technical detail.** Just enough to make the exposure legible. The eval-metric table goes in an annex; the body of the briefing translates the metric into the shape of the exposure.
- **Required cross-references.** The underlying artefact ID (`EVAL-`, `INC-`, `RISK-`, `IA-`, `CTL-`), the applicable statute / regulation citation (with article number, not just a name), and — where relevant — the tracker row from `mod-106`.
- **Delivery channel.** Email or memo, with a subject line that names the artefact ID and the legal question. *"INC-2026-0018 — potential Article 22 automated-decision exposure — please review by Friday."*

**Translation moves the analyst makes for legal.**

- *"Demographic-parity difference is 0.08 with 95 % CI [0.05, 0.11] on the female-vs-male axis"* becomes *"the model's approval rate for female applicants is 8 percentage points below the male approval rate, well outside the four-fifths rule the EEOC Uniform Guidelines apply to selection procedures. Legal-adjacent exposure: Title VII disparate impact if the model is used for hiring decisions."*
- *"Prompt-injection finding on the RAG assistant, OWASP LLM01"* becomes *"a customer or third party can craft input to the assistant that causes it to reveal internal-only information. Legal-adjacent exposure: contractual confidentiality obligations if the internal-only information is a customer's; potential regulator interest if the disclosed information is PII."*
- *"CTL-2026-0044 tested this quarter, evidence is stale, control is inoperative"* becomes *"the control the enterprise pointed to in its EU AI Act Article 9 risk-management response was not operating during the sampled period; the assurance the enterprise's ISO/IEC 42001 certification depends on is at risk."*

### Privacy

- **Length.** One to two pages, plus a lawful-basis / data-flow annex where a DPIA re-open is triggered.
- **Vocabulary anchor.** GDPR articles (5, 6, 9, 22, 25, 32, 35), the enterprise's DPIA methodology, the ICO's AI-and-data-protection guidance, or the equivalent DPA guidance for the applicable jurisdiction. For US-flavoured privacy, HIPAA, GLBA, or the applicable state privacy statute (CCPA/CPRA, VCDPA, CPA, CTDPA).
- **Depth of technical detail.** Data-flow and processing detail — what personal data is processed, where it is stored, for how long, who has access, whether it crosses borders, whether it is used to train, whether the output reaches a data subject.
- **Required cross-references.** The DPIA identifier (`DPIA-<year>-<sequence>` from `mod-105`), the affected `INV-` inventory row's data-flow section, the vendor row (`VND-<year>-<sequence>`) if a third-party model or vendor is in the flow, and the tracker row for the applicable privacy statute.
- **Delivery channel.** Email / Teams / GRC-platform DPIA update, with a subject line naming the DPIA re-open trigger.

**Translation moves for privacy.**

- *"Data drift detected: 14 % of inputs are out-of-distribution vs the training distribution"* becomes *"the model is now being used with input populations it was not originally assessed on. If any of the new input population is a special-category personal data (Article 9), the DPIA needs to re-open the necessity-and-proportionality assessment for that population."*
- *"New retrieval-index source added in Sprint 22 release"* becomes *"the RAG assistant now retrieves from a source that was not documented in the original data-flow. Article 5(1)(a) lawful-basis and Article 13/14 transparency-notice implications: the enterprise's privacy notice may not currently cover the new source's processing."*
- *"Hallucination-driven-harm incident with a wrong policy citation to a customer"* becomes *"the model produced an inaccurate personal-data output about the enterprise's own policies. Article 5(1)(d) accuracy principle and Article 16 right-to-rectification are potentially triggered; DPIA re-open assessment per `mod-105` chapter 05 is warranted."*

### Security

- **Length.** One to two pages, with a mitigation-tracking annex when a security-ticket is opened.
- **Vocabulary anchor.** The four security-taxonomy references from `mod-108`: OWASP LLM Top 10, MITRE ATLAS, NIST AI 100-2, and Google SAIF. Also — where the artefact touches classical security — the enterprise's classical vulnerability-severity model (CVSS, or the enterprise's internal equivalent).
- **Depth of technical detail.** Enough to make the threat class, the exploit path, and the mitigation surface legible. The security audience reads the technical detail directly; the translation is *from* eval / risk / incident vocabulary *into* threat-taxonomy vocabulary.
- **Required cross-references.** The underlying artefact ID; the OWASP-LLM-Top-10 / ATLAS / NIST-AI-100-2 / SAIF entry (or entries) the finding maps to; the affected inventory row; the existing security ticket (or the request to open one); the vendor row if a third-party model is implicated.
- **Delivery channel.** Security ticket in the enterprise's security-work-tracker, cross-linked from the GRC record.

**Translation moves for security.**

- *"The eval battery's refusal-rate on jailbreak-attempt prompts dropped from 94 % to 71 % after the model update"* becomes *"a regression on OWASP LLM01 (prompt-injection) resistance. The updated model is 3× more likely to comply with a prompt-injection attempt than the pre-update model was."*
- *"CTL-2026-0031 (output-classifier freshness) is not-tested this quarter"* becomes *"the enterprise's declared mitigation for OWASP LLM05 (improper output handling) does not currently have evidence of operating. If exploited, blast radius per the affected `INV-` row: [description]."*
- *"An FRIA identified a fundamental-rights concern on the CV-screener"* becomes *"a downstream data source (the CV-screener's decision) may be a target for adversarial evasion (per MITRE ATLAS AML.T0043 category). Recommend red-team scoping with `ai-risk-engineer`."*

### Product

- **Length.** One page, with a launch-gate recommendation and the mitigation surface if the gate is *conditional*.
- **Vocabulary anchor.** The launch date, the feature name, the customer segment, the launch gate, the roadmap milestone, and the specific mitigation the launch is conditioned on. Product does not read for framework citations — it reads for what does or does not ship next Monday.
- **Depth of technical detail.** Just enough to make the launch-gate call defensible. Metric detail goes in the appendix; the body is the launch-gate call and the "why."
- **Required cross-references.** The underlying artefact ID; the launch-gate record (or the ticket where it lives); the mitigation ticket if one is required.
- **Delivery channel.** Product-team channel (Slack, Teams, or the product-tracker's launch record), with a subject line that names the feature and the gate call.

**Translation moves for product.**

- *"The residual-risk score on RISK-2026-0104 is 4×3=12 on the enterprise's matrix; the risk owner has re-accepted after the mitigation"* becomes *"Feature X is approved to launch on the planned date, conditional on the mitigation in ticket [ID] shipping to production by Wednesday."*
- *"The 42001 clause 9.1 evidence for this system's control set is complete for release 1 and open for release 2"* becomes *"Feature X release 1 has passed the release-assurance gate. Release 2's assurance is scheduled to complete in [N] weeks — plan the release-2 launch after that date."*
- *"Article 27 FRIA identified a specific-conditions clause that needs a data-subject-notice update"* becomes *"before Feature X launches to EU users, we need to update the privacy notice. Estimated turnaround with privacy: [N] business days; recommend planning the EU launch [N+2] business days after the domestic launch."*

### Executive committee

- **Length.** Half a page to one page. The executive committee reads a portfolio-level view; a briefing that does not fit on one page is being read by someone else's team, not by the executive.
- **Vocabulary anchor.** The enterprise's own strategic-priority language, the portfolio-level metrics the executive committee tracks (revenue, cost, risk exposure, customer trust, regulatory posture, competitive position). Framework citations go in an annex or a footnote; the body speaks the enterprise's language.
- **Depth of technical detail.** Minimal in the body; the executive committee reads for portfolio-level decisions, not for methodology. The technical detail is in the underlying artefact, cited by ID for anyone who wants to walk down into it.
- **Required cross-references.** The underlying artefact ID(s), the portfolio-level dashboard the finding appears on, the council packet or minute-entry if the finding has already been to council.
- **Delivery channel.** Executive-committee pre-read pack (drafted by the analyst, delivered by `head-of-ai-governance`); occasionally a one-off memo when the finding needs a between-meeting escalation.

**Translation moves for the executive committee.**

- *"Two register entries scored above the CAIO-attention threshold this month"* becomes *"Two AI systems in the portfolio have unmitigated risk levels above the level the enterprise's risk appetite currently accepts. Both are on the current AI governance council agenda for a residual-risk-acceptance decision."*
- *"The regulator tracker added three new EU AI Act guidance documents this quarter and one new US-state statute"* becomes *"Four new external obligations landed this quarter. Estimated policy-work impact: [N] weeks of senior-architect effort to update the internal control library. Recommended sequencing on the standing agenda."*
- *"A serious-incident notification was drafted and submitted under EU AI Act Article 73"* becomes *"The enterprise's first regulator notification under the EU AI Act's serious-incident regime was filed on [date]. The next likely regulator touch-point is [date]. Communications and legal are running the follow-through."*

## The common failure modes

- **Writing the framework vocabulary the analyst is fluent in, not the audience's.** A legal-audience briefing that cites *ISO/IEC 42001 clause 9.1.2* without translating what the clause obliges. A product-audience briefing that cites *NIST AI RMF MEASURE 2.11* without saying whether the launch is approved. Fix: name the audience-and-decision before drafting; write the headline in the audience's language and only *then* backfill the citations in a footnote or annex.
- **Summarising rather than translating.** A four-paragraph briefing that omits the metric's confidence interval, or the incident's affected-user count, or the residual-risk score. The audience acts on the summary and does not know the omitted information exists. Fix: include the underlying quantitative claim (with its uncertainty), even when it is uncomfortable — if it is uncomfortable, name the discomfort explicitly rather than by omission.
- **Adding claims the artefact does not support.** *"The model is unbiased"* when the eval measured demographic parity on one axis and found a small difference — the eval does not support *unbiased*, only *within-threshold on demographic parity along that axis*. Fix: pick the words the eval or the risk register uses, and preserve them in the translation.
- **Sending the same briefing to all five audiences.** The security team gets the executive-committee half-pager; legal gets the launch-gate note. Neither can act on it. Fix: write one briefing per audience even when the underlying artefact is the same. It is more work; it is the work.
- **Deferring the audience's decision by burying it in the appendix.** A launch-gate briefing where the actual *approved / not-approved* call sits three pages in. Fix: put the call in the first paragraph. If the analyst cannot state the call in the first paragraph, the analyst has not yet done the translation — go back and do it before sending.
- **Citing framework text verbatim instead of translating it.** Copying an EU AI Act article number and its Recital wording into a product briefing without saying what the product team needs to do about it. Fix: cite the article; then say, in the product team's language, what the citation means for the launch.

## The routing dependency

Every audience-adapted briefing has a routing dependency the analyst manages explicitly.

- **Legal briefings** may open a legal-privilege question. The analyst's briefing itself may or may not be privileged, depending on the enterprise's privilege posture; where privilege is in question, the analyst asks legal counsel *before* sending, and marks the briefing accordingly. `legal` owns the privilege call, not the analyst.
- **Privacy briefings** where a DPIA re-open is triggered route through the DPO (or the equivalent privacy office) for sign-off on the re-open. The analyst drafts; the DPO closes.
- **Security briefings** open a security ticket in the security-work-tracker and route to the security engineer named for the affected system. `ai-infra-security` owns the mitigation call.
- **Product briefings** land in the product tracker and route to the PM plus the engineering lead. The launch-gate call may become a council agenda item if the residual risk is above the enterprise's council-attention threshold; that routing is chapter 04's territory.
- **Executive-committee briefings** are delivered *by `head-of-ai-governance`*, not by the analyst directly. The analyst drafts; the head of governance decides whether and how the briefing lands on the executive-committee agenda. The analyst does not go around the head of governance to the executive committee.

## What to memorise

- **Translation ≠ summarisation ≠ rewriting.** Preserve the underlying claim; use the audience's vocabulary; do not add claims the artefact does not support.
- **Name the audience and the decision *before* drafting.** The briefing's structure follows the decision.
- **One briefing per audience.** The security team's briefing is not the executive committee's briefing.
- **The audience-adapted briefing must trace to the underlying artefact by ID for every claim it makes.** No traceability, no briefing.
- **Executive-committee briefings are delivered by `head-of-ai-governance`, not by the analyst.** The analyst drafts.
- **The board-level briefing has its own vocabulary constraint — ISO/IEC 38507.** Chapter 03 walks it.

## Summary

Translation is the analyst's day-to-day verb across the five audiences. Legal reads for exposure, privacy for lawful basis and rights, security for threat class and exploit path, product for the launch gate, the executive committee for portfolio-level decisions. Each audience gets its own briefing, in its own vocabulary, at its own depth, over its own delivery channel — with the underlying artefact ID cited for every claim. The analyst does not summarise (which drops information), does not rewrite (which changes claims), and does not add claims the artefact cannot support. Chapter 03 adds the sixth audience — the board — and the ISO/IEC 38507 vocabulary the board briefing must use.
