# The Rolling AI Regulatory Tracker — Method, Schema, and Cadence

## Why this chapter

By this point in the track the analyst has an inventory (`mod-102`), a register of assessed risks (`mod-103`), a bias-review note per relevant system (`mod-104`), and an impact-assessment corpus (`mod-105`). Every one of those artefacts was authored against a specific state of the regulatory landscape — GDPR is in force, the EU AI Act's obligations are phasing in on a schedule, the Colorado AI Act takes effect on a known date, NYC Local Law 144 is being enforced, the FDA's Good Machine Learning Practice principles are non-binding but referenced in submissions, and any number of state, federal, and sector rules are in flight.

The problem is that the landscape does not sit still. Article 6 delegated acts land, supervisory-authority guidance is published, states pass new AI statutes and preempt or reference each other, banking supervisors update model-risk expectations, an executive order is issued or rescinded, and every one of those events can invalidate the *this is what we knew when we signed off* footer on last quarter's impact assessment.

The analyst-tier discipline for keeping the corpus current is a **rolling regulatory tracker**: a single canonical source that names every obligation the enterprise is watching, tags it to the affected systems in the inventory, records its status and the last time the analyst looked at it, and produces a **regulatory-change note** when a change lands (chapter 10). This chapter defines the tracker's field shape, the refresh cadence, the sources the analyst reads to keep it current, and the hand-off pattern to counsel.

## The tracker is a register, not a memo

The most common first-year failure mode is to keep regulatory awareness as tacit knowledge in the analyst's head plus a bookmark folder in a browser. That works until the analyst goes on leave, or the enterprise's second analyst is hired, or an auditor asks *what were you tracking on 2026-03-12 when this system was deployed*.

The tracker is a register: one row per obligation, columns filled in, updated on a cadence, discoverable in the same governance repository or GRC platform that holds the inventory (`mod-102` chapter 04). It is not the enterprise's legal-opinion database — legal characterisation stays with counsel — but it is the analyst's *situational awareness* rendered as evidence.

Analyst-tier default: the tracker lives alongside the inventory, uses the same identifier convention (`REG-<year>-<sequence>`), and every inventory row carries a foreign-key list of the regulatory obligations that apply to it. When a row in the tracker changes, the analyst walks the affected inventory rows and either updates the review-trigger field or files a change note (chapter 10).

## Jurisdiction taxonomy

The tracker groups obligations by jurisdiction so that no whole layer is quietly dropped. The analyst-tier taxonomy — one branch per column-family in the tracker:

- **EU** — [Regulation (EU) 2024/1689](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) (AI Act), [Regulation (EU) 2016/679](https://eur-lex.europa.eu/eli/reg/2016/679/oj) (GDPR), the [Council of Europe Framework Convention on AI](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence), and the sector overlays the EU stack references.
- **US federal** — [EEOC](https://www.eeoc.gov/) enforcement of Title VII / ADA / ADEA on AI-mediated employment decisions; [FTC](https://www.ftc.gov/) Section 5 unfair-or-deceptive-practices; [HHS OCR](https://www.hhs.gov/ocr/index.html) Section 1557 non-discrimination in health programmes; [FDA](https://www.fda.gov/) medical-device software (SaMD) and Good Machine Learning Practice; White House executive orders in force at the date of tracker refresh.
- **US state** — [Colorado AI Act (SB24-205)](https://leg.colorado.gov/bills/sb24-205); [NYC Local Law 144 of 2021](https://rules.cityofnewyork.us/wp-content/uploads/2023/04/DCWP-NOA-for-Use-of-Automated-Employment-Decisionmaking-Tools-2.pdf) on automated employment decision tools; [Illinois BIPA (740 ILCS 14)](https://www.ilga.gov/legislation/ilcs/ilcs3.asp?ActID=3004) for biometric AI implications; state-level AI legislation passed or in trailer in the enterprise's operating states (California, Utah, Tennessee, Texas, and others as they attach).
- **UK** — the principles-based approach articulated in the [pro-innovation AI regulation white paper (2023)](https://www.gov.uk/government/publications/ai-regulation-a-pro-innovation-approach) and any subsequent legislative trajectory, plus [ICO guidance on AI and data protection](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/).
- **Canada** — the AIDA legislative trajectory (as of prior Parliaments, part of [Bill C-27](https://www.parl.ca/DocumentViewer/en/44-1/bill/C-27/first-reading)) and the [TBS Directive on Automated Decision-Making](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592) for federal use cases.
- **Sector overlays** — [FDA GMLP guiding principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles); banking model-risk management ([SR 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) / [OCC 2011-12](https://www.occ.gov/news-issuances/bulletins/2011/bulletin-2011-12.html)); insurance ([NAIC Model Bulletin on the Use of Artificial Intelligence Systems by Insurers](https://content.naic.org/sites/default/files/inline-files/2023-12-4%20Model%20Bulletin_Adopted_0.pdf), [EIOPA guidance](https://www.eiopa.europa.eu/) as it develops).

Every jurisdiction the enterprise operates in should have at least one row in the tracker even if the row's status is *no active obligation — monitoring for change*. A jurisdiction with no row is a jurisdiction the enterprise is not looking at.

## Tracker field shape

The analyst-tier tracker schema, column by column:

- **Regulation ID.** `REG-<year>-<sequence>`. Stable; never re-used.
- **Short name.** Human-readable — *EU AI Act — Article 27 FRIA*, *Colorado AI Act — consumer notice*, *NYC LL 144 — bias audit and candidate notice*.
- **Jurisdiction.** The taxonomy branch above.
- **Instrument.** The specific regulation, statute, rule, guidance, or executive order. Full citation to the primary source (URL and, where applicable, official register reference).
- **Scope trigger.** In one or two sentences: what makes an AI system in-scope for this obligation. This is the field that decides whether an inventory row inherits the obligation.
- **Deployer / provider / controller / covered entity role.** Who owes the obligation — the deployer, the provider, a data controller, a covered health-plan or provider, a financial institution, and so on. AI regulation almost always distinguishes these roles; getting the role wrong is the fastest way to author the wrong obligation.
- **Status.** One of: *in force*, *phased — [date]*, *proposed*, *guidance — non-binding*, *voluntary code*, *rescinded*. The status field carries the date the analyst last verified it (see cadence below).
- **Effective date and phase-in schedule.** For phased-in regulations (the AI Act), the specific dates each obligation becomes enforceable.
- **Enforcement authority.** The regulator or supervisory authority that enforces the obligation. Populated even when enforcement machinery is still standing up — an *authority not yet designated — see [source]* note is a valid answer.
- **Affected inventory rows.** Foreign-key list of inventory row identifiers (`INV-<year>-<sequence>`) that the analyst has determined are in scope. Empty is a valid answer; unpopulated (unwritten) is not.
- **Related obligations.** Foreign-key list of other tracker rows — the AI Act row cross-references the GDPR row where processing is engaged; the Colorado AI Act row cross-references the NYC LL 144 row for hiring-adjacent overlap.
- **IAPP AIGP body-of-knowledge tag.** The AIGP domain the obligation sits in — regulatory landscape, risk management, governance, and so on (chapter 08). Optional but recommended; the tag makes it easy to filter the tracker for a specific certification-domain review.
- **Last-verified date and by-whom.** The single most important field. If this date is more than one review-cadence unit stale, the row is not evidence — it is a claim.
- **Primary-source URLs.** The regulation itself and, ideally, the version-controlled or archived link (e.g., a stable EUR-Lex CELEX URL, an archived rules-of-the-city URL, a Federal Register document URL). Guidance and secondary summaries — IAPP briefings, law-firm client alerts, trade-press coverage — are useful reading but do not go in this column.
- **Notes for counsel.** A short field flagging open questions that counsel should decide when a specific system is up for sign-off. Not a legal opinion — a *question* for counsel.

The row is a piece of evidence. A row with a stale last-verified date and no affected inventory rows is a candidate for either an update or an explicit *no longer tracked — [reason]* retirement.

## Refresh cadence

The tracker is not a one-shot document. The analyst-tier cadence:

- **Weekly light touch (30 minutes).** Skim the enforcement authority press pages for the top-priority jurisdictions the enterprise operates in. Update *last-verified* on any row where nothing has changed since the last look; note anything that has changed for the next monthly deep read.
- **Monthly deep read (2–4 hours).** Read every row where status is *phased* or *proposed* or where the weekly touch flagged a change. Refresh the tracker fields. Author change notes (chapter 10) for any obligation that has moved.
- **Quarterly cross-check.** Walk the inventory: for every row, check that the *applicable regulations* field is still accurate given any tracker changes. Update review-trigger fields on impact assessments as needed.
- **On-demand refresh.** Whenever a new system's intake questionnaire (`mod-102` chapter 01) surfaces a jurisdiction the tracker does not yet cover, add the row before the intake is closed.

The cadence is not a piety — the *last-verified* field is auditable. An enterprise that certifies against ISO/IEC 42001 will typically have an internal-audit finding on any tracker row with a last-verified date more than 90 days old.

## Sources the analyst reads to keep it current

There is no single feed. The analyst-tier source list:

- **Primary — regulatory publications.** [EUR-Lex](https://eur-lex.europa.eu/) for EU legal acts; the [Federal Register](https://www.federalregister.gov/) for US federal rulemakings; state legislative-tracking pages (e.g., [California Legislative Information](https://leginfo.legislature.ca.gov/), [Colorado General Assembly](https://leg.colorado.gov/)); the [UK Parliament](https://bills.parliament.uk/) and [gov.uk](https://www.gov.uk/) for UK legislation and guidance; the [Council of Europe](https://www.coe.int/) treaty office for CoE instruments.
- **Primary — regulator communications.** EU AI Office announcements; EDPB opinions; national supervisory-authority guidance (CNIL, BfDI, ICO, etc.); EEOC and FTC press releases and guidance documents; HHS OCR, FDA, and sector-supervisor bulletins.
- **Secondary — practitioner briefings.** [IAPP](https://iapp.org/) resource pages and their AI governance dashboard; large-firm regulatory-tracker publications; the OECD.AI policy observatory. These are useful for *catching* a change quickly but must not be cited as the source of the obligation — the analyst chases the primary reference before updating the row.
- **Tertiary — practitioner community.** IAPP AIGP-holder community; internal legal-team mailing lists; industry associations (BSA, ITI, national bar-association AI committees). Useful signal; never sufficient evidence.

The rule: primary references populate the tracker's *primary-source URLs* column; secondary references are how the analyst *noticed* the change and belong in the analyst's reading log, not in the evidence field.

## Where the tracker stops for the analyst

- **Not a legal opinion.** The tracker records that an obligation exists, when it takes effect, which authority enforces it, and which inventory rows are in scope. Whether a specific system's design *complies* with the obligation is a legal characterisation counsel owns.
- **Not the enterprise's compliance programme.** The tracker feeds the impact-assessment corpus, the control library (`mod-108`), and the review-trigger fields on individual systems. It is a source; the compliance programme is downstream.
- **Not a lobbying position.** The tracker is descriptive, not advocacy. If the enterprise takes a policy position on a proposed regulation, that position lives in a separate document; the tracker records only that the proposal exists and its current status.
- **Not the horizon-scan.** Proposals in early stages of legislative process may sit in a *horizon* tab, but only obligations that are enforceable, phased-in, or currently in a well-defined proposal stage go in the main tracker. A horizon-scan that pollutes the main tracker with every legislator's press release is un-usable within a month.

## What to memorise

- **The tracker is a register, not a memo** — one row per obligation, discoverable, versioned, tied to inventory rows.
- **The six jurisdiction branches** — EU, US federal, US state, UK, Canada, sector overlays. Every jurisdiction the enterprise operates in has at least one row.
- **The tracker field shape** — scope trigger, role, status, effective date, enforcement authority, affected inventory rows, related obligations, last-verified date, primary-source URLs, notes for counsel.
- **The refresh cadence** — weekly touch, monthly deep read, quarterly cross-check, on-demand for new intake.
- **The primary / secondary source distinction** — primary references populate the evidence field; secondary references are reading, not evidence.

## Summary

The rolling regulatory tracker is the analyst-tier register that keeps the enterprise's situational awareness of AI regulation current, discoverable, and tied to the specific inventory rows the obligations attach to. It is organised by jurisdiction — EU, US federal, US state, UK, Canada, sector — and every row carries a scope trigger, a role assignment, a status, an effective date, an enforcement authority, foreign-keys to affected inventory rows and related obligations, and a *last-verified date* that turns the row into evidence rather than a claim. The refresh cadence is weekly, monthly, and quarterly, backed by primary regulatory sources and secondary practitioner briefings. Chapters 02–06 walk each jurisdictional branch; chapter 07 covers the privacy-law flagging discipline that decides when to hand off to counsel; chapter 10 covers the regulatory-change-note that turns a tracker update into routed action across the affected system owners.
