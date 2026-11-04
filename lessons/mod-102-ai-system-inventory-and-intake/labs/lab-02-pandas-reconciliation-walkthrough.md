# Lab 02 — Pandas Reconciliation Walkthrough on a Fixed Dataset

**Duration:** 90 minutes.
**Grounding chapters:** [03](../03-inventory-row-and-registry-sync.md) (material-change definition), [05](../05-pandas-and-excel-reconciliation.md) (the pandas walk).
**Difficulty:** Core — guided code walkthrough with a fixed dataset.

## Objective

Run the chapter 05 pandas reconciliation code against a **fixed, pre-seeded eight-row dataset**, read the three-set output, apply the chapter 03 material-change criteria, and produce the one-paragraph reconciliation record row the chapter asks for. The point is to feel the pandas commands land and to read their output critically — not to design your own test cases.

Exercise 05 asks you to *construct* a 15–20 row dataset with the discrepancy shape you want, run the pandas reconciliation end-to-end, and author a full reconciliation memo with three sample follow-up drafts. This lab is the complementary shape: a fixed, smaller dataset that walks you through the pandas steps line-by-line, so you internalise the shape of the code before you design your own cases in the exercise.

## Prerequisites

- Chapters 03 and 05 read.
- Python 3.10+ with [pandas](https://pandas.pydata.org/docs/) installed. Alternative: open a Google Colab or Kaggle notebook so pandas is pre-installed.
- A notebook environment: Jupyter, Colab, VS Code with the Python extension, or a `.py` file if you prefer scripts.
- A terminal and a markdown editor.

## The dataset (fixed input)

Use *exactly* the two CSVs below — do not substitute. A fixed dataset lets the lab's expected output match what the chapter 05 code should produce.

### `model_registry_export.csv`

```
system_id,name,version,provider,technical_owner,training_data_sources,deployed_date,status
AI-2027-0029,ServiceLens,v1.2.0,VendorX,Alex Kim,"support_tickets_2024,support_tickets_2025",2027-04-01,live
AI-2027-0031,Marketing Copy Draft Assistant,v1.4.0,VendorV,Priya Nair,"product_briefs,prior_campaigns,launch_notes",2026-09-15,live
AI-2027-0033,Fraud Score Model,v2.1.0,internal,Dana Ortiz,"claims_2021_2024,sanctions_lists",2026-02-10,live
AI-2027-0040,Doc Classifier,v0.9.1,VendorY,Sam Lee,"vendor_contracts_corpus",2027-06-20,live
,Vector Search Experiment,v0.1.0,VendorZ,Jules Park,"internal_wiki_snapshot",2027-07-12,live
AI-2027-0045,candidate-screener,v0.3.0,VendorX,Robin Patel,"applicant_tracking_2022_2026",2027-08-01,live
AI-2027-0021,Support Chatbot,v3.0.0,VendorX,Sam Lee,"support_tickets_2024,support_tickets_2025,kb_articles",2025-11-15,live
AI-2027-0019,Churn Predictor,v1.0.3,internal,Dana Ortiz,"customer_events_2023_2025",2025-06-30,live
```

### `governance_inventory_export.csv`

```
system_id,name,last_reviewed_version,provider,technical_owner,training_data_sources,business_owner,enterprise_tier,eu_ai_act_tier,status,last_reviewed_date
AI-2027-0029,ServiceLens,v1.2.0,VendorX,Alex Kim,"support_tickets_2024,support_tickets_2025",Jordan Reeve,Medium,Limited-risk,in-production,2027-04-05
AI-2027-0031,Marketing Copy Draft Assistant,v1.3.2,VendorV,Priya Nair,"product_briefs,prior_campaigns",Priya Nair,Medium,Limited-risk,in-production,2026-11-02
AI-2027-0033,Fraud Score Model,v1.8.0,internal,Casey Wu,"claims_2021_2024,sanctions_lists",Dana Ortiz,High,High-risk,in-production,2026-02-15
AI-2027-0040,Doc Classifier,v0.9.1,VendorY,Sam Lee,"vendor_contracts_corpus",Chris Alvi,Low,Minimal,in-development,2027-06-25
,Vector-Search Experiment,v0.1.0,VendorZ,Jules Park,"internal_wiki_snapshot",Jules Park,Low,Minimal,in-development,2027-07-15
AI-2027-0038,Legacy Support Classifier,v2.9.0,VendorX,Sam Lee,"support_tickets_2022_2024",Jordan Reeve,Low,Minimal,retired,2026-12-01
AI-2027-0021,Support Chatbot,v3.0.0,VendorX,Sam Lee,"support_tickets_2024,support_tickets_2025,kb_articles",Jordan Reeve,Medium,Limited-risk,in-production,2026-02-10
```

The dataset is deliberately small (8 registry rows, 7 inventory rows) so you can hand-verify each of the three sets against the expected shape in the checkpoint section.

## Steps

### Step 1 — Set up the workspace (5 min)

```bash
mkdir -p ~/aicg-labs/mod-102-lab-02
cd ~/aicg-labs/mod-102-lab-02
touch model_registry_export.csv governance_inventory_export.csv reconciliation.py reconciliation-record.md
```

Paste the registry CSV above into `model_registry_export.csv` and the inventory CSV into `governance_inventory_export.csv`. Confirm from a terminal:

```bash
wc -l model_registry_export.csv governance_inventory_export.csv
```

Expect `9` lines on the registry (1 header + 8 rows) and `8` on the inventory (1 header + 7 rows).

### Step 2 — Load and normalise identity keys (15 min)

Open `reconciliation.py` and author the loader, following the chapter 05 code shape:

```python
import pandas as pd

registry = pd.read_csv("model_registry_export.csv")
inventory = pd.read_csv("governance_inventory_export.csv")

def norm(s):
    return s.str.lower().str.strip().str.replace(r"\s+", "_", regex=True)

registry["key"] = registry["system_id"].fillna(norm(registry["name"]))
inventory["key"] = inventory["system_id"].fillna(norm(inventory["name"]))
```

Now print the keys so you can eyeball the normalisation step:

```python
print("registry keys:", sorted(registry["key"].tolist()))
print("inventory keys:", sorted(inventory["key"].tolist()))
```

Run the script:

```bash
python reconciliation.py
```

**Expected shape of output.** Most rows should produce the `AI-2027-00NN` system IDs unchanged. The blank-system-ID rows should produce normalised-name keys — a trap: the registry's `Vector Search Experiment` normalises to `vector_search_experiment`, while the inventory's `Vector-Search Experiment` normalises to `vector-search_experiment` (hyphen left intact). The composite-key fallback as shipped by chapter 05 **does not** collapse the hyphen. You will handle that explicitly in step 3.

### Step 3 — Patch the normaliser for the hyphen trap (10 min)

Chapter 05 warns that the shipped normaliser handles whitespace and casing but not every punctuation case, and that where you *add* normalisation you add it with a comment citing why. Extend `norm` to also strip hyphens:

```python
def norm(s):
    # Chapter 05 shipped normaliser — lower + strip + collapse whitespace.
    # Extension: also collapse hyphens to underscores so
    # "Vector Search Experiment" and "Vector-Search Experiment" reconcile.
    return (
        s.str.lower()
        .str.strip()
        .str.replace(r"[\s\-]+", "_", regex=True)
    )
```

Re-run. The two experiment rows should now share the same key (`vector_search_experiment`). This is the chapter 05 "normalisation choices captured as assumptions" rule in practice — the choice gets recorded in the reconciliation-record row in step 7.

### Step 4 — Compute the three sets (15 min)

Append to `reconciliation.py`:

```python
registry_only = registry[~registry["key"].isin(inventory["key"])].copy()
inventory_only = inventory[~inventory["key"].isin(registry["key"])].copy()
both = registry.merge(inventory, on="key", how="inner", suffixes=("_reg", "_inv"))

print("\n=== Registry only ({} rows) ===".format(len(registry_only)))
print(registry_only[["key", "name", "technical_owner"]].to_string(index=False))

print("\n=== Inventory only ({} rows) ===".format(len(inventory_only)))
print(inventory_only[["key", "name", "status"]].to_string(index=False))

print("\n=== In both ({} rows) ===".format(len(both)))
print(both[["key", "name_reg"]].to_string(index=False))
```

Re-run. **Hand-check against the data before continuing.** You should see:

- **Registry-only:** 1 row — `AI-2027-0045 candidate-screener` (in the registry, no inventory row — shadow AI).
- **Inventory-only:** 1 row — `AI-2027-0038 Legacy Support Classifier` (retired in the inventory, pruned from the registry — the benign case).
- **In both:** 6 rows — `ServiceLens`, `Marketing Copy Draft Assistant`, `Fraud Score Model`, `Doc Classifier`, `vector_search_experiment`, `Support Chatbot`.

If the counts differ, your normaliser is not doing what you think — go back to step 3 and print `sorted(set(registry["key"]) ^ set(inventory["key"]))` to see the symmetric difference, then fix.

### Step 5 — Filter 'both' for material-change drift (20 min)

Append to `reconciliation.py` the material-change filter from the chapter 05 code sample:

```python
material_change = both[
    (both["version_reg"] != both["last_reviewed_version_inv"])
    | (both["provider_reg"] != both["provider_inv"])
    | (both["technical_owner_reg"] != both["technical_owner_inv"])
    | (both["training_data_sources_reg"] != both["training_data_sources_inv"])
].copy()

tier_order = {"Critical": 0, "High": 1, "Medium": 2, "Low": 3}
material_change["tier_rank"] = material_change["enterprise_tier_inv"].map(tier_order)
material_change = material_change.sort_values("tier_rank")

cols = [
    "key",
    "name_reg",
    "enterprise_tier_inv",
    "version_reg",
    "last_reviewed_version_inv",
    "provider_reg",
    "provider_inv",
    "technical_owner_reg",
    "technical_owner_inv",
    "training_data_sources_reg",
    "training_data_sources_inv",
]
print("\n=== Material-change drift ({} rows) ===".format(len(material_change)))
print(material_change[cols].to_string(index=False))
```

Re-run. **Hand-check.** You should see material-change drift on at least:

- `AI-2027-0031 Marketing Copy Draft Assistant` — version bumped from `v1.3.2` to `v1.4.0`; training-data-sources added `launch_notes`.
- `AI-2027-0033 Fraud Score Model` — version bumped from `v1.8.0` to `v2.1.0`; technical-owner changed from `Casey Wu` to `Dana Ortiz` (enterprise tier High — this row sorts to the top).

**Classify each material-change row** against chapter 03's material-change list by writing a comment in the script next to the output interpretation (or in your notebook's next markdown cell):

