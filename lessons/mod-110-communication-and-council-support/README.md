# mod-110 — Stakeholder Communication, Council Support, and Policy Drafting at the Analyst Tier

**Estimated effort:** 10 hours

The nine modules before this one produced artefacts — the inventory row, the register entry, the fairness note, the impact assessment, the tracker row, the eval-evidence row, the control-status report, the vendor row, the incident record, the monitoring-reading note, the PMS summary. Each was written in the vocabulary its module fixed. The audiences that read those artefacts — legal, privacy, security, product, executive committee, board / governance council — are not fluent in that vocabulary. This module is the discipline that translates the artefact into the audience's language, walks the packet into the council-meeting pre-read, captures the council's decisions in minutes an internal auditor can still reconstruct three years later, drafts the first-cut internal-policy work the enterprise's AI governance program depends on, contributes to external-facing responsible-AI communication under legal and executive review, and positions the analyst's own certification portfolio (AIGP → CIPP or ISO/IEC 42001 lead-implementer) as the shared vocabulary with cross-functional peers.

The role's stance in this module: the analyst is a *translator, meeting-packet packager, minutes-and-decisions recorder, and first-cut drafter*. The analyst is not the council decision-maker, not the policy ratifier, not the enterprise spokesperson, and not the accountable executive who sits on the record for what the council or the regulator receives. Chapter 09 walks the boundary in full.

## Learning objectives

- Translate a technical eval / risk / audit output into business-facing language for legal, privacy, security, product, and executive audiences — using ISO/IEC 38507 governance-body vocabulary where the audience is board-level.
- Prepare pre-read decks and one-pagers for AI governance council meetings; capture decisions and assign owners; write meeting minutes that survive audit.
- Draft first-cut internal AI policies and standards — acceptable-use policy, model-approval standard, third-party AI vendor review standard, generative-AI employee guidance — routing for `senior-ai-governance-architect` edits and `head-of-ai-governance` ratification.
- Position the IAPP AIGP body of knowledge as the shared communication vocabulary; know when to pursue CIPP/US or CIPP/E as the privacy-adjacent add-on and ISO/IEC 42001 lead-implementer / lead-auditor as a rising preferred credential.
- Contribute to external-facing responsible-AI communication (trust site, model card publication, regulator responses) at an analyst level.

## Chapters

