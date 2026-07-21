# The AI System Inventory — Row Schema and Registry Sync

## Why this chapter

The AI system inventory is the enterprise's authoritative answer to "which AI systems are we running?" — and, therefore, the authoritative answer to almost every regulator, auditor, or board question about AI in the organisation. If the inventory row for a system is wrong or stale, the risk assessment attached to it is wrong or stale by definition, and the enterprise cannot report against ISO/IEC 42001 Clause 8 (operational planning and control) or [EU AI Act Article 12 (record-keeping)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj).

The analyst does not architect the inventory schema — that is the [senior AI governance architect](https://github.com/ai-governance-curriculum/senior-ai-governance-architect-learning) desk. The analyst **maintains** it: adds new rows from intake, updates rows on change, files gaps against the ML team's model registry, and closes them.

## The inventory row — canonical schema

Enterprise inventories converge on a schema like the one below. Field-by-field, and with a note on where it comes from and where it flows to.

### Identity and ownership

| Field | Source | Downstream |
|---|---|---|
| **System ID** | Assigned at intake acceptance | All artefacts trace here |
| **System name** | Intake | Human-readable label |
| **Version / release** | ML team registry export | Change tracking |
| **Business owner** | Intake | RACI |
| **Technical owner** | Intake or ML partner | RACI |
| **Governance owner (analyst)** | Assigned at triage | RACI |
| **Status** | Enum: proposed / in-development / in-production / retired | Filters downstream reports |
| **First deployed date** | ML team registry | ISO 42001 Clause 8 evidence |
| **Last material change date** | Change log | Trigger for re-assessment |

### Classification

| Field | Source | Downstream |
|---|---|---|
| **Model family** | Intake | Determines applicable overlays |
| **Model provider** | Intake | GOVERN 6 supplier list |
| **Data sources** | Intake | Data-governance overlap |
| **Autonomy level** | Intake | Human-oversight design (Art. 14) |
| **Deployment surface** | Intake | Article 50 disclosure trigger |
| **EU AI Act tier** | Triage | FRIA / Annex IV / registration |
| **Enterprise tier** | Triage | Internal review cadence |
| **Sector regulator(s)** | Triage | Sector-overlay templates |
| **Applicable framework** | Triage | Which assessment template |

### Artefact cross-references

| Field | Points to |
|---|---|
| **Risk register entries** | The rows in the risk register that tie to this system |
| **Risk assessment** | The latest NIST RMF MAP walk artefact |
| **Impact assessment(s)** | AIA / FRIA / DPIA / sector IA |
| **Model card / system card / datasheet** | Documentation-set links |
| **Control matrix row** | The Statement of Applicability slice for this system |
| **Vendor review record(s)** | Third-party review artefacts for any external component |
| **Eval / red-team report(s)** | Latest evidence set |
| **Incidents** | Any incident register entries filed against this system |

### Lifecycle and status

| Field | Source | Downstream |
|---|---|---|
| **Next review due** | Program cadence + tier-driven multiplier | Analyst work queue |
| **Continuous monitoring dashboard link** | ML / eval team | Analyst monitoring interpretation (`mod-109`) |
| **Retirement plan** | System owner | End-of-life record |

## What the inventory is *not*

- **Not the model registry.** The ML team runs a model registry (MLflow, Vertex AI Model Registry, SageMaker, Weights & Biases, an internal thing). It carries *engineering* facts: model artefacts, hyperparameters, training runs, evaluation metrics. The governance inventory carries *governance* facts: ownership, tier, obligations, artefacts. They intersect on system identity, provider, version — that is where sync work happens.
- **Not the risk register.** The risk register is per-*risk*, one row per identified risk item routed to an owner with a residual claim. The inventory is per-*system*. A single inventory row points to many risk-register entries.
- **Not the control matrix.** The control matrix is a Statement of Applicability slice per system — control-by-control status. The inventory row points *at* it.

Keeping these distinct matters. When a stakeholder asks "how many AI systems do we have?" the answer comes from the inventory. When they ask "how many open risks?" the answer comes from the risk register. Conflating the two produces reports that neither track.

## Registry-sync work — the actual daily rhythm

The inventory and the model registry are both moving. Someone re-trains a model and pushes a new version to the registry; the inventory needs to know so the governance owner can decide whether it is a material change. Someone deprecates an old model artefact in the registry; the inventory row needs to move to *retired*. Someone stands up a new model in the registry that never went through governance intake at all — that is a gap to close.

The analyst-tier work pattern is a **weekly reconciliation**:

1. Pull a registry export (typically a CSV, JSON, or a query against a registry API) with the fields (system name, version, deployed date, provider, owner).
2. Pull the governance inventory export with the same identity fields.
3. Compute three sets:
   - **In inventory not in registry** — investigate whether the system was retired without notification.
   - **In registry not in inventory** — file an inventory-gap ticket per row; email the ML owner to run intake retrospectively.
   - **In both, but material-change signals differ** (new version deployed since last review, provider changed, owner changed) — flag for governance re-review.
4. File the delta as a governance-record row with the three-set counts, the specific gap tickets opened, and the SLA for closing them.

This is the workflow the `mod-102 exercise-05 pandas reconciliation drill` walks through with code.

## The material-change definition

A material change is a change that could invalidate the last risk-and-impact assessment. Analyst-tier list of what counts (borrow it verbatim into the enterprise's own definition):

- Change of model family or model provider.
- Change of training / grounding data sources or introduction of a new fine-tune.
- Change of decisioning autonomy (moving from advisory to assistive, or up).
- Change of deployment surface (moving from internal to external, or scope expansion).
- Change of user population (materially — e.g., rolling out to a new country).
- Addition of a new tool / API in an agentic pipeline.
- Change of applicable jurisdictions.
- A material incident against the system.

Any material change fires a re-assessment. Non-material changes (a bug-fix patch, a prompt-template tweak that does not change intent, a monitoring-tool swap) are logged in the change-note field but do not trigger the assessment cycle.

## Retirement and evidence retention

When a system retires, the inventory row moves to *retired* but does **not** get deleted. Regulators and auditors ask about systems that ran for years and were then shut down — the evidence chain (assessments, incidents, controls, monitoring records) has to survive the retirement. The analyst's retirement checklist:

- Record retirement date and reason.
- Confirm data-handling wind-down (deletion or archival per data-retention policy).
- Freeze artefact links so a later reader can walk them.
- Record whether the retirement was a *replacement* (link to the successor inventory row) or a *decommission* (no successor).

## Concrete example — a stable inventory row

The Marketing Copy Draft Assistant (MCDA) from chapter 01, now three months into production, has an inventory row that looks like:

- **System ID:** AI-2026-0087
- **Name:** Marketing Copy Draft Assistant (MCDA)
- **Version:** v1.3.2
- **Status:** in-production
- **Business owner:** Priya Nair
- **Technical owner:** Marketing Data Platform team lead
- **Governance owner:** *you*
- **First deployed:** 2026-09-15
- **Last material change:** 2026-11-02 (added a per-brand prompt template — noted as material because it changes the user population served)
- **Model family:** Hosted foundation model (LLM)
- **Model provider:** Vendor V, model M v2024-06
- **Data sources:** Internal product briefs, prior campaigns
- **Autonomy level:** Assistive
- **Deployment surface:** Internal user-facing
- **EU AI Act tier:** Limited (Article 50 — disclosure of generative content in downstream campaigns)
- **Enterprise tier:** Medium
- **Sector regulators:** Marketing / advertising (no direct AI-specific regulator; FTC / state advertising rules)
- **Framework:** NIST AI RMF + ISO/IEC 42001
- **Risk register:** RR-2026-0212 (confabulation on product facts), RR-2026-0213 (brand-voice homogenisation)
- **Impact assessment:** IA-2026-0091 (algorithmic IA + light DPIA)
- **Model card:** MC-2026-0087
- **Control matrix:** CM-2026-0087
- **Vendor review:** VR-2026-0044 (Vendor V) — expires 2027-04
- **Eval reports:** ER-2026-0089 (v1.3.2 acceptance eval)
- **Incidents:** none
- **Next review due:** 2027-03-01 (annual review — Medium tier)
- **Monitoring dashboard:** internal-obs://mcda-v1

That single row is the audit answer to "how do I trace everything about this system?" and it fits on one screen.

## What to memorise

- The **three sections** of the inventory row: identity/ownership, classification, artefact cross-references (plus lifecycle).
- The **distinction between inventory, model registry, risk register, and control matrix** — each has a different key and a different owner.
- The **material-change list** — memorise it verbatim; it drives when re-assessment fires.
- The **weekly registry-sync three-set pattern**: inventory-only, registry-only, both-with-drift.
- The rule: **retired ≠ deleted** — the evidence chain outlives the system.

## Summary

The AI system inventory is per-system, governance-owned, and the ground-truth answer to "which AI systems are we running?" It is a peer of — not the same as — the ML team's model registry, the risk register, and the control matrix. Analyst work is maintenance: add new rows at intake acceptance, update on material change, run weekly registry-sync, file gaps, and preserve retired rows for the audit trail. A stable inventory row fits on one screen and points cleanly at every downstream artefact for the system.
