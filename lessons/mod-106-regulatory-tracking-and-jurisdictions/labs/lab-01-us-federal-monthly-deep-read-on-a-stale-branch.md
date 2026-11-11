# Lab 01 — US Federal Monthly Deep Read on a Stale Branch

**Duration:** 2 hours.
**Grounding chapters:** [01](../01-rolling-regulatory-tracker-method.md), [03](../03-us-federal-patchwork.md), [10](../10-regulatory-change-note-routing.md); AIGP tagging per [08](../08-iapp-aigp-shared-vocabulary.md).
**Difficulty:** Core — exercises the monthly deep-read cadence from chapter 01 against the US federal patchwork from chapter 03, which the module's five exercises do not directly drill.

## Objective

Take a *fixed, pre-assembled* US federal branch of the regulatory tracker — six rows with deliberately-stale last-verified dates and one row whose status is wrong as the branch sits — and run the chapter 01 monthly-deep-read cadence. For each row, verify the status against the chapter 03 content, refresh the row's columns in a `tracker-refresh.md` artefact, and — for the one row where a material change has landed — author a chapter 10 regulatory-change note (`CN-2026-LAB01-01`) routing an action list to the affected inventory-row owner.

The module's exercises drill the tracker *schema* (ex 01), crosswalks against the state and EU stacks (ex 02), Article 22 flagging (ex 03), the sector overlays (ex 04), and the change-note shape in the general case (ex 05). None of them asks the analyst to run a deep-read cadence end-to-end on a *drifted* US federal branch — the specific place where the EO overlay's refresh discipline, the joint-statement rebuttal, and the five-authorities-plus-NIST framing from chapter 03 all converge. This lab is that inverted shape — the branch has been authored and has gone stale; the analyst walks it, refreshes it, and routes the one change-note the walk surfaces.

## Prerequisites

- All ten chapters read; chapter 01's cadence (weekly / monthly / quarterly / on-demand), chapter 03's five-authorities-plus-NIST framing and dynamic EO overlay, and chapter 10's change-note structure fresh in memory.
- A markdown editor; no Python or GRC-platform tooling required — the branch below is a Markdown-only stand-in for the records that would live in the GRC platform in production.
- Exercise 01 completed, or at minimum skimmed, so the tracker schema is familiar. The branch below is written to that schema, compressed to the columns a walker reads from.

## The fixed input — a deliberately-stale US federal branch

Use *exactly* this branch. Do not substitute instruments, dates, or identifiers, and do not pre-correct the staleness — the staleness is the point. Each row is reproduced only at the level of the fields a walker reads from. Identifiers are illustrative; treat the whole block as `pedagogic example — numbers and dates illustrative`.

### A. The tracker rows

