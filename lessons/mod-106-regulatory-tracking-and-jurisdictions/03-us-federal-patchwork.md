# The US Federal Patchwork — EEOC, FTC, HHS, FDA, and Executive Orders

## Why this chapter

Unlike the EU stack (chapter 02), the US federal AI-governance landscape is not a single horizontal regulation. There is no US AI Act. What there is instead is a set of long-standing sector regulators and civil-rights enforcers who have made clear — through enforcement, guidance, and joint statements — that their existing statutory authorities cover AI systems in their domain. Layered on top is a shifting set of White House executive orders that direct federal-agency behaviour and — with some indirect force — private-sector expectations.

For the tracker, the US federal branch is therefore not organised around a single instrument. It is organised around the regulator: for each enforcement authority the analyst tracks the authority's statutory hooks, its most-cited AI-relevant guidance, and any enforcement actions that signal how it reads its own authority. This chapter walks the five most-cited authorities, positions the executive-order layer, and describes how to track a landscape where the *instrument* field of the tracker changes more often than the *authority* field.

## The joint statement — five authorities agreeing they already have authority

The load-bearing artefact for the analyst is the [Joint Statement on Enforcement Efforts Against Discrimination and Bias in Automated Systems](https://www.eeoc.gov/joint-statement-enforcement-efforts-against-discrimination-and-bias-automated-systems), first issued 25 April 2023 and re-affirmed 12 April 2024, signed by the CFPB, DOJ Civil Rights Division, EEOC, and FTC. The statement's plain reading: existing federal law prohibits discrimination and other harms in automated systems, and the four signing authorities intend to enforce those laws against AI-driven violations.

The statement matters because it is the authoritative pushback against the argument *there is no federal law on AI*. The reply is: *there is federal law on hiring discrimination (Title VII), on consumer credit (ECOA), on unfair or deceptive practices (Section 5 of the FTC Act), on housing (Fair Housing Act) — those laws apply when a hiring decision, a credit decision, a marketing claim, or a housing-related determination is made by an AI system*.

The analyst-tier reading: for every US-federal tracker row, the row's *scope trigger* names the substantive statute the authority enforces, not just the authority's name. *EEOC* is not a scope trigger; *EEOC enforcement of Title VII / ADA / ADEA on AI-mediated employment decisions* is.

## EEOC — employment discrimination

The [Equal Employment Opportunity Commission](https://www.eeoc.gov/) enforces:

- **[Title VII of the Civil Rights Act of 1964](https://www.eeoc.gov/statutes/title-vii-civil-rights-act-1964)** — prohibits employment discrimination on the basis of race, color, religion, sex (including pregnancy, sexual orientation, and gender identity), and national origin. The load-bearing standard for AI systems is the *disparate impact* doctrine — a facially-neutral practice that has an adverse impact on a protected class, absent a bona fide job-related justification, is unlawful.
- **[Americans with Disabilities Act (ADA)](https://www.eeoc.gov/statutes/americans-disabilities-act-1990-original-text)** — prohibits discrimination against qualified individuals on the basis of disability; requires reasonable accommodation. AI hiring tools that screen out otherwise-qualified applicants with disabilities are a specific EEOC concern.
- **[Age Discrimination in Employment Act (ADEA)](https://www.eeoc.gov/statutes/age-discrimination-employment-act-1967)** — prohibits employment discrimination against persons 40 or older.

Two guidance documents the tracker cites:

- **[EEOC technical-assistance document on the ADA and AI in employment decisions](https://www.eeoc.gov/laws/guidance/americans-disabilities-act-and-use-software-algorithms-and-artificial-intelligence)** (May 2022) — sets out how the ADA applies to AI-driven employment tools, and specifically the reasonable-accommodation and disability-related-inquiry rules.
- **[EEOC technical-assistance document on Title VII and AI](https://www.eeoc.gov/select-issues-assessing-adverse-impact-software-algorithms-and-artificial-intelligence-used)** (May 2023) — sets out how disparate-impact analysis (including the four-fifths rule from the Uniform Guidelines on Employee Selection Procedures) applies to AI selection tools.

The [Uniform Guidelines on Employee Selection Procedures (29 CFR Part 1607)](https://www.ecfr.gov/current/title-29/subtitle-B/chapter-XIV/part-1607) — the *four-fifths rule* — is the operational rule of thumb the EEOC and DOJ apply to selection tools. `mod-104` chapter 04 develops the fairness-metric context.

## FTC — unfair or deceptive practices and consumer protection

The [Federal Trade Commission](https://www.ftc.gov/) enforces:

- **[Section 5 of the FTC Act](https://www.ftc.gov/legal-library/browse/statutes/federal-trade-commission-act)** — prohibits unfair or deceptive acts or practices affecting commerce. Applied to AI in two shapes: (a) *deceptive* — false or unsubstantiated claims about an AI system's capabilities; (b) *unfair* — an AI system that causes or is likely to cause substantial injury to consumers not reasonably avoidable and not outweighed by countervailing benefits.
- **[Section 5 unfair-methods-of-competition authority](https://www.ftc.gov/system/files/ftc_gov/pdf/P221202Section5PolicyStatement.pdf)** — the FTC has re-asserted a broad unfair-methods reading; relevant where AI systems are used in ways that harm competition.
- **[Fair Credit Reporting Act (FCRA)](https://www.ftc.gov/legal-library/browse/statutes/fair-credit-reporting-act)** — applies whenever an AI system generates a *consumer report* used for credit, employment, insurance, housing, or other permissible purpose.
- **[Equal Credit Opportunity Act (ECOA)](https://www.ftc.gov/legal-library/browse/statutes/equal-credit-opportunity-act) / Regulation B** — prohibits discrimination in any aspect of a credit transaction on prohibited bases; applies to AI-driven credit-decision systems.
- **[COPPA](https://www.ftc.gov/legal-library/browse/rules/childrens-online-privacy-protection-rule-coppa)** — applies to any AI system directed at children under 13 or with actual knowledge of collecting personal information from them.

FTC business-guidance blogs, staff reports, and enforcement actions signal expectations well before formal rulemakings. The tracker holds staff-guidance URLs in the *primary-source URLs* column with the note *guidance — not a regulation but cited in enforcement*.

## HHS — health-programme non-discrimination and privacy

Two HHS units carry AI-relevant enforcement authority:

- **[HHS Office for Civil Rights (OCR)](https://www.hhs.gov/ocr/index.html)** — enforces [Section 1557 of the Affordable Care Act](https://www.hhs.gov/civil-rights/for-individuals/section-1557/index.html), which prohibits discrimination on the basis of race, color, national origin, sex (including sexual orientation and gender identity), age, and disability in covered health programmes and activities. The [May 2024 Section 1557 final rule](https://www.federalregister.gov/documents/2024/05/06/2024-08711/nondiscrimination-in-health-programs-and-activities) at [45 CFR 92.210](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-A/part-92) addressed AI and clinical algorithms explicitly, requiring covered entities to make reasonable efforts to identify and mitigate discrimination arising from the use of *patient care decision support tools*.
- **HHS OCR — HIPAA enforcement.** The [HIPAA Privacy, Security, and Breach Notification Rules (45 CFR Parts 160 and 164)](https://www.hhs.gov/hipaa/for-professionals/index.html) apply whenever protected health information is used by an AI system. Business-associate agreements (BAAs) attach to AI vendors that touch PHI on behalf of covered entities. Chapter 07 develops the HIPAA flagging discipline.

<!-- needs-research: the Section 1557 rule provisions on patient-care decision support tools were subject to legal challenge in 2024–2025; verify the current enforcement posture and any injunctive relief in force before citing the specific provision to a covered entity. -->

## FDA — medical-device software (SaMD) and Good Machine Learning Practice

The [Food and Drug Administration](https://www.fda.gov/) regulates AI-enabled software as a medical device (SaMD) where the software meets the [21 U.S.C. §321(h) device definition](https://www.fda.gov/medical-devices/classify-your-medical-device/how-determine-if-your-product-medical-device). The tracker rows most-often cited:

- **[Software as a Medical Device (SaMD) framework](https://www.fda.gov/medical-devices/digital-health-center-excellence/software-medical-device-samd)** — the pathway through which AI-enabled clinical software is authorised (510(k), De Novo, or PMA depending on classification).
- **[Predetermined Change Control Plan (PCCP) guidance](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/marketing-submission-recommendations-predetermined-change-control-plan-artificial-intelligence)** — final guidance December 2024 on how a manufacturer can pre-specify anticipated modifications to an AI/ML-enabled device without a new marketing submission for each change.
- **[Good Machine Learning Practice for Medical Device Development: Guiding Principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles)** (October 2021, updated) — ten guiding principles jointly with UK MHRA and Health Canada. Non-binding but referenced in submissions. Chapter 06 (sector regulators) develops GMLP.
- **[FDA-listed AI/ML-enabled medical devices](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-and-machine-learning-aiml-enabled-medical-devices)** — the FDA maintains a public list of authorised AI/ML-enabled medical devices; useful as evidence for the *this device class has been authorised through this pathway* framing.

The tracker's *role* column for FDA rows is either *manufacturer* (when the enterprise develops the AI-enabled device) or *user facility / practitioner* (when the enterprise deploys an already-authorised device); the obligations differ substantially.

## White House executive orders — the shifting overlay

Executive orders direct federal agencies. They do not, on their own, create private-sector obligations. But two indirect effects matter for the tracker:

- **Federal procurement.** EOs that direct federal agencies to require specific AI-governance practices in procurement flow to any enterprise selling to the federal government.
- **Agency behaviour.** EOs direct enforcement priorities and rulemaking agendas at agencies (EEOC, FTC, HHS, FDA, NIST). A change in EO stack can therefore change the practical enforcement posture of the sector regulators the tracker is already watching.

The current EO stack changes with the presidential administration. The analyst-tier discipline: the tracker's *US federal — executive orders* row (or short list of rows) is refreshed on the monthly deep read, and cites (a) the EOs *currently in force*, (b) any EOs *rescinded* in the current administration, and (c) any [Federal Register](https://www.federalregister.gov/) notices adopting or rescinding EO-derived requirements at specific agencies.

<!-- needs-research: the White House EO stack on AI has changed substantially across administrations. As of the module's authoring, EO 14110 of 30 October 2023 (Safe, Secure, and Trustworthy Development and Use of AI) was rescinded on 20 January 2025 by EO 14148, and EO 14179 of 23 January 2025 (Removing Barriers to American Leadership in AI) was issued as the successor policy. Verify the current stack — including any additional EOs, delegated actions to OMB or agency heads, and the [OMB memoranda on federal AI use](https://www.whitehouse.gov/wp-content/uploads/2024/03/M-24-10-Advancing-Governance-Innovation-and-Risk-Management-for-Agency-Use-of-Artificial-Intelligence.pdf) — at the date of tracker refresh before citing to an internal audience. -->

For the tracker, the analyst names the *currently-in-force* EOs by number, date of signature, and Federal Register citation; the *rescinded* EOs are moved to a separate archived row with the rescission event captured. Neither the currently-in-force nor the rescinded rows are legal opinions; they are situational-awareness fields for the analyst and their reviewers.

## NIST — the framework the enforcers cite

NIST does not enforce. But the [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) — walked at length in `mod-101` chapter 01 and `mod-103` chapter 01 — is cited by the enforcement authorities (EEOC, FTC, HHS OCR, FDA) as a reasonable structuring of AI risk-management practice. The [Generative AI Profile (NIST AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) and the sector companion documents cited from `mod-103` are similarly non-regulatory but referenced.

The tracker holds the NIST framework and the sector companions as *guidance — non-binding* rows. They are load-bearing evidence in an enforcement or audit context that the enterprise has structured its programme against a recognised framework.

## How the US federal branch of the tracker looks

Minimum viable rows for a mid-size enterprise operating in the US:

| Row | Instrument | Role | Status |
|---|---|---|---|
| `REG-2026-US-FED-001` | Title VII / ADA / ADEA — EEOC enforcement on AI hiring / promotion / discipline | Employer | In force |
| `REG-2026-US-FED-002` | Section 5 FTC Act — unfair-or-deceptive practices on AI marketing claims and consumer harms | Firm engaged in commerce | In force |
| `REG-2026-US-FED-003` | FCRA — where AI generates consumer reports for permissible-purpose uses | User or furnisher of consumer report | In force |
| `REG-2026-US-FED-004` | ECOA / Regulation B — AI-driven credit decisions | Creditor | In force |
| `REG-2026-US-FED-005` | Section 1557 ACA — AI in health programmes and activities | Covered entity | In force |
| `REG-2026-US-FED-006` | HIPAA — PHI processed by AI systems and vendors | Covered entity or business associate | In force |
| `REG-2026-US-FED-007` | FDA SaMD framework — AI-enabled medical device | Manufacturer or user facility | In force |
| `REG-2026-US-FED-008` | FDA PCCP guidance — pre-specified changes for AI/ML-enabled devices | Manufacturer | Guidance — non-binding but cited in submissions |
| `REG-2026-US-FED-009` | FDA Good Machine Learning Practice | Manufacturer | Guidance — voluntary |
| `REG-2026-US-FED-010` | White House EO stack — currently in force | Federal contractor (direct) / all firms (indirect) | Refresh cadence: monthly |
| `REG-2026-US-FED-011` | NIST AI RMF + GenAI Profile | All | Guidance — voluntary; cited in enforcement |

Each row's *affected inventory rows* list determines which of the enterprise's systems are actually engaged. A row with no affected inventory rows is still worth carrying — the enterprise's next deployment may attach to it — but the analyst notes *no current in-scope systems* explicitly.

## Where the US federal branch stops for the analyst

- **Not the enterprise's federal-affairs strategy.** Whether the enterprise submits comments on an FTC proposed rulemaking or a NIST framework revision is a policy decision; the tracker records the rulemaking and the comment deadline, not the enterprise's position.
- **Not counsel's read on which statute applies.** The tracker names the statute the enforcement authority cites; counsel opines on whether a specific system's design engages the statute.
- **Not the case-law digest.** The tracker cites primary sources (statutes, regulations, guidance, EOs, Federal Register notices). Notable enforcement actions or consent orders are captured in a *notes* field per row rather than in a case-law tab; case law is a legal-research task and lives with counsel.
- **Not the trade-press pulse.** IAPP, industry-association briefings, and law-firm client alerts are how the analyst *notices* changes. Primary sources are what populates the tracker.

## What to memorise

- **The joint statement** — four authorities agreed in 2023 (re-affirmed 2024) that existing federal law applies to AI. That is the analyst's rebuttal to *there is no US AI law*.
- **The five authorities to know** — EEOC (Title VII/ADA/ADEA), FTC (Section 5, FCRA, ECOA), HHS OCR (Section 1557, HIPAA), FDA (SaMD, PCCP, GMLP), and NIST as the framework-supplier the enforcers cite.
- **The role-per-row discipline** — the enterprise can be an employer, a creditor, a covered entity, a manufacturer, or a federal contractor for different systems; the tracker's *role* column is per-row and per-system.
- **The EO overlay is dynamic** — the tracker's EO row is refreshed monthly and cites currently-in-force plus rescinded plus any Federal Register notices adopting or rescinding EO-derived requirements at specific agencies.
- **NIST is guidance the enforcers cite** — non-binding but load-bearing evidence in an audit or enforcement posture.

## Summary

The US federal AI-governance landscape is a patchwork of long-standing statutory authorities enforced by sector regulators and civil-rights enforcers, backed by a joint statement in which the authorities agreed the existing statutes apply to AI. The tracker holds one row per authority-and-statute pair — EEOC on Title VII / ADA / ADEA, FTC on Section 5 and FCRA and ECOA, HHS OCR on Section 1557 and HIPAA, FDA on SaMD and PCCP and GMLP — plus a row for the currently-in-force executive-order stack and a row for the NIST framework and the sector profiles cited by the enforcers. Each row's role and scope-trigger fields are populated per system, and the EO row is refreshed monthly against Federal Register publications. Chapter 04 walks the US state stack that layers on top; chapter 06 develops the sector overlays where an enterprise's system is regulated as a medical device, a bank model, or an insurer's actuarial tool.