```markdown
- Marketing Copy Draft Assistant: version bump + training-data-source added ("launch_notes").
  - Fires under chapter 03 criterion "Change of training / grounding data sources".
  - Also potentially under "Change of user population" if launch_notes implies a new brand/segment — ask the ML owner.
- Fraud Score Model: version bump + technical-owner change.
  - Fires under chapter 03 criterion "Change of model family or model provider" only if the version bump reflects a model-provider or family change; otherwise soft.
  - Technical-owner change alone is not on the chapter 03 material-change list — note as a stewardship update, not an automatic re-review trigger.
```

Doc Classifier shows up in `both` with no drift — all four material-change fields match across registry and inventory. That is the healthy case and should **not** appear in the material-change DataFrame.

### Step 6 — Write the four output CSVs (5 min)

Append to `reconciliation.py`:

```python
registry_only.to_csv("registry_only.csv", index=False)
inventory_only.to_csv("inventory_only.csv", index=False)
both.drop(columns=["key"]).to_csv("both.csv", index=False)
material_change.drop(columns=["tier_rank"]).to_csv("material_change_drift.csv", index=False)
```

Re-run. Confirm the four CSVs appear:

```bash
ls -l *.csv
```

The four output CSVs are the immutable evidence attachments for the reconciliation record row chapter 05 requires.

