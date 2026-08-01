# Distinguishing AI-Specific Incidents from General Software Incidents

## Why this chapter

The analyst-tier verb chapter 01 opens with is *recognise*: is the surfaced event an AI-specific incident or a general software incident, and how does it route? The recognition matters because the two incident types route to different places, produce different post-mortem shapes, trigger different governance follow-through, and — critically — differ on whether the AI system's inventory row, impact assessment, and risk-register residual claim need to be re-opened.

A general software incident on a system that happens to have an AI component often does not need any of that follow-through: an outage caused by a load balancer misconfiguration on the RAG-backend service is a load-balancer incident, not an AI incident, even though the affected service serves an LLM. Conversely, an AI-specific incident — a model regression, a jailbreak, a biased-outcome escalation, a hallucination reaching a user — often has no classical-software root cause at all, so the general software-incident-response process (`change management → rollback → post-mortem`) either misses it entirely or files it in the wrong queue.

This chapter fixes the six AI-specific incident classes the analyst must be able to name, the boundary against general software incidents, the *both-at-once* pattern where a single event is both, and the routing rule per class.

## The six AI-specific incident classes

The taxonomy the analyst uses at intake. Each class carries a working definition, one or two representative examples described at the level of an intake ticket, and the primary route the analyst files under. Chapter 03 walks how the class field lands on the incident record.

### 1. Model regression

- **Working definition.** A deployed model's task performance degrades against its established baseline — the release-assurance eval, a scheduled re-eval, or a continuous-monitoring quality panel — without a corresponding change in the *evaluated* input distribution. Includes provider-side model updates that shift behaviour without notice, retrieval-index refreshes that degrade RAG groundedness, prompt-template edits that reduce output quality, and fine-tune runs that produce a checkpoint with worse metrics on the reference set than the incumbent.
- **Representative examples.** *After the vendor's silent model-version update on 2026-06-14, the customer-support copilot's task-completion rate on the internal reference set fell from 0.82 to 0.71.* *The nightly re-index of the product-documentation retrieval corpus dropped RAG groundedness on the internal eval set from 0.87 to 0.73; the drop persisted for three days before the eval was re-run.*
- **Primary route.** `ai-eval-engineer` (metric owner) for the re-eval and root-cause on the model / retrieval / prompt side; `ai-infra-mlops` for the rollback or version-pin if one is available; `ai-governance-analyst` files the incident record and coordinates the IA re-open if the regression's magnitude crosses the assessment's *materiality* threshold (chapter 04).

### 2. Jailbreak

- **Working definition.** A user or a red-team confirms that the deployed model can be induced to bypass its safety training or its guardrail layer and produce content that violates the enterprise's acceptable-use policy or the model provider's usage policy. Distinct from *prompt injection* (which is an attack on trust boundaries between untrusted inputs and the model — see class 3): jailbreak targets the *policy* layer; prompt injection targets the *instruction* boundary. The two frequently co-occur but are separate classes at intake.
- **Representative examples.** *A support agent submitted a jailbreak prompt that induced the copilot to produce content in a category the acceptable-use policy prohibits; the prompt was screenshotted and forwarded to the trust-and-safety inbox.* *A community-forum post published a working jailbreak against the enterprise's public-facing chat assistant; the internal red-team confirmed reproducibility within four hours.*
- **Primary route.** `ai-infra-security` (per OWASP LLM01:2025 and `mod-108` chapter 04) for triage, severity, and mitigation. `ai-red-team-engineer` for reproducibility characterisation and payload capture. `ai-governance-analyst` files the incident record and — if the enterprise has published a system card claiming a specific refusal-rate — coordinates the system-card update.

### 3. Prompt-injection exploitation

