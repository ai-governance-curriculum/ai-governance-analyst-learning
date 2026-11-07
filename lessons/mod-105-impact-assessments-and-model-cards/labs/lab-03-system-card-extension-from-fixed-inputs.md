# Lab 03 — System-Card Extension From a Fixed Model Card and Composition Manifest

**Duration:** 90 minutes.
**Grounding chapters:** [06](../06-model-cards-mitchell-hf-mct.md), [07](../07-system-cards-and-datasheets.md), [08](../08-cross-referencing-artefacts-and-walk-discipline.md).
**Difficulty:** Core — exercises the system-card half of chapter 07, which the module's six exercises do not cover (exercise 06 covers only the datasheet half of the chapter).

## Objective

Starting from a *fixed, already-authored* enterprise model card plus a *fixed composition manifest* supplied by the ML / platform team, author the three system-card extension sections [chapter 07](../07-system-cards-and-datasheets.md) names — Section 10 Composition and Deployment Context, Section 11 Safety Evaluation Coverage, Section 12 Change-Management Triggers — as a single file `system-card-extension.md` that sits alongside the model card and does not duplicate it. The lab's integration test is chapter 07's load-bearing claim that *a change to the retrieval index scope or a change to the tool inventory can shift the FRIA-relevant risk without any change to the model* — the extension must make that story visible.

