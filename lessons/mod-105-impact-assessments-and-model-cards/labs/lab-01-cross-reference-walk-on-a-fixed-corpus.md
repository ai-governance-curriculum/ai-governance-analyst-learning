# Lab 01 — Cross-Reference Walk on a Fixed Corpus

**Duration:** 2 hours.
**Grounding chapters:** [01](../01-iso-42005-scaffold-and-shared-template.md), [06](../06-model-cards-mitchell-hf-mct.md), [07](../07-system-cards-and-datasheets.md), [08](../08-cross-referencing-artefacts-and-walk-discipline.md).
**Difficulty:** Core — exercises chapter 08's discipline, which the module's six exercises do not directly drill.

## Objective

Take a *fixed, pre-assembled* MCDA governance corpus — inventory row, register entries, canonical impact assessment, model card, system card, datasheets, eval report, incident-response plan, monitoring dashboard — and run the six walks from [chapter 08](../08-cross-referencing-artefacts-and-walk-discipline.md), hunting for the six failure modes the chapter enumerates. Produce a single `walk-log.md` artefact that reads like the audit-facing output of a quarterly tier-1 cross-reference walk: each walk start-point, the chain followed, the drift found, and the corrective action routed.

The six module exercises each drill a single chapter's authoring mechanics (template, AIA, FRIA, DPIA, model card, datasheet). None of them tests the *reading-across* discipline that [chapter 08](../08-cross-referencing-artefacts-and-walk-discipline.md) frames as the analyst's standing obligation. This lab is the inverted shape — a corpus has already been authored; the analyst walks it.

## Prerequisites

- All eight chapters read; chapter 08's six walks, six failure modes, and walk cadence fresh in memory.
- A markdown editor; no Python or GRC-platform tooling required — the corpus below is a Markdown-only stand-in for the records that would live in the GRC platform in production.
- Exercise 01 completed, or at minimum skimmed, so the canonical-document shape is familiar. The lab's corpus is written to that shape.

## The fixed input — a deliberately drifted MCDA corpus

Use *exactly* this corpus. Do not substitute artefacts and do not pre-correct the drift — the drift is the point. Each artefact below is reproduced only at the level of its cross-reference block plus the fields a walker reads from. Numbers and identifiers are illustrative; treat the whole block as `pedagogic example — numbers illustrative`.

### A. Inventory row — INV-2026-0088

```
System: MCDA (Marketing Copy Draft Assistant)
Tier tag: Tier 2 (medium)
Owner: Marketing Ops
Related register entries: RR-2026-0212, RR-2026-0213, RR-2026-0214, RR-2026-0215
Canonical impact assessment: CDX-2026-0198
Model card: MC-2026-0044 (enterprise supplement)
System card: SC-2026-0044
Datasheets: DS-2026-0071
Bias-review note: BR-2026-0117
Eval reports: EV-2026-0091
Vendor reviews: VR-2026-0044, VR-2026-0031
Incident-response plan: IR-2026-0011
Monitoring dashboard: MON-2026-0055
```

### B. Register entries

```
RR-2026-0212 — confabulation of product facts
    Source inventory: INV-2026-0088
    Canonical impact assessment: CDX-2026-0198
    NIST MAP: MAP 5.1
    Current residual: Medium
    Last revised: 2026-07-02

RR-2026-0213 — brand-voice homogenisation
    Source inventory: INV-2026-0088
    Canonical impact assessment: CDX-2026-0198
    NIST MAP: MAP 5.1
    Current residual: Low
    Last revised: 2026-05-14

RR-2026-0214 — IP contamination
    Source inventory: INV-2026-0088
    Canonical impact assessment: (not populated)
    NIST MAP: MAP 5.1
    Current residual: Medium
    Last revised: 2026-06-20

RR-2026-0215 — data leakage in prompts
    Source inventory: INV-2026-0088
    Canonical impact assessment: CDX-2026-0198
    NIST MAP: MAP 5.1
    Current residual: Low
    Last revised: 2026-06-20
```

### C. Canonical impact assessment — CDX-2026-0198 (v2, 2026-08-01)

