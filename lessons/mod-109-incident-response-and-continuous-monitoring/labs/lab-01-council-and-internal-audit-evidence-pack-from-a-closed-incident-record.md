# Lab 01 — Council and Internal-Audit Evidence-Pack Composition from a Pre-Assembled Closed Incident Record

**Duration:** 2 hours.
**Grounding chapters:** [08](../08-post-incident-evidence-packaging.md), [03](../03-incident-record-and-register-linkage.md), [04](../04-coordinating-impact-assessment-update.md), [05](../05-monitoring-dashboards-for-governance-signoff.md), [06](../06-monitoring-signal-escalation-patterns.md), [09](../09-delegation-boundary-and-escalation-patterns.md).
**Difficulty:** Core — exercises chapter 08's seven-section pack discipline against a fixed, pre-assembled closed incident record. The module's four exercises each drill a *different* authoring act (exercise 01 classifies twelve intake tickets; exercise 02 composes one `INC-<year>-<sequence>` record across intake, triage, post-mortem, and closure; exercise 03 composes a monthly monitoring-reading note; exercise 04 composes a quarterly PMS summary plus an Article 73 notification draft). None of them asks the analyst to compose the *post-incident evidence pack* that packages a closed record for the governance council and for internal audit — the chapter-08 artefact that is a *reading* of the record rather than a duplicate of it, dated and versioned, self-limiting, staying at the systemic-condition altitude, and audience-tailored on §1, §4 emphasis, and §7. This lab is that specific authoring act, run against a fixed, pre-assembled closed record so that the analyst can concentrate on the pack discipline rather than on re-authoring the underlying record.

## Objective

Take a *fixed, pre-assembled* closed incident record — composed in the weeks after closure from the record's state at 2026-11-07 17:00 Europe/Berlin — and produce two audience-tailored evidence packs: one for the governance council's standing meeting on 2026-11-20, and one for the internal-audit engagement scoping on 2026-11-28. Both packs share substantive content on sections 2, 3, 5, and 6; each tailors §1, §4 emphasis, and §7 per chapter 08's council-vs-internal-audit discipline. The deliverable demonstrates every chapter-08 rule: the pack *cites* rather than reproduces; it is *dated and versioned*; it *names its own limits* where the underlying state has moved or is incomplete; it *respects read-permission boundaries*; it stays at the *systemic-condition altitude* rather than translating technical error into individual blame; and the Section 7 recommendation is *phrased as recommendation, not decision*.

The deliverables are three Markdown files in `~/aicg-labs/mod-109-lab-01/`:

- `master-pack.md` — the seven-section master pack from which the two audience-tailored versions derive.
- `council-pack.md` — the council-tailored version with §1 and §7 re-pitched for the governance council and §4 emphasising the register and assessment interactions.
- `internal-audit-pack.md` — the internal-audit-tailored version with §1 re-pitched for an auditor with technical vocabulary, §4 emphasising the control-record interactions, §5 at deeper read-depth on the monitoring-reading notes, and §6 at audit-visible depth on the corrective / preventive action outcomes.

A reviewer should be able to read all three in thirty minutes and see every chapter-08 rule applied: the §1 one-page limit respected; the §2 timeline rows each citing an artefact ID; the §3 three-questions-plus-one-chapter-04-question narrative in analyst voice without jargon or blame; the §4 one-paragraph-per-affected-artefact walk; the §5 before / during / after monitoring context with placeholder panel-screenshot references; the §6 action table with status per row; the §7 recommendation that stops at recommendation rather than decision; and the audience-tailored differences between the two versions readable at a glance.

## Prerequisites

- Chapters 08, 03, 04, 05, 06, and 09 read; the seven-section pack shape (one-page summary; timeline; root-cause narrative in analyst voice; cross-reference walk; monitoring context; corrective and preventive actions; analyst recommendation), the composition discipline (self-contained-but-not-duplicative; dated and versioned; cites its own limits; respects read-permission boundaries; stays at the systemic-condition altitude), and the council-vs-internal-audit tailoring rules fresh in memory.
- A Markdown editor; no Python, GRC, or vendor tooling required — the closed record snapshot below is a Markdown-only stand-in for what would live in the GRC platform in production.
- Exercise 02 completed, or at minimum skimmed, so the `INC-<year>-<sequence>` row schema is familiar. The snapshot below reproduces the record at the level of the fields a pack-composer reads from; it does not reproduce every field verbatim.
- The MCDA (`INV-2026-0088`), the contract-review-assistant (`INV-2026-0104`), and any RAG-augmented system inventory rows from `mod-102` conceptually in mind; the snapshot references `INV-2026-0104`.

## The fixed input — a pre-assembled closed incident record

Use *exactly* this record state. Do not substitute identifiers, dates, versions, or evidence identifiers, and do not re-derive the underlying facts — the fixed state is the point of the lab. The record is reproduced at the level of the fields a pack-composer reads from. Treat the whole block as `pedagogic example — identifiers, numbers, and dates illustrative`.

### A. The closed incident record (state at 2026-11-07 17:00 Europe/Berlin)

