# Cross-Referencing the Impact Assessment, Model Card, and Inventory Row

## Why this chapter

By this chapter the analyst is holding, per system, at least: an inventory row (`mod-102`), a risk register with entries (`mod-103`), a bias-review note where relevant (`mod-104`), a 42005-shaped canonical impact-assessment document (chapter 01), one or more regulator-shaped views (chapters 02–05), a model card (chapter 06), possibly a system card and one or more datasheets (chapter 07), and downstream artefacts — eval reports, vendor reviews, incident-response plans, monitoring outputs — the analyst references.

The load-bearing analyst-tier discipline: a reader entering the corpus at *any one* artefact must be able to walk to any of the others without contacting the analyst. The audit test three years on is: *can the reviewer reconstruct what the enterprise knew when the system was deployed?* The answer is only yes if the artefacts cross-reference each other with stable identifiers.

This chapter walks the cross-reference block, the provenance chain, the walk discipline, and the failure modes that break it.

## The cross-reference block

Every governance-facing artefact in the corpus carries a short cross-reference block near the head — three to eight lines, structured. A minimal viable block:

```
System: MCDA (Marketing Copy Draft Assistant)
Inventory row: INV-2026-0088
Risk register entries: RR-2026-0212, RR-2026-0213, RR-2026-0214, RR-2026-0215
Canonical impact assessment: CDX-2026-0198
Regulator views: (none — internal-only system)
Model card: MC-2026-0044 (enterprise supplement to Vendor V card MC-2026-0044-Vendor)
System card: SC-2026-0044
Datasheets: DS-2026-0071 (retrieval index)
Bias-review note: BR-2026-0117
Eval reports: EV-2026-0091 (template rev v1.4)
Vendor reviews: VR-2026-0044, VR-2026-0031
Incident-response plan: IR-2026-0011
Monitoring dashboard: MON-2026-0055
```

Every artefact in the corpus has one. The block is machine-parseable — a tabular schema in the GRC platform or a YAML front-matter block in a Markdown document.

The identifiers are stable — they do not change when the artefact revisions. A version suffix (`-v2`, or date-versioning `-2026-08-01`) tracks revisions. The identifier `RR-2026-0212` refers to the same conceptual risk-register entry regardless of how many times it has been updated; the current revision is retrievable from the identifier.

## The provenance chain

The identifiers are not just labels. Each artefact in the corpus asserts what other artefacts it *reads from* and what artefacts *depend on* it. The chain that runs through the MCDA:

- **Intake questionnaire (`mod-102`)** → **inventory row INV-2026-0088** — the intake row lists what fields were captured and cites the questionnaire response.
- **INV-2026-0088** → **risk register entries RR-2026-0212 through RR-2026-0215** — the register entries name their source inventory row.
- **RR-2026-0212 through RR-2026-0215** → **canonical impact assessment CDX-2026-0198** — the canonical document's *enumerated impacts* section reads directly from the register entries. Where the register entry is amended, the canonical document's next revision picks up the change.
- **CDX-2026-0198** → **regulator views** (AIA / FRIA / DPIA / sector, chapters 02–05) — each view names its source canonical document and version.
- **CDX-2026-0198** → **model card MC-2026-0044 (enterprise supplement)** — the model card's ethical-considerations section reads from the same register entries; the model card cites the canonical document.
- **MC-2026-0044** → **system card SC-2026-0044** — the system card *extends* the model card and cites it; it does not repeat model-tier content.
- **MC-2026-0044** → **datasheet DS-2026-0071** — the model card's training-data / evaluation-data sections cite the datasheet.
- **All of the above** → **eval report EV-2026-0091** — the metrics claims across model card and system card cite the eval report.
- **All of the above** → **incident-response plan IR-2026-0011** and **monitoring dashboard MON-2026-0055** — the monitoring surface and the incident-response mechanics tie back to the register entries and the impact assessment.

Reading the chain in the other direction — starting from a monitoring alert — the operator can walk: alert → dashboard entry → register entry → canonical document → regulator view. That is the walk discipline.

## Six walks the reader must be able to perform

Six read-paths the corpus must support without analyst intervention:

1. **From the inventory row to everything.** A director-level review of the AI portfolio starts at the inventory. The row lists every downstream artefact for the system by ID. The reader can pull each in turn.

2. **From the register entry to the canonical impact assessment.** A risk-committee review of a single high-residual risk. The entry cites the canonical document and the section of it that develops the risk's affected-population and treatment narrative.

3. **From the canonical impact assessment to the regulator views.** Legal counsel asks: *what did we tell the market-surveillance authority*. The canonical document lists its derived views and their filing dates.

4. **From the model card to the risk register.** A downstream deployer of the model asks: *what are the known risks and their treatments*. The model card's ethical-considerations section cites the register entries.

5. **From the eval report to everywhere it is cited.** The ML team updates an eval report. The corpus must surface every artefact that cites the old version so revisions can propagate. The eval report's cross-reference block lists its consumers.

6. **From an incident to the artefacts affected.** An incident is logged in the monitoring channel. The incident-response plan cites the register entries the incident maps to; from there the canonical document and the model card can be revised. The corpus supports the reverse walk.

Any of the six walks that breaks — a dangling reference, a stale identifier, an artefact with no cross-reference block — is a finding.