The lab exists because exercise 05 covers the Mitchell nine-section model card (chapter 06) and exercise 06 covers the Gebru datasheet (chapter 07's second half), but no exercise asks the analyst to author the chapter-07 *system-card extension* on top of an existing model card. This lab is the missing drill.

## Prerequisites

- Chapter 06 read; the Mitchell nine sections, the analyst / ML division of labour, and the vendor-supplement pattern fresh in memory.
- Chapter 07 read; the three extra system-card sections (10, 11, 12), the Composition-is-load-bearing framing, and the public-system-card exemplars list fresh in memory.
- Chapter 08 skimmed — the system-card extension's cross-reference block feeds the walk discipline.
- Exercise 05 completed, or at minimum read, so the model-card shape the lab's fixed input assumes is familiar.
- A markdown editor; no Python tooling required.

## The fixed inputs

Use *exactly* these two inputs. Do not re-author the model card and do not substitute the composition manifest — the lab's discipline is to produce a complementary artefact, not to rewrite the ones already supplied.

### Input 1 — the enterprise model card (reproduced to its cross-reference block and headings only)

```
Model card: MC-2027-0019 — MCDA-Radiology enterprise supplement
Extends vendor card: MC-2027-0019-Vendor (Vendor V, model version 2026-01)
Inventory row: INV-2027-0012
Canonical impact assessment: CDX-2027-0033
Register entries read from: RR-2027-0051, RR-2027-0052, RR-2027-0053, RR-2027-0054
Datasheets cited: DS-2027-0014 (retrieval index — imaging-report corpus slice)
Eval report cited: EV-2027-0028 (clinical-performance eval slice; template rev v1.2)
Bias-review note: BR-2027-0007
Regeneration triggers (card-level): vendor version change, prompt-template major rev, incident logged

Section headings present (Mitchell 1–9):
1. Model Details
2. Intended Use (assistive drafting; not for pediatric imaging; not autonomous diagnosis)
3. Factors
4. Metrics (reference to EV-2027-0028)
5. Evaluation Data (reference to DS-2027-0014 and EV-2027-0028 eval-set description)
6. Training Data (vendor-controlled; defer to vendor card)
7. Quantitative Analyses (reference to EV-2027-0028 tables)
8. Ethical Considerations (reads from RR-2027-0051 through RR-2027-0054)
9. Caveats and Recommendations (annual review; card regenerated on vendor version change, prompt-template major rev, incident logged)
```

### Input 2 — the composition manifest (from the ML / platform team)

```
System: MCDA-Radiology (SC target identifier: SC-2027-0019)

Model layer
    - Base model: Vendor V foundation model, version 2026-01 (pinned; API call-through).
    - Fine-tuning: none; vendor base model used as hosted.

Prompting layer
    - Prompt template: MCDA-RAD-PROMPT-v1.0 (versioned in platform repo).
    - Safety instructions block: SI-2027-0003 (refusal cues for pediatric imaging and autonomous-diagnosis requests).

Retrieval layer
    - Retrieval index: DS-2027-0014 (enterprise imaging-report corpus slice; last refreshed 2027-01-15).
    - Scope: enterprise imaging-report corpus 2022-01 forward; pediatric imaging excluded.

Tool-use layer
    - Tool inventory: none at first release; tool-use disabled at the platform layer.

Guardrail layer
    - Pre-generation guardrail: PII pre-scan on prompt (GR-2027-0005).
    - Post-generation guardrail: output-safety classifier GR-2027-0006 (refusal on pediatric-imaging surface; refusal on diagnosis-assertion surface).

Orchestration layer
    - Rate limits per radiologist session; audit logging of prompt-plus-output pairs with per-session identifiers; session state scoped to the sign-off workflow and not persisted beyond it.

User-facing surface
    - PACS workstation integration; radiologist-facing accept / edit / reject controls; sign-off not available without a human review event logged.

Safety evaluation coverage (ML / safety team note)
    - Pre-release evals (completed): confabulation rate on EV-2027-0028 eval set; refusal behaviour on pediatric-imaging scenarios; PII-leakage detection on prompt pre-scan; bias-review across patient sex, age band, imaging modality per BR-2027-0007.
    - Pre-release evals (not run): adversarial-prompt stress test against safety instructions block; multilingual report input (English-only at first release); jailbreak-prompt refusal on pediatric-diagnosis requests.
    - Red-team findings summary: one internal red-team pass on 2027-02-02 by the enterprise AI red-team; three findings routed to model-card revision (incorporated in MC-2027-0019); two findings routed to guardrail-config update (incorporated in GR-2027-0006).

Change-management triggers (platform-team-registered)
    - Base-model version change by Vendor V.
    - Prompt-template major rev (v1.0 → v2.0).
    - Retrieval-index scope expansion (pediatric imaging ever added, any corpus beyond enterprise imaging-report corpus added).
    - Guardrail configuration change (any file-level change to GR-2027-0005 or GR-2027-0006).
    - Tool-inventory change (any tool added or removed).
    - Incident-response event mapped to any of RR-2027-0051 through RR-2027-0054.
```

All identifiers are illustrative. Treat both inputs as given; do not re-produce the model card and do not re-produce the composition manifest — the lab's deliverable is the system-card *extension* that sits on top of them.

## Steps

### Step 1 — Scaffold the extension (5 min)

Create the working folder and file.

```bash
mkdir -p ~/aicg-labs/mod-105-lab-03
cd ~/aicg-labs/mod-105-lab-03
touch system-card-extension.md
```

Open the file and lay in the section headers up front:

```markdown
# System-card extension — MCDA-Radiology (SC-2027-0019)

Extends model card: MC-2027-0019
Authored by: <your-name>
Date: <today>

## Cross-reference block
## §10. Composition and Deployment Context
## §11. Safety Evaluation Coverage
## §12. Change-Management Triggers
```

Chapter 07's shape — sections 10, 11, 12 extending the Mitchell nine — is the exact section skeleton. Do not renumber; do not compress the three into two; do not add a fourth section at this scope.

### Step 2 — Fill the cross-reference block (5 min)

Reproduce the chapter 08 cross-reference block for the system card, drawing from both inputs:

```
System: MCDA-Radiology
System-card ID: SC-2027-0019
Extends model card: MC-2027-0019 (which extends Vendor V card MC-2027-0019-Vendor)
Inventory row: INV-2027-0012
Canonical impact assessment: CDX-2027-0033
Composition artefacts: prompt template MCDA-RAD-PROMPT-v1.0; safety instructions SI-2027-0003; retrieval index DS-2027-0014; guardrails GR-2027-0005, GR-2027-0006.
Register entries read from: RR-2027-0051, RR-2027-0052, RR-2027-0053, RR-2027-0054
Eval report cited: EV-2027-0028 (template rev v1.2)
Bias-review note: BR-2027-0007
Red-team summary: internal pass dated 2027-02-02.
Regeneration triggers: see §12.
```

Chapter 08's one-way-reference discipline means both the model card MC-2027-0019 and the canonical document CDX-2027-0033 should ultimately be updated to cite the new SC-2027-0019 back. Note the citation-back obligation at the bottom of the block as a pending action (open a ticket in the walk log — chapter 08's walk-cadence rule: on every new artefact, every referenced artefact is updated to cite it back).

### Step 3 — Fill §10 Composition and Deployment Context (25 min)

Open chapter 07 in a second window. Section 10 is the load-bearing section: chapter 07 names it as the one that *can shift the FRIA-relevant risk without any change to the model*. Author it in two parts:

**§10.1 Composition inventory (ML / platform team authored; analyst reads).** Reproduce the composition manifest (input 2) as a structured table — one row per layer, columns for *layer*, *artefact identifier and pin*, *scope*, *change trigger it registers for §12*. The seven layers from the composition manifest map to the seven layers chapter 07 names (base model; prompting; retrieval; tool-use; guardrails; orchestration; user-facing surface). Do not re-author the manifest — read it, structure it, and name the pins.