```
INC-2026-0231 — hallucinated legal citation on the contract-review-assistant
  Status:                closed-with-open-follow-through (preventive action iv still in flight)
  Opened:                2026-09-04 16:52 Europe/Berlin
  Opened by:             [analyst-name]
  Closed:                2026-10-19
  Closed by:             [analyst-name]
  Surface of report:     customer complaint (law-firm partner; EU customer base)
  Source link:           [support-ticket-URL-2026-09-04]

  AI-specific class:     class 5 — hallucination-driven harm
  Reclassification:      2026-09-08 11:00 Europe/Berlin — class-1 model-regression
                         secondary suspected (by `ai-eval-engineer`); closed 2026-09-22
                         not-confirmed after re-eval on the extended reference set
  External-corpus ref:   closest-match shape — AIID's hallucinated-legal-citation cluster
                         (live lookup would surface a specific entry; not reproduced here)
  Classical cross-ref:   none

  Affected INV:          INV-2026-0104 (contract-review-assistant; RAG-based; High-tier)
  Affected RISK:         RISK-2026-0079 — residual re-scored high → medium post-guardrail
  Affected FRIA:         FRIA-2026-0033 — re-opened under chapter-04 Q3; v3 → v4 signed
                         2026-10-02 with the `human-review-of-every-output-before-filing`
                         measure re-scoped and a new `citation-provenance-guardrail`
                         measure added
  Affected IA / DPIA:    not-triggered — chapter-04 Q1/Q2/Q4 evaluated no; Q3 triggered
                         FRIA only; DPIA remains in force with no re-open rationale
  Affected EVAL:         EVAL-2026-0119-r2 — extended reference set with comparative-
                         clause-memo queries; current-model baseline landed 2026-09-22
  Affected CTL:          CTL-2026-0411 (human-review-of-every-output) — re-tested post-
                         incident; control-passes-but-outcome-failed pattern recorded
  Affected VND:          none (model provider's silent updates ruled out in the
                         reclassification close; vendor row unchanged)
  Affected PMS:          not-applicable — INV-2026-0104 is not currently in Annex III
                         scope; the record carries the *flag-for-scope-review* note on
                         the regulator-notification-status field

  Severity (specialist): SEV-2 — high; external-customer harm confirmed; legal exposure
                         open; set by `ai-eval-engineer` at triage 2026-09-07
  Availability state:    available — under-monitoring; no availability interruption in
                         the incident window
  Containment actions:
    2026-09-06 19:14     citation-must-be-retrieved guardrail deployed to production
                         (by: ML platform team)
    2026-09-08 09:00     customer-communication template drafted by `legal`
    2026-09-14 10:30     general customer notification sent
  Duration of impact:    2026-09-01 (first known use with fabricated citation) through
                         2026-09-06 19:14 (guardrail deployment); re-opened for
                         customer-notification-period handling 2026-09-08 → 2026-09-14
  Users/systems affect:  one firm confirmed harm; 12 firms with similar comparative-
                         clause-memo query patterns in the same 30-day window reached
                         out to; no additional confirmed-harm instances surfaced

  IA/FRIA/DPIA re-open:  triggered — FRIA-2026-0033 v3 → v4 completed 2026-10-02 per
                         chapter-04 walk protocol; sign-off by [FRIA-accountable-exec];
                         DPO consulted on DPIA no-re-open rationale
  Register re-open:      triggered — RISK-2026-0079 residual re-scored high 2026-09-08,
                         re-scored medium 2026-10-25 after two consecutive clean months
                         of guardrail-fire evidence; risk-owner re-accepted
  System-card update:    triggered — system-card-INV-2026-0104-v3 published 2026-09-30
                         with citation-provenance-guarantee claim; legal review 2026-09-26
  Customer notification: individual firm 2026-09-08; general customer base 2026-09-14
                         (both by product owner per `legal` template)
  Regulator notification: not-applicable — INV-2026-0104 not currently Annex III;
                         Article 3(49) walk recorded: (a) not-implicated — no bodily
                         harm; (b) not-implicated — not critical infrastructure;
                         (c) plausibly-implicated — access-to-justice if system were
                         Annex III, but current scope does not attach Article 73;
                         (d) not-implicated — no property or environmental harm.
                         Flag-for-scope-review note filed to `senior-ai-governance-
                         architect` and the compliance function.
  Control re-test:       CTL-2026-0411 re-tested 2026-09-20 — control-passes-but-outcome-
                         failed pattern recorded; EV-2026-1088 attached (the customer's
                         own confirmation they read the memo satisfies the process
                         control; the outcome failure drives library-design-fix)
  Escalation entries:    ESC-2026-0431 (chapter-9 class-1 library-design-fix on the
                         prompt-template-change-requires-eval control, open with
                         `senior-ai-governance-architect`; filed 2026-09-20);
                         ESC-2026-0455 (chapter-9 class-4 pattern-recognition —
                         *second class-5 hallucination-driven-harm against a RAG-based
                         tool within a rolling quarter* trigger from chapter 03; filed
                         2026-10-05 to the governance council, open — to be read at the
                         2026-11-20 council meeting this pack supports)

  Post-mortem ID:        PM-2026-0044 (ML platform team wiki; versioned)
  Post-mortem link:      [wiki-URL-PM-2026-0044-v2]
  Root cause (post-     The model produced a confabulated citation because the prompt
  mortem technical):    template asked for *"the most relevant precedent"* without
                        requiring the citation to be traceable to a retrieved document,
                        and the RAG configuration did not enforce a citation-provenance
                        check at generation time. The release-assurance eval's reference
                        set did not include comparative-clause-memo queries with case-
                        law-precedent asks, so the failure mode was not exercised at
                        pre-deployment.
  Contributing factors: evaluation gap (reference set did not include the query
                        shape); prompt-template drift (the *"most relevant precedent"*
                        language was added in a Q2 2026 edit without a corresponding
                        eval); guardrail gap (no citation-must-be-retrieved guardrail
                        in place before this incident)
  Corrective actions:
    i.   citation-must-be-retrieved guardrail permanent (completed 2026-10-02; owner
         ML platform team; evidence EV-2026-1021)
    ii.  prompt template reverted to a citation-must-be-in-retrieved-documents form
         (completed 2026-09-18; owner product owner; evidence EV-2026-1014)
    iii. internal reference set extended with comparative-clause-memo queries
         (completed 2026-09-22; owner `ai-eval-engineer`; evidence EVAL-2026-0119-r2)
    iv.  customer-communication programme and system-card update (notifications
         completed 2026-09-14; card published 2026-09-30; evidence EV-2026-1035,
         EV-2026-1052)
  Preventive actions:
    v.   prompt-template-change-requires-eval control authored into the master
         control library — in-flight with `senior-ai-governance-architect`; target
         2026-12-31; status escalation ESC-2026-0431 open
    vi.  citation-provenance-check pattern added to the RAG-application scaffold
         used by future systems — completed 2026-10-30 for the scaffold; adoption
         across other RAG-based systems scheduled for Q1 2027; evidence EV-2026-1079

  Closure rationale:    All corrective actions (i)–(iv) complete; preventive action (v)
                        is on a tracked open track with ESC-2026-0431; preventive
                        action (vi) is complete at the scaffold level with a scheduled
                        cross-system rollout. FRIA v4, register re-score, system-card
                        v3, customer notifications, and control re-test are all
                        complete and recorded. Residual-risk re-acceptance by the risk
                        owner (RISK-2026-0079) is in place; Article 3(49) walk is
                        recorded with the flag-for-scope-review note. Closure is
                        appropriate; pattern-recognition escalation ESC-2026-0455 is
                        open on the parallel track to the governance council.
```

