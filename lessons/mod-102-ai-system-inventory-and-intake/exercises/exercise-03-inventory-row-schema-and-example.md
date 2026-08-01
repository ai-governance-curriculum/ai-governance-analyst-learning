# Exercise 03 — Inventory Row Schema and Example

**Estimated effort:** 2 hours
**Grounding chapter:** [03 — The AI System Inventory — Row Schema and Registry Sync](../03-inventory-row-and-registry-sync.md)

## Objective

Design a working AI-system inventory schema — the canonical row that answers "which AI systems are we running, and what do we know about each?" — and populate it for three systems across three lifecycle states (proposed, in-production, retired). The goal is to feel the shape of the artefact well enough to open one in a real GRC platform or spreadsheet on day one of a job and start maintaining it without reinventing the fields.

You should finish this exercise able to write a governance-facing sentence like "the inventory row for AI-2026-0087 shows Medium tier, annual review due 2027-03-01, next material-change re-review pending" without pausing.

## Prerequisites

- Chapter 03 read; exercise-02 completed (you need triage output to have realistic tier tags).
- The [NIST AI RMF Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) MAP 1 through MAP 4 entries open, since inventory fields map back to them.
- The [ISO/IEC 42001:2023](https://www.iso.org/standard/81230.html) Clause 8 (operation) and Clause 9 (performance evaluation) references skimmed — the inventory is one of the artefacts these clauses want to see.
- A drafting surface: a Markdown table, a `.yaml` / `.json` schema, a Google Sheet / Excel workbook, or a Notion database. Whichever you would defend to an auditor as version-controlled.

## Problem statement

Produce three artefacts:

1. **A schema file** (`inventory-schema.yaml` / `.json` / `.md`) defining every column of the inventory row. For each field: name, data type, whether it is required, whether it is single- or multi-valued, where it is sourced from (intake / triage / ML registry / analyst-fill / other artefact), and where it is consumed downstream (which register, which artefact, which report).
2. **Three populated inventory rows** covering three lifecycle states:
   - **A proposed system** — post-intake, post-triage, pre-development. Some fields are legitimately empty; those should be marked `pending` with a target date and owner, not left blank.
   - **An in-production system** — a fully populated row like the MCDA example in the chapter, but for a *different* system. Do not reuse MCDA verbatim.
   - **A retired system** — a row where status = retired, with the retirement date, the reason, the replacement pointer (or explicit "no successor"), and every artefact link still resolving. Frozen but not deleted.
3. **A material-change register** (`change-log.md` or an appended section) that captures the change history for the in-production system across at least three plausible events — two non-material (a bug-fix release, a monitoring-tool swap) and two material (a version bump that changed data sources; a user-population expansion to a new jurisdiction). Show which events fire the re-assessment cycle and which do not.

## Requirements

- **Every canonical section from chapter 03 is present** in the schema: identity and ownership, classification, artefact cross-references, lifecycle and status. If you add fields (sector-specific compliance IDs, cloud-provider tags, cost-attribution codes), justify them with a one-line comment; if you remove any canonical field, justify the removal.
- **The System ID field is the primary key** and appears on every downstream artefact reference in the three populated rows. A row without a System ID is not a row.
- **The distinction between inventory / model registry / risk register / control matrix is respected.** Fields that belong on the model registry (hyperparameters, training-run IDs, evaluation metric values) do NOT belong on the inventory row. Fields that belong on the risk register (per-risk owner, likelihood, impact, treatment) do not belong on the inventory row. If in doubt, put the field on the artefact it *primarily* belongs to and reference it from the inventory.
- **Every artefact cross-reference in the three populated rows resolves** — either to a real placeholder ID in a paired file (`risk-register.md`, `assessments.md`, etc.), or to an explicit `not yet authored` note. Broken cross-references silently rot the row.
- **The retirement row demonstrates the "retired ≠ deleted" rule.** Every artefact link that was live at retirement remains resolvable; the retirement date, reason, and successor pointer (or explicit "no successor — full decommission") are populated.
- **The material-change register cites the material-change list from chapter 03 by name.** Each event says which specific criterion it satisfies (or does not), and whether re-assessment fires.
- **No fabricated tools, vendors, or artefact IDs presented as real.** The inventory rows are exercises — that is fine — but the artefact IDs should be internally consistent placeholders, not references to real regulator IDs or real vendor products you have not actually reviewed.

## Starter guidance

- Start by copying the chapter 03 tables (identity/ownership, classification, artefact cross-references, lifecycle) into your schema file. Convert the Markdown tables into structured fields (`yaml` is easier for humans to review than `json`).
- For the *proposed* system row, use one of the vignettes from exercise-02 that landed as `in-scope`. That gives you a plausible intake and tier tag to build on.
- For the *in-production* system, pick a use case that lets you show a full set of artefact cross-references — a hosted-LLM tool with a vendor review, a risk register with two or three entries, an impact assessment, a model card. This is your "look-what-a-good-row-looks-like" sample.
- For the *retired* system, prefer a plausible reason like "replaced by successor system" or "product line sunset — no successor" rather than an incident-driven retirement (incident-driven retirements involve `mod-109` machinery you have not covered yet).
- On the material-change log, the pattern is: date, event description, criterion satisfied (or "not material — no criterion satisfied"), re-assessment triggered (yes / no), record ID for the re-review if yes.
- If you cannot decide whether a field belongs on the inventory row or elsewhere, ask "who *owns* this field — the governance analyst, the ML engineer, or the risk owner?" That usually tells you.

## Acceptance criteria

- `mod-102-ex-03-schema.yaml` (or `.json` / `.md`) with every field described per the requirements above.
- `mod-102-ex-03-rows.md` (or three separate files) with the proposed, in-production, and retired inventory rows populated.
- `mod-102-ex-03-change-log.md` with at least four events on the in-production system, showing which fire re-assessment.
- Every canonical section from chapter 03 is present; every removal or addition is justified.
- Every cross-reference resolves to a placeholder ID or an explicit `not yet authored` note.
- No fabricated real-world IDs; any factual claim about a specific vendor / regulator / framework is either verifiable or marked `<!-- needs-research: -->`.

## Stretch goals

- **Publish the schema as JSON Schema** with proper `type`, `enum`, and `required` declarations. Include a validator (Python `jsonschema` or `ajv` in a tiny script) that a peer can run to check inventory rows against the schema.
- **Add a governance-metrics view.** Derive from the inventory: how many systems by tier, how many with an assessment older than 12 months, how many with an expiring vendor review, how many pending retirement. Sketch the SQL or pandas query.
- **Cross-walk to a specific GRC platform.** Take your schema and map each field to the corresponding field name in Credo AI, Holistic AI, ModelOp, or ServiceNow AI Control Tower (whichever has published enough public documentation for you to be able to cite). Note fields that do not have a native home in the platform.
- **Add a machine-readable "review cadence" derivation.** Given the tier tag, autonomy level, and deployment surface, write the rule that produces the next-review-due date. Have your peer test it against three edge cases (a high-risk internal tool; a limited-risk external-facing tool; a minimal-risk internal tool with a recent material change).
- **Author a retention policy.** Retired-but-not-deleted rows still need a retention rule. Sketch the policy: retention length, storage location, access controls, and the destruction event (if ever).

## Deliverables

- `mod-102-ex-03-schema.<yaml|json|md>` — the schema.
- `mod-102-ex-03-rows.md` — three populated rows.
- `mod-102-ex-03-change-log.md` — the material-change register.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The reference solution in the paired solutions repo picks a particular set of three systems and a particular schema serialisation (YAML with a JSON Schema validator). Your schema *should* differ in the sector-specific field additions and the choice of populated systems; what should not differ is the primary-key discipline, the artefact cross-reference resolution, and the material-change criterion citations. If your rows tell a governance-record story a reviewer can read without needing to ask questions, the exercise is complete.