| # | Chapter | Focus |
|---|---|---|
| 01 | [The Analyst's Scope on Communication and Council Support](01-analyst-scope-on-communication-and-council-support.md) | Role stance (translator, packager, recorder, first-cut drafter); the three tangible outputs (audience-adapted briefing, council packet, first-cut policy / standard draft); delegation preview; vocabulary |
| 02 | [Translating Technical Evidence for Five Audiences](02-translating-technical-evidence-for-five-audiences.md) | The translation-not-summarisation rule; the five day-to-day audiences (legal, privacy, security, product, executive committee); per-audience length, vocabulary, depth, cross-references, delivery channel; per-audience translation moves; the routing dependency |
| 03 | [ISO/IEC 38507 and Board-Level Governance-Body Vocabulary](03-iso-iec-38507-and-board-level-vocabulary.md) | What ISO/IEC 38507:2022 is and is not; the governance-body / management distinction; the *evaluate / direct / monitor* spine; the AI-specific considerations vocabulary (autonomy, opacity, data use, cultural change, third-party dependence); board vs board committee vs council |
| 04 | [The Council Pre-Read: Deck, One-Pager, Standing Agenda](04-council-pre-read-deck-and-one-pager.md) | The standing-agenda spine; the deck + one-pager pack; the decisions-needed slide; the M − 14 to M + 5 cadence; how each pre-read section maps to a prior-module artefact set; the sensitive-item pattern |
| 05 | [Council Minutes That Survive Audit](05-council-minutes-that-survive-audit.md) | The minutes template; what *survives audit* means field-by-field; language discipline; the action-item register; retention, access, versioning; the five-field decision-record pattern |
| 06 | [Drafting First-Cut Internal AI Policies and Standards](06-first-cut-internal-ai-policies-and-standards.md) | Policy vs standard vs guidance vs procedure; the four-phase routing chain (analyst → architect → consultation → ratification); the universal section shape; the four canonical first-cut drafts (AUP, model-approval standard, third-party vendor review standard, GenAI employee guidance) |
| 07 | [External-Facing Responsible AI Communication](07-external-facing-responsible-ai-communication.md) | The four external artefact families (trust site, published model cards, regulator responses, public consultation responses); the review-and-approval chain; the stop-and-escalate red flags; the public-facing vocabulary discipline; EU AI Act Article 50 transparency notices |
| 08 | [Certifications: AIGP, CIPP, and ISO/IEC 42001 Lead Implementer / Lead Auditor](08-certifications-aigp-cipp-and-iso-42001.md) | AIGP as shared communication vocabulary; CIPP/US and CIPP/E as privacy-adjacent depth extensions; ISO/IEC 42001 lead-implementer / lead-auditor as standards-and-assurance depth extensions; peer-role credentials the analyst does *not* pursue; three worked portfolio sequences |
| 09 | [Delegation Boundary and Escalation Patterns](09-delegation-boundary-and-escalation-patterns.md) | Full delegation-boundary table (translation, packaging, drafting, external comms, certifications, cross-module rows); four escalation classes (content-owner delay, boundary-holding request, regulator / external audit / public exposure, recurring pattern → policy-work); the recurring-pattern promotion rule |

## Exercises

Hands-on prompts; solutions live in the paired `ai-governance-analyst-solutions` repository.

| # | Exercise | Estimated |
|---|---|---|
| 01 | [Audience-Adapted Briefing Drill](exercises/exercise-01-audience-adapted-briefing-drill.md) | 2 h |
| 02 | [Council Pre-Read and Minutes](exercises/exercise-02-council-pre-read-and-minutes.md) | 2 h |
| 03 | [Acceptable-Use Policy First Draft](exercises/exercise-03-acceptable-use-policy-first-draft.md) | 2 h |
| 04 | [Certifications Portfolio Planner](exercises/exercise-04-certifications-portfolio-planner.md) | 2 h |

## Lab

- `lab-01` — Not yet authored; scheduled for the next content cycle.

## Quiz

- Knowledge check per the curriculum plan. Not yet authored; scheduled for the next content cycle.

## Resources

Curated primary references are in [`resources.md`](resources.md).

## Prerequisites

Fluency in every prior module in the track. The three tangible outputs of this module — audience-adapted briefing, council packet, first-cut policy / standard draft — are packaging and translating of artefacts the earlier modules produced. Specifically: `mod-102` (the inventory row roll-up that anchors the pre-read's portfolio-at-a-glance section), `mod-103` (the register roll-up and the council-attention threshold), `mod-104` (fairness-review evidence that the audience-adapted briefing translates for legal and product), `mod-105` (the IA / FRIA / DPIA sign-off pipeline that lands on the council for endorsement), `mod-106` (the tracker rows that feed the regulator-headlines section), `mod-107` (the eval-evidence rows the model-approval standard's release-assurance gate cites), `mod-108` (the control-status report and vendor-risk-register that feed the pre-read's control-status and vendor roll-ups; the escalation register the council's incoming class-4 items sit on), `mod-109` (the incident register, monitoring-reading note, and PMS summary that feed the incident-and-monitoring roll-up).

## Downstream dependencies

- `project-101` — the end-to-end deliverable set uses one worked pre-read pack, one set of minutes, and at least one first-cut policy draft (typically the AUP) as the *governance-in-operation* backbone.
- The analyst's own promotion path — the demonstrated ability to translate, draft, package, and route through ratification is what promotes an analyst into the `senior-ai-governance-architect` track (chapter 09).