### B. Related artefact identifiers (for Section 4 cross-reference walking)

```
INV-2026-0104    contract-review-assistant (RAG-based; High-tier; EU ~40% MAU)
RISK-2026-0079   residual-risk claim for INV-2026-0104 (currently medium)
FRIA-2026-0033   v4 current (signed 2026-10-02); v3 incumbent retained
EVAL-2026-0119-r2  extended release-assurance baseline (hallucination rate 0.4%,
                   groundedness 0.87 on extended reference set, refusal-rate 0.09)
CTL-2026-0411    human-review-of-every-output-before-filing (post-incident re-test)
PM-2026-0044     engineering post-mortem (v2)
ESC-2026-0431    chapter-9 class-1 library-design-fix (`senior-ai-governance-architect`)
ESC-2026-0455    chapter-9 class-4 pattern-recognition (governance council)
system-card-INV-2026-0104-v3  published 2026-09-30 (citation-provenance-guarantee)
MON-2026-06-INV-2026-0104    pre-incident monitoring-reading note (three-months-prior)
MON-2026-07-INV-2026-0104    pre-incident monitoring-reading note (two-months-prior)
MON-2026-08-INV-2026-0104    pre-incident monitoring-reading note (one-month-prior;
                                groundedness 0.83 against system-card ≥ 0.85 flagged
                                as a *warning* in that note — related exercise-03 shape)
MON-2026-09-INV-2026-0104    monitoring-reading note capturing the incident window
MON-2026-10-INV-2026-0104    monitoring-reading note after containment; guardrail-fire
                                rate 0.8%; groundedness 0.86 restored
```

### C. Two downstream audiences and their scheduled reads

