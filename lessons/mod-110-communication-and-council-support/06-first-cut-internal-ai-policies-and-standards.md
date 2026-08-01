# Drafting First-Cut Internal AI Policies and Standards

## Why this chapter

The enterprise's AI governance program lives in artefacts (the modules before this one produced them) and in *policies* the artefacts operate against. The policy layer is what tells an employee whether they can paste customer data into a public chatbot; tells a PM whether a new agentic feature needs a formal model-approval step before launch; tells a vendor manager which contract terms to require of a foundation-model provider; tells `head-of-ai-governance` what to ratify when the risk-appetite statement changes.

Those policies do not descend from head office as a finished product. Somebody writes a first cut, someone senior edits it, and the accountable executive ratifies it into the enterprise's policy library. In an enterprise with a working `ai-governance-analyst` on staff, the *first cut* is the analyst's work. The senior architect edits; the head of governance ratifies. That routing is the module's spine.

This chapter walks the four canonical first-cut drafts the analyst is expected to originate:

- The **acceptable-use policy (AUP)** — the enterprise-wide, employee-facing statement of what AI use is permitted, what is restricted, and what is prohibited.
- The **model-approval standard** — the internal standard that operationalises how a new AI system passes from concept through intake, assessment, approval, and post-deployment monitoring.
- The **third-party AI vendor review standard** — the internal standard that operationalises the vendor-and-model intake work `mod-108` chapter 06 walked, at the standard level required for procurement, legal, and security to align.
- The **generative-AI employee guidance** — the plain-language, non-normative companion to the AUP that helps employees act consistently with policy without imposing enforceable requirements the AUP does not already carry.

It also fixes the vocabulary distinction between policy, standard, and guidance; the routing chain; and the versioning and consultation discipline the drafts move through.

## Policy vs standard vs guidance vs procedure

The enterprise's policy library has an internal hierarchy. Confusing the four levels is the most common failure of a first-cut draft, because each level has different scope, different length, different tone, different ratification authority, and different audience.

| Level | What it is | Length | Ratifier | Audience |
|---|---|---|---|---|
| Policy | Enterprise-wide statement of intent — *what the enterprise commits to and requires*. High-altitude. Rarely changes. | 1–5 pages | Board or C-level executive (varies by enterprise) | All employees, all systems, all vendors |
| Standard | Normative requirement that operationalises a policy — *what specifically must be done to satisfy the policy*. Mid-altitude. Changes yearly or so. | 5–20 pages | `head-of-ai-governance` or the enterprise's equivalent AI-accountable executive | Named practitioner audiences (developers, PMs, vendor managers, incident responders) |
| Guidance | Non-normative recommendation for a named audience — *how you should typically act consistently with policy and standards*. Plain language. Changes as needed. | 2–10 pages | `head-of-ai-governance` (usually a lighter ratification path than a standard) | A named employee audience (all-employees, engineers, sales, HR, etc.) |
| Procedure | Step-by-step operational instructions — *the exact steps to complete a specific task*. Prescriptive. Changes with tooling. | Any length | The team that operates it | The team that operates it |

The analyst-owned first-cut drafts sit at policy, standard, and guidance levels. Procedures typically belong to the team that runs the underlying tooling — the analyst may write the procedure for the analyst's own workflow (the pre-read cadence in chapter 04, for example) but does not usually originate procedures for engineering, security, or legal functions.

**A tell for level confusion.** If the first-cut draft of an *acceptable-use policy* contains *"install version 3.2.1 of the enterprise browser extension and configure setting X = Y"*, the draft is doing procedure work — it belongs in a standard or a companion procedure, not in the policy. Conversely, if a first-cut draft of a *standard* contains only high-altitude statements of intent — *"the enterprise commits to responsible AI use"* — the draft is doing policy work; the standard needs to be more prescriptive.

## The routing chain

Every first-cut draft moves through a routing chain the analyst manages explicitly on the document itself. The chain has four named phases; each phase has an owner, an entrance criterion, and an exit criterion.

