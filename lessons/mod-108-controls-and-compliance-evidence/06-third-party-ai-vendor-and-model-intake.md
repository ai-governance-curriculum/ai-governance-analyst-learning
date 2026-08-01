# Third-Party AI Vendor, Model, and Dataset Intake

## Why this chapter

Most AI systems the analyst inventories are not built end-to-end inside the enterprise. They embed a hosted foundation model (OpenAI, Anthropic, Google, Azure OpenAI, AWS Bedrock, Mistral, Cohere, IBM watsonx), a self-hosted open-weights model taken from a public source (a Hugging Face release, a Meta Llama release, a Mistral release, a DeepSeek release), a licensed or public dataset, an evaluation vendor's tooling, a bias-audit vendor's engagement, or a monitoring vendor's platform. Each of those is a third-party dependency; each carries risks the enterprise inherits by using it.

This chapter fixes the second headline deliverable of the module: the *vendor-risk-register row*. The row is what the vendor-management office reads to decide renewal vs off-boarding, what `procurement` and `legal` reference in the contract file, and what `internal-audit` reads to trace the residual-risk claims on a downstream `mod-102` inventory row back to their upstream vendor evidence.

The analyst does not sign the contract, negotiate the DPA, or issue the letter of engagement. What the analyst *does* is read the vendor's published evidence and questionnaire responses, produce the row with a residual-risk assessment and an inheritance decision, hand the row to the vendor-management office, and re-review on the cadence set by the master control library.

## The six vendor-evidence artefacts

Every vendor intake looks at the same six artefact classes. Not every vendor produces all six; the row records which are present, which are missing, and which were requested and refused.

### 1. Model card (or system card)

A public document describing the model — what it is, how it was trained, what it was evaluated on, what it should and should not be used for.

- **Where it lives.** For hosted foundation models, on the vendor's site (e.g., [OpenAI's system-card page](https://openai.com/index/gpt-4o-system-card/) for the current GPT-4o release, [Anthropic's model-card and add-ons](https://www.anthropic.com/news) index for Claude releases, [Google DeepMind's Gemini technical report](https://deepmind.google/technologies/gemini/), [Meta's Llama model cards](https://ai.meta.com/blog/) per release, [Mistral's model cards](https://mistral.ai/technology/#models)). For self-hosted models pulled from Hugging Face, on the model's repository page. For datasets, in a datasheet-style companion or in a licensing README.
- **What to read for.** Intended use; out-of-scope use; training-data description; evaluation coverage; known limitations; safety-evaluation coverage.
- **What the analyst records.** URL + version-of-record; the release date; the analyst-tier summary — one sentence per intended-use, out-of-scope, and known-limitation.
- **Failure modes.** Vendor did not publish a model card, or the model card is a marketing page rather than a Mitchell-shaped card (per `mod-105` chapter 06). Record *no-model-card* or *marketing-only card* on the row and treat as a residual-risk contributor.

### 2. Sub-processor list

For any vendor that processes personal data on behalf of the enterprise, the list of downstream sub-processors the vendor engages — cloud providers, data-labelling contractors, model-training partners, third-party API dependencies.

- **Where it lives.** Vendor's trust site (typical URLs: `/trust`, `/subprocessors`, `/legal/subprocessors`); DPA appendix.
- **What to read for.** Complete list of named sub-processors with location; notification obligation the vendor commits to when adding a new sub-processor; any objection right the enterprise has.
- **What the analyst records.** Snapshot date; list length; whether any sub-processor is in a jurisdiction that changes the enterprise's data-transfer posture (e.g., new sub-processor in a jurisdiction outside the enterprise's approved transfer footprint).
- **Failure modes.** No published list; list is incomplete or vague ("*and other regional cloud providers*"). Record and escalate to `data-protection-officer`.

### 3. Data-processing agreement (DPA)

The contractual instrument that binds the vendor to specific data-protection obligations when processing personal data on the enterprise's behalf — for GDPR-scoped work, an Article 28 processor agreement; for jurisdictions with similar processor obligations, the local equivalent.

