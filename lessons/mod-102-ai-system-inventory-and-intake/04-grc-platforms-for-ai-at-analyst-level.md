# GRC-for-AI Platforms at Analyst Level — and the Spreadsheet Fallback

## Why this chapter

Enterprise governance programs run on a tool. Sometimes it is a dedicated GRC-for-AI product with prebuilt intake templates, an inventory schema, control libraries pre-crosswalked across ISO/IEC 42001, NIST AI RMF, and EU AI Act, and workflow automation. Sometimes it is a general-purpose GRC platform (ServiceNow, Archer, MetricStream) with AI-specific modules bolted on. Sometimes it is the Governance-Risk-Compliance module of a productivity suite. And sometimes, especially early-stage or mid-market, it is a shared spreadsheet.

At analyst tier your job is to *use* whichever tool the enterprise has adopted, at a level that keeps the register clean and the workflow moving. You do not architect the platform. You do not run the tool procurement. You need to know enough to sit an intake, an inventory row, and a control-testing cycle inside it.

This chapter gives you the vendor landscape as of the middle of 2026, the analyst-tier features of each, and the spreadsheet fallback for programs that have not adopted a dedicated tool.

## The vendor landscape

The GRC-for-AI category is young — most vendors reached general availability between 2022 and 2025 — and consolidating fast. The four vendors below are the ones an analyst is most likely to encounter in job interviews and on live programs. Read their marketing pages at [Credo AI](https://www.credo.ai/), [Holistic AI](https://www.holisticai.com/), [ModelOp](https://www.modelop.com/), and [ServiceNow AI Control Tower](https://www.servicenow.com/products/ai-control-tower.html); the marketing shifts, but the analyst-tier feature shape is stable.

<!-- needs-research: verify each vendor's current feature set and product name against their official documentation before citing in an external-facing document; the GRC-for-AI product category is fluid and product-name refactors are common. -->

### Credo AI

Positioned as an AI governance platform with prebuilt template libraries for use-case intake, model / system registration, risk-and-impact assessment, and policy-attached controls. Publishes a public [Responsible AI Standard](https://www.credo.ai/) that its templates crosswalk against. Strongest analyst-tier features are the prebuilt intake questionnaires, the policy attach mechanism, and the tie-out to model documentation.

Analyst usage: run intake through Credo's intake template; register the system; select policies to attach; monitor the alerts Credo raises when a system drifts against a policy.

### Holistic AI

Positioned around auditing and monitoring, with a portfolio of technical assessments (bias, robustness, explainability, privacy) that plug into the governance record. Uses these to produce a *risk report* per system. Strongest analyst-tier features are the technical audit modules and the export-shaped-for-regulators reports.

Analyst usage: run the technical assessment modules against a system when the ML team provides model access; ingest the outputs into the governance record; use the risk-report export as an attachment for reviewer packs.

### ModelOp

Positioned around ModelOps and the operational lifecycle — model deployment, monitoring, control-testing — with governance features layered over. Strongest analyst-tier features are the model lifecycle inventory (pulls from major ML platforms out of the box) and the continuous-monitoring integration.

Analyst usage: reconcile the governance inventory against ModelOp's model lifecycle inventory (this is the tool where your `mod-102 exercise-05` reconciliation might, in practice, happen inside the platform rather than in pandas); use ModelOp's monitoring alerts as the source of your `mod-109` monitoring-interpretation work.

### ServiceNow AI Control Tower

Positioned as an enterprise workflow overlay leveraging ServiceNow's existing ITSM / GRC install base. Adds AI-specific intake, inventory, risk, compliance, and monitoring modules on top of ServiceNow's Now Platform. Strongest analyst-tier features are the workflow automation (auto-routing based on tier), the integration with the rest of the ServiceNow install (change management, incident response), and the reporting.

Analyst usage: run every intake through the AI Control Tower intake flow; every triage decision, every routing decision, every SLA sits inside ServiceNow; the risk register, the control matrix, and the incident register all live as ServiceNow tables.

## What analyst-tier features look like across platforms

The platforms differ in emphasis but the analyst-facing feature set converges. Expect any of the platforms above to give you:

- **A configurable intake template** with conditional logic (e.g., "if personal data = yes, show DPIA fields").
- **A system / model inventory** with linked artefacts (assessments, controls, incidents).
- **A prebuilt control library** cross-walked across ISO 42001 Annex A, NIST AI RMF subcategories, and EU AI Act obligations — with the SoA machinery for status tracking.
- **A risk register** with owner, likelihood, impact, treatment, residual, and evidence-attach.
- **Policy-attach and drift alerts** — when a system moves out of alignment with an attached policy, an alert fires.
- **An assessment workflow** for AIA / FRIA / DPIA / sector IAs — either a template inside the tool or an integration to an authoring surface.
- **A vendor-review workflow** with a due-diligence questionnaire and re-review cadence.
- **Reporting and export** for reviewer packs, council decks, and regulator responses.

Analyst-tier interviews and take-homes will ask you to *run* one of these workflows in a demo environment — not to configure the templates. The demo is a good place to feel the difference between a well-designed workflow (fields you can fill in one sitting; alerts that make sense; exports that regulator-shaped) and a badly-configured one (fields nobody can answer; alerts that fire on noise; exports that a regulator would reject).

## The spreadsheet fallback — when the program has not adopted a platform

Many programs, especially in their first six to twelve months, run on spreadsheets. The analyst-tier work is to make sure the spreadsheet is at least as auditable as a tool-hosted equivalent.

Minimum viable spreadsheet-shape:

- **`inventory.xlsx`** — one row per AI system, fields from chapter 03.
- **`risk_register.xlsx`** — one row per risk item, columns for system link, risk type (NIST GenAI Profile risk / ISO 23894 risk source / SR 11-7 risk category), owner, likelihood, impact, residual, evidence-attach, status.
- **`control_matrix.xlsx`** — one row per (system, control) pair, with status (implemented / not applicable with justification / gap), evidence link, last tested date, next test due.
- **`vendor_review.xlsx`** — one row per third-party AI-relevant vendor, with due-diligence status and re-review date.
- **`incidents.xlsx`** — one row per incident, per `mod-109`.
- **`change_log.md`** — every material change captured with date, system, and one-line description.

Spreadsheet-fallback discipline:

- **Version-control the files.** A shared drive with revision history at minimum; a git repo for the source-of-truth files if the enterprise allows it.
- **Log every change with a timestamp and initials.** In a tool this is automatic; in a spreadsheet you do it manually.
- **Freeze exports on any decision date** (a governance council meeting, a regulator response, an audit). The frozen exports are the evidence, not the live spreadsheet.
- **Do not scatter across multiple owners' local copies.** One authoritative version, one edit at a time.

Most enterprises graduate from the spreadsheet fallback to a platform inside twelve months. The analyst-tier job during the transition is to make sure the migration is loss-less — every row, every artefact link, every history entry lands in the platform.

## Cross-platform patterns to recognise

Whether you are on Credo AI, ServiceNow AI Control Tower, ModelOp, or a spreadsheet, these patterns recur:

- **Every intake produces one and only one inventory row.** If the tool lets you create disconnected intakes-without-inventory-rows, that is a data-hygiene bug.
- **Every risk-register entry ties to at least one control and at least one system.** Orphan risk items — risks nobody owns and no control speaks to — are the analyst's most common finding in the register cleanup pass.
- **Every control has a status: implemented / not applicable (with justification) / gap.** ISO 42001 Statement of Applicability shape. "Not implemented, no justification" is not a legal status; it is a gap.
- **Every vendor has a re-review date.** A vendor review from three years ago is no longer evidence.

## Concrete example — moving MCDA into a GRC-for-AI platform

Return to the Marketing Copy Draft Assistant. The enterprise has just procured a GRC-for-AI platform. The analyst-tier migration steps:

1. **Create the system record** — one system, one ID, populated from the existing inventory row.
2. **Attach the intake** — the original intake questionnaire becomes an immutable record on the system.
3. **Register the artefacts** — the risk assessment, the impact assessment, the model card link, the vendor review record all attach to the system record.
4. **Configure applicable policies** — Responsible AI Policy, Generative AI Employee Guidance, Vendor Standard.
5. **Configure controls** — the applicable subset of the crosswalked control library (ISO 42001 A.6, A.7, A.8; NIST GOVERN 1, GOVERN 6, MAP 5, MEASURE 2, MANAGE 4; EU AI Act Art. 50 disclosure obligations).
6. **Set the review cadence** — Medium tier drives an annual review; a monitoring alert threshold fires if a specific eval metric drops.
7. **Freeze the pre-migration state** — the spreadsheet files that predate the platform are archived as evidence of the migration point.

Done cleanly, the platform now runs the system's governance rhythm without the analyst needing to open a spreadsheet again — except for the ad-hoc exercises `mod-102 exercise-05` walks through.

## What to memorise

- The **four vendor names** and the emphasis of each: Credo AI (policies-and-templates), Holistic AI (technical audit), ModelOp (lifecycle-and-monitoring), ServiceNow AI Control Tower (workflow-and-ITSM-integration).
- The **converged analyst-facing feature set** — you will use it whichever tool the enterprise has.
- The **spreadsheet fallback file list** — inventory, risk register, control matrix, vendor review, incidents, change log.
- The **cross-platform patterns** — one intake per inventory row; every risk ties to a control and a system; every control has an ISO-42001-shaped status; every vendor has a re-review date.

## Summary

At analyst tier your job is to sit inside whichever GRC-for-AI platform (or spreadsheet) the enterprise has adopted, not to select or configure the tool. The vendor landscape has converged on a similar analyst-facing feature set — configurable intake, system inventory, crosswalked control library, risk register, policy-attach, assessment workflow, vendor-review workflow, reporting. When there is no tool yet, the spreadsheet fallback is auditable if the analyst enforces one-source-of-truth discipline and freezes exports on every decision. Migration between spreadsheet and platform is loss-less if the analyst treats it as a data-hygiene job, not a design job.