```
System: MCDA
Inventory row: INV-2026-0088
Register entries read from: RR-2026-0212, RR-2026-0213, RR-2026-0215
Regulator views: (none — internal-only system)
Model card: MC-2026-0044
System card: see MCDA system card
Datasheets: DS-2026-0071
Bias-review note: BR-2026-0117
Eval reports: EV-2026-0091 (template rev v1.4)
Vendor reviews: VR-2026-0044, VR-2026-0031
Incident-response plan: IR-2026-0011
Monitoring dashboard: MON-2026-0055
Review cadence: annual (Tier 2); ad-hoc on vendor-version change, prompt-template >= v2.0, incident, scope expansion.
```

### D. Model card — MC-2026-0044 (enterprise supplement, 2026-06-15)

```
System: MCDA
Vendor base card: MC-2026-0044-Vendor (Vendor V, model version 2024-06)
Inventory row: INV-2026-0088
Canonical impact assessment: CDX-2026-0198
Register entries read from: RR-2026-0212, RR-2026-0213, RR-2026-0214, RR-2026-0215
Datasheets cited: DS-2026-0071
Eval reports cited: EV-2026-0091 (template rev v1.3)
Bias-review note: BR-2026-0117
Regeneration triggers: vendor version change, prompt-template major rev, incident logged
```

### E. System card — SC-2026-0044 (2026-06-15)

```
System: MCDA
Extends: MC-2026-0044
Inventory row: INV-2026-0088
Canonical impact assessment: CDX-2026-0198
Composition inventory (§10): prompt template v1.4; retrieval index DS-2026-0071; tool inventory (none); guardrail configuration GR-2026-0012.
Safety evaluation coverage (§11): see eval report EV-2026-0091 and red-team summary.
Change-management triggers (§12): vendor version change, prompt-template major rev, tool-inventory change, guardrail configuration change, incident.
```

### F. Datasheet — DS-2026-0071 (2026-02-10)

```
Dataset: MCDA retrieval index (past-campaign corpus)
Consumers (model cards citing this datasheet): MC-2026-0044
Collection Process: no personal data; Marketing Ops approval; see Collection Process §3.
Maintenance: monthly refresh.
```

### G. Bias-review note — BR-2026-0117 (2026-07-21)

```
System: MCDA
Inventory row: INV-2026-0088
Register entries referenced: RR-2026-0213 (brand-voice-homogenisation reading)
Model card consumer: MC-2026-0044 (ethical-considerations section cites this note)
```

### H. Eval report — EV-2026-0091 (template rev v1.4; 2026-07-10)

```
System: MCDA
Inventory row: INV-2026-0088
Prior template rev: v1.3 (superseded 2026-07-10)
Consumers: MC-2026-0044; SC-2026-0044.
Metrics claims: confabulation-on-eval-set; brand-voice-drift; PII-leakage detection on prompt pre-scan.
```

### I. Incident-response plan — IR-2026-0011

```
System: MCDA
Inventory row: INV-2026-0088
Register entries mapped: RR-2026-0212, RR-2026-0213, RR-2026-0214, RR-2026-0215
Open incidents: IR-2026-0011-INC-0003 (opened 2026-09-02, status: investigation open)
    Maps to register entry: RR-2026-0212 (confabulation of product facts)
    Canonical impact assessment reference: CDX-2026-0198
    Model card revision requested: see the model card's ethical-considerations section.
```

### J. Monitoring dashboard — MON-2026-0055

```
System: MCDA
Inventory row: INV-2026-0088
Alerts active: confabulation-rate above threshold (2026-08-29); references "the eval report" without identifier.
```

## Steps

### Step 1 — Scaffold the walk log (10 min)

Create the working folder and file.

```bash
mkdir -p ~/aicg-labs/mod-105-lab-01
cd ~/aicg-labs/mod-105-lab-01
touch walk-log.md
```

Open `walk-log.md` and lay in the section headers up front:

```markdown
# MCDA cross-reference walk log — quarterly Tier-2 walk

Walker: <your-name>
Walk date: <today>
System: MCDA (INV-2026-0088)
Scope: six walks per chapter 08; six failure modes per chapter 08.

## 1. Walk one — from the inventory row to everything
## 2. Walk two — from a register entry to the canonical impact assessment
## 3. Walk three — from the canonical impact assessment to the regulator views
## 4. Walk four — from the model card to the risk register
## 5. Walk five — from the eval report to everywhere it is cited
## 6. Walk six — from an incident to the artefacts affected
## 7. Failure-mode summary
## 8. Corrective-action tickets
## 9. Walk verdict
```

