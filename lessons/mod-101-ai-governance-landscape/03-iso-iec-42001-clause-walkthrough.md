# ISO/IEC 42001:2023 — Clause Walkthrough and the ISO/IEC 27001 Correspondence

## Why this chapter

[ISO/IEC 42001:2023](https://www.iso.org/standard/81230.html) is the world's first *management-system standard* for AI. Where the NIST AI RMF is a voluntary framework, ISO/IEC 42001 is a certifiable standard: an organisation can be audited against it and issued a certificate the way it can against [ISO/IEC 27001](https://www.iso.org/standard/27001) for information security or ISO 9001 for quality. That certification lifts it above "a good practice we chose" into "a documented AI Management System (AIMS) auditors can trace."

For an analyst, the practical stakes are two-fold:

1. Many employers — especially in EU-touching, healthcare, and financial-services shops — are pursuing or already hold ISO 27001 certification. They will layer ISO 42001 on top rather than start from scratch. The AI governance analyst is the person who *walks the parallel clauses* so the AIMS lives inside the existing ISMS management-review cadence.
2. When an intake asks "does this go into our AIMS scope?", you need to answer against ISO 42001 Clause 4 (Context of the organisation), not from intuition.

You do not need to memorise every subclause. You need to know the ten top-level clauses, the four Annexes, and where they meet the ISO 27001 equivalents.

## The Annex L "High-Level Structure"

Modern ISO management-system standards — 9001 (quality), 14001 (environment), 27001 (information security), 42001 (AI), and others — all share the same top-level clause skeleton, sometimes called the *Harmonised Structure* (formerly Annex L / Annex SL). That is the *reason* ISO 42001 layers so cleanly onto an existing ISMS: the clause numbering, the language, and the audit rhythm are all the same. Clause 4 is always "Context of the organisation". Clause 6 is always "Planning". Clause 9 is always "Performance evaluation".

If the enterprise already runs an ISO 27001 management review every quarter with an internal-audit report and a set of corrective actions, ISO 42001 does not invent a new rhythm — it fits inside that same rhythm.

## Top-level clauses (1–10)

Clauses 1–3 are the ISO housekeeping (scope; normative references; terms and definitions). Clauses 4–10 are the working parts of the management system. Below is a one-line intent per clause plus the ISO 27001 counterpart.

| Clause | ISO/IEC 42001 topic | Intent (one line) | ISO/IEC 27001 correspondence |
|---|---|---|---|
| 4 | Context of the organisation | Determine internal / external issues, interested parties, and AIMS scope | Clause 4 (ISMS scope) — same shape, AI-flavoured issues and parties |
| 5 | Leadership | Top-management commitment, AI policy, roles and responsibilities | Clause 5 — same shape, AI policy replaces / augments information-security policy |
| 6 | Planning | Address risks and opportunities, AI objectives, AI risk assessment, AI impact assessment | Clause 6 — same shape, adds AI *impact* assessment as a peer to risk assessment |
| 7 | Support | Resources, competence, awareness, communication, documented information | Clause 7 — same shape; AI competence adds ML/AI literacy |
| 8 | Operation | Operational planning and control, AI risk assessment / treatment, AI impact assessment in operation | Clause 8 — same shape; ISO 42001 adds AI-specific operational controls |
| 9 | Performance evaluation | Monitoring, measurement, analysis, evaluation; internal audit; management review | Clause 9 — identical rhythm; AI KPIs join information-security KPIs |
| 10 | Improvement | Nonconformity and corrective action; continual improvement | Clause 10 — identical corrective-action machinery |

For a shop that already runs 27001, the analyst's practical work is: extend Clause 4 scope to include AI systems; add AI policy to Clause 5; add AI risk-and-impact assessments to Clauses 6 and 8; feed AI KPIs into the existing Clause 9 management review; run AI-specific corrective actions through the existing Clause 10 pipeline.

## The four Annexes

The teeth of ISO/IEC 42001 are in its Annexes.

- **Annex A — Reference control objectives and controls.** The AI-management-system analogue of ISO 27001 Annex A. Contains AI-specific controls the organisation *considers* and either implements, justifies excluding, or documents as not applicable. This is what an auditor will point to when asking "show me your Statement of Applicability."
- **Annex B — Implementation guidance for AI controls.** Expands Annex A with implementation guidance — the "how" for each control. Analogous to ISO 27002 for the information-security world.
- **Annex C — Potential AI-related organisational objectives and risk sources.** A menu of objectives (e.g., fairness, robustness, transparency, privacy) and risk sources (e.g., data quality, environmental impact, complexity) that the organisation draws on when doing its Clause 6 planning.
- **Annex D — Use of the AIMS across domains or sectors.** Guidance on tailoring the AIMS for particular sectors (healthcare, financial services, public sector), including how to combine ISO 42001 with sector-specific standards.

The Statement of Applicability (SoA) — a document listing every Annex A control with status *implemented / not implemented (with justification) / not applicable* — is often the analyst's most visible clause-work deliverable and is directly analogous to the ISO 27001 SoA.

## The 27001 ↔ 42001 mapping in practice

The correspondence is *structural* at the clause level and *conceptual* at the Annex level. It is not a control-for-control map — ISO 27001 controls are about information assets, ISO 42001 controls are about AI systems. But the machinery is the same.

**Where the two systems reinforce each other**

- **Scope (Clause 4).** ISO 27001's ISMS scope is usually described in terms of information assets, sites, and services. ISO 42001's AIMS scope extends that to AI systems the organisation *develops, provides, or uses*. Analyst work: keep the two scopes reconciled — a system that is out of ISMS scope but in AIMS scope (or vice versa) is a governance smell.
- **Policy (Clause 5).** ISO 27001 requires an information-security policy; ISO 42001 requires an AI policy. In practice most enterprises publish a single umbrella responsible-AI policy and cross-reference the ISMS policy for security controls.
- **Risk assessment (Clause 6).** ISO 27001 references [ISO/IEC 27005](https://www.iso.org/standard/80585.html) for information-security risk management; ISO 42001 references [ISO/IEC 23894](https://www.iso.org/standard/77304.html) for AI risk management. These are peer standards. Analyst work: know which risk register you are adding a row to, because the fields differ.
- **Documented information (Clause 7).** Same document-control machinery — approvals, versioning, retention.
- **Internal audit and management review (Clause 9).** Same cadence, same rhythm. The AI review can be a track inside the existing management-review meeting or its own agenda item.

**Where ISO 42001 adds new machinery**

- **AI impact assessment** (Clause 6 and Clause 8) — a peer of risk assessment, not a replacement. ISO 27001 has no direct equivalent. The AI IA sits closer to a GDPR Article 35 DPIA in spirit and is expanded in [ISO/IEC 42005](https://www.iso.org/standard/44545.html).
- **Annex A AI-specific controls** — controls for data quality, model documentation, human oversight, AI system life-cycle stages, third-party AI use. These do not have ISMS analogues; they are the AI-specific delta.

## Where you will feel the difference on the job

- **The intake questionnaire** (`mod-102`) includes fields the ISMS never asked about: training-data provenance, decisioning autonomy, EU AI Act tier, applicable sector regulator. Those exist because the AIMS needs the answers under Clause 6 and Clause 8.
- **The Statement of Applicability** grows an AI section. The analyst-tier work is to keep the AI SoA row aligned with the enterprise's control library — a task that lives in `mod-108`.
- **Model, system, and dataset documentation** (`mod-105`) becomes documented information under Clause 7.5 and evidence for the Annex A controls that require documentation.
- **Incident response** (`mod-109`) becomes both a Clause 10 corrective action and a MANAGE 4 action in the RMF; the analyst files against both frames.

The general rule: if the enterprise already runs an ISMS, you do not stand up a parallel governance rhythm — you add AI-specific evidence to the rhythm that already exists.

## Concrete example — layering an AIMS onto an existing ISMS

Suppose the enterprise is a mid-size SaaS company already certified to ISO 27001. Product leadership wants an ISO 42001 certificate to sell into EU customers.

- **Clause 4 update.** Extend the existing scope statement to include the two production AI systems and the one internal RAG assistant.
- **Clause 5 update.** Publish a Responsible AI Policy referencing the OECD AI Principles and the enterprise's own values; identify the AI governance council (chartered per GOVERN 2).
- **Clause 6 update.** Adopt ISO/IEC 23894 for AI risk sources; adopt ISO/IEC 42005 as the template for AI impact assessment; commit to running risk-and-impact at intake for every new AI system and at every material change.
- **Clause 7 update.** Add "AI literacy" competence for all developers, product managers, and analysts (an EU AI Act Article 4 obligation too — see `mod-104-communication-and-council-support` and the EU AI Act chapter).
- **Clause 8 update.** Bake the intake questionnaire and the risk-and-impact templates into the SDLC.
- **Clause 9 update.** Add three AI KPIs (percentage of AI systems with a current impact assessment, mean time to close a MANAGE-1 register item, count of open MEASURE-2 findings above threshold) to the quarterly management review.
- **Clause 10 update.** Reuse existing corrective-action machinery.
- **Statement of Applicability.** Add an AI section listing every Annex A control with status.

That is a realistic month-of-work programme, and analyst-tier participation is scoped to the templating, the SoA maintenance, and the management-review evidence pack — not to the architecture decisions.

## What to memorise

- Clauses **4–10** and the fact that 1–3 are housekeeping.
- The **four Annexes** and what each is for.
- The claim that ISO 42001 and ISO 27001 share the **Annex L / Harmonised Structure**, which is why they layer cleanly.
- The **Statement of Applicability** is the single most-visible clause artefact.

## Summary

ISO/IEC 42001:2023 is an ISO-family management-system standard for AI, sharing its top-level clause structure with ISO/IEC 27001 and other MS standards. Clauses 4–10 give you the management-system rhythm; the four Annexes carry the AI-specific controls, guidance, objectives, and sector tailoring. When an enterprise already runs an ISMS, the analyst's job is to extend scope, add AI risk-and-impact assessments, keep a Statement of Applicability, and feed AI KPIs into the existing management-review cadence — not to invent a parallel governance program.