- **Governance council — standing meeting on 2026-11-20, 09:00 Europe/Berlin.** `head-of-ai-governance` convened. Attendees include the Chief Product Officer, General Counsel, the Chief Risk Officer, the head of HR-technology (as the enterprise's most AI-exposed business unit), the chair of the audit committee, and the enterprise's Board-nominated non-executive member with AI-literacy. None has read the incident record in full; some remember the general shape of the September customer complaint; none has read PM-2026-0044. ESC-2026-0455 is on the standing agenda for this meeting as item 4 (policy discussion on recurring class-5 hallucination-driven-harm against RAG-based tools).

- **Internal audit — engagement scoping on 2026-11-28.** The internal-audit lead has opened a scoping engagement covering *"AI-system incident response and continuous monitoring: Q3–Q4 2026 operating effectiveness"*. The lead has requested the evidence pack for `INC-2026-0231` as a specimen pack and will use it to scope the engagement's depth, request further evidence artefacts per their own `mod-108`-informed sampling plan, and test the claims the pack makes (the corrective actions completed on the dates stated; the FRIA update sign-off landed; the register re-score is in the register; the system-card v3 is published and legally reviewed). The lead reads technical vocabulary and will walk every cited artefact.

## Steps

### Step 1 — Scaffold the three files (10 min)

Create the working folder and files.

```bash
mkdir -p ~/aicg-labs/mod-109-lab-01
cd ~/aicg-labs/mod-109-lab-01
touch master-pack.md council-pack.md internal-audit-pack.md
```

Open `master-pack.md` and lay in the chapter-08 seven-section skeleton.

```markdown
# INC-2026-0231 — Post-Incident Evidence Pack (master)

Pack ID:              PACK-2026-INC-2026-0231-v1
Composed:             2026-11-08 by [analyst-name]
Composed-against:     INC-2026-0231 state as of 2026-11-07 17:00 Europe/Berlin
Underlying-pin:       [GRC-platform-record-URL-INC-2026-0231@2026-11-07T17:00Z]
Audience (this file): master — the single source of truth from which the
                      council-pack and internal-audit-pack derive.
Pack limits (this     Preventive action (v) (prompt-template-change-requires-eval
version):             control authoring) is open with `senior-ai-governance-architect`
                      under ESC-2026-0431 as of pack compose date; a v2 pack will
                      incorporate the architect's resolution.

## §1 — One-page summary

## §2 — Timeline

## §3 — Root-cause narrative in analyst voice

## §4 — Cross-reference walk

## §5 — Monitoring context (before / during / after)

## §6 — Corrective and preventive actions

## §7 — Analyst recommendation
```

Open `council-pack.md` and `internal-audit-pack.md` and mirror the skeleton with the audience in the header. The two audience-tailored packs *share* the master's §2, §3, §5, and §6 content; they differ on §1, §4 emphasis, and §7.

The three-file scaffold is the structure the reviewer reads to confirm every section is present. The audience-tailored differences are scoped — not a free re-draft.

### Step 2 — Compose §1 (the one-page summary) — master version (10 min)

Open `master-pack.md` §1. The one-page limit is hard (~500 words). Cover, in this order:

- **What happened.** One sentence in factual voice — no root-cause claim, no responsibility assignment. *A customer of the contract-review-assistant filed a memo citing a case that did not exist; the model had confabulated the citation.*
- **When.** Awareness 2026-09-04 16:52 Europe/Berlin; containment 2026-09-06 19:14; closure 2026-10-19; preventive action (v) open as of pack compose date 2026-11-08.
- **What system.** `INV-2026-0104` (contract-review-assistant) — one-line description.
- **How it was surfaced.** Customer complaint from an EU law-firm partner.
- **Immediate impact.** One firm confirmed harm; 12 firms with similar query patterns reached out to; no additional confirmed-harm instances. The Article 3(49) walk is recorded on the record with the flag-for-scope-review note (the system is not currently Annex III; if it were, outcome class (c) would plausibly implicate).
- **What the enterprise did.** Guardrail deployed within 50 hours of awareness; FRIA re-opened and signed v4; register residual re-scored (high 2026-09-08 → medium 2026-10-25 after two clean guardrail-fire months); system card v3 published with citation-provenance-guarantee; customer notifications individual 2026-09-08 and general 2026-09-14.
- **What changed as a result.** Four corrective actions complete (`EV-2026-1021`, `EV-2026-1014`, `EVAL-2026-0119-r2`, `EV-2026-1035`/`EV-2026-1052`); one preventive action complete at scaffold level (`EV-2026-1079`); one preventive action open with `senior-ai-governance-architect` under `ESC-2026-0431`.
- **What remains open.** Preventive action (v) — the *prompt-template-change-requires-eval* control; target 2026-12-31. Pattern-recognition escalation `ESC-2026-0455` open to the council as a standing agenda item on 2026-11-20.
- **What decision the reader is being asked to make.** *(Audience-tailored — leave the master version at "information-only, with the pattern-recognition escalation ESC-2026-0455 on the 2026-11-20 council agenda as item 4"; the council pack and internal-audit pack will re-pitch.)*

Respect the one-page limit. If it overruns, the pack has the wrong altitude — tighten before proceeding.

### Step 3 — Compose §2 (the timeline) — shared across both audiences (15 min)

Open `master-pack.md` §2. The timeline is a factual chronological table from awareness to closure. Every row cites the underlying artefact; silent gaps are called out rather than omitted. Use this table template and populate against the record state above:

```markdown
| Time (Europe/Berlin) | Event | Actor | Artefact |
|---|---|---|---|
| 2026-09-04 14:23 | Customer first observed the fabricated citation in a filed memo | Customer (law-firm partner) | — |
| 2026-09-04 16:52 | Incident record opened at intake (T0 of the record) | Analyst | INC-2026-0231 |
| 2026-09-04 17:30 | Legal looped in by the account executive | Account executive / Legal | — |
| 2026-09-06 19:14 | citation-must-be-retrieved guardrail deployed to production | ML platform team | EV-2026-1021 (deployment record) |
| 2026-09-07 16:00 | Triage: `ai-eval-engineer` confirmed class-5; severity SEV-2 set; class-1 secondary suspected (retained pending re-eval) | ai-eval-engineer | INC-2026-0231 (triage update) |
| 2026-09-08 09:00 | Individual-firm customer-communication template drafted by legal | Legal | EV-2026-1035 (notification record) |
| 2026-09-08 11:00 | FRIA Q3 evaluation returned triggered (human-review-of-every-output measure technically met but outcome failed) | Analyst | INC-2026-0231 field update |
| 2026-09-08 — | Register residual re-scored high (RISK-2026-0079) | Risk owner | RISK-2026-0079 re-score record |
| 2026-09-14 — | General customer-base notification sent | Product owner per legal template | EV-2026-1052 |
| 2026-09-18 — | Prompt template reverted; corrective action (ii) complete | Product owner | EV-2026-1014 |
| 2026-09-20 — | ESC-2026-0431 filed (class-1 library-design-fix); CTL-2026-0411 re-test logged with control-passes-but-outcome-failed pattern | Analyst | ESC-2026-0431; EV-2026-1088 |
| 2026-09-22 — | Class-1 secondary (model-regression) not-confirmed after re-eval on extended reference set; reclassification history logged | ai-eval-engineer | INC-2026-0231 reclassification entry; EVAL-2026-0119-r2 |
| 2026-09-30 — | System card v3 published with citation-provenance-guarantee (legal review 2026-09-26) | Product owner / Legal | system-card-INV-2026-0104-v3 |
| 2026-10-02 — | FRIA v3 → v4 signed off; corpus entry updated; v3 retained as versioned prior | FRIA accountable executive | FRIA-2026-0033-v4 |
| 2026-10-02 — | Corrective action (i) guardrail permanent; corrective action (iv) notifications complete | ML platform team; product owner | EV-2026-1021; EV-2026-1035; EV-2026-1052 |
| 2026-10-05 — | ESC-2026-0455 filed (class-4 pattern-recognition — second class-5 hallucination-driven-harm against a RAG-based tool within a rolling quarter) | Analyst | ESC-2026-0455 |
| 2026-10-19 — | Record closed-with-open-follow-through | Analyst | INC-2026-0231 closure rationale |
| 2026-10-25 — | Register residual re-scored medium after two consecutive clean guardrail-fire months | Risk owner | RISK-2026-0079 re-score (2nd) |
| 2026-10-30 — | Preventive action (vi) complete at the scaffold level; cross-system rollout scheduled Q1 2027 | ML platform team / senior-ai-governance-architect | EV-2026-1079 |
| 2026-11-08 — | Evidence pack composed (this document) | Analyst | PACK-2026-INC-2026-0231-v1 |
```

Silent gaps between 2026-09-14 and 2026-09-18, between 2026-09-22 and 2026-09-30, and between 2026-10-02 and 2026-10-05 are not actually silent — the enterprise was waiting on specific signals (customer response window; legal review on the system card; the second class-5 pattern becoming visible after the second parallel incident landed). Add a one-line note under the table characterising each gap honestly rather than leaving the reader to guess.

Copy the completed §2 verbatim into `council-pack.md` and `internal-audit-pack.md`.

### Step 4 — Compose §3 (the root-cause narrative in analyst voice) — shared across both audiences (15 min)

Open `master-pack.md` §3. The chapter-08 shape is three questions plus one chapter-04 question, un-technical, three-to-five sentences total, no blame.

- **What condition made the incident possible?** *The release-assurance evaluation reference set did not include comparative-clause-memo queries with case-law-precedent asks, so the failure mode — the model confabulating a plausible-looking citation under a prompt template that asked for "the most relevant precedent" without requiring the citation to be traceable to a retrieved document — was not exercised before deployment. The RAG configuration did not enforce a citation-provenance check at generation time, so when the confabulation occurred there was no mitigation to catch it.*
- **What made it happen at the time it did?** *A customer in the EU customer base used the tool for a comparative-clause memo on limitation-of-liability — a query shape outside the evaluation reference set — and the model produced a response citing a fabricated case with a verbatim quotation and page number. Three other citations in the same response were real and correctly quoted, so the fabricated citation was camouflaged among correct output.*
- **What allowed it to reach a user or downstream system?** *The FRIA's "human-review-of-every-output-before-filing" measure was technically met — the customer confirmed reading the memo before filing — but the measure did not envelop the case where a reader with sound reading habits does not spot a plausible-looking fabrication in text they otherwise trust; the control that encoded the measure (`CTL-2026-0411`) therefore passed as a process control while the outcome failed. No downstream guardrail layer was in place to catch the confabulated citation at generation time.*
- **What did the enterprise assume that turned out to be false?** *The enterprise assumed that human review of every output would catch the class of failure the FRIA was designed around — specifically, that a human reader using the tool for a task within its approved scope would spot an incorrect factual claim before filing. The incident falsified that assumption on the specific sub-class of plausible-looking legal citations in text the reader was otherwise comfortable with. Chapter-04's Q3 — a measure-section commitment rendered inoperative — triggered the FRIA re-open.*

The narrative stops here. The engineering post-mortem's technical detail (the specific prompt-template language, the specific retrieval-augmentation configuration, the specific guardrail architecture) stays in `PM-2026-0044`; the pack cites rather than reproduces. No engineer, team, or individual customer is named; blame — if anywhere — belongs in the post-mortem, not the governance pack.

Copy the completed §3 verbatim into `council-pack.md` and `internal-audit-pack.md`.

### Step 5 — Compose §4 (the cross-reference walk) — master version (15 min)

Open `master-pack.md` §4. The chapter-08 shape is one paragraph per affected artefact, in the order a governance reader thinks about them. Walk:

- **The system (`INV-2026-0104`).** One paragraph — governance status (High-tier per `mod-102`), current FRIA v4 and current `EVAL-2026-0119-r2` baseline, EU customer base share, the system's role as a RAG-based legal-drafting assistant used by law firms.
- **The register (`RISK-2026-0079`).** One paragraph — the residual-risk claim's pre-incident state (medium), the incident's implication (the claim rested on human-review-of-every-output as an enveloping measure), the re-scoring trajectory (high 2026-09-08 → medium 2026-10-25 after two clean months of guardrail-fire evidence), and the risk-owner's re-acceptance.
- **The assessments (`FRIA-2026-0033`; DPIA not-triggered rationale).** One paragraph per — FRIA re-open trigger (chapter-04 Q3), update timeline (15-working-day default met), sign-off completion (2026-10-02), and what the v4 added (segment-monitoring cadence plus a citation-provenance-guardrail measure plus a re-scoping of the human-review measure); DPIA no-re-open rationale (chapter-04 Q1/Q2/Q4 all no; Q3 triggered FRIA only).
- **The evaluations (`EVAL-2026-0119-r2`).** One paragraph — the release-assurance eval the sign-off cited, the evaluation-gap finding (the reference set did not include the query shape), and the current-model baseline against the extended reference set.
- **The controls (`CTL-2026-0411`).** One paragraph — the human-review-of-every-output control statement, the post-incident re-test outcome (passed on the process side, the control-passes-but-outcome-failed pattern recorded), and the `mod-108` library-design-fix escalation (`ESC-2026-0431`) that follows.
- **The vendors.** One paragraph — the model provider's silent updates were ruled out as a contributing factor during the reclassification close (class-1 model-regression secondary not-confirmed); the vendor row is unchanged; no vendor-relationship action follows from this incident.
- **The PMS record.** One paragraph — `INV-2026-0104` is not currently in Annex III scope; the Article 3(49) walk is complete on the record (a/b/d not-implicated; c plausibly-implicated-if-Annex-III-scope); a flag-for-scope-review note was filed to `senior-ai-governance-architect` and the compliance function. Article 73 does not attach at the current scope.

Every paragraph cites the underlying artefact ID.

### Step 6 — Compose §5 (the monitoring context) — shared across both audiences, with depth-level audience note (15 min)

Open `master-pack.md` §5. The chapter-08 shape is three monitoring-reading notes before, the panel state at awareness, and two notes after.

- **Before (`MON-2026-06`, `MON-2026-07`, `MON-2026-08`).** Walk each one-paragraph: what the note showed, whether it contained an unheeded escalation trigger (the August note's groundedness-below-system-card-claim *warning* is exercise-03's shape — it was flagged but had not yet crossed the two-consecutive-month escalation threshold; the first two were clean readings), and whether the three notes revealed a pattern in retrospect (groundedness was trending down from July; the August warning was the first *below-published-claim* reading; the September incident would have been consistent with that trend if the extended-query-shape had been monitored, which it was not).
- **During (incident window 2026-09-04 → 2026-09-06).** Panel state at awareness per the September note's detail — groundedness, refusal-rate, cost, drift values at the moment the customer complaint landed. Note that *no dashboard alert fired* for the specific confabulated-citation failure — the panels tracked groundedness but did not specifically monitor citation-provenance before the guardrail (added 2026-09-06). Reference the screenshots-of-record with placeholder markers (see §7 below in this lab's step 8).
- **After (`MON-2026-09`, `MON-2026-10`).** September note captured the incident window and the containment (guardrail firing at 0.8%); October note confirmed groundedness restored to 0.86, guardrail-fire rate stable, no new confabulation reports. The *reading-was-done-but-the-escalation-was-not* pattern does *not* apply here — the September reading was concurrent with the incident, not preceding-but-unescalated; the August *warning* was filed, not missed.