```
REG-2026-US-FED-001 — Title VII / ADA / ADEA — EEOC enforcement on AI hiring / promotion / discipline
  Status:          In force
  Last verified:   2026-05-12
  Scope trigger:   Enterprise is an employer using AI in hiring, promotion, discipline,
                   or related employment decisions affecting applicants or employees
                   in the US.
  Role:            Employer
  Affected inv:    INV-2026-HIRE-07 (ATS-AssistedRanker)
  AIGP tag:        D3
  Primary src:     https://www.eeoc.gov/joint-statement-enforcement-efforts-against-discrimination-and-bias-automated-systems

REG-2026-US-FED-002 — Section 5 FTC Act — unfair-or-deceptive practices on AI
  Status:          In force
  Last verified:   2026-05-12
  Scope trigger:   Enterprise engaged in commerce making claims about an AI product's
                   capabilities, or whose AI system causes or is likely to cause
                   substantial injury to consumers.
  Role:            Firm engaged in commerce
  Affected inv:    INV-2026-MKTG-11 (MCDA), INV-2026-SUPPORT-04 (ChatTriage)
  AIGP tag:        D3
  Primary src:     https://www.ftc.gov/legal-library/browse/statutes/federal-trade-commission-act

REG-2026-US-FED-005 — Section 1557 ACA — AI in health programmes and activities
  Status:          In force (final rule May 2024 — patient-care-decision-support provisions)
  Last verified:   2026-02-28
  Scope trigger:   Covered entity under Section 1557 using a patient-care-decision-support
                   tool, including AI/ML clinical algorithms, in a health programme or
                   activity.
  Role:            Covered entity
  Affected inv:    INV-2026-CLIN-02 (TriageAssist)
  AIGP tag:        D3
  Primary src:     https://www.federalregister.gov/documents/2024/05/06/2024-08711/nondiscrimination-in-health-programs-and-activities
  Notes:           (none)

REG-2026-US-FED-007 — FDA SaMD framework — AI-enabled medical device
  Status:          In force
  Last verified:   2026-03-30
  Scope trigger:   Enterprise manufactures or deploys an AI-enabled software meeting the
                   21 U.S.C. §321(h) device definition and intended for clinical use.
  Role:            Manufacturer (for INV-2026-CLIN-02); user facility (for
                   INV-2026-CLIN-05 as a deployed-only authorised device)
  Affected inv:    INV-2026-CLIN-02 (TriageAssist), INV-2026-CLIN-05 (PathTriage)
  AIGP tag:        D4
  Primary src:     https://www.fda.gov/medical-devices/digital-health-center-excellence/software-medical-device-samd

REG-2026-US-FED-010 — White House EO stack — currently in force
  Status:          In force — EO 14110 of 30 October 2023 (Safe, Secure, and Trustworthy
                   Development and Use of AI).
  Last verified:   2024-11-08
  Scope trigger:   Federal contractor flow-down (direct); agency enforcement priorities
                   under cited EOs (indirect).
  Role:            Federal contractor (direct); all firms (indirect)
  Affected inv:    INV-2026-GOV-03 (FedBidDraft)
  AIGP tag:        D4
  Primary src:     https://www.federalregister.gov/documents/2023/11/01/2023-24283/safe-secure-and-trustworthy-development-and-use-of-artificial-intelligence
  Notes:           Row has not been refreshed through two presidential-administration
                   transitions; review deferred pending agency-level guidance.

REG-2026-US-FED-011 — NIST AI RMF + GenAI Profile
  Status:          Guidance — voluntary; cited in enforcement
  Last verified:   2026-04-01
  Scope trigger:   All; non-binding framework the enforcement authorities cite.
  Role:            All
  Affected inv:    INV-2026-HIRE-07, INV-2026-MKTG-11, INV-2026-SUPPORT-04,
                   INV-2026-CLIN-02, INV-2026-CLIN-05, INV-2026-GOV-03
  AIGP tag:        D4
  Primary src:     https://www.nist.gov/itl/ai-risk-management-framework
```

### B. The inventory rows (affected-inventory-row identifiers used across the branch)

```
INV-2026-HIRE-07    ATS-AssistedRanker (candidate-ranking model used in US hiring)
                    Owner: Talent Acquisition Ops
INV-2026-MKTG-11    MCDA (marketing-copy draft assistant, US-wide)
                    Owner: Marketing Ops
INV-2026-SUPPORT-04 ChatTriage (consumer-support intake and routing)
                    Owner: Customer Ops
INV-2026-CLIN-02    TriageAssist (clinical triage AI, US health-system deployment)
                    Owner: Clinical Informatics
INV-2026-CLIN-05    PathTriage (authorised AI/ML-enabled SaMD device,
                    user-facility deployment)
                    Owner: Pathology Service Line
INV-2026-GOV-03     FedBidDraft (bid-response drafting assistant for federal procurements)
                    Owner: Federal Business Development
```

### C. The today-date for the walk

Treat today as **2026-11-11**. All freshness checks and tracking-date calculations resolve against that date.

## Steps

### Step 1 — Scaffold the refresh artefact (10 min)

Create the working folder and files.

```bash
mkdir -p ~/aicg-labs/mod-106-lab-01
cd ~/aicg-labs/mod-106-lab-01
touch tracker-refresh.md change-notes.md
```

Open `tracker-refresh.md` and lay in the headers up front.

```markdown
# US federal branch — monthly deep-read refresh — 2026-11-11

Walker:        <your-name>
Walk date:     2026-11-11
Branch scope:  US federal (REG-2026-US-FED-*)
Cadence:       Monthly deep read per chapter 01.

## Row-by-row refresh

### REG-2026-US-FED-001 — Title VII / ADA / ADEA — EEOC
### REG-2026-US-FED-002 — Section 5 FTC Act
### REG-2026-US-FED-005 — Section 1557 ACA
### REG-2026-US-FED-007 — FDA SaMD framework
### REG-2026-US-FED-010 — White House EO stack
### REG-2026-US-FED-011 — NIST AI RMF + GenAI Profile

## Change-notes authored from this walk

## Walk verdict
```