- **Working definition.** A confirmed exploitation of the model's instruction-following behaviour where untrusted input embedded in the model's context (a retrieved document, a tool-call return, a user-supplied file, an agent's memory) causes the model to take an action or produce an output the deploying system did not authorise. Includes *direct* injection (the user pastes an instruction) and *indirect* injection (the instruction sits in a source the model retrieves). Distinct from jailbreak (class 2) — prompt injection typically bypasses the *instruction hierarchy* the deployer set, whereas jailbreak bypasses the *safety policy* the provider or deployer set.
- **Representative examples.** *A user uploaded a document containing embedded instructions; the RAG-based assistant included the document in its context and executed the instruction — sending an email via the mail-tool that the user was not authorised to send.* *A support ticket-triage assistant retrieved a ticket comment containing an injected instruction; the model followed the instruction and reassigned the ticket to a queue the requester was not entitled to.*
- **Primary route.** `ai-infra-security` (per OWASP LLM01:2025 — prompt injection, indirect variant) with `application-security` copied if the exploited action crosses an authorisation boundary. `ai-governance-analyst` files the incident record; the IA re-open trigger is whether the injected action produced harm to a person, a system, or a business outcome.

### 4. Biased-outcome escalation

- **Working definition.** A surfaced pattern (through a customer complaint, a fairness-monitoring signal, a media report, a regulator query, or an internal audit finding) that the deployed model produces outcomes that disparately impact a protected class or a legally significant group, at a magnitude that the enterprise's fairness-review notes (`mod-104`) did not predict or the residual-risk claims on the register (`mod-103`) did not envelop. Includes complaint-driven signals (an individual complaint that turns out to reflect a pattern) and monitoring-driven signals (a fairness metric on a dashboard crosses a threshold).
- **Representative examples.** *Three separate complaints in the current month allege the resume-screening tool disadvantages applicants from a specific geography; the fairness-monitoring dashboard confirms the demographic-parity ratio in that geography fell below the acceptable band.* *NYC's Department of Consumer and Worker Protection queried the enterprise's Local Law 144 bias-audit publication after receiving a complaint; the analyst's response requires the incident to be logged in the register.*
- **Primary route.** `ai-eval-engineer` for the deeper eval and the disaggregated re-analysis; `ai-risk-engineer` for the residual-risk re-open on the register entry; `legal` for the regulator interaction if one is in scope; `ai-governance-analyst` files the incident record and coordinates the FRIA re-open (chapter 04). The escalation frequently crosses `head-of-ai-governance` given the enterprise-level exposure.

### 5. Hallucination-driven harm

- **Working definition.** A confirmed instance where the deployed model produced factually incorrect content that reached a person or a downstream system and caused (or credibly could have caused) harm — a wrong medical or financial recommendation delivered to a user, a fabricated legal citation submitted to a court by a customer using the tool, a wrong operational instruction executed by a downstream automation. The class is not *the model hallucinated*; the class is *the hallucination reached and affected someone*.
- **Representative examples.** *The RAG-based clinical-decision-support prototype produced a dosing recommendation that cited a fabricated study; the clinician user reported it via the internal safety channel.* *A customer using the public-facing legal-drafting assistant submitted a court filing with a fabricated case citation; the court's clerk raised it and the customer complained to the enterprise.*
- **Primary route.** `ai-eval-engineer` for the factuality / groundedness re-eval; the affected system's product owner for the customer-facing follow-up; `legal` and `head-of-ai-governance` for high-severity cases where harm is medical, financial, or legal-actionable; `ai-governance-analyst` files the incident record and coordinates the IA re-open. Frequently crosses the *serious incident* threshold under EU AI Act Article 73 if the affected system is high-risk (chapter 07).

### 6. Unauthorised model use

- **Working definition.** A confirmed instance of an AI system, capability, or vendor being used in the enterprise outside the approved envelope — a team using a hosted model provider that has not been through vendor intake, a use case running production traffic against a model version not on the approved-list, an application invoking a model for a purpose not covered by the impact assessment, personal data being sent to a third-party model that the DPA does not cover. Includes both *shadow AI* (an unapproved capability introduced by a team) and *scope creep* (an approved capability used outside its approved scope).
- **Representative examples.** *A marketing team started routing customer-support conversation data through an unvetted transcription provider that has an LLM feature enabled by default; the practice surfaced during a routine `mod-102` inventory reconciliation.* *An engineering team started using an approved model for a customer-messaging use case that the impact assessment does not cover; the practice surfaced during a `mod-108` control test on the *approved-purpose* control.*
- **Primary route.** `ai-governance-analyst` opens the incident record, pauses net-new use in coordination with the technical owner, and drives a fresh intake pass (`mod-102` and, if a third-party is involved, `mod-108` chapter 06). `procurement` / `legal` for the vendor path; `data-protection-officer` if personal data is in scope. `head-of-ai-governance` on the enterprise-level pattern (repeated shadow-AI findings are policy work per chapter 09).

## What is a *general software* incident on an AI system

Not every incident on a system that has an AI component is an AI incident. The four common general-software incident shapes the analyst should recognise and *not* mis-classify as AI incidents:

- **Infrastructure outage.** The service returns 5xx errors; the model is fine; the load balancer, the network, the container platform, the database, or a dependency is down. Classical incident-response; the analyst does not open an AI incident record unless the outage also caused an AI-specific effect (chapter §"The both-at-once pattern").
- **Deployment failure.** A release rolled out with a bad configuration, a mis-set feature flag, a mis-scaled resource, a mis-configured secret. The AI capability is unavailable or misbehaving because the deployment is broken, not because the model changed. Classical change-management incident.
- **Data-pipeline bug.** The ETL that feeds the retrieval index, the feature store, the labelled-data set, or the eval reference dropped rows / duplicated rows / mis-typed a field; the downstream AI capability produces bad outputs because its inputs are bad. Classical data-engineering incident, *unless* the bad inputs reached production and caused an AI-specific effect that the analyst then records against the AI incident record cross-referenced to the data-pipeline incident.
- **Classical security incident.** A credential leak, a privilege-escalation exploit, a known-CVE exploitation against the platform. Classical security-incident-response process; the AI-specific incident classes cover the *AI-specific* attack surfaces (jailbreak, prompt injection, model theft, membership inference, data exfiltration through the model, evasion). Classical security incidents route through the enterprise's existing security-incident process; the analyst opens an AI incident record only if the AI component was itself the exfiltration channel or the exploited asset.

The recognition rule: **an AI incident is one where the AI component's specific behaviour is what makes the event worth recording separately from the enterprise's classical incident processes.** If the event would have looked identical had the AI component been a deterministic function, it is a general software incident.

## The both-at-once pattern

A single event can be *both* a general software incident and an AI-specific incident. The pattern is common enough that the intake question is not *is it one or the other* but *is it one, or the other, or both, and how do the two records cross-reference*.

Representative examples of the both-at-once pattern:

- **Retrieval-index refresh bug (general software) + RAG groundedness regression (model regression, class 1).** The ETL that refreshes the retrieval index shipped a version that indexed by a wrong field; RAG groundedness collapsed. The data-pipeline incident carries the ETL root cause; the AI incident record carries the groundedness regression, the affected inventory row, and the IA re-open (if triggered).
- **Credential leak (classical security) + unauthorised model use (class 6).** A cloud credential leaked; the actor used it to spin up model traffic against an internal endpoint for purposes not covered by any impact assessment. The security incident carries the credential-leak root cause; the AI incident record carries the unauthorised-use finding and the fresh-intake trigger.
- **Deployment failure (general software) + jailbreak (class 2).** A release flipped the guardrail flag off inadvertently; a customer discovered the resulting output-filter bypass within hours. The change-management incident carries the flag-flip root cause; the AI incident record carries the jailbreak class-2 record and — because the customer-facing exposure occurred — the system-card / customer-notification follow-through.
- **Vendor security incident (general security or vendor incident) + AI supply-chain effect.** The model-hosting vendor discloses a security incident affecting shared infrastructure; the analyst assesses whether any of the enterprise's AI systems were affected in an AI-specific way (model-weight exfiltration, prompt-log exposure, inference-time behaviour change). Two records: the vendor-incident record on the enterprise's vendor register and — if the AI-specific effect is confirmed — the AI incident record.

The *both-at-once* pattern is what makes the cross-reference discipline (chapter 03) load-bearing: the AI incident record cites the classical incident record, and the classical record's post-mortem references the AI incident record. A reader picking up either record can walk to the other.

## The routing rule per class

The one-page summary the analyst consults at intake.

| Class | Primary route | Secondary route | IA / FRIA / DPIA re-open trigger |
|---|---|---|---|
| 1. Model regression | `ai-eval-engineer`, `ai-infra-mlops` (rollback) | `ai-risk-engineer` (register residual re-open if magnitude crosses IA materiality threshold) | Yes, if the regressed metric was a load-bearing claim in the IA |
| 2. Jailbreak | `ai-infra-security`, `ai-red-team-engineer` | Product owner (system-card / disclosure) | Yes, if the enterprise's system card or IA claims a specific refusal-rate that the jailbreak now falsifies |
| 3. Prompt-injection exploitation | `ai-infra-security`, `application-security` (if action crossed authorisation boundary) | Product owner; `data-protection-officer` if personal data exposed | Yes, if the injected action caused harm |
| 4. Biased-outcome escalation | `ai-eval-engineer` (disaggregated re-eval), `ai-risk-engineer` (register re-open) | `legal` (regulator interaction), `head-of-ai-governance` | Yes — FRIA re-open is the default, DPIA re-open if personal data / automated-decision-making triggers apply |
| 5. Hallucination-driven harm | `ai-eval-engineer` (factuality re-eval), product owner (customer-facing follow-up) | `legal`, `head-of-ai-governance` (high-severity), regulator (if EU AI Act Article 73 threshold — chapter 07) | Yes, if the harm reached the level the IA claimed the *measures* would prevent |
| 6. Unauthorised model use | `ai-governance-analyst` (pause + fresh intake), technical owner | `procurement` / `legal` (vendor path), `data-protection-officer` (personal data), `head-of-ai-governance` (pattern) | Yes — the IA never covered the use, so the IA is new, not an update |

The analyst does *not* set severity, does *not* commit to a mitigation, and does *not* commit to a public-communication position. Severity is set by the receiving specialist role (informed by the specialist's own severity taxonomy — the ML incident-severity scale, the security-incident-severity scale, the enterprise's crisis-management scale). The analyst's routing action is: *class X per this chapter; primary route Y; IA re-open trigger evaluated as Z; owner ack requested by <date>*.

## Referring to external incident corpora

Two external corpora are useful for the analyst-tier vocabulary. Both are cited on the incident record where an entry in either corpus corresponds to the enterprise's incident.

- **The AI Incident Database (AIID)** at `incidentdatabase.ai` catalogues publicly reported AI incidents by incident ID (`AIID Incident nnn`) with a common data schema — deployer, developer, harmed party, damage, references — that the analyst can borrow when the enterprise's incident is publicly reportable or mirrors a corpus entry.
- **The OECD AI Incidents Monitor** at `oecd.ai/en/incidents-monitor` maintains a real-time feed of AI incidents drawn from global news reporting, structured by principle (safety, fairness, privacy, transparency, accountability). Useful when the enterprise's incident type matches a systemic pattern the monitor has surfaced.

These are external references; neither is the enterprise's system of record. The enterprise's system of record is the `INC-<year>-<sequence>` incident record (chapter 03) and — for high-risk systems — the EU AI Act's post-market-monitoring plan and serious-incident notifications (chapter 07).

## Common failure modes

- **Filing an AI incident as a general software incident.** The on-call team files a jailbreak or hallucination-driven-harm event through the general change-management or IT-incident queue because that is the muscle memory. The analyst who monitors the queues (per chapter 03's intake) escalates and opens the parallel AI incident record. The fix is not the filing team's fault; the fix is the intake discipline.
- **Filing a general software incident as an AI incident.** An infrastructure outage on a service that happens to serve an LLM is filed as an AI incident, cluttering the AI incident record set and diluting the governance signal. The intake question in chapter §"What is a general software incident" is the filter.
- **Missing the both-at-once pattern.** The classical incident is filed and closed; nobody opens the parallel AI incident record even though an AI-specific effect occurred. The fix is the intake question: *did the AI component behave in an AI-specific way as part of this event?*
- **Setting severity at intake.** The analyst annotates a severity guess on the incident record at intake. The receiving specialist ignores the guess or, worse, treats it as authoritative. The fix: severity is *unset* at intake and lands after the specialist triage; the analyst records what the specialist set.
- **Mis-classifying jailbreak as prompt injection or vice versa.** The two look similar at the surface but route differently and drive different follow-through. The distinction: jailbreak breaks the safety policy; prompt injection breaks the instruction hierarchy. When in doubt, file *both* class fields and let `ai-infra-security` triage into one.

## What to memorise

- **Six AI-specific incident classes** — model regression, jailbreak, prompt-injection exploitation, biased-outcome escalation, hallucination-driven harm, unauthorised model use.
- **The AI-vs-software recognition rule.** An AI incident is one where the AI component's specific behaviour is what makes the event worth recording separately. Otherwise it is a general software incident.
- **The both-at-once pattern is common.** Two cross-referenced records — one classical, one AI — is the correct answer.
- **The routing rule per class is a one-page table.** Primary route, secondary route, IA / FRIA / DPIA re-open trigger. Chapter 03 lands the class field on the incident record; chapter 04 walks the IA re-open coordination.
- **Severity is not set at intake.** The receiving specialist sets it.
- **External corpora (AIID, OECD monitor) are references, not the system of record.** The `INC-<year>-<sequence>` record is.

## Summary

This chapter fixes the taxonomy the analyst's *recognition* verb depends on. Six AI-specific incident classes — model regression, jailbreak, prompt-injection exploitation, biased-outcome escalation, hallucination-driven harm, unauthorised model use — with primary and secondary routing per class, and an IA / FRIA / DPIA re-open trigger evaluated at intake. The boundary against general software incidents (infrastructure outage, deployment failure, data-pipeline bug, classical security incident) is the recognition-rule: *is the AI component's specific behaviour what makes the event worth recording separately?* The both-at-once pattern — a single event that is both classical and AI, with two cross-referenced records — is common and drives the cross-reference discipline chapter 03 fixes on the record shape. External corpora — the AIID and the OECD AI Incidents Monitor — are the analyst-tier reference set; the enterprise's `INC-<year>-<sequence>` record is the system of record.
