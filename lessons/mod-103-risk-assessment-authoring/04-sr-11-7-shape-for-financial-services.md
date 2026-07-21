# SR 11-7 Shape — Model Risk for Regulated Financial Institutions

## Why this chapter

Financial-services enterprises have been running Model Risk Management (MRM) programs long before "AI governance" acquired a name. The reference document is [US Federal Reserve SR 11-7 (2011)](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm), companion to [OCC Bulletin 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) and, informally, the shape most non-US regulators emulate.

SR 11-7 is not an AI standard. It is a *model risk* standard — where "model" means any quantitative method used for decision-making, from a spreadsheet-based credit-scoring rule to a deep-learning fraud detector. When an enterprise's AI governance work happens inside a bank, insurer, or asset manager, the analyst's first-draft risk assessment has to speak SR 11-7's vocabulary alongside NIST AI RMF and ISO/IEC 42001.

You are not becoming a model-risk officer. You are becoming fluent enough to (a) map an AI risk assessment onto the SR 11-7 shape when the enterprise requires it, and (b) route to a Model Risk Management group cleanly.

## What SR 11-7 says at analyst-tier depth

SR 11-7 defines a model as *"a quantitative method, system, or approach that applies statistical, economic, financial, or mathematical theories, techniques, and assumptions to process input data into quantitative estimates."* That definition is broad enough to cover every ML / AI system the analyst will meet in a regulated financial institution.

The guidance rests on three pillars.

### 1. Robust model development, implementation, and use

- Models are developed with clear purpose statements, documented methodology, and defensible assumptions.
- Model outputs are used within the intended purpose; boundaries and known limitations are explicit.
- Documentation is complete enough that a competent third party can reconstruct the model.

### 2. Sound model validation

- Independent validation before use and periodically thereafter.
- Includes conceptual soundness review, ongoing monitoring, and outcomes analysis.
- Validators are independent of developers.

### 3. Governance, policies, and controls

- Board-approved model risk policy.
- Clear roles and responsibilities.
- Model inventory.
- Reporting on model risk to senior management.

The three pillars are the *shape* the analyst maps AI RMF and ISO/IEC 42001 output into when the enterprise is a regulated FSI.

## Mapping AI RMF and ISO 42001 to SR 11-7

The good news is that every serious AI framework overlaps SR 11-7 substantially. The mapping the analyst files:

| SR 11-7 pillar | NIST AI RMF anchor | ISO/IEC 42001 anchor |
|---|---|---|
| Development, implementation, and use | MAP 2 (categorisation and methods), MAP 3 (scope), MEASURE 2 (evaluation) | Clause 8.2 (AI system operation), Annex A controls on documentation |
| Independent validation | MEASURE 2, MEASURE 3, MEASURE 4 | Clause 9 (performance evaluation), Annex A controls on internal audit |
| Governance | GOVERN 1, GOVERN 2, GOVERN 6 | Clauses 5 (Leadership), 7 (Support), Statement of Applicability |

Analyst-tier work: when a use case is FSI, the first-draft risk assessment carries a table like the above with the specific artefacts filled in (which document evidences MAP 2 for this system; which validation report evidences MEASURE 3, etc.).

## What SR 11-7 adds that AI RMF alone does not

SR 11-7 predates modern AI framing and adds three things the NIST AI RMF does not spell out at the same depth.

- **Explicit distinction between developer and validator.** MEASURE says the model must be evaluated. SR 11-7 says the evaluator must be *independent of the developer* — and that independence is a formal role. In FSI programs, MRM is a separate reporting line from the ML team. The analyst records the independence explicitly.
- **Model tiering by materiality.** SR 11-7 asks the enterprise to tier its models by materiality — how central to a business decision, how large the potential loss. High-materiality models get more validation intensity. This is a peer of the EU AI Act tier but framed around monetary and decision-materiality rather than fundamental rights.
- **Ongoing performance monitoring is mandatory, not optional.** SR 11-7 requires ongoing monitoring for material models — outcomes analysis, back-testing, benchmarking. In practice this is where AI-specific monitoring (concept drift, fairness monitors, calibration monitors) plugs in.

The analyst's job is to know these exist and cite them where the FSI framing calls for it.

## The model inventory in an FSI

The FSI equivalent of the AI system inventory is the *model inventory* — required explicitly by SR 11-7. In an FSI, the AI governance inventory *is* (or is a slice of) the model inventory. The analyst-tier work is to keep the AI slice populated to the standard the MRM group expects — which typically means additional fields the general AI inventory row does not carry.

Additional FSI-specific fields:

- **Model tier / materiality rating** — the SR 11-7 tier.
- **Validation status** — *pre-validation / conditionally approved / approved / suspended / retired*.
- **Last validation date** and **next validation due.**
- **Validator name** — the individual owning the validation record.
- **Assumptions and limitations** — a formal field carrying the developer's stated boundaries.
- **Compensating controls** — the controls that address known limitations.

