# Sector Regulators — FDA GMLP, Banking Model Risk, and Insurance Actuarial Oversight

## Why this chapter

Horizontal AI regulation (chapter 02, chapter 04) sits above the sector-regulator layer, not in place of it. When an AI system is used to decide whether to authorise a medical device, adjust a bank's credit-loss reserves, or price a life-insurance policy, the sector regulator's expectations engage in parallel with — and often in more operational detail than — the horizontal AI statute.

The analyst-tier tracker therefore holds a separate sector-overlays branch that is *not* jurisdiction-nested. A sector overlay applies across whichever jurisdictions the enterprise operates in — the FDA GMLP principles were developed jointly with the UK MHRA and Health Canada, and are cited well outside US SaMD submissions. The three most-cited overlays for an enterprise analyst to know:

- **Medical device software** — FDA GMLP + IMDRF SaMD framework + jurisdictional analogues.
- **Banking model risk** — [SR 11-7 (Federal Reserve)](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) / [OCC Bulletin 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) — model-risk management, applied to AI/ML models.
- **Insurance actuarial oversight** — [NAIC Model Bulletin on the Use of Artificial Intelligence Systems by Insurers](https://content.naic.org/sites/default/files/inline-files/2023-12-4%20Model%20Bulletin_Adopted_0.pdf) and state adoptions; EU EIOPA guidance for European insurers.

This chapter walks each overlay's scope trigger, core expectations, and tracker representation. The point is not depth in any one sector — the analyst is not a device-submission specialist, a model-risk manager, or a chief actuary — but the shape sufficient to know when a system's inventory row must inherit the overlay and when to route to the sector specialist inside the enterprise.

## FDA GMLP and the medical-device software overlay

The [FDA Good Machine Learning Practice for Medical Device Development: Guiding Principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles), first published October 2021 jointly with the UK [Medicines and Healthcare products Regulatory Agency (MHRA)](https://www.gov.uk/government/organisations/medicines-and-healthcare-products-regulatory-agency) and [Health Canada](https://www.canada.ca/en/health-canada.html), enumerates ten guiding principles:

1. Multi-disciplinary expertise is leveraged throughout the total product life cycle.
2. Good software engineering and security practices are implemented.
3. Clinical study participants and data sets are representative of the intended patient population.
4. Training data sets are independent of test sets.
5. Selected reference datasets are based upon best available methods.
6. Model design is tailored to the available data and reflects the intended use of the device.
7. Focus is placed on the performance of the human-AI team.
8. Testing demonstrates device performance during clinically relevant conditions.
9. Users are provided clear, essential information.
10. Deployed models are monitored for performance and re-training risks are managed.

The principles are **non-binding** — they are not a regulation. But they are cited by FDA in pre-submission and in reviewer feedback, and they set the practical expectation for what an AI/ML-enabled SaMD submission looks like. `mod-105` chapter 05 walks the sector-specific-impact-assessment overlay for the FDA context.

The regulatory instruments that carry actual force on the medical-device side:

- **[21 CFR Part 820](https://www.ecfr.gov/current/title-21/chapter-I/subchapter-H/part-820)** — Quality System Regulation (transitioning to the [Quality Management System Regulation (QMSR)](https://www.federalregister.gov/documents/2024/02/02/2024-01709/medical-devices-quality-system-regulation-amendments) aligned with ISO 13485, per the February 2024 final rule with a 2 February 2026 compliance date).
- **[21 CFR Part 807](https://www.ecfr.gov/current/title-21/chapter-I/subchapter-H/part-807) 510(k) premarket notification** or **[21 CFR Part 814](https://www.ecfr.gov/current/title-21/chapter-I/subchapter-H/part-814) premarket approval** — pathway depending on classification.
- **[Predetermined Change Control Plan (PCCP) guidance](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/marketing-submission-recommendations-predetermined-change-control-plan-artificial-intelligence)** — final December 2024; specifies how anticipated modifications to an AI/ML-enabled device can be pre-authorised without a new submission per change.
- **[IMDRF SaMD framework](https://www.imdrf.org/documents/software-medical-device-samd-key-definitions)** — International Medical Device Regulators Forum documents that harmonise SaMD terminology across jurisdictions.

Tracker rows for the medical-device overlay, minimum viable:

- `REG-2026-SEC-MED-001` — FDA SaMD framework + 21 CFR Parts 807/814/820 (transitioning to QMSR). Role: manufacturer.
- `REG-2026-SEC-MED-002` — FDA PCCP guidance for AI/ML-enabled devices. Role: manufacturer.
- `REG-2026-SEC-MED-003` — FDA GMLP guiding principles. Status: guidance — voluntary.
- `REG-2026-SEC-MED-004` — MHRA and Health Canada analogues (co-authored on GMLP; local implementation).
- `REG-2026-SEC-MED-005` — EU Medical Device Regulation (MDR) 2017/745 and In Vitro Diagnostic Regulation (IVDR) 2017/746 — where the enterprise's AI/ML software qualifies as a medical device or IVD under EU rules.

Where the enterprise is not the manufacturer but is a *user facility* deploying an authorised device — a common analyst-tier case in a hospital-system-plus-analyst context — the row's *role* is *user facility* and the obligation shifts to reporting, training, and post-market-surveillance participation rather than pre-market submission.

## Banking model risk — SR 11-7 and OCC 2011-12

The joint [SR 11-7 (Federal Reserve)](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) / [OCC Bulletin 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) *Supervisory Guidance on Model Risk Management* — issued April 2011 — is the load-bearing US banking-supervisory guidance on how banks manage the risk that a model's use produces adverse consequences from decisions based on incorrect or misused model outputs. It predates the current AI wave by a decade, but its shape is the reason US banks were structurally prepared for AI/ML model risk before the analytical wave arrived.

The guidance covers three components of the model-risk-management framework:

1. **Robust model development, implementation, and use.** Sound design, theory, and logic; comprehensive documentation; testing prior to production use.
2. **Sound model validation.** Effective challenge from parties independent of model development. Three elements to any validation: evaluation of conceptual soundness; ongoing monitoring including process verification and benchmarking; outcomes analysis including back-testing.
3. **Governance, policies, and controls.** Board and senior management oversight; a model inventory; policies and procedures; roles and responsibilities; internal audit's role.

`mod-103` chapter 04 walks the SR 11-7 shape as it applies to AI systems in financial services. The tracker for the banking-model-risk overlay:

- `REG-2026-SEC-BANK-001` — SR 11-7 / OCC 2011-12 — supervisory guidance on model-risk management. Applies to institutions supervised by the [Federal Reserve](https://www.federalreserve.gov/) and [OCC](https://www.occ.gov/) respectively; adopted or referenced by the [FDIC](https://www.fdic.gov/) and [NCUA](https://www.ncua.gov/) in analogous supervisory work.
- `REG-2026-SEC-BANK-002` — Model-inventory requirement (implicit in SR 11-7; explicit in bank internal-audit expectations).
- `REG-2026-SEC-BANK-003` — [Interagency Statement on the Use of Alternative Data in Credit Underwriting](https://www.federalreserve.gov/newsevents/pressreleases/files/bcreg20191203a1.pdf) (December 2019) — five-agency statement on consumer-protection implications of alternative data in AI-driven credit underwriting.
- `REG-2026-SEC-BANK-004` — [FRB SR 21-14 / OCC 2021-52 — third-party risk management](https://www.federalreserve.gov/supervisionreg/srletters/sr2114.htm) — where the AI/ML model is sourced from a third party.
- `REG-2026-SEC-BANK-005` — Non-US bank analogues — [European Central Bank guide to internal models](https://www.bankingsupervision.europa.eu/ecb/pub/pdf/ssm.guidetointernalmodels_consolidated_202310~b0f210cbb0.en.pdf); [Basel Committee](https://www.bis.org/bcbs/) principles on AI/ML in the banking supervisory context as they develop.

The *role* for banking-model-risk rows is *institution supervised by [primary regulator]*; the analyst names the primary supervisor for the enterprise's chartered institutions. Where the enterprise is a fintech that is not itself a chartered bank but that provides model-driven services to banks, the applicable framework is often the [FFIEC third-party-risk expectations](https://www.ffiec.gov/) rather than SR 11-7 directly.

## Insurance actuarial oversight — NAIC and EIOPA

The insurance-industry overlay has two anchor instruments:

- **US — [NAIC Model Bulletin on the Use of Artificial Intelligence Systems by Insurers](https://content.naic.org/sites/default/files/inline-files/2023-12-4%20Model%20Bulletin_Adopted_0.pdf)** — adopted 4 December 2023 by the National Association of Insurance Commissioners. A *model bulletin* is not itself law — insurance is regulated state-by-state in the US — but it is drafted for state insurance regulators to adopt into their own guidance, and a majority of states have done so or are in the process of doing so.
- **EU — [EIOPA Opinion on the Use of Artificial Intelligence in the Insurance Sector](https://www.eiopa.europa.eu/publications/opinion-artificial-intelligence-governance_en)** and subsequent guidance from the European Insurance and Occupational Pensions Authority. Layered on top of the EU AI Act (which classifies AI systems used for risk assessment and pricing in life and health insurance as Annex III high-risk).

### The NAIC Model Bulletin

The Model Bulletin sets out state-insurance-regulator expectations on insurers' governance of AI systems. Its core requirement is a documented AI Systems Program (AISP) covering:

- Governance — board and senior-management responsibilities, roles, and reporting lines.
- Risk management and internal controls — an inventory of AI systems used in decision-making across insurance functions; risk assessments proportional to the system's degree of decision-making and its consumer impact; testing and validation.
- Third-party AI systems and data — due diligence and oversight of third-party providers.
- Documentation — audit-facing evidence of the AISP.

The Bulletin distinguishes insurance functions where AI is used — underwriting, rating, pricing, claims handling, marketing, fraud detection — and expects proportional governance across the functions. It cross-references [NAIC Model Law #672 on Unfair Trade Practices](https://content.naic.org/model-laws) and long-standing state insurance non-discrimination provisions.

Tracker rows for the insurance overlay, minimum viable:

- `REG-2026-SEC-INS-001` — NAIC Model Bulletin — AISP requirement. Scope: insurers doing business in states that have adopted or referenced the Bulletin. Enforcement: state insurance department per state of licensure.
- `REG-2026-SEC-INS-002` — State-by-state adoption of the NAIC Model Bulletin. Row-body holds the state-adoption map, updated on the monthly deep read.
- `REG-2026-SEC-INS-003` — [Colorado Insurance Regulation 10-1-1](https://drive.google.com/file/d/16LZY-e9CyoxSpvsAmwjXfjKb9ITw2DEO/view) — testing and reporting of external-consumer-data-and-information-source-driven and algorithm-and-predictive-model-driven insurance practices. First state-specific insurance AI regulation.
- `REG-2026-SEC-INS-004` — EIOPA opinion + EU AI Act Annex III point 5(c) — life and health insurance risk assessment and pricing. Role: insurer (deployer, and — where applicable — provider).
- `REG-2026-SEC-INS-005` — [NY DFS Circular Letter on the Use of AI and External Consumer Data and Information Sources in Insurance Underwriting and Pricing](https://www.dfs.ny.gov/industry_guidance/circular_letters/cl2024_07) — New York-specific guidance.

The *role* for insurance-overlay rows is *insurer authorised in [state or member state]*; the analyst names the specific state or EU member-state authorisations that engage.

## The pattern — every sector overlay pairs a scope trigger with a specialist inside the enterprise

The sector overlays are the branch of the tracker where the analyst's *scope of role* framing (`mod-101` chapter 06) matters most. The analyst is not the specialist. In each sector, an enterprise-internal specialist holds the depth:

| Overlay | Enterprise-internal specialist |
|---|---|
| FDA / MDR SaMD | Regulatory affairs / quality assurance |
| SR 11-7 / OCC 2011-12 model risk | Model risk management (MRM) team |
| NAIC Model Bulletin / state insurance AISP | Chief actuary / product-actuarial / insurance-compliance |

The analyst-tier discipline: for each sector overlay row in the tracker, the *notes for counsel* column carries a second name — *routed to [specialist team / role]*. When a change lands in that overlay (chapter 10), the change note goes to both counsel and the specialist team. The analyst does not opine on the sector-specific details.

Where the enterprise has no sector-specialist team — because it is not in the sector — the sector overlay row still exists but its scope trigger is unmet and the row's status is *no in-scope systems; row retained as horizon-scan*.

## Where the sector-overlays branch stops for the analyst

- **Not the medical-device submission.** The 510(k) or PMA submission is a regulatory-affairs artefact; the analyst records the fact of submission and cites the FDA-authorised device listing entry.
- **Not the model-validation report.** The independent model validation under SR 11-7 is authored by the MRM team; the analyst records the fact of validation and cites the validation report in the impact-assessment corpus.
- **Not the actuarial pricing memo.** The actuarial rationale for a rating factor is a chief-actuary artefact; the analyst records that the rating decision engaged an AI system and that the AISP process was followed.
- **Not the specialist opinion.** Every sector overlay has its own specialists; the analyst frames the obligation and routes to the specialist.

## What to memorise

- **The three anchor overlays** — medical-device (FDA GMLP + SaMD + PCCP + MDR/IVDR), banking model risk (SR 11-7 / OCC 2011-12), insurance actuarial (NAIC Model Bulletin + EIOPA + state analogues).
- **Sector overlays are not jurisdiction-nested** — a single overlay applies across whichever jurisdictions the enterprise operates in that are covered by that sector regulator.
- **FDA GMLP is guidance, not regulation** — the underlying US regulation is 21 CFR Parts 807/814/820, transitioning to QMSR; GMLP is cited in submissions and reviewer feedback.
- **SR 11-7 predates AI/ML** — its three components (development / validation / governance) apply cleanly to AI/ML models; the model inventory is a key evidence artefact.
- **NAIC Model Bulletin is a template for state adoption** — the tracker holds a state-adoption map that is refreshed monthly.
- **The specialist-routing discipline** — every sector overlay row names the enterprise-internal specialist alongside the analyst's tracker entry.

## Summary

The sector-overlays branch of the tracker sits alongside the jurisdictional branches and holds obligations that apply across jurisdictions where the enterprise operates. Medical-device software engages FDA GMLP guiding principles layered on 21 CFR Parts 807/814/820 (transitioning to QMSR) with PCCP as the change-control mechanism for AI/ML-enabled devices; the same shape is cited in MHRA and Health Canada regulatory activity and in EU MDR/IVDR conformity work. Banking model risk engages SR 11-7 / OCC 2011-12 supervisory guidance on model-risk management, applied to AI/ML models within the three-component (development / validation / governance) framework. Insurance actuarial oversight engages the NAIC Model Bulletin as adopted by individual state insurance departments, layered on top of EIOPA guidance and EU AI Act Annex III point 5(c) for European insurers. In every case the analyst names the obligation, records the affected inventory rows, and routes to the enterprise-internal specialist — regulatory affairs / model risk management / chief actuary — for the sector-specific depth. Chapter 07 develops the privacy-law flagging discipline that decides when to hand off to counsel; chapter 10 covers the change-note that routes an overlay update to the affected system owners.