The *pin* column is load-bearing. Chapter 06's analyst-tier check is that a card citing "GPT-4" without a version pin is under-specified; the same discipline applies across every row of §10.1. If a row has no pin (no version string, no file identifier), flag it as a §10.1 under-specification finding and route back to the platform team.

**§10.2 Deployment context (analyst authored from MAP 1.1 / 3.3).** The narrative sits on top of the inventory. Four to six sentences on:

- *Where the system is deployed.* PACS workstation integration in the US hospital system; radiologist-facing surface; not customer-facing.
- *Who the users are.* Board-certified radiologists only; pediatric-imaging radiologists excluded by intent (pediatric imaging is out-of-scope).
- *The human-in-the-loop controls.* Accept / edit / reject; sign-off blocked without a logged review event.
- *What the orchestration pins mean for risk.* Rate limits and audit logging per session; session state scoped to the sign-off workflow only.

Chapter 07's framing to carry through: §10 is written so that a future reviewer who learns the retrieval scope expanded to include pediatric imaging can read §10.2 and know immediately that the deployment-context claim ("pediatric imaging excluded by intent") no longer holds. §10 is where a scope change becomes a FRIA-relevant risk shift.

### Step 4 — Fill §11 Safety Evaluation Coverage (15 min)

Chapter 07 names Section 11 as ML- / safety-team-owned; the analyst reads. The composition manifest (input 2) already supplies the raw material. The analyst's authoring job is to *structure* and *route*, not to run an eval. Author in three sub-parts:

**§11.1 Evaluations completed (pre-release).** One line per eval with the specific identifier the eval report EV-2027-0028 uses for it. Link each to the register entry the eval produces evidence for — e.g., confabulation rate maps to RR-2027-0051; bias-review across the patient-sex / age-band / imaging-modality strata maps to RR-2027-0052; PII-leakage detection on prompt pre-scan maps to RR-2027-0054.

**§11.2 Evaluations not run (at this release) and the governance-side justification.** From the input — adversarial-prompt stress test against the safety-instructions block; multilingual-input handling; jailbreak-prompt refusal on pediatric-diagnosis requests. For each, state the governance-side position: *which register entry would be the target of the eval, what the current compensating control is, when it is scheduled to run.* A not-run eval without a compensating-control and scheduling note is a §11 finding.

**§11.3 Red-team findings summary.** From the input — one internal pass dated 2027-02-02; three findings routed to model-card revision; two findings routed to guardrail-config update. Do not reproduce the red-team report itself — chapter 07 is explicit that Section 11 *references* the red-team findings; it does not reproduce them. Cite the pass identifier (if the enterprise maintains one; otherwise cite the date) and the routing outcome.

The public-system-card exemplars chapter 07 cites — the OpenAI system cards for GPT-4, GPT-4V, o1; the Anthropic Claude 3 model-and-system card — are useful shape references for §11; they are *hundreds of pages* because they come from large in-house safety programmes. An internal enterprise §11 is *not* that long. Chapter 07's target is 5–15 pages for the whole extension, not per section. Keep §11 to roughly one page.

### Step 5 — Fill §12 Change-Management Triggers (15 min)

Chapter 07 names §12 as analyst-authored from the enterprise change-management policy plus the register-entry change triggers. The composition manifest (input 2) supplies the full platform-team-registered trigger list. Author §12 as a table with four columns: *trigger*, *who detects it* (platform team / vendor-watch / incident response / eval-run), *who routes it* (analyst / platform team / ML team), *regeneration scope* (model card re-rev, system-card re-rev, canonical-impact-assessment re-rev, downstream regulator-view re-rev).

Six to eight rows cover the composition-manifest-named triggers plus the analyst-added ones:

| Trigger | Detected by | Routed by | Regeneration scope |
|---|---|---|---|
| Base-model version change by Vendor V | Vendor-watch | Analyst | Model card, system card, canonical impact assessment |
| Prompt-template major rev (v1.0 → v2.0) | Platform team | Analyst | Model card, system card |
| Retrieval-index scope expansion (any corpus beyond enterprise imaging-report corpus, including pediatric imaging added) | Platform team | Analyst | System card (§10 and §11 if coverage changes); canonical impact assessment; model card §2 (intended use) and §8 (ethical considerations) |
| Guardrail configuration change (GR-2027-0005 or GR-2027-0006) | Platform team | Analyst | System card §10 and §11 |
| Tool-inventory change (any tool added) | Platform team | Analyst | System card §10; model card §2; canonical impact assessment |
| Incident mapped to RR-2027-0051 through -0054 | Incident response (IR-2027-0005) | Analyst | Model card §8; system card §11; canonical impact assessment; monitoring dashboard |
| Eval-report template rev (EV-2027-0028 moves to v1.3 or later) | ML team | Analyst | Model card §4; system card §11 |

