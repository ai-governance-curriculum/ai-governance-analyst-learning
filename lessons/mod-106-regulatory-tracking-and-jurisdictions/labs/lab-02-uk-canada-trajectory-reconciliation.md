# Lab 02 — UK and Canada Trajectory Reconciliation on a Drifted Branch

**Duration:** 90 minutes.
**Grounding chapters:** [01](../01-rolling-regulatory-tracker-method.md), [05](../05-uk-canada-trajectories.md); AIGP tagging per [08](../08-iapp-aigp-shared-vocabulary.md).
**Difficulty:** Core — exercises chapter 05's *status field for legislative-trajectory rows carries the current parliamentary state honestly* discipline, which the module's five exercises do not directly drill.

## Objective

Take a *fixed, pre-assembled* UK and Canada branch of the regulatory tracker that a previous analyst authored at two different points in time — the UK rows were drafted in 2024 against the pro-innovation white paper with the horizontal AI statute optimistically marked *likely to pass*, and the Canada rows were drafted in late 2022 when Bill C-27 was still progressing through the 44th Parliament. The branch has not been touched since. Walk it, reconcile each row's status field against chapter 05's current-state framing, produce a `tracker-reconciliation.md` artefact that records the before / after per row, and author a one-line entry in the branch's `horizon-scan.md` for the two trajectories that currently sit in a *watch* rather than *in force* posture.

The point of the lab is the status discipline chapter 05 insists on — *proposed*, *died on order paper*, *in second reading*, *enacted — pending commencement*, *in force* are not interchangeable, and a row that says *proposed — AI Act (Canada)* without the died-on-order-paper annotation misleads a reviewer. The module's exercises do not drill this status-field discipline; this lab does.

## Prerequisites

- All ten chapters read; chapter 05's UK principles-based regulator-led framing, Canada's TBS Directive + AIDA trajectory, and the status-field discipline for legislative-trajectory rows fresh in memory.
- A markdown editor; no Python or GRC-platform tooling required — the branch below is a Markdown-only stand-in for the records that would live in the GRC platform in production.
- Exercise 01 completed, or at minimum skimmed, so the tracker schema is familiar.

## The fixed input — a drifted UK and Canada branch

Use *exactly* this branch. Do not substitute instruments and do not pre-correct the drift. Identifiers are illustrative; treat the whole block as `pedagogic example — numbers and dates illustrative`.

### A. The tracker rows — UK

```
REG-2026-UK-001 — UK GDPR + Data Protection Act 2018 — AI and personal data
  Status:         In force
  Last verified:  2024-04-01
  Scope trigger:  Processing of personal data of UK data subjects by an AI system
                  under a controller established in the UK or offering goods or
                  services to UK data subjects.
  Role:           Controller
  Enforcement:    ICO
  AIGP tag:       D3
  Primary src:    https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/

REG-2026-UK-002 — UK GDPR Article 22 + DPA 2018 §14 — solely-automated decisions
  Status:         In force (UK GDPR Article 22 retained from EU GDPR; DPA 2018 §14
                  supplements)
  Last verified:  2024-04-01
  Scope trigger:  Solely-automated decision with legal or similar significant
                  effect on a UK data subject.
  Role:           Controller
  Enforcement:    ICO
  AIGP tag:       D3
  Primary src:    https://www.legislation.gov.uk/ukpga/2018/12/section/14

REG-2026-UK-004 — UK principles-based AI regulation — cross-regulator
  Status:         Proposed — pro-innovation white paper March 2023; horizontal AI
                  statute likely to pass in next session.
  Last verified:  2024-04-01
  Scope trigger:  AI system deployed in a sector under an existing UK regulator's
                  remit (ICO, FCA, MHRA, Ofcom, CMA, EHRC, HSE).
  Role:           Varies by regulator
  Enforcement:    Existing sector regulators within statutory remit
  AIGP tag:       D4
  Primary src:    https://www.gov.uk/government/publications/ai-regulation-a-pro-innovation-approach

REG-2026-UK-005 — ICO AI-and-data-protection guidance and audit framework
  Status:         Guidance — in force reference
  Last verified:  2024-04-01
  Scope trigger:  AI system processing personal data of UK data subjects.
  Role:           Controller
  Enforcement:    ICO (as evidence weight, not as rule)
  AIGP tag:       D3
  Primary src:    https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/
```

### B. The tracker rows — Canada