| Phase | Owner | Enters when | Exits when |
|---|---|---|---|
| First-cut draft | `ai-governance-analyst` | The council or `head-of-ai-governance` has commissioned the draft (or the analyst has proposed a new draft on standing-agenda item 8 per chapter 04 and had it accepted) | The analyst has completed a self-review against the checklist below and named the draft as *ready for architect edits* on the routing header |
| Architect edits | `senior-ai-governance-architect` | The first-cut is on the routing header as *ready for architect edits* | The architect has completed edits and named the draft as *ready for consultation* on the routing header |
| Cross-functional consultation | `senior-ai-governance-architect` (running) + named contributors from `legal`, `privacy`, `security`, `HR`, `procurement`, business lines | The architect has released the draft for consultation | The named contributors have signed off (or the architect has documented dissent and its resolution) and the draft is on the routing header as *ready for ratification* |
| Ratification | `head-of-ai-governance` or the enterprise's policy-approval workflow authority | The consultation is complete and the draft is *ready for ratification* | The ratifier has approved (or returned for revisions); if approved, the draft moves into the enterprise's policy library with the ratification date, the ratifier's name, and the version identifier |

The analyst maintains a *routing header* at the top of every draft document. A minimal shape:

```
Document: [Policy / Standard / Guidance]  ·  Title  ·  Version: 0.3 draft
Routing state: [first-cut / architect-edits / consultation / ratification / ratified]
First-cut author: [analyst name] — [YYYY-MM-DD]
Architect editor: [senior-architect name] — [YYYY-MM-DD] — status: [in-flight / complete]
Consultation contributors: [named roles]  ·  status per contributor: [in-flight / signed off]
Ratifier: [role] — [YYYY-MM-DD if ratified] — status: [pending / approved / returned]
Supersedes: [prior version link, if this is a re-issue]
Effective date: [YYYY-MM-DD, set at ratification]
Next scheduled review: [YYYY-MM-DD]
```

The routing header is the analyst's discipline; it means an auditor, a member of council, or a subsequent editor can pick up the draft cold and know exactly where it is in its ratification path.

## Universal shape for all four drafts

Every policy, standard, and guidance document the analyst originates carries the following sections. The section content differs; the section presence does not.

- **Purpose.** One paragraph. What the document is for and what it is not for.
- **Scope.** One paragraph. Who and what the document applies to (systems, roles, jurisdictions, data types). Where the scope has explicit exclusions, they are named.
- **Definitions.** A short glossary of any term the document uses whose meaning is not obvious. Cross-references to the AIGP body of knowledge (chapter 08) or to `mod-101`'s vocabulary where the term is defined there.
- **Requirements (for policy and standard) or recommendations (for guidance).** The substantive body. Numbered so downstream audits and controls can cite them.
- **Roles and responsibilities.** Who does what to comply with the document. Names roles, not individuals.
- **Exceptions and waivers.** How an exception is requested, who approves, and how the exception is recorded (typically as an `EXC-<year>-<sequence>` in the GRC platform).
- **Enforcement (for policy and standard) or effect (for guidance).** For policy and standard, the consequences of non-compliance and where the enforcement authority sits. For guidance, the (non-enforcement) statement that the document is non-normative and that non-compliance does not by itself constitute a violation.
- **Related documents.** Cross-references to other policies, standards, guidance, standards frameworks (ISO/IEC 42001, NIST AI RMF), statutes (EU AI Act, GDPR, US-state statutes), and enterprise artefacts.
- **Revision history.** Version, date, author, summary of change. Superseded versions link forward to the current one.

## The four canonical first-cut drafts

### 1. Acceptable-use policy (AUP)

**What it is.** The enterprise-wide, employee-facing policy that names what AI use is permitted (approved-and-sanctioned systems for approved-and-sanctioned purposes), what is restricted (permitted subject to conditions and audit), and what is prohibited (prohibited outright — the enterprise's own *prohibited-AI-use* register, which parallels the EU AI Act's Article 5 prohibitions with enterprise-specific additions).

**Length.** 3 to 5 pages. Policies that run longer than this stop being read.

**Anchor content per section.**

