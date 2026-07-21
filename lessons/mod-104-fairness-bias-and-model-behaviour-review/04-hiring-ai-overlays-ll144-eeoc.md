# Hiring AI — NYC Local Law 144, EEOC Title VII, and the Analyst Overlay

## Why this chapter

Hiring is the most-regulated single use case for AI. Screening tools, résumé rankers, and video-interview scorers touch employment law that predates AI by half a century (Title VII of the Civil Rights Act, 1964) and AI-specific rules enacted in the last few years ([NYC Local Law 144, 2023](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page); [Illinois AI Video Interview Act, 2020](https://www.ilga.gov/legislation/publicacts/101/101-0260.htm); [Colorado SB 24-205, 2024](https://leg.colorado.gov/bills/sb24-205)). The [EU AI Act (Regulation (EU) 2024/1689)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) puts recruitment squarely in Annex III item 4 — high-risk with the full documentation and oversight obligations.

When a hiring AI use case lands at intake, the analyst is unlikely to be new to *the technology* but is very likely to be new to *the overlay*. This chapter walks the overlays the analyst-tier work uses.

## The Title VII framing

[Title VII of the Civil Rights Act (1964)](https://www.eeoc.gov/statutes/title-vii-civil-rights-act-1964) prohibits employment discrimination on the basis of race, color, religion, sex, or national origin. Two doctrines are load-bearing.

- **Disparate treatment.** Intentional discrimination. A rule that treats candidates differently because of a protected characteristic. Analyst-tier signal: any explicit use of a protected attribute as an input feature — or clear evidence the ML team used one — is a stop.
- **Disparate impact.** A facially neutral practice that produces a substantially different outcome across protected groups, with no defensible business necessity. Analyst-tier signal: the four-fifths rule below 0.80.

The [EEOC's Uniform Guidelines on Employee Selection Procedures](https://www.eeoc.gov/uniform-guidelines-employee-selection-procedures) codify the four-fifths rule and the burden-shift structure — once a plaintiff shows disparate impact, the employer must show the practice is *job-related and consistent with business necessity*, after which the plaintiff can still prevail if a less-discriminatory alternative exists.

The [EEOC guidance "Assessing Adverse Impact in Software, Algorithms, and Artificial Intelligence"](https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial) (May 2023) applies this frame to AI selection tools. Two key claims:

- The four-fifths rule applies to AI selection procedures, and vendors who claim otherwise are wrong.
- The employer using an AI selection tool is responsible for the disparate-impact assessment, not the vendor.

Analyst-tier work: any hiring-AI risk assessment must include a disparate-impact analysis, must cite the Uniform Guidelines, and must have a plan for the less-discriminatory-alternative review. The plan is not the analyst's to author, but the analyst's to make sure exists.

## NYC Local Law 144 — the automated employment decision tool (AEDT) rule

[NYC LL 144](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page), in force since July 2023, is the first US local law imposing AI-specific hiring obligations. It applies to any *automated employment decision tool* used to make an employment decision (screening, hiring, promotion) for a candidate for a role in NYC.

Employer obligations:

- **Annual independent bias audit.** Conducted within one year of use. Auditor must be independent of the tool's development and use.
- **Published audit summary.** The employer must publicly post the summary of the audit on the employer's website.
- **Candidate notification.** At least 10 business days before use, the employer must notify candidates that the tool is being used, the job qualifications and characteristics the tool assesses, and how to request an accommodation or alternative selection process.
- **Data protection information.** The employer must publish, on the employer's website, the type of data collected by the AEDT and, if applicable, the retention period.

Audit shape (per DCA rules):

- Impact ratio by sex categories.
- Impact ratio by race/ethnicity categories.
- Impact ratio by intersectional categories (sex × race/ethnicity).
- Selection rate per category.
- Sample size per category, with the requirement that categories with too-small samples be disclosed.
- The auditor's independence attested.

Analyst-tier check at intake: is the tool used for candidates for NYC-based roles? If yes, LL 144 obligations kick in. Even if the tool is not called an "AEDT" by the vendor, the substantive test is *substantially assist or replace discretionary decision-making*.

<!-- needs-research: verify the current DCA implementation rule text and the specific audit-scope requirements against the latest published rule; the LL 144 rulemaking has produced multiple updates. -->

## Other US state and local overlays

Beyond NYC, several US jurisdictions have enacted or proposed hiring-AI rules. The analyst tracks jurisdictions the enterprise operates in.

- **[Illinois Artificial Intelligence Video Interview Act](https://www.ilga.gov/legislation/publicacts/101/101-0260.htm)** — applies to AI use in analysing video interviews. Requires notification, consent, and limits on data retention.
- **[Maryland HB 1202](https://mgaleg.maryland.gov/mgawebsite/Legislation/Details/hb1202?ys=2020rs)** — restricts use of facial-recognition in job interviews.
- **[Colorado SB 24-205](https://leg.colorado.gov/bills/sb24-205)** — the first US-state comprehensive AI act; risk-based obligations on high-risk AI including consequential-decision tools like employment.
- **[California AB 331 / AB 2930](https://leginfo.legislature.ca.gov/) and successor bills** — automated-decision-tool notice and assessment requirements, evolving through the state legislature. <!-- needs-research: verify the currently-enacted California bill and its effective date; the AI-in-employment landscape in California has moved multiple times. -->

Analyst-tier tracker: what jurisdictions does the tool operate in? What are the notification, audit, and assessment obligations in each? The tracker feeds `mod-106-regulatory-tracking-and-jurisdictions`.

## EU AI Act — hiring is Annex III

Under [EU AI Act Regulation (EU) 2024/1689](https://eur-lex.europa.eu/eli/reg/2024/1689/oj), *AI systems intended to be used for recruitment or selection of natural persons* fall under Annex III item 4 and are therefore **high-risk**. Obligations that flow to the deployer include (paraphrased — cite the article text for the definitive list):

- Article 26 deployer obligations — human oversight, monitoring, log-keeping, cooperation with authorities.
- Article 27 — Fundamental Rights Impact Assessment before first deployment.
- Article 50 transparency — the candidate is informed they are interacting with an AI system.

Providers of the tool carry the Article 8–15 obligations (risk-management, data governance, technical documentation, logging, transparency, human oversight, accuracy / robustness / cybersecurity, conformity assessment, registration).

Analyst-tier work at intake: tier the tool as high-risk, initiate the FRIA (see `mod-105`), and record the specific EU AI Act obligations the enterprise assumes as deployer.

## The disparate-impact / four-fifths pass — analyst script

For a hiring AI intake, the analyst runs the following pass:

1. **Identify protected attributes** the disparate-impact analysis will cover — at minimum sex and race/ethnicity; age (ADEA), disability (ADA), national origin, religion for coverage of Title VII/ADEA/ADA breadth.
2. **Confirm the analysis dataset** — realistic sample of candidates from the jurisdictions the tool serves; not just training data.
3. **Compute selection rates and impact ratios** per protected category and intersection. This is the ML team's work; the analyst reviews.
4. **Flag any impact ratio below 0.80.** File the finding; open the business-necessity / less-discriminatory-alternative review with the hiring-legal team.
5. **Check sample sizes.** Categories below N=100 are unreliable; flag.
6. **Check calibration and precision per group.** Even where the four-fifths pass is clean, unequal precision or calibration can produce downstream harms.
7. **Verify candidate notification.** Is the required disclosure text on the careers site? Does it name the tool?
8. **Verify the annual LL 144 audit** (if applicable) is scheduled and the auditor is independent.
9. **File the register entries** with all overlays anchored.

That pass takes a day of analyst work for a mid-complexity tool.

## Boundary — what the analyst does not do

- **Not the disparate-impact analysis itself.** The ML team runs the numbers; the analyst reads and files.
- **Not the business-necessity legal argument.** Legal owns the argument. The analyst provides evidence.
- **Not the less-discriminatory-alternative analysis.** This is a joint ML + Legal work; the analyst tracks that it is happening.
- **Not the LL 144 audit.** Independent auditor conducts. The analyst verifies the audit exists, verifies independence, and files the summary in the governance record.

## Concrete example — a résumé-triage intake

Intake: a hosted-model résumé-triage tool for a Fortune-500 enterprise with offices in NYC, London, Toronto, Sydney, and Bangalore.

Analyst-tier overlay:

- **EU AI Act:** Annex III item 4 → high-risk. Article 27 FRIA required (deployer of essential-service adjacent — check whether the enterprise's deployer status attaches). Article 26 deployer obligations attach.
- **US federal:** Title VII / EEOC Uniform Guidelines apply. Disparate-impact analysis required.
- **NYC LL 144:** applies to NYC-based roles. Annual independent audit; candidate notification; published summary.
- **Illinois AI Video Interview Act:** does not apply — no video interviews.
- **Colorado SB 24-205:** applies to Colorado-based roles once phased in; consequential-decision-tool obligations.
- **UK:** [Equality Act 2010](https://www.gov.uk/guidance/equality-act-2010-guidance) — analogous disparate-impact framing; no AI-specific rule as of writing beyond regulator guidance.
- **Canada:** [Canadian Human Rights Act](https://laws-lois.justice.gc.ca/eng/acts/H-6/) and provincial equivalents — analogous framing.
- **India (Bangalore):** [Article 15/16 of the Indian Constitution](https://www.indiacode.nic.in/) prohibit discrimination in state employment; private employment is thinner. Local labour codes govern process.

The register carries a jurisdictional table — one row per jurisdiction, per obligation. The tracker feeds `mod-106`.

## What to memorise

- The **two Title VII doctrines**: disparate treatment; disparate impact — plus the four-fifths rule and the burden-shift structure.
- The **EEOC 2023 guidance** — the four-fifths rule applies to AI selection tools, and the employer is responsible for the analysis.
- The **NYC LL 144 four obligations** — annual independent audit; published summary; candidate notification; data-protection disclosure.
- The **EU AI Act framing for hiring** — Annex III item 4; Article 26 deployer obligations; Article 27 FRIA.
- The **analyst-tier disparate-impact pass** — the nine steps.
- The **boundary** — analyst does not run the analysis, does not argue business necessity, does not conduct the LL 144 audit.

## Summary

Hiring AI is the most-regulated single AI use case, with Title VII / EEOC Uniform Guidelines / the 2023 EEOC AI guidance at the federal US level, NYC LL 144 and analogous state/local rules, and the EU AI Act Annex III item 4 all applying in parallel. The analyst's job at intake is to identify which overlays apply for the jurisdictions and roles served, verify the disparate-impact pass has been run, verify LL 144 audit and notification obligations are met where applicable, and file register entries with the overlay-specific anchors. The methodology and the legal argument belong to the ML team and to Legal respectively.