The nine-section scaffold is the audit answer to *did you keep the corpus consistent?*. The verdict at the end is the one-line record a reviewer reads first; everything above it is the evidence.

### Step 2 — Walk one: from the inventory row to everything (10 min)

Open [chapter 08](../08-cross-referencing-artefacts-and-walk-discipline.md) in a second window and keep its "Six walks the reader must be able to perform" list visible.

For walk one, start at `INV-2026-0088` (block A). The row lists ten downstream artefact identifiers. Produce a sub-table with four columns: *artefact ID*, *pulled from the corpus?* (yes / no), *cross-reference back to INV-2026-0088?* (yes / no), *finding*. Every row with a *no* in either of the middle columns is a finding and is logged.

Specifically check: does every artefact's cross-reference block cite `INV-2026-0088` as the inventory row? Chapter 08's **one-way-reference** failure mode fires when A cites B but B does not cite A.

Chapter 08's hint: *when a new artefact is authored, every referenced artefact is updated to cite it back* — the walk is the mechanical check that this happened.

### Step 3 — Walk two: from a register entry to the canonical impact assessment (10 min)

Start at each of RR-2026-0212, RR-2026-0213, RR-2026-0214, RR-2026-0215 in block B. Each entry names a canonical impact assessment in its cross-reference block. Walk from the entry to `CDX-2026-0198` (block C) and confirm:

- The canonical document's *enumerated impacts* read-from list cites this register entry.
- If the register entry's *canonical impact assessment* field is empty, that is a finding (**dangling reference** / **verbal-only reference**).
- If the canonical document names a register entry that does not exist in block B, that is a finding.
- If the register entry cites the canonical document but the canonical document does not cite the entry back, that is a **one-way-reference** finding.

Log each walk as a sub-section. Tag each finding with the failure-mode name from chapter 08.

### Step 4 — Walk three: from the canonical impact assessment to the regulator views (5 min)

Start at `CDX-2026-0198` (block C). Chapter 01 says MCDA is an internal-only system — no AIA, FRIA, DPIA, or sector views apply. Chapter 08's walk-three answer in that case is: *no regulator view exists; the canonical document explicitly records that none applies*. Confirm the canonical document's *Regulator views* field says exactly that; if the field is missing or silent, log the finding.

If the canonical document ever sprouts a regulator view later, this is the walk that catches a missing filing date.

### Step 5 — Walk four: from the model card to the risk register (10 min)

Start at `MC-2026-0044` (block D). The model card's *Register entries read from* field lists four entries (RR-2026-0212, -0213, -0214, -0215). For each entry, confirm the entry exists in block B and its cross-reference back to the model card is recorded.

Specific checks:

- Does the model card cite a register entry the canonical document has already dropped? `CDX-2026-0198` (block C) reads from only three of the four entries. If `MC-2026-0044` reads from a fourth that the canonical document does not, that is a drift finding — either the canonical document is incomplete or the model card is citing an entry whose canonical-document hook was lost in revision.
- Is the model card citing the eval report at the correct version? Walk-five picks this up explicitly, but note it here.

### Step 6 — Walk five: from the eval report to everywhere it is cited (10 min)

Start at `EV-2026-0091` (block H). The report is currently at template rev v1.4; its *prior template rev* field names v1.3 as superseded on 2026-07-10. Scan every artefact in the corpus that cites `EV-2026-0091` and confirm it cites the current template rev.

Specifically: the model card `MC-2026-0044` (block D) cites `EV-2026-0091 (template rev v1.3)`. The report has moved to v1.4. That is a **version drift** finding — the model card's eval-report citation is stale.

Chapter 08's cadence rule: *on every artefact revision, downstream artefacts that cite the revised one are scanned; where the revision materially changes a claim they cite, they are re-visited*. The analyst-tier question to route: has the v1.3 → v1.4 bump changed a claim the model card quotes? If yes, the model card is revised; if no, the citation is updated and the walk is logged.

### Step 7 — Walk six: from an incident to the artefacts affected (15 min)

