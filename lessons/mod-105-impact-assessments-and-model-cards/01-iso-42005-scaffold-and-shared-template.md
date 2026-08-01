# ISO/IEC 42005 as the Impact-Assessment Scaffold and the Shared-Template Idea

## Why this chapter

By the time the analyst reaches this module, an intake row exists (`mod-102`) and a first-draft risk register exists (`mod-103`). The next artefact the reviewer, the regulator, or the enterprise customer asks for is an *impact assessment*: a structured, human-readable document that says *this is what the system does, this is who it affects, this is what we have done to reduce harm, and this is what we accept*.

There are at least four such documents in circulation — the Canadian algorithmic impact assessment (AIA), the EU AI Act Article 27 fundamental-rights impact assessment (FRIA), the GDPR Article 35 data-protection impact assessment (DPIA), and any sector-specific overlay (FDA good machine-learning practice, financial-services model risk, and so on). Writing each from scratch is a fast route to inconsistent artefacts and an audit finding.

The analyst-tier discipline: adopt an AI-specific impact-assessment scaffold — [ISO/IEC 42005:2025 — Information technology — Artificial intelligence — AI system impact assessment](https://www.iso.org/standard/44545.html) — as the single canonical shape, populate it from the MAP walk once, then export the regulator-shaped views on top. This chapter explains what ISO 42005 covers, how it reuses the NIST AI RMF MAP output produced in `mod-103`, and what "shared template" means in practice.

## Where ISO 42005 sits in the standard stack

ISO/IEC 42005:2025 is the AI-system-impact-assessment standard published by ISO/IEC JTC 1/SC 42, the same committee that publishes ISO/IEC 42001 (AI management system) and ISO/IEC 23894 (AI risk management guidance). The three standards are designed to interlock:

- **ISO/IEC 42001** — the AI management system standard the enterprise certifies against. Clause 6 requires an AI risk assessment and an AI system impact assessment. It points at 23894 for the risk-management shape and at 42005 for the impact-assessment shape.
- **ISO/IEC 23894** — the AI-specific risk-management guidance the analyst uses as the risk-source scan-list (`mod-103` chapter 02).
- **ISO/IEC 42005** — the AI-specific impact-assessment guidance. It is procedural (how to perform the assessment) and it is documentary (what the resulting artefact contains).

An enterprise that certifies against 42001 will typically adopt 42005 as its impact-assessment method-of-record. The AIA, FRIA, DPIA, and sector overlays then become *views* generated from the same 42005-shaped source document.

<!-- needs-research: ISO/IEC 42005:2025 is paywalled. Verify current clause numbering and section titles against the published text before quoting verbatim in an audit-facing artefact. This chapter uses the terminology in the ISO public abstract and the SC 42 published summaries; enterprise use will need a licensed copy. -->

## What ISO 42005 asks for

At the level of the public abstract and the SC 42 committee summaries, 42005 covers the following procedural and documentary elements. Titles are paraphrased where verbatim clause names are not publicly available.

**Procedural elements (how to perform the impact assessment).**

- Determine when an impact assessment is required and at what depth.
- Define the impact-assessment scope and boundary — which system, which lifecycle stage, which deployment context.
- Identify affected individuals, groups, and societal interests.
- Identify potential impacts — beneficial, harmful, direct, indirect.
- Analyse each potential impact — likelihood, magnitude, reversibility, affected population size, severity to the individual.
- Evaluate the analysed impacts against the enterprise's risk-tolerance and legal obligations.
- Treat the impacts — controls, mitigations, avoidance, transfer, informed acceptance.
- Document the assessment as a discoverable artefact with a defined review cadence.
- Consult with affected stakeholders where required by law or policy.

**Documentary elements (what the resulting artefact contains).**

- System description — purpose, deployment context, users, providers.
- Data description — training / evaluation / operational data at the level relevant to impact.
- Affected-stakeholder inventory.
- Enumerated impacts with the analysis and evaluation results.
- Treatment plan and residual acceptance.
- References to related artefacts — risk register, model card, evaluation reports, incident-response plan.
- Review triggers and review cadence.

At analyst-tier depth, that documentary shape is the template. The procedural steps read as the workflow that produces it.

## How 42005 reuses NIST AI RMF MAP output

The good news for the analyst who has just walked `mod-103`: 42005 does not ask for anything the MAP walk did not already surface. The scaffolding is different — 42005 is organised around *impacts on stakeholders*, MAP is organised around *governance functions* — but the underlying facts are the same.

| 42005 documentary element | Sourced from (MAP walk) |
|---|---|
| System description | MAP 1.1, MAP 1.3, MAP 1.4, MAP 2.1, MAP 2.2 |
| Data description | MAP 2.1, MAP 4.1 (data sources), plus intake fields |
| Affected-stakeholder inventory | MAP 1.2 |
| Enumerated impacts + analysis | MAP 5.1 with the two-lens sweep from `mod-103` chapter 02 |
| Treatment plan + residual | The mitigations and residual columns from `mod-103` chapter 03 |
| Related-artefact references | Inventory row, register entries, model card, eval reports |
| Review triggers and cadence | MAP 1.5 (risk tolerance) + enterprise policy |

The mechanical implication: the analyst does not perform a new MAP walk to author an impact assessment. The impact assessment is a *re-projection* of the MAP narrative into the 42005 shape, plus the extra fields required by whichever regulator's view is being generated.

That is the load-bearing idea of this module. Everything else follows.

## The shared-template idea

Because AIA, FRIA, DPIA, and sector overlays all draw from the same underlying facts, the analyst-tier authoring pattern is:

1. **One canonical source document per system.** Shaped by 42005. Held in the enterprise governance repository or GRC platform alongside the register entry.
2. **Regulator-shaped views layered on top.** Each view is a rendering of the canonical document into the fields and headings a specific regulator requires. Missing fields are added; the underlying evidence is reused.
3. **A cross-reference map.** A short table at the head of each view that says *this AIA reads from canonical document CDX-2026-0198; the model card is at MC-2026-0044; the register entries are RR-2026-0212 through RR-2026-0215*.

Analyst-tier authoring order:

- Author the 42005-shaped canonical document once (this module, chapters 01 and 08).
- Generate the AIA view when Canadian federal deployment is in scope (chapter 02).
- Generate the FRIA view when EU AI Act Article 27 applies (chapter 03).
- Generate the DPIA view when GDPR Article 35 applies (chapter 04).
- Generate the sector-specific view when a sector regulator is in scope (chapter 05).

The *canonical document* is the source of truth. Views are cheap and disposable — regenerate when the regulator's form changes.

## Concrete example — the MCDA 42005-shaped canonical document

Returning to the Marketing Copy Draft Assistant (MCDA) from `mod-103`.

The 42005 canonical document skeleton, populated from the MAP walk:

- **System description.** MCDA — internal marketing-copy drafting assistant. Hosted foundation-model API from Vendor V, called from an internal web tool, drafts consumed by internal copywriters, reviewed and edited before external release. Not customer-facing; not fully autonomous.
- **Data description.** Prompt inputs are structured campaign briefs; retrieval-augmented from an internal past-campaign store; outputs are draft copy. Training data belongs to the vendor and is not enumerable at deployer scope — see model card and vendor documentation.
- **Affected-stakeholder inventory.** Internal copywriters (users), marketing leaders (owners), Legal (reviewers), external customers reading the eventually-published copy (indirect but load-bearing), regulators watching brand claims (indirect).
- **Enumerated impacts.** Four register entries reused verbatim from `mod-103`: RR-2026-0212 (confabulation of product facts), RR-2026-0213 (brand-voice homogenisation), RR-2026-0214 (IP contamination), RR-2026-0215 (data leakage in prompts).
- **Treatment plan.** Human-in-the-loop review, PII prompt-scanning, vendor review sign-off, monthly copywriter forum for feedback; residuals accepted at ordinal *Medium* by the Marketing Ops owner.
- **Related-artefact references.** Inventory row INV-2026-0088; register entries RR-2026-0212 through -0215; model card MC-2026-0044 (Vendor V provided, enterprise-supplemented); vendor reviews VR-2026-0044 and VR-2026-0031; eval report EV-2026-0091 (Marketing Data Platform team, template rev v1.4).
- **Review triggers and cadence.** Annual review; ad-hoc review on any of: model version change by vendor, prompt-template rev >= v2.0, incident logged in monitoring channel, expansion of scope beyond internal copywriters.

That is the canonical document. Every regulator view in chapters 02–05 is derived from that seven-section skeleton.

## What analyst-tier ISO 42005 work is *not*

- **Not an ISO conformance audit.** Whether the enterprise's 42005 method conforms to the standard is an auditor's judgement, not the analyst's. The analyst applies the method the enterprise adopted.
- **Not a rewrite of the standard.** The analyst does not re-organise 42005 or invent new documentary sections. The regulator views layer over the canonical shape; they do not replace it.
- **Not the risk-management method itself.** ISO 23894 is where risk sources live; ISO 42005 is where the impact assessment lives. They are sibling standards; the analyst uses both.

## What to memorise

- **The three interlocking standards**: 42001 (AIMS) requires the assessment; 23894 supplies the risk-source lens; 42005 supplies the impact-assessment shape.
- **The seven documentary elements**: system description, data description, affected-stakeholder inventory, enumerated impacts with analysis, treatment plan and residual, related-artefact references, review triggers and cadence.
- **The nine procedural steps**: determine required depth, scope, stakeholders, impacts, analyse, evaluate, treat, document, consult.
- **The shared-template rule**: one canonical 42005-shaped document per system; regulator views layer on top; the canonical document reuses the MAP walk one-for-one.

## Summary

ISO/IEC 42005:2025 is the AI-specific impact-assessment standard the analyst uses as the shared scaffold for AIA, FRIA, DPIA, and sector-specific views. Its documentary shape and procedural steps map cleanly onto the NIST AI RMF MAP walk authored in `mod-103` — no new evidence gathering is required; the impact assessment is a re-projection of the MAP narrative into the 42005 shape. The analyst authors one canonical document per system, layers regulator-shaped views on top, and keeps a cross-reference map so any reader can walk from the impact assessment to the register, the model card, and the inventory row.
