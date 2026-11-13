# Lab 01 — Mid-Cycle Stale-Evidence Sweep on a Pre-Assembled Control-Record Snapshot

**Duration:** 2 hours.
**Grounding chapters:** [02](../02-control-testing-cycle-and-evidence-artefacts.md), [03](../03-control-status-report-for-internal-audit.md), [09](../09-delegation-boundary-and-escalation-patterns.md).
**Difficulty:** Core — exercises the chapter-02 four stale-evidence flag rules, the chapter-03 four-verdict discipline, and the chapter-09 four escalation classes against a pre-assembled control-record snapshot that has drifted in six specific, deliberate ways. The module's five exercises each drill authoring-from-scratch — exercise 01 authors a runbook and fresh test rows, exercise 02 authors OWASP tagging decisions, exercise 03 authors MITRE ATLAS / NIST AI 100-2 / SAIF reference composition, exercise 04 authors vendor intake rows, exercise 05 authors the crosswalk matrix. None of them asks the analyst to walk a *pre-filed control-record set mid-cycle*, catch the drift the GRC platform has not yet flagged, apply the verdict language without softening, and roll the stale-evidence findings into the §6 of the control-status report plus the right escalation classes. This lab is that specific convergence — the hour of work the analyst runs between the full periodic cycle and the full report issuance, when the flag rules trigger a re-test and the four-verdict discipline has to be applied to a record that was *pass* last quarter.

## Objective

Take a *fixed, pre-assembled* control-record snapshot — six control records filed in a prior quarterly cycle with deliberately-induced drift and stale evidence — and run a mid-cycle sweep over it. For each record, compute which of the four stale-evidence flag rules has tripped, re-verify the control statement against the recorded evidence, assign the correct chapter-03 verdict (*pass*, *fail*, *deviation*, *not-tested-in-period*), draft the follow-up action, and — for the rows where the drift crosses into an escalation trigger — author the chapter-09 escalation entry of the correct class. Close by composing a §6 stale-evidence roll-up block for a control-status report (`CSR-2026-Q4`) that is drafting and projecting the entries into the escalation register.

The deliverable is three Markdown files in `~/aicg-labs/mod-108-lab-01/`:

- `sweep-log.md` — the walk log, one sub-section per control record.
- `csr-section-6-stale-evidence-rollup.md` — the §6 block the sweep contributes to the drafting `CSR-2026-Q4` report.
- `escalation-register.md` — the `ESC-<year>-<sequence>` entries authored from the sweep, projected into the chapter-9 register shape.

A reviewer should be able to read all three in twenty minutes and see every control record walked, every flag rule explicitly applied or confirmed not-tripped, every verdict assigned by the four-word discipline, every follow-up named with owner and due date, and every escalation routed per the chapter-9 classes.

## Prerequisites

- Chapters 02, 03, and 09 read; the four cycle phases, the six evidence-artefact classes, the ten-field evidence-attachment record shape, the four stale-evidence flag rules (cadence-window, config-change, model-version-change, regulatory-obligation-change), the four verdicts (*pass*, *fail*, *deviation*, *not-tested-in-period*), the nine-section report shape with §6 as the stale-evidence roll-up, and the four escalation classes fresh in memory.
- A Markdown editor; no Python, GRC, or vendor tooling required — the control-record snapshot below is a Markdown-only stand-in for what would live in the GRC platform in production.
- Exercise 01 completed, or at minimum skimmed, so the `CTL-<year>-<sequence>-<test-N>` row schema (twenty columns) and the §2 scope / §3 verdict rollup / §4 findings / §5 escalations / §6 stale-evidence roll-up / §7 delegation-boundary notes structure is familiar. The snapshot below is written at the level of the columns a mid-cycle walker reads from — it does not reproduce every column verbatim.
- The MCDA (`INV-2026-0088`) and MCDA-Benefits (`INV-2026-0311`) inventory rows from `mod-102` conceptually in mind; the snapshot references both.

## The fixed input — a deliberately-drifted control-record snapshot

Use *exactly* this record set. Do not substitute identifiers, dates, model versions, or evidence identifiers, and do not pre-correct the drift — the drift is the point of the lab. Each record is reproduced only at the level of fields a mid-cycle walker reads from. Treat the whole block as `pedagogic example — identifiers, numbers, and dates illustrative`.

### A. Six control records as filed last quarter

