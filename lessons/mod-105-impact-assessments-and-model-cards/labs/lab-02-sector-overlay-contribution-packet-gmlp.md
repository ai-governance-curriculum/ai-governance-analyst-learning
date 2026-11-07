# Lab 02 — Sector-Overlay Contribution Packet for an FDA / GMLP Device

**Duration:** 2 hours.
**Grounding chapters:** [01](../01-iso-42005-scaffold-and-shared-template.md), [05](../05-sector-specific-impact-assessment-fda-gmlp.md), [06](../06-model-cards-mitchell-hf-mct.md), [08](../08-cross-referencing-artefacts-and-walk-discipline.md).
**Difficulty:** Core — exercises chapter 05, which has no paired exercise in the module.

## Objective

For a fixed MCDA-Radiology use case — a draft-radiology-report assistant assembled from a hosted foundation model with retrieval-augmented grounding, which [chapter 05](../05-sector-specific-impact-assessment-fda-gmlp.md) walks as a candidate software-as-a-medical-device (SaMD) submission — author a **governance-side contribution packet** that the enterprise's regulatory-affairs team folds into an FDA pre-market submission. Produce a single `gmlp-contribution-packet.md` artefact that maps onto the chapter 05 contribution-packet table, names every analyst / regulatory-affairs boundary honestly, and references rather than duplicates the ISO 14971 risk-management file.

The lab exists because chapter 05 is the one chapter in the module with no paired exercise — the exercises each drill a horizontal instrument (AIA, FRIA, DPIA) or a card (model card, datasheet); none drill the horizontal-plus-vertical pattern that defines a sector overlay. The lab's inverted shape — a *contribution packet* rather than a submission — is deliberate: the analyst's product is not the regulatory submission itself but the governance-side input the submission reuses.

## Prerequisites

