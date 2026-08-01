# Exercise 04 — NYC LL 144 and EEOC Hiring Drill

**Estimated effort:** 2 hours
**Grounding chapter:** [04 — Hiring AI — NYC Local Law 144, EEOC Title VII, and the Analyst Overlay](../04-hiring-ai-overlays-ll144-eeoc.md)

## Objective

Take a hiring-AI use case at intake and produce the full analyst-tier overlay: the Title VII / EEOC framing, the NYC LL 144 obligations checklist, the EU AI Act Annex III attachment, the jurisdictional overlay table, and the disparate-impact-analysis pass. The output is what the analyst hands to the hiring-legal team and to the ML team so the risk assessment can proceed with the correct set of statutory anchors on file.

After this exercise you should be able to sit at intake for a hiring-AI tool and, within two hours, produce a complete overlay pack that names every applicable regulation for every jurisdiction the tool serves, cites each to a primary instrument, and files the register entry with the correct anchors.

## Prerequisites

- Chapter 04 read; the two Title VII doctrines (disparate treatment / disparate impact), the four LL 144 obligations, and the nine-step analyst pass fresh in memory.
- The following primary instruments open — you will cite each at least once in the deliverable:
  - [EEOC Uniform Guidelines on Employee Selection Procedures](https://www.eeoc.gov/uniform-guidelines-employee-selection-procedures).
  - [EEOC — Assessing Adverse Impact in Software, Algorithms, and AI (May 2023)](https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial).
  - [NYC Local Law 144 — Automated Employment Decision Tools](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page) and the DCA implementation rules.
  - [EU AI Act (Regulation (EU) 2024/1689)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) — Annex III item 4; Articles 26, 27, 50.
  - [Title VII of the Civil Rights Act (1964)](https://www.eeoc.gov/statutes/title-vii-civil-rights-act-1964).
- Skimmed: at least two of [Illinois AI Video Interview Act](https://www.ilga.gov/legislation/publicacts/101/101-0260.htm), [Maryland HB 1202](https://mgaleg.maryland.gov/mgawebsite/Legislation/Details/hb1202?ys=2020rs), [Colorado SB 24-205](https://leg.colorado.gov/bills/sb24-205), [California AB 2930 / SB 942 successors](https://leginfo.legislature.ca.gov/) — the exact state overlay set that applies depends on which use case you pick.
- Fluency in the intake row shape from `mod-102` and the register scoring pass from `mod-103` — you will not re-triage or re-score; you will produce the *overlay* that anchors those artefacts.

## Problem statement

Pick **one** of the following hiring-AI intake use cases as your target. All three deliberately span multiple jurisdictions so the overlay table does real work.

### Hiring-A — ResuméRank Screener (large US-plus-EU employer)

- **System.** Vendor-hosted résumé-screening tool that scores incoming résumés against a job's requirements and returns a ranked list to the recruiter.
- **Deployer.** Fortune-500 enterprise; hiring in the US (New York City, Illinois, Colorado, California, plus 20 other states), Ireland, Germany, France, and the UK.
- **Automation.** Advisory — the recruiter reviews the ranked list and moves candidates forward manually.
- **Data.** Résumé text; job-description text; historical hire-outcome data used to train the model (bias-in-the-training-data question).
- **Vendor.** Third-party SaaS; vendor publishes an LL 144-compliant bias audit summary annually.

### Hiring-B — HireLoop Video Interview Analyser (mid-size US employer)

- **System.** Vendor-hosted video-interview platform that records candidate answers and produces a *fit score* from a combination of transcript-text scoring and (per vendor claim) prosodic / paralinguistic signals.
- **Deployer.** Mid-size US enterprise; hiring in Illinois, Maryland, New York City, and 15 other states. No non-US hiring.
- **Automation.** Advisory — the recruiter reviews scored interviews and interview transcripts before advancing candidates.
- **Data.** Video and audio; transcript text; candidate demographic self-disclosure (voluntary; used for the LL 144 impact-ratio report).
- **Vendor.** Third-party SaaS; vendor claims the paralinguistic scoring component was disabled by default after 2023.

### Hiring-C — SkillsMatch Public-Sector Placement Tool (state workforce agency)

- **System.** In-house ML classifier that scores unemployment-insurance recipients for placement recommendations to open state-funded job postings and re-training programs.
- **Deployer.** US state workforce development agency. Deployed statewide; no non-US or private-sector use.
- **Automation.** Advisory — the caseworker reviews the recommendation in the intake meeting.
- **Data.** Jobseeker profile; job-posting metadata; some protected-class inference through proxy features (ZIP, education, employment history).
- **Vendor.** SaaS vendor for the model-hosting layer; in-house ownership of the model itself.

## Requirements

Produce one Markdown file, `mod-104-ex-04-hiring-overlay.md`, with the following sections in order.

### Section 1 — intake summary

A short (~1 page) intake summary for the chosen system using the mod-102 intake shape. Include the mod-103-style tier tagging (enterprise tier + EU AI Act tier + any FSI / sector overlays). This is the same shape you already know from `mod-102` and `mod-103`; keep it tight.

### Section 2 — Title VII / EEOC overlay

Two subsections.

- **Disparate treatment.** Is the tool at risk of a disparate-treatment claim? Cite the Title VII text and the EEOC's Uniform Guidelines. Name specifically the datapoints that would fire an analyst-tier stop (explicit use of a protected attribute as an input feature; clear evidence of intentional differential treatment).
- **Disparate impact.** The four-fifths rule pass. Cite the Uniform Guidelines and the 2023 EEOC AI guidance. Describe what a disparate-impact assessment for this tool would need to cover (protected attributes; dataset shape; sample-size floor; intersectional axes). Do not run the assessment — chapter 04 is explicit that this is ML-team scope; state what the analyst *asks* the ML team to produce.

### Section 3 — NYC LL 144 obligations checklist

The four LL 144 obligations from chapter 04:

1. **Annual independent bias audit.** Verify the audit exists, is within 12 months, and covers the sex / race-ethnicity / intersectional categories required. Note the auditor and evidence of independence.
2. **Published audit summary.** Verify the employer has posted the summary on its website. Cite the URL if you can find it for a real vendor's audit; otherwise, state where the enterprise would post it.
3. **Candidate notification.** Verify the notification is on the enterprise careers page, is at least 10 business days before use, and includes the required content (tool identified; job qualifications and characteristics assessed; how to request an accommodation / alternative process).
4. **Data-protection information.** Verify the enterprise has published the data categories collected and the retention period.

For each obligation, produce a verdict: **satisfied / partially satisfied / gap / not applicable** (LL 144 only applies to candidates for NYC-based roles — Hiring-A and Hiring-B qualify, Hiring-C does not). For any *gap*, name the ask: what evidence is required, who owns it, and by when.

### Section 4 — EU AI Act Annex III attachment

Applies to Hiring-A only in the three cases as stated, because Hiring-B and Hiring-C do not deploy in the EU. State this explicitly at the top of the section — do not silently omit.

If Hiring-A: tier the system under Annex III item 4 (high-risk). Name the deployer obligations (Article 26 — human oversight, monitoring, log-keeping, cooperation with authorities), the FRIA obligation (Article 27), and the transparency obligation (Article 50 — the candidate is informed they are interacting with an AI system). For each obligation, name the artefact the enterprise must produce and the module in this track that owns the depth (Article 26 monitoring → `mod-109`; Article 27 FRIA → `mod-105`; Article 50 disclosure → `mod-110`).

If Hiring-B or Hiring-C: write a one-sentence "N/A — no EU deployment" note plus a two-sentence forward-look on what would change if the enterprise did decide to hire in the EU next year.

### Section 5 — jurisdictional overlay table

One row per jurisdiction the chosen system serves. Columns:

- Jurisdiction (state / country / city).
- Applicable statute or rule.
- Primary obligation the deployer takes on.
- Analyst artefact required.
- Owner (Legal / Talent / Analyst) and the module in this track that owns the depth.

For Hiring-A, cover at minimum: New York City (LL 144); Illinois (AI Video Interview Act — determine applicability); Colorado (SB 24-205); California (successor to AB 2930 — mark `<!-- needs-research: verify current CA enacted statute and effective date -->` if uncertain); Ireland / Germany / France (EU AI Act); UK ([Equality Act 2010](https://www.gov.uk/guidance/equality-act-2010-guidance)); plus a catch-all row for the remaining 20 US states citing the underlying federal Title VII / EEOC frame.

For Hiring-B, cover at minimum: Illinois (AI Video Interview Act — direct applicability); Maryland (HB 1202 facial-recognition restriction); NYC (LL 144); Colorado (SB 24-205); the catch-all US federal row.

For Hiring-C, the table is smaller: the state's civil-rights statute; the federal Title VII / EEOC frame; the state's unemployment-insurance program rules and any state-level algorithmic-accountability act. Cite the state's own statute rather than fabricating one — if you do not know the specifics for the state you're picking, choose a state whose framework is documented (California, Colorado, Illinois, New York State) or mark `<!-- needs-research: verify state-specific overlay -->`.

### Section 6 — the nine-step analyst pass

Walk the nine-step disparate-impact pass from chapter 04 for the chosen system:

1. Identify protected attributes covered.
2. Confirm the analysis dataset.
3. Compute selection rates and impact ratios per category and intersection — the ML team owns the computation; you *specify* what needs to be computed.
4. Flag any impact ratio below 0.80.
5. Check sample sizes.
6. Check calibration and precision per group.
7. Verify candidate notification.
8. Verify the annual LL 144 audit (if applicable).
9. File the register entries with the overlays anchored.

For each step, one to three sentences on what the analyst does for this specific system. Do not skip any step; if a step is not applicable, say so and cite the reason.

### Section 7 — boundary / handoff note

A short (5–10 sentence) note that lists what the analyst *does not do* on this intake, and where each item lands:

- Disparate-impact analysis itself → ML team.
- Business-necessity legal argument → Legal.
- Less-discriminatory-alternative analysis → joint ML + Legal.
- LL 144 audit → independent auditor.
- Fairness-audit methodology depth → [ai-risk-engineer](https://github.com/ml-engineering-curriculum/ai-risk-engineer-learning).

## Requirements — cross-cutting

- **The chosen use case is walked all the way through.** No `TBD` sections. Where a fact cannot be resolved without another team, write `pending — routed to X, due Y` with a plausible SLA.
- **Every statutory reference cites the primary instrument.** EEOC guidelines to `eeoc.gov`; LL 144 to `nyc.gov/dca`; EU AI Act to `eur-lex.europa.eu`. No blog-post citations, no vendor-summary citations.
- **The four-fifths rule is described in the language of the Uniform Guidelines** (the ratio, the 0.80 threshold, the presumptive evidence of adverse impact, the business-necessity burden shift). Do not simplify to "if the ratio is below 0.80, the system is unlawful" — that is not what the Guidelines say.
- **The LL 144 checklist produces a verdict for each of the four obligations**, with an ask for any gap. No obligation is silently skipped.
- **The EU AI Act section is present even if the answer is N/A.** The analyst-tier discipline is to state N/A explicitly with the reason; silent omission is a fail.
- **The jurisdictional overlay table has one row per jurisdiction the system serves.** No collapsing of 20 US states into "US". If the row is the same for multiple states because Title VII is the anchor, use a single row and enumerate the states in the cell — the row is per-obligation, not per-jurisdiction-name, but the enumeration must be present.
- **Uncertain statutory claims are marked `<!-- needs-research: -->`.** California algorithmic-accountability legislation is the classic trap; do not assert a specific enacted statute without verifying.
- **No fabricated vendor names, audit URLs, or auditor identities.** If you use a real vendor's public LL 144 audit summary, cite it; if not, use a fabricated name clearly marked as such (e.g., `VendorH — fabricated for the exercise`).

## Starter guidance

- Pick Hiring-A if you want the maximum-breadth overlay (four US-state / local rules plus three EU member states plus UK). Pick Hiring-B if you want the deepest engagement with the Illinois AI Video Interview Act and the LL 144 audit specifics. Pick Hiring-C if you want to practise the public-sector overlay pattern (state civil-rights statute; unemployment-insurance program rules; state-level algorithmic-accountability acts).
- Chapter 04's mapping is the scaffold. Do not try to write Section 5 from memory; open the chapter, extract the overlay table shape, and adapt.
- On the EEOC 2023 AI guidance: the two key claims are that (a) the four-fifths rule applies to AI selection tools and (b) the employer using the tool is responsible for the disparate-impact assessment, not the vendor. Both claims should appear in Section 2, cited to the guidance URL.
- On LL 144 audit-scope specifics: the DCA implementation rules have been updated multiple times. The chapter carries a `<!-- needs-research -->` marker on this exact point; carry the same marker forward in your deliverable rather than asserting an outdated rule.
- On the jurisdictional overlay table, the trap is over-claiming. If you are not sure whether Colorado SB 24-205 has phased in for the effective date of the enterprise's deployment, mark it as `<!-- needs-research: verify SB 24-205 effective date and phase-in schedule -->` rather than asserting. The Colorado law's phase-in was staged; do not fabricate a specific date.
- On the nine-step analyst pass, resist the urge to skip. Every step is written down even where the answer is short — the discipline of the pass is that it forces the analyst to consider each anchor. Missing one step in the field is how a hiring-AI risk assessment leaves the LL 144 audit off the record.
- On the boundary / handoff note, the analyst does not run the disparate-impact assessment, does not argue business necessity, does not conduct the LL 144 audit. Naming what you do not do is as important as naming what you do — the overlay is the analyst's artefact; the analysis, the argument, and the audit are somebody else's.

## Acceptance criteria

- `mod-104-ex-04-hiring-overlay.md` with the seven sections above, in order, for the chosen hiring-AI system.
- Every LL 144 obligation carries a verdict (satisfied / partially satisfied / gap / not applicable) and, for gaps, a routed ask.
- EU AI Act section is present with an explicit applicability verdict — high-risk under Annex III item 4 (for Hiring-A) or explicit N/A with reason (for Hiring-B and Hiring-C).
- Jurisdictional overlay table has one row per jurisdiction the system serves, each cited to a primary instrument.
- Nine-step disparate-impact analyst pass walked in full; each step produces a specific-to-this-system output.
- Boundary / handoff note names the five handoffs listed above.
- Every statutory citation is to a primary instrument; every uncertain claim marked `<!-- needs-research: -->`.
- No fabricated vendor names, audit URLs, or auditor identities without the fabrication marker.

## Stretch goals

- **A candidate-notification draft.** Write the actual candidate-notification text for the chosen system, meeting the LL 144 requirements (tool identified; job qualifications and characteristics assessed; accommodation / alternative process). Keep it plain-language; a candidate should be able to read it in under two minutes.
- **A model-card excerpt.** Write a short (300-word) model-card excerpt for the chosen system covering the sections a hiring-AI model card must have per the EU AI Act Article 13 / Annex IV framing. Preview work for `mod-105`.
- **A vendor-audit review letter.** Write a letter to the vendor's LL 144 auditor asking three specific questions about the audit methodology (sample size floor; intersectional categories covered; auditor independence evidence). This is preview work for `mod-107`.
- **A jurisdictional monitoring alert.** Sketch what your enterprise's regulatory-tracking system needs to flag for this use case in the next 12 months (California algorithmic-accountability bills; NYC LL 144 rule updates; EU AI Act phase-in dates; any new state AI-in-employment law). Preview work for `mod-106`.
- **A council-facing overlay one-pager.** Compress the seven-section overlay into a single-page memo for the AI governance council. The point of the compression is deciding what the council actually needs to see.

## Deliverables

- `mod-104-ex-04-hiring-overlay.md` — the seven-section hiring overlay.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works Hiring-A (ResuméRank) as the reference. A strong deliverable against Hiring-B or Hiring-C is not penalised — the point is that the analyst can hold the overlay pattern across whichever hiring-AI system lands at intake. The commonest failure modes are (a) reducing the four-fifths rule to a legality determination rather than a burden-shift trigger; (b) leaving the EU AI Act section silent when the system does not deploy in the EU rather than writing an explicit N/A; (c) fabricating a specific California statute or Colorado effective date rather than marking uncertainty; (d) forgetting that the analyst *specifies* what the disparate-impact assessment must cover but does not *run* it. A cleanly-argued overlay on Hiring-C (the smallest jurisdictional footprint) beats a sprawling overlay on Hiring-A that misses the boundary between what the analyst does and what the analyst asks the ML team to do.
