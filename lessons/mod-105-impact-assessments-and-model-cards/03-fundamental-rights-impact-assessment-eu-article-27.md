# The Fundamental-Rights Impact Assessment — EU AI Act Article 27

## Why this chapter

The EU AI Act ([Regulation (EU) 2024/1689](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)) introduced a new impact-assessment obligation on top of the pre-existing GDPR DPIA. Article 27 requires certain deployers of high-risk AI systems to perform a **fundamental-rights impact assessment** (FRIA) *before* first use. Missing or badly-authored FRIAs are one of the analyst-tier findings that most often triggers escalation to counsel — the obligation is new, the scope is contested at the edges, and the enforcement machinery through EU member-state supervisory authorities is being built out in parallel with the deployer's first drafts.

This chapter walks the Article 27 scope (who owes a FRIA, on what systems), the six required elements, the interlock with the DPIA, and the analyst-tier authoring pattern that reuses the 42005 canonical document.

## Who owes a FRIA

Article 27 applies to specific *deployers* of specific *high-risk* systems. The three scoping questions:

1. **Is the system a high-risk AI system?** High-risk is defined by [Article 6](https://artificialintelligenceact.eu/article/6/) and [Annex III](https://artificialintelligenceact.eu/annex/3/) of the AI Act. Annex III enumerates areas (biometrics, critical infrastructure, education, employment, essential services, law enforcement, migration, administration of justice, democratic processes). Deployment in one of those areas presumptively makes the system high-risk unless a Article 6(3) exemption applies.

2. **Is the deployer in scope?** Article 27 attaches to *deployers* that are:
   - **Bodies governed by public law**, or
   - **Private operators providing public services**, or
   - **Deployers of high-risk systems used to evaluate creditworthiness or credit-scoring** (Annex III point 5(b)), or
   - **Deployers of high-risk systems used for risk assessment and pricing in life and health insurance** (Annex III point 5(c)).
   
   Deployers of *other* Annex III high-risk systems (e.g., employment-decision systems under Annex III point 4) are outside the Article 27 FRIA obligation, though they carry other Article 26 deployer obligations. This is a common early-authoring error — the analyst must not assume all high-risk deployment triggers a FRIA.

3. **Is the assessment already covered?** Article 27(4) permits reuse of an existing DPIA under Article 35 GDPR if it substantively covers the same fundamental-rights impacts. In practice most enterprises complete the FRIA as a distinct artefact and cross-reference the DPIA — the two documents are close but not the same (chapter 04 develops the overlap).

<!-- needs-research: verify the current scoping of Article 27 against the AI Act's consolidated text at eur-lex.europa.eu; the Article 27 scope was among the more actively-negotiated provisions and the final text — including which private-sector deployers are pulled in — should be re-checked before citing to an audit or regulator. -->

## The six required elements

Article 27(1) enumerates the FRIA content. The six elements the analyst produces:

1. **A description of the deployer's processes** in which the high-risk AI system will be used in line with its intended purpose.
2. **A description of the period of time and frequency** during which the high-risk AI system is intended to be used.
3. **The categories of natural persons and groups** likely to be affected by its use in the specific context.
4. **The specific risks of harm likely to have an impact** on the categories of natural persons or groups identified pursuant to (3), taking into account information provided by the provider under Article 13.
5. **A description of the implementation of human-oversight measures**, according to the instructions for use.
6. **Measures to be taken in case of the materialisation of those risks**, including the arrangements for internal governance and complaint mechanisms.

Two mechanical points the analyst enforces:

- **Article 13 information from the provider is a load-bearing input.** The provider of a high-risk system must supply instructions for use that cover intended purpose, characteristics, capabilities, and limitations. The FRIA cannot be completed without that document; if the provider has not supplied it, the analyst notes the gap and escalates.
- **The FRIA is notified to the market-surveillance authority.** Under Article 27(3), on completion the deployer notifies the relevant national market-surveillance authority of the FRIA's results using the template established by the AI Office. This is not just an internal artefact.

<!-- needs-research: track the AI Office's published FRIA notification template as it becomes available; at the time of writing the template was under development and enterprises were preparing based on the Article 27 text alone. -->

## Fundamental rights — what is in scope

Unlike the DPIA (which is bounded by data-protection rights), the FRIA covers the full range of fundamental rights recognised under the [Charter of Fundamental Rights of the European Union](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:12012P/TXT). The rights most commonly load-bearing in an AI impact context:

- **Dignity** (Article 1).
- **Non-discrimination** (Article 21) — the largest single category of AI-relevant FRIA finding.
- **Data protection** (Article 8) — overlaps DPIA; do not omit here because the DPIA covers it.
- **Freedom of expression** (Article 11) — relevant for moderation and content-recommendation systems.
- **Right to good administration and effective remedy** (Article 41 and Article 47) — relevant for automated administrative or judicial-support systems.
- **Right to work** (Article 15) and **workers' rights** (Article 27–31) — relevant for hiring, allocation, and monitoring systems.
- **Rights of the child** (Article 24) and **rights of the elderly** (Article 25) — relevant where the affected population includes protected groups.
- **Consumer protection** (Article 38) — relevant for scoring, pricing, and recommendation systems.

The analyst-tier discipline: for each identified risk of harm (element 4 above), name which Charter right it engages, in one line. If the answer is "no Charter right is engaged", that is either wrong or the system is not the kind that Article 27 was designed for — escalate.

## Mapping the 42005 canonical document into the FRIA

The mapping the analyst uses:

| Article 27 element | Sourced from 42005 canonical section |
|---|---|
| (1) Deployer processes using the system | System description + treatment plan |
| (2) Period and frequency of use | System description + review-triggers section |
| (3) Categories of affected persons | Affected-stakeholder inventory |
| (4) Specific risks of harm + Article 13 provider info | Enumerated impacts + related-artefact reference to the provider's instructions for use |
| (5) Human-oversight implementation | Treatment plan (oversight controls) |
| (6) Response to materialised risk + governance + complaint mechanisms | Treatment plan + related-artefact reference to incident-response plan |

The gaps the analyst fills on top of the canonical document:

- **The Article 13 provider-info attachment or reference.** The FRIA cites the provider's instructions for use; the canonical document points at the vendor review, but the FRIA must reference the specific provider document.
- **The Charter-right tag per identified risk.** The canonical document names harms; the FRIA names the fundamental right each harm engages.
- **The notification record.** After the FRIA is complete and notified to the market-surveillance authority, the notification acknowledgement or reference goes into the FRIA as a permanent field.

## Concrete example — the MCDA-Hiring FRIA view

Assume the MCDA is repurposed to draft interview-invitation and rejection letters for a European hiring pipeline — an Annex III point 4 use case (employment, hiring). The deployer is a private-sector enterprise providing a public service? No — a pure private hiring pipeline is *not* in the Article 27 scope for private deployers of Annex III point 4 systems. So this variant would not trigger the FRIA obligation. Change the example.

Assume instead the MCDA drafts response text for a public employment agency assessing benefits eligibility — a public-body deployer using a high-risk system that determines access to essential public benefits (Annex III point 5(a)). This *does* trigger Article 27.

The FRIA view derived from the MCDA-Benefits canonical document:

- **(1) Deployer processes.** Benefits caseworkers request a draft response for a routine eligibility decision; the caseworker reviews and, if endorsed, dispatches to the applicant.
- **(2) Period and frequency.** Deployed for at least 24 months from go-live; used in ~2,000 draft-request events per week across the agency; used for standard-eligibility decisions only; not used for appeal responses.
- **(3) Categories of persons affected.** Benefits applicants (all working-age adults resident in scope); protected sub-groups include persons with disabilities, non-native language speakers, applicants with irregular residency history.
- **(4) Specific risks of harm.** Confabulation of eligibility criteria (Charter Article 41 — right to good administration); differential accuracy across language and literacy strata (Charter Article 21 — non-discrimination); over-reliance by caseworkers leading to less individualised assessment (Charter Article 41). Reference: provider's instructions for use, MC-2026-0044-v3.
- **(5) Human-oversight implementation.** Every draft reviewed by the caseworker; no draft dispatched without caseworker endorsement; caseworker training programme running quarterly; monitoring of endorsement-rate anomalies as an over-reliance early warning.
- **(6) Response to materialised risk.** Incident-response plan IR-2026-0011; complaint mechanism — existing agency complaints channel with an added AI-decision-flag; internal governance — quarterly AI oversight committee review; escalation to the DPO and to the market-surveillance authority per Article 73 in the event of a serious-incident-triggering event.

That six-element narrative *is* the FRIA. The canonical document is retained; the FRIA is notified to the market-surveillance authority via the AI Office template.

## Where the FRIA stops for the analyst

- **Not a Charter-rights legal opinion.** Naming which Charter right a risk engages is a analyst-tier factual note; the legal characterisation is counsel's. The analyst names the right; counsel opines on the strength of the engagement.
- **Not a substitute for the DPIA.** Article 27(4) allows reuse where the DPIA covers the same fundamental-rights impacts, but the practical pattern is to author both and cross-reference (see chapter 04).
- **Not the provider's conformity assessment.** The provider's high-risk conformity assessment (Article 43) is separate; the FRIA is a *deployer*-side artefact.
- **Not the market-surveillance authority's decision.** The notification informs the authority; it does not authorise deployment.

## What to memorise

- **The scoping filter.** High-risk system + one of {public-law body, private operator of public services, credit / credit-scoring, life or health insurance risk / pricing}. All three tests must be met to trigger Article 27.
- **The six required elements** — processes, period-and-frequency, affected persons, specific risks, human oversight, response to materialised risk.
- **The Article 13 provider-info dependency** — no FRIA without the provider's instructions for use.
- **The notification obligation** — the FRIA is notified to the national market-surveillance authority using the AI Office template.
- **The Charter-right tag** — every identified risk names the fundamental right it engages.

## Summary

The EU AI Act Article 27 FRIA is a deployer-side impact assessment that attaches to a narrow set of high-risk-system deployers — public bodies, private operators of public services, and certain credit and insurance deployers. It requires six enumerated elements, depends on the provider's Article 13 instructions for use, and must be notified to the national market-surveillance authority. The analyst-tier authoring pattern reuses the 42005 canonical document and layers on the Charter-right tags, the provider-info attachment, and the notification record. Legal characterisation of Charter engagements sits with counsel.
