# Reconciling the Model Registry Against the Governance Inventory — pandas / Excel

## Why this chapter

The weekly reconciliation between the ML team's model registry and the governance inventory is the single most common data-hygiene task the AI governance analyst runs. It surfaces the systems that got into production without going through governance (the *shadow AI* problem), the systems that were retired without notifying governance, and the systems that had a material change since the last review.

You do not need to be a data engineer. You need to be able to open a CSV in pandas or Excel, do a set difference on two identity keys, filter for material-change signals, and file a governance-record row with the results. This chapter walks that workflow with concrete code.

## The reconciliation shape

Two exports, one join. On the left, the model registry. On the right, the governance inventory. The reconciliation produces three sets:

- **Registry-only.** Present in the ML team's registry, absent from the governance inventory. Almost always a *shadow AI* row — the ML team deployed something without governance intake. Analyst work: open a gap ticket per row and route to the technical owner for retroactive intake.
- **Inventory-only.** Present in the governance inventory, absent from the registry. Often benign (the system was retired and the registry pruned it, but the inventory row correctly persisted as *retired*). Sometimes a smell (the inventory has a stale entry for a system nobody remembers running).
- **Both, but material-change drift.** Present in both, but with a signal that something changed since the last governance review — a new version deployed, a provider changed, an owner changed, a training-data source added. Analyst work: fire a governance re-review.

## The identity-key problem

The single most consequential design decision is *what identifies a system*. The obvious answer — the system name — is fragile. Names drift ("Marketing Copy Assistant" → "Marketing Copy Draft Assistant" → "MCDA"). Analysts use them, ML engineers rename them, product-marketing teams rebrand them.

The reliable identifier is a **system ID** assigned at intake acceptance (per chapter 03), and carried into the model registry as a tag / label / metadata field on the model artefact. When the ML team registers a new model, they pass the governance system ID. When the ML team creates a *new* system without an ID, that is itself a signal — the reconciliation surfaces it.

If the enterprise has not yet standardised on system IDs, the fallback join key is a **composite** — normalised system name + business unit + version-independent slug. Ugly, but it is what programs use in month one.

## The pandas walk

The `mod-102 exercise-05` walks the code with a sample dataset. Here is the annotated shape.

```python
import pandas as pd

registry = pd.read_csv("model_registry_export.csv")
inventory = pd.read_csv("governance_inventory_export.csv")

# Normalise identity keys.
def norm(s):
    return s.str.lower().str.strip().str.replace(r"\s+", "_", regex=True)

registry["key"] = norm(registry["system_id"].fillna(norm(registry["name"])))
inventory["key"] = norm(inventory["system_id"].fillna(norm(inventory["name"])))

# Set differences.
registry_only = registry[~registry["key"].isin(inventory["key"])].copy()
inventory_only = inventory[~inventory["key"].isin(registry["key"])].copy()
both = registry.merge(inventory, on="key", how="inner", suffixes=("_reg", "_inv"))

# Material-change signals inside 'both'.
material_change = both[
    (both["version_reg"] != both["last_reviewed_version_inv"])
    | (both["provider_reg"] != both["provider_inv"])
    | (both["technical_owner_reg"] != both["technical_owner_inv"])
    | (both["training_data_sources_reg"] != both["training_data_sources_inv"])
].copy()

# Rank by tier so high-risk drift jumps to the top of the report.
tier_order = {"Critical": 0, "High": 1, "Medium": 2, "Low": 3}
material_change["tier_rank"] = material_change["enterprise_tier_inv"].map(tier_order)
material_change = material_change.sort_values("tier_rank")
```

The output is three DataFrames that turn directly into three sections of the weekly governance-record row.

## The Excel-only walk

Not every analyst has pandas available. The reconciliation is doable in Excel — slower and more error-prone, but auditable.

- Load both exports into two sheets of the same workbook.
- Add a normalised-key column to each with `=LOWER(TRIM(SUBSTITUTE(A2," ","_")))`.
- In the registry sheet, add a column `In inventory?` = `=IF(COUNTIF(inventory!B:B, B2)>0, "Y", "N")`.
- In the inventory sheet, add a column `In registry?` similarly.
- Filter each to `N` and copy to a `registry_only` / `inventory_only` sheet.
- For rows in both, use `VLOOKUP` or `XLOOKUP` to pull the registry-side value for each field into the inventory row, and add a `Material change?` column checking for any inequality.

