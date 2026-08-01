# OWASP LLM Top 10 and the Analyst-Tier Taxonomy

## Why this chapter

Chapters 01–03 fixed the control-cycle scope and deliverables. This chapter fixes the *tagging convention* the analyst uses whenever a control or a control-test finding is security-linked — the AI/LLM security threat category the finding sits under, and the routing decision to `ai-infra-security` that follows.

The analyst does not perform the security analysis, reproduce the exploit, or write the mitigation. What the analyst *does* is recognise the finding well enough to (a) open the record in the right category so the security team can triage it correctly, (b) tag any related control test with the taxonomy identifier so the crosswalk (chapter 07) resolves cleanly, and (c) surface the pattern in the control-status report so recurring themes reach the escalation register.

Four public references are load-bearing for that recognition, and this chapter walks the first — [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/), because it is the most-referenced list in the LLM-application space and the one product-and-infra teams most often name in their own security reviews. Chapter 05 covers the other three (MITRE ATLAS, NIST AI 100-2, Google SAIF) and how they compose with the OWASP list.

The tagging is not a security opinion. The tagging is a filing convention. The `ai-infra-security` team decides whether a finding is real, severe, exploitable, and worth engineering time; the analyst decides only where to file it.

## The OWASP GenAI Security Project

The list is published by the [OWASP GenAI Security Project](https://genai.owasp.org/), an OWASP-hosted project that maintains a rolling set of AI-security artefacts. The Top 10 for LLM Applications is the flagship artefact; the project also publishes an *AI Security Solutions Landscape* and a growing set of practitioner-oriented deep-dive guides.

Two version notes for the analyst.

- **The list has been revised.** The current published list is *OWASP Top 10 for LLM Applications 2025*, released in late 2024; a *2023 edition* preceded it. Item numbering, wording, and coverage differ between the two. Analyst-tier: cite the version by year when tagging (*"LLM01:2025 — Prompt Injection"*, not *"LLM01"*), so a reader can resolve the tag to the correct list even after another revision.
- **The list is community-maintained.** New entries and re-framings appear each cycle. The analyst reads the list every time the OWASP project ships a new version, updates the crosswalk (chapter 07), and files the delta as a library-level review request to `senior-ai-governance-architect` for any controls whose statements reference the changed items by identifier.

## The 2025 list

The ten items in the 2025 edition, with the analyst's tagging-and-routing framing per item. Verbatim item titles are per the [published 2025 list](https://genai.owasp.org/llm-top-10/). The threat descriptions here are analyst-tier paraphrases; enterprise use with an audit-facing artefact should cite the OWASP page directly.

### LLM01:2025 — Prompt Injection

- **What it is.** An attacker crafts input — direct (in the user's prompt) or indirect (in a document or web page the model retrieves) — that manipulates the model into ignoring its system prompt, revealing hidden context, invoking unauthorised tools, or producing content that would otherwise be refused.
- **Where the analyst sees it.** Red-team engagement report findings (chapter walked in `mod-107` chapter 04); a customer-reported jailbreak; an incident-response ticket referencing "system-prompt leak" or "guardrail bypass"; a control-test log sample showing the guardrail did not fire on adversarial input.
- **How to tag.** *LLM01:2025 — Prompt Injection* on the record; if the vector is retrieval-based, note *indirect variant* in the analyst note; if the target is tool-use, note *agentic variant*.
- **Where to route.** `ai-infra-security` for triage; `ai-red-team-engineer` for reproduction; the ML platform owner for guardrail-classifier improvement.

### LLM02:2025 — Sensitive Information Disclosure

- **What it is.** The model reveals sensitive content — training-data snippets that include PII or trade secrets, retrieval-augmented context intended for a different user, credentials or system-prompt content that should not be reachable, or downstream tool output containing sensitive fields.
- **Where the analyst sees it.** A DLP alert on model output; a customer report of another customer's data appearing in output; an eval-report finding on data-leakage; a red-team output showing membership-inference-style disclosure.
- **How to tag.** *LLM02:2025 — Sensitive Information Disclosure*. If the source is training data (versus retrieval context or downstream tool), note *training-data variant*; if the vector is a membership-inference query pattern, cite the crosswalk to *NIST AI 100-2* privacy attacks (chapter 05).
- **Where to route.** `ai-infra-security` for exploit assessment; `data-protection-officer` if the disclosed content is personal data (a DPIA re-open trigger, per `mod-105` chapter 04); `procurement` / `legal` if the disclosure is training-data-sourced and the training corpus is a vendor artefact.

### LLM03:2025 — Supply Chain

- **What it is.** A compromise in the ingredients of the LLM application — a poisoned base-model weight file, a malicious fine-tuning dataset, a compromised dependency in the model-serving stack, an LoRA / adapter of unknown provenance, a data-preprocessing pipeline pulling from an untrusted source, a hosted-inference-provider vulnerability.
- **Where the analyst sees it.** A vendor-security notice (part of chapter 06's vendor intake); an internal supply-chain-scan hit against a model registry; an incident-response ticket referencing "unsigned model", "unknown model provenance", or a fine-tuning dataset with license/provenance issues.
- **How to tag.** *LLM03:2025 — Supply Chain*. Cross-reference the specific artefact class (weight / adapter / dataset / dependency / hosted inference) in the analyst note.
- **Where to route.** `ai-infra-security` and `supply-chain-security` (if the enterprise runs a distinct programme); `procurement` / `legal` for vendor-artefact recall or contract-clause escalation; the ML platform owner for internal-registry policy update.

### LLM04:2025 — Data and Model Poisoning

- **What it is.** Adversarial manipulation of training, fine-tuning, or RAG-index data such that the model learns behaviours the enterprise did not intend — biased or hostile output on specific triggers, backdoored responses under specific keys, degraded performance on adversary-relevant queries.
- **Where the analyst sees it.** A fairness-review-note finding of unexplained performance skew on a specific slice (surfaced via `mod-104`); a data-provenance audit finding on a training set (surfaced via `mod-102` intake); a red-team engagement report finding of a backdoor trigger.
- **How to tag.** *LLM04:2025 — Data and Model Poisoning*. Note the artefact class (training data / fine-tuning data / RAG index / adapter) and the vector (author-of-input / label-manipulation / gradient-manipulation / model-supply-chain — see LLM03).
- **Where to route.** `ai-infra-security` and `ai-red-team-engineer`; the training-pipeline owner (typically `ml-engineer`) for pipeline hardening; `procurement` / `legal` if the dataset provenance is vendor-sourced.

### LLM05:2025 — Improper Output Handling

- **What it is.** The application-side handling of LLM output does not treat the output as untrusted — passing it directly to a shell, a database, a downstream tool call, or a browser rendering without validation, allowing content injection, code execution, XSS, SSRF, or SQL-injection-style attacks in the downstream layer.
- **Where the analyst sees it.** A control test on output-handling middleware; a pentest report on the LLM-integrating service; a security review of an agentic system with unmediated tool calls.
- **How to tag.** *LLM05:2025 — Improper Output Handling*. Note the downstream sink class — *shell*, *SQL*, *tool-call*, *browser*, *email*, *external-API*.
- **Where to route.** `application-security` first (the flaw is in the app-side handling, not the model); `ai-infra-security` copied for the model-side context; the application owner for remediation.

### LLM06:2025 — Excessive Agency

- **What it is.** An agentic system granted more permissions, tools, or autonomy than its function requires — a tool-set that includes write actions when read actions would suffice, an authorisation model that trusts model-generated tool-call arguments without policy checks, an autonomy setting that lets the model act without human-in-the-loop for actions with real-world side effects.
- **Where the analyst sees it.** A design-review artefact for a new agentic system; a control test on tool-call authorisation policy; a red-team report on tool-abuse; an incident-response ticket referencing "agent triggered X without approval".
- **How to tag.** *LLM06:2025 — Excessive Agency*. Note the axis — *tool-set*, *permission*, *autonomy*.
- **Where to route.** `ai-infra-security` and the agentic-system owner; `principal-ai-engineer` for design-review reopen; the human-oversight owner (per `mod-105` FRIA) if the excessive-agency finding voids a human-oversight assumption.

### LLM07:2025 — System Prompt Leakage

- **What it is.** The model's system prompt — including any credentials, hidden context, or trust-boundary-defining instructions — is extractable via user prompts. The 2025 edition elevates this from a sub-case of prompt injection to a distinct entry because the class of harm (a leaked prompt reveals the enterprise's control design to an attacker) is worth its own tracking.
- **Where the analyst sees it.** Red-team engagement reports; an internal jailbreak-attempt corpus test; a customer report of "the system prompt looks like...".
- **How to tag.** *LLM07:2025 — System Prompt Leakage*. Note whether the leaked prompt contained credentials, tool-authorisation instructions, or business logic.
- **Where to route.** `ai-infra-security` for exploit assessment; `senior-ai-governance-architect` for control-library review if the leaked prompt exposes the enterprise's guardrail design; the ML platform owner for prompt-relocation to non-leakable channels (per-request context, tool-side policy).

### LLM08:2025 — Vector and Embedding Weaknesses

- **What it is.** Attacks and weaknesses in the retrieval-augmented-generation (RAG) layer — poisoned vector-database entries, embedding-inversion attacks that reconstruct source text from vectors, tenant-isolation failures in shared vector stores, embedding-model-choice-driven bias in retrieval.
- **Where the analyst sees it.** A RAG-quality eval report (per `mod-107` chapter 03) with an unexpected groundedness drop tied to specific corpus content; a security review of the vector store; a tenant-isolation-review artefact.
- **How to tag.** *LLM08:2025 — Vector and Embedding Weaknesses*. Note the specific axis — *poisoned index*, *inversion*, *tenant-isolation*, *embedding-choice bias*.
- **Where to route.** `ai-infra-security` and the RAG-platform owner (typically `ml-engineer` or `data-engineer`); `data-protection-officer` if the reconstruction risk touches personal data.

### LLM09:2025 — Misinformation

- **What it is.** The model produces confident but incorrect output — hallucination, fabricated citations, over-confident answers on domains the model was not built to handle — where downstream consumers act on the output as if it were verified.
- **Where the analyst sees it.** RAG-triad eval-report groundedness findings; user-facing incident reports of a model asserting false facts; a downstream-consumer complaint about acted-on hallucination.
- **How to tag.** *LLM09:2025 — Misinformation*. Note whether the vector is a *grounding-gap* (no retrieval available; model confabulates) or a *retrieval-failure* (retrieval available but ignored).
- **Where to route.** `ai-evaluation-engineer` and the ML platform owner for the eval-and-mitigation loop; `product` for downstream-consumer messaging; `ai-infra-security` copied where the misinformation risk creates a downstream security decision (e.g., a model asserting a URL is safe when it is not).

### LLM10:2025 — Unbounded Consumption

- **What it is.** The absence of rate limits, cost caps, or token budgets on model invocations — leading to denial-of-wallet, denial-of-service, and abuse-of-tenant patterns. Includes model-extraction-by-query patterns where an attacker uses cheap-per-call inference to reconstruct a valuable model.
- **Where the analyst sees it.** A cost-anomaly alert; an infra-team ticket referencing "runaway agentic loop"; a security review of an unauthenticated inference endpoint; a suspected model-extraction traffic pattern.
- **How to tag.** *LLM10:2025 — Unbounded Consumption*. Note the vector — *denial-of-wallet*, *denial-of-service*, *model-extraction*.
- **Where to route.** `ai-infra-security` and the infra-platform owner; `finops` for cost-impact; `procurement` if the runaway usage sits with a third-party vendor.

Item numbering here matches the 2025 published list at the time of authoring. Confirm against the OWASP page before quoting in an audit-facing artefact. `<!-- needs-research: cross-check the 2025 list against the current published state of https://genai.owasp.org/llm-top-10/ before an audit-facing citation, and refresh both wording and item order if the project has revised the list. -->`

## The analyst's tagging rule

The tagging rule is one line — *tag every security-linked control record and every security-linked control-test finding with the OWASP LLM Top 10 identifier the finding most naturally maps to* — plus these five constraints:

- **Tag by the *primary* category.** A finding that touches multiple items (prompt injection that extracts a system prompt, then triggers a tool-call that mishandles output) gets the primary tag plus one or two secondary tags in the analyst note. The primary is what the security team triages first.
- **Cite the version.** *LLM01:2025* not *LLM01*. When the OWASP project ships a new edition, controls whose statements reference the old numbering get a library-level review request to `senior-ai-governance-architect`.
- **Tag *findings*, not *systems*.** The tag lives on the finding, the control record, and the incident ticket. It does not live on the inventory row (`mod-102` fields do that job). A system that has had five distinct prompt-injection findings has five *LLM01:2025* tags in the finding set, not one on the system.
- **Do not tag when the finding is not security-linked.** A fairness-review-note finding of demographic-slice underperformance is a `mod-104` artefact, not a *LLM04:2025* poisoning finding — unless the analyst has evidence of a *deliberate* poisoning vector. When in doubt, leave the tag off and ask `ai-infra-security` to assess.
- **Do not use the tag as a severity claim.** OWASP does not assign severities per entry. Severity is `ai-infra-security`'s call on the specific finding in context.

## Mapping OWASP items to evidence-artefact classes

The tagging rule composes with chapter 02's six evidence-artefact classes. Common shapes:

| OWASP LLM 2025 item | Typical evidence-artefact class(es) |
|---|---|
| LLM01 Prompt Injection | Log sample (jailbreak-classifier hits + misses); eval-report link (red-team engagement) |
| LLM02 Sensitive Information Disclosure | Log sample (DLP alerts on output); eval-report link (leakage eval) |
| LLM03 Supply Chain | Config export (model registry allow-list); sign-off record (vendor intake acceptance from chapter 06); eval-report link (vendor artefact hash verification) |
| LLM04 Data and Model Poisoning | Config export (training-pipeline signing / dataset hash); eval-report link (backdoor eval or fairness-slice eval) |
| LLM05 Improper Output Handling | Config export (output-handler middleware policy); eval-report link (pentest report on the app) |
| LLM06 Excessive Agency | Config export (tool-set + authorisation policy); sign-off record (design-review acceptance) |
| LLM07 System Prompt Leakage | Log sample (leakage-attempt corpus); eval-report link (red-team engagement) |
| LLM08 Vector and Embedding Weaknesses | Config export (vector-store tenant isolation policy); eval-report link (RAG-quality + security review) |
| LLM09 Misinformation | Eval-report link (RAG-triad groundedness); log sample (post-market user feedback) |
| LLM10 Unbounded Consumption | Config export (rate limits + cost caps); log sample (anomaly alerts) |

The mapping is not exhaustive. It is a starting point the analyst adjusts against the specific control's evidence class expectations set by `senior-ai-governance-architect` in the master library.

## The file-and-route pattern

Once tagged, every security-linked record follows a short file-and-route pattern the enterprise runs the same way each time.

- **Open the record.** The GRC platform or the security-issue tracker (per enterprise convention). Fields: OWASP tag(s), affected `INV-<year>-<sequence>` systems, source artefact (the eval report / log sample / customer report), analyst note, requested action.
- **Route to `ai-infra-security`.** The security team owns triage, severity, exploitability, and mitigation-design. The analyst supplies the record; the analyst does not co-own the mitigation.
- **Copy the ML / infra / product owner.** The team whose surface the finding sits on is copied for context and to prevent duplicate discovery.
- **Cross-reference the control tests.** If the finding relates to a control the analyst has tested this period, add the finding as a follow-up on the control-test row (chapter 03). If the finding is not covered by an existing control, flag *no-corresponding-control* as an escalation to `senior-ai-governance-architect` per chapter 09.
- **Add to the control-status report.** The report's §5 escalations and §7 delegation-boundary notes carry security-linked routings; the report's appendix carries the ticket identifiers. Internal audit sees what was routed even if the resolution sits with `ai-infra-security` beyond the report window.

The analyst does not wait for the mitigation to appear in the report. The routing is the visible action; the resolution shows up next period.

## What the analyst does not do

Restating for tagging clarity:

- **The analyst does not exploit.** No prompt-injection payload construction beyond what an existing red-team report shows. No independent jailbreak development. If asked to help construct an attack, the analyst refers the request to `ai-red-team-engineer` or an authorised external red-team engagement.
- **The analyst does not evaluate mitigation code.** A pull request proposing a new guardrail classifier is not the analyst's review; it belongs to `ai-infra-security` and the platform team.
- **The analyst does not set severity.** Severity is a security-team decision informed by exploitability, blast radius, and mitigation cost. The analyst reports the tag; the security team reports the severity.
- **The analyst does not tag speculatively.** A hypothetical concern is not a finding. If the analyst suspects an OWASP-item risk but has no evidence, the analyst files a *scoping-request* to `ai-red-team-engineer` for an evaluation, not a *finding* tagged with the item.

## What to memorise

- **The list is *OWASP Top 10 for LLM Applications 2025*.** Cite by year; refresh when the project ships a new edition.
- **Ten items.** LLM01 Prompt Injection, LLM02 Sensitive Information Disclosure, LLM03 Supply Chain, LLM04 Data and Model Poisoning, LLM05 Improper Output Handling, LLM06 Excessive Agency, LLM07 System Prompt Leakage, LLM08 Vector and Embedding Weaknesses, LLM09 Misinformation, LLM10 Unbounded Consumption.
- **Tag findings, not systems.** The tag lives on the finding, the control record, and the ticket.
- **Route to `ai-infra-security`.** The analyst files; the security team triages, sets severity, and owns mitigation.
- **The tag maps to an evidence-artefact class.** Chapter 02's six classes compose with the ten items into predictable evidence shapes.
- **Speculative tagging is not tagging.** A hypothesis becomes a tag only when an eval, log, or report substantiates it.

## Summary

The OWASP LLM Top 10 is the analyst's primary filing convention for security-linked control records and findings. The 2025 edition has ten items covering prompt injection, sensitive information disclosure, supply chain, data and model poisoning, improper output handling, excessive agency, system prompt leakage, vector and embedding weaknesses, misinformation, and unbounded consumption. The analyst's job is to recognise, tag, and route — not to exploit, evaluate mitigations, or set severity. Each item maps to one or two of the evidence-artefact classes from chapter 02, which composes with the control-cycle discipline so security-linked findings show up naturally in the control-status report. Chapter 05 covers the three complementary references (MITRE ATLAS, NIST AI 100-2, Google SAIF) that the analyst uses when the OWASP list is not the right filing convention or when the finding needs a second, more specific tag from an adjacent taxonomy.