Add a one-line audience note at the bottom of §5 in the master: *"The internal-audit pack walks each monitoring-reading note in deeper detail; the council pack stays at the pattern level."* This is the audience hook the two tailored versions will pick up.

### Step 7 — Compose §6 (corrective and preventive actions) — shared across both audiences (10 min)

Open `master-pack.md` §6. The chapter-08 shape is a table from the record's *corrective* and *preventive* action fields with a status column:

```markdown
| Action | Type | Owner | Target date | Status | Resolving artefact |
|---|---|---|---|---|---|
| (i) citation-must-be-retrieved guardrail permanent | corrective | ML platform team | 2026-10-02 | complete | EV-2026-1021 |
| (ii) prompt template reverted | corrective | Product owner | 2026-09-18 | complete | EV-2026-1014 |
| (iii) extended reference set | corrective | ai-eval-engineer | 2026-09-22 | complete | EVAL-2026-0119-r2 |
| (iv) customer-communication programme + system-card update | corrective | Product owner / Legal | 2026-09-30 | complete | EV-2026-1035; EV-2026-1052; system-card-INV-2026-0104-v3 |
| (v) prompt-template-change-requires-eval control authoring | preventive | senior-ai-governance-architect | 2026-12-31 | in-flight | ESC-2026-0431 (open) |
| (vi) citation-provenance-check pattern in RAG scaffold | preventive | ML platform team | 2026-10-30 (scaffold); Q1 2027 (adoption) | complete (scaffold) / in-flight (adoption) | EV-2026-1079 |
```