The Excel approach is defensible when the register is small (< 200 systems). Above that, pandas or the platform-native workflow scales better.

## What to report

The reconciliation output is a governance-record row, not a raw DataFrame. Structure it as:

- **Reconciliation date and analyst.**
- **Registry-only count and list**, with a gap-ticket ID opened per row.
- **Inventory-only count and list**, with disposition per row (verified retired / opened for follow-up).
- **Material-change count and list**, ordered by tier, with the re-review action taken per row.
- **Assumptions** — any normalisation choices the analyst had to make when the identity key was ambiguous.
- **Turnaround SLA on gap tickets** — a stated commitment.

Attach the three CSV / Excel exports as immutable evidence of the reconciliation state at that date.

## Common failure modes

- **Registry export is stale.** Some ML platforms treat model retirement as a soft-delete; a naive export includes retired rows. Check the export includes only currently-live artefacts, or add a status filter.
- **Provider strings differ non-substantively.** "OpenAI" vs "openai" vs "OpenAI (Azure)" all describe the same provider. Normalise before comparing, or the material-change filter fires spuriously.
- **Training-data-sources field is unstructured text.** A change from "Product briefs" to "Product briefs; prior campaigns" is real; a change from "Product briefs" to "product-briefs" is punctuation. Normalise, and where the field is genuinely free text, mark material-change signals as *soft* — worth flagging to the ML owner but not automatically firing a re-review.
- **The registry export lacks the system ID.** Then the fallback join key is composite, and matches are lossier. File a gap ticket to the ML team asking them to plumb the system ID through — this pays back every week thereafter.

## Cross-jurisdiction and privacy touchpoints

Some reconciliation outputs have specific downstream obligations. If the reconciliation reveals a system that:

- Is in-production and handles EU personal data but has no DPIA on file → route immediately to the privacy team.
- Is in-production and falls under Annex III but has no FRIA on file → route immediately to the FRIA workflow.
- Is in-production, EU AI Act high-risk, and not registered in the EU database → route to legal per EU AI Act Article 71.

These are the analyst-tier findings the reconciliation is *for*.

## Concrete example — the MCDA reconciliation

The weekly reconciliation runs. The registry shows `MCDA` at version `v1.4.0`; the inventory has last reviewed version `v1.3.2`. The material-change filter fires. The analyst inspects the version-diff notes from the ML team and finds the difference is a new prompt template for a new brand. That is a change of user population — per chapter 03's material-change list, it fires a re-assessment. The analyst opens `RR-2027-0044` as the re-review ticket, tags the governance owner (still you), and notes the SLA. The reconciliation record row captures the finding and the routing.

At the same time, the reconciliation surfaces a new system `Support Ticket Classifier` in the registry with no inventory row. The analyst emails the technical owner listed in the registry ("please run governance intake retroactively — SLA is five business days"), opens a gap ticket, and includes both findings in the weekly reconciliation summary sent to the governance council.

## What to memorise

- The **three sets**: registry-only, inventory-only, both-with-drift.
- The **join key priority**: system ID first; composite normalised-name fallback second.
- The **material-change signals**: version, provider, owner, data sources, autonomy, deployment surface, jurisdictions.
- The **governance-record row shape** for the weekly reconciliation output.
- The **specific high-severity findings**: EU personal data + missing DPIA; Annex III + missing FRIA; EU AI Act high-risk + missing EU database registration.

## Summary

Reconciling the ML team's model registry against the governance inventory is a weekly analyst-tier task that surfaces shadow AI, retired systems, and material-change drift. The workflow is a three-set diff on a well-chosen identity key, followed by a filter for material-change signals, followed by a governance-record row with actions and SLAs. pandas is the faster path; Excel works for small registers; either produces auditable evidence when the analyst captures normalisation choices as assumptions. The findings are the point — the reconciliation is a governance instrument, not a data-engineering exercise.
