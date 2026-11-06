# Lab 01 — One Fixed Bias Report, Walked Through All Four Chapters

**Duration:** 2 hours.
**Grounding chapters:** [01](../01-fairness-metric-glossary-and-limits.md), [02](../02-reading-fairlearn-and-aif360-reports.md), [03](../03-what-if-tool-code-free-exploration.md), [04](../04-hiring-ai-overlays-ll144-eeoc.md).
**Difficulty:** Core — threads all four chapters through a single artefact.

## Objective

Take **one** pre-written Fairlearn-style bias report on **one** fixed hiring-AI system and walk it end-to-end through each chapter's mechanics: metric-glossary identification (ch 01) → five-thing reading pass with coverage-gap call-outs (ch 02) → WIT follow-up plan (ch 03) → hiring-AI overlay attachments including the LL 144 checklist (ch 04). Produce a single `bias-review-walk.md` artefact that reads like a first-draft analyst trace from the metric table to the remediation ticket and non-technical summary.

The module's exercises each exercise *one* chapter's mechanics on an open-ended input: exercise 01 asks you to author the metric glossary from the chapters; exercise 02 asks you to train a classifier and generate the Fairlearn report yourself; exercise 03 runs a 45-minute WIT walk; exercise 04 produces the full seven-section hiring overlay. This lab is the inverted shape — *one* bias report, *four* chapters chained — so the analyst feels every anchor fire on the same row without the thread drifting between stages. It is the integration muscle an analyst actually uses when a reviewer asks "walk me through this one system's bias review end-to-end."

## Prerequisites

- All four chapters read.
- Exercises 01 and 02 completed, or at minimum read, so the metric vocabulary and the five-thing reading pass are not being learned here.
- A markdown editor. No Python or notebook environment required — the bias report is pre-written.

## The fixed input

Use *exactly* this bias report on *exactly* this system — do not substitute. A fixed input lets you compare your walk to the chapter-anchored expected shape in the checkpoint section. All numbers below are marked `pedagogic example — numbers illustrative` to match the exercise-01 discipline; do not treat them as a real audit output.

> **System.** ResuméRank Screener (RRS-2027-01), third-party SaaS vendor Hiring-AI Inc. (vendor name fabricated for the lab). Deployer: a Fortune-500 enterprise hiring in New York City, Illinois, Colorado, California, 20 other US states, Ireland, Germany, France, and the UK.
>
> **Automation.** Advisory — recruiters review the ranked list and advance candidates manually.
>
> **Use case.** Automated résumé scoring against a job description; returns a ranked list of candidates for a recruiter to review.
>
> **Evaluation dataset.** 10,300 historical résumés from the enterprise's 2024–2025 applicant pool; labelled by downstream hire outcome (positive class = "advanced past screen").
>
> **Primary fairness metric adopted by the enterprise.** Equal opportunity (equalised-odds relaxation on true positive rate) — recorded in the register as the metric the enterprise optimises for, with the trade-off that unequal precision and unequal selection rates may persist.
>
> **Fairlearn report (vendor-generated), pedagogic example — numbers illustrative.**
>
> | Group | N | Selection rate | TPR | FPR | Precision | Calibration slope |
> |---|---|---|---|---|---|---|
> | Male | 5,200 | 0.42 | 0.78 | 0.14 | 0.68 | 1.02 |
> | Female | 4,100 | 0.33 | 0.64 | 0.12 | 0.69 | 0.97 |
> | Non-binary | 410 | 0.26 | 0.52 | 0.17 | 0.54 | 0.79 |
> | Undisclosed | 590 | 0.30 | — | — | — | — |
>
> **Disparity metrics as reported.**
>
> - Selection-rate ratio (min / max across disclosed groups) = 0.26 / 0.42 = 0.62. Vendor flags: *below 0.80 four-fifths threshold*.
> - True-positive-rate ratio (min / max) = 0.52 / 0.78 = 0.67.
> - Calibration slope for the non-binary group = 0.79 (deviation from 1.0 greater than for the other two disclosed groups).
>
> **What the report also contains.** A single-attribute breakdown by sex; a vendor-signed narrative audit letter asserting "no material disparities beyond those documented"; a statement that the auditor is Hiring-AI Inc.'s in-house compliance team.
>
> **What the report does not contain.** Breakdown by race/ethnicity; intersectional breakdown (sex × race, sex × age); base rates (underlying positive rate per group in the labelled set); confidence intervals on the per-group metrics; a per-group confusion matrix; fairness on an out-of-time hold-out; any threshold-sensitivity sweep.