### Step 7 — Write the reconciliation record (15 min)

Open `reconciliation-record.md` and author the governance-record row using the chapter 05 "What to report" structure:

```markdown
# Weekly reconciliation record — <YYYY-MM-DD>

**Analyst:** <your name>
**Dataset:** model_registry_export.csv (8 rows); governance_inventory_export.csv (7 rows).

## 1. Registry-only (1 row — shadow AI)

- `AI-2027-0045 candidate-screener` (v0.3.0, VendorX, owner Robin Patel) — in registry, no inventory row.
  Gap ticket: `GAP-2027-NNN` (placeholder). Routing: email Robin Patel asking for retrospective intake; SLA 5 business days. Flag: the system *name* ("candidate-screener") plus data-source ("applicant_tracking_2022_2026") suggest an EU AI Act Annex III item 4 (employment / recruitment) use case — expect a High-risk tier on intake, which raises the severity of the shadow-AI finding.

## 2. Inventory-only (1 row — verified retired)

- `AI-2027-0038 Legacy Support Classifier` (last reviewed v2.9.0, VendorX, retired 2026-12-01) — in inventory, pruned from registry. Disposition: **verified retired**. No action.

## 3. Material-change drift (2+ rows, ordered by tier)

- **`AI-2027-0033 Fraud Score Model` — High tier.** Version bump v1.8.0 → v2.1.0; technical-owner Casey Wu → Dana Ortiz. Criteria from chapter 03: version alone is not on the material-change list unless it reflects a provider / family / data-source change — ask the ML owner for the v1.8 → v2.1 diff notes. Technical-owner change is a stewardship update, not an automatic re-review trigger. Re-review ticket: open **only** if the diff notes confirm one of the chapter 03 criteria. Placeholder ticket `RR-2027-NNN`.
- **`AI-2027-0031 Marketing Copy Draft Assistant` — Medium tier.** Version v1.3.2 → v1.4.0; training-data-sources added `launch_notes`. Criterion from chapter 03 satisfied: *Change of training / grounding data sources*. Re-review fires. Placeholder ticket `RR-2027-NNN`.

## 4. In both, no drift (3 rows — the healthy majority)

- `AI-2027-0029 ServiceLens` — all four material-change fields match. No action.
- `AI-2027-0040 Doc Classifier` — all match. No action.
- `AI-2027-0021 Support Chatbot` — all match. No action.
- `vector_search_experiment` — reconciled via composite-key fallback after a punctuation-normalisation extension; no drift on the four material-change fields. No action but flag the normalisation choice in section 5.

## 5. Assumptions and normalisation choices

- Extended the chapter 05 normaliser to collapse hyphens (`[\s\-]+` → `_`) so the `Vector Search Experiment` / `Vector-Search Experiment` rows reconcile. If future records introduce further punctuation drift (apostrophes, periods), the normaliser needs a follow-up pass.
- Technical-owner change is not on the chapter 03 material-change list; treated as a stewardship update, not a re-review trigger.
- Version diffs for the Fraud Score Model (v1.8 → v2.1) and Marketing Copy Draft Assistant (v1.3.2 → v1.4.0) were not inspected for semantic content; the chapter 03 criteria citation assumes the version-diff notes confirm one of the listed criteria — a follow-up to the ML owner is the first action.

## 6. SLAs

- Shadow-AI retrospective intake: 5 business days.
- Material-change re-review (version + data-source bump on MCDA): 10 business days.
- Fraud Score Model stewardship-and-diff review: 5 business days (depends on the ML owner's diff-notes response).

## 7. Attachments

- `model_registry_export.csv`, `governance_inventory_export.csv` — the two inputs for the reconciliation date.
- `registry_only.csv`, `inventory_only.csv`, `both.csv`, `material_change_drift.csv` — the four outputs, immutable at the reconciliation date.
```