```
REG-2026-CA-001 — TBS Directive on Automated Decision-Making
  Status:         In force (since 1 April 2019; amended)
  Last verified:  2022-11-15
  Scope trigger:  Federal-institution use of an automated decision system for an
                  administrative decision about a client; via flow-down, a
                  contractor supplying such a system to a federal institution.
  Role:           Federal institution (direct); contractor (flow-down)
  Enforcement:    Treasury Board of Canada Secretariat and internal-audit
                  function of the deploying institution
  AIGP tag:       D4
  Primary src:    https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592

REG-2026-CA-003 — AIDA — Artificial Intelligence and Data Act
  Status:         In progress — Bill C-27 Part 3; progressing through 44th Parliament;
                  expected enactment 2024.
  Last verified:  2022-11-15
  Scope trigger:  Person responsible for a high-impact AI system in the Canadian
                  private sector.
  Role:           Person responsible
  Enforcement:    Minister of Innovation, Science, and Industry (as tabled)
  AIGP tag:       D4
  Primary src:    https://www.parl.ca/DocumentViewer/en/44-1/bill/C-27/first-reading
  Notes:          Reserve row for the enacted-text columns once Bill C-27 passes.

REG-2026-CA-004 — PIPEDA + OPC generative-AI principles
  Status:         In force (PIPEDA); OPC principles published 2023
  Last verified:  2024-01-10
  Scope trigger:  Private-sector organisation processing personal information of a
                  Canadian data subject in the course of commercial activity.
  Role:           Organisation subject to PIPEDA
  Enforcement:    Office of the Privacy Commissioner of Canada
  AIGP tag:       D3
  Primary src:    https://www.priv.gc.ca/en/privacy-topics/technology/artificial-intelligence/gd_principles_ai/

REG-2026-CA-005 — Quebec Law 25 — automated-decisionmaking-notification provisions
  Status:         In force (commencement 22 September 2023 for the ADM provisions)
  Last verified:  2023-10-02
  Scope trigger:  Private-sector organisation using an automated decision system
                  to render a decision based exclusively on automated processing
                  of personal information about a Quebec data subject.
  Role:           Organisation subject to Quebec Law 25
  Enforcement:    Commission d'accès à l'information du Québec (CAI)
  AIGP tag:       D3
  Primary src:    https://www.cai.gouv.qc.ca/documents/CAI_A_Loi_25_EN.pdf
```

### C. The today-date for the reconciliation

Treat today as **2026-11-11**. All freshness checks resolve against that date.

## Steps

### Step 1 — Scaffold the reconciliation artefact (5 min)

Create the working folder and files.

```bash
mkdir -p ~/aicg-labs/mod-106-lab-02
cd ~/aicg-labs/mod-106-lab-02
touch tracker-reconciliation.md horizon-scan.md
```

Open `tracker-reconciliation.md` and lay in the headers.

```markdown
# UK + Canada branch — status reconciliation — 2026-11-11

Walker:        <your-name>
Walk date:     2026-11-11
Branch scope:  UK (REG-2026-UK-*) and Canada (REG-2026-CA-*)
Reconciliation discipline: per chapter 05 — status fields on legislative-trajectory
rows carry the current parliamentary state honestly.

## UK — row-by-row reconciliation
### REG-2026-UK-001 — UK GDPR + DPA 2018
### REG-2026-UK-002 — UK GDPR Article 22 + DPA 2018 §14
### REG-2026-UK-004 — UK principles-based AI regulation
### REG-2026-UK-005 — ICO guidance and audit framework

## Canada — row-by-row reconciliation
### REG-2026-CA-001 — TBS Directive on Automated Decision-Making
### REG-2026-CA-003 — AIDA
### REG-2026-CA-004 — PIPEDA + OPC generative-AI principles
### REG-2026-CA-005 — Quebec Law 25

## Rows added to horizon-scan

## Reconciliation verdict
```

### Step 2 — Reconcile REG-2026-UK-001 and REG-2026-UK-002 (10 min)

Open chapter 05's "The ICO as the load-bearing regulator for AI-and-data" and "UK GDPR Article 22" sub-sections. For each row, confirm the status is still *in force* and refresh last-verified to 2026-11-11.

Chapter 05 also names the Data (Use and Access) Act 2025 as having amended the UK's automated-decision-making rules — this is a *material change* the branch has not captured. Specifically, the branch has `REG-2026-UK-002` sitting as *in force* with a 2024-04-01 last-verified date; the Act's commencement is a load-bearing refresh target. Do not fabricate the enacted text (the chapter 05 needs-research marker is explicit); the analyst-tier move is:

- Keep `REG-2026-UK-002` as *in force (UK GDPR Article 22 retained; DPA 2018 §14 supplements)*.
- Add a new row identifier placeholder `REG-2026-UK-003` for the Data (Use and Access) Act 2025 — this is the row the earlier author missed. Status: *in force — ADM provisions commenced; enacted text and commencement dates to be verified against the enacted Act before citing to a UK deployment per chapter 05 needs-research marker*. Carry a `<!-- needs-research: verify enacted text and commencement dates of the Data (Use and Access) Act 2025 ADM provisions at bills.parliament.uk and legislation.gov.uk as of 2026-11-11 before citing to a UK deployment -->` marker in the notes column.