Note the distinction: *corrective* fixes the specific instance; *preventive* stops the class. Preventive actions named but not yet complete are called out explicitly — the audience wants to know what the enterprise learned versus what the enterprise merely committed to.

Copy the completed §6 verbatim into `council-pack.md` and `internal-audit-pack.md`.

### Step 8 — Compose §7 — master version (10 min)

Open `master-pack.md` §7. The chapter-08 shape is a paragraph-length recommendation, in three parts:

- **What the analyst thinks the enterprise should consider.** *The analyst recommends the enterprise consider whether the evaluation reference sets for RAG-based legal-drafting tools adequately cover the comparative-clause-memo-with-case-law-precedent query shape, and whether the prompt-template-change-requires-eval control (preventive action (v)) should be scoped not just to this system but across the enterprise's RAG-based tool portfolio.*
- **What the analyst recommends against.** *The analyst recommends against a blanket-policy restriction on the contract-review-assistant's output to citations the user retrieved themselves — the FRIA's expressive-use scope and the tool's utility to customers in the comparative-clause-memo workflow weigh against that posture; the citation-must-be-retrieved guardrail already enforces provenance at generation time without restricting legitimate use.*
- **What the analyst commits to doing next.** *The analyst will re-open the FRIA at the next scheduled cycle regardless of whether `ESC-2026-0431` resolves on target, and will carry forward the pattern-recognition observation (second class-5 hallucination-driven-harm against a RAG-based tool within a rolling quarter — `ESC-2026-0455`) into the 2026-Q4 PMS summary cycle for whichever systems in scope the pattern reaches.*

The recommendation stops here. The analyst does not pre-empt the council's or the auditor's judgement; the §7 is analyst voice, honestly stated.

