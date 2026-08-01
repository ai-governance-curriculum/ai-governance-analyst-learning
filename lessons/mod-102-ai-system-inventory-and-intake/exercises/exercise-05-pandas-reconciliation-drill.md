# Exercise 05 — Pandas Reconciliation Drill

**Estimated effort:** 2 hours
**Grounding chapter:** [05 — Reconciling the Model Registry Against the Governance Inventory — pandas / Excel](../05-pandas-and-excel-reconciliation.md)

## Objective

Build the analyst's most common data-hygiene reflex: given a model-registry export and a governance-inventory export, produce the three-set diff, filter for material-change signals, and file the weekly reconciliation as a governance-record row with concrete follow-up actions. The goal is not to become a data engineer; the goal is to be *comfortable* enough with pandas or Excel that reconciliation-day does not scare you.

You should finish this exercise able to open two CSVs a hiring manager hands you, produce the three-set diff and a signed-off reconciliation memo, and open the right follow-up tickets in under an hour.

## Prerequisites

- Chapter 05 read; exercise-03 completed (you need an inventory schema you know cold).
- Python 3.10+ with [pandas](https://pandas.pydata.org/docs/) installed (or a JupyterLab / Google Colab environment). If pandas is genuinely off-limits, Excel is acceptable — see the Excel path below.
- A notebook environment: Jupyter, Colab, VS Code with the Python extension, or a `.py` file if you prefer scripts.
- The [pandas merge / join / concatenate guide](https://pandas.pydata.org/docs/user_guide/merging.html) bookmarked.

## Problem statement

You will be given (or you will construct) two CSV exports that mimic a real registry-inventory reconciliation. Then you will run the reconciliation, produce the three-set output, filter for material-change drift, and file the weekly reconciliation record. The exercise has three parts.

### Part A — construct the sample data

If you do not have real exports to work from (the usual case at learner tier), construct two CSVs of ~15–20 systems each with deliberate discrepancies. Use this shape:

`model_registry_export.csv` columns:

- `system_id` (some rows blank, to simulate ML-team-side gaps)
- `name`
- `version`
- `provider`
- `technical_owner`
- `training_data_sources`
- `deployed_date`
- `status` (`live` / `retired`)

`governance_inventory_export.csv` columns (using the schema from exercise-03):

- `system_id`
- `name`
- `last_reviewed_version`
- `provider`
- `technical_owner`
- `training_data_sources`
- `business_owner`
- `enterprise_tier` (`Critical` / `High` / `Medium` / `Low`)
- `eu_ai_act_tier` (`Unacceptable` / `High-risk` / `Limited-risk` / `Minimal`)
- `status` (`proposed` / `in-development` / `in-production` / `retired`)
- `last_reviewed_date`

Seed the two files with:

- **At least three "registry-only" rows** (shadow AI — models in the registry with no inventory row). Include one where the `system_id` is blank and the reconciliation has to fall back to the composite key.
- **At least two "inventory-only" rows** — one legitimately retired, one stale-and-suspicious.
- **At least four "in both, material-change drift" rows** — one with a version bump, one with a provider swap, one with a technical-owner change, one with a new training-data-source added.
- **At least four "in both, no drift" rows** — the boring healthy majority.
- **At least two "normalisation trap" rows** where the same system appears in both files but with different casing / punctuation on the name and no system_id — so the composite-key fallback has to normalise before matching.

Commit both CSVs to the workspace. They are part of the deliverable.

### Part B — run the reconciliation in pandas

Author a Jupyter notebook (`reconciliation.ipynb`) or a script (`reconciliation.py`) that:

1. Loads both CSVs.
2. Normalises the identity key — system_id first, composite normalised-name fallback second.
3. Computes the three sets: `registry_only`, `inventory_only`, `both`.
4. Inside `both`, filters for material-change drift on the fields in the chapter 05 code sample (version, provider, technical_owner, training_data_sources).
5. Sorts material-change drift by enterprise tier so Critical / High rows are at the top of the report.
6. Prints (or displays) each of the four resulting DataFrames with clear section headers.
7. Writes each of the four DataFrames back out as CSV (`registry_only.csv`, `inventory_only.csv`, `both_no_drift.csv`, `material_change_drift.csv`).

### Part C — write the reconciliation record row

Author `reconciliation-record.md` — the governance-record row for the week. Use the structure from chapter 05:

- **Reconciliation date and analyst.**
- **Registry-only count and list**, with a gap-ticket ID per row and the technical-owner-to-email.
- **Inventory-only count and list**, with a disposition per row (verified retired / open for follow-up).
- **Material-change count and list**, ordered by tier, with the re-review action per row.
- **Assumptions** — normalisation choices you made when the identity key was ambiguous.
- **Turnaround SLA** on the gap tickets — stated commitment.
- **Attach**: the four output CSVs from Part B and the two input CSVs from Part A.

Then produce three sample follow-up drafts:

1. **A gap-ticket description** for one of the registry-only rows (Jira-ready or ServiceNow-ready).
2. **A follow-up email** to the technical owner of a registry-only shadow-AI system, asking them to run intake retrospectively, with the SLA and the link to the intake form.
3. **A re-review request** for one of the material-change drift rows — a short paragraph in the governance-record register naming the material-change criterion satisfied (per chapter 03's list) and the required re-assessment scope.

## Requirements

- **The two input CSVs are present in the deliverable** and match the discrepancy shape described in Part A. Reviewers should be able to open them and see the seeded gaps and drift.
- **The notebook / script runs end-to-end.** A reviewer can clone the workspace, run `jupyter nbconvert --to notebook --execute reconciliation.ipynb` or `python reconciliation.py` and get the four output CSVs and the printed report.
- **The composite-key fallback is exercised.** The seeded normalisation-trap rows must correctly reconcile — if the composite key silently misses them, the exercise is not passing.
- **Material-change filtering uses the chapter 03 criteria.** Version change, provider change, technical-owner change, data-source change — each fires the drift filter. Add a comment in the code linking to the chapter 03 material-change list.
- **The reconciliation record row is audit-facing.** It reads like a governance artefact, not a debug log. Named columns, cited assumptions, per-row dispositions, stated SLAs.
- **No fabricated ticket IDs presented as real** — the exercise's ticket IDs are placeholders (`GAP-2026-001`, `RR-2026-0044`) and the memo says so.
- **A short reflection note** at the end of the memo (5–10 sentences): what surprised you in the reconciliation, which normalisation choices you would want a peer to sanity-check, and one weakness of this reconciliation shape that would bite at scale (100+ systems, cross-registry federation, multi-jurisdiction inventories, etc.).

## Starter guidance

- Copy the chapter 05 code sample as a starting point. Adapt the column names to match your CSVs; do not adapt the shape.
- The composite-key normalisation function in chapter 05 (`str.lower().str.strip().str.replace(r"\s+", "_", regex=True)`) is the right starting point but does not handle everything — punctuation, accents, abbreviations. Where you add normalisation, cite in a comment why.
- For the `training_data_sources` material-change filter, the chapter warns that pure string inequality fires spuriously on punctuation. Consider normalising or tokenising both sides before comparing, and mark this drift as a *soft* signal — flagged, but not automatically re-review-firing.
- If you use Excel instead of pandas, the Excel walk in chapter 05 is the reference. The three-set diff is `COUNTIF`-based; the material-change filter is `XLOOKUP` per column; the output is four sheets rather than four CSVs. Everything else — the reconciliation record row, the follow-up drafts — is identical.
- On the follow-up email, aim for the tone chapter 05 mentions: "the requester should never feel abandoned". The email is asking for retrospective intake, not scolding.

## Acceptance criteria

- `model_registry_export.csv` and `governance_inventory_export.csv` committed; each with 15–20 rows and the seeded gaps / drift described in Part A.
- `reconciliation.ipynb` or `reconciliation.py` runs end-to-end and produces the four output CSVs.
- The composite-key fallback correctly reconciles the seeded normalisation-trap rows.
- `reconciliation-record.md` present, structured per chapter 05, with the three follow-up drafts included as appendices or inline.
- Every uncertain claim marked `<!-- needs-research: -->`; every placeholder ID clearly flagged as a placeholder.
- Reflection note of 5–10 sentences at the end of the memo.

## Stretch goals

- **A cross-jurisdiction filter.** Extend the material-change filter with the chapter 05 high-severity findings: EU personal data + missing DPIA; Annex III + missing FRIA; EU AI Act high-risk + missing EU database registration. Add columns to the inventory CSV so you can compute each finding, and print a "high-severity" section in the report ordered above everything else.
- **A repeatable reconciliation harness.** Wrap the notebook logic in a small CLI (`python reconcile.py --registry X.csv --inventory Y.csv --out out/`) with a `--dry-run` flag. Have a peer run it against their own CSVs.
- **A soft-vs-hard drift classification.** Extend the drift filter to distinguish "hard" signals (version change, provider change) from "soft" signals (training-data-source string diff, technical-owner-name typo). Hard signals fire re-review automatically; soft signals get a "confirm with owner" note.
- **An assumption audit.** Take the assumptions section of your reconciliation record and rewrite it as a checklist a peer could apply to future reconciliations. Publish it as `reconciliation-assumptions-checklist.md`.
- **A GRC-platform equivalent.** Sketch how the same reconciliation would work inside ModelOp or ServiceNow AI Control Tower — where the pandas step becomes a platform-native query, and where the analyst still has to file a governance record by hand. Reference back to exercise-04's platform tour.

## Deliverables

- `mod-102-ex-05/model_registry_export.csv` — the seeded registry CSV.
- `mod-102-ex-05/governance_inventory_export.csv` — the seeded inventory CSV.
- `mod-102-ex-05/reconciliation.ipynb` (or `.py`) — the working notebook or script.
- `mod-102-ex-05/output/registry_only.csv`, `inventory_only.csv`, `both_no_drift.csv`, `material_change_drift.csv` — the four output CSVs from the reconciliation run.
- `mod-102-ex-05/reconciliation-record.md` — the governance-record row for the week, with the three follow-up drafts.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The reference solution in the paired solutions repo constructs a specific 20-row example, runs the pandas reconciliation, and produces a reconciliation record. Your CSVs and your record will differ; what should not differ is that the reconciliation runs end-to-end, the composite-key fallback works, the material-change filter cites the chapter 03 criteria, and the record reads like a governance artefact rather than a debug log. If a hiring manager could hand you their real exports next week and get an equivalent memo back within an hour, the exercise is complete.