Fill the placeholders (`<YYYY-MM-DD>`, `<your name>`, the `NNN` ticket IDs) with your own values. Keep the `placeholder` language on the ticket IDs so a reviewer does not read them as real register entries.

### Step 8 — Self-check (5 min)

Walk the four output CSVs, the script, and the record row and verify:

- The counts match the chapter-anchored expected shape: 1 registry-only, 1 inventory-only, 2+ material-change drift, 3 (or 4 if you count the normalisation-trap row) with no drift. If the counts differ, step 3 or step 5 has a bug.
- Every material-change row in the record row cites a specific chapter 03 criterion by name — or explicitly flags that no criterion fires and the row is a soft signal only.
- The normalisation extension you added in step 3 is captured in section 5 of the record row — chapter 05's "normalisation choices captured as assumptions" rule.
- No fabricated ticket IDs presented as real register entries — the `GAP-2027-NNN` and `RR-2027-NNN` placeholders are flagged.
- The shadow-AI finding (`candidate-screener`) is called out with the name-plus-data-source signal that suggests a High-risk tier — chapter 05's "The findings are the point" rule.

## Expected output

In `~/aicg-labs/mod-102-lab-02/`:

- `model_registry_export.csv`, `governance_inventory_export.csv` — the two inputs, verbatim from the dataset block above.
- `reconciliation.py` — a working end-to-end script (load → normalise → three-set diff → material-change filter → write outputs).
- `registry_only.csv`, `inventory_only.csv`, `both.csv`, `material_change_drift.csv` — the four outputs.
- `reconciliation-record.md` — the seven-section governance-record row from step 7.