The *retrieval-index scope expansion* row is the chapter-07 load-bearing row — a scope change there can shift the FRIA-relevant risk without any change to the model. The regeneration-scope column must therefore include the canonical impact assessment (not just the system card), or §12 has under-estimated the propagation.

### Step 6 — Cross-check the extension (10 min)

Walk the extension top-to-bottom and verify:

- **Nothing is duplicated from the model card.** §10 refers to *composition* (prompts, retrieval, tools, guardrails, orchestration, deployment surface); it does not re-state Mitchell section 1 (Model Details), section 2 (Intended Use beyond the deployment-context narrative), or section 7 (Quantitative Analyses). Duplicating any of these is the chapter-07 anti-pattern.
- **§11 references rather than reproduces the eval report and the red-team report.** If §11 contains a table of per-eval numbers, it has crossed into the eval report; cite and remove.
- **§12 lists at least one trigger that forces a canonical-impact-assessment re-rev.** Chapter 07's whole argument is that a composition-layer change can shift the FRIA-relevant risk; §12 has to make that visible by routing at least one trigger upstream to the canonical document.
- **The cross-reference block names a citation-back obligation.** Chapter 08's one-way-reference discipline: the new system card SC-2027-0019 must be cited back from MC-2027-0019 and CDX-2027-0033. §10 is only complete when that back-citation is pending-or-filed.
- **The whole file sits under roughly 1,200 words** (chapter 07's size target for an internal system card is 5–15 pages; §10–§12 is a subset of that).

### Step 7 — Self-check (5 min)

Final pass. Verify:

- Every composition-layer row in §10.1 has a pin (version string, file identifier, or dated manifest reference). Under-specified pins are logged as findings at the foot of §10.1.
- Every not-run eval in §11.2 has a compensating-control note and a scheduling note. A not-run eval with neither is a §11 finding.
- Every trigger in §12 names *who detects it*. A trigger that lists *who routes it* without a detector has an orphaned left-hand-side — if the detector is "no one yet", that is itself a §12 finding (the trigger exists only on paper).
- The file's title cites `SC-2027-0019` by identifier, not by name.
- Fabricated owner names (if any) are flagged in a Fabrication note at the bottom.

## Expected output

One markdown file in `~/aicg-labs/mod-105-lab-03/`:

- `system-card-extension.md` — cross-reference block plus §10 / §11 / §12.

Total length: roughly 800–1,500 words. A reviewer should be able to read it in ten minutes alongside the model card and see the deployment composition, the safety-eval coverage, and the change-trigger routing without ambiguity.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did you resist duplicating the model card?** If §10's deployment-context narrative re-states Mitchell section 2's intended-use language verbatim, the extension has recreated the model card on a larger page. Chapter 07's rule is that §10–§12 *sit alongside* the Mitchell nine, not inside them.
2. **Does §12 route at least one trigger to the canonical impact assessment?** Chapter 07's load-bearing claim is that a composition-layer change can shift the FRIA-relevant risk without any change to the model. A §12 whose triggers all stop at the model card or the system card has missed the chapter's whole point.
3. **Is §11 a reference set rather than an evidence set?** If §11 contains per-eval numeric results, it has crossed into eval-report content. Cite and remove.
4. **Did you flag under-specified pins?** Chapter 06's version-pin discipline is the same test applied to §10.1 — a row without a pin is under-specified.
5. **Is the file within chapter 07's size envelope?** An internal system card is 5–15 pages total; §10–§12 is only part of that. If the extension is 3,000 words, it has absorbed content that belongs elsewhere.

If any of the five is "no", revise *that section* before considering the lab done.

## Why this is a lab, not an exercise

Exercise 05 covers the Mitchell nine-section model card (chapter 06) end-to-end. Exercise 06 covers the Gebru datasheet (the datasheet half of chapter 07) end-to-end. Neither exercise exercises the chapter-07 *system-card extension* — the three extra sections that chapter 07 says internal enterprise system cards add on top of the Mitchell shape to describe the composition, the safety-evaluation coverage, and the change-management triggers.

This lab's inverted shape — a fixed model card plus a fixed composition manifest, with the analyst authoring only the extension that sits on top — matches the real-world shape of the task. The platform team supplies the composition manifest; the ML / safety team supplies the eval-coverage lines; the analyst reads both, structures the extension, and routes the change-management triggers into the canonical-document re-rev cadence. A lab is the correct shape because the learning objective is *integration* across three input sources (model card, composition manifest, register) into one supplementary artefact — not single-artefact authoring from scratch, which is what the exercises drill.