```
CTL-2026-0341 — Jailbreak-classifier threshold + human-review queue
  Statement:            For every customer-facing endpoint, the input length is capped
                        at 8000 tokens; the jailbreak-classifier fires and returns the
                        refusal message on prompts scoring >= 0.85; the human-review
                        queue is invoked when the classifier score is between 0.6 and
                        0.85.
  Applicable systems:   INV-2026-0088 (MCDA), INV-2026-0091 (support-chat-copilot),
                        INV-2026-0104 (contract-review-assistant).
  Owner:                ML platform team; ml-platform-lead@ escalation.
  Cadence:              Quarterly, plus on-change.
  Expected evidence:    config export + log sample.
  Last test (Q3):       EV-2026-0812 (config export, time-of-export 2026-08-14),
                        EV-2026-0813 (log sample, window 2026-07-15 → 2026-08-14,
                        uniform 1000-record sample),
                        EV-2026-0814 (log sample on INV-2026-0104, window 2026-07-15
                        → 2026-08-14, should-have-fired-but-did-not subset could not
                        be produced by the platform).
  Last-verified:        2026-08-20.
  Last Q3 verdict:      deviation (log-sample sampling limitation on INV-2026-0104).
  Follow-up open:       Class-1 escalation ESC-2026-0051 filed 2026-08-25 to
                        senior-ai-governance-architect for library-level sampling
                        rule; status open as of this snapshot.

CTL-2026-0344 — MCDA-Benefits RAG groundedness
  Statement:            For every MCDA-Benefits release, the RAG-triad eval runs on
                        the current retrieval index and groundedness stays >= 0.90 on
                        the in-scope query set and >= 0.80 on the negative-query
                        subset.
  Applicable systems:   INV-2026-0311 (MCDA-Benefits).
  Owner:                Internal Safety Eval Team; safety-eval-lead@ escalation.
  Cadence:              Per release + monthly.
  Expected evidence:    eval-report link.
  Last test (Q3):       Attached EV-2026-0828 pointing to EVAL-2026-089 (RAG-triad
                        eval run 2026-06-30; next-due 2026-07-30 per the row's
                        cadence).
  Last-verified:        2026-08-10.
  Last Q3 verdict:      pass (per the EVAL-2026-089 row's then-status of
                        evidence-current).
  Follow-up open:       None.

CTL-2026-0347 — AEDT bias-audit publication
  Statement:            For every AEDT used in NYC hiring, an independent bias audit
                        is conducted within the past twelve months and the audit
                        summary is published on the employer's website.
  Applicable systems:   INV-2026-0121 (HR-screening-assistant).
  Owner:                HR-tech product owner; hr-tech-lead@ escalation.
  Cadence:              Annual + on-event (new AEDT deployed, DCWP guidance revision).
  Expected evidence:    independent audit report link + sign-off record (published-
                        summary URL + legal review of publication).
  Last test (Q3):       EV-2026-0901 (bias audit report dated 2025-11-10,
                        BABL-trained auditor, ForHumanity NYC LL 144 criteria v1.3;
                        attached), EV-2026-0902 (publication URL captured
                        2025-11-15; legal-review sign-off record 2025-11-18).
  Last-verified:        2026-08-18.
  Last Q3 verdict:      pass.
  Follow-up open:       None.

CTL-2026-0352 — Vendor DPA currency
  Statement:            For every third-party AI vendor processing personal data on
                        enterprise behalf, a DPA is in place, reflects the current
                        transfer mechanism, and names all current sub-processors.
  Applicable systems:   Enterprise-wide (applies to VND-2026-0044 through
                        VND-2026-0058 per vendor-risk-register).
  Owner:                Procurement + Legal; data-protection-officer@ copied.
  Cadence:              Annual + on-event (new sub-processor, transfer-mechanism
                        change, vendor DPA revision).
  Expected evidence:    sign-off record (DPA execution record per vendor) + screenshot
                        (vendor trust-site sub-processor list snapshot).
  Last test (Q3):       EV-2026-0810 (DPA execution records for VND-2026-0044 through
                        VND-2026-0058; all dated within last 12 months),
                        EV-2026-0811 (trust-site sub-processor list snapshots per
                        vendor, dated 2026-08-01 through 2026-08-14).
  Last-verified:        2026-08-22.
  Last Q3 verdict:      pass.
  Follow-up open:       None.

CTL-2026-0355 — High-tier release-assurance sign-off
  Statement:            For every High-tier model release, a release-assurance sign-
                        off from ai-evaluation-engineer is recorded in the release-
                        management system with the paired review packet
                        (PACKET-<year>-<sequence>) identifier.
  Applicable systems:   All INV-<year>-<sequence> rows with tier = High.
  Owner:                Release management; release-mgmt-lead@ escalation.
  Cadence:              On-release.
  Expected evidence:    sign-off record.
  Last test (Q3):       EV-2026-0872 (sign-off records for the three High-tier
                        releases that shipped between 2026-07-01 and 2026-09-30, each
                        linked to its PACKET-<year>-<sequence>).
  Last-verified:        2026-10-02.
  Last Q3 verdict:      pass.
  Follow-up open:       None.

CTL-2026-0361 — Fairness-review note refresh on High-tier
  Statement:            For every High-tier model, a fairness-review note is produced
                        at release and refreshed at least annually with a signed
                        comment from the model owner.
  Applicable systems:   INV-2026-0088 (MCDA), INV-2026-0121 (HR-screening-assistant).
  Owner:                Responsible-AI team; ra-lead@ escalation.
  Cadence:              Annual + on-release.
  Expected evidence:    sign-off record + interview note.
  Last test (Q3):       EV-2026-0885 (fairness-review notes for both systems,
                        refreshed 2025-11-15 and 2025-12-02 respectively), EV-2026-
                        0886 (model-owner signed comment on each).
  Last-verified:        2026-08-19.
  Last Q3 verdict:      pass.
  Follow-up open:       None.
```

### B. Related artefact identifiers