The eight-section scaffold is what the reviewer reads to confirm the walk ran; the per-row sub-sections carry the evidence.

### Step 2 — Compute each row's staleness against the cadence (10 min)

Chapter 01's cadence says *monthly deep read* reads every row where status is *phased*, *proposed*, or where the weekly touch flagged a change. For *in force* and *guidance* rows that have not been flagged, the deep read still confirms the row's columns are current if the last-verified date is more than one monthly cycle (roughly 30 days) stale.

Compute days-stale for each row against the walk date 2026-11-11. Record the per-row verdict as *fresh — refresh last-verified only*, *stale — read primary sources and refresh columns*, or *stale and known-changed — read primary sources, refresh columns, and author a change-note*.

Expected per-row verdict after this step:

- `REG-2026-US-FED-001` — 183 days stale; *stale — read primary sources and refresh*.
- `REG-2026-US-FED-002` — 183 days stale; *stale — read primary sources and refresh*.
- `REG-2026-US-FED-005` — 257 days stale; *stale — read primary sources and refresh* (and verify the Section 1557 injunction status per the chapter 03 needs-research marker).
- `REG-2026-US-FED-007` — 226 days stale; *stale — read primary sources and refresh*.
- `REG-2026-US-FED-010` — 733 days stale and *status is wrong as the row sits*; *stale and known-changed — read primary sources, refresh columns, and author a change-note* (the chapter 03 needs-research marker on the EO stack names EO 14110 as rescinded by EO 14148 on 20 January 2025 and EO 14179 of 23 January 2025 as the successor; the row still cites EO 14110 as in force, which is wrong).
- `REG-2026-US-FED-011` — 224 days stale; *stale — read primary sources and refresh*.

Record the verdicts in the respective sub-sections of `tracker-refresh.md`.

### Step 3 — Refresh REG-2026-US-FED-001 and REG-2026-US-FED-002 (15 min)

Open chapter 03's EEOC and FTC sub-sections. For each row, confirm:

- The scope trigger still names the statutes chapter 03 cites (Title VII / ADA / ADEA for EEOC; Section 5, FCRA, ECOA, COPPA for FTC where applicable).
- The primary-source URL resolves to the joint statement (for `001`) or to Section 5 of the FTC Act (for `002`) as chapter 03 lists them.
- The affected-inventory-row list is accurate given the inventory rows in block B.
- The AIGP tag per chapter 08 is D3 (both rows sit under *how current laws apply to AI systems*).

In `tracker-refresh.md` under each row's sub-section, record *columns verified; last-verified refreshed to 2026-11-11*. If any column needs a textual update (e.g., scope-trigger wording tightened to the chapter 03 shape — *EEOC enforcement of Title VII / ADA / ADEA on AI-mediated employment decisions* is the chapter 03 formulation), record the before / after.

### Step 4 — Refresh REG-2026-US-FED-005 (15 min)

Open chapter 03's HHS sub-section and the needs-research marker on the Section 1557 patient-care-decision-support provisions. Chapter 03 names the May 2024 final rule at 45 CFR 92.210 and explicitly flags that the provisions were subject to legal challenge in 2024–2025 — the analyst must verify the current enforcement posture and any injunctive relief in force before citing to a covered entity.

Analyst-tier action for the lab: record *verified: chapter 03 names a legal-challenge status that the analyst must verify against the current primary source before citing to an audience. Row refreshed with a `<!-- needs-research: verify current enforcement posture of 45 CFR 92.210 patient-care-decision-support provisions against the HHS OCR page and any pending injunctive relief as of 2026-11-11 before citing to a covered entity -->` marker in the notes column.*

The last-verified date moves to 2026-11-11 because the analyst *did* look at it; the needs-research marker is the analyst-tier honesty about what the look did not resolve.

### Step 5 — Refresh REG-2026-US-FED-007 (10 min)

Open chapter 03's FDA sub-section and chapter 06's medical-overlay sub-section. Confirm:

- The scope trigger covers both manufacturer and user-facility roles (chapter 06 explicitly names both roles and attaches different obligations).
- The affected-inventory-row list distinguishes the two roles — `INV-2026-CLIN-02` (TriageAssist, manufacturer) and `INV-2026-CLIN-05` (PathTriage, user facility).
- The primary-source URL chain extends to the chapter 06 instruments (PCCP guidance, GMLP, 21 CFR Parts 807/814/820 transitioning to QMSR).

