# Privacy Laws and the Flagging Discipline — GDPR Article 22, GDPR Article 35, CCPA/CPRA, and HIPAA

## Why this chapter

Privacy laws are the layer of the regulatory landscape where the analyst most often needs to *hand off* — not opine, not draft, not decide, but flag to counsel or to the privacy office with enough specificity that they can pick up the file and act. This chapter defines the discipline: what triggers a flag, what a flag says, what the analyst does *not* say when raising a flag, and how the flag is recorded so that it is discoverable.

Four instruments carry the load:

- **[GDPR Article 22](https://gdpr-info.eu/art-22-gdpr/)** — solely-automated individual decision-making with legal or similar significant effect.
- **[GDPR Article 35](https://gdpr-info.eu/art-35-gdpr/)** — the DPIA trigger, walked at length in `mod-105` chapter 04.
- **[California CCPA/CPRA](https://oag.ca.gov/privacy/ccpa)** — with the [California Privacy Protection Agency's automated-decisionmaking-technology (ADMT) regulations](https://cppa.ca.gov/regulations/).
- **[HIPAA](https://www.hhs.gov/hipaa/for-professionals/index.html)** — Privacy, Security, and Breach Notification rules, applied wherever an AI system touches protected health information.

The flagging discipline is analyst-tier. It does not require depth in privacy law — that is the DPO's, the privacy counsel's, and (in the US) the general counsel's. It requires recognising the shape of the trigger, phrasing the flag as a *question* rather than a *conclusion*, and recording it so the file survives the analyst going on leave.

## GDPR Article 22 — solely-automated decisions with legal or similar significant effect

Article 22(1) grants the data subject the right *not to be subject to a decision based solely on automated processing, including profiling, which produces legal effects concerning him or her or similarly significantly affects him or her*. Article 22(2) sets three exemption bases (necessary for a contract, authorised by Union or Member State law with suitable safeguards, or based on explicit consent). Article 22(3) requires *suitable measures to safeguard the data subject's rights and freedoms and legitimate interests, at least the right to obtain human intervention on the part of the controller, to express his or her point of view and to contest the decision*. Article 22(4) prohibits solely-automated decisions based on special-category data (Article 9) except with explicit consent or substantial public interest.

Three tests decide whether Article 22 is engaged:

1. **Is the decision *solely* automated?** The [WP 251 rev.01 guidance](https://ec.europa.eu/newsroom/article29/items/612053) — endorsed by the EDPB — establishes that *meaningful human involvement* prevents a decision from being solely automated. Rubber-stamp human review (a caseworker who invariably accepts the model's output) is not meaningful; substantive human review that can and does modify the decision is meaningful.
2. **Does the decision produce *legal effects*?** Cancellation of a contract, denial of a benefit, refusal of admission to a country, disciplinary action — legal effects are ones that affect the person's legal status or rights.
3. **Does the decision *similarly significantly* affect the person?** Even absent legal effect, decisions with comparable significance — automatic refusal of credit, denial of e-recruitment, differential pricing at levels that effectively exclude access — engage Article 22.

The analyst's flag is written when *any two of the three tests plausibly land yes on a specific inventory row*. The flag says:

> *Inventory row `INV-XXXX-XXXX` (`[system name]`) is a candidate for GDPR Article 22 engagement. Test outcomes: solely-automated — [analyst's read]; legal effects — [analyst's read]; similarly significant effects — [analyst's read]. Requesting privacy counsel's opinion on whether Article 22 is engaged and, if so, which Article 22(2) exemption basis and Article 22(3) safeguards apply. Deployment date `[date]`. This flag does not constitute an analyst legal opinion.*

The flag is filed in the inventory row's *counsel questions* field and referenced from the impact-assessment corpus. It is *not* the analyst deciding Article 22 applies; it is the analyst noting that it plausibly could and routing to the person who owns the decision.

## GDPR Article 35 — the DPIA trigger

Article 35 is walked at length in `mod-105` chapter 04. The flagging discipline is compressed here:

- If two or more [WP 248 rev.01](https://ec.europa.eu/newsroom/article29/items/611236) nine-criteria filter items are met, a DPIA is *presumptively required*.
- If the system is on the relevant supervisory authority's [Article 35(4) always-required list](https://www.edpb.europa.eu/), a DPIA is required regardless of the WP 248 outcome.
- If the DPIA's residual risks stay High after mitigation, Article 36 *prior consultation* with the supervisory authority is required.

The analyst's flag: *inventory row `INV-XXXX-XXXX` engages [count] of the WP 248 nine criteria — [list]. Requesting DPO to open a DPIA under GDPR Article 35, and — pending DPIA completion — Article 36 prior-consultation determination.* Again, the flag routes; the DPO decides.

## CCPA/CPRA and the ADMT regulations

The [California Consumer Privacy Act of 2018 (CCPA)](https://cppa.ca.gov/regulations/consumer_privacy_act.html), as amended by the [California Privacy Rights Act of 2020 (CPRA)](https://oag.ca.gov/privacy/ccpa), is the US anchor state consumer-privacy statute. Its Article 22-analogous provisions on **automated decisionmaking technology (ADMT)** were the subject of substantial California Privacy Protection Agency rulemaking through 2024 and 2025.

The [CPPA-finalised ADMT regulations](https://cppa.ca.gov/regulations/) — <!-- needs-research: verify the current status and effective date of the CPPA ADMT regulations. As of 2026-08-01 the CPPA had proceeded through several rounds of ADMT rulemaking; the finalised effective text and any risk-assessment / cybersecurity-audit companion regulations must be verified against the [CPPA rulemaking page](https://cppa.ca.gov/regulations/) before citing to a covered inventory row. --> — establish:

- **Pre-use notice** — businesses must provide consumers with a pre-use notice explaining the use of ADMT for a *significant decision concerning the consumer*, before the decision is made.
- **Right to opt out** — consumers have a right to opt out of the use of ADMT for a significant decision, subject to defined exceptions.
- **Right to access** — consumers have a right to access meaningful information about how the ADMT was used with respect to the consumer.
- **Risk assessments** — businesses must conduct risk assessments before processing that presents significant risk to consumer privacy, including certain ADMT uses. The risk-assessment content and submission obligations layer alongside the enterprise's GDPR-DPIA and 42005 canonical-document work (`mod-105` chapter 01).

*Significant decision* is defined term — it includes decisions producing legal or similarly significant effects, comparable to the GDPR Article 22 threshold. The analyst-tier flag structure is analogous: name the inventory row, apply the CCPA/CPRA-and-ADMT tests, route to counsel and the privacy office.

The other state-privacy analogues — Virginia CDPA, Colorado CPA, Connecticut CTDPA, Utah UCPA, and roughly two dozen others as of 2026 — each carry their own profiling and consumer-rights provisions. The analyst-tier discipline is to track the state-privacy statutes as a single tracker sub-branch and flag inventory rows against the states in which the enterprise processes personal information of state residents.

## HIPAA — protected health information touched by AI

The [HIPAA Privacy Rule (45 CFR Part 164 Subpart E)](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-164/subpart-E), [Security Rule (45 CFR Part 164 Subpart C)](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-164/subpart-C), and [Breach Notification Rule (45 CFR Part 164 Subpart D)](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-164/subpart-D) apply to *covered entities* and *business associates*. Where an AI system processes protected health information (PHI) — patient records, claim data with identifiers, appointment histories — the analyst-tier flags to raise:

- **Is the enterprise a covered entity or a business associate?** Covered entities (health plans, health care clearinghouses, health care providers who transmit health information electronically in connection with certain transactions) owe direct HIPAA duties. Business associates (vendors and contractors handling PHI on behalf of a covered entity) owe HIPAA duties by regulation and by [business associate agreement (BAA)](https://www.hhs.gov/hipaa/for-professionals/covered-entities/sample-business-associate-agreement-provisions/index.html) with the covered entity.
- **Is the AI vendor a business associate that requires a BAA?** Any third-party AI service that receives PHI to perform a function on behalf of the covered entity typically requires a BAA. Enterprise contracts with hosted-AI APIs where PHI is placed into the prompt are the specific case to flag — a hosted model API used without a BAA on PHI is a covered-entity HIPAA violation.
- **Does the enterprise's use case engage the [minimum-necessary rule (45 CFR 164.502(b))](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-164/subpart-E)?** Yes for most uses — the analyst-tier flag is to confirm that the AI system's inputs are limited to the minimum PHI necessary for the intended purpose.
- **Are individual rights (access, amendment, accounting of disclosures under 164.524–528) affected?** AI system outputs stored in the designated record set are subject to individual-access rights; the analyst flags for the covered entity's privacy officer to confirm the enterprise's individual-access process covers AI-generated records.
- **Does the deployment trigger [Section 1557 of the ACA](https://www.hhs.gov/civil-rights/for-individuals/section-1557/index.html) patient-care-decision-support-tool obligations?** Chapter 03 walks the Section 1557 rule. The analyst flags for the covered entity's compliance officer.

The analyst's flag structure: *inventory row `INV-XXXX-XXXX` processes PHI; enterprise role is [covered entity / business associate]; open items — BAA status with [vendor], minimum-necessary confirmation, individual-access process coverage, Section 1557 rule engagement. Requesting privacy officer / OCR-liaison counsel review.*

## The flagging discipline — three rules

Across all four instruments the analyst's flagging discipline is the same:

1. **The flag is a question, not a conclusion.** The analyst does not write *this system violates Article 22*; the analyst writes *this system is a candidate for Article 22 engagement — requesting counsel's opinion*. The distinction is not cosmetic — a written legal conclusion by a non-lawyer creates exposure that a properly-framed question does not.
2. **The flag names the inventory row and cites the trigger.** *This system might be a problem* is not a flag. *`INV-2026-0088` (`MCDA-Benefits`) — appears to meet WP 248 criteria 1 (evaluation/scoring), 2 (automated decision-making with similarly significant effect), and 8 (innovative use of new technology). Requesting DPO to open DPIA under GDPR Article 35* — that is a flag.
3. **The flag is recorded, not spoken.** A flag mentioned in a hallway conversation is not a flag. The flag lives in the inventory row's *counsel questions* field and in the impact-assessment corpus's *related-artefact references* section; a copy goes to counsel and the privacy office via the enterprise's documented channel.

## The counsel/privacy-office interface

The analyst's counterpart varies by jurisdiction and enterprise:

- **EU GDPR** — the enterprise's [Data Protection Officer (DPO)](https://edpb.europa.eu/sme-data-protection-guide/data-protection-officer_en) where designated under Article 37; otherwise privacy counsel. The DPO consultation is a required input into the DPIA (Article 35(2)).
- **US HIPAA** — the covered entity's privacy officer (required under 45 CFR 164.530(a)(1)) and security officer (required under 45 CFR 164.308(a)(2)); OCR liaison counsel where an enforcement matter is open.
- **CCPA/CPRA and state privacy laws** — the enterprise's privacy team and general counsel; where the enterprise operates in multiple states, a single privacy-programme lead typically covers.
- **CoE Framework Convention** — the treaty is inter-state; direct private-sector engagement is limited. Signatory-state implementation is what attaches operationally (chapter 02).

The routing is documented on the tracker's *notes for counsel* column and mirrored in the inventory row's *counsel questions* field. When a flag is raised, the analyst does not chase the answer — the answer lands in a specific field, dated, and signed off by the counsel or privacy officer who opined.

## Concrete example — the MCDA-Benefits flag block

Reusing the MCDA-Benefits variant from `mod-105` chapter 03 (public employment agency using MCDA to draft benefits-eligibility response text). The flag block the analyst attaches to `INV-2026-0088`:

- **GDPR Article 22 flag.** Solely-automated — no; every draft is reviewed by a caseworker before dispatch, per treatment plan; the meaningful-human-involvement threshold appears met. Legal effects — yes; the underlying eligibility decision determines access to essential benefits. Similarly significant effects — yes. Analyst-tier read: Article 22 does not appear engaged because the meaningful-human-review test is met, but the caseworker's review-behaviour is the load-bearing safeguard and this depends on the caseworker training and monitoring in the treatment plan holding up in practice. Requesting DPO opinion.
- **GDPR Article 35 DPIA flag.** WP 248 criteria met: 1 (evaluation/scoring), 2 (automated decision-making with similarly significant effect via the caseworker workflow), 4 (arguably — some applicant records include sensitive information), 7 (vulnerable data subjects — benefits applicants often are), 8 (innovative use of generative AI). Five criteria; DPIA presumptively required. DPO to open DPIA under Article 35; residual-High cases route to Article 36 prior consultation.
- **CCPA/CPRA flag.** Not applicable — no California-resident data subjects in scope for this deployment.
- **HIPAA flag.** Not applicable — no PHI processed; deployment is in a public-benefits (non-healthcare) context.

Every field is a question or a *not applicable* with a reason; nothing is a legal conclusion.

## Where the flagging discipline stops for the analyst

- **Not a legal opinion.** The flags name the trigger and route the question; the opinion belongs to counsel or the DPO.
- **Not a comprehensive privacy-law scan.** The four instruments walked in this chapter cover the majority of the analyst's day-to-day flagging surface, but jurisdictions layer additional instruments (Quebec Law 25, Brazil LGPD, Singapore PDPA, and others) — those are added to the tracker as the enterprise's data-processing footprint attaches to them, and flags are constructed on the same *question, not conclusion* pattern.
- **Not the resolution.** Once the flag is filed, the analyst tracks the resolution in the inventory row's *counsel questions* field but does not draft the resolution. Deploying before the resolution lands is a business decision; the analyst records that the deployment happened *pending resolution* and — if the residual risk is High — escalates via the routing pattern from `mod-103` chapter 05.
- **Not a substitute for the enterprise's privacy programme.** The enterprise's privacy programme is broader than AI — records-of-processing, subject-rights operations, breach response, vendor-privacy diligence, cross-border transfer mechanisms. The analyst's flagging discipline is the AI-specific slice.

## What to memorise

- **The three GDPR Article 22 tests** — solely automated, legal effects, similarly significant effects. Two-of-three-yes triggers the flag.
- **The WP 248 nine-criteria filter** — two-or-more triggers a presumptive DPIA under Article 35.
- **The CCPA/CPRA ADMT regulation shape** — pre-use notice, right to opt out, right to access, risk assessment. Verify current text at the CPPA before citing.
- **The HIPAA covered-entity/business-associate distinction** — BAA required for AI vendors handling PHI on behalf of a covered entity; hosted-API deployment on PHI without a BAA is a specific case to flag.
- **The three flagging rules** — question not conclusion; name the row and cite the trigger; record, do not speak.

## Summary

Privacy laws are where the analyst most often hands off. The four load-bearing instruments — GDPR Article 22, GDPR Article 35, CCPA/CPRA with the CPPA ADMT regulations, and HIPAA — each engage a specific pattern of inventory-row triggers, and each has a specific counterpart inside the enterprise: DPO for GDPR, privacy officer and general counsel for CCPA/CPRA, privacy officer and OCR-liaison counsel for HIPAA. The analyst-tier discipline is to write flags as questions rather than conclusions, to name the inventory row and cite the trigger explicitly, and to record the flag in the inventory row's *counsel questions* field so the file survives handovers. The deep opinion belongs to counsel; the flag belongs to the analyst.