Treat the report as given. The lab starts from this report; do not re-author it. If the walk surfaces a correction, annotate the correction — do not silently rewrite the numbers.

## Steps

### Step 1 — Scaffold the artefact (10 min)

Create the working folder and file.

```bash
mkdir -p ~/aicg-labs/mod-104-lab-01
cd ~/aicg-labs/mod-104-lab-01
touch bias-review-walk.md
```

Open `bias-review-walk.md` and lay in the section headers up front:

```markdown
# Bias-review walk — RRS-2027-01 ResuméRank Screener

## 1. Metric-glossary slice (chapter 01) — what the report is measuring and what it cannot tell us
## 2. Five-thing reading pass (chapter 02) — the pass against the vendor report
## 3. WIT follow-up plan (chapter 03) — what a 45-minute WIT walk would add
## 4. Hiring overlay — Title VII / EEOC / LL 144 / EU AI Act (chapter 04)
## 5. Remediation-ticket draft and the five-question non-technical summary
```

Add a one-line `Analyst / date:` entry at the top so the artefact is time-stamped.

The scaffolded order matters: chapter 01's metric vocabulary first, then chapter 02's reading pass, then chapter 03's WIT follow-up, then chapter 04's statutory overlay, with the remediation ticket and the stakeholder translation last. Walking out of order is where real analysts drift — follow the scaffold.

### Step 2 — Fill section 1: metric-glossary slice (20 min)

Open chapter 01 in a second window. For *each* metric visible in the Fairlearn table, write one row with three fields:

- **Metric name** (as the chapter names it).
- **Plain-English definition** — two sentences a non-technical stakeholder can read and repeat back.
- **What this metric cannot tell us about *this* system** — the load-bearing field. Name one other fairness property the metric can silently violate for this report shape.

Cover at minimum: selection rate / demographic parity; true positive rate (and the equal-opportunity framing the enterprise has adopted); false positive rate; precision; calibration slope; the selection-rate ratio against the four-fifths threshold.

Close the section with a two- to three-sentence **impossibility-result note**: name the trio from chapter 01 that cannot simultaneously hold (calibration within groups; equal FPR across groups; equal FNR across groups), and state what the enterprise's equal-opportunity choice implicitly concedes (unequal selection rates may persist; unequal precision may persist). This mirrors chapter 01's "Metric-choice implications the analyst records" discipline.

Two tripwires to watch:

- **Do not re-derive the maths.** The section is a *glossary slice*, not a proof. One line of plain-English per metric is enough; the chapter 01 definitions are the reference.
- **The "cannot tell us" column is load-bearing.** If any row's "cannot tell us" is empty, re-read chapter 01's row for that metric — every metric has at least one property it can silently violate.

### Step 3 — Fill section 2: run the five-thing reading pass (25 min)

Open chapter 02 in a second window. Author section 2 in two parts.

**Part A — the five-thing pass.** For each of the five things in chapter 02's "What to look for first" list, write one row with three columns: *observation from the report*, *threshold / expected shape*, *verdict (clean / soft-flag / hard-flag / breach)*.

| Thing | Observation | Threshold / expected shape | Verdict |
|---|---|---|---|
| 1. Sample sizes per group | … | Groups with N < 100 are statistically unreliable (chapter 02). | … |
| 2. Selection-rate ratio | … | Below 0.80 → EEOC four-fifths breach; automatic remediation ticket. | … |
| 3. TPR / FPR differences | … | Substantial gaps → equalised-odds breach relative to the enterprise's adopted metric. | … |
| 4. Calibration slope per group | … | Slope materially different from 1.0 indicates miscalibration; consequential if the score is used downstream. | … |
| 5. Precision differences | … | Under-reported by most vendors; load-bearing when the cost of a false positive is high. | … |

