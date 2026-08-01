# The US State Stack — Colorado AI Act, NYC Local Law 144, and Illinois BIPA

## Why this chapter

The US does not have a single federal AI statute, so US states have been legislating. As of 2026 the state landscape is heterogeneous, active, and often the *first* place a new AI obligation attaches to an enterprise operating nationally. The analyst's tracker must therefore carry US state rows at the same granularity it carries the EU AI Act — sometimes more, because a state statute may cover a use case the EU AI Act does not touch.

This chapter walks the three most-cited state instruments an analyst will meet on a US-operating enterprise: **the Colorado AI Act (SB24-205)**, **NYC Local Law 144 of 2021**, and **Illinois BIPA (740 ILCS 14)** for its biometric-AI implications. It closes with the pattern the analyst uses to keep a broader state-legislation tracker current without letting it turn into a policy blog.

## Colorado AI Act — the first US comprehensive AI statute

The [Colorado AI Act (SB24-205)](https://leg.colorado.gov/bills/sb24-205) was signed into law 17 May 2024 and — as originally passed — is scheduled to take effect **1 February 2026**. It is the first US state comprehensive AI statute; it draws structural cues from the EU AI Act but on a different scope shape.

<!-- needs-research: the Colorado AI Act's effective date and specific obligations were the subject of active amendment in 2025 with a Colorado Governor's task-force process and expected refinements. Verify the current effective date, the current text of the statute, and any published implementing regulations at the [Colorado General Assembly](https://leg.colorado.gov/) and the [Colorado Attorney General's office](https://coag.gov/) before citing to an inventory row's applicable-regulations field. -->

### The scope trigger

The Act applies to any *developer* or *deployer* doing business in Colorado of a **high-risk artificial intelligence system**. A high-risk system is one that, when deployed, makes or is a *substantial factor* in making a **consequential decision** — a decision that has a material legal or similarly significant effect on the provision or denial of, or the cost or terms of, one of the enumerated services:

- Education enrolment or opportunity.
- Employment or employment opportunity.
- A financial or lending service.
- An essential government service.
- Healthcare services.
- Housing.
- Insurance.
- A legal service.

The definition draws obviously on the EU AI Act Annex III shape but the substantial-factor test is a US-litigation-friendly formulation not present in the EU text.

### The obligations

The Act splits the obligations between developers and deployers:

- **Developer duties.** Use reasonable care to protect consumers from any known or reasonably foreseeable risk of algorithmic discrimination arising from the intended and contracted uses of the system. Provide the deployer with documentation supporting the deployer's obligations (a shape analogous to the AI Act Article 13 instructions-for-use). Notify the Colorado Attorney General and known deployers of any risk of algorithmic discrimination discovered post-deployment within a specified window.
- **Deployer duties.** Use reasonable care to protect consumers from algorithmic discrimination; implement a risk-management policy and programme; complete impact assessments; notify consumers when a consequential decision is made about them by a high-risk AI system, and — if the decision is adverse — provide an explanation, an opportunity to correct data, and a right to appeal to human review; publish a summary of the enterprise's use of high-risk AI systems.

The Colorado Attorney General is the exclusive enforcement authority. There is no private right of action under the Act as originally passed.

### How it interacts with the tracker

Analyst-tier tracker rows for Colorado, minimum viable:

- `REG-2026-US-CO-001` — Colorado AI Act — developer duties. Scope trigger: enterprise develops a high-risk AI system used in a consequential decision affecting Colorado consumers. Role: developer.
- `REG-2026-US-CO-002` — Colorado AI Act — deployer duties. Scope trigger: enterprise deploys a high-risk AI system in a consequential decision affecting Colorado consumers. Role: deployer.
- `REG-2026-US-CO-003` — Colorado AI Act — consumer notice, explanation, correction, appeal. Scope trigger: adverse consequential decision made by a high-risk AI system. Role: deployer.
- `REG-2026-US-CO-004` — Colorado AI Act — public-summary publication. Role: deployer.

Each row cross-references the EU AI Act Article 27 FRIA rows from chapter 02 — the impact-assessment shapes overlap enough that the analyst-tier authoring pattern reuses a single canonical document (`mod-105` chapter 01) with a Colorado-view projection.

## NYC Local Law 144 — bias audits for automated employment decision tools

[New York City Local Law 144 of 2021](https://legistar.council.nyc.gov/LegislationDetail.aspx?ID=4344524&GUID=B051915D-A9AC-451E-81F8-6596032FA3F9) took effect 1 January 2023; the [Department of Consumer and Worker Protection began enforcement on 5 July 2023](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page). The [implementing rules are at 6 RCNY §§ 5-300 to 5-304](https://rules.cityofnewyork.us/wp-content/uploads/2023/04/DCWP-NOA-for-Use-of-Automated-Employment-Decisionmaking-Tools-2.pdf).

### The scope trigger

The Law regulates an **automated employment decision tool (AEDT)** — a computational process derived from machine learning, statistical modelling, data analytics, or artificial intelligence, that issues a simplified output including a score, classification, or recommendation, that is used to *substantially assist or replace* discretionary decision-making for making employment decisions that impact natural persons. It applies where the AEDT is used to screen candidates for employment or promotion within New York City.

### The obligations

The three load-bearing duties:

1. **Bias audit.** The AEDT must have been the subject of a **bias audit** conducted no more than one year prior to its use, by an *independent auditor*. The audit computes selection-rate and impact-ratio metrics by protected class (using EEOC race/ethnicity and sex categories), and by intersectional sex-and-race/ethnicity subgroups where sample size supports it.
2. **Public summary of the bias audit.** A summary of the most recent bias audit and the distribution date of the AEDT must be **published on the employer's website** and updated when a new audit is conducted.
3. **Candidate notice.** Candidates or employees who reside in NYC must be notified at least **10 business days before** the AEDT is used, that an AEDT will be used, the job qualifications and characteristics the tool will assess, and an opportunity to request an alternative selection process or accommodation.

`mod-104` chapter 04 walks the fairness-metric reading discipline for the bias-audit shape.

### How it interacts with the tracker

Tracker rows for NYC LL 144, minimum viable:

- `REG-2026-US-NY-001` — NYC Local Law 144 — AEDT bias audit. Scope trigger: AEDT used for hiring or promotion within NYC. Role: employer / employment agency.
- `REG-2026-US-NY-002` — NYC LL 144 — bias-audit public-summary publication. Same trigger; same role.
- `REG-2026-US-NY-003` — NYC LL 144 — candidate notice. Same trigger; same role.

Cross-references: EU AI Act Annex III point 4 (employment-decision high-risk category, which is *provider*/*deployer*-side but excluded from the Article 27 FRIA scoping filter for pure private deployers); Colorado AI Act deployer duties (consequential-decision framing covers employment); federal EEOC guidance (Title VII / ADA disparate-impact).

## Illinois BIPA — biometric implications for AI

The [Illinois Biometric Information Privacy Act (740 ILCS 14)](https://www.ilga.gov/legislation/ilcs/ilcs3.asp?ActID=3004) took effect 3 October 2008. It is not an AI-specific statute, but it is the most-litigated US biometric-privacy law and it applies wherever an AI system collects, uses, or stores biometric identifiers (retina or iris scans, fingerprints, voiceprints, or scans of hand or face geometry) or biometric information (any information based on biometric identifiers used to identify an individual) of Illinois residents.

### The scope trigger

The Act applies to any *private entity* in possession of biometric identifiers or biometric information — no revenue threshold, no residency-of-entity requirement; residence of the *subject* matters. AI systems commonly in scope: facial-recognition products, voice-biometric authentication, gait recognition, palm-vein authentication, retina scanners in workplace time-and-attendance systems, face-detection features that fingerprint faces to identify individuals across images.

### The obligations

The core duties under §15:

- **Written policy** publicly available establishing a retention schedule and destruction guidelines for biometric identifiers and information. Destroy the biometric data when the initial purpose has been satisfied or within three years of the individual's last interaction, whichever occurs first.
- **Informed written consent** obtained before collection, disclosing the specific purpose and the length of term for which the biometric data will be collected, stored, and used.
- **No sale, lease, trade, or otherwise profit** from an individual's biometric identifiers or biometric information.
- **No disclosure** except with consent, to complete a financial transaction requested or authorised by the subject, or as required by law.
- **Reasonable standard of care** in storing, transmitting, and protecting biometric data from disclosure.

### The private right of action

BIPA carries a **private right of action** — an individual whose rights are violated may sue for either actual damages or the greater of:

- **$1,000 per negligent violation**, or
- **$5,000 per intentional or reckless violation**,

plus attorneys' fees and injunctive relief. In [*Cothron v. White Castle System, Inc.*, 2023 IL 128004](https://ilcourts.info/SupremeCourt/2023/128004.pdf) the Illinois Supreme Court held that a separate BIPA claim accrues with each scan or transmission, though a subsequent statutory amendment in August 2024 ([Public Act 103-0769](https://www.ilga.gov/legislation/publicacts/103/PDF/103-0769.pdf)) limited per-scan accrual so that repeated collections from the same person in the same manner produce a single claim. The financial exposure remains significant.

### How it interacts with the tracker

Tracker rows for BIPA, minimum viable:

- `REG-2026-US-IL-001` — Illinois BIPA — written policy on biometric retention and destruction. Scope trigger: enterprise collects biometric identifiers or information from Illinois residents.
- `REG-2026-US-IL-002` — Illinois BIPA — informed written consent. Same trigger.
- `REG-2026-US-IL-003` — Illinois BIPA — reasonable-standard-of-care and prohibition on sale/lease/profit.

Cross-references: EU AI Act Article 5 (prohibited practices — untargeted scraping of facial images for facial-recognition databases) and Article 6 / Annex III point 1 (biometric identification as high-risk). GDPR Article 9 (biometric data as special-category data). Multiple state analogues have appeared — Texas ([CUBI](https://statutes.capitol.texas.gov/Docs/BC/htm/BC.503.htm)), Washington ([RCW 19.375](https://app.leg.wa.gov/rcw/default.aspx?cite=19.375)), and — in the general-privacy-law wave — provisions in California, Colorado, Virginia, and others. The tracker carries a *biometric-privacy state analogues* umbrella row that lists the analogues by state without a full row per state, until a specific inventory row is affected.

## The broader state-legislation tracker

Beyond the three anchor states, US states are actively legislating. Categories the tracker should have room for:

- **Comprehensive AI statutes.** Colorado is first; other states have similar bills in various stages (as of authoring, at least Texas, Virginia, Connecticut, and California have carried variants of comprehensive-AI or automated-decisionmaking legislation with different scopes).
- **Sector-specific AI statutes.** State insurance regulators are adopting variants of the [NAIC Model Bulletin on the Use of Artificial Intelligence Systems by Insurers](https://content.naic.org/sites/default/files/inline-files/2023-12-4%20Model%20Bulletin_Adopted_0.pdf) (chapter 06); state education departments are publishing AI guidance for schools; state licensing boards for healthcare are addressing AI in clinical practice.
- **Employment-and-hiring AI statutes.** [Illinois HB 3773 (2024)](https://www.ilga.gov/legislation/publicacts/103/PDF/103-0804.pdf) — amendments to the Illinois Human Rights Act — took effect 1 January 2026 and imposes obligations on employers using AI for employment decisions.
- **Comprehensive consumer-privacy statutes.** [California CCPA/CPRA](https://oag.ca.gov/privacy/ccpa), [Virginia CDPA](https://law.lis.virginia.gov/vacodefull/title59.1/chapter53/), [Colorado CPA](https://coag.gov/resources/colorado-privacy-act/), [Connecticut CTDPA](https://portal.ct.gov/AG/Sections/Privacy/The-Connecticut-Data-Privacy-Act), [Utah UCPA](https://le.utah.gov/xcode/Title13/Chapter61/13-61.html), and roughly two dozen others as of 2026. Most carry provisions on **automated decisionmaking** or **profiling** relevant to AI systems, and — in the case of CCPA/CPRA — the California Privacy Protection Agency has finalised specific [automated-decisionmaking-technology regulations](https://cppa.ca.gov/regulations/) that engage AI use cases directly (chapter 07).

Analyst-tier discipline: not every state statute needs a full row on day one. A *state-legislation horizon-scan* tab holds bills-in-progress or newly-enacted statutes with a single-paragraph summary, an effective date, and a *watch-list* status. A statute is promoted to the main tracker when either (a) its effective date is within the current rolling six-month window, or (b) an inventory row is identified as affected. A statute is retired from the horizon-scan when it fails to pass in a session or is preempted by later action.

## Where the US state stack stops for the analyst

- **Not a state-by-state legal opinion.** The tracker names the state statute and the specific obligation; whether a specific system is a covered *automated employment decision tool*, or is a *substantial factor* in a consequential decision, or handles *biometric identifiers* as BIPA defines them, is counsel's characterisation.
- **Not the enterprise's state-affairs strategy.** Whether the enterprise submits comments on a state rulemaking or advocates for statutory amendments is a policy decision; the tracker records the rulemaking and the comment deadline, not the enterprise's position.
- **Not the plaintiff bar's docket.** BIPA and other private-right-of-action statutes generate a heavy stream of class-action filings; those are relevant to counsel's risk-management view but the tracker cites primary regulatory sources, not case dockets.
- **Not a preemption analysis.** Federal preemption of state AI statutes is an active area of legal debate; the analyst names the state statute and defers the preemption question to counsel.

## What to memorise

- **Colorado AI Act** — first US comprehensive AI statute; effective date 1 February 2026 (verify); developer and deployer duties; consequential-decision framing; Attorney General enforcement; no private right of action.
- **NYC LL 144** — bias audit + public summary + candidate notice for automated employment decision tools; effective January 2023, enforcement July 2023; DCWP enforces.
- **Illinois BIPA** — biometric identifiers and information; written policy, informed written consent, no sale; private right of action with statutory damages of $1,000 negligent / $5,000 intentional; per-scan accrual limited by 2024 amendment.
- **The state stack is heterogeneous** — the tracker has an anchor-state row set (CO / NYC / IL), a comprehensive-consumer-privacy row set, a horizon-scan tab for bills-in-progress, and a promotion rule that moves rows into the main tracker on effective-date-within-window or inventory-row-affected triggers.
- **The state analogues for biometrics** — Texas CUBI, Washington RCW 19.375, and state-privacy-law analogues — sit as an umbrella row until a specific inventory row engages one.

## Summary

The US state stack is heterogeneous, active, and often first-to-attach to an AI system operating nationally. The Colorado AI Act is the anchor comprehensive statute (effective 1 Feb 2026, developer and deployer duties, consequential-decision framing); NYC Local Law 144 is the anchor employment-AI statute (bias audit, public summary, candidate notice); and Illinois BIPA is the anchor biometric-privacy statute with the private right of action that makes it disproportionately consequential. The tracker holds a row per obligation, cross-references the EU AI Act and US federal rows where the substantive obligation overlaps, and maintains a horizon-scan tab for bills-in-progress that promotes to the main tracker on effective-date-within-window or inventory-row-affected triggers. Chapter 06 walks the sector regulators layered on top; chapter 07 develops the privacy-law flagging discipline that decides when a US-state-privacy or federal-privacy hook needs to be handed to counsel.