Record *columns verified; last-verified refreshed to 2026-11-11; row cross-reference to `REG-2026-SEC-MED-*` sector-overlay rows noted*. The analyst-tier discipline here is that the FDA SaMD row in the US federal branch and the medical-overlay rows in the sector-overlays branch are mutually reinforcing — a change in one requires a walk across to the other.

### Step 6 — Refresh REG-2026-US-FED-010 and prepare the change-note (25 min)

This is the row with the material change. Open chapter 03's "White House executive orders — the shifting overlay" sub-section and the needs-research marker that names EO 14110 as rescinded on 20 January 2025 by EO 14148, with EO 14179 of 23 January 2025 as the successor policy.

The row as it sits still cites EO 14110 as in force, with a 2024-11-08 last-verified date that pre-dates the rescission. This is the exact failure mode chapter 10 names — *the regulation moves and the impact assessment does not*. The row has been dormant through two administrations.

Update the row in `tracker-refresh.md`:

- *Status.* *In force — EO 14179 of 23 January 2025 (Removing Barriers to American Leadership in AI) as the successor policy following rescission of EO 14110 (30 October 2023) by EO 14148 (20 January 2025). Current EO stack and any additional delegated OMB actions to be verified at Federal Register and the White House site before citing to an internal audience.*
- *Last verified.* 2026-11-11.
- *Notes.* Replace *Row has not been refreshed through two presidential-administration transitions* with the rescission / succession chain, a `<!-- needs-research: verify the current OMB memoranda stack and any additional EOs on AI issued after EO 14179 against Federal Register as of 2026-11-11 before citing to internal audience -->` marker, and the change-note identifier reserved in step 7.

Then flip to `change-notes.md` and author `CN-2026-LAB01-01` per chapter 10's shape — header (identifier, date, filer, tracker row updated, related regulator artefacts), body (*what changed*: the EO stack changed through two administrations; the row was dormant; EO 14110 was rescinded 20 Jan 2025 and EO 14179 of 23 Jan 2025 is the successor; *why it matters here*: `INV-2026-GOV-03` FedBidDraft is a federal-procurement-facing system whose compliance posture is shaped by the EO stack that is flowed down through federal contracts), *affected inventory rows* (`INV-2026-GOV-03`), *affected impact-assessment artefacts* (the FedBidDraft canonical document, register entries, model card — cite illustrative identifiers), *recommended action per owner* (three concrete actions with target dates — refresh canonical document's regulatory-context section, confirm no federal-procurement clause the enterprise is already bound by references EO 14110 as live, revisit review-triggers list), *counsel / privacy-officer flag* (routed to General Counsel on the federal-procurement-clause question), *analyst next-step tracking date* (two weeks — 2026-11-25), footer (*Open*; cross-reference to `REG-2026-US-FED-010`).

### Step 7 — Refresh REG-2026-US-FED-011 (10 min)

Open chapter 03's NIST sub-section. The NIST row is *guidance — voluntary; cited in enforcement*. Confirm:

- The scope trigger — chapter 03 names the AI RMF and the GenAI Profile (NIST AI 600-1) as the two instruments; the sector companions from `mod-103` are related but separate.
- The affected-inventory-row list is a *cites against this row* list — every inventory row that uses the AI RMF as the structuring framework in its canonical document.
- The AIGP tag per chapter 08 is D4 (*existing and emerging AI laws and standards*).

Record *columns verified; last-verified refreshed to 2026-11-11*. The NIST row does *not* produce a change-note — the framework has not changed in a way the chapter 03 content signals, and the row's status is honest as it sits. The point of walking it is confirming no change rather than finding one.

### Step 8 — Fill the walk-verdict section (10 min)

One paragraph, three or four sentences:

- *Walk ran on 2026-11-11 across six rows; six last-verified dates refreshed; five refreshed with no material change; one — `REG-2026-US-FED-010` — surfaced a material change (the EO stack moved through two administrations while the row was dormant) and was closed by authoring change-note `CN-2026-LAB01-01` routed to the FedBidDraft system owner. Next deep read due 2026-12-11; next weekly light touch due 2026-11-18. Section 1557 `<!-- needs-research: -->` marker on `REG-2026-US-FED-005` is open and tracked.*