For *this* report, the selection-rate ratio verdict should be **breach** (0.62 < 0.80). The TPR ratio verdict should be **hard-flag** (0.67 is a substantial gap relative to the enterprise's adopted equal-opportunity metric). The non-binary calibration slope at 0.79 should be **soft-flag at minimum** — the chapter 02 line is "materially different from 1.0." The non-binary N = 410 is above the chapter 02 N < 100 floor, but the undisclosed row has no TPR / FPR / precision at all — note it.

**Part B — coverage gaps against the four common omissions.** Chapter 02's four omissions list: base rates per group; confidence intervals; sub-group (intersectional) breakdown; fairness on an out-of-time hold-out. For each omission, name whether the report covers it, and if not, what the analyst-tier ask to the ML team or the vendor looks like. For *this* report, all four are omitted; none can be silently passed over.

Close section 2 with a one-line **auditor-independence note**: the audit letter states the auditor is Hiring-AI Inc.'s in-house compliance team. Chapter 02's LL 144 specifics and chapter 04's LL 144 obligations both name *independence from the tool's developer and user* as a requirement. The in-house compliance team of the vendor is not independent of the vendor developer. Flag this — it is the single most important finding on the report as presented, and the aggregate-metric reading can mislead the stakeholder if the independence problem is not called out up front.

### Step 4 — Fill section 3: author the WIT follow-up plan (20 min)

Open chapter 03 in a second window. Section 3 does *not* require a live WIT session — the point is to name what a 45-minute WIT walk would add to the aggregate report the vendor already handed over. Author it as five bullets, one per section of chapter 03's 45-minute walk sequence that is *additive* to the aggregate report the lab already has in hand.

- **Per-group confusion matrices in WIT.** Chapter 01 names the per-group confusion matrix as the base artefact. The vendor's report omits it. A WIT session would surface the matrices directly; note the ask.
- **ROC / precision-recall curves per group.** Overlapping curves would soften the equalised-odds finding; separated curves would sharpen it. The aggregate report cannot answer that question.
- **Counterfactuals.** Sample five to ten datapoints per group; note what feature would flip the prediction. Flag any nearest-counterfactual flipping feature that is a plausible proxy for a protected attribute (the chapter 03 proxy-variable list: ZIP / postcode, educational institution, employment-gap length, employer name, language spoken). The chapter 03 rule applies: a proxy-flipping counterfactual is a *finding routed to the ML team*, not a determination.
- **Partial-dependence plots.** Especially for features chapter 03 names as classic proxies. Does the model lean heavily on educational institution — a plausible proxy for race or socio-economic background in a résumé-triage setting?
- **Threshold sweep.** The vendor's report contains no threshold-sensitivity sweep. A WIT session would walk the enterprise's chosen threshold ±0.05 and ±0.10 and name whether the profile is fragile (a small move changes the verdict). The chapter 03 rule applies: a profile that flips its disparate-impact-ratio verdict on a 0.05 threshold move is *fragile*; the analyst records that.

Close section 3 with a one-sentence verdict: *WIT session recommended before the remediation ticket closes*, with the ML-team owner named (fabricate a plausible name if you must; mark fabricated names in a Fabrication note at the bottom of the file).

### Step 5 — Fill section 4: attach the hiring overlay (25 min)

Open chapter 04 in a second window. Section 4 is the overlay pack as a per-system slice — not the full seven-section exercise-04 shape, but every sub-section the chapter requires for *this* system.

**4.1 Title VII framing.**

- *Disparate treatment* — is there evidence a protected attribute is used as a direct input? The vendor report does not evidence a protected attribute as an input feature, but the report also does not evidence the *absence* of such an input. Note the ask.
- *Disparate impact* — the four-fifths ratio of 0.62 is below 0.80. Chapter 04's framing: this is *presumptive evidence of adverse impact* and triggers the business-necessity analysis under the EEOC Uniform Guidelines. Do not restate it as "the tool is unlawful" — that is chapter 01's and chapter 04's shared discipline.

**4.2 EEOC 2023 AI-adverse-impact guidance.** Cite the two load-bearing claims the chapter names: the four-fifths rule applies to AI selection procedures (vendor claims to the contrary are wrong), and the *employer* — not the vendor — is responsible for the disparate-impact assessment. For *this* system, the enterprise is the employer; the register entry should name the enterprise as the responsible party and the vendor's audit as evidence, not as a substitute for the employer's analysis.

**4.3 NYC LL 144 obligations checklist.** The enterprise hires for NYC-based roles, so LL 144 applies. For each of the four obligations from chapter 04, produce a verdict (satisfied / partially satisfied / gap / not applicable) and, for any gap, the ask.

| Obligation | Verdict | Ask (if gap) |
|---|---|---|
| Annual independent bias audit | … | … |
| Publicly posted audit summary | … | … |
| Candidate notification ≥ 10 business days before use, with the required content | … | … |
| Published data-protection information (categories collected; retention period if applicable) | … | … |

The auditor-independence note from section 2 feeds the first row — the audit is almost certainly a **gap**, because the vendor's in-house compliance team is not independent of the vendor developer. The other three obligations the lab does not have direct evidence on; mark them `pending — evidence request routed to Talent / Legal, due <date>` rather than guessing.

**4.4 EU AI Act Annex III attachment.** The enterprise hires in Ireland, Germany, and France — so EU deployment is in scope. Tier the tool as Annex III item 4 (high-risk — recruitment and selection of natural persons). Name the three deployer obligations the chapter names:

- Article 26 — human oversight, monitoring, log-keeping, cooperation with authorities. Owner routing: `mod-109`.
- Article 27 — Fundamental Rights Impact Assessment before first deployment. Owner routing: `mod-105`.
- Article 50 — the candidate is informed they are interacting with an AI system. Owner routing: `mod-110`.

For each, name whether the artefact exists or is `pending — evidence request routed to <owner>, due <date>`.

**4.5 Other US state and local overlays — one-liner per jurisdiction in scope.** Chapter 04's list for a US-plus-EU hiring tool. For *this* system:

- **Illinois** — AI Video Interview Act. One-liner: does not apply — no video interviews in this tool. Confirm by naming the tool's input (résumé text + structured features).
- **Colorado** — SB 24-205 (consequential-decision-tool obligations). One-liner: applies to Colorado-based roles once phased in; mark effective-date verification as `<!-- needs-research: verify SB 24-205 effective date and phase-in schedule -->` rather than asserting.
- **California** — algorithmic-accountability successor to AB 2930. One-liner with the chapter's `<!-- needs-research: -->` marker carried forward verbatim; do not fabricate an enacted statute.
- **Catch-all 20 US states** — Title VII / EEOC Uniform Guidelines apply federally.
- **UK** — Equality Act 2010 analogous framing.

### Step 6 — Fill section 5: remediation ticket and non-technical summary (15 min)

Open chapter 02 in the second window; section 5 is the chapter 02 remediation-ticket shape plus the chapter 02 five-question summary.

**5.1 Remediation-ticket draft.** One ticket, not a project charter. The chapter 02 shape: concrete finding, threshold breached, proposed follow-up scope, and the explicit boundary that the *methodology* belongs to `ai-risk-engineer` and the *legal determination* belongs to Legal. For *this* system, the headline finding is the four-fifths breach (0.62 < 0.80) layered over the independent-auditor gap under LL 144 — write the ticket with both. Name a fabricated ML-team lead as owner and flag the fabrication.

**5.2 Five-question non-technical summary.** The chapter 02 five questions, one to two sentences per question — no metric names, no thresholds, plain English.

- Was a fairness audit done (and when)?
- What is the bottom line per group?
- What are we doing about any breaches?
- What could the audit have missed?
- When is the next audit?

If the finance director cannot skim it and know what to do, rewrite. Chapter 02's discipline: no metric names, no thresholds in this sub-section — the stakeholder does not want "the four-fifths ratio is 0.62"; they want "the tool advances one protected group materially less than the other."

### Step 7 — Cross-check the five sections (10 min)

Walk the five sections side-by-side. Every value that appears on more than one section must be identical across all of them. High-tripwire fields:

- **The four-fifths ratio.** Section 1 (as a metric), section 2 (as a verdict against threshold), section 4 (as a Title VII trigger), and section 5 (as the plain-English headline). All four must point at the same number and the same verdict.
- **The equal-opportunity primary-metric choice.** Section 1 (as the chapter 01 metric-choice implications), section 2 (as the comparator for the TPR-ratio verdict), section 4 (consistent with the EEOC framing). Drift here is where the enterprise's governance decision gets lost.
- **The independent-auditor gap.** Section 2 (as the chapter 02 LL 144 auditor-independence note), section 4 (as the chapter 04 LL 144 obligation verdict), section 5 (named in the remediation ticket and the stakeholder summary). If any of the three drops the independence point, the register is already drifting.
- **Owner routing.** Section 3 (WIT follow-up owner), section 4 (overlay-ask owners for each obligation), section 5 (remediation-ticket owner). Each named owner — even fabricated — should appear in the Fabrication note if fabricated.

Any mismatch is a bug — fix it before the artefact is considered complete.

### Step 8 — Self-check (5 min)

Walk the artefact top-to-bottom and verify:

- Every statute, Article, Annex item, DCA rule, or EEOC guidance reference is sourced from the chapter it appears in or marked `<!-- needs-research: … -->`. Do not invent Article numbers, Annex items, or DCA rule-section numbers.
- No fabricated vendor audit URL, auditor identity, or incident citation. The vendor name is already fabricated and flagged; keep any owner / team names in the Fabrication note at the bottom of the file.
- The five-question non-technical summary in section 5.2 is genuinely non-technical — no metric names, no thresholds. If any snuck in, rewrite 5.2 only.
- The lab has one bias report walked all the way through; a second bias report has not crept in. That would be exercise 02 scope, not this lab.

## Expected output

One markdown file in `~/aicg-labs/mod-104-lab-01/`:

- `bias-review-walk.md` — five populated sections (plus optional Fabrication note), one timestamp, one named analyst.

Total length: roughly 1,500–2,500 words. A senior reviewer or governance lead should be able to read it in fifteen minutes and either accept the review as drafted or push back on specific fields.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did the four-fifths finding survive unchanged from section 2 into sections 4 and 5?** Chapter 01 and chapter 04 both frame the 0.62 ratio as *presumptive evidence of adverse impact* triggering the business-necessity analysis — *not* a legality determination. If section 5.1's remediation ticket or section 5.2's non-technical summary silently escalates the finding to "the tool is illegal," you have exceeded chapter 01's and chapter 04's boundary.
2. **Did you flag the independent-auditor gap at the top of section 2 and carry it into section 4 and section 5?** Chapter 02's LL 144 specifics and chapter 04's LL 144 obligations both name auditor independence as required. The vendor's in-house compliance team is not independent. If the finding appears only in section 4, the five-thing reading pass has silently accepted the vendor's narrative; revise.
3. **Did you keep WIT as a *follow-up plan*, not a performed session?** This lab is a reading drill; chapter 03's 45-minute walk is the scope of exercise 03. If section 3 reads as though you ran the session, scope-creep has set in — reframe as what the next step would add and which ML-team ask it unlocks.
4. **Did section 5.2 stay genuinely non-technical?** Chapter 02's discipline is that the five-question summary has no metric names and no thresholds. If any snuck back in, the stakeholder-facing translation is already broken.
5. **Did you respect the boundary — the analyst does not run the disparate-impact analysis, does not argue business necessity, does not conduct the LL 144 audit, does not design the bias-audit methodology?** Chapter 04's handoff list is the reference. If any section of the walk silently takes on one of those four handoffs, revise.

If any of the five is "no", revise *that section* before considering the lab done.

## Why this is a lab, not an exercise

Exercise 01 asks you to author a whole metric glossary across all five families with worked-disagreement scenarios. Exercise 02 asks you to train a classifier, generate your own Fairlearn report, and produce a bias-review note. Exercise 03 runs a 45-minute WIT session and produces a WIT note with a per-datapoint comparison memo. Exercise 04 produces a full seven-section hiring overlay on one of three fabricated hiring-AI systems.

This lab inverts the shape. It takes *one* bias report — pre-written and fixed — and chains all four chapters' mechanics against it on a single page, with cross-section consistency enforced. The failure mode an analyst actually has in review is not "cannot author a metric glossary" or "cannot generate a Fairlearn report" — it is "reads one bias report and the four-fifths finding, the equal-opportunity primary-metric choice, the independent-auditor gap, and the hiring-overlay routing each drift silently between the glossary, the reading pass, the WIT plan, and the stakeholder translation." This lab exercises the cross-section consistency that the module requires and the exercises — each anchored in one chapter at a time — do not directly test.
