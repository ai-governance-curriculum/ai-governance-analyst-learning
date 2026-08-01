# The UK and Canada Trajectories — Principles-Based Regulation and Federal-Sector Directives

## Why this chapter

The UK and Canada sit at similar points on the AI-regulation trajectory: both have adopted a *principles-first* posture rather than a horizontal statute like the EU AI Act, both have active data-protection authorities that have published operational AI guidance, and both carry a federal-sector direct-obligation regime — the UK through cross-regulator guidance and the Canadian federal government through the Treasury Board Secretariat's [Directive on Automated Decision-Making](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592). Both jurisdictions have carried legislative proposals for a comprehensive AI statute — the UK's [pro-innovation white paper](https://www.gov.uk/government/publications/ai-regulation-a-pro-innovation-approach) and Canada's [Bill C-27 AIDA](https://www.parl.ca/DocumentViewer/en/44-1/bill/C-27/first-reading) — and both trajectories have changed shape multiple times.

The analyst-tier discipline for the UK and Canada: read *what is currently in force*, track *what is proposed with a credible parliamentary path*, and do not treat *what a previous government proposed* as evidence of current obligation. This chapter walks the current-state and trajectory for each.

## The UK — principles-based, regulator-led

The UK's stated approach as of the [2023 white paper](https://www.gov.uk/government/publications/ai-regulation-a-pro-innovation-approach) and the [2024 government response](https://www.gov.uk/government/consultations/ai-regulation-a-pro-innovation-approach-policy-proposals/outcome/a-pro-innovation-approach-to-ai-regulation-government-response) is *principles-based, context-specific, and regulator-led*. Five cross-sectoral principles are the shared reference:

1. **Safety, security, and robustness.**
2. **Appropriate transparency and explainability.**
3. **Fairness.**
4. **Accountability and governance.**
5. **Contestability and redress.**

The principles are non-statutory. The operational effect is that existing UK regulators — [ICO](https://ico.org.uk/), [FCA](https://www.fca.org.uk/), [MHRA](https://www.gov.uk/government/organisations/medicines-and-healthcare-products-regulatory-agency), [Ofcom](https://www.ofcom.org.uk/), [CMA](https://www.gov.uk/government/organisations/competition-and-markets-authority), [EHRC](https://www.equalityhumanrights.com/), and the [Health and Safety Executive](https://www.hse.gov.uk/) — apply the principles within their existing statutory remits. There is no single AI regulator and no horizontal AI statute in force.

<!-- needs-research: the UK government's position on whether to legislate for a horizontal AI statute has shifted with successive administrations. As of 2026-08-01, verify current government policy, any King's Speech commitment on AI legislation, any published bill, and any parliamentary progress; the trajectory has been active and the tracker's status field on any UK legislative row must be current. -->

### The ICO as the load-bearing regulator for AI-and-data

The [Information Commissioner's Office](https://ico.org.uk/) is the UK data-protection authority — the successor to the DPA-1998 regulator, now enforcing UK GDPR (retained EU law with UK amendments) and the Data Protection Act 2018. For AI systems that process personal data — which is most of them — the ICO is the primary point of enforcement.

The ICO's [Guidance on AI and data protection](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/) is the operational reference the tracker cites. It covers:

- **Accountability and governance implications of AI**, including [DPIA-shape guidance for AI systems](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/guidance-on-ai-and-data-protection/how-should-we-assess-security-and-data-minimisation-in-ai/).
- **The fairness principle** (UK GDPR Article 5(1)(a)) applied to AI, including handling of bias.
- **The security principle** (Article 5(1)(f) and Article 32) applied to AI.
- **Data-minimisation** (Article 5(1)(c)) applied to model training and inference.
- **Individual rights and automated decision-making** (Article 22 as retained in UK GDPR).
- **[The AI-and-data-protection-risk toolkit](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/ai-and-data-protection-risk-toolkit/)** — a spreadsheet-shaped ICO risk-toolkit the analyst can lift for internal use.

The ICO also publishes an [audit framework for AI](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/guidance-on-ai-and-data-protection/ai-auditing-framework/) that gives the analyst a mapped-to-controls shape suitable for use as an internal-audit reference.

### UK GDPR Article 22

UK GDPR Article 22 — as retained from EU GDPR, subject to UK amendments — carries the same solely-automated-decision provisions as EU GDPR Article 22. The [Data Protection Act 2018 §14](https://www.legislation.gov.uk/ukpga/2018/12/section/14) supplements Article 22 by requiring specific safeguards when automated decisions are made under Article 22(2)(b) (legal-obligation basis).

The [Data (Use and Access) Act 2025](https://bills.parliament.uk/bills/3825) — as enacted — amended the UK's automated-decision-making rules. <!-- needs-research: verify the enacted text and commencement dates of the Data (Use and Access) Act 2025 provisions on automated decision-making before citing to a UK deployment; the Act's ADM provisions materially shifted the Article 22 posture and the tracker must carry the current text. -->

### UK tracker rows, minimum viable

- `REG-2026-UK-001` — UK GDPR + Data Protection Act 2018 — general AI-and-personal-data processing. Enforcement: ICO.
- `REG-2026-UK-002` — UK GDPR Article 22 + DPA 2018 §14 — solely-automated decisions with legal or similar effect. Enforcement: ICO.
- `REG-2026-UK-003` — Data (Use and Access) Act 2025 — ADM provisions as commenced. Enforcement: ICO.
- `REG-2026-UK-004` — UK principles-based AI regulation — cross-regulator guidance (ICO / FCA / MHRA / Ofcom / CMA / EHRC / HSE). Status: guidance, non-statutory; regulator-specific enforcement within each regulator's remit.
- `REG-2026-UK-005` — ICO AI-and-data-protection guidance and audit framework. Status: guidance; load-bearing evidence for the AI-and-personal-data slice of the enterprise's programme.
- `REG-2026-UK-006` — UK horizontal AI legislation. Status: watch — see needs-research above.

## Canada — federal-sector directives and stalled federal legislation

Canada carries two parallel tracks that the tracker treats separately:

- **Federal-sector direct obligation.** The [Treasury Board Secretariat Directive on Automated Decision-Making](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592) has been in force since 1 April 2019 (with subsequent amendments) and applies to Government of Canada institutions using automated decision systems to make administrative decisions about clients.
- **Private-sector horizontal legislation trajectory.** The [Artificial Intelligence and Data Act (AIDA)](https://ised-isde.canada.ca/site/innovation-better-canada/en/artificial-intelligence-and-data-act) was proposed as Part 3 of [Bill C-27](https://www.parl.ca/DocumentViewer/en/44-1/bill/C-27/first-reading), tabled June 2022. Bill C-27 did not pass before the prorogation of the 44th Parliament on 6 January 2025 and — under Canadian parliamentary procedure — died on the order paper.

### The TBS Directive on Automated Decision-Making

The Directive applies to any *automated decision system* — technology that either assists or replaces the judgement of human decision-makers — used by a federal institution to make an administrative decision or a related assessment about a client. Its central mechanism is the [Algorithmic Impact Assessment (AIA)](https://open.canada.ca/aia-eia-js) — a scored, publish-by-default questionnaire that classifies the system into one of four impact levels (I, II, III, IV) and attaches obligations that scale with the level. `mod-105` chapter 02 walks the AIA at length.

The Directive obligations that scale by impact level include:

- **Peer review** — required at Levels III and IV; scope of review scales.
- **Notice to affected clients** — required at all levels; content scales.
- **Explanation of decisions** — required at all levels; depth scales.
- **Human intervention** on request — required for Levels II–IV depending on decision type.
- **Publication of the AIA on the Government of Canada Open Government portal**.
- **Testing, monitoring, contingency planning, gender-based-analysis-plus, and quality-assurance** obligations that scale.

The Directive is a Treasury Board policy instrument — binding on federal institutions but not on private-sector actors unless they are contracting to build or supply an automated decision system to a federal institution, in which case the contracting institution flows the obligations down through procurement.

The [Guide on the use of generative AI](https://www.canada.ca/en/government/system/digital-government/digital-government-innovations/responsible-use-ai/guide-use-generative-ai.html) — issued by the Treasury Board — supplements the Directive for federal-institution use of generative AI. It is guidance layered on top of the Directive.

### The AIDA trajectory

AIDA — Part 3 of Bill C-27 — proposed a horizontal AI statute for the private sector with the following core obligations (as tabled; the bill did not pass):

- Duties on persons responsible for a *high-impact* AI system to assess and mitigate risks of harm and biased output.
- Record-keeping, monitoring, and — for anonymised data used in AI systems — data-governance obligations.
- Duty to notify the Minister of Innovation, Science, and Industry when a high-impact AI system results, or is likely to result, in material harm.
- An enforcement regime with administrative monetary penalties and offences for reckless conduct.

Because AIDA did not pass, it is *not law* and the tracker's status field is *proposed — died on order paper 6 Jan 2025*. A re-tabled version — or a substantially different successor bill — may appear in a subsequent Parliament; the tracker's *needs-research* marker on the AIDA row is refreshed on the monthly deep read.

<!-- needs-research: monitor the Canadian federal Parliament for any successor legislation to AIDA — either a re-tabled version or a new bill on AI regulation for the private sector. Verify the status of any successor before updating the tracker beyond a *proposed* status. -->

### The Office of the Privacy Commissioner of Canada

The [Office of the Privacy Commissioner of Canada (OPC)](https://www.priv.gc.ca/) enforces the [Personal Information Protection and Electronic Documents Act (PIPEDA)](https://www.priv.gc.ca/en/privacy-topics/privacy-laws-in-canada/the-personal-information-protection-and-electronic-documents-act-pipeda/) federally for private-sector use of personal information. PIPEDA does not have an equivalent of GDPR Article 22 but the OPC has published [Principles for responsible, trustworthy, and privacy-protective generative AI technologies](https://www.priv.gc.ca/en/privacy-topics/technology/artificial-intelligence/gd_principles_ai/) that shape how the OPC applies PIPEDA to AI systems. The tracker holds an OPC guidance row alongside the TBS Directive row.

Provincial private-sector privacy laws — [Quebec's Law 25 (Act 25)](https://www.cai.gouv.qc.ca/documents/CAI_A_Loi_25_EN.pdf), [British Columbia's PIPA](https://www.bclaws.gov.bc.ca/civix/document/id/complete/statreg/03063_01), and [Alberta's PIPA](https://www.qp.alberta.ca/documents/Acts/P06P5.pdf) — carry provisions on automated decision-making that engage AI use cases. Quebec Law 25 in particular carries an automated-decisionmaking-notification obligation on private-sector organisations that is analogous to a light-touch Article 22-plus.

### Canada tracker rows, minimum viable

- `REG-2026-CA-001` — TBS Directive on Automated Decision-Making. Scope: federal-institution use of automated decision systems for administrative decisions about clients; and — via flow-down — contractors supplying such systems. Enforcement: Treasury Board of Canada Secretariat and internal-audit function of the deploying institution.
- `REG-2026-CA-002` — TBS Guide on the use of generative AI (federal institutions). Status: guidance layered on Directive.
- `REG-2026-CA-003` — AIDA (proposed, Bill C-27, died on order paper 6 Jan 2025). Status: proposed — no current federal private-sector AI statute in force.
- `REG-2026-CA-004` — PIPEDA + OPC generative-AI principles. Enforcement: Office of the Privacy Commissioner of Canada.
- `REG-2026-CA-005` — Quebec Law 25 automated-decisionmaking-notification provisions. Enforcement: Commission d'accès à l'information du Québec (CAI).
- `REG-2026-CA-006` — BC PIPA and Alberta PIPA. Enforcement: BC OIPC and Alberta OIPC respectively.

## How the UK and Canada trajectories inform the tracker

Two operational implications:

- **Absence of a horizontal statute is not absence of obligation.** An enterprise deploying an AI system that processes personal data of UK or Canadian residents is subject to UK GDPR / DPA 2018 (UK) or PIPEDA and provincial analogues (Canada) — enforced by data-protection regulators that have published operational AI guidance. The tracker names the guidance and cites the enforcing authority.
- **Legislative-trajectory rows must carry status honestly.** A *proposed* row that says *AI Act — Canada* without noting that AIDA died on the order paper misleads a reviewer. The status field for legislative-trajectory rows carries the current parliamentary state and — where applicable — the date on which the previous instrument was withdrawn or lapsed.

## Where the UK and Canada trajectories stop for the analyst

- **Not a legal opinion on principles-based regulation.** Whether a UK principle applies in a specific case is the relevant regulator's judgement; the analyst names the principle and the regulator.
- **Not a prediction of what the next Parliament will pass.** The tracker's status is *what is enacted or in force now*; horizon-scan tabs hold *what is proposed with a credible parliamentary path*. Speculating about the next bill is a policy activity, not a tracker activity.
- **Not a substitute for local counsel.** UK-and-Canada-specific fields — including whether a specific enterprise's model falls under a specific provincial statute, or whether a specific federal contract flows down TBS Directive obligations — require local-jurisdiction counsel.

## What to memorise

- **The UK is principles-based, regulator-led** — five principles, existing regulators enforce, ICO is the load-bearing regulator for AI-and-personal-data, no horizontal AI statute currently in force.
- **The Data (Use and Access) Act 2025 shifted ADM under UK GDPR Article 22** — verify current text against the enacted statute before citing.
- **Canada carries two tracks** — the TBS Directive on ADM (federal-institution, in force since 2019; contractor flow-down); and the AIDA trajectory (proposed as Bill C-27, died on order paper 6 Jan 2025, no current federal private-sector AI statute).
- **PIPEDA + OPC generative-AI principles + Quebec Law 25 + BC/AB PIPA** — the current Canadian private-sector layer for AI-and-personal-data.
- **Status fields for legislative-trajectory rows carry the current parliamentary state honestly** — *proposed*, *died on order paper*, *in second reading*, *enacted — pending commencement*, *in force*.

## Summary

The UK and Canada both sit on a principles-first AI-regulation trajectory with no horizontal AI statute currently in force. The UK operates through the 2023 white-paper principles enforced by existing sector regulators — the ICO carrying the load for AI-and-personal-data — with the Data (Use and Access) Act 2025 shifting the automated-decision-making posture under UK GDPR Article 22. Canada carries the TBS Directive on Automated Decision-Making binding on federal institutions and flow-down applicable to contractors, alongside PIPEDA and the OPC's generative-AI principles at the private-sector layer; the AIDA horizontal statute proposed in Bill C-27 died on the order paper on 6 January 2025 and there is no current federal private-sector AI statute. The tracker carries an anchor row per instrument, an anchor row per enforcing regulator, and a horizon-scan row for the AIDA trajectory that is refreshed on the monthly deep read.
