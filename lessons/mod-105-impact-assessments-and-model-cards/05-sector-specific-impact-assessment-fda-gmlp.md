# Sector-Specific Impact Assessments — The FDA Good ML Practice Slice

## Why this chapter

The AIA, FRIA, and DPIA in the previous chapters are *horizontal* impact assessments — they apply across sectors when their scoping conditions are met. Sector regulators add *vertical* overlays that reshape the impact-assessment obligation for a specific industry.

For AI systems in medical devices, the load-bearing overlay in the United States is the [FDA's marketing pathway for software as a medical device (SaMD)](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-and-machine-learning-software-medical-device) combined with the joint FDA / Health Canada / MHRA *Good Machine Learning Practice for Medical Device Development: Guiding Principles*. Those principles do not themselves prescribe a form. They do prescribe the shape of the evidence that a device sponsor produces during a pre-market submission — and the pre-market submission itself takes an impact-assessment-shaped set of information about the device and its intended use.

This chapter walks the GMLP guiding principles, the pre-market submission slice that maps most cleanly to the analyst's canonical document, and — critically — the divide between what an enterprise AI governance analyst produces and what a regulated device sponsor's regulatory-affairs team owns.

## Where sector-specific IAs sit

Sector-specific impact assessments are not a replacement for the horizontal instruments. A medical-device deployer in the EU still owes the DPIA and, where the device is a high-risk AI system in a public-body deployment, may still owe the FRIA. The sector overlay adds specific evidence, specific documentary sections, and specific approval steps *on top of* the horizontal shape.

Common sector overlays the analyst will meet:

- **Medical devices** — [FDA SaMD guidance](https://www.fda.gov/medical-devices/software-medical-device-samd), FDA / Health Canada / MHRA GMLP guiding principles, [EU Medical Device Regulation (MDR)](https://eur-lex.europa.eu/eli/reg/2017/745/oj), [In Vitro Diagnostic Regulation (IVDR)](https://eur-lex.europa.eu/eli/reg/2017/746/oj).
- **Financial services** — [SR 11-7 model risk management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) covered in `mod-103` chapter 04; [OCC Bulletin 2011-12](https://www.occ.treas.gov/news-issuances/bulletins/2011/bulletin-2011-12.html); [FDIC FIL-22-2017](https://www.fdic.gov/news/financial-institution-letters/2017/fil17022.html); consumer-credit rules under [ECOA / Regulation B](https://www.consumerfinance.gov/rules-policy/regulations/1002/) and [CFPB Circular 2022-03](https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/).
- **Employment and hiring** — [NYC LL 144](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) covered in `mod-104` chapter 04; [Colorado SB 24-205](https://leg.colorado.gov/bills/sb24-205); state-by-state statutes tracked in `mod-106`.
- **Insurance** — [NAIC Model Bulletin on Use of AI Systems by Insurers](https://content.naic.org/sites/default/files/inline-files/2023-12-4%20Model%20Bulletin_Adopted_0.pdf); state department-of-insurance guidance.
- **Education** — [FERPA](https://studentprivacy.ed.gov/ferpa) considerations for student-record processing; state-by-state student-data statutes.

This chapter walks the FDA / GMLP slice as the worked example because it is well-published, internationally-coordinated, and its evidence shape is the most legible to the AI governance analyst. The other sector overlays follow a similar analyst-versus-specialist division.

## The GMLP guiding principles

In October 2021, the FDA, Health Canada, and the UK MHRA jointly published [Good Machine Learning Practice for Medical Device Development: Guiding Principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) — ten principles at the level of intent rather than prescription. Paraphrased:

1. **Multi-disciplinary expertise** is leveraged throughout the total product life cycle.
2. **Good software engineering and security practices** are implemented.
3. **Clinical study participants and datasets** are representative of the intended patient population.
4. **Training datasets are independent** of test sets.
5. **Selected reference datasets** are based upon best available methods.
6. **Model design** is tailored to the available data and reflects the intended use of the device.
7. **Focus is placed on the performance of the human-AI team.**
8. **Testing demonstrates device performance** during clinically relevant conditions.
9. **Users are provided clear, essential information.**
10. **Deployed models are monitored** for performance and re-training risks are managed.

Two follow-on documents extend the ten principles. The FDA published [Transparency for Machine Learning-Enabled Medical Devices: Guiding Principles (2024)](https://www.fda.gov/medical-devices/software-medical-device-samd/transparency-machine-learning-enabled-medical-devices-guiding-principles) — expanding principle 9 — and, jointly with the UK MHRA and Health Canada, [Predetermined Change Control Plans for Machine Learning-Enabled Medical Devices: Guiding Principles (2023)](https://www.fda.gov/medical-devices/software-medical-device-samd/predetermined-change-control-plans-machine-learning-enabled-medical-devices) — extending principle 10.

The guiding principles do not have the force of rulemaking. They shape what an FDA reviewer expects to see in a 510(k), De Novo, or PMA submission for a machine-learning-enabled device.

## Where the pre-market submission needs impact-assessment-shaped evidence

An FDA pre-market submission for a machine-learning-enabled device (SaMD or hardware-embedded) contains, among many other things, a set of *device description and intended-use* sections that map to the analyst's canonical 42005 document:

- **Indications for use / intended use.** Who the device is for; what condition; what setting. Aligns with 42005 *system description* + *affected-stakeholder inventory*.
- **Device description.** Model family, inputs, outputs, deployment mode. Aligns with 42005 *system description* + *data description*.
- **Human factors and usability engineering.** How clinicians interact with the device. Aligns with 42005 *treatment plan (oversight controls)*.
- **Performance evaluation and clinical performance evidence.** Test-set performance, sub-group performance, clinical study data. Aligns with 42005 *enumerated impacts + analysis* + related-artefact reference to the eval report.
- **Risk management file per ISO 14971.** The device-specific risk-management file. Overlaps with the 42005 *enumerated impacts + treatment plan*, but is a distinct artefact governed by [ISO 14971 — Medical devices — Application of risk management](https://www.iso.org/standard/72704.html), and it is the *device sponsor's regulatory-affairs* artefact.
- **Post-market surveillance plan.** How performance is monitored after deployment. Aligns with 42005 *review triggers and cadence*.
- **Labelling — the instructions for use.** Communicated to the clinical user. Aligns with related-artefact reference to model card.
- **Predetermined change control plan (where applicable).** How planned model updates will be managed without a new 510(k). Aligns with 42005 *review triggers and cadence* + change-management controls.

The analyst-tier discipline: for a device use case, the 42005 canonical document is authored as one input to the submission, not as the submission itself. Regulatory affairs assembles the submission and owns the risk-management file per ISO 14971. The analyst's canonical document supplies the intended-use, stakeholder, and impact narrative — and the analyst is the coordination point between the enterprise AI governance function and the regulatory affairs function.

## Mapping the 42005 canonical document into the sector-specific view

For the FDA / GMLP overlay, the mapping is not a straight one-for-one; the analyst produces a *contribution packet* the regulatory-affairs team reuses inside their submission:

| GMLP / submission element | Sourced from 42005 canonical section |
|---|---|
| Indications for use / intended use | System description + affected-stakeholder inventory |
| Device description (from a governance angle) | System description + data description |
| Human-AI team performance framing (Principle 7) | Treatment plan (oversight controls) |
| Sub-group performance framing (Principle 3, 8) | Enumerated impacts + reference to bias-review note from `mod-104` |
| Post-market monitoring intent (Principle 10) | Review triggers and cadence |
| Predetermined change control plan intent | Review triggers and cadence + change-management controls |
| Transparency / instructions-for-use content (Principle 9) | Related-artefact reference to model card |

The gaps the analyst does *not* fill on the sector view:

- ISO 14971 risk-management file (regulatory-affairs owns).
- Clinical performance analysis and statistical inference (biostatistics and clinical-evaluation owns).
- Predetermined change control plan mechanics (regulatory-affairs plus ML engineering).
- Labelling regulatory language (regulatory-affairs plus legal).

The analyst-tier gap that the analyst *does* fill: the *governance-side representation* of the same intended-use and post-market monitoring story that appears in the submission. This gives the enterprise a single internal source-of-truth even when the regulatory submission itself is owned elsewhere.

## Concrete example — the MCDA-Radiology sector view

Suppose an entirely different device use case that reuses the analyst's canonical-document machinery: MCDA-Radiology, a draft-radiology-report assistant for internal radiologist use in a US hospital system, using a hosted foundation model with retrieval-augmented grounding on the enterprise's imaging-report corpus. This is a candidate SaMD — the FDA has been explicit that generative-AI clinical draft tools may cross into SaMD depending on intended use.

The canonical document, before any sector overlay, is authored as in chapter 01. The analyst's sector contribution packet to regulatory affairs:

- **Indications for use.** Assistive drafting of radiology reports for review by a board-certified radiologist prior to sign-off; not intended for use as an autonomous diagnostic tool; not intended for use in pediatric imaging (out-of-scope population).
- **Device description contribution.** Hosted foundation model MCDA-Radiology-v1; inputs: DICOM report metadata and prior-report retrieval; outputs: draft text for radiologist review; log: prompt-plus-output pairs stored per enterprise retention policy.
- **Human-AI team framing (Principle 7).** Every draft is edited by a radiologist before sign-off; no draft is auto-committed; sign-off is the medical decision, not the draft.
- **Sub-group framing (Principle 3, 8).** Reference to bias-review note BR-2026-0117 (from `mod-104`), covering performance by patient sex, age band, and imaging modality; contribution recommends the regulatory-affairs team add clinical-performance evaluation across the same strata.
- **Post-market monitoring intent (Principle 10).** Monthly review of draft-edit-distance and radiologist-flagged inaccuracy rate; quarterly re-baseline against a held-out set; incident-response plan IR-2026-0011.
- **Change-control intent.** Any change to the underlying foundation model version, prompt template major rev, or retrieval index scope triggers a review pass; regulatory-affairs is the owner of the change-control plan itself.
- **Transparency contribution.** Reference to model card MC-2026-0044-Radiology-v1 and the intended-clinician-facing instructions-for-use draft.

Regulatory affairs takes this packet, folds it into the 510(k) / De Novo submission alongside the ISO 14971 file, the clinical performance evidence, and the labelling, and files. The analyst's contribution is one internal input; the submission is the sponsor's.

## Where the sector-specific IA stops for the analyst

- **Not the regulatory submission itself.** The submission is prepared and filed by regulatory affairs; the analyst supplies governance-side inputs.
- **Not the ISO 14971 risk-management file.** That file is device-specific and belongs to regulatory affairs / quality.
- **Not clinical evaluation.** Clinical-performance evidence is generated by the clinical-evaluation team; the analyst references the resulting report.
- **Not the predetermined change control plan mechanics.** The analyst's canonical document references the change-control plan; regulatory affairs and ML engineering own the plan.
- **Not the equivalent for other sectors uncritically.** Financial-services model risk under SR 11-7 (chapter 04 of `mod-103`) has its own three-pillar shape; insurance under the NAIC Model Bulletin has its own; the analyst does not reuse the FDA slice verbatim in another sector.

## What to memorise

- **The horizontal-plus-vertical model.** Sector overlays are on top of AIA / FRIA / DPIA, not instead of.
- **The ten GMLP guiding principles at intent level** — you do not need verbatim wording, but you must know they exist and are the shape FDA reviewers expect.
- **The pre-market-submission element-to-42005 mapping** — intended use, device description, human-factors, performance evidence, ISO 14971 file, post-market surveillance, labelling, predetermined change control plan.
- **The analyst / regulatory-affairs boundary** — analyst supplies the governance contribution packet; regulatory affairs owns the submission.

## Summary

Sector regulators layer vertical overlays on top of the horizontal AIA / FRIA / DPIA obligations. The FDA / Health Canada / MHRA Good Machine Learning Practice guiding principles are the analyst-legible shape of the medical-device overlay; the pre-market submission needs impact-assessment-shaped evidence about intended use, human-AI team performance, sub-group performance, post-market monitoring, and transparency. Analyst-tier work on a sector overlay is a *contribution packet* to the specialist team — regulatory affairs for medical devices, model risk management for financial services, department-of-insurance liaison for insurance. The analyst's canonical 42005 document is the single internal source-of-truth from which the contribution packet is derived.