### Step 9 — Cross-check the walk log and change-note (10 min)

Walk the refresh artefact and the change-note side-by-side. Every row named in step 2's staleness verdict must appear in a per-row sub-section with its refresh recorded. The one row with a material change must appear in the change-notes section and must cite the exact change-note identifier `CN-2026-LAB01-01`. The change-note's *tracker row updated* field must match the refresh-artefact row's identifier.

High-tripwire fields:

- **The EO row's status change.** Named in step 6, refreshed with the rescission / succession chain, and closed into `CN-2026-LAB01-01`'s *what changed* field. The rescission date (20 January 2025) and the successor EO number (14179) must be consistent across the refresh artefact and the change-note.
- **The Section 1557 needs-research marker.** Named in step 4 and recorded in the row's notes column. The marker is the analyst-tier honest answer when chapter 03 explicitly asks the analyst to verify current enforcement posture against a primary source.

### Step 10 — Self-check (10 min)

Walk both files top-to-bottom and verify:

- Every row has a per-row sub-section in `tracker-refresh.md` with a verdict from step 2 and a refresh record.
- The one change-note authored from the walk follows the chapter 10 structure field-by-field (header / body / footer) and routes to the specific system owner rather than a mass distribution.
- No fabricated EO numbers, no fabricated rescission dates, no fabricated agency actions. The EO 14110 / 14148 / 14179 chain is reproduced from chapter 03's needs-research marker; any further refinement carries its own `<!-- needs-research: -->` marker.
- No legal-conclusion language in either artefact. The refresh is situational awareness; the change-note is a routed action; neither is an opinion on whether the enterprise complies with any specific EO flow-down.

## Expected output

Two markdown files in `~/aicg-labs/mod-106-lab-01/`:

- `tracker-refresh.md` — eight sections (one per row plus change-notes and verdict); six rows refreshed; five with *columns verified; last-verified refreshed to 2026-11-11*; one with a before / after status change; one needs-research marker carried on the Section 1557 row.
- `change-notes.md` — one change-note (`CN-2026-LAB01-01`) following chapter 10's structure field-by-field.

Total length: roughly 1,200–2,000 words across both files. A reviewer should be able to read both in ten minutes and see every row walked, the one material change closed into a change-note, and the next-cadence dates recorded.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did you walk every row, including the ones that turned out to be fresh?** It is tempting to skip the rows whose last-verified date is only mildly stale. Chapter 01's cadence rule says the deep read reads every row; the discipline is not skipping the rows that look boring.
2. **Did the EO row's refresh resolve the rescission / succession chain honestly?** The EO stack is the one row where chapter 03's needs-research marker is the primary source the lab uses for the material change. If the refresh cites EO 14110 as in force, the walk has failed its headline test.
3. **Did the Section 1557 row carry a needs-research marker rather than a guess?** Chapter 03 flags the legal-challenge status explicitly. A refresh that confidently asserts the May 2024 final rule's patient-care-decision-support provisions are in force without a marker is the kind of silent-fabrication the analyst-tier discipline prevents.
4. **Does the change-note route to the specific system owner (FedBidDraft) rather than a mass distribution?** Chapter 10's no-mass-distribution rule is the discipline. A change-note that goes to *all system owners* has spectators, not owners.
5. **Is `CN-2026-LAB01-01`'s *recommended action per owner* action-shaped?** Three concrete tasks with owner, artefact, and date — not *please revisit*.

If any of the five is "no", revise *that artefact* before considering the lab done.

## Why this is a lab, not an exercise

The module's five exercises each drill a single aspect of the tracker discipline — the schema (ex 01), a crosswalk (ex 02), one chapter's flagging (ex 03), one chapter's overlay set (ex 04), one chapter's change-note shape in the general case (ex 05). None of them asks the analyst to run a *cadence cycle* end-to-end against an already-stale branch, which is the specific place where the chapter 01 refresh discipline, the chapter 03 dynamic EO overlay, and the chapter 10 change-note shape all converge into a single hour of work the analyst will do every month. This lab is that convergence. The failure mode it prevents is the analyst who can author each artefact in isolation but who has never once refreshed a branch that had gone dormant through an administration transition, caught the status drift, routed the change-note, and closed the loop into an inventory row.