Total artefact set: ~120 lines of Python and ~70 lines of markdown. A governance-council reader should be able to get the shadow-AI finding and the two material-change re-reviews off section 1 and section 3 of the record row in under two minutes.

## Checkpoint

A self-review walk. Answer honestly:

1. **Did the hyphen-trap row reconcile?** The `Vector Search Experiment` registry row and the `Vector-Search Experiment` inventory row refer to the same system. If they appear on *both* `registry_only.csv` and `inventory_only.csv` instead of collapsing into `both.csv`, your normaliser is still broken — go back to step 3.
2. **Did you catch the shadow-AI severity signal?** `candidate-screener` with an `applicant_tracking_2022_2026` data source is almost certainly an employment / recruitment use case under EU AI Act Annex III item 4, which means the shadow-AI finding is not low-severity — it is a High-risk system running in production without a governance row. Chapter 05's "Cross-jurisdiction and privacy touchpoints" section is the anchor. If your record row treats the shadow-AI finding as a routine gap ticket, revise.
3. **Did you distinguish version bumps from material changes?** Chapter 03's material-change list names *Change of model family or model provider*, *Change of training / grounding data sources*, *Change of autonomy level*, *Change of deployment surface*, *Change of user population*, *Addition of a new tool / API in an agentic pipeline*, *Change of applicable jurisdictions*, *A material incident*. A version bump alone is not on that list — it is a *signal that one of those criteria may have fired*. If your record row fires an automatic re-review on the Fraud Score Model v1.8 → v2.1 without asking for the diff notes first, you are over-firing.
4. **Did you note technical-owner change as stewardship, not material change?** `technical_owner` appears in the chapter 05 code sample's material-change filter — but the chapter 03 material-change list does not include ownership changes. The right analyst move is to flag ownership drift as a stewardship update and route it to the ML owner / technical lead for confirmation, not to fire a full re-assessment.
5. **Does the inventory-only row have a non-null disposition?** `AI-2027-0038 Legacy Support Classifier` is in the inventory with `status = retired` and not in the registry — chapter 05's "Inventory-only" guidance calls this *often benign*. The record row should name it as **verified retired** with no further action; a blank disposition is the smell chapter 05 warns about.

If any of the five is "no", revise *that section* before considering the lab done.

## Why this is a lab, not an exercise

Exercise-05 asks you to *construct* a 15–20 row dataset with a specific discrepancy shape (at least 3 registry-only, at least 2 inventory-only, at least 4 drift, at least 4 no-drift, at least 2 normalisation traps), run the pandas reconciliation, write a full reconciliation memo, and author three sample follow-up drafts (gap ticket, follow-up email, re-review request). The exercise is open-ended design work.

This lab is the complementary shape: a *fixed, smaller* dataset the chapter-anchored expected counts can be checked against, a *step-by-step* code walk that forces you to run and interpret each command, and a focused record-row authoring pass. The failure mode a new analyst actually has on a Monday morning is not "cannot design their own test CSV" — it is "runs pandas commands against a real export and does not catch the hyphen-trap normalisation, or over-fires re-reviews on every version bump, or under-flags a shadow-AI system whose name already screams Annex III". This lab exercises that interpretation reflex on a dataset with the answer key hidden in the checkpoint section.
