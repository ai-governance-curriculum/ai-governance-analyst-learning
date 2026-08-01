# MITRE ATLAS, NIST AI 100-2, and Google SAIF

## Why this chapter

Chapter 04 fixed the OWASP LLM Top 10 as the analyst's primary tagging convention. This chapter fixes three complementary references the analyst uses when the OWASP list is not the right shape for the finding, when the finding needs a second tag from a taxonomy closer to the attack primitive, or when the enterprise's security team has standardised on one of the three.

The three references overlap in coverage but do different work.

- **MITRE ATLAS** is an adversarial-tactics-and-techniques matrix — the same shape as MITRE ATT&CK, but populated with AI-system-specific tactics and techniques. It answers *what did the adversary do*, and it is what `ai-infra-security` and `ai-red-team-engineer` will most often cite when they write an engagement report.
- **NIST AI 100-2** — the *Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations* report — is a taxonomy that names and defines the classes of AML attack, their attack surfaces, and the mitigations known to reduce them. It is what an internal-audit reviewer or a regulator will most often ask the analyst to cite for the *why-we-tag-what-we-tag* justification.
- **Google SAIF** — the *Secure AI Framework* — is a defender-oriented framework naming six areas of AI-security work that the enterprise should have in place. It is what `senior-ai-governance-architect` will most often cite when structuring the master control library and what the analyst reads to understand which control families exist.

None of the three replaces OWASP LLM Top 10; they augment it. The analyst's rule: OWASP tag on every security-linked finding, plus one ATLAS technique identifier where the security team's report names one, plus one NIST AI 100-2 attack-class citation where the finding sits inside a defined class, plus a SAIF-area anchor on the control-library side. The analyst's job is *recognition*, not *analysis*: knowing when to reach for each reference and where to file the tag.

## MITRE ATLAS