## Cross-referencing failure modes

Six recurring failure modes the analyst pre-empts:

- **The renaming drift.** An artefact is renamed and downstream references are not updated. Enforced by using stable identifiers and not names in cross-reference blocks.
- **The version drift.** An artefact is revised and downstream references still cite the old version. Enforced by dated version suffixes and a re-cite policy on major revisions.
- **The forked-artefact drift.** The enterprise renders an external card and the external and internal cards drift over time. Enforced by treating the internal card as the source and the external card as the rendering (chapter 06).
- **The dangling reference.** An artefact cites another artefact that no longer exists. Enforced by pre-deletion cross-reference-block scan.
- **The one-way reference.** Artefact A cites artefact B, but B does not cite A. The walk from B to A fails. Enforced by bidirectional cross-reference discipline — when a new artefact is authored, every referenced artefact is updated to cite it back.
- **The verbal-only reference.** *See the eval report* without an identifier. Enforced by mechanical review — every reference in a governance artefact carries an identifier.

The GRC platform (`mod-102` chapter 04) is where the cross-reference discipline scales. Manual enforcement works at ten systems; it breaks at a hundred.

## The cadence — when the cross-references get walked

The corpus is walked on a set cadence:

- **On every new artefact.** The new artefact's cross-reference block is populated; every artefact it references is updated to cite it back.
- **On every artefact revision.** Downstream artefacts that cite the revised one are scanned; where the revision materially changes a claim they cite, they are re-visited.
- **Quarterly for tier-1 (high-tier) systems.** A full walk of the cross-references by the analyst; findings recorded.
- **Annually for tier-2 (medium-tier) systems.** Same walk at lower cadence.
- **On any incident.** The incident-affected artefacts' cross-reference blocks are walked; upstream and downstream references confirmed.
- **On any regulator inquiry.** The affected view's cross-reference chain is walked, and the walk is logged as evidence.

The analyst-tier discipline: the walk is a *doing*, not a *reading*. Each walk produces a small artefact of its own — a walk log that says *walked on X date; all references valid; no drift; no findings*. That artefact is the audit answer to *did you keep the corpus consistent?*

## Concrete example — walking the MCDA corpus

Assume an incident is logged: *copywriter published draft externally without review; content contained fabricated product spec; customer-support ticket opened*. The walk from the incident to the affected artefacts:

- Incident report IR-2026-0011-INC-0003 references risk-register entry RR-2026-0212 (confabulation of product facts).
- RR-2026-0212 references canonical document CDX-2026-0198 and NIST MAP subcategory MAP 5.1.
- CDX-2026-0198 is not a regulator-view-triggering system (MCDA is internal), so no regulator-view revision required.
- CDX-2026-0198 references model card MC-2026-0044 whose ethical-considerations section discusses this exact risk; the section is revised to note the incident and the new mitigation.
- MC-2026-0044 references eval report EV-2026-0091; the ML team is asked whether the eval should be re-run against the incident-relevant slice.
- MC-2026-0044 references monitoring dashboard MON-2026-0055; the analyst adds a monitoring hook to flag any similar future draft that lacks a review-endorsement marker.
- Cross-reference block on IR-2026-0011-INC-0003 confirms the walk was completed on the incident date; the walk log is filed alongside the incident.

Every citation resolves. Nothing dangles. The next reviewer can start from any artefact in the chain and reach every other artefact.

## What analyst-tier cross-referencing work is *not*

- **Not the GRC platform administration.** Enterprise GRC administration is `mod-102` chapter 04 and, at scale, a GRC-platform team scope. The analyst uses the platform; the platform's schema and cross-reference machinery are the platform team's.
- **Not the enterprise identifier scheme.** The identifier convention (INV-, RR-, CDX-, MC-, SC-, DS-, BR-, EV-, VR-, IR-, MON-) is a governance-architecture decision; the analyst applies it.
- **Not the archival policy.** How long revisions are retained is a records-management call. The analyst references the archival policy from the review-cadence section of the canonical document.
- **Not automation authorship.** Tools that scan for dangling references (a `governance-lint` job in CI, a scheduled GRC platform scan) may exist; authoring them is platform-team scope, though the analyst may specify the checks.

## What to memorise

- **The cross-reference block** — every governance-facing artefact carries one; it names the whole corpus for that system by stable identifier.
- **The provenance chain** — intake → inventory → register → canonical impact assessment → regulator views + model card + system card + datasheets → eval reports + vendor reviews + incident and monitoring plan.
- **The six walks** — from inventory, from register entry, from canonical impact assessment, from model card, from eval report, from incident.
- **The six failure modes** — renaming drift, version drift, forked-artefact drift, dangling reference, one-way reference, verbal-only reference.
- **The walk cadence** — every new artefact, every revision, quarterly / annual by tier, on incident, on regulator inquiry.

## Summary

The impact assessment, model card, and inventory row cross-reference each other by stable identifier so a reader can walk from any one artefact to any of the others without analyst intervention. The provenance chain runs from intake through inventory, register, canonical impact assessment, and regulator views, into model card, system card, datasheets, and downstream eval / incident / monitoring artefacts. Every artefact carries a cross-reference block; the analyst walks the block on new authoring, on revision, and on cadence. The audit answer to *did you keep the corpus consistent?* is the walk log.