Start at `IR-2026-0011-INC-0003` in block I (incident opened 2026-09-02; investigation open). The incident maps to `RR-2026-0212` and the canonical document `CDX-2026-0198`.

Walk the chain forward and backward:

- Backward from the incident to the register entry to the canonical document (block I → block B → block C). Each link must resolve to a current-revision artefact.
- Forward from the incident to the model card (the incident reports a *model card revision requested*). Block D is at version dated 2026-06-15; the incident is from 2026-09-02; has the model card been revised since the incident? If not, that is a finding — the chain names a request that has not been actioned.
- Sideways to the monitoring dashboard (block J). The dashboard's alert references *the eval report* without an identifier — chapter 08's **verbal-only-reference** failure mode fires exactly here. Log it; the corrective action is to re-cite the eval report by identifier (`EV-2026-0091` at the current template rev).

### Step 8 — Fill section 7: failure-mode summary (10 min)

Walk the six failure-mode names from chapter 08 and, for each, list the findings you attached to that mode across walks 1–6:

```markdown
### 7.1 Renaming drift — findings
### 7.2 Version drift — findings
### 7.3 Forked-artefact drift — findings
### 7.4 Dangling reference — findings
### 7.5 One-way reference — findings
### 7.6 Verbal-only reference — findings
```

For *this* corpus, the pre-seeded drifts a walker should at minimum surface:

- **Dangling reference / one-way reference** — `RR-2026-0214` has no canonical-impact-assessment back-reference while `MC-2026-0044` reads from it (block B shows the entry's *Canonical impact assessment* field is `not populated`; block C's *Register entries read from* list omits `RR-2026-0214`).
- **Version drift** — `MC-2026-0044` cites `EV-2026-0091 (template rev v1.3)` after the eval report moved to v1.4 (block D vs block H).
- **Verbal-only reference** — `MON-2026-0055` cites *the eval report* without an identifier (block J).
- **Dangling-request / open-loop reference** — the incident requests a model-card revision that has not landed (block I vs block D dates).

Any drift the lab's walker finds that is *not* in the pre-seeded set is either a bonus catch (log it) or a mis-read (verify by re-walking the relevant section).

Chapter 08's **forked-artefact drift** does not apply in this corpus (no external card has been rendered). **Renaming drift** does not apply either. Record *not applicable — no renamings or external renderings visible in this corpus* so the walker who reads the log later knows these were checked rather than skipped.

### Step 9 — Fill section 8: corrective-action tickets (10 min)

For each finding in section 7, produce a one-line ticket in the chapter-02-remediation-ticket shape: concrete finding, specific fix, owner routing (named — fabricate a plausible analyst / platform-team / ML-team owner if you must, and flag fabrications in a Fabrication note at the bottom of the file).

Four likely tickets for *this* corpus:

| # | Finding | Fix | Owner | Due |
|---|---|---|---|---|
| T-01 | `RR-2026-0214` not cited by `CDX-2026-0198`; `MC-2026-0044` reads from it. | Update `CDX-2026-0198` to a new revision citing `RR-2026-0214` in the enumerated-impacts section; re-walk from the register entry. | AI governance analyst | <today + 7d> |
| T-02 | `MC-2026-0044` cites `EV-2026-0091` at template rev v1.3; current rev is v1.4. | Open the eval report at v1.4; confirm no material claim quoted by the model card has changed; update the citation. If a claim changed, open a model-card revision request. | AI governance analyst | <today + 7d> |
| T-03 | `MON-2026-0055` alert references *the eval report* without identifier. | Platform team updates the monitoring configuration to cite `EV-2026-0091` at the current template rev. | GRC-platform team | <today + 14d> |
| T-04 | Incident IR-2026-0011-INC-0003 requested a model-card revision that is not yet in block D. | Confirm with the incident owner whether the revision is open; if not, close the request; if open, add the revision ETA to the incident. | Incident owner | <today + 3d> |

The **ticket is a doing, not a reading**. Chapter 08's cadence rule makes the walk itself a filed artefact — the walk log is the audit answer; the tickets are the work that closes the drift.

### Step 10 — Fill section 9: walk verdict (5 min)

