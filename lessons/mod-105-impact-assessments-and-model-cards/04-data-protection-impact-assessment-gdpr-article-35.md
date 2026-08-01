# The Data-Protection Impact Assessment — GDPR Article 35 and Its Overlap With the FRIA

## Why this chapter

The [General Data Protection Regulation](https://eur-lex.europa.eu/eli/reg/2016/679/oj) data-protection impact assessment (DPIA) is the oldest and most-litigated impact assessment the analyst will meet. [Article 35 GDPR](https://gdpr-info.eu/art-35-gdpr/) has required it since 25 May 2018 whenever a type of processing is *likely to result in a high risk to the rights and freedoms of natural persons*, and case-law and supervisory-authority guidance across the eight years since have converged on a fairly specific expectation of what a DPIA looks like.

For AI systems, three points matter to the analyst:

1. The DPIA is often already required whether or not the FRIA is — most AI systems that process personal data at scale trigger the Article 35 threshold.
2. The DPIA and FRIA overlap substantively. Poor coordination between them produces contradictory artefacts that are worse than either alone.
3. The DPIA carries a specific consultation-of-supervisory-authority obligation under Article 36 when residual high risk remains — the analyst must know when to raise that flag.

This chapter walks the Article 35 trigger, the four required elements, the DPO consultation and Article 36 prior-consultation mechanics, and how the DPIA is authored alongside the FRIA from the same 42005 canonical document.

## When a DPIA is required

Article 35(1) sets the general trigger: a DPIA is required *where a type of processing, in particular using new technologies, and taking into account the nature, scope, context and purposes of the processing, is likely to result in a high risk to the rights and freedoms of natural persons*.

Article 35(3) lists three cases where a DPIA is always required:

- **(a)** Systematic and extensive evaluation of personal aspects relating to natural persons which is based on automated processing, including profiling, and on which decisions are based that produce legal effects concerning the natural person or similarly significantly affect them.
- **(b)** Processing on a large scale of special categories of data (Article 9) or personal data relating to criminal convictions and offences (Article 10).
- **(c)** A systematic monitoring of a publicly accessible area on a large scale.

The [Article 29 Working Party guidance WP 248 rev.01](https://ec.europa.eu/newsroom/article29/items/611236) — endorsed by the European Data Protection Board on its inaugural meeting — supplies nine criteria for identifying *likely high risk*; where two or more criteria are met, a DPIA is presumptively required:

1. Evaluation or scoring.
2. Automated decision-making with legal or similar significant effect.
3. Systematic monitoring.
4. Sensitive data or data of a highly personal nature.
5. Data processed on a large scale.
6. Matching or combining datasets.
7. Data concerning vulnerable data subjects.
8. Innovative use or applying new technological or organisational solutions.
9. When the processing in itself prevents data subjects from exercising a right or using a service or contract.

Most enterprise AI systems that process personal data hit at least *evaluation or scoring* + *innovative use or applying new technological solutions* (WP 248 criteria 1 and 8) — two criteria — and are therefore presumptively in scope. The analyst-tier default: on any AI system processing personal data, run the WP 248 filter as a first pass; document the outcome.

Each supervisory authority also publishes a list of processing operations for which a DPIA is *always* required under Article 35(4). The analyst checks the relevant supervisory authority's list for the jurisdictions where the enterprise processes personal data.

## The four required elements

Article 35(7) specifies the DPIA's minimum content:

- **(a)** A systematic description of the envisaged processing operations and the purposes of the processing, including, where applicable, the legitimate interest pursued by the controller.
- **(b)** An assessment of the necessity and proportionality of the processing operations in relation to the purposes.
- **(c)** An assessment of the risks to the rights and freedoms of data subjects referred to in paragraph 1.
- **(d)** The measures envisaged to address the risks, including safeguards, security measures and mechanisms to ensure the protection of personal data and to demonstrate compliance with this Regulation, taking into account the rights and legitimate interests of data subjects and other persons concerned.

Analyst-tier discipline: elements (a) and (d) are typically the largest sections; element (b) — necessity and proportionality — is the one under-populated in first drafts. *Necessity* asks whether the personal-data processing is required to achieve the stated purpose; *proportionality* asks whether the processing is limited to what is required. Both need explicit answers, not implicit ones.

## The DPO and Article 36 prior consultation

Two consultative obligations sit inside Article 35 and Article 36:

- **Article 35(2) — DPO consultation.** The controller *shall seek the advice of the data protection officer*, where designated, when carrying out a DPIA. The analyst records the DPO consultation as a related-artefact reference in the canonical document.

- **Article 36 — Prior consultation with the supervisory authority.** If the DPIA indicates the processing would result in a *high risk in the absence of measures taken by the controller to mitigate the risk*, the controller shall consult the supervisory authority before beginning the processing. The analyst-tier flag: any residual likelihood-magnitude in the register that lands *High* after mitigation, on a DPIA-in-scope system, is a candidate for Article 36 prior consultation. The analyst does not decide whether to trigger prior consultation — legal / privacy owns that — but the analyst *raises* it.

Enterprises often use the DPIA's residual-risk column as the trigger indicator. When residuals stay High, the DPIA cannot be closed without an Article 36 decision by the DPO or Head of Privacy.

## DPIA and FRIA overlap — the practical pattern

Article 27(4) of the AI Act permits reuse of an existing DPIA if it *complements* the FRIA. The pragmatic pattern most enterprises are settling into:

- **The DPIA is authored first** (Article 35 has been in force since 2018; DPO teams are staffed).
- **The FRIA is authored alongside or shortly after** the DPIA when the AI Act applies.
- **The two documents cross-reference** rather than duplicate. The DPIA covers data-protection rights depth; the FRIA covers the broader Charter of Fundamental Rights and adds the AI-specific elements (Article 13 provider info, human-oversight design, market-surveillance-authority notification).

A short overlap table the analyst carries at the head of both documents:

| Concern | DPIA covers | FRIA covers |
|---|---|---|
| Data protection (Charter Article 8) | Yes — this is the DPIA's purpose | By reference to the DPIA |
| Non-discrimination (Charter Article 21) | Only insofar as the discrimination is driven by personal-data processing | Yes — full scope |
| Human oversight of the AI system | Only as a data-protection mitigation | Yes — Article 27(1)(e) required element |
| Article 13 provider-info dependency | Not required | Yes — load-bearing |
| Market-surveillance-authority notification | Not applicable | Yes — Article 27(3) |
| Consultation of supervisory authority (residual high risk) | Article 36 GDPR | Not the FRIA's mechanism; but the FRIA can trigger separate scrutiny |

The DPO consults on the DPIA and reviews the FRIA. If the enterprise has a separate AI governance owner (a senior AI governance architect or head of AI governance), that owner co-signs the FRIA.

## Mapping the 42005 canonical document into the DPIA

The mapping the analyst uses:

| Article 35(7) element | Sourced from 42005 canonical section |
|---|---|
| (a) Systematic description of processing + purposes | System description + data description |
| (b) Necessity and proportionality | Treatment plan (rationale) + related-artefact reference to purpose-limitation analysis |
| (c) Risks to rights and freedoms | Enumerated impacts + analysis (subset touching personal-data processing) |
| (d) Measures to address risks | Treatment plan |

The gaps the analyst fills on top of the canonical document:

- **The necessity-and-proportionality narrative.** The canonical document says *what* is processed; the DPIA must say *why the processing is required* and *why less could not achieve the purpose*. This is often the most rewritten section.
- **The lawful-basis reference per Article 6 GDPR** — consent, contract, legal obligation, vital interests, public task, or legitimate interests. Not implied; stated. Where Article 9 special-category data is in scope, the additional Article 9(2) basis is stated.
- **The retention and international-transfer statements.** The canonical document holds these by reference to enterprise privacy schedules; the DPIA resolves the references.
- **The DPO opinion.** A short written opinion from the DPO on the DPIA, dated, is a load-bearing field.

## Concrete example — the MCDA-Benefits DPIA view

Reusing the MCDA-Benefits public-body deployment from chapter 03.

- **(a) Systematic description of processing and purposes.** MCDA-Benefits drafts response text for benefits-eligibility decisions. Personal data processed: applicant identifier, application details, prior-correspondence excerpts retrieved from case file. Processing occurs on the enterprise's tenant of Vendor V's hosted model API; prompt-plus-response pairs logged to internal audit store. Purpose: reduce caseworker drafting time; drive consistency of correspondence.
- **(b) Necessity and proportionality.** The processing is necessary because the drafting task requires reference to case-specific information; the same purpose cannot be achieved with anonymised or minimised data because the response must reference the specific application. Proportionality is enforced through prompt-scanning that removes fields not required for drafting (e.g., financial-account numbers, health-condition detail beyond the eligibility criterion) and through retention limits: audit-log retention 12 months, no long-term storage of the applicant's information in the retrieval index. Article 6 lawful basis: Article 6(1)(e) — task carried out in the public interest. Article 9 basis: not applicable (no Article 9 data used in the prompt after minimisation).
- **(c) Risks to rights and freedoms.** Draws directly from the canonical document register entries touching personal data: RR-2026-0311 (confabulation of eligibility criteria — accuracy risk to the data subject); RR-2026-0312 (data leakage in prompts — confidentiality risk); RR-2026-0313 (differential accuracy across language and literacy strata — non-discrimination risk); RR-2026-0314 (over-reliance by caseworker leading to less individualised assessment — Article 22 GDPR-adjacent automated-processing risk).
- **(d) Measures to address risks.** Human review of every draft; PII prompt-scanning per RR-2026-0312 mitigation; retrieval-only grounding on the case file; audit logging; vendor review VR-2026-0044; DPO opinion attached; residuals accepted at Medium for RR-2026-0311 and RR-2026-0313, Low for RR-2026-0312 and RR-2026-0314.

The DPO opinion is attached. Because residuals do not stay High after mitigation, Article 36 prior consultation is not triggered; this decision is recorded explicitly rather than left implicit.

## Where the DPIA stops for the analyst

- **Not the enterprise's data-protection policy.** The policy is enterprise-wide; the DPIA is per-processing.
- **Not the record of processing activities (Article 30).** The RoPA is a separate register the DPO team maintains; the DPIA references it.
- **Not a data-transfer-impact-assessment.** International transfers (Schrems II framework) may require an additional TIA; the DPIA references the TIA.
- **Not counsel's opinion.** The DPIA is an operational artefact; the legal characterisation of processing is counsel's. On Article 22 questions (solely-automated decisions with legal effect), the analyst flags for counsel — do not opine.

## What to memorise

- **The Article 35(1) general trigger** and the **Article 35(3)(a)/(b)/(c) always-required cases**.
- **The WP 248 nine-criteria filter** — two-or-more triggers a presumptive DPIA.
- **The four required elements** — processing description, necessity-and-proportionality, risks, measures.
- **The DPO consultation and Article 36 prior-consultation mechanics** — residual-High triggers the flag.
- **The DPIA / FRIA overlap table** — cross-reference, do not duplicate.

## Summary

The DPIA is required whenever a processing operation is likely to result in high risk to natural persons, presumptively so on most AI systems processing personal data. Article 35(7) enumerates four required elements — processing description, necessity-and-proportionality, risks, measures — and Article 36 requires prior consultation with the supervisory authority when residual risk stays High after mitigation. Analyst-tier authoring reuses the 42005 canonical document and fills the DPIA-specific extras: necessity-and-proportionality narrative, Article 6 lawful-basis reference, retention statement, DPO opinion. Where the AI Act applies, the DPIA and FRIA are authored alongside each other with a cross-reference table and no duplication.