## What SR 11-7 does not cover — where AI-specific overlays add

SR 11-7 was published in 2011. It is silent on modern AI-specific concerns:

- **Foundation-model providers** — SR 11-7 was written for internal models. Hosted third-party LLMs stress the guidance's assumptions on developer control and validation-data access. The [OCC 2020-10 Bulletin on Model Risk Management](https://www.occ.gov/news-issuances/bulletins/2020/bulletin-2020-10.html) starts to address third-party model use; the OCC third-party risk guidance ([OCC 2013-29 / 2023-17](https://www.occ.gov/news-issuances/bulletins/2023/bulletin-2023-17.html)) complements it. Analyst-tier work: cite both bulletins when the model is third-party hosted.
- **Fairness and bias** — SR 11-7 does not use those words. Overlay [CFPB circular 2022-03 on adverse action notices for algorithmic decisions](https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/) and the underlying [ECOA / Regulation B](https://www.consumerfinance.gov/rules-policy/regulations/1002/) for consumer-finance systems.
- **Generative AI-specific risks** — SR 11-7 does not name Confabulation, Prompt Injection, or IP contamination. The NIST GenAI Profile fills the gap; the analyst cites the Profile risks in the FSI framing.

<!-- needs-research: verify the latest supervisory guidance letters that OCC, Federal Reserve, and FDIC have published on AI / model use; the 2020s have produced multiple companion pieces and the analyst-facing citation should track the current supervisory posture. -->

## When SR 11-7 does *not* apply

- **Non-FSI enterprises.** SR 11-7 is US federally-regulated banking guidance. Non-banks — retail, healthcare, tech, marketing — do not fall under it directly, though they sometimes adopt the vocabulary for maturity.
- **Non-US FSI.** [ECB Guide to Internal Models](https://www.bankingsupervision.europa.eu/) and [PRA SS1/23 on model risk management](https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss) are the EU and UK peer references. The shape is similar; the analyst cites the correct instrument for the jurisdiction.
- **Systems that do not meet the SR 11-7 model definition.** Purely rules-based systems, chat routing without ML, retrieval-only tools — the FSI's MRM group typically tiers these out. The analyst confirms tiering with the MRM group before excluding.

## Concrete example — MCDA if the enterprise were an FSI

Imagine MCDA were being deployed at a regional bank rather than a consumer-brand company. The analyst-tier delta:

- **Model tier / materiality:** Low. Marketing copy is not a credit or safety-of-funds decision, but internal MRM policy typically requires all models to be inventoried and tiered.
- **Independent validation:** Delegated to MRM group — a lighter-touch validation for a Low-materiality model, but on record.
- **Assumptions and limitations:** Carried on the inventory row: "assistive; not authoritative for regulatory disclosures; no use in loan-approval-adjacent content."
- **Additional overlays:** [SR 11-7 pillar 2](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) validation requirements; OCC 2023-17 third-party risk (Vendor V is a third-party model provider); ECOA / Regulation B if any marketing copy references credit products (adverse-action-notice overlay).
- **Register-entry framing:** Confabulation and IP-contamination risks would be routed additionally to MRM (validation), Compliance (advertising regulation), and Legal (Regulation B if credit copy is generated).

The point is not that FSI framing changes the analytical work — it does not. It adds an overlay that ties the analyst's output into an existing MRM process the enterprise has been running for over a decade.

## What to memorise

- The **three SR 11-7 pillars**: development / implementation / use; independent validation; governance.
- The **mapping table** — SR 11-7 pillar ↔ NIST AI RMF anchor ↔ ISO 42001 anchor.
- The **three FSI-specific additions**: developer/validator independence; materiality tiering; mandatory ongoing monitoring.
- The **FSI-specific inventory fields**: tier, validation status, validation dates, validator name, assumptions/limitations, compensating controls.
- The **overlays SR 11-7 does not cover** — foundation-model third-party guidance (OCC 2020-10, OCC 2023-17); fairness (CFPB 2022-03, ECOA); GenAI risks (NIST GenAI Profile).
- The **jurisdictional peers**: ECB Guide to Internal Models (EU); PRA SS1/23 (UK).

## Summary

SR 11-7 is the US financial-services shape most AI governance programs at banks, insurers, and asset managers layer over the NIST AI RMF + ISO/IEC 42001 stack. It adds developer/validator independence, materiality tiering, and mandatory ongoing monitoring — none of which the NIST framework spells out at the same depth. The analyst maps AI RMF and ISO 42001 output onto the three SR 11-7 pillars, adds the FSI-specific inventory fields, and reaches for OCC / CFPB / ECOA overlays for third-party and fairness gaps SR 11-7 predates. Non-FSI enterprises do not fall under SR 11-7 directly; non-US FSIs use ECB or PRA peers.
