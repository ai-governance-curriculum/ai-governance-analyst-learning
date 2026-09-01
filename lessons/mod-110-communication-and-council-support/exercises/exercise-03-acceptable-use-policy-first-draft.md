# Exercise 03 — Acceptable-Use Policy First Draft

**Estimated effort:** 2 hours
**Grounding chapters:** [01 — The Analyst's Scope on Communication and Council Support](../01-analyst-scope-on-communication-and-council-support.md), [06 — Drafting First-Cut Internal AI Policies and Standards](../06-first-cut-internal-ai-policies-and-standards.md), [07 — External-Facing Responsible AI Communication](../07-external-facing-responsible-ai-communication.md), [09 — Delegation Boundary and Escalation Patterns](../09-delegation-boundary-and-escalation-patterns.md).

## Objective

Compose the analyst-tier first-cut draft of the enterprise's AI acceptable-use policy (AUP) per chapter 06, with the routing header populated for the analyst → senior architect → cross-functional consultation → ratification chain. The AUP is the enterprise-wide, employee-facing statement of what AI use is permitted, restricted, and prohibited; it is the *policy-level* document that sits above the model-approval standard and the third-party AI vendor review standard and above the generative-AI employee guidance that lives underneath it. Getting the AUP's level right — policy, not standard, not procedure — is chapter 06's most-common failure mode; this exercise is where the analyst practises against that failure.

The drill's point is that a first-cut is a first-cut. The analyst does not need to consult privacy, security, legal, HR, and procurement before releasing the draft — that is the *consultation phase*, owned by `senior-ai-governance-architect` (chapter 06 routing chain). The analyst does need to produce a draft that (a) sits at the correct policy level, (b) carries the universal section shape, (c) mirrors EU AI Act Article 5 prohibitions in the prohibited-use list, (d) carries a working exception process, (e) is short enough to be read, and (f) routes cleanly into the chain.

After this exercise you should have a ready-to-route first-cut AUP draft that the analyst can hand to `senior-ai-governance-architect` for the architect-edits phase, plus the analyst's own scratch-pad noting the sections the analyst expects the consultation phase will surface substantive edits on.

## Prerequisites

- Chapter 01 read; the analyst's role (first-cut drafter, not ratifier) and the three tangible outputs fresh in memory.
- Chapter 06 read at depth. Particularly: the policy-vs-standard-vs-guidance-vs-procedure hierarchy, the four-phase routing chain (first-cut, architect edits, cross-functional consultation, ratification), the routing header shape, the universal section shape (purpose, scope, definitions, requirements, roles, exceptions, enforcement, related documents, revision history), the AUP anchor content, and the AUP common first-cut failure modes.
- Chapter 07 read, particularly the external-facing vocabulary discipline (*certified* vs *aligned* vs *implementing* vs *compliant*) — the AUP does not usually make external-facing claims, but the vocabulary discipline applies internally too, particularly to any *related documents* references to ISO/IEC 42001 or NIST AI RMF.
- Chapter 09 read; the delegation-boundary rows for policy and standard drafting (analyst originates; architect edits; head of governance ratifies) and the class-2 (boundary-holding request) and class-4 (recurring-pattern → policy-work) escalation shapes.
- EU AI Act Article 5 (prohibited AI practices) read at analyst-tier depth. The AUP's prohibited-use list mirrors Article 5 with enterprise-specific additions layered on; the analyst reads the article directly rather than a summary.
- The enterprise's existing policies you have carried from earlier work, if any (an existing information-security policy, an existing acceptable-use policy for IT resources generally, an existing data-protection policy) — the AUP intersects with these and should cross-reference them rather than re-authoring their content.

## Problem statement

The deliverable is a **single Markdown file `mod-110-ex-03-aup-first-cut.md`** containing:

- The routing header per chapter 06 (routing state = *first-cut*, phase 1 of 4).
- The AUP's universal-shape sections populated with substantive first-cut content.
- A short *analyst's scratch-pad* at the end (a section clearly separated from the AUP body) noting the areas the analyst expects the consultation phase will surface substantive edits on.

Assume the enterprise is a mid-sized multi-jurisdictional company with a materially-sized AI portfolio (dozens of AI systems across product, customer support, HR, and internal-productivity domains), operating in the UK (primary) and EU (secondary) with limited US-consumer-facing exposure. The enterprise has an existing IT-and-information-security acceptable-use policy the AUP does not replicate but does cross-reference. The enterprise's inventory (`mod-102`) is the source-of-truth for approved AI tools; the model-approval standard (chapter 06's second canonical draft — hypothetical for this exercise) is the source-of-truth for how a new AI use gets approved.