### Step 9 — Tailor the council pack (10 min)

Open `council-pack.md`. The chapter-08 council-pack tailoring is on §1, §4 emphasis, and §7.

- **§1.** Re-pitch the last line: *"The council is being asked to read the pattern-recognition escalation `ESC-2026-0455` as agenda item 4 of the 2026-11-20 standing meeting. The council is not being asked to re-litigate the closed incident."* Keep the one-page limit; drop any detail the council-level reader does not need (e.g., specific evidence identifiers like `EV-2026-1021` — the council-pack §1 can summarise as *"four corrective actions complete; two preventive actions, one complete and one in-flight"*).
- **§4 emphasis.** Keep the seven-paragraph structure but *re-weight* — expand the register (`RISK-2026-0079`) and assessment (`FRIA-2026-0033`) paragraphs to half-again their master length, and compress the control (`CTL-2026-0411`) and evaluation (`EVAL-2026-0119-r2`) paragraphs to a single sentence each. The council reads the register and the assessments as their primary governance vocabulary; the control and eval detail the council does not usually walk.
- **§7.** Re-pitch for a council audience. *"The analyst recommends the council consider — in the context of agenda item 4 — whether the enterprise's prompt-template-change-requires-eval control should be scoped across the RAG-based tool portfolio rather than only on this system, and whether a shorter re-review cadence on High-tier RAG systems' evaluation reference sets would be proportionate to the pattern observed."* The analyst's commitment-to-do-next from the master §7 remains unchanged.

Add a *pack length* line at the top: *"Council pack: ~8 pages of which §1 is the one-page read-first artefact; §2–§7 are the walk-through."* This matches chapter-08's 8-to-12-pages typical.

### Step 10 — Tailor the internal-audit pack (15 min)