[MITRE ATLAS](https://atlas.mitre.org/) — the *Adversarial Threat Landscape for Artificial-Intelligence Systems* — is a knowledge base of adversary tactics and techniques targeting AI-enabled systems, published and maintained by MITRE under an open-community model similar to ATT&CK.

### The shape

ATLAS uses the ATT&CK matrix shape. The horizontal axis is *tactics* (the adversary's high-level objective in a phase of the attack); the vertical axis under each tactic is *techniques* (the specific ways the adversary can achieve that objective). Each technique has a stable identifier (e.g., `AML.T0043` for *Craft Adversarial Data*), a description, a set of known case studies, and, where relevant, links to related ATT&CK techniques.

At the level of tactics, ATLAS covers the adversary lifecycle from *Reconnaissance* through *Impact*, in the same order as ATT&CK. Analyst-tier note: the exact set of tactics has been extended and re-named as ATLAS has matured; do not memorise the list from a snapshot. Read the current [ATLAS matrix](https://atlas.mitre.org/matrices/ATLAS) at test time and cite the identifier as it appears there.

<!-- needs-research: ATLAS is a living matrix; the tactic list, technique count, and specific identifiers have shifted between annual releases. Before an audit-facing citation, re-read the current matrix and confirm the identifier still resolves to the same technique. -->

### What the analyst does with it

- **Cite the technique identifier when the source artefact does.** A red-team engagement report that calls out `AML.T0051 (LLM Prompt Injection)` carries that identifier onto the analyst's control-record tag; the analyst does not re-derive the identifier.
- **Do not derive an identifier from scratch.** ATLAS technique identification is `ai-red-team-engineer` / `ai-infra-security` scope. The analyst who sees an unfamiliar finding but no ATLAS identifier in the report files the record with the OWASP tag alone and asks the security team for the ATLAS identifier if they consider one applicable.
- **Use the tactic name for grouping.** In the control-status report (chapter 03), grouping findings by ATLAS tactic (*Reconnaissance*, *ML Model Access*, *Exfiltration*, *Impact*) surfaces adversary-phase clustering the OWASP list does not.
- **Read the case studies for pattern recognition.** ATLAS publishes a growing set of [case studies](https://atlas.mitre.org/studies) drawn from public incidents and research; reading them is how the analyst builds the mental library that distinguishes *this is probably an evasion attack* from *this is probably a poisoning attack*.

## NIST AI 100-2

The [NIST AI 100-2 report](https://csrc.nist.gov/pubs/ai/100/2/e2025/final) — *Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations* — is NIST's normative reference on AML attack classification. It sits alongside NIST AI 100-1 (the [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework), the module's foundational spine from `mod-101`) and the AI 600-1 [Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) used in `mod-103` chapter 03.

Two version notes.

- **The report has been revised.** NIST published *AI 100-2e2023* in January 2024 and revised it as *AI 100-2e2025*, released in 2025. Analyst-tier: cite the edition (`AI 100-2e2025`) not just the series number, and re-verify attack-class names between editions.
- **The taxonomy covers both predictive AI and generative AI attacks.** The predictive-AI side has been stable across editions; the generative-AI side has expanded substantially. Cite the section that applies to the finding.

<!-- needs-research: NIST AI 100-2e2025 attack-class terminology should be cross-checked against the published text before verbatim quotation. This chapter uses commonly cited names from the field literature and the report's public abstract. -->

### The four attack-class families

At the level the analyst needs to recognise, AI 100-2 groups AML attacks into four families:

- **Evasion attacks.** The adversary crafts an input at inference time that causes the model to produce a wrong output — an adversarial example that misclassifies, an image with a perturbation that flips the label, a prompt engineered to bypass a safety filter. The classic *cat-vs-dog with a pixel patch* example lives here. In LLM terms, evasion overlaps heavily with OWASP LLM01 Prompt Injection.
- **Poisoning attacks.** The adversary manipulates the training data, fine-tuning data, or model weights *before deployment* such that the model learns behaviour the enterprise did not intend — a backdoor trigger, a biased slice, degraded performance on specific adversary-relevant queries. Overlaps with OWASP LLM04 Data and Model Poisoning; also with LLM03 Supply Chain when the poisoning vector is a compromised upstream artefact.
- **Privacy attacks.** The adversary uses query access to the deployed model to reconstruct information the model should not reveal — training data samples (data reconstruction / model inversion), whether a specific record was in the training set (membership inference), or the model itself (model extraction / model theft). Overlaps with OWASP LLM02 Sensitive Information Disclosure and, for model theft, with LLM10 Unbounded Consumption.
- **Abuse attacks.** The adversary uses the model *as designed but for adversary purposes* — using a generative model to produce phishing content, misinformation, or CSAM; using an agentic system to perform tasks that circumvent trust controls elsewhere. The AI 100-2e2025 revision materially expanded coverage of this class for generative AI.

Each family in AI 100-2 further decomposes by *attacker capability* (black-box / grey-box / white-box), *attacker goal* (targeted / untargeted / availability), and *attack surface* (training-time / deployment-time / inference-time). Analyst-tier depth: know that the decomposition exists and cite it when the security team's report already uses the vocabulary.

### What the analyst does with it

- **Use the family name as the secondary tag.** *Evasion*, *poisoning*, *privacy*, *abuse* are the analyst's second-level shorthand. A finding tagged *LLM01:2025 — Prompt Injection* often also merits *AI 100-2 — Evasion* on the record.
- **Use it as the justification citation.** When internal audit asks *why is this control classed as prompt-injection-defence rather than data-quality?*, the answer is anchored in an AI 100-2 attack-class definition, not in a personal opinion. The analyst cites the section (with edition and page-or-clause identifier).
- **Do not mint new attack-class names.** AI 100-2 is the reference; if a finding does not fit any of the four families, the analyst records it as *outside AI 100-2 taxonomy* in the analyst note and asks `ai-infra-security` and `senior-ai-governance-architect` how the enterprise wants it classed.

## Google SAIF

Google's [Secure AI Framework (SAIF)](https://safety.google/cybersecurity-advancements/saif/) is a defender-oriented reference for structuring an AI-security programme. Where OWASP names the risks and NIST AI 100-2 names the attacks, SAIF names the *defence programme areas* the enterprise should have in place. It is published by Google's cybersecurity team as a practitioner framework and is not a standard; it is influential enough that `senior-ai-governance-architect` will often cite it when structuring the master control library.

### The six core elements

SAIF is organised around six core elements the enterprise addresses across its AI stack.

- **Expand strong security foundations to the AI ecosystem.** Extend the enterprise's existing security controls (identity, network, data-at-rest / in-transit protection, secret management, secure software development lifecycle) to the AI-specific components (training pipelines, model registries, inference endpoints, prompt stores, vector stores).
- **Extend detection and response to bring AI into the enterprise threat universe.** AI-specific telemetry, incident-response playbooks that include AI-native events (prompt injection detection, model-extraction traffic patterns), and integration with the enterprise SOC.
- **Automate defences to keep pace with existing and new threats.** Instrument the defensive stack so AI-specific attacks are detected and mitigated at the pace they emerge; use AI in defence where the workload demands it.
- **Harmonise platform-level controls to ensure consistent security across the organisation.** Move AI-security controls into the platform layer where they can be applied uniformly, rather than re-implemented per application.
- **Adapt controls to adjust mitigations and create faster feedback loops for AI deployment.** Continuous testing (red-team, evals, adversarial-test suites) that feeds back into the control set; a control lifecycle short enough to keep pace with model change.
- **Contextualise AI system risks in surrounding business processes.** End-to-end risk assessment that treats the AI model as one component of a business process, not the whole risk surface.

<!-- needs-research: SAIF wording and the exact six-element list should be verified against the current https://safety.google/cybersecurity-advancements/saif/ page before an audit-facing citation. Google has revised SAIF materials over time. -->

### What the analyst does with it

- **Anchor control-library structure conversations.** When `senior-ai-governance-architect` reworks a control family, SAIF's six-element decomposition is a useful frame. The analyst reads it enough to recognise which element a proposed control sits under.
- **Cite it as the defender-side counterpart to OWASP / NIST / ATLAS.** In the analyst's crosswalk (chapter 07), SAIF elements form a defensible column when the enterprise wants to see coverage across the six defence areas.
- **Do not use it as a threat taxonomy.** SAIF is not a taxonomy of attacks; it is a taxonomy of defence programme areas. A finding is not "*a SAIF-2 finding*"; a *control* addresses a *SAIF element*.

## The seven top categories the analyst must recognise

The learning objective for this chapter and the previous one names seven categories the analyst must recognise. Consolidated across the four references, they are:

| Category | Primary OWASP LLM 2025 tag | Primary AI 100-2 family | Typical ATLAS tactic anchor | Typical SAIF element anchor |
|---|---|---|---|---|
| Prompt injection | LLM01 | Evasion | ML Model Access / Initial Access | Automate defences; Adapt controls |
| Data exfiltration (sensitive info disclosure via output) | LLM02 | Privacy | Exfiltration | Expand strong security foundations |
| Model theft | LLM10 (via model-extraction subclass) | Privacy | Exfiltration | Expand strong security foundations |
| Membership inference | LLM02 (as the disclosure surface) | Privacy | Exfiltration | Expand strong security foundations; Contextualise risks |
| Adversarial evasion (predictive-AI classic) | *(often outside the LLM Top 10 scope; nearest is LLM01 for LLM equivalents)* | Evasion | ML Model Access | Automate defences |
| Supply-chain compromise | LLM03 | Poisoning (when the vector is training-time) | Resource Development / Initial Access | Expand strong security foundations; Harmonise platform-level controls |
| Guardrail bypass (jailbreak / system-prompt leak / excessive-agency abuse) | LLM01 + LLM06 + LLM07 | Evasion + Abuse | ML Model Access + Impact | Adapt controls; Contextualise risks |

The analyst does not need to memorise every ATLAS technique identifier or every AI 100-2 sub-class. The analyst needs to recognise which of the seven categories a finding sits in well enough to *tag it with the right OWASP identifier*, *cite the right AI 100-2 family*, *pass along the ATLAS technique the security team names*, and *anchor the control against the right SAIF element*.

## Recognition depth vs exploitation depth

The delegation boundary from chapter 01 restated for this chapter.

- **Recognition depth** is what the analyst has. It supports tagging, filing, routing, control-status reporting, and crosswalk maintenance. The analyst can read a red-team report and know what class of attack it describes. The analyst can look at a finding and know which security team will own the response.
- **Exploitation depth** is what `ai-red-team-engineer` and `ai-infra-security` have. It supports payload construction, jailbreak development, adversarial-example generation, pentest execution, and mitigation design. The analyst does not have and should not attempt to acquire this depth as part of role work.

The distinction is the *how far can I go before I am doing security-team work*. Tagging a finding with `AML.T0051` because the security team's report already names it: recognition depth. Constructing a payload that demonstrates `AML.T0051` on a new endpoint: exploitation depth. The analyst stops at the first.

## Cross-referencing across the four taxonomies

A well-tagged security-linked control record carries all four references where they apply.

- **OWASP tag.** The primary filing convention. Version-cited (`LLM01:2025`).
- **AI 100-2 attack-class citation.** The family and, where the source artefact names it, the sub-class. Edition-cited (`AI 100-2e2025 — Evasion`).
- **ATLAS technique identifier.** The specific technique from the source artefact. Identifier-cited (`AML.T0051`).
- **SAIF element anchor.** The defence-programme area the corresponding control sits under. Element-named (`SAIF — Adapt controls`).

Not every finding will have all four; a red-team engagement report may name ATLAS but not the AI 100-2 sub-class, or vice versa. The analyst carries forward whatever the source artefact provides and does not manufacture the missing ones.

## Common failure modes

The tagging-and-referencing failures the analyst should watch for.

- **Manufacturing ATLAS identifiers.** The analyst reads a finding and looks up an ATLAS technique that seems similar without the security team having named it. The identifier is then treated as authoritative downstream. Fix: only carry the identifier the source artefact names; ask the security team when in doubt.
- **Tagging systems, not findings.** The four references belong on the finding, control record, or ticket — not on the inventory row. Fix: `mod-102` inventory fields are the system-level anchor; these tags live on the security-linked artefact.
- **Confusing SAIF with a threat taxonomy.** Treating "*a SAIF-2 finding*" as if it named an attack class rather than a defence area. Fix: the analyst uses SAIF to anchor controls (defender side), not findings (attacker side).
- **Missing edition citations.** Citing *NIST AI 100-2* without the edition, or *OWASP LLM Top 10* without the year. Fix: the version discipline in chapter 04 applies to all four references.
- **Speculative tagging.** Tagging a control with an ATLAS technique that has not appeared in any incident, eval, or red-team artefact. Fix: tagging is retrospective on evidence; forecast is `senior-ai-governance-architect` / `ai-infra-security` scope.

## What to memorise

- **Four references, three of which are threat-side and one of which is defender-side.** OWASP LLM Top 10 (primary filing), NIST AI 100-2 (attack-class citation), MITRE ATLAS (technique identifier from the security team's report), Google SAIF (defence-programme area anchor).
- **The seven top categories the analyst recognises** — prompt injection, data exfiltration, model theft, membership inference, adversarial evasion, supply-chain compromise, guardrail bypass — each with predictable OWASP / AI 100-2 / ATLAS / SAIF anchors.
- **Cite edition and identifier.** *LLM01:2025*, *AI 100-2e2025 — Evasion*, `AML.T0051`, *SAIF — Adapt controls*. Bare series names are not citations.
- **Recognition depth, not exploitation depth.** The analyst tags, files, and routes. The analyst does not construct payloads or design mitigations.
- **Carry forward what the source names; do not manufacture the missing.** Speculative tagging inflates the finding set and misleads downstream teams.

## Summary

The AI/LLM security-threat recognition the analyst needs sits across four references. OWASP LLM Top 10 is the primary filing convention (chapter 04). NIST AI 100-2 is the attack-class taxonomy that anchors the *why-we-tag-what-we-tag* justification and names the four families — evasion, poisoning, privacy, abuse. MITRE ATLAS is the adversary-tactics-and-techniques matrix, published in the same shape as MITRE ATT&CK, whose technique identifiers the analyst carries forward when the security team's report names them. Google SAIF is a defender-oriented programme framework naming six areas of AI-security work that anchors the *control* side rather than the *finding* side. The analyst's job is recognition — recognising the seven top categories (prompt injection, data exfiltration, model theft, membership inference, adversarial evasion, supply-chain compromise, guardrail bypass) well enough to tag, file, and route to `ai-infra-security` — not exploitation. Chapter 06 turns from internal security to the third-party AI vendor / model / dataset intake that produces the vendor-risk-register row.