- *Purpose.* States the enterprise's commitment to responsible, lawful, and human-oversighted AI use. One paragraph.
- *Scope.* All employees, contractors, and consultants operating on enterprise infrastructure or with enterprise data or on the enterprise's behalf. All AI systems the enterprise builds, procures, or uses. Named jurisdictions if the enterprise operates multi-jurisdictionally.
- *Requirements.* Numbered requirements grouped as *permitted uses*, *restricted uses (permitted-with-conditions)*, and *prohibited uses*. Example requirements:
  - *Permitted-1.* Employees may use enterprise-sanctioned AI tools for the purposes documented in the tool's model card (`mod-105`).
  - *Restricted-1.* Employees may not enter customer personal data into any AI tool not on the enterprise's approved-AI-tools list (`mod-102` inventory). Restricted uses require sign-off per the model-approval standard.
  - *Prohibited-1.* Employees may not use AI systems to make final decisions on hiring, termination, credit, or benefits eligibility without documented human oversight per the EU AI Act Article 14 human-oversight requirements for high-risk systems in the enterprise's inventory.
  - *Prohibited-2.* Employees may not use AI systems for purposes prohibited under EU AI Act Article 5 (social scoring, real-time remote biometric identification in public spaces except under the article's narrow exceptions, emotion recognition in the workplace or educational institutions except under the article's exceptions, etc.).
- *Roles.* Every employee (compliance); managers (oversight); `ai-governance-analyst` (intake and register); `senior-ai-governance-architect` (standards); `head-of-ai-governance` (ratification and exception approval); `legal` and `HR` (enforcement).
- *Exceptions.* An exception form and the approval authority; typical routing is `senior-ai-governance-architect` for standard-level exceptions and `head-of-ai-governance` for policy-level exceptions.
- *Enforcement.* HR consequence framework by reference to the enterprise's disciplinary policy; regulator, contract, and legal-exposure consequences by reference to the enterprise's legal policy.

**Common first-cut failure modes.**

- *Policy language reads like a standard.* Fix: strip out the operational detail (version numbers, tool names, configuration settings). The AUP names *categories*, not *tools*. The list of approved tools lives in the inventory (`mod-102`), not in the policy.
- *Prohibited-use list is silent on EU AI Act Article 5.* Fix: mirror Article 5 in the prohibited-use list, with enterprise-specific additions layered on. This ties the policy to the statute the enterprise is anyway obliged to comply with.
- *No exception process.* Fix: every policy needs an exception process because every policy has legitimate exceptions; a policy with no path for exceptions gets ignored rather than followed.

### 2. Model-approval standard

**What it is.** The internal standard that operationalises how a new AI system moves from concept through intake, assessment, approval, and post-deployment monitoring — the operational spine of `mod-102` (intake), `mod-103` (risk), `mod-104` (fairness), `mod-105` (impact assessment), `mod-107` (release-assurance eval evidence), and `mod-108` (controls) at the *this-is-what-you-shall-do* altitude.

**Length.** 10 to 20 pages, typically. Standards are longer than policies because they are prescriptive.

**Anchor content.**

