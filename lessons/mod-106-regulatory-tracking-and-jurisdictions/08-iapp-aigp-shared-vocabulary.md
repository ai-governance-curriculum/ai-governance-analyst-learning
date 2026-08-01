# The IAPP AIGP Body of Knowledge as the Shared Vocabulary

## Why this chapter

Regulatory tracking is a discipline other people in the enterprise need to speak with the analyst about — the DPO, the general counsel, the CISO, the chief risk officer, the head of compliance, the internal auditor, and the AI governance council or oversight committee. Each of them reads a different quarterly reading list. What the analyst needs is a *shared vocabulary* — a set of terms and topic categories the other functions recognise — so that a tracker row does not need to be paraphrased into three different framings for three different audiences.

The [International Association of Privacy Professionals (IAPP)](https://iapp.org/) publishes a certification and body-of-knowledge specifically for AI governance: the [Artificial Intelligence Governance Professional (AIGP)](https://iapp.org/certify/aigp/) certification. Its body of knowledge (BoK) is the closest thing the AI-governance field has to a shared taxonomy — comparable in role to what the CIPP/E BoK is for privacy or the CISSP CBK is for information security. This chapter positions the AIGP BoK as the shared vocabulary for this tracker work, walks its domain structure, and describes how tracker rows are tagged to the AIGP domains so that reports up to counsel, risk, and audit read fluently in the same language.

The analyst is not required to hold the AIGP certification. The BoK is public — [the Body of Knowledge PDF is published by IAPP](https://iapp.org/certify/aigp/) — and its category structure is a durable reference regardless of whether the certification is pursued.

## What the AIGP is

The AIGP is IAPP's AI-governance-professional certification, launched in 2023. It targets the practitioner who governs AI programmes across development and deployment — the role this track is educating for. The exam and the accompanying body of knowledge cover:

- The foundations of AI and machine learning at a working-vocabulary level.
- The AI governance and risk-management landscape.
- The core regulatory and policy landscape across major jurisdictions.
- AI-specific risks and how they map to governance controls.
- The full AI system life cycle from problem definition through post-deployment monitoring.

The BoK is organised into a small number of domains — the exact domain names and weights are on the IAPP AIGP page and are updated by IAPP periodically. As of authoring, the AIGP BoK's five domains are:

1. **Understanding the Foundations of Artificial Intelligence.**
2. **Understanding AI Impacts on People and Responsible AI Principles.**
3. **Understanding How Current Laws Apply to AI Systems.**
4. **Understanding the Existing and Emerging AI Laws and Standards.**
5. **Understanding the AI Development Life Cycle.**

<!-- needs-research: verify the current AIGP body-of-knowledge domain names, weights, and sub-domain enumeration against the [IAPP AIGP body of knowledge page](https://iapp.org/certify/aigp/) before quoting to a candidate or a certification-track brief. IAPP revises the BoK on a periodic basis. -->

Six sub-topics per domain in the BoK (paraphrased at analyst-tier depth):

- **Domain 1 — Foundations.** AI/ML technical vocabulary — types of AI, model architectures, training vs inference, evaluation, common failure modes. Sits underneath the whole track; `mod-101` chapter 02 covers the GenAI Profile risk vocabulary that the analyst reuses.
- **Domain 2 — Impacts and Responsible AI Principles.** Ethical frameworks, harm categorisation, non-discrimination, transparency, accountability, contestability. Overlaps `mod-101` chapter 05 (international values baseline) and `mod-104` (fairness reviews).
- **Domain 3 — How Current Laws Apply to AI Systems.** Privacy laws (GDPR, CCPA, HIPAA), non-discrimination (Title VII, EU non-discrimination directives), consumer-protection (FTC Section 5, UDAP analogues), sector-specific laws applied to AI. Overlaps chapter 07 of this module directly.
- **Domain 4 — Existing and Emerging AI Laws and Standards.** EU AI Act, Colorado AI Act, NYC LL 144, sector-specific overlays, ISO/IEC 42001, ISO/IEC 42005, NIST AI RMF, voluntary codes. Overlaps chapters 02–06 and chapter 09 of this module.
- **Domain 5 — AI Development Life Cycle.** Problem framing, data governance, model development, testing, deployment, monitoring, incident response, decommissioning. Overlaps `mod-102` through `mod-109` of the full track.

The BoK is thus a *cross-section* of the same content the track teaches, organised for a certification exam rather than for a role's day-one workflow. Analyst-tier discipline: use the AIGP domain names as *tags* on tracker rows so that a reader oriented around the BoK can filter, read, and interpret quickly.

## Why the shared-vocabulary framing matters

Three specific audiences the analyst reports to:

- **The DPO** typically holds a privacy-first certification — [CIPP/E](https://iapp.org/certify/cippe/), [CIPP/US](https://iapp.org/certify/cipp-us/), or the [CIPM](https://iapp.org/certify/cipm/). The DPO reads GDPR-shaped terminology natively — *controller*, *processor*, *lawful basis*, *DPIA*, *Article 22*. The DPO recognises AIGP domain 3 immediately.
- **The CISO or CRO** typically holds a [CISSP](https://www.isc2.org/certifications/cissp), [CISM](https://www.isaca.org/credentialing/cism), or [CRISC](https://www.isaca.org/credentialing/crisc) certification. They read risk-management-shape terminology — *inherent*, *residual*, *control*, *appetite*, *tolerance*. AIGP domain 2 and domain 4 are the tabs that read fluently to them.
- **The internal auditor** reads standard-and-control-shape terminology — *management assertion*, *evidence*, *test of design*, *test of operating effectiveness*. AIGP domain 4 gives them the standards-inventory shape they recognise; AIGP domain 5 gives them the lifecycle shape.

The analyst who tags tracker rows with AIGP domains — and labels executive summaries with the domain the row sits in — reduces the *what does this term mean* friction that otherwise turns an oversight-committee meeting into a definition negotiation.

## How to tag tracker rows with AIGP domains

The analyst-tier tagging pattern:

- **Every tracker row carries at least one AIGP domain tag.** Rows are often multi-domain (an EU AI Act row on high-risk classification touches domain 4 primarily and domain 3 for the interaction with GDPR); the analyst lists the primary domain first.
- **Sub-domain tags are optional but useful.** *Domain 3 — GDPR Article 22 automated decision-making* is more specific than *domain 3*; where the BoK sub-topic enumeration supports it, name the sub-topic.
- **The tag is not the source of authority.** The primary regulatory citation stays in the *instrument* column; the AIGP tag is a discoverability index.
- **Filtering by tag produces the certification-domain reading list.** *All rows tagged domain 3* is a coherent set for a CIPP-holder DPO's monthly reading; *all rows tagged domain 4* is a coherent set for a CISSP-holder CRO's quarterly view.

Example — an inventory row and its tracker-row tag block:

```
INV-2026-0088 (MCDA-Benefits) — applicable regulations:
  REG-2026-EU-002 (AI Act — high-risk classification)          — AIGP D4
  REG-2026-EU-003 (AI Act — Article 27 FRIA)                    — AIGP D4
  REG-2026-EU-006 (GDPR Article 22)                             — AIGP D3
  REG-2026-EU-007 (GDPR Article 35 DPIA)                        — AIGP D3
  REG-2026-EU-008 (GDPR Article 36 prior consultation)          — AIGP D3
  REG-2026-US-FED-001 (Title VII / ADA / ADEA — EEOC)           — AIGP D3
  REG-2026-US-CO-002 (Colorado AI Act — deployer duties)        — AIGP D4
  REG-2026-SEC-INS-004 (EIOPA + AI Act Annex III point 5(c))   — AIGP D4
```

The tag block is short and mechanical. A DPO looking for the day's D3 reading pulls the four D3 rows and reads them; a CRO looking for the quarter's D4 reading pulls the D4 rows. Both are looking at the same underlying tracker; the tag makes filtering a single-step operation.

## Related IAPP resources the analyst uses alongside the tracker

Beyond the AIGP BoK itself, IAPP publishes maintained resources the analyst references in the *primary-source URLs* column of relevant tracker rows:

- **[IAPP Resource Center](https://iapp.org/resources/) and topic guides** — the AI governance topic guide is a living hub of IAPP content on AI governance.
- **[IAPP US State Privacy Legislation Tracker](https://iapp.org/resources/article/us-state-privacy-legislation-tracker/)** — a maintained map of enacted and proposed US state consumer-privacy laws with AI-adjacent provisions. Used as *how the analyst noticed a state statute*; the primary source (state legislative website) is what populates the tracker's evidence field.
- **[IAPP Global AI Legislation Tracker](https://iapp.org/resources/article/global-ai-legislation-tracker/)** — a similar map at global scope.
- **[IAPP webinars, KnowledgeNet events, and Global Privacy Summit AI programme](https://iapp.org/conference/)** — a stream of practitioner discussion. Useful signal; not tracker evidence.

The analyst-tier discipline for IAPP-sourced content: treat IAPP trackers and topic-guide entries as *secondary references* — the entry pointed the analyst at a change or a resource; the tracker's evidence field cites the primary source the IAPP entry itself links to.

## The AIGP certification decision

Whether the analyst pursues the AIGP certification is an individual professional-development decision. The track is designed around the same body of knowledge, so a track-completing analyst is materially prepared for the AIGP exam without dedicated additional study.

Two factors argue for pursuing the certification:

- **External recognition.** Career mobility across enterprises is easier with a widely-recognised certification. The AIGP is the AI-governance analog of what CIPP/E is for privacy — recognised by hiring managers as a floor-of-competence signal.
- **BoK-refresh discipline.** IAPP updates the BoK periodically as the field moves. Certification-holders receive continuing-privacy-education requirements that keep the BoK fresh; the certification decision is often paired with an enterprise professional-development budget commitment.

Two factors argue against or for delay:

- **Timing relative to a stable BoK.** The AIGP BoK is still relatively young (2023 launch) and IAPP has revised it. Sitting the exam against a version of the BoK that will be superseded within twelve months is worse than waiting for the next revision to settle.
- **Enterprise-recognition alternative.** Some enterprises value ISO/IEC 42001 lead-implementer certifications or NIST AI RMF training over the AIGP; the analyst reads the specific enterprise's culture before committing.

The decision is out of scope for this module. What is in scope is that the BoK — with or without the certification — is the reference vocabulary the analyst uses to organise the tracker and to communicate up.

## Where the AIGP-as-shared-vocabulary framing stops for the analyst

- **Not a substitute for the primary regulatory citation.** The AIGP tag is discoverability; the tracker row's evidence is the primary regulatory source.
- **Not a scope-of-analyst-work definition.** The BoK enumerates topics an AI-governance professional is expected to know; the specific work the enterprise's analyst does is defined by the role and by the intake / inventory / register / assessment / tracker / evidence / incident / communication chain from `mod-102` through `mod-110`.
- **Not the enterprise's competency framework.** Enterprises maintain their own competency frameworks and career ladders; the AIGP BoK is one input to those, not a replacement.

## What to memorise

- **The AIGP is IAPP's AI-governance-professional certification and body of knowledge.** Launched 2023; the closest thing the field has to a shared taxonomy.
- **The five current domains.** Foundations; impacts and responsible-AI principles; how current laws apply to AI; existing and emerging AI laws and standards; AI development life cycle. Verify against the IAPP page before quoting.
- **Tag every tracker row with at least one AIGP domain.** Discoverability index for readers oriented around the BoK.
- **The certification decision is individual, the vocabulary is not.** Whether the analyst pursues the AIGP is a professional-development choice; using the BoK as the shared reference vocabulary is a tracker-hygiene rule.
- **IAPP-published trackers are secondary references.** The primary source they cite is what populates the tracker's evidence field.

## Summary

The IAPP AIGP body of knowledge is the closest the AI-governance field has to a shared taxonomy. The five current AIGP domains — foundations, impacts and responsible-AI principles, current laws applied to AI, existing and emerging AI laws and standards, AI development life cycle — read fluently to the DPO, CISO, CRO, and internal auditor whose day-jobs the analyst reports into. Tagging every tracker row with at least one AIGP domain turns the tracker into a filterable reading list for each of those audiences without paraphrasing the underlying content. The AIGP certification is optional; using its BoK as the shared vocabulary is not. Chapter 09 walks the EU AI Office GPAI Code of Practice as the anchor example of a voluntary code that anticipates regulator expectations; chapter 10 closes the module with the regulatory-change-note that routes an update into the affected inventory rows.