Adjust the assumed enterprise profile to match your own worked-artefacts context if you have one; note the substitution at the top of the deliverable.

### The routing header

Populate chapter 06's routing header at the top of the document:

```
Document: Policy  ·  AI Acceptable-Use Policy  ·  Version: 0.1 draft
Routing state: first-cut
First-cut author: [analyst name] — [YYYY-MM-DD]
Architect editor: TBD-senior-ai-governance-architect — status: pending
Consultation contributors: TBD-legal, TBD-privacy/DPO, TBD-security, TBD-HR, TBD-procurement, TBD-business-line-owner(s)  ·  status per contributor: pending
Ratifier: TBD-head-of-ai-governance — status: pending
Supersedes: N/A (first issue)
Effective date: TBD (set at ratification)
Next scheduled review: 12 months after effective date
```

### The AUP body

Populate chapter 06's universal sections with substantive first-cut content. Anchor content per section:

#### 1. Purpose

One paragraph. State the enterprise's commitment to responsible, lawful, and human-oversighted AI use. Name the policy's fit in the enterprise's broader policy library (above the model-approval standard and the third-party AI vendor review standard; below the enterprise's overarching code of conduct). Do not restate what the model-approval standard operationalises; that is a level-confusion failure.

#### 2. Scope

One paragraph. All employees, contractors, and consultants operating on enterprise infrastructure or with enterprise data or on the enterprise's behalf. All AI systems the enterprise builds, procures, or uses — including free-tier and trial vendors (chapter 06 was explicit that the free-tier gap is a common vendor-standard failure; the AUP closes it explicitly). Name the UK and EU jurisdictions specifically. Name any explicit exclusions (research-and-development sandboxes with named isolation, if the enterprise has them).

#### 3. Definitions

A short glossary (6 to 10 terms) covering at minimum: *AI system*, *AI use*, *approved AI tool*, *personal data* (by reference to the enterprise's data-protection policy), *high-risk AI system* (by reference to the enterprise's tiering methodology and the EU AI Act Annex III), *deployer* and *provider* (per EU AI Act Article 3 definitions), *generative-AI tool*, *automated decision-making* (by reference to GDPR Article 22). Cross-references to `mod-101` vocabulary or to the AIGP body of knowledge (chapter 08) where the term is defined there.

#### 4. Requirements

Numbered requirements grouped as *permitted uses*, *restricted uses (permitted-with-conditions)*, and *prohibited uses*. The requirements are the substantive body of the policy and must exercise chapter 06's AUP anchor content specifically:

- **Permitted uses.** At least three requirements. Examples of the shape (compose your own specifics):
  - *Permitted-1.* Employees may use enterprise-sanctioned AI tools on the approved-AI-tools list (`mod-102` inventory) for the purposes documented in the tool's model card (`mod-105`).
  - *Permitted-2.* Employees may use approved generative-AI tools for internal drafting, brainstorming, summarisation of publicly available reference material, and other productivity-adjacent uses subject to the accuracy-review-of-output requirement under Restricted uses.
  - *Permitted-3.* [Your third; think of a plausible permitted use in your enterprise context.]

- **Restricted uses (permitted-with-conditions).** At least five requirements. Each must name the condition specifically. Examples:
  - *Restricted-1.* Employees may not enter customer or worker personal data (as defined) into any AI tool not on the approved-AI-tools list. Restricted uses require sign-off per the model-approval standard.
  - *Restricted-2.* Employees may not use AI tools to produce content that will reach a customer, a regulator, or a public audience without a human review of the output. The enterprise's accuracy standards apply to AI-assisted work exactly as they apply to human work.
  - *Restricted-3.* Employees may not deploy generative-AI tools in a customer-facing role that is not transparently labelled as AI-assisted, per EU AI Act Article 50 transparency requirements where they apply.
  - *Restricted-4.* Employees using AI tools in the course of hiring, performance evaluation, benefits eligibility, or credit decisions may not use the tool as the sole decision-maker; documented human oversight is required per the enterprise's model-approval standard (chapter 06) and EU AI Act Article 14 for high-risk systems.
  - *Restricted-5.* [Your fifth; think of a plausible restricted use.]