- *Purpose.* Operationalise the AUP by defining the mandatory gates every AI system passes through before deployment and the mandatory monitoring after deployment.
- *Scope.* Every AI system in the enterprise's `mod-102` inventory. Standard applies uniformly across teams; exceptions require a documented waiver.
- *Requirements* (numbered, testable):
  - Intake (mandatory `INV-<year>-<sequence>` inventory row before development starts).
  - Tiering (per the enterprise's tiering methodology, referencing EU AI Act Article 6 and Annex III where applicable).
  - Risk assessment (`mod-103`, mandatory register entry, threshold for council-attention).
  - Fairness review where the system's inventory row indicates human-adjacent decisions (`mod-104`).
  - Impact assessment (`mod-105`, mandatory `IA-`, `FRIA-`, or `DPIA-` per the tiering and jurisdiction).
  - Release-assurance eval evidence (`mod-107`).
  - Controls in place per the control library (`mod-108`, cross-referenced by control ID).
  - Council sign-off where required by the tiering (chapter 04 above).
  - Post-deployment monitoring plan (`mod-109`, cross-referenced by monitoring-plan ID).
- *Roles.* Product / engineering (owns the system and the intake); `ai-governance-analyst` (runs the intake, opens the register, tracks assessments to sign-off); `ai-eval-engineer` and `ai-risk-engineer` (produce the eval and risk artefacts); `senior-ai-governance-architect` (approves methodology deviations); `head-of-ai-governance` and the AI governance council (sign-off for high-risk).
- *Exceptions.* Waiver process — waivers are named, scoped, dated, and time-limited; waivers above the enterprise's threshold require council endorsement.
- *Enforcement.* Systems that skip a mandatory gate are un-approved by definition; deployment of un-approved systems is a policy violation.

**Common first-cut failure modes.**

- *Standard tries to be exhaustive.* Fix: standards describe *what*, not *how in detail*. Detail belongs in the procedures the operational teams write.
- *Standard omits the post-deployment plan.* Fix: model approval that stops at pre-deployment gates is a pre-deployment discipline, not a model-approval discipline. The standard covers the whole lifecycle.
- *Standard has no waiver process.* Fix: same reason as the AUP — waivers exist; the standard governs them.

### 3. Third-party AI vendor review standard

**What it is.** The internal standard that operationalises `mod-108` chapter 06 (vendor and model intake) at the *this-is-what-you-shall-do* altitude for procurement, legal, security, and the analyst. It ties the vendor-risk-register row (`VND-<year>-<sequence>`) to the enterprise's procurement, contracting, and vendor-lifecycle workflows.

**Length.** 8 to 15 pages.

**Anchor content.**

- *Purpose.* Ensure every third-party AI vendor, model, and dataset the enterprise procures or integrates has been assessed at a consistent level of rigour before contract execution, and that the vendor-risk-register carries the artefacts the enterprise's ongoing assurance depends on.
- *Scope.* All third-party AI vendors, foundation-model providers, model-serving providers, retrieval-source providers, and dataset vendors the enterprise integrates with. Also *free-tier* and *trial* vendors — a common gap; the standard closes it explicitly.
- *Requirements.*
  - Vendor row (`VND-<year>-<sequence>`) opened at first evaluation, populated before contract execution.
  - Vendor-supplied artefacts required: model card (or equivalent documentation), sub-processor list, DPA (where personal data is in scope), ISO/IEC 42001 certification letter (or a documented alternative and its rationale), independent audit report (SOC 2, ISAE 3000, or the equivalent for the vendor's jurisdiction), security questionnaire response.
  - Contract clause requirements: the enterprise's mandatory AI-specific contract clauses (data-use, model-change notification, audit-right, incident-notification, exit-and-portability, sub-processor consent, applicable-jurisdiction). Named per clause; the enterprise's contract-clause library owns the exact text.
  - Ongoing review cadence: annual re-assessment; on-trigger re-assessment (major model update by the vendor, incident, change of ownership, expiring certification).
  - Deprecation and exit plan: how the enterprise unwinds the integration if the vendor's posture becomes unacceptable.
- *Roles.* `procurement` (owns the contract lifecycle); `legal` (contract clauses); `security` (security questionnaire and pen-test posture); `ai-governance-analyst` (vendor-risk-register row and artefact assembly); `senior-ai-governance-architect` (methodology and clause-library ownership).
- *Exceptions.* Waivers for missing vendor-supplied artefacts (e.g., a vendor that does not have ISO/IEC 42001 certification yet) with time-boxed remediation dates.
- *Enforcement.* Vendors that do not meet the standard are not integrated; the standard is a pre-contract gate.

**Common first-cut failure modes.**

- *Standard omits the free-tier / trial vendor case.* Fix: name it explicitly — the analyst has seen too many enterprises whose *"we don't have any generative-AI vendors"* audit response was falsified by an engineer's ChatGPT Plus subscription.
- *Standard names artefacts but not the contract clauses.* Fix: artefacts alone do not create ongoing enterprise leverage; contract clauses do. The two co-exist.

### 4. Generative-AI employee guidance

**What it is.** The plain-language companion to the AUP that tells an ordinary employee — who is not a developer, not a governance specialist, not a security engineer — *how* to use generative-AI tools in day-to-day work consistently with the AUP.

**Length.** 2 to 6 pages. Guidance is meant to be read.

**Anchor content.**

- *Purpose.* Help employees make good day-to-day decisions about generative-AI use without having to read the AUP end-to-end.
- *Scope.* All employees. Non-normative.
- *Recommendations.* Practical, phrased in employee language:
  - *"Do use the enterprise-sanctioned generative-AI tools on the approved-tools list [link] for tasks like drafting internal communication, summarising publicly available reference material, and brainstorming."*
  - *"Do not paste customer names, contact details, financial information, or other personal data into any generative-AI tool that is not on the approved-tools list."*
  - *"Do check any generative-AI output that will reach a customer, a supplier, a regulator, or a public audience — the enterprise's accuracy standards apply to AI-assisted work exactly as they apply to human work."*
  - *"Do report incidents where a generative-AI output surprised you or produced inaccurate, biased, or unsafe content — the intake form is [link]."*
  - *"If unsure whether a use is permitted, ask [team / mailbox] — asking never puts you in the wrong."*
- *Common scenarios.* A short set of worked examples — a marketing copy request, a customer-email summarisation, a code-completion use, a data-analysis use — with the recommended approach.
- *Roles.* All employees (readers); `HR` and the enterprise's L&D function (distributors); `ai-governance-analyst` (author of the guidance and the intake mailbox owner).
- *Effect.* Explicitly non-normative — the guidance is a good-faith aid, and non-compliance with the guidance is not by itself a policy violation; the AUP defines the enforceable requirements.

**Common first-cut failure modes.**

- *Guidance reads like a legal document.* Fix: cut the passive voice, cut the *"employees shall"* language, use *"you"* and *"we"*. Guidance is meant to be read, not obeyed.
- *Guidance conflicts with the AUP.* Fix: whenever the AUP and the guidance say different things about the same case, the AUP wins; the analyst reconciles by editing the guidance rather than by adding qualifiers.

## Cross-functional consultation discipline

The consultation phase — architect-owned, analyst-supported — is where the draft gets its cross-functional legitimacy. Named contributors typically include:

| Contributor | What they look for |
|---|---|
| `legal` | Contract-clause language, regulator-interpretation risk, enforceability, statutory alignment (EU AI Act, GDPR, US-state statutes) |
| `privacy` / DPO | Lawful-basis, data-flow, transparency-notice, cross-border transfer, DPIA-trigger implications |
| `security` | Threat-taxonomy alignment (OWASP LLM Top 10, MITRE ATLAS, NIST AI 100-2, Google SAIF), incident-integration, control-set implications |
| `HR` | Employment-law implications of any AUP or guidance that touches worker monitoring, hiring, or performance |
| `procurement` | Vendor-lifecycle integration for the third-party standard |
| Business lines | Operational feasibility — do the requirements actually work in the operations they cover? |

The analyst tracks consultation by contributor and by section — a signed-off consultation checklist on the routing header. Silent sign-off (a contributor never responded, so the analyst assumes agreement) is a failure mode; the analyst chases explicitly and, where a contributor declines to sign, files the declination in the routing history.

## Version discipline

- **Version numbers are semantic-adjacent.** `0.x` = pre-ratification drafts. `1.0` = first ratified version. `1.1`, `1.2`, ... = ratified minor changes (clarifications, editorial). `2.0` = ratified major change (substantive scope or requirement change). Version bumps at ratification, not on the analyst's desk.
- **Supersession is explicit.** A new version supersedes the prior version's effective date and cross-references it in the revision history. The prior version stays in the library for reference; it is not deleted.
- **Effective dates are set at ratification.** The ratifier sets the date; the analyst does not.
- **Next-review dates are mandatory.** Every ratified document has a *next scheduled review* date. The analyst tracks these and puts pending reviews on the council's standing agenda (chapter 04 item 8).

## What to memorise

- **Four canonical first-cut drafts.** AUP, model-approval standard, third-party AI vendor review standard, generative-AI employee guidance.
- **Policy vs standard vs guidance vs procedure — get the level right before drafting.** Level confusion is the most common failure of a first-cut.
- **Routing chain: analyst → senior architect → cross-functional consultation → head of governance ratification.** Track it on the document's routing header.
- **Universal shape: purpose, scope, definitions, requirements (or recommendations), roles, exceptions, enforcement (or effect), related documents, revision history.**
- **Consultation is architect-owned and analyst-supported.** Silent sign-off is a failure; chase explicitly.
- **Versioning is semantic-adjacent, supersession is explicit, next-review dates are mandatory.**

## Summary

The analyst originates the first-cut drafts the enterprise's AI policy library depends on. Four canonical drafts sit under the analyst's originating role: the acceptable-use policy, the model-approval standard, the third-party AI vendor review standard, and the generative-AI employee guidance. Each carries the universal shape (purpose, scope, definitions, requirements, roles, exceptions, enforcement, related documents, revision history) and moves through the same four-phase routing chain — first-cut, architect edits, cross-functional consultation, ratification — with the routing state visible on the document header. The analyst does not ratify, does not sign the contract, and does not enforce; the head of governance ratifies, procurement and legal sign contracts, HR enforces. Chapter 07 turns to the small but consequential piece of external-facing communication the analyst contributes to under legal and executive review.
