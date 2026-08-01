# The EU Stack — AI Act, GDPR, and the Council of Europe Framework Convention

## Why this chapter

The EU is the densest jurisdiction the tracker will hold. Three instruments sit on top of each other and every one of them is load-bearing for a European deployment:

- **The AI Act** ([Regulation (EU) 2024/1689](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)) — a horizontal product-safety-style regulation for AI systems, phased in on a schedule that runs from 2025 through 2027.
- **GDPR** ([Regulation (EU) 2016/679](https://eur-lex.europa.eu/eli/reg/2016/679/oj)) — in force since 25 May 2018; the personal-data layer that engages whenever an AI system processes personal data.
- **The Council of Europe Framework Convention on AI** — the first international treaty on AI, opened for signature 5 September 2024, covering AI systems' impact on human rights, democracy, and the rule of law.

None of them supersedes the others. An enterprise deploying a hiring-assistance system in France in 2026 typically owes obligations under all three plus at least one supervisory-authority guidance layer. This chapter walks how the analyst represents the EU stack in the tracker, the AI Act phase-in schedule that determines what is enforceable on any given date, and the Council of Europe framework's role as the international baseline that the AI Act operationalises.

## The AI Act — tier structure and phase-in

The AI Act sits over a four-tier risk classification:

- **Unacceptable risk** — prohibited practices under [Article 5](https://artificialintelligenceact.eu/article/5/) (social scoring by public authorities, real-time remote biometric identification in public spaces subject to narrow exceptions, exploitative techniques targeting vulnerable groups, and others). Not deployed; deployment is unlawful.
- **High risk** — systems under [Article 6](https://artificialintelligenceact.eu/article/6/) and enumerated in [Annex III](https://artificialintelligenceact.eu/annex/3/). Providers owe conformity assessment, technical documentation, transparency, human oversight design, and post-market monitoring obligations; deployers owe the Article 26 obligations plus, in a narrow slice, the Article 27 fundamental-rights impact assessment (`mod-105` chapter 03).
- **Limited risk / transparency** — systems under [Article 50](https://artificialintelligenceact.eu/article/50/) (interaction-with-natural-persons, synthetic content generation, deepfake labelling, emotion-recognition). The obligation is disclosure to the user.
- **Minimal risk** — the residual category. No specific AI Act obligations; voluntary codes of conduct.

A separate track sits on top for **general-purpose AI models** ([Chapter V, Articles 51–56](https://artificialintelligenceact.eu/chapter/5/)) with additional obligations for models with systemic risk. The [GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) — covered in chapter 09 — is the voluntary compliance route the AI Office maintains for GPAI providers.

The phase-in schedule the analyst tracks:

| Date | Obligation |
|---|---|
| 2 February 2025 | Prohibitions under Article 5 apply; AI-literacy obligation under Article 4 applies |
| 2 August 2025 | Governance provisions apply; obligations for providers of general-purpose AI models apply (Chapter V); penalties framework applies (Chapter XII) |
| 2 August 2026 | Most other provisions apply — high-risk system obligations for Annex III systems, transparency obligations under Article 50, notified-body machinery |
| 2 August 2027 | Provisions for high-risk systems governed by Union harmonisation legislation in Annex I (e.g., medical devices, machinery) apply |

<!-- needs-research: the phase-in dates above are drawn from Article 113 of Regulation (EU) 2024/1689 as originally published. If the Commission, Council, or Parliament adopts a delegated or implementing act adjusting the phase-in, verify against the current consolidated text at eur-lex.europa.eu before citing to an audit or a regulator. -->

Analyst-tier discipline: every tracker row for an AI Act obligation carries the *effective date* explicitly. A row that says *AI Act — high risk conformity* with no phase-in date attached is not usable — the reviewer of the enterprise's next deployment cannot tell whether the obligation is live yet.

## Deployer vs provider — the load-bearing role distinction

The AI Act attaches different obligations to different actors. The Article 3 definitions the analyst uses to populate the tracker's *role* column:

- **Provider** ([Article 3(3)](https://artificialintelligenceact.eu/article/3/)) — natural or legal person who develops an AI system or has one developed and places it on the market or puts it into service under their own name or trade mark, whether for payment or free of charge. Owes the bulk of the high-risk obligations (Chapter III Section 2 — Articles 8 through 22 of the AI Act shape).
- **Deployer** ([Article 3(4)](https://artificialintelligenceact.eu/article/3/)) — natural or legal person using an AI system under their own authority, except in the course of a personal non-professional activity. Owes Article 26 obligations (use in accordance with instructions, human oversight, input-data governance, monitoring, keeping logs, informing affected persons in the applicable cases) and — where the scoping filter is met — the Article 27 FRIA.
- **Importer** and **Distributor** — narrower obligations covered by Articles 23–24.

The important note for the tracker: the same enterprise can be a *provider* for one system (an internally-developed model exposed to a downstream customer) and a *deployer* for another (a hosted foundation-model API used inside a workflow). The role is per-system, not per-enterprise. The tracker's *affected inventory rows* column pairs each inventory row with the role the enterprise plays for that system.

## GDPR — the always-on layer

GDPR is not new, but its intersection with AI has sharpened as the AI Act enters into force:

- **Article 22 GDPR — automated individual decision-making, including profiling.** A data subject has the right not to be subject to a decision based solely on automated processing, including profiling, which produces legal effects concerning them or similarly significantly affects them, subject to Article 22(2) exemptions. Chapter 07 walks the flagging discipline; the load-bearing tracker note is that Article 22 is engaged whenever a solely-automated decision produces legal or similarly significant effects.
- **Article 35 GDPR — data protection impact assessment.** Required whenever processing is likely to result in high risk to natural persons; the WP 248 nine-criteria filter is the practical scoping tool (`mod-105` chapter 04). Most AI systems processing personal data trigger this.
- **Article 36 GDPR — prior consultation with the supervisory authority.** Required when the DPIA indicates the processing would result in high risk in the absence of measures taken by the controller to mitigate the risk.
- **Article 5 and 6 GDPR — principles and lawful basis.** Any AI system that processes personal data must satisfy the six principles (Article 5) and have a lawful basis under Article 6 (and, where special-category data is involved, Article 9).

For the tracker, GDPR sits as one or two rows: the *Article 22 flag*, the *Article 35 DPIA trigger*, and — often — a separate row for the *supervisory-authority-specific list of processing operations always requiring a DPIA* under Article 35(4). Rows cross-reference the AI Act rows: the Article 27 FRIA and the Article 35 DPIA overlap substantially and must be authored coherently (`mod-105` chapter 04).

The [European Data Protection Board](https://www.edpb.europa.eu/) publishes opinions and guidelines that shape how supervisory authorities interpret the personal-data layer of AI systems; the EDPB's guidance is monitored in the weekly light-touch refresh. Guidance is not a regulation but is cited in enforcement — the tracker holds the guidance links in the *primary-source URLs* column.

## The Council of Europe Framework Convention on AI

The [Council of Europe Framework Convention on Artificial Intelligence and Human Rights, Democracy and the Rule of Law](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence) — opened for signature 5 September 2024 in Vilnius — is the first international treaty on AI. It is a *framework* convention: it sets principles (human dignity, human autonomy, equality and non-discrimination, respect for privacy, transparency and oversight, accountability, safety, and remedy) and requires parties to implement the principles in domestic law rather than laying down operational obligations directly.

For the enterprise, the convention matters in two ways:

- **Signatory states will implement its principles in domestic law.** The EU AI Act is the EU's operational implementation for private-sector AI within EU scope. Other signatories (including the UK, US, Israel, Canada, Japan, Australia — signatories as of the opening) will implement through their own instruments; the tracker anticipates that domestic implementations will land and be added as rows over the next several years.
- **The convention sets an international baseline for AI human-rights due diligence.** Enterprises operating globally often reference the convention's principles in their public AI-governance policies, alongside [OECD AI Principles](https://www.oecd.org/going-digital/ai/principles/) and the [UNESCO Recommendation on the Ethics of AI](https://www.unesco.org/en/artificial-intelligence/recommendation-ethics). The convention is voluntary in the sense that no direct obligation flows to a private actor from the convention itself, but the principles show up as expectations in enterprise customer contracts, sovereign-buyer requirements, and (indirectly) in the risk-source scan-list from ISO/IEC 23894 (`mod-103` chapter 02).

<!-- needs-research: track ratifications and deposit of instruments of ratification as they land. As of 2026-08-01 the convention had been opened for signature but the analyst should verify how many states have ratified and whether the enterprise's operating jurisdictions are among them before citing the convention as *in force in [state]*. -->

## How the three interlock in the tracker

The analyst-tier layout for the EU stack in the tracker — minimum viable rows per system:

| Row | Instrument | Role | Status |
|---|---|---|---|
| `REG-2026-EU-001` | EU AI Act — Article 5 prohibitions | All | In force (from 2 Feb 2025) |
| `REG-2026-EU-002` | EU AI Act — Article 6 + Annex III high-risk classification | Provider or deployer per inventory row | Phased — most provisions 2 Aug 2026 |
| `REG-2026-EU-003` | EU AI Act — Article 27 FRIA | Deployer (scoped) | Phased — 2 Aug 2026 |
| `REG-2026-EU-004` | EU AI Act — Article 50 transparency | Provider or deployer per system | Phased — 2 Aug 2026 |
| `REG-2026-EU-005` | EU AI Act — Chapter V GPAI | Provider of GPAI model | In force (from 2 Aug 2025) |
| `REG-2026-EU-006` | GDPR — Article 22 solely-automated decisions | Controller | In force |
| `REG-2026-EU-007` | GDPR — Article 35 DPIA | Controller | In force |
| `REG-2026-EU-008` | GDPR — Article 36 prior consultation | Controller | In force (triggered by DPIA outcome) |
| `REG-2026-EU-009` | CoE Framework Convention on AI | Enterprise (indirect via signatory-state implementations) | Awaiting signatory-state implementation |
| `REG-2026-EU-010` | GPAI Code of Practice (voluntary) | Provider of GPAI model | Voluntary — see chapter 09 |

Each row has its own primary-source URL, scope trigger, enforcement authority (national market-surveillance authority per Article 70 for the AI Act; national supervisory authority per Article 51 GDPR; treaty-implementing regulator per signatory-state law for the CoE convention), affected inventory rows, and last-verified date.

The AI Office ([DG CNECT within the European Commission](https://digital-strategy.ec.europa.eu/en/policies/ai-office)) is the coordinating body for the AI Act at Union level; national market-surveillance authorities per member state carry the day-to-day enforcement.

## Where the EU stack stops for the analyst

- **Not the enterprise's EU market strategy.** Whether the enterprise deploys a system in the EU at all is a business decision; the tracker records what the obligations would be if the enterprise does.
- **Not the conformity assessment.** The AI Act's Chapter III Section 4 conformity assessment for high-risk systems is a provider-side product-safety process; where the enterprise is the provider, it is executed by the product / engineering / quality team with notified-body involvement where required. The analyst records that the obligation exists and cites the finished assessment in the impact-assessment corpus.
- **Not the market-surveillance authority notification content.** The Article 27(3) notification of the FRIA outcome to the market-surveillance authority uses the AI Office template; content in that notification is authored jointly with counsel.
- **Not the counsel's read on Article 22.** The analyst *flags* solely-automated decisions with legal or similar significant effects; counsel opines on whether Article 22 is engaged and whether an Article 22(2) exemption applies. Chapter 07 develops the flagging discipline.

## What to memorise

- **The AI Act four-tier structure** — prohibited, high risk, limited (transparency), minimal — plus the GPAI overlay.
- **The AI Act phase-in schedule** — Article 5 and Article 4 apply from 2 Feb 2025; governance and GPAI from 2 Aug 2025; most other provisions from 2 Aug 2026; Annex I high-risk overlay from 2 Aug 2027.
- **The provider / deployer / importer / distributor role distinctions** — per Article 3, per system, not per enterprise.
- **The GDPR Article 22, 35, 36 triggers** — always-on layer; DPIA and prior consultation cited in chapter 07 and `mod-105` chapter 04.
- **The Council of Europe Framework Convention** — international baseline; domestic implementations by signatory states are what attaches operationally.

## Summary

The EU regulatory stack sits in three interlocking layers: the AI Act as the horizontal AI product-safety regulation with a four-tier risk structure and a phased-in effective schedule running through 2027; GDPR as the always-on personal-data layer with Article 22, Article 35, and Article 36 as the AI-relevant hooks; and the Council of Europe Framework Convention on AI as the international baseline whose principles will land through signatory-state implementation. The tracker holds one row per instrument, each with a scope trigger, a role assignment, a status, an effective date, an enforcement authority, and links to the affected inventory rows. The analyst's job is to keep the rows current, to flag Article 22 questions to counsel, and to route AI Act phase-in changes to the impact-assessment corpus via the change-note discipline in chapter 10.