```
INV-2026-0088    MCDA (marketing-copy draft assistant)      Tier: High
INV-2026-0091    support-chat-copilot                        Tier: Medium
INV-2026-0104    contract-review-assistant                   Tier: High
INV-2026-0121    HR-screening-assistant (AEDT, NYC hiring)   Tier: High
INV-2026-0311    MCDA-Benefits                               Tier: High
VND-2026-0044    [hosted-foundation-model-vendor-X]          via API
VND-2026-0058    [embedding-model-vendor-Y]                  via API
EVAL-2026-089    MCDA-Benefits RAG-triad eval, run 2026-06-30
PACKET-2026-096  MCDA v3.6 release-assurance packet (prior quarter)
REG-2026-US-STATE-003    Colorado AI Act
REG-2026-US-NYC-001      NYC Local Law 144
REG-2026-EU-001          EU AI Act
ESC-2026-0051    Class-1 escalation on CTL-2026-0341 sampling rule; open since Q3
POL-2026-0018 §4 Internal responsible-AI policy, prompt-injection controls
CSR-2026-Q3      Prior-period control-status report (issued 2026-09-15)
CSR-2026-Q4      Current-period control-status report (drafting; issuance 2026-12-15)
```

### C. What has changed in the quarter since the Q3 report issued

Treat today as **2026-11-14**. The following events are known to have occurred in the current quarter; some are reflected in the records above and some are *not*. The sweep's job is to notice which is which.