Open `internal-audit-pack.md`. The chapter-08 internal-audit-pack tailoring is on §1 (technical-vocabulary reader needing governance framing), §4 emphasis (control-record interaction), §5 depth (deeper walk on monitoring-reading notes as evidence of continuous-monitoring operation), §6 depth (audit-visible confirmation of action outcomes), and §7 (the analyst's recommendation framed for the auditor).

- **§1.** Re-pitch the last line: *"The internal-audit lead is being asked to use this pack as a specimen for the 2026-11-28 engagement scoping; the pack cites every underlying artefact by ID so the audit sample can be drawn directly from the citations."* Keep the one-page limit; the internal-audit-pack §1 names specific evidence identifiers because the auditor will follow them.
- **§4 emphasis.** Keep the seven-paragraph structure but expand the control (`CTL-2026-0411`) paragraph — walk the control-passes-but-outcome-failed pattern in full, cite `ESC-2026-0431` as the library-design-fix follow-through, and name the re-test evidence identifier `EV-2026-1088`. The register and FRIA paragraphs stay at master length. The evaluation paragraph expands to describe the extended reference set and its baseline values. The internal-audit-pack §4 is the auditor's sampling-frame starting point.
- **§5 depth.** Expand each monitoring-reading note's paragraph — for the three *before* notes, walk the specific metric values the note recorded against the system-card and eval-evidence baselines; for the September *during* note, cite the panel-state screenshots with placeholder references; for the October *after* note, cite the restoration-of-groundedness value. The chapter-08 internal-audit rule is that the auditor reads the monitoring-reading notes as evidence of the enterprise's continuous-monitoring assurance operation — the internal-audit pack's §5 gives the auditor what they need to assess that operation.
- **§6 depth.** Leave the table unchanged but add a *verification note* below each row naming where the audit sample should look to confirm the completion claim: *"(i) guardrail permanent — verify against the production change-management record referenced in EV-2026-1021 and against the panel-state in MON-2026-10"*; *"(iv) customer-communication programme — verify the individual firm notification against EV-2026-1035 and the general notification against EV-2026-1052; verify the system-card-v3 publication date against system-card-INV-2026-0104-v3's version-control history"*. Each verification note gives the auditor the specific sample path.
- **§7.** Re-pitch for the auditor: *"The analyst recommends the internal-audit engagement consider whether the control-passes-but-outcome-failed pattern on `CTL-2026-0411` is a `mod-108` library-design finding (as the analyst has filed under `ESC-2026-0431`) or whether the audit's independent reading supports a stronger finding on the enterprise's control-library design discipline more broadly."* The analyst's commitment-to-do-next from the master §7 remains unchanged.

Add a *pack length* line at the top: *"Internal-audit pack: ~15 pages; the auditor will read every section."* This matches chapter-08's 10-to-20-pages typical.

### Step 11 — Dating, versioning, limits, read-permission self-check (5 min)

Chapter-08 discipline closes with four composition rules. Walk each self-check at the bottom of `master-pack.md` as a short `## Composition self-check` block:

1. **Dating and versioning.** Every file has the compose date and the pack ID (`PACK-2026-INC-2026-0231-v1`); every file's header names the underlying-pin (`INC-2026-0231@2026-11-07T17:00Z`); if the underlying record changes after today, a v2 pack ships. Confirm present on all three files.
2. **Self-limiting.** The pack's limits are named in each file's header — specifically, preventive action (v) is in-flight with `senior-ai-governance-architect` and a v2 pack will incorporate the architect's resolution. Confirm present.
3. **Read-permission boundaries.** The reporting-party personal-data-adjacent details (the law-firm name, the specific filing details, counsel names) are *not* on any of the three files — they stay in the incident record where the read-permission model controls access. The pack describes the customer as *"an EU law-firm partner"* and the filing as *"a comparative-clause memo on limitation-of-liability"* without naming either. Confirm present.
4. **Systemic-condition altitude.** No engineer, team, or specific individual is named as the cause of the incident in any file; the §3 narrative stays at the systemic-condition level; any individual naming in §2 is role-tagged (e.g., *"ML platform team"*, not *"engineer X"*). Confirm present.

If any of the four self-checks fails, revise the relevant file before considering the lab done.

## Expected output

Three Markdown files in `~/aicg-labs/mod-109-lab-01/`:

- `master-pack.md` — seven sections, ~2,500–3,500 words, with the composition-self-check block at the bottom. Every section carries artefact-ID citations; §7 is a paragraph-length recommendation in three parts (consider / recommend-against / commit-to-next).
- `council-pack.md` — seven sections, ~8 pages (roughly 2,000–2,500 words). §1 one-page summary tailored for the council audience ending with the standing-meeting agenda item; §4 emphasis re-weighted to register / assessment paragraphs; §7 re-pitched to recommend council-level considerations. §2, §3, §5, §6 identical to master.
- `internal-audit-pack.md` — seven sections, ~15 pages (roughly 3,500–5,000 words). §1 tailored for the internal-audit lead ending with the specimen-pack framing for the 2026-11-28 engagement scoping; §4 emphasis re-weighted to control / evaluation paragraphs; §5 at deeper depth with per-note metric walks; §6 with per-row verification notes giving the auditor sample paths; §7 re-pitched for the auditor. §2, §3 identical to master.

Total length across the three files: roughly 8,000–11,000 words. A reviewer should be able to read all three in thirty minutes and see every chapter-08 rule applied: the §1 one-page limit respected per audience; the §2 timeline rows each citing an artefact ID; the §3 narrative in analyst voice without jargon or blame; the §4 one-paragraph-per-affected-artefact walk; the §5 before / during / after monitoring context with placeholder panel-screenshot references; the §6 action table with status per row and (internal-audit version) verification notes; the §7 recommendation stopping at recommendation rather than decision; and the audience-tailored differences on §1, §4 emphasis, and §7 readable at a glance.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Does §1 fit on one page in every pack?** Chapter-08 is explicit: *the one-page summary is a hard limit; if it does not fit, the pack has the wrong altitude*. A §1 that spills to two pages is a chapter-08 failure mode; tighten the detail that belongs in §2–§6.
2. **Does every §2 timeline row cite an artefact ID?** Rows with no artefact ID are either the T0 awareness row (no internal artefact) or a composition error. Chapter-08's discipline is that the timeline is factual, not narrative.
3. **Does §3 stay at the systemic-condition altitude?** No engineer is named; no team is blamed; the narrative reads the post-mortem and translates the technical root cause into governance vocabulary without reproducing technical specifics. Chapter-08's *does not translate technical error into governance blame* line is the test.
4. **Does §4 walk every affected artefact by paragraph?** The seven paragraphs (system, register, assessments, evaluations, controls, vendors, PMS) are each one paragraph in the master; the council pack re-weights to register + assessments; the internal-audit pack re-weights to controls + evaluations. A §4 that collapses to a bullet list is off-side.
5. **Does §5 call out the pattern-reading-was-done-but-escalation-was-not as *does-not-apply* rather than silently omitting?** The August *warning* was filed, not missed; the chapter-08 discipline is that the pattern is addressed in the pack even when it does not apply.
6. **Does §6 distinguish corrective from preventive by type column?** Corrective fixes the instance; preventive stops the class. A §6 that collapses both into a single *actions* type is a chapter-08 discipline failure.
7. **Does §7 recommend rather than decide?** The analyst's §7 uses *recommend*, *consider*, and *commits to doing next*; a §7 that reads *"the council should adopt"* or *"the audit should find"* has crossed into decision-taking.
8. **Is the composition self-check populated with all four rules?** Dating/versioning; self-limiting; read-permission boundaries; systemic-condition altitude. A pack that ships without the self-check is a chapter-08 process failure.
9. **Does the council pack avoid naming specific `EV-*` evidence identifiers in §1?** The council reader does not walk evidence identifiers directly — the council pack summarises; the internal-audit pack names them.
10. **Does the internal-audit pack name specific `EV-*` evidence identifiers and give the auditor the sample-path verification notes in §6?** The internal-audit lead will follow every citation; the pack's job is to give them the path.

If any of the ten is "no", revise *that artefact* before considering the lab done.

## Why this is a lab, not an exercise

The module's four exercises each drill a *different* authoring act — exercise 01 classifies twelve intake tickets; exercise 02 composes one `INC-<year>-<sequence>` record across intake, triage, post-mortem, and closure; exercise 03 composes a monthly monitoring-reading note; exercise 04 composes a quarterly PMS summary plus an Article 73 notification draft. None of them asks the analyst to compose the *post-incident evidence pack* from a fixed closed record — the specific chapter-08 artefact that is a *reading* of the record rather than a duplicate, dated and versioned, self-limiting, audience-tailored on §1, §4 emphasis, and §7, and stopped at the systemic-condition altitude. This lab is that specific authoring act. The failure mode it prevents is the analyst who can author every underlying artefact (the record, the monitoring-reading note, the PMS summary) in isolation but has never once packaged a closed record for a council audience alongside an internal-audit audience — and who, under pressure of a 2026-11-20 council slot and a 2026-11-28 audit scoping, ends up shipping the same pack to both audiences, or shipping a pack that reproduces the record rather than reading it, or shipping a §3 narrative that blames an engineer, or shipping a §7 that pre-empts the council's decision.