Record the before / after in the reconciliation artefact sub-section.

### Step 3 — Reconcile REG-2026-UK-004 (10 min)

The row's current status reads *Proposed — pro-innovation white paper March 2023; horizontal AI statute likely to pass in next session.*

Open chapter 05's "The UK — principles-based, regulator-led" sub-section. The chapter is explicit that the UK's stated approach is principles-based, context-specific, and regulator-led; there is no single AI regulator and no horizontal AI statute in force. Chapter 05 also carries a needs-research marker on current government policy — the trajectory has been active, and the row's status must be current.

The before / after:

- *Before.* *Proposed — pro-innovation white paper March 2023; horizontal AI statute likely to pass in next session.*
- *After.* *Guidance — non-statutory; principles-based regulator-led approach per 2023 white paper and 2024 government response. Horizontal AI statute not currently in force; any proposed legislation to be tracked in the horizon-scan rather than against this row. Last verified 2026-11-11 against chapter 05 content; current primary sources at `gov.uk` to be verified before citing to an internal audience per chapter 05 needs-research marker.*

The row's status is corrected; the speculative *likely to pass* language is removed; the enforcement note is adjusted to *existing sector regulators within statutory remit* with the chapter 05 list (ICO, FCA, MHRA, Ofcom, CMA, EHRC, HSE) preserved. Add a `<!-- needs-research: -->` marker for current government policy.

### Step 4 — Reconcile REG-2026-UK-005 (5 min)

Open chapter 05's ICO sub-section. The row's status is *guidance — in force reference*, which maps onto chapter 05's *guidance — non-binding; load-bearing evidence for the AI-and-personal-data slice*. No material change. Refresh last-verified to 2026-11-11.

Record *columns verified; last-verified refreshed; no material change*.

### Step 5 — Reconcile REG-2026-CA-001 (5 min)

Open chapter 05's "The TBS Directive on Automated Decision-Making" sub-section. The Directive has been in force since 1 April 2019 with amendments. The row's status is correct. Refresh last-verified to 2026-11-11.

Chapter 05 also names a related instrument — the TBS *Guide on the use of generative AI* — which the row does not currently carry. Add a placeholder note *related: TBS Guide on the use of generative AI (Guidance layered on Directive); candidate for `REG-2026-CA-002` row*.

Record *columns verified; last-verified refreshed; related guidance not yet carried as a separate row — noted for the horizon-scan*.

### Step 6 — Reconcile REG-2026-CA-003 — the AIDA correction (15 min)

This is the row with the material and *wrong* status. Open chapter 05's "The AIDA trajectory" sub-section. The chapter is explicit:

- Bill C-27 did not pass before the prorogation of the 44th Parliament on 6 January 2025.
- Under Canadian parliamentary procedure, the bill died on the order paper.
- The tracker's status field is *proposed — died on order paper 6 Jan 2025*. A re-tabled version or successor bill is monitored in the horizon-scan.
- Chapter 05 carries a needs-research marker to monitor for any successor legislation.

The before / after:

- *Before.* *In progress — Bill C-27 Part 3; progressing through 44th Parliament; expected enactment 2024.*
- *After.* *Proposed — died on order paper 6 January 2025 when the 44th Parliament of Canada prorogued; no current federal Canadian private-sector AI statute. Monitor for successor legislation in the horizon-scan per chapter 05 needs-research marker.*

Remove the *expected enactment 2024* line (it is both wrong and speculative). Remove the *reserve row for the enacted-text columns once Bill C-27 passes* notes-column text (it is counterfactual). Replace with the died-on-order-paper annotation and a `<!-- needs-research: monitor the Canadian federal Parliament for any successor legislation to AIDA against parl.ca as of 2026-11-11 -->` marker.

Add the AIDA trajectory to the horizon-scan file (step 8 below).

Record the full before / after in the reconciliation artefact sub-section. This row is the headline test of the lab — a reconciliation that leaves this row saying *in progress* has failed.

### Step 7 — Reconcile REG-2026-CA-004 and REG-2026-CA-005 (5 min)

Open chapter 05's PIPEDA sub-section and the Quebec Law 25 reference. For each row:

- Confirm status is still *in force*.
- Confirm scope-trigger wording tracks the chapter 05 shape (PIPEDA applies to private-sector organisations processing personal information in the course of commercial activity; Quebec Law 25's ADM provisions apply to decisions based exclusively on automated processing of personal information about a Quebec data subject).
- Refresh last-verified to 2026-11-11.

Record *columns verified; last-verified refreshed; no material change*.

### Step 8 — Author the horizon-scan entries (10 min)

Open `horizon-scan.md` and lay in the headers.

```markdown
# UK + Canada horizon-scan — 2026-11-11

Promotion rule: a horizon-scan row is promoted to the main tracker when its
effective date is within the current rolling six-month window, or when an
inventory row is identified as affected.

## UK
## Canada
```

Under *UK*, add a short entry for any UK horizontal AI statute trajectory — status *watch*, primary-source URL to the gov.uk page, and the `<!-- needs-research: -->` marker from step 3.

Under *Canada*, add an entry for the AIDA successor-legislation trajectory — status *watch — no successor tabled as of 2026-11-11 per primary-source verification*, primary-source URL to the Parliament of Canada page, and the `<!-- needs-research: -->` marker from step 6.

The horizon-scan is where chapter 05's *status field for legislative-trajectory rows carries the current parliamentary state honestly* discipline lives operationally. A row in the main tracker that says *proposed* has to be either on the brink of enactment or a live, in-flight bill; speculative trajectories live in the horizon-scan and are promoted when the chapter 04 promotion rule fires.

### Step 9 — Fill the reconciliation-verdict section (5 min)

One paragraph:

- *Reconciliation ran on 2026-11-11 across four UK rows (plus one new row added for the Data (Use and Access) Act 2025 ADM provisions) and four Canada rows. The UK branch's horizontal AI statute row corrected from `proposed — likely to pass` to the principles-based regulator-led status chapter 05 describes; the Canada branch's AIDA row corrected from `in progress` to `died on order paper 6 January 2025`; both trajectories carried over to the horizon-scan. Four `<!-- needs-research: -->` markers open against primary sources that chapter 05 names as the verification points before citing to an audience. Next deep read due 2026-12-11.*

### Step 10 — Self-check (10 min)

Walk both files top-to-bottom and verify:

- Every row has a per-row sub-section with before / after; the three material changes (`REG-2026-UK-004`, `REG-2026-CA-003`, new row `REG-2026-UK-003`) carry explicit before / after text.
- The AIDA row is corrected. The row no longer says *in progress* or *expected enactment 2024*; it says *died on order paper 6 January 2025*.
- The UK horizontal statute row no longer says *likely to pass*. The status is *guidance — non-statutory; principles-based regulator-led*.
- The horizon-scan file carries one UK entry and one Canada entry, both with the chapter 05 needs-research markers reproduced.
- No fabricated enacted-text citations, no fabricated dates. Every uncertain fact carries a `<!-- needs-research: -->` marker pointing at the primary source chapter 05 names.

## Expected output

Two markdown files in `~/aicg-labs/mod-106-lab-02/`:

- `tracker-reconciliation.md` — row-by-row reconciliation with explicit before / after on the three material changes and *columns verified; no material change* on the four fresh rows.
- `horizon-scan.md` — one UK entry and one Canada entry with the promotion-rule header.

Total length: roughly 900–1,500 words across both files. A reviewer should be able to read both in eight minutes and see every row reconciled, the two legislative-trajectory corrections made honestly, and the horizon-scan entries filed.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did the AIDA row land on *died on order paper 6 January 2025*?** This is the headline test. A reconciliation that leaves the row on *in progress* or *expected enactment 2024* has failed the chapter 05 status-field discipline.
2. **Did the UK horizontal statute row drop the speculative *likely to pass* language?** Chapter 05's needs-research marker asks the analyst to verify current government policy; speculative trajectory language in the main tracker row is precisely what the marker is designed to replace.
3. **Did the Data (Use and Access) Act 2025 get its own row?** Chapter 05 names it as the instrument that shifted UK GDPR Article 22 ADM provisions; a branch that does not carry it has a gap chapter 05 explicitly flags.
4. **Did every uncertain fact carry a `<!-- needs-research: -->` marker rather than a guess?** Chapter 05 is particularly explicit that speculating about the next bill is a policy activity, not a tracker activity. Markers over guesses.
5. **Is the horizon-scan file actually a separate file, not a note inside the main reconciliation?** Chapter 05's discipline is that the main tracker and the horizon-scan are different artefacts with different promotion rules. Collapsing them undoes the discipline.

If any of the five is "no", revise *that artefact* before considering the lab done.

## Why this is a lab, not an exercise

The module's five exercises drill the tracker schema, crosswalks against the EU and US-state stacks, Article 22 flagging, the sector overlays, and the change-note shape. None of them walks a UK and Canada branch that has been quietly wrong for eighteen months because the previous analyst's status-field discipline lapsed. Chapter 05's integration muscle is the honest status field — *proposed*, *died on order paper*, *in second reading*, *enacted — pending commencement*, *in force* — and the ability to distinguish them under light pressure. This lab exercises that muscle on a drifted branch; the failure mode it prevents is the analyst who has read chapter 05 but has never actually corrected an *in progress* row on a bill that died two years earlier.