1. **MCDA (`INV-2026-0088`) system prompt** was hot-fixed on 2026-10-05 from v1.8 to v1.8.1, tightening the competitor-disparagement refusal behaviour. The GitOps repo commit touched the system-prompt file that the `CTL-2026-0341` config-export evidence (`EV-2026-0812`) was baselined against.
2. **MCDA-Benefits retrieval index** was refreshed on 2026-09-01 and again on 2026-10-15. The `EVAL-2026-089` RAG-triad eval has not been re-run against the new indexes (per the paired `mod-107` lab-01 fixture — the eval row has itself drifted into *evidence-stale* status; a Class-3 escalation `ESC-2026-LAB01-03` is open against it). The eval-report link on `CTL-2026-0344` therefore resolves to an eval whose own row is `escalated` as of this snapshot.
3. **`REG-2026-US-STATE-003` (Colorado AI Act)** consumer-notice provisions entered a new enforcement window on 2026-10-01; the `mod-106` regulatory-tracker row was updated 2026-10-03 to reflect the new window. The *last material change* field on the tracker is newer than the *last verified* date on controls that map to this regulation.
4. **A new sub-processor** was added by `VND-2026-0044` on 2026-10-22, in a jurisdiction (Jurisdiction Y) outside the enterprise's approved data-transfer footprint. The vendor published the new sub-processor on its trust site; the enterprise's DPA with `VND-2026-0044` does not reference Jurisdiction Y. `procurement` has not yet been notified by the enterprise-side process; the vendor has met its notification obligation via the trust-site update.
5. **A High-tier release of `INV-2026-0104` (contract-review-assistant)** shipped on 2026-10-28. The release-management system has a sign-off record attached (`EV-2026-1041`) with signer `release-mgmt-lead@` — *not* `ai-evaluation-engineer`. No paired `PACKET-<year>-<sequence>` identifier is on the record.
6. **The `INV-2026-0121` (HR-screening-assistant) annual bias audit** is due by 2026-11-10 (twelve months after the 2025-11-10 audit on record). As of 2026-11-14, no new audit report has been attached to the control record and no new publication URL has been captured. The HR-tech product owner reports that the audit vendor's engagement is in flight with report delivery expected 2026-11-28.
7. **The `INV-2026-0121` fairness-review note** annual refresh is due by 2026-11-15 (one year after the 2025-11-15 refresh). As of 2026-11-14, no refresh has been filed.
8. **ESC-2026-0051** (the Q3 class-1 escalation on `CTL-2026-0341`'s sampling rule) remains open; `senior-ai-governance-architect` has acknowledged but has not yet published a library-level fix. No resolving artefact identifier exists.

## Steps

### Step 1 — Scaffold the sweep log and the §6 draft (10 min)

Create the working folder and files.

```bash
mkdir -p ~/aicg-labs/mod-108-lab-01
cd ~/aicg-labs/mod-108-lab-01
touch sweep-log.md csr-section-6-stale-evidence-rollup.md escalation-register.md
```

Open `sweep-log.md` and lay in the structure up front.

```markdown
# Mid-cycle stale-evidence sweep — CSR-2026-Q4 drafting — 2026-11-14

Walker:       <your-name>
Sweep date:   2026-11-14
Record set:   CTL-2026-0341, CTL-2026-0344, CTL-2026-0347,
              CTL-2026-0352, CTL-2026-0355, CTL-2026-0361
Cadence:      Mid-cycle sweep against the four chapter-02 stale-evidence
              flag rules; CSR-2026-Q4 drafting with issuance 2026-12-15.

## Record-by-record walk

### CTL-2026-0341 — Jailbreak-classifier threshold + human-review queue
### CTL-2026-0344 — MCDA-Benefits RAG groundedness
### CTL-2026-0347 — AEDT bias-audit publication
### CTL-2026-0352 — Vendor DPA currency
### CTL-2026-0355 — High-tier release-assurance sign-off
### CTL-2026-0361 — Fairness-review note refresh on High-tier

## Escalations authored from this sweep

## Sweep verdict

## Pre-close completeness check
```

Open `csr-section-6-stale-evidence-rollup.md` and lay in the §6 skeleton.

```markdown
# CSR-2026-Q4 §6 — Stale-evidence roll-up (draft)

Period:                2026-10-01 → 2026-12-31 (drafting as of 2026-11-14).
Sweep date:            2026-11-14.
Walker:                <your-name>.
Pre-issuance review:   pending with senior-ai-governance-architect.

## Rows flagged — by rule

### Cadence-window rule
### Config-change rule
### Model-version-change rule
### Regulatory-obligation-change rule

## Rows walked clean (no flag tripped)

## Cross-reference to §5 escalations

## §6 verdict summary
```

Open `escalation-register.md` and lay in the entry-plus-register-table skeleton.

```markdown
# Escalations from the 2026-11-14 mid-cycle sweep

## ESC entries

## Register table
```

The three-file scaffold is what the reviewer reads to confirm the sweep ran; the per-record sub-sections carry the evidence and the §6 and the register carry the roll-ups.

### Step 2 — Apply the four flag rules to each record (20 min)

For each of the six records, compute which of the four chapter-02 flag rules has tripped against the walk date 2026-11-14 and cross-check against the Section-C change list. The flag rules are *independent* — a record can trip zero, one, or more than one. Record the per-record flag verdict in the sub-section of `sweep-log.md` as a four-line block:

```
cadence-window:              tripped | not-tripped — <reason>
config-change:               tripped | not-tripped — <reason>
model-version-change:        tripped | not-tripped — <reason>
regulatory-obligation-change: tripped | not-tripped — <reason>
```

Expected per-record flag verdict after this step — these drive what each later step does:

- **`CTL-2026-0341` — Jailbreak-classifier.** *cadence-window* not-tripped (last-verified 2026-08-20; quarterly cadence; mid-cycle re-test is this sweep). *config-change* tripped (MCDA system prompt v1.8 → v1.8.1 hot-fix on 2026-10-05 touched a file the Q3 config export was baselined against). *model-version-change* not-tripped (no model-version change). *regulatory-obligation-change* not-tripped (control is policy-anchored to `POL-2026-0018 §4`; no material change this quarter). Also carry forward the open `ESC-2026-0051` from Q3.
- **`CTL-2026-0344` — MCDA-Benefits RAG groundedness.** *cadence-window* tripped (monthly cadence; last-verified 2026-08-10 is beyond the monthly window). *config-change* tripped (retrieval index refreshed twice on 2026-09-01 and 2026-10-15 since last verified). *model-version-change* not-tripped (embedding and generation models unchanged per Section C event 2). *regulatory-obligation-change* not-tripped on this control directly (control is quality-anchored, not regulator-anchored). Additional: the cited `EVAL-2026-089` row has itself been escalated (`ESC-2026-LAB01-03` from the paired `mod-107` lab) — the eval-report-link evidence class is pointing at a row whose own status is `evidence-stale` + `escalated`.
- **`CTL-2026-0347` — AEDT bias-audit publication.** *cadence-window* tripped (annual cadence; the 2025-11-10 audit is at 12 months on 2026-11-10, which has passed as of 2026-11-14; publication URL dated 2025-11-15 is similarly over 12 months). *config-change* not-tripped (no config knob applies). *model-version-change* not-tripped. *regulatory-obligation-change* not-tripped on the Local Law 144 side (no material change in the current quarter); mark the in-flight 2026-11-28 audit delivery as an open follow-up, not as a trip.
- **`CTL-2026-0352` — Vendor DPA currency.** *cadence-window* not-tripped (annual; last-verified 2026-08-22; still within window). *config-change* not-tripped on the control-record side (DPA is not a config knob; the vendor-side sub-processor change is captured as a vendor-row event, which this control inherits via the per-vendor evidence). *model-version-change* not-tripped. *regulatory-obligation-change* tripped (the new sub-processor addition on 2026-10-22 in Jurisdiction Y is the on-event trigger named in the control statement; the DPA with `VND-2026-0044` does not reference Jurisdiction Y, so the evidence on the record is no longer consistent with the control statement).
- **`CTL-2026-0355` — High-tier release-assurance sign-off.** *cadence-window* not-tripped (on-release cadence; the Q3 evidence is scoped to Q3 releases). *config-change* not-tripped (not a config knob). *model-version-change* not-tripped (control-record level). *regulatory-obligation-change* not-tripped. However: the Q4 release of `INV-2026-0104` on 2026-10-28 attached a sign-off with the wrong signer and no paired `PACKET-<year>-<sequence>` identifier (Section C event 5) — this is a *fail* on the Q4 release instance, not a stale-evidence flag; record under findings, not §6.
- **`CTL-2026-0361` — Fairness-review note refresh.** *cadence-window* tripped (annual; the `INV-2026-0121` refresh is due 2026-11-15; as of 2026-11-14 the refresh is in the last-day window and has not been filed — the *last-verified* on the control record is 2026-08-19, but the *evidence's* 2025-11-15 refresh date is what the cadence runs from). *config-change* not-tripped. *model-version-change* not-tripped (fairness-review refresh is model-version-aware but no version has shipped on `INV-2026-0121` in-quarter). *regulatory-obligation-change* not-tripped. Record `INV-2026-0088` refresh dated 2025-12-02 as still within window (one year lands 2026-12-02).

Record the six per-record flag verdicts in the sub-sections of `sweep-log.md`.

### Step 3 — Assign the four-word verdict per record (15 min)

For each record, apply the chapter-03 four-verdict discipline against the flag verdicts from step 2 plus the evidence state. The verdict is one of *pass*, *fail*, *deviation*, *not-tested-in-period* — nothing else. Soften-words like *mostly-pass* / *pending* / *observed* are report-formatting failures per chapter 03.

Expected verdict assignments after this step:

- **`CTL-2026-0341`.** Verdict: *deviation*. Rationale: the config-change flag tripped (hot-fix touched the baselined knob); the Q3 deviation on `INV-2026-0104` sampling remains open via `ESC-2026-0051`; a fresh config export is required for `INV-2026-0088` under v1.8.1 before this control re-passes. Follow-up: re-pull config export on MCDA post-hot-fix (owner ML platform team; due 2026-11-21); keep `ESC-2026-0051` open.
- **`CTL-2026-0344`.** Verdict: *fail*. Rationale: the eval-report-link evidence class (`EVAL-2026-089`) is pointing at a row that is itself `evidence-stale` and under Class-3 escalation (`ESC-2026-LAB01-03`); the control cannot read as satisfied without a current eval against the deployed retrieval index. Follow-up: coordinate with `ai-evaluation-engineer` on the `EVAL-2026-089` re-run (per the paired `mod-107` lab escalation); re-test this control once the re-run completes (owner Internal Safety Eval Team; due 2026-12-15 or on re-run completion).
- **`CTL-2026-0347`.** Verdict: *deviation*. Rationale: the annual cadence has passed (audit-report evidence ≥ 12 months old; publication URL likewise); the vendor engagement is in flight with 2026-11-28 report delivery expected, so this is not a *fail* on the control's design intent — the enterprise is mid-engagement — but it is a *deviation* against the control statement's *within the past twelve months* wording until the fresh report and publication land. Follow-up: receive fresh audit report; capture new publication URL; obtain legal sign-off; re-test (owner HR-tech product owner; due 2026-12-05).
- **`CTL-2026-0352`.** Verdict: *fail*. Rationale: the new `VND-2026-0044` sub-processor in Jurisdiction Y means the DPA no longer reflects all current sub-processors; the control statement reads *names all current sub-processors*, which the evidence no longer supports. The on-event cadence specifically names *new sub-processor* as a trigger and that trigger has fired. Follow-up: route to `procurement` and `data-protection-officer` as a Class-3 escalation (the analyst does not redline the DPA); request *pause net-new use of `VND-2026-0044` pending resolution* as the interim-risk posture (the accountable executive decides whether to pause).
- **`CTL-2026-0355`.** Verdict: *fail*. Rationale: the 2026-10-28 release of `INV-2026-0104` has a sign-off recorded with the wrong signer (`release-mgmt-lead@` not `ai-evaluation-engineer`) and no `PACKET-<year>-<sequence>` reference — the control statement is explicit on both. The signature is not evidence if the signer was not the accountable party (chapter 02 failure mode). Follow-up: obtain the correct sign-off from `ai-evaluation-engineer`; attach the paired `PACKET-<year>-<sequence>`; file as a finding in §4 (owner Release management; due 2026-11-25).
- **`CTL-2026-0361`.** Verdict: *deviation*. Rationale: the `INV-2026-0121` refresh is at the last-day boundary of the annual cadence and has not been filed; the cadence-window has tripped but the control owner has not formally declared the refresh missed. A single-system deviation at the window boundary with named follow-up is *deviation*, not *fail*; a *fail* would require the window to have decisively passed without a follow-up path. `INV-2026-0088` refresh remains within window and does not contribute to the deviation. Follow-up: deliver the `INV-2026-0121` refresh with model-owner signed comment (owner Responsible-AI team; due 2026-11-21 — interpret as a one-week grace against a 2026-11-15 due date for an annual cadence).

Record each verdict in the sub-section of `sweep-log.md` with the one-paragraph rationale and the follow-up action, owner, and due date.

### Step 4 — Compose §6 — the stale-evidence roll-up (15 min)

Open `csr-section-6-stale-evidence-rollup.md` and fill in the four rule sub-sections with the records that tripped each rule plus the row that walked clean under *all four* rules. §6 is the chapter-03 stale-evidence roll-up — it names the rule, the controls that tripped it, and the resulting re-test date; it is *not* the findings section (that is §4).

- **Cadence-window rule.** `CTL-2026-0344` (monthly cadence; last-verified 2026-08-10; re-test on `EVAL-2026-089` re-run completion). `CTL-2026-0347` (annual; evidence at 12 months; re-test 2026-12-05). `CTL-2026-0361` (annual; `INV-2026-0121` refresh at boundary; re-test 2026-11-21).
- **Config-change rule.** `CTL-2026-0341` (MCDA system prompt v1.8 → v1.8.1 hot-fix 2026-10-05; re-test 2026-11-21). `CTL-2026-0344` (retrieval index v2026-06-15 → v2026-09-01 → v2026-10-15; re-test on `EVAL-2026-089` re-run).
- **Model-version-change rule.** None tripped this sweep; record explicitly as *none* rather than omitting the sub-section (omission reads as *not run*, not *not needed*, per chapter 03).
- **Regulatory-obligation-change rule.** `CTL-2026-0352` (new sub-processor 2026-10-22 in Jurisdiction Y; re-test on DPA / procurement resolution — Class-3 escalation `ESC-2026-LAB01-11`). Note the Colorado AI Act consumer-notice-provisions enforcement window (Section C event 3) opened 2026-10-01; no control in this sweep's subset maps directly to the consumer-notice provisions, so the trigger does not trip any record in scope — record this as a *tracker-change observed; no in-scope control affected* note so internal audit knows the walker looked.

- **Rows walked clean.** `CTL-2026-0355` — none of the four flag rules tripped; the control's Q4 failure is a release-instance *fail* in §4, not a §6 entry. Record under *rows walked clean* with a cross-reference to §4.

- **Cross-reference to §5 escalations.** List the escalation IDs from this sweep that §6 rows are routed under (`ESC-2026-LAB01-10`, `-11`, `-12`, and the carried-forward `ESC-2026-0051`; `ESC-2026-LAB01-13` and `-14` cover the other follow-ups).

- **§6 verdict summary.** Four or five sentences: *Mid-cycle sweep ran 2026-11-14 against six in-scope controls; five controls tripped one or more of the four stale-evidence flag rules (one tripped two rules); one control walked clean on all four; one carried-forward class-1 escalation (`ESC-2026-0051`) remains open from Q3 pending `senior-ai-governance-architect` resolution; six new escalations were filed (five tied to this sweep's findings and one tracking the Colorado AI Act regulator-tracker update that no in-scope control in this sweep carries directly). The sweep's stale-evidence findings feed §3 (verdict rollup) with the per-record verdicts from step 3, §4 (findings) with the follow-ups, and §5 (escalations) with the ESC entries. Model-version-change rule tripped on no record this sweep.*

### Step 5 — Author the escalation entries (20 min)

Open `escalation-register.md`. The sweep generates up to seven escalation entries plus one carried-forward entry; walk them in order and populate each with the chapter-9 template. Not every finding becomes an escalation — apply the chapter-9 threshold (recurs across periods, cross-role, out-of-window, cross-system, or exposes a library gap). Otherwise the item is a §4 finding with a follow-up, not an escalation.

Author the following entries using the per-class template:

- **`ESC-2026-0051` (carried forward from Q3, Class 1 — library-design fix).** Not re-authored; referenced in the register table with status *open — architect acknowledged, resolving artefact pending*. Flag the carry-forward age (filed 2026-08-25; open 81 days as of sweep date) so §5 of the report shows the pattern.
- **`ESC-2026-LAB01-10` — Class 1 library-design fix on `CTL-2026-0355`.** The *fail* on the 2026-10-28 release is a single-instance release-management failure resolvable by obtaining the correct sign-off — a §4 finding, not an escalation, on its own. But the *control statement specifies the signer by role and the enterprise's release-management system permitted a different signer to attach the sign-off record* is a library-plus-system design gap. File a Class-1 escalation requesting `senior-ai-governance-architect` and `release-management` review together whether the control statement should encode a system-enforced signer-role constraint. Rationale: a single release slipped past; the gap is that the system allowed it.
- **`ESC-2026-LAB01-11` — Class 3 vendor / contract action on `CTL-2026-0352` + `VND-2026-0044`.** Rationale: new sub-processor in Jurisdiction Y, outside approved transfer footprint, DPA does not reference the jurisdiction. Route to `procurement` and `data-protection-officer`; copy `ai-infra-security` for the security questionnaire follow-up; copy the technical owner for context. Requested action: *re-negotiate DPA to reflect the new sub-processor jurisdiction; request current ISO/IEC 42001 certification letter in case jurisdictional scope affects it; pause net-new use of `VND-2026-0044`-backed functions pending resolution*. Target: 2026-11-28. The analyst does not pause unilaterally — the request is *requested pause* and the accountable executive decides.
- **`ESC-2026-LAB01-12` — Class 1 library-design fix on `CTL-2026-0344`.** Rationale: the control's expected evidence class is *eval-report link*, and the `EVAL-2026-089` row it links to has itself drifted into *evidence-stale* under `ESC-2026-LAB01-03` (the paired `mod-107` lab escalation). The control cannot read current while the linked eval is stale; the library-level question is whether the control should encode a *linked-eval-currency* sub-check or trigger a re-test automatically on the linked row's status change. Route to `senior-ai-governance-architect` with the paired `mod-107` escalation attached.
- **`ESC-2026-LAB01-13` — Class 1 library-design fix on `CTL-2026-0361`.** Rationale: the control's annual cadence is month-of-anniversary; the two systems in scope (`INV-2026-0088` and `INV-2026-0121`) have anniversaries two weeks apart, creating a rolling cadence rather than a batched one. The *deviation* on `INV-2026-0121`'s 2026-11-15 refresh is single-instance; the library question is whether the control should batch annual refreshes onto a single quarterly review cycle to avoid single-system window boundaries. Route to `senior-ai-governance-architect`. This is a *pattern* escalation — a one-off slip does not itself warrant a Class 1, but the recurrence pattern across systems and across the two controls in-scope (`CTL-2026-0361` and `CTL-2026-0347` both run annual cadences with single-system triggers) does.
- **`ESC-2026-LAB01-14` — Class 1 library-design fix on `CTL-2026-0341` (joined with `ESC-2026-0051`).** Rationale: the hot-fix on 2026-10-05 touched a knob that the control's config-export evidence is baselined against, and the deployment process did not trip a re-test request to the analyst. The library-level question is whether on-change-triggered re-tests should post into the GRC platform's task queue automatically when the GitOps repo touches a flagged file. Join this escalation with `ESC-2026-0051` as a related-entry so `senior-ai-governance-architect` sees the full pattern.

Entries that are *not* authored as escalations — and why:

- The `INV-2026-0104` sign-off *fail* on `CTL-2026-0355` on its own is a §4 finding with a 2026-11-25 follow-up — single-release, named owner, clear remediation; apply the chapter-9 threshold *finding, not escalation*.
- The `CTL-2026-0347` annual-cadence *deviation* is a §4 finding with a 2026-12-05 follow-up — in-flight engagement, named owner; *finding, not escalation* on the control itself. The pattern escalation (`ESC-2026-LAB01-13`) covers the library-level cadence-design question across the two annual controls.
- The Colorado AI Act tracker change is noted in §6 as a *tracker-change observed; no in-scope control in sweep* note; the actual tracker-change-driven library re-anchoring runs through `mod-106` and `senior-ai-governance-architect`, not through this sweep.

### Step 6 — Project into the register table (10 min)

Below the entries in `escalation-register.md`, project them into the chapter-9 register-table shape.

```markdown
## Register table

| ID | Class | Source | Filed | Route | Status | Resolution | Impact on report |
|---|---|---|---|---|---|---|---|
| ESC-2026-0051 | 1 | CTL-2026-0341 (Q3 sweep) | 2026-08-25 | senior-ai-governance-architect | open — acknowledged, resolving artefact pending | — | carried forward into CSR-2026-Q4 §5; 81 days open |
| ESC-2026-LAB01-10 | 1 | CTL-2026-0355 2026-10-28 release | 2026-11-14 | senior-ai-governance-architect; release-management copied | open — awaiting owner response | — | CSR-2026-Q4 §5 |
| ESC-2026-LAB01-11 | 3 | CTL-2026-0352 + VND-2026-0044 | 2026-11-14 | procurement; data-protection-officer; ai-infra-security cc; technical owner cc | open — awaiting owner response | — | CSR-2026-Q4 §5; requested pause pending exec decision |
| ESC-2026-LAB01-12 | 1 | CTL-2026-0344 + EVAL-2026-089 | 2026-11-14 | senior-ai-governance-architect | open — awaiting owner response | — | CSR-2026-Q4 §5; cross-referenced to ESC-2026-LAB01-03 (mod-107 lab) |
| ESC-2026-LAB01-13 | 1 | CTL-2026-0361 + CTL-2026-0347 (pattern) | 2026-11-14 | senior-ai-governance-architect | open — awaiting owner response | — | CSR-2026-Q4 §5 |
| ESC-2026-LAB01-14 | 1 | CTL-2026-0341 on-change trigger | 2026-11-14 | senior-ai-governance-architect; joined with ESC-2026-0051 | open — awaiting owner response | — | CSR-2026-Q4 §5 |
```

The register is the chapter-9 first-class artefact. Auditors read it as the connective tissue between the control-status report's §5 and the library-level work that resolves the findings.

### Step 7 — Compose the sweep verdict (5 min)

Open the `## Sweep verdict` section at the bottom of `sweep-log.md`. Four or five sentences:

*Mid-cycle sweep ran 2026-11-14 across six control records against the four chapter-02 stale-evidence flag rules; five records tripped at least one flag (one tripped two rules), one walked clean. Verdicts: two passes-equivalent (one clean; one carried-forward escalation on an earlier deviation), three deviations (`CTL-2026-0341`, `CTL-2026-0347`, `CTL-2026-0361`), two fails (`CTL-2026-0344`, `CTL-2026-0352`), and one in-scope control (`CTL-2026-0355`) failing on a release-instance not covered by the four flag rules. Six new escalations filed — five Class 1 (library-design fixes on four controls plus a pattern escalation) and one Class 3 (vendor / contract action on `VND-2026-0044`); one Class 1 escalation carried forward from Q3. §6 of CSR-2026-Q4 is drafted; §4, §5, and §3 take the follow-ups from step 3 and the entries from steps 5 and 6. Next scheduled sweep: 2026-12-15 (full Q4 cycle close) or on any of (a) the hot-fix re-export completing, (b) the `EVAL-2026-089` re-run completing, (c) `VND-2026-0044` DPA resolving, (d) `INV-2026-0121` audit and fairness-review refresh landing — whichever is sooner. No Class 4 escalation was warranted by this sweep; the six Class 1 and Class 3 entries are all resolvable within the Q4 cycle window.*

### Step 8 — Self-check against the pre-close completeness block (5 min)

Chapter 03's report has a §6 stale-evidence roll-up whose content comes from this sweep; chapter 02's four flag rules are the discipline the sweep applies; chapter 09's escalation classes are the shape the sweep's findings file under. Walk the sweep log against the following four checks before closing:

1. **Every record walked, including those that trip zero flags.** Six records in scope; six per-record sub-sections populated; the one record (`CTL-2026-0355`) that walked clean under the four flag rules has an explicit *rows walked clean* entry in §6 and is cross-referenced to §4 for the release-instance *fail*.
2. **Every flag rule explicitly applied per record** — not inferred by silence. Each record's four-line flag block names each rule as *tripped* or *not-tripped* with a one-line reason. Confirm pass.
3. **Every verdict is one of the four words.** Walk the per-record verdict assignments from step 3; no *mostly-pass* / *pending* / *observed* language. Confirm pass.
4. **Every escalation has the per-class fields** — trigger source, affected systems, rationale, requested action, owner, target date, status. Six new entries plus one carried-forward in the register table; the Class 3 entry names the vendor ID; the Class 1 entries name the control IDs and (where applicable) the pattern they join. Confirm pass.

Record the four checks at the bottom of `sweep-log.md` as a short `## Pre-close completeness check` block.

## Expected output

Three Markdown files in `~/aicg-labs/mod-108-lab-01/`:

- `sweep-log.md` — one walk log with (a) six per-record sub-sections each recording the Section-C change-list cross-check, the four-line flag-rule block, the four-word verdict, the one-paragraph rationale, and the follow-up action / owner / due date; (b) an `## Escalations authored from this sweep` section naming the entries by ID with a one-line summary; (c) a `## Sweep verdict` paragraph; (d) a `## Pre-close completeness check` block.
- `csr-section-6-stale-evidence-rollup.md` — four rule-named sub-sections (with explicit *none* where no record tripped), a *rows walked clean* sub-section, a cross-reference to §5, and a four-or-five-sentence verdict summary.
- `escalation-register.md` — up to seven escalation entries using the chapter-9 per-class templates (one carried-forward summary, two to three full Class-1 entries, one Class-3 entry, and the joined / pattern entries), plus the chapter-9 register-table projection beneath.

Total length: roughly 2,000–3,000 words across the three files. A reviewer should be able to read all three in twenty minutes and see every record walked, every flag tagged, every verdict assigned, and every escalation routed.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did `CTL-2026-0341` get the *deviation* verdict (not *pass*) once the config-change flag tripped on the hot-fix?** Chapter 02's config-change rule trips the re-test regardless of cadence; the Q3 open escalation on sampling joins the config-change trip to make *deviation* the correct call. A silent *pass* carried over from Q3 would be the chapter-9 *silent-library-edit* failure mode.
2. **Did `CTL-2026-0344` read *fail* (not *deviation*) once the eval-report-link resolved to a row that is itself `evidence-stale`?** The chapter 02 failure-mode discipline treats evidence pointing at a stale upstream artefact as evidence-not-present for the control statement's purposes; the chapter 03 four-verdict discipline reads *evidence missing or inconsistent* as *fail*.
3. **Did `CTL-2026-0352` read *fail* (not *deviation*) once the new `VND-2026-0044` sub-processor fired the regulatory-obligation-change rule and the DPA did not name the new jurisdiction?** The control statement reads *names all current sub-processors*; the evidence no longer supports that claim. A sweeper who softens to *deviation* is the chapter-3 *verdict-language-drift* failure mode.
4. **Did `CTL-2026-0355` get a *fail* (not a *not-tested-in-period*) on the 2026-10-28 release's wrong-signer sign-off, with the finding in §4 and not in §6?** The on-release cadence fired for the Q4 release; the sign-off's wrong signer is a *fail* per chapter 02's sign-off-failure-mode discipline; §6 is only stale-evidence, not findings.
5. **Does every Class-1 escalation name the library-level question rather than proposing wording?** Chapter 09 is explicit — the analyst *raises the gap*, does *not* draft the control statement. A sweeper who proposes a new control wording to `senior-ai-governance-architect` is the chapter-7 *analyst suggests, architect decides* line crossed in the wrong direction.
6. **Is `ESC-2026-0051` carried forward in the register table and flagged for age?** Chapter 09's *registers that grow without triage* failure mode names this specifically; an 81-day-open Class-1 reads correctly only when the register table carries the age.
7. **Does any record's verdict read *mostly-pass* / *pending* / *observed*?** If yes, the sweep has drifted; the four-verdict discipline is the chapter-3 anchor and the first thing an internal auditor will call out.

If any of the seven is "no", revise *that artefact* before considering the lab done.

## Why this is a lab, not an exercise

The module's five exercises each drill *authoring from scratch* — exercise 01 authors a runbook and fresh test rows, exercise 02 authors OWASP tagging decisions on fresh artefacts, exercise 03 authors MITRE ATLAS / NIST AI 100-2 / SAIF reference composition, exercise 04 authors vendor intake rows, exercise 05 authors the crosswalk matrix. None of them asks the analyst to walk a *pre-filed control-record snapshot across a mid-cycle sweep* — which is the specific hour of work that converges chapter 02's stale-evidence flag rules, chapter 03's four-verdict discipline, and chapter 09's four escalation classes into the mid-cycle check between the full periodic cycle and the full report issuance. This lab is that convergence. The failure mode it prevents is the analyst who can author each artefact in isolation but has never once walked a record set that had drifted between cycles, applied the four flag rules explicitly rather than by silence, held the four-verdict discipline against the pull to soften, and filed the right escalation class per finding rather than batching everything to `senior-ai-governance-architect`.