- **Where it lives.** In the vendor's contract file, held by `procurement` / `legal`. Public boilerplate versions are often on the vendor's trust site (e.g., a downloadable draft DPA).
- **What to read for.** The scope of processing; the purposes; the categories of personal data and data subjects; the sub-processor terms (references item 2); the transfer mechanism used (Standard Contractual Clauses, adequacy decision, Data Privacy Framework certification); the audit rights the enterprise retains; the notification obligations on breach.
- **What the analyst records.** DPA version + effective date; the transfer mechanism named; the audit right named; any material deviation from the enterprise's model DPA position that `legal` accepted.
- **Failure modes.** DPA not in place, DPA outdated (e.g., pre-Schrems-II with no updated SCCs), vendor accepts only their own DPA with no negotiated terms. The analyst records; `legal` decides.
- **Delegation note.** The analyst reads the DPA to summarise its shape onto the row; `legal` and `data-protection-officer` decide whether the terms are acceptable. The analyst does not redline.

### 4. ISO/IEC 42001 certification letter (or comparable AI management system attestation)

Where the vendor claims certification against [ISO/IEC 42001](https://www.iso.org/standard/81230.html) (AI management system) or a comparable AI-focused management-system attestation, the *certification letter* is the artefact — issued by an accredited certification body, dated, naming the scope of the certification and the certification-body accreditation.

- **Where it lives.** Vendor's trust site; on request from the vendor's compliance team; via a shared trust portal (Whistic, Vanta, Drata, OneTrust, SecurityScorecard trust pages).
- **What to read for.** The certifying body's name and its accreditation (the certifying body must itself be accredited by a national accreditation body signatory to the IAF Multilateral Recognition Arrangement); the scope of the certification (which entities, which processes, which locations — not always the whole of the vendor); the effective and expiry dates; any qualifications or limitations noted.
- **What the analyst records.** Certifying body + accreditation; scope statement; effective / expiry; any qualifications; the URL or portal identifier where the letter can be retrieved.
- **Failure modes.** No certification, certification scope excludes the specific service the enterprise uses, certifying body is not accredited (a "*certification*" from an unaccredited entity is not equivalent), expired certification. Record on the row.
- **Adjacent attestations to note.** [ISO/IEC 27001](https://www.iso.org/standard/27001) (information-security management system — near-universal), [ISO/IEC 27701](https://www.iso.org/standard/71670.html) (privacy information management), [SOC 2 Type II](https://us.aicpa.org/interestareas/frc/assuranceadvisoryservices/aicpasoc2report) reports (US-audit-firm-issued security / availability / processing-integrity / confidentiality / privacy attestation), [ISO/IEC 42005](https://www.iso.org/standard/44545.html) (AI system impact assessment — process reference used per `mod-105`). These are common; ISO/IEC 42001 is the analyst's headline AI-specific attestation.

<!-- needs-research: ISO/IEC 42001 has been publicly available since December 2023; the analyst-visible certification population is growing but still small as of authoring. Confirm the vendor-side certification claim by requesting the letter and verifying the certifying body's accreditation via the IAF portal or the national accreditation body's site rather than trusting a badge on a vendor page. -->

### 5. Independent audit report

An audit report issued by an accredited external auditor, examining a specific scope against a named framework, producing an opinion the enterprise can rely on.

- **Where it lives.** SOC 2 reports typically under NDA on the vendor's trust portal; ForHumanity-independent audit reports (chapter 08) on the vendor's site or the [ForHumanity Charity index](https://forhumanity.center/) once published; bias-audit reports (NYC Local Law 144-style) publicly linked from the vendor's site.
- **What to read for.** The auditor's identity and accreditation; the scope and boundaries of the audit; the period covered; the framework the audit examines against; the opinion issued; the exceptions or qualifications noted; the management response.
- **What the analyst records.** Auditor + credentialing / accreditation; scope; period; framework; opinion; exceptions.
- **Failure modes.** No independent audit; audit scope is a sales one-pager rather than a full engagement; auditor is not accredited; audit opinion is qualified in a way that materially changes the residual-risk assessment. Record on the row.
- **Delegation note.** Chapter 08 covers the two credential bodies most often behind AI-specific independent audits — ForHumanity and BABL AI.

### 6. Security questionnaire response

The vendor's response to the enterprise's own security questionnaire, or their standardised responses to industry questionnaires (CAIQ, SIG, VSA, HECVAT).

- **Where it lives.** In the enterprise's vendor-management platform; on the vendor's trust portal (many vendors publish pre-filled CAIQ / SIG responses).
- **What to read for.** Coverage of the questions the enterprise cares about; consistency with items 1–5 (a questionnaire response claiming ISO/IEC 42001 certification with no supporting letter in item 4 is a red flag); the timestamp on the response.
- **What the analyst records.** Response version + date; the analyst's summary of gaps, inconsistencies, or answers that require follow-up; the routing decision — which of the answers the analyst kept, which are routed to `ai-infra-security` for evaluation, which are routed to `legal` for contract-clause work.
- **Failure modes.** No questionnaire response; response is over a year old; response is inconsistent with the vendor's own published artefacts. Record and open a follow-up with the vendor.

The row records all six artefact classes even for vendors that produce fewer than six. A row that says *no sub-processor list published* is more useful than a row that omits the artefact class altogether.

## The `VND-<year>-<sequence>` vendor-risk-register row

The vendor-risk-register row is the analyst's tangible output per vendor. Analyst-tier row schema (twenty-two columns):

| # | Column | Content |
|---|---|---|
| 1 | Vendor ID | `VND-<year>-<sequence>` — enterprise-assigned |
| 2 | Vendor name | Legal name; corporate parent if different |
| 3 | Dependency class | *hosted-foundation-model*, *self-hosted-model-artefact*, *dataset*, *evaluation-tooling*, *bias-audit-service*, *monitoring-platform*, *other-AI-tooling* |
| 4 | Named artefact | Specific model / dataset / tool / service the enterprise consumes (e.g., "*Anthropic Claude Sonnet 4.5 via Anthropic API*"; "*Meta Llama 3.1 70B weights via Hugging Face*"; "*OpenAI GPT-4o via Azure OpenAI Service*") |
| 5 | Enterprise-side integration | Which `INV-<year>-<sequence>` systems consume the artefact; what surface (API endpoint, deployment platform, offline batch) |
| 6 | Data classification handled | The data classification classes the enterprise sends to the vendor (public, internal, confidential, restricted, personal, special-category — per enterprise convention and `mod-102` intake) |
| 7 | Contract owner | The `procurement` / `legal` owner of the contract file |
| 8 | Technical owner | The `ml-engineer` / `ai-platform-owner` responsible on the enterprise side |
| 9 | Model card | URL + version + summary; or *not-published* |
| 10 | Sub-processor list | URL + snapshot date + summary; or *not-published* / *not-applicable-no-personal-data* |
| 11 | DPA | Version + effective date + transfer mechanism + audit right + material-deviation note; or *not-in-place* / *not-applicable* |
| 12 | ISO/IEC 42001 certification | Body + accreditation + scope + effective + expiry + qualifications; or *not-certified* |
| 13 | Adjacent attestations | ISO/IEC 27001, ISO/IEC 27701, SOC 2 Type II, SOC 2 Type I, others — with body + scope + period |
| 14 | Independent audit report | Auditor + credentialing + scope + period + framework + opinion + exceptions; or *not-conducted* |
| 15 | Security questionnaire | Version + date + gaps summary + routing decisions |
| 16 | OWASP / ATLAS / AI 100-2 / SAIF tags | Any tags relevant from chapters 04 and 05 (e.g., a hosted-model vendor whose model has a documented jailbreak-robustness limitation is tagged *LLM01:2025 — Prompt Injection* on the vendor row) |
| 17 | Residual-risk assessment | Analyst summary: what risk remains after the vendor's controls and the enterprise's compensating controls. One paragraph. |
| 18 | Inheritance decision | *inherit* (accept the vendor's controls; enterprise-side compensating controls minimal), *inherit-with-compensating-controls* (list the enterprise controls needed), *do-not-inherit* (this vendor should not be used until specific gaps close) |
| 19 | Compensating controls | If inherit-with-compensating-controls: the `CTL-<year>-<sequence>` identifiers of the enterprise controls that close the gap |
| 20 | Re-review cadence | Annual as a default; more frequent for High-tier system dependencies; on-event for named triggers (vendor breach, DPA change, new sub-processor, certification lapse) |
| 21 | Last reviewed / Next review | Two dates; on issue of the row and the scheduled next-review |
| 22 | Analyst note | One-paragraph free text — recurring themes, watch-items, unresolved follow-ups |

The row supersedes any earlier vendor row for the same vendor + named-artefact combination. A new model version, a new deployment surface, or a materially changed DPA opens a new row; the previous row is closed with a pointer to the new one.

## The pull sequence

The intake runs in a predictable order per vendor. Deviations are noted on the row.

- **Trigger.** A new vendor dependency is being evaluated (`procurement` initiated), an existing vendor is up for re-review (cadence-driven), or an event has fired (breach, DPA change, sub-processor change, certification lapse).
- **Step 1 — enterprise intake row.** Confirm the `mod-102` inventory rows for systems that consume (or would consume) the vendor artefact. The vendor row is meaningless without knowing which enterprise systems inherit its risks.
- **Step 2 — data classification and DPA scope.** Determine the data classification the enterprise sends. If personal data or special-category personal data is in scope, escalate to `data-protection-officer` for DPA sign-off before other steps proceed.
- **Step 3 — public evidence sweep.** Read the vendor's trust site: model card, sub-processor list, DPA boilerplate, certification letters, published audit reports, any published incident notices.
- **Step 4 — private evidence request.** Request via the vendor's account team any evidence not publicly published — the current ISO/IEC 42001 certification letter, the latest SOC 2 Type II report (under NDA), the current DPA text, the latest security questionnaire response (CAIQ / SIG). Record the request date; record the response.
- **Step 5 — questionnaire consistency check.** Compare the questionnaire response against the public and requested evidence. Flag any inconsistency for `ai-infra-security` and `procurement` follow-up.
- **Step 6 — residual-risk draft.** Write column 17. Do not skip to the inheritance decision without the residual-risk paragraph.
- **Step 7 — compensating-controls draft.** For any gap the enterprise cannot close by relying on the vendor, propose the compensating enterprise-side control(s). Reference existing `CTL-<year>-<sequence>` identifiers where possible; if a new control is needed, flag to `senior-ai-governance-architect`.
- **Step 8 — inheritance decision draft.** Column 18. The analyst drafts; the vendor-management office and `head-of-ai-governance` finalise for high-impact vendors.
- **Step 9 — hand-off.** Ship the row to the vendor-management office; copy `procurement`, `legal`, `data-protection-officer`, and `ai-infra-security` on the routings that apply to each.
- **Step 10 — cadence.** Set the next-review date. Close the row for the current period.

## Hosted-foundation-model vendors vs self-hosted-model artefacts vs datasets

The row schema is the same across dependency classes; the readings and the risk emphases shift.

- **Hosted foundation model.** Emphasis on DPA, sub-processor list, ISO/IEC 42001 certification, the vendor's own eval and safety-evaluation coverage (via system card and Responsible Scaling Policy / Preparedness Framework disclosure — per `mod-107` chapters 06–07), the model-version change protocol the vendor operates, the deprecation policy. Data-flow considerations: does the vendor use enterprise inputs for training? What is the retention on prompts and completions? Is there an enterprise-tier that guarantees no training use (e.g., Azure OpenAI, AWS Bedrock, and the enterprise tiers of OpenAI, Anthropic, and Google are the common ones)?
- **Self-hosted-model artefact.** Emphasis on the model card, the training-data description (or its absence), the licence (Meta Llama Community License, Apache 2.0, Mistral non-commercial vs commercial, RAIL, MIT, custom), the provenance of the weight file (upstream URL + verified hash), any adapter / fine-tune the enterprise applies, the supply-chain-scan artefact. DPA is usually not applicable (the enterprise runs the model). Independent audit is usually not applicable (the vendor is the model releaser, not a running service). Sub-processor list is usually not applicable.
- **Dataset.** Emphasis on the datasheet-for-a-dataset (`mod-105` chapter 07), the licence, the copyright and consent posture, the data-subject-rights coverage (where personal data is present), the retraction / take-down protocol the dataset publisher operates.
- **Evaluation tooling / bias-audit service / monitoring platform.** Emphasis on the vendor's own methodology description, their independent-audit posture (a bias-audit service that is not itself independently audited is a governance red flag — chapter 08), and the credentialing of the individuals or teams performing the work.

The analyst's *row shape* is invariant; the *reading emphasis* is calibrated to the dependency class.

## Common failure modes

The intake failures the analyst should watch for.

- **Trust-portal drift.** A vendor's trust portal moves URLs or gates behind a portal login without notice. Fix: record snapshot dates + retrieved-copies of each artefact where terms of use permit; do not rely on a link that could rot.
- **Certification-letter theatre.** A vendor's marketing page claims ISO/IEC 42001 certification with no letter, or with a "*self-attestation*" from an unaccredited body. Fix: request the letter, verify the certifying body against the [IAF Members list](https://iaf.nu/en/iaf-members/); record *unverified* on the row until confirmed.
- **DPA fresh-in-file, stale-in-fact.** The DPA in the contract file has not been updated to reflect changed transfer mechanisms, revised sub-processor terms, or new AI-specific processing purposes. Fix: cross-check DPA version against the vendor's public boilerplate and note any lag.
- **Model card is a marketing page.** The vendor's "*model card*" is a landing page rather than a Mitchell-shaped card. Fix: record *marketing-only card* and treat the missing intended-use / out-of-scope / limitations content as a residual-risk contributor.
- **Sub-processor list without geographic detail.** The vendor lists sub-processors without indicating jurisdictions. Fix: request the jurisdiction detail; escalate to `data-protection-officer` if jurisdictions cannot be established.
- **Inheritance decision without residual-risk paragraph.** The analyst jumps from evidence to *inherit* without writing the residual paragraph. Fix: enforce the row's Step 6 → Step 7 → Step 8 sequence.
- **Missing compensating-controls anchor.** The row says *inherit-with-compensating-controls* but names no `CTL-<year>-<sequence>` identifiers. Fix: at least one control identifier per compensating claim, or a `senior-ai-governance-architect` request for a new control.
- **Vendor rows that never re-review.** The cadence date passes; no one runs the re-review. Fix: the GRC platform's task queue owns the re-review reminder; the analyst does not rely on memory.

## What to memorise

- **Six vendor-evidence artefact classes** — model card, sub-processor list, DPA, ISO/IEC 42001 certification letter, adjacent attestations + independent audit report, security questionnaire response.
- **The `VND-<year>-<sequence>` row is the analyst's headline deliverable per vendor** — twenty-two columns; supersedes prior rows on material change.
- **The intake sequence is ten steps** — from inventory anchor through public sweep, private request, consistency check, residual-risk paragraph, compensating-controls draft, inheritance decision, hand-off, cadence.
- **Inheritance decision is one of three** — *inherit*, *inherit-with-compensating-controls*, *do-not-inherit*. Nothing else.
- **The analyst reads and rows; `procurement` / `legal` / `data-protection-officer` decide.** No redlining, no contract signing, no DPA acceptance.
- **Reading emphasis shifts with dependency class** — hosted foundation model, self-hosted artefact, dataset, tooling — but the row schema is invariant.

## Summary

The vendor-risk-register row is the second headline deliverable of this module. The analyst reads six vendor-evidence artefacts — model card, sub-processor list, DPA, ISO/IEC 42001 certification letter, adjacent attestations plus independent audit report, security questionnaire response — and produces one row per vendor per named artefact per period, following a ten-step intake sequence that anchors on the `mod-102` inventory rows, sweeps the public evidence, requests the private evidence, checks consistency, drafts the residual-risk paragraph, drafts the compensating-controls list, draws the inheritance decision, and hands off to the vendor-management office with the right routings copied. Hosted foundation models, self-hosted artefacts, datasets, and tooling / audit / monitoring vendors all use the same row schema but shift the reading emphasis. Chapter 07 turns to the crosswalk maintenance that lets the row's compensating-controls references resolve into external-framework obligations without re-authoring the whole master library.
