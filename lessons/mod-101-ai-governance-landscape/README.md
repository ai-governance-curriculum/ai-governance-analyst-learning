# mod-101 — AI Governance Landscape: Frameworks, Standards, and Values Baselines

**Estimated effort:** 12 hours

This module is the shared vocabulary for the rest of the track. Everything downstream — intake, risk assessments, impact assessments, model cards, regulatory tracking, controls, incident response — assumes you can open the NIST AI RMF, ISO/IEC 42001, and the EU AI Act, find the right section, and cite it in a governance record without hallucinating clauses that are not there. This module gets you to that fluency.

## Learning objectives

- Paraphrase the four functions of NIST AI RMF 1.0 — GOVERN, MAP, MEASURE, MANAGE — and the sub-categories most cited by employers, using the Playbook as a day-to-day reference.
- Recite the 12 generative-AI risks enumerated in the NIST AI RMF Generative AI Profile (AI 600-1) and match each to a plausible internal use case.
- Walk the clause structure of ISO/IEC 42001:2023 (AI Management System) and know which clauses map to the equivalent ISMS clauses in ISO/IEC 27001.
- Read the EU AI Act risk-tier scheme (unacceptable / high / limited / minimal) and locate Annex III high-risk domains at a level sufficient to tag an incoming intake.
- Position OECD AI Principles, the Council of Europe AI Framework Convention, and the UNESCO Ethics Recommendation as the international values baseline the enterprise policy should not undercut.
- Explain where the analyst role stops and where the senior-ai-governance-architect / head-of-ai-governance roles begin, using explicit deferral rules from the ownership map.

## Chapters

| # | Chapter | Focus |
|---|---|---|
| 01 | [NIST AI RMF 1.0 — The Four Functions and the Playbook](01-nist-ai-rmf-four-functions.md) | GOVERN, MAP, MEASURE, MANAGE; trustworthy-AI characteristics; how to use the Playbook |
| 02 | [NIST AI RMF Generative AI Profile — The Twelve Risks](02-genai-profile-twelve-risks.md) | The 12 GenAI risks with plausible internal use cases and defaults |
| 03 | [ISO/IEC 42001 — Clause Walkthrough and the ISO/IEC 27001 Correspondence](03-iso-iec-42001-clause-walkthrough.md) | Clauses 4–10, the four Annexes, the SoA, and how it layers on an ISMS |
| 04 | [EU AI Act — Risk Tiers and Annex III](04-eu-ai-act-risk-tiers-and-annex-iii.md) | Unacceptable / high / limited / minimal; Annex III areas; GPAI; phase-in dates |
| 05 | [The International Values Baseline — OECD, Council of Europe, and UNESCO](05-international-values-baseline.md) | The three instruments and where each sits in the enterprise policy stack |
| 06 | [Role Scope and Deferrals — What Stays on the Analyst Desk](06-role-scope-and-deferrals.md) | Owned scope, up / sideways / out-of-family defers, boundary-holding heuristics |

## Exercises

Hands-on prompts; solutions live in the paired `ai-governance-analyst-solutions` repository.

| # | Exercise | Estimated |
|---|---|---|
| 01 | [NIST RMF Four Functions Flashcards](exercises/exercise-01-nist-rmf-four-functions-flashcards.md) | 2 h |
| 02 | [ISO 42001 Clause Walkthrough](exercises/exercise-02-iso-42001-clause-walkthrough.md) | 2 h |
| 03 | [EU AI Act Tier Tagging Drill](exercises/exercise-03-eu-ai-act-tier-tagging-drill.md) | 2 h |
| 04 | [GenAI Profile Risks Mapped to Use Cases](exercises/exercise-04-genai-profile-risks-mapped-to-use-cases.md) | 2 h |
| 05 | [Role Scope and Deferral Map](exercises/exercise-05-role-scope-and-deferral-map.md) | 2 h |

## Lab

- `lab-01` — One-Page Framework Cheatsheet for a Product Team. Not yet authored; scheduled for the next content cycle.

## Quiz

- One knowledge check per the curriculum plan. Not yet authored; scheduled for the next content cycle.

## Resources

Curated references — official standards, regulations, and instruments cited across the chapters — are in [`resources.md`](resources.md).

## Prerequisites

See the track-level [`PREREQUISITES.md`](../../PREREQUISITES.md). No AI-specific prerequisites for this module — the material is the entry point.

## Downstream dependencies

Every module that follows assumes fluency in this material. In particular:

- `mod-102-ai-system-inventory-and-intake` uses EU AI Act tiers and the NIST RMF MAP function at every intake.
- `mod-103-risk-assessment-authoring` walks NIST RMF MAP subcategory-by-subcategory.
- `mod-105-impact-assessments-and-model-cards` cites ISO/IEC 42001, ISO/IEC 42005, and EU AI Act Article 27.
- `mod-106-regulatory-tracking-and-jurisdictions` builds on the EU AI Act baseline and the international values instruments.
- `mod-108-controls-and-compliance-evidence` uses ISO/IEC 42001 Annex A as a control anchor.
- `mod-110-communication-and-council-support` cites the OECD / CoE / UNESCO baseline in policy-drafting work.