- **Prohibited uses.** At least four requirements. Mirror EU AI Act Article 5 (chapter 06 was explicit that omitting Article 5 from the prohibited-use list is a common first-cut failure mode). Examples:
  - *Prohibited-1.* Employees may not use AI systems for practices prohibited under EU AI Act Article 5, including but not limited to: subliminal techniques materially distorting behaviour; exploitation of vulnerabilities of specific groups; social scoring by public authorities; real-time remote biometric identification in publicly accessible spaces (except under the article's narrow law-enforcement exceptions, which do not apply to the enterprise's operations); untargeted scraping to build facial-recognition databases; emotion recognition in the workplace or educational institutions (except under the article's exceptions); biometric categorisation of individuals based on protected characteristics; predictive policing based solely on profiling; individual criminal-risk assessment based solely on profiling.
  - *Prohibited-2.* Employees may not use AI systems to make final decisions on hiring, termination, credit, or benefits eligibility without documented human oversight and without following the model-approval standard's high-risk sign-off path.
  - *Prohibited-3.* Employees may not paste customer personal data, worker personal data, market-sensitive commercial information, legally privileged material, or credentials into any AI tool that is not on the approved-AI-tools list and specifically approved for that data category.
  - *Prohibited-4.* Employees may not use AI systems to circumvent enterprise security controls, to conceal the AI-assisted origin of content where transparency is required, or to violate the enterprise's code of conduct or applicable law.

Number the requirements consistently so downstream controls (`mod-108`) and audits can cite them by number.

#### 5. Roles and responsibilities

Name the following roles at minimum:

- **Every employee, contractor, and consultant** — compliance with the policy; reporting non-compliance and incidents.
- **Managers** — oversight of team members' AI use; ensuring team members complete required AI-use training.
- **`ai-governance-analyst`** — intake of new AI use cases into the inventory; running the model-approval process; register maintenance; reporting to the AI governance council.
- **`senior-ai-governance-architect`** — standard-level exception approvals; ownership of the enterprise's AI policy library architecture.
- **`head-of-ai-governance`** — ratification of the AUP and its revisions; approval of policy-level exceptions; chair of the AI governance council (if that is the enterprise's terms of reference).
- **`legal`** — enforcement partnership with HR; interpretation of statutory and regulatory obligations the AUP references.
- **`HR`** — enforcement of the AUP through the enterprise's disciplinary policy; distribution of the generative-AI employee guidance to the workforce.
- **`security`** — enforcement of security-adjacent AUP requirements (credentials, information categorisation).
- **`procurement`** — enforcement of the AUP's vendor-and-tool intake requirements in the procurement workflow.
- **The AI governance council** — governance-level oversight of AI use across the enterprise; escalations from role owners.

#### 6. Exceptions and waivers

Name the exception process explicitly. Chapter 06 was explicit that every policy needs an exception process; a policy with no path for exceptions gets ignored. At minimum:

- **Standard-level exceptions** (exceptions to specific restricted-use requirements) — routed through `senior-ai-governance-architect` for approval; recorded as `EXC-<year>-<sequence>` in the GRC platform.
- **Policy-level exceptions** (exceptions to prohibited-use requirements, or exceptions with enterprise-wide effect) — routed through `head-of-ai-governance` for approval; escalated to the AI governance council for endorsement; recorded as `EXC-<year>-<sequence>` in the GRC platform with a stated time-bound expiry.
- **No self-approved exceptions.** Employees do not approve exceptions to their own use.
- **Exception register review cadence.** Reviewed monthly at the AI governance council (chapter 04 standing-agenda item).
- **Prohibited-use exceptions.** The prohibited-use requirements are not subject to exception under the AUP; where an enterprise use case appears to require an EU AI Act Article 5 exception (e.g., a narrow law-enforcement exception the enterprise might qualify for), the request routes through `legal` and `head-of-ai-governance` and requires a separate policy-level decision, not an exception under the AUP.

#### 7. Enforcement

Name the consequences of non-compliance and where enforcement authority sits. Reference-and-cross-reference discipline: the AUP does not restate the disciplinary policy or the code of conduct; it names them and states that AUP non-compliance is a violation under those. At minimum:

- **Employees, contractors, consultants** — enforcement through the enterprise's disciplinary policy (cite by name), which may include remedial training, formal warning, suspension of tool access, and termination for repeated or severe non-compliance.
- **Regulator, contract, and legal-exposure consequences** — reference the enterprise's legal policy; consequences under applicable statutes and regulations (EU AI Act, UK Equality Act, GDPR, others).
- **Reporting non-compliance.** Named channels — the intake mailbox for the AI governance analyst; the whistleblower channel for reports the reporter believes require anonymity; the enterprise's incident-response channel for incidents (chapter 09).

#### 8. Related documents

Cross-references to other policies, standards, guidance, and external frameworks. At minimum:

- The enterprise's Code of Conduct.
- The enterprise's IT and Information Security Acceptable-Use Policy (the AUP for IT resources generally).
- The enterprise's Data Protection Policy.
- The enterprise's Model Approval Standard (chapter 06 second canonical draft).
- The enterprise's Third-Party AI Vendor Review Standard (chapter 06 third canonical draft).
- The enterprise's Generative-AI Employee Guidance (chapter 06 fourth canonical draft).
- The enterprise's Incident Response Policy (or equivalent) — the AI-incident intake feeds into this per `mod-109`.
- External frameworks (cited as *aligned with*, not *compliant with* — chapter 07 vocabulary discipline): ISO/IEC 42001:2023 AI management system; ISO/IEC 38507:2022 governance implications of AI; NIST AI Risk Management Framework 1.0. Applicable statutes cited (EU AI Act — Regulation (EU) 2024/1689; UK Equality Act 2010; UK GDPR; EU GDPR — Regulation (EU) 2016/679).

#### 9. Revision history

The first entry — v0.1 first-cut draft, [YYYY-MM-DD], [analyst], initial issue.

### The analyst's scratch-pad

At the end of the deliverable, a section clearly separated from the AUP body:

```
--- Analyst's scratch-pad (not part of the AUP) ---
```

with 200 to 400 words on:

- The two or three sections the analyst expects the consultation phase to surface the most substantive edits on (candidates chapter 06 named: legal on statute-alignment; privacy on lawful-basis and data-flow; security on threat-taxonomy alignment; HR on employment-law implications of the worker-monitoring adjacencies; business lines on operational feasibility).
- The one or two requirements the analyst is *least confident* about — where the analyst has drafted a first cut but expects the architect or the contributor group to substantively rework the language. Naming this explicitly is what makes the routing chain honest.
- Any candidate for a chapter-04 sensitive-item flag if this policy's ratification lands at the council (usually not, but occasionally an AUP touches personnel-relations or trade-union-consultation questions that shift the disposition).
- Any candidate for a chapter-09 class-4 escalation surfacing from the AUP work — recurring policy-exception patterns that suggest the section is misspecified, or recurring intake questions from the workforce that suggest the guidance (chapter 06 fourth canonical draft) needs updating.

## Requirements

- **The file is a single Markdown file** `mod-110-ex-03-aup-first-cut.md`.
- **The routing header is present and populated** per chapter 06's header shape. Routing state = *first-cut*; the analyst is named as the first-cut author; TBD placeholders for the architect, contributors, and ratifier are acceptable.
- **All nine universal-shape sections are present.** Purpose, Scope, Definitions, Requirements, Roles, Exceptions and waivers, Enforcement, Related documents, Revision history.
- **The document is at policy-level, not standard-level or procedure-level.** Chapter 06 was explicit that the AUP names *categories* not *tools*; a first-cut that lists specific tool names, specific versions, or specific configuration settings has drifted to standard-level and is off-side.
- **Length is 3 to 5 pages.** Chapter 06 was explicit that policies longer than this stop being read. Enforce the length.
- **The prohibited-use list mirrors EU AI Act Article 5 explicitly** and cites the article. Chapter 06 named the Article 5 omission as a common failure mode.
- **The exception process is present and specific.** Named routing, named approvers (standard-level to `senior-ai-governance-architect`, policy-level to `head-of-ai-governance`), named recording (`EXC-<year>-<sequence>` in the GRC platform), no self-approved exceptions, review cadence on the council standing agenda, and the explicit position that prohibited-use requirements are not subject to exception under the AUP.
- **The related-documents section cites both internal and external references.** Internal at minimum: Code of Conduct, IT AUP, Data Protection Policy, Model Approval Standard, Third-Party AI Vendor Review Standard, GenAI Employee Guidance, Incident Response Policy. External at minimum: ISO/IEC 42001:2023, ISO/IEC 38507:2022, NIST AI RMF 1.0, EU AI Act (Regulation (EU) 2024/1689), UK Equality Act 2010, UK GDPR, EU GDPR (Regulation (EU) 2016/679).
- **External-facing vocabulary discipline is applied.** Chapter 07 was explicit: *certified* only if a certificate exists; *aligned* for framework tracking; *compliant* usually avoided outside legal review. The related-documents section names frameworks with versions.
- **The analyst's scratch-pad is a distinct section** (clearly separated from the AUP body, not part of the policy) covering the sections the analyst expects the consultation to substantively rework, the least-confident requirements, any sensitive-item flag, and any class-4 escalation candidate.
- **No fabricated statutes, no fabricated case law, no fabricated regulator enforcement precedents.** The AUP cites what exists; it does not invent enforcement.
- **The analyst's role in the routing chain is *first-cut author* only.** The document does not read as if the analyst intends to ratify, sign, or enforce.

## Starter guidance

- Read EU AI Act Article 5 directly before drafting the prohibited-use list. The list should mirror the article's structure, not paraphrase it into something looser. Chapter 06 was explicit that this is a common first-cut miss.
- Draft the routing header first, then the Definitions section, then the Requirements section, then the surrounding sections. The Definitions section anchors the language the Requirements use; drafting Requirements first often produces terms the analyst has to go back and define.
- For the Definitions section, cross-reference to `mod-101` and to the AIGP body of knowledge where the term is defined there. Chapter 06 was explicit that duplicating a definition that exists elsewhere in the policy library introduces drift; cross-reference instead.
- Keep the tone formal but readable. The AUP is read by every employee; a first-cut written in only-lawyer-legible language is one the consultation phase will strip and rewrite. Chapter 06 was explicit that the guidance (chapter 06 fourth canonical draft) is the *plain-language* companion — the AUP itself is a policy, but a policy read by non-lawyers.
- For the Requirements section, aim for a total of 12 to 18 numbered requirements across permitted / restricted / prohibited. Fewer is under-scoped for an enterprise-wide AUP; more starts to bleed into standard-level detail.
- For the Restricted-use section, name the *condition* specifically. *"Restricted use — human oversight required"* is not a condition; *"human oversight required, with documented approval and review per the model-approval standard section [n]"* is.
- For the Prohibited-use section, note that chapter 06 also identified the *"employees may not use AI systems for purposes prohibited under EU AI Act Article 5"* requirement as one of the enterprise's own *prohibited-AI-use* register additions. The analyst layers enterprise-specific prohibitions on top of Article 5 (e.g., prohibition on using generative-AI to produce material for regulatory filings without legal review; prohibition on using AI-generated code in specific security-critical modules) as the enterprise's context warrants.
- For the Exceptions section, the *prohibited-use requirements are not subject to exception under the AUP* line is load-bearing. Chapter 06's exception discipline distinguishes standard-level exceptions (routine) from policy-level exceptions (escalated) and treats prohibited-use as a further-restricted category. Do not allow the AUP's own exception process to swallow the prohibitions.
- For the Enforcement section, do not restate the disciplinary policy. Chapter 06 was explicit that the policy library's other documents own their content; the AUP cross-references. If the AUP starts to look like it is trying to be a disciplinary policy in addition, level confusion has crept in.
- For the Related documents section, chapter 07's vocabulary discipline applies. The frameworks are named with versions, cited as *aligned with*, not *compliant with*. Statutes are cited with their instrument number where applicable.
- Do not draft the model-approval standard, the third-party AI vendor review standard, or the generative-AI employee guidance in the same file. The AUP references them; they are separate first-cut drafts. Chapter 06 was explicit that the four canonical drafts are separate documents in separate positions in the policy library.
- For the analyst's scratch-pad, be honest. Naming the sections the analyst expects the consultation to substantively rework is not a weakness; it is the routing chain functioning as designed. Chapter 06 was explicit that the consultation phase is where the draft gets its cross-functional legitimacy.
- If your enterprise context differs from the assumed profile (US-only, or public-sector, or a professional-services partnership), substitute the details at the top and adjust the Related documents accordingly. Chapter 06 was explicit that policies are enterprise-specific; a template adopted verbatim will not survive first council pass.

## Acceptance criteria

- Single file `mod-110-ex-03-aup-first-cut.md` filed.
- Routing header present, populated, routing state = *first-cut*, analyst named as first-cut author.
- All nine universal-shape sections present with substantive content.
- Length within 3 to 5 pages.
- Requirements section has 12 to 18 numbered requirements across permitted / restricted / prohibited, with the specific shape called out (at least 3 permitted, at least 5 restricted with specific conditions, at least 4 prohibited).
- Prohibited-use list mirrors EU AI Act Article 5 explicitly and cites the article.
- Exception process is present, with named routing (standard-level to architect, policy-level to head of governance), named recording (`EXC-<year>-<sequence>`), no self-approved exceptions, review cadence on council standing agenda, and the explicit *prohibited-use requirements not subject to exception* position.
- Related documents section cites internal policies (Code of Conduct, IT AUP, Data Protection Policy, model-approval standard, third-party vendor review standard, generative-AI employee guidance, incident response policy) and external frameworks (ISO/IEC 42001:2023, ISO/IEC 38507:2022, NIST AI RMF 1.0, EU AI Act, UK Equality Act 2010, UK GDPR, EU GDPR) with versions and instrument numbers where applicable, applying chapter 07's *aligned with* vocabulary discipline.
- The document is at policy-level (categories, not tools; statements of intent and requirement, not step-by-step procedures).
- Analyst's scratch-pad section is present, clearly separated from the AUP body, 200 to 400 words, covering expected consultation-phase edits, least-confident requirements, sensitive-item flags, and class-4 escalation candidates.
- No fabricated statutes, case law, or enforcement precedents.
- The analyst is named as first-cut author only, not as ratifier / signer / enforcer.

## Stretch goals

- **A first-cut generative-AI employee guidance draft.** In a second file `mod-110-ex-03-genai-guidance-first-cut.md`, draft the plain-language guidance companion per chapter 06's fourth canonical draft anchor content. The guidance should exercise the *"you"* and *"we"* voice, the common-scenarios structure, and the explicit *non-normative* effect. This exercises chapter 06's level-4 vocabulary — guidance, not policy.
- **A first-cut model-approval standard draft.** In a third file `mod-110-ex-03-model-approval-standard-first-cut.md`, draft the model-approval standard per chapter 06's second canonical draft anchor content. This exercises chapter 06's standard-level vocabulary and the prescriptive-requirements-with-lifecycle-gates structure.
- **A first-cut third-party AI vendor review standard draft.** In a fourth file `mod-110-ex-03-vendor-review-standard-first-cut.md`, draft the third-party AI vendor review standard per chapter 06's third canonical draft, closing the free-tier / trial-vendor gap explicitly. This exercises chapter 06's standard-level vocabulary and the vendor-lifecycle-and-contract-clauses structure.
- **The consultation-tracker artefact.** In a fifth file `mod-110-ex-03-consultation-tracker.md`, draft the consultation-tracker for the AUP first cut — the analyst's own tracking artefact for the M − 10 to M day cadence of the consultation phase. For each named contributor role, the tracker carries the requested-input due date, the received date, the sign-off status, and any dissent-with-resolution. Chapter 06 was explicit that silent sign-off is a failure mode; the tracker is what prevents it.
- **The class-4 pattern-recognition memo.** In a sixth file `mod-110-ex-03-class-4-memo.md`, draft the class-4 pattern-recognition memo the analyst would compose if the AUP first-cut consultation surfaces a recurring pattern (e.g., repeated privacy-office pushback on the restricted-use language for worker-facing systems, suggesting the underlying restricted-use category is misspecified). Chapter 09 was explicit that the class-4 memo is where the analyst's first-cut drafting voice meets the analyst's council packaging voice.

## Deliverables

- `mod-110-ex-03-aup-first-cut.md` — the AUP first-cut draft with routing header, universal-shape sections, and analyst's scratch-pad.
- Optional stretch files named per the stretch-goals list.

## Notes on evaluation

The paired solutions repo works one reference AUP first-cut. The load-bearing calls your draft is expected to match: (a) the routing header is present with routing state = *first-cut* and analyst named as first-cut author; (b) all nine universal-shape sections are present with substantive content; (c) the document is at policy-level (categories, not tools; intent and requirement, not step-by-step procedures); (d) 12 to 18 numbered requirements across permitted / restricted / prohibited; (e) the prohibited-use list mirrors EU AI Act Article 5 explicitly and cites the article; (f) the exception process is present with named routing, recording, review cadence, and the prohibited-use-not-subject-to-exception position; (g) the related documents section cites the specific internal and external references applying chapter 07's *aligned with* vocabulary discipline; (h) the analyst's scratch-pad section is present and honest; (i) no fabricated statutes or enforcement precedents. The narrower calls — the specific enterprise-specific prohibitions, the specific business-line requirements, the specific consultation-contributor names — will differ per your worked-artefacts context. What should not differ is the level discipline, the routing chain, the Article 5 mirroring, and the exception-process shape. A tight first-cut at the correct level beats a longer first-cut that drifts to standard-level or that omits the Article 5 mirror or the exception process.