One paragraph, two to four sentences, in chapter 08's walk-log shape: *walked on <date>; <N> references validated; <M> findings; corrective actions filed under T-01 through T-NN; next walk due <date per cadence>*. For MCDA (Tier 2), chapter 08 names annual cadence for medium-tier systems and quarterly for high-tier. Record the next walk date accordingly.

### Step 11 — Cross-check the walk log (5 min)

Walk the nine sections side-by-side. Every finding named in a walk section (1–6) must appear in the failure-mode summary (7) and in at least one corrective-action ticket (8). If a finding appears in walk 5 but not in section 7, the mode-tagging has drifted. If a finding appears in section 7 but has no ticket in section 8, the walker has observed drift without routing a fix — that is itself a walk-log finding.

High-tripwire fields:

- **The eval-report version-drift finding.** Named in walk 5, tagged under 7.2, fixed in T-02. All three mentions must cite the exact version delta (v1.3 → v1.4), not a paraphrase.
- **The missing register-to-canonical back-reference.** Named in walk 2 (or walk 4), tagged under 7.4 or 7.5, fixed in T-01. The ticket must name the specific register entry.
- **The verbal-only reference in the monitoring dashboard.** Named in walk 6, tagged under 7.6, fixed in T-03.

### Step 12 — Self-check (5 min)

Walk the walk log top-to-bottom and verify:

- Every finding cites the chapter 08 failure-mode name — renaming drift, version drift, forked-artefact drift, dangling reference, one-way reference, or verbal-only reference. The analyst-tier framing is that the catalogue is exactly those six.
- Every artefact ID in the corpus appears in at least one walk. If an artefact in the corpus was not walked, the Tier-2 quarterly walk is incomplete.
- No fabricated artefacts have been added (new INV-, MC-, DS-, etc. identifiers that do not appear in the input blocks). Fabricated owner names in tickets are flagged in a Fabrication note.
- The walk log is a *doing* record, not a re-authoring of the corpus. If any section rewrites the model card's intended-use section or the canonical document's enumerated impacts, the scope has drifted from chapter 08 back into chapter 06 / 01.

## Expected output

One markdown file in `~/aicg-labs/mod-105-lab-01/`:

- `walk-log.md` — nine populated sections, one timestamp, one named walker, four or more corrective-action tickets.

Total length: roughly 1,200–2,000 words. A reviewer should be able to read it in ten minutes and see every walk performed, every drift logged, every ticket routed, and the next walk date.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did you tag every finding with one of chapter 08's six failure-mode names?** If any finding is logged as "misc drift" or left untagged, the taxonomy has drifted. Revise.
2. **Did walks 1–6 all actually run?** It is tempting to skip walk 3 because MCDA has no regulator views. Chapter 08's walk-three answer in that case is still a record — *no regulator view applies; canonical document confirms this*. Not skipping the walk is the discipline the chapter asks for.
3. **Did each finding land in a ticket?** Chapter 08 names the walk as a *doing*, not a *reading*. A walk log with findings but no tickets is a partial deliverable.
4. **Did you resist re-authoring the corpus?** This lab is about *reading-across*, not about fixing the content. If section 1 of walk-log.md contains a rewritten canonical-document narrative, the scope has drifted out of chapter 08 and into chapter 01.
5. **Is the next-walk-due date present in section 9 and consistent with chapter 08's cadence by tier tag?** Tier 2 is annual; a quarterly date on a Tier-2 system is a drift from the cadence policy.

If any of the five is "no", revise *that section* before considering the lab done.

## Why this is a lab, not an exercise

The module's six exercises author the artefacts of the corpus: exercise 01 authors the canonical template and a worked example; exercise 02 authors an AIA view; exercise 03 authors a FRIA; exercise 04 authors a DPIA plus the FRIA / DPIA overlap table; exercise 05 authors a model card; exercise 06 authors a datasheet. None of them asks the analyst to *read across* a completed corpus and route the drift findings.

Chapter 08's walk discipline is the module's integration muscle — the audit answer to *did you keep the corpus consistent?* This lab exercises exactly that. The failure mode it prevents is the analyst who can author each artefact in isolation but who, three years into the role with a portfolio of thirty systems, has never once walked a corpus end-to-end to catch the drift that silently accumulates between artefact revisions. A lab is the correct shape because the learning objective is procedural (walk, log, route), not authoring (which is what the exercises drill).