- Chapter 05 read; the ten GMLP guiding principles, the pre-market-submission-element-to-42005 mapping, and the analyst / regulatory-affairs boundary fresh in memory.
- Chapter 01 read (the 42005 canonical document shape) and exercise 01 completed — the contribution packet reads from a canonical document, not from a blank slate.
- Chapter 06 skimmed — the packet's transparency contribution cites a model card.
- The joint [FDA / Health Canada / MHRA GMLP guiding principles](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) page open as the shape reference.
- Optional: the FDA [Transparency for Machine Learning-Enabled Medical Devices: Guiding Principles (2024)](https://www.fda.gov/medical-devices/software-medical-device-samd/transparency-machine-learning-enabled-medical-devices-guiding-principles) and the joint [Predetermined Change Control Plans for Machine Learning-Enabled Medical Devices: Guiding Principles (2023)](https://www.fda.gov/medical-devices/software-medical-device-samd/predetermined-change-control-plans-machine-learning-enabled-medical-devices) pages open.
- A markdown editor. No submission tooling — the deliverable is governance-side.

## The fixed input — MCDA-Radiology

Use *exactly* this input. Do not substitute the use case or re-tier the device; chapter 05's framing attaches to this specific intended use and no other.

> **Device concept.** MCDA-Radiology — a draft-radiology-report assistant for internal radiologist use in a US hospital system. Hosted foundation model from Vendor V, called from an internal web tool integrated with the radiologist's PACS workstation.
>
> **Intended use.** Assistive drafting of radiology reports for review by a board-certified radiologist prior to sign-off. Not intended for use as an autonomous diagnostic tool. Not intended for use in pediatric imaging — out-of-scope population.
>
> **Model family.** Hosted foundation model (Vendor V, model version 2026-01). Retrieval-augmented on the enterprise's imaging-report corpus. Prompt template v1.0.
>
> **Deployment context.** US hospital system; US regulatory scope (FDA is the sector regulator in scope). No EU deployment at first release — the FRIA / DPIA are not in scope for this lab. The analyst has already authored a 42005-shaped canonical document for the system — CDX-2027-0033 — and populated register entries RR-2027-0051 through RR-2027-0054 covering confabulation, differential performance across patient sex / age band / imaging modality, over-reliance by the radiologist, and label-and-instructions-for-use mis-interpretation.
>
> **Related artefacts already on disk (fabricated identifiers for lab use).**
>
> - Inventory row INV-2027-0012.
> - Canonical impact assessment CDX-2027-0033.
> - Register entries RR-2027-0051 through RR-2027-0054.
> - Bias-review note BR-2027-0007 (per `mod-104`), covering performance by patient sex, age band, and imaging modality.
> - Model card MC-2027-0019 (enterprise supplement to Vendor V's card MC-2027-0019-Vendor).
> - Eval report EV-2027-0028 (clinical-performance eval slice).
> - Incident-response plan IR-2027-0005.
> - Monitoring dashboard MON-2027-0011.
>
> **Related artefacts *not* on disk (owned elsewhere, referenced only).**
>
> - ISO 14971 risk-management file — regulatory-affairs / quality scope.
> - Clinical-performance evaluation and statistical inference — biostatistics and clinical-evaluation scope.
> - Predetermined change control plan — regulatory-affairs plus ML engineering scope.
> - Device labelling regulatory language — regulatory-affairs plus legal scope.

All names, identifiers, and version strings above are illustrative. Treat the input as given. Do not pre-produce the ISO 14971 file or the clinical-performance analysis — chapter 05's boundary is that those are *not* the analyst's artefacts, and the lab tests the boundary as much as it tests the packet.

## Steps

### Step 1 — Scaffold the packet (10 min)

Create the working folder and file.

```bash
mkdir -p ~/aicg-labs/mod-105-lab-02
cd ~/aicg-labs/mod-105-lab-02
touch gmlp-contribution-packet.md
```

Open the file and lay in the section headers up front — these mirror chapter 05's contribution-packet table one-for-one:

```markdown
# GMLP contribution packet — MCDA-Radiology

Analyst: <your-name>
Date: <today>
Canonical impact assessment: CDX-2027-0033
Inventory row: INV-2027-0012
Target submission team: regulatory affairs
Target submission type: (to be confirmed by regulatory affairs — candidate 510(k) / De Novo)

## 1. Cross-reference block
## 2. Indications for use
## 3. Device description (governance view)
## 4. Human-AI team performance framing (Principle 7)
## 5. Sub-group performance framing (Principles 3 and 8)
## 6. Post-market monitoring intent (Principle 10)
## 7. Predetermined change control intent
## 8. Transparency contribution (Principle 9)
## 9. Explicit non-contributions — what regulatory affairs owns
## 10. Hand-off note
```

The *explicit non-contributions* section (9) is load-bearing. Chapter 05's "Where the sector-specific IA stops for the analyst" is the exact content of that section and keeps the packet inside the analyst-tier boundary.

### Step 2 — Fill section 1: cross-reference block (5 min)

Reproduce the chapter 08 cross-reference block for MCDA-Radiology. Pull the identifiers from the fixed input:

```
System: MCDA-Radiology
Inventory row: INV-2027-0012
Canonical impact assessment: CDX-2027-0033
Register entries: RR-2027-0051, RR-2027-0052, RR-2027-0053, RR-2027-0054
Bias-review note: BR-2027-0007
Model card: MC-2027-0019 (enterprise supplement to Vendor V card MC-2027-0019-Vendor)
Eval report: EV-2027-0028
Incident-response plan: IR-2027-0005
Monitoring dashboard: MON-2027-0011
Regulatory affairs point of contact: <named — flag as fabricated>
Submission type (regulatory affairs confirms): <to be confirmed>
```

The cross-reference block is the contract that the packet reads *from* and *into* a stable corpus — if regulatory affairs refers a question back to the packet six months from now, the block is the first thing they walk.

### Step 3 — Fill section 2: indications for use (10 min)

Open chapter 05 in a second window. The *indications for use / intended use* element aligns with the 42005 *system description* + *affected-stakeholder inventory*. Pull both from CDX-2027-0033 (per the fixed input; author the content as the chapter-05 example narrates):

- The *for whom* clause — board-certified radiologists in the US hospital system.
- The *for what condition* / *in what setting* clause — assistive drafting prior to the radiologist's sign-off; the sign-off is the medical decision.
- The *not-for* clause — not an autonomous diagnostic tool; not for pediatric imaging.

Two tripwires chapter 05 is specific about:

- The *not-for* clause is the sector-regulator-legible version of the model card's *out-of-scope use cases* field. Chapter 06 names that field as under-populated in first drafts. The analyst-tier discipline is to populate it here fully — regulatory affairs will quote it into the submission's intended-use statement verbatim.
- The intended-use statement is *not* a marketing claim. If the sentence reads as *MCDA-Radiology accelerates radiology throughput by…*, it is marketing copy and will fail submission review; chapter 05's framing is a devices-regulator-legible statement of use.

### Step 4 — Fill section 3: device description (governance view) (10 min)

Chapter 05's row: *device description (from a governance angle)* aligns with 42005 *system description* + *data description*. Author the governance-side device description. Three to five bullets on:

- Model family and version pin (hosted foundation model MCDA-Radiology-v1; Vendor V model version 2026-01; prompt template v1.0).
- Inputs (DICOM report metadata plus prior-report retrieval on the enterprise imaging-report corpus).
- Outputs (draft report text for radiologist review).
- Log and retention (prompt-plus-output pairs stored per enterprise retention policy; cross-reference the enterprise records schedule).
- Dependency pins (Vendor V card by URL and version; model card supplement MC-2027-0019; eval report EV-2027-0028).

Chapter 05's discipline: this is the *governance-side* device description. The regulatory-affairs team writes the device description in the submission itself — including the clinical-engineering content and the quality-system references — which the analyst does not duplicate. Keep this to the pieces the governance function owns.

### Step 5 — Fill section 4: human-AI team performance framing (Principle 7) (15 min)

Principle 7 reads: *focus is placed on the performance of the human-AI team*. Chapter 05 maps this row to the 42005 *treatment plan (oversight controls)* section. Author three to four bullets:

- Every draft is edited by a board-certified radiologist before sign-off.
- Sign-off is the medical decision; the draft is not the decision.
- Monitoring of edit-distance / radiologist-flagged-inaccuracy rate per `MON-2027-0011`; threshold at which the Human-AI team is flagged as under-performing is named.
- Over-reliance register entry RR-2027-0053 is cited with its mitigation summary.

The failure mode chapter 05 is implicitly warning against: writing Principle 7 as *the radiologist reviews the draft* and stopping there. That is an *oversight asserted*, not an *oversight implemented*. The chapter asks for the mechanism — who reviews, at what moment, with what evidence of the review happening.

### Step 6 — Fill section 5: sub-group performance framing (Principles 3 and 8) (15 min)

Chapter 05 row: *sub-group performance framing (Principle 3, 8)* aligns with the 42005 *enumerated impacts* section plus a reference to the bias-review note from `mod-104`. Author the content:

- Sub-groups in scope — patient sex, age band, and imaging modality (per BR-2027-0007; name explicitly which sub-groups the bias-review covered).
- The register entry RR-2027-0052 (differential performance across these strata) is cited with its inherent and residual claim.
- A recommendation routed to regulatory affairs — chapter 05's example line is *contribution recommends the regulatory-affairs team add clinical-performance evaluation across the same strata*. Reproduce that routing verbatim as the analyst-tier handshake.
- A note that the clinical-performance evaluation itself — the statistical inference on the clinical-performance-eval slice — is *not* the analyst's artefact. Cite EV-2027-0028 as the eval-report input; name the clinical-evaluation team (owner-tier handshake) as the owner of the clinical-performance evidence.

Chapter 05's **sub-group framing is a governance-side framing**. The analyst does not state a clinical-performance conclusion; the analyst states the governance expectation that clinical-performance evidence must be produced across the same strata the bias-review note covered. This is where the two teams meet.

### Step 7 — Fill section 6: post-market monitoring intent (Principle 10) (10 min)

Principle 10 reads: *deployed models are monitored for performance and re-training risks are managed*. Chapter 05 maps this to 42005 *review triggers and cadence*. Author:

- Monthly review of draft-edit-distance and radiologist-flagged-inaccuracy rate.
- Quarterly re-baseline against a held-out set.
- Incident-response plan IR-2027-0005 is cited as the mechanism for a serious performance degradation.
- Review-cadence integration with the canonical document's *review triggers and cadence* section — the trigger set is the same list; the monitoring dashboard is the live surface.

Chapter 05's distinction: the post-market monitoring *intent* goes into the contribution packet; the post-market-surveillance *plan itself* is the regulatory-affairs artefact. The analyst records the governance-side commitment; regulatory affairs assembles the plan.

### Step 8 — Fill section 7: predetermined change control intent (10 min)

Chapter 05's row: *predetermined change control plan intent* aligns with the 42005 *review triggers and cadence* plus change-management controls. Author:

- Triggers that force a review of the deployed configuration — base-model version change by Vendor V; prompt-template major rev; retrieval-index scope expansion; guardrail configuration change; any confabulation-rate alert above threshold.
- The joint [Predetermined Change Control Plans for Machine Learning-Enabled Medical Devices: Guiding Principles (2023)](https://www.fda.gov/medical-devices/software-medical-device-samd/predetermined-change-control-plans-machine-learning-enabled-medical-devices) is cited by title.

Chapter 05's bright-line boundary: the *plan itself* — the predetermined-change-control-plan mechanics — is a regulatory-affairs plus ML-engineering artefact. The packet records the *intent* (what the governance function expects the plan to cover); the plan is written elsewhere. Any ten-bullet attempt at a full PCCP in this section has crossed the boundary.

### Step 9 — Fill section 8: transparency contribution (Principle 9) (10 min)

Chapter 05's row: *transparency / instructions-for-use content (Principle 9)* aligns with the related-artefact reference to the model card. Author:

- Reference model card MC-2027-0019 and the Vendor V base card MC-2027-0019-Vendor.
- Name the model card's ethical-considerations and intended-use sections as the specific hooks the submission's labelling draws from.
- Reference the FDA [Transparency for Machine Learning-Enabled Medical Devices: Guiding Principles (2024)](https://www.fda.gov/medical-devices/software-medical-device-samd/transparency-machine-learning-enabled-medical-devices-guiding-principles) by title as the shape reference Principle 9 was extended by.
- Explicitly route the *clinician-facing instructions-for-use regulatory language* to regulatory affairs plus legal. The analyst's transparency contribution is the governance artefact set; the regulatory language is not.

### Step 10 — Fill section 9: explicit non-contributions (10 min)

Chapter 05's "Where the sector-specific IA stops for the analyst" and the "gaps the analyst does *not* fill on the sector view" list is the exact content of section 9. Author it as a short enumerated list:

- **ISO 14971 risk-management file** — regulatory affairs / quality own. The packet references but does not reproduce.
- **Clinical performance analysis and statistical inference** — biostatistics and clinical-evaluation own.
- **Predetermined change control plan mechanics** — regulatory affairs plus ML engineering own.
- **Device labelling regulatory language** — regulatory affairs plus legal own.
- **The regulatory submission itself (510(k) / De Novo / PMA)** — regulatory affairs assembles and files.

Each non-contribution lists the owner it routes to. Chapter 05's failure mode is the analyst who produces a full-looking packet that silently recreates the ISO 14971 file — a harm because now the enterprise has two drifting risk-management artefacts where it should have one, and the audit-facing risk-management artefact is the ISO 14971 file, not the packet.

### Step 11 — Fill section 10: hand-off note (5 min)

One paragraph, four to six sentences, in a plain prose shape: the analyst hands this packet to regulatory affairs as one input to the pre-market submission; the canonical document CDX-2027-0033 is retained as the enterprise's internal source-of-truth; regulatory affairs confirms the submission type (510(k) / De Novo) and folds the packet into the submission alongside the ISO 14971 file, the clinical-performance evidence, the labelling, and the predetermined-change-control-plan; the analyst remains the coordination point for any updates to the packet as the canonical document revises. Name the regulatory-affairs point of contact (fabricated — flag the fabrication).

### Step 12 — Cross-check against chapter 05's mapping table (5 min)

Walk the chapter-05 mapping table against your packet sections 2–8:

| Chapter 05 element | Your section | Sourced-from check |
|---|---|---|
| Indications for use / intended use | §2 | Reads from CDX-2027-0033 system description + stakeholder inventory |
| Device description (governance view) | §3 | Reads from CDX-2027-0033 system description + data description |
| Human-AI team framing (P7) | §4 | Reads from CDX-2027-0033 treatment plan (oversight controls) |
| Sub-group framing (P3, P8) | §5 | Reads from CDX-2027-0033 enumerated impacts + BR-2027-0007 |
| Post-market monitoring intent (P10) | §6 | Reads from CDX-2027-0033 review triggers and cadence |
| Predetermined change control intent | §7 | Reads from CDX-2027-0033 review triggers + change controls |
| Transparency (P9) | §8 | Reads from model card MC-2027-0019 |

Any row with a *your section* that does not read from the chapter-05-mapped canonical source is a drift. Revise before submission to regulatory affairs.

### Step 13 — Self-check (5 min)

Walk the packet top-to-bottom and verify:

- No fabricated GMLP principle wording. The chapter 05 paraphrases are the reference shape; fabricated verbatim quotations are a tripwire.
- No clinical-performance claim in sections 4–8. The analyst is not the clinical evaluator; the packet names which clinical-performance evidence is expected but does not produce it.
- No ISO 14971 content. If section 4 is reading like a *harm / hazard / preventive measure* table, chapter 05's boundary has been crossed.
- Every artefact ID from the fixed input is cited in the packet at least once. The packet is a *reading* of the canonical corpus into the sector-regulator-legible shape; dropping an artefact silently is a drift from chapter 08's cross-reference discipline.
- The explicit non-contributions section (9) names at least the four non-contributions chapter 05 lists. A fifth or sixth that the analyst defensibly argues is also-not-mine is a bonus, not a required addition.
- Fabricated owner names are flagged in a Fabrication note at the bottom.

## Expected output

One markdown file in `~/aicg-labs/mod-105-lab-02/`:

- `gmlp-contribution-packet.md` — ten populated sections, one timestamp, one named analyst, one named regulatory-affairs point of contact (fabricated — flagged).

Total length: roughly 1,500–2,500 words. Regulatory affairs should be able to read it in fifteen minutes and either fold it into their submission draft or push back on specific sections.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did sections 2–8 read *from* the canonical document rather than re-authoring it?** Chapter 05's packet is a re-projection of CDX-2027-0033 into a sector-legible shape, not a second canonical document. If section 3 contains facts that are not in the canonical document, either the canonical document is incomplete (open a revision request) or the packet has fabricated content.
2. **Did section 9 name at least four non-contributions and route each to its owner?** Chapter 05's bright-line boundary is that regulatory affairs owns the submission, the ISO 14971 file, clinical-performance analysis, the PCCP mechanics, and the labelling. A section 9 that names only one or two of these is under-populated.
3. **Did you keep Principle 7 as an *oversight implemented*, not an *oversight asserted*?** If section 4 reads as *the radiologist reviews the draft* and stops, the mechanism (who, when, how evidenced) is missing.
4. **Did you resist producing the ISO 14971 file?** A packet that silently contains *hazard — foreseeable misuse — preventive measure — residual-risk-after-measure* tables has imported ISO 14971 content; chapter 05 is explicit that the file is not the analyst's.
5. **Is the submission-type field marked *to be confirmed by regulatory affairs*?** Chapter 05's division of labour is that regulatory affairs decides submission type (510(k) / De Novo / PMA) — not the analyst. If section 1 claims a submission type as fact, the packet has assumed a regulatory-affairs decision.

If any of the five is "no", revise *that section* before considering the lab done.

## Why this is a lab, not an exercise

The module's six exercises each drill either a horizontal instrument (AIA, FRIA, DPIA) or a card (model card, datasheet). There is no exercise for chapter 05 — the sector overlay is not practised at exercise depth. That leaves a specific authoring muscle undeveloped: the analyst who can produce a horizontal impact-assessment view confidently but who, on a sector-regulated use case, either over-produces a submission the analyst does not own (crossing into regulatory-affairs scope) or under-produces a sketch the specialist team cannot reuse.

This lab makes the muscle explicit. A fixed input, a packet that maps one-for-one onto chapter 05's contribution-packet table, and a load-bearing non-contributions section that names the boundary at the end. The lab passes when the specialist team can lift the packet into their submission draft without re-doing the governance-side work — and when the audit, three years on, can see one 42005-shaped canonical source-of-truth for the device, not two drifting copies of the risk-management content.
