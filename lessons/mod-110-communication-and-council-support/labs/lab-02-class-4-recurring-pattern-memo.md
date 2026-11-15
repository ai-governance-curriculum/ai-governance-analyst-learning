# Lab 02 — Class-4 Recurring-Pattern Memo from Four Consecutive Council Cycles

**Duration:** 90 minutes.
**Grounding chapters:** [09](../09-delegation-boundary-and-escalation-patterns.md), [06](../06-first-cut-internal-ai-policies-and-standards.md), [04](../04-council-pre-read-deck-and-one-pager.md), [05](../05-council-minutes-that-survive-audit.md).
**Difficulty:** Core — exercises chapter 09's recurring-pattern promotion rule, the class-4 memo shape, and the chapter-09 → chapter-06 bridge (the memo is where the analyst's *first-cut drafting* voice meets the analyst's *council packaging* voice). The module's four exercises each drill a *different* authoring act. Exercise 02 asks the analyst to *identify* a class-4 recurring-pattern signal in a single meeting cycle and capture it as an action-item for a future memo — but it does *not* ask the analyst to compose the memo itself. This lab is that specific authoring act, run against four consecutive council cycles whose minutes show the pattern accumulating, so that the analyst can concentrate on the recognition-recurrence-promotion walk and the memo-drafting discipline rather than on inventing the pattern.

## Objective

Take four consecutive council-cycle minute summaries — drawn from the enterprise's AI governance council meetings on 2026-07-21, 2026-08-18, 2026-09-21, and 2026-10-19 — identify the recurring class-4 pattern they jointly reveal, apply the chapter-09 recognition-recurrence-promotion rule, and compose the analyst's class-4 pattern-recognition memo for the 2026-11-16 council. The memo lands on that council's standing-agenda item 8 (*policy and standard work in flight*) as the analyst-proposed standing-agenda entry for discussion and, if the council approves the routing, as the originating artefact for a first-cut policy-work item that `senior-ai-governance-architect` will take forward.

The deliverable exercises every chapter-09 rule the class-4 memo depends on: (i) the recognition rule (same class of problem across multiple meetings, systems, or content owners, where the fix is *not* another instance of the same operational action but a change to policy, standard, training material, tooling configuration, or role-clarity statement); (ii) the promotion rule (second recurrence notes the pattern in the pre-read *for information*; third recurrence promotes to class-4 with a proposed policy-work item; instance-count on the register after promotion tracks whether the policy-work is closing the pattern); (iii) the memo's substantive shape (the recurring incidents, their common cause, the operational cost of continuing to handle them one-at-a-time, the proposed policy-work item with the analyst's rough scope estimate); (iv) the delegation discipline (the analyst *raises the pattern*; the owning roles — `senior-ai-governance-architect` and `head-of-ai-governance` — set the policy direction from there).

The deliverable is a single Markdown file in `~/aicg-labs/mod-110-lab-02/`:

- `class-4-memo.md` — the analyst's class-4 pattern-recognition memo to `senior-ai-governance-architect` and `head-of-ai-governance`, with a copy on the 2026-11-16 council pre-read as standing-agenda item 8 for discussion.

A reviewer should be able to read the memo in fifteen minutes and see every chapter-09 rule applied: the pattern recognised and named precisely, the three (or more) instances cited by minute reference and underlying artefact ID, the common cause stated at the systemic-condition altitude rather than at the individual-incident altitude, the operational cost quantified, the proposed policy-work item named with a rough scope, and the recommendation phrased as a *recommendation* (what the memo asks the owning roles to do next) rather than as a *decision* (which the analyst does not take).

## Prerequisites

- Chapter 09 read; the four escalation classes, the class-4 trigger, the common class-4 patterns the chapter names, and the recurring-pattern promotion rule fresh in memory.
- Chapter 06 read; the first-cut drafting routing chain and the universal section shape — the memo's *proposed policy-work item* names which of the four canonical first-cut drafts (AUP, model-approval standard, third-party AI vendor review standard, generative-AI employee guidance) the policy-work target is, or names that the target is a *fifth* draft (a policy-section revision, a new standard section, a training material update, a tooling configuration, a role-clarity statement) that does not fit the four canonical shapes.
- Chapter 04 read; the standing-agenda spine and the way a class-4 memo lands on item 8 (policy and standard work in flight) as an analyst-proposed entry.
- Chapter 05 read; the five-field decision-record pattern — the memo cites the prior council decisions that related to the pattern by decision ID, so the owning roles can walk back from the memo to the decision records that preceded it.
- A Markdown editor; no Python, GRC, or vendor tooling required. The four minute summaries in Section A below are a Markdown-only stand-in for what would live in the enterprise's minute archive in production.
- Exercise 02 completed, or at minimum skimmed — the exercise asked the analyst to *identify* the class-4 signal in a single cycle; this lab assumes that recognition and drills the next step.

## The fixed input — four consecutive council-cycle minute summaries

Use *exactly* these minute summaries. Do not substitute identifiers, dates, versions, or evidence identifiers, and do not re-derive the underlying facts — the fixed state is the point of the lab. Treat the whole block as `pedagogic example — identifiers, numbers, and dates illustrative`. The four summaries are reproduced at the level of the fields the memo-drafter reads from; they do not reproduce every field verbatim.

### A. The four minute summaries

#### July 2026 — AI governance council, 2026-07-21

Chair: `head-of-ai-governance`. Secretary: analyst. Quorum met. Prior minutes (2026-06-16) approved.

Substantive items and decisions:

- **Agenda item 5 — IA sign-off pending.** `FRIA-2026-0049` on `INV-2026-0128` (HR-tooling-Phase-2, candidate-shortlisting assistant) returned for edits — the FRIA's *measure* section cites `CTL-2026-0044` (hiring-panel-review-of-every-shortlist) as the enveloping human-oversight measure; two council members (DPO, legal delegate) flagged that the FRIA does not say what happens if the hiring panel accepts the shortlist without reading it. Decision `DEC-2026-0066`: *returned for edits — FRIA owner to revise the measure section to specify an operating condition for the control, by 2026-08-18.*
- **Agenda item 9 — regulatory tracker.** New EU AI Act implementing-act draft on Article 27 FRIA-reporting obligations noted. Sequencing deferred to September cycle.
- **Agenda item 10 — escalation register.** `EXC-2026-0034` filed — a business line requested a standard-level exception to the model-approval standard's *mandatory human-oversight-measure-with-named-operating-condition* clause for a low-risk marketing-copy tool. Decision `DEC-2026-0067`: *exception approved for 90 days, pending the business line's documentation of an alternative measure. `senior-ai-governance-architect` to review the alternative by 2026-10-19.*

#### August 2026 — AI governance council, 2026-08-18

Chair: `head-of-ai-governance`. Secretary: analyst. Quorum met. Prior minutes (2026-07-21) approved.

Substantive items and decisions:

- **Agenda item 5 — IA sign-off pending.** `FRIA-2026-0049` (returned from July) re-presented. Revised *measure* section now cites `CTL-2026-0044` with an operating condition *"panel chair confirms each shortlist entry has been read against the role's criteria."* The DPO accepted; the legal delegate noted *"the control statement treats the panel chair's confirmation as a proxy for the panel's reading, which is not the same thing; consider revisiting on the next FRIA re-open."* Decision `DEC-2026-0073`: *signed off with conditions — Condition 1: FRIA owner to re-examine the operating-condition language at the next scheduled FRIA review (due 2027-02); Condition 2: `ai-governance-analyst` to raise the pattern for the council's attention if the legal delegate's concern recurs on another system's FRIA. `ACT-2026-0119` assigned to analyst.*
- **Agenda item 6 — residual-risk acceptance.** `RISK-2026-0117` on `INV-2026-0129` (content-moderation-Phase-1) — residual accepted with conditions. The enveloping measure cited in the risk register (`CTL-2026-0051`, human-reviewer-sampling-at-5-percent) was challenged by the fairness / responsible-AI SME on the grounds that *"5-percent sampling doesn't tell us what the other 95 percent of decisions look like"* — the risk owner argued the sampling methodology was signed off in the original FRIA. Decision `DEC-2026-0075`: *endorsed with conditions — risk owner to expand sampling to 10 percent for one quarter and report back. `ACT-2026-0122` assigned.*
- **Agenda item 10 — escalation register.** `ESC-2026-0220` opened — the September 2026 vendor review of `VND-2026-0019` identified that the vendor-supplied model-card does not describe the operating conditions under which the vendor's safety-evaluation results hold. Routed to `senior-ai-governance-architect` and copied to the AI governance council for awareness.

#### September 2026 — AI governance council, 2026-09-21

Chair: `head-of-ai-governance`. Secretary: analyst. Quorum met. Prior minutes (2026-08-18) approved.

Substantive items and decisions:

- **Agenda item 5 — IA sign-off pending.** `FRIA-2026-0054` on `INV-2026-0137` (Writing-Assistant-EU) re-opened following `INC-2026-0184`. Re-presented at v2. The *measure* section's *"human-review-of-every-output-before-filing"* language was discussed at length — three council members (chair, legal delegate, fairness SME) separately observed that the measure is phrased as an *intention* on the user's part rather than as an *operating condition* the control can test against; the fairness SME noted *"this is the third FRIA this quarter where the measure reads as an intention rather than a condition."* Decision `DEC-2026-0088`: *signed off with conditions — Condition 1: FRIA owner to revise *measure* section language to specify an operating condition the control can test, by 2026-11-16; Condition 2: `ai-governance-analyst` and `senior-ai-governance-architect` to consider whether this is a pattern across the enterprise's FRIAs and bring a recommendation to the 2026-11-16 council. `ACT-2026-0131` and `ACT-2026-0132` assigned.* The pattern was noted on the 2026-09-21 pre-read one-pager under *since-last-meeting* (second recurrence — per chapter 09, pattern is on the pre-read *for information*).
- **Agenda item 6 — residual-risk acceptance.** `RISK-2026-0131` on `INV-2026-0137` (Writing-Assistant-EU) — residual re-scored high 2026-08-04 → medium 2026-09-30; acceptance endorsed `DEC-2026-0088` (above).
- **Agenda item 10 — escalation register.** `EXC-2026-0041` opened — a second standard-level exception request against the model-approval standard's *mandatory human-oversight-measure-with-named-operating-condition* clause, from the HR-technology business line for a candidate-communication tool. Decision `DEC-2026-0092`: *exception deferred — pending the resolution of `ACT-2026-0132` (the pattern analysis). The council noted that a recurring exception pattern against the same clause suggests the clause may be misspecified.*

#### October 2026 — AI governance council, 2026-10-19

Chair: `head-of-ai-governance`. Secretary: analyst. Quorum met. Prior minutes (2026-09-21) approved.

Substantive items and decisions:

- **Agenda item 2 — action items from previous meetings.** `ACT-2026-0119` (analyst to raise FRIA pattern) — in-flight; on the agenda at 2026-11-16 per the September council's direction. `ACT-2026-0132` (analyst and architect to consider pattern) — in-flight; memo in preparation. `ACT-2026-0122` (risk owner to expand sampling to 10 percent on `RISK-2026-0117`) — complete; expanded sampling shows a modest segment skew the risk owner is investigating with the specialist tracks.
- **Agenda item 5 — IA sign-off pending.** `FRIA-2026-0059` on `INV-2026-0142` (customer-support-copilot-Phase-3) presented for sign-off. The *measure* section cites a new control `CTL-2026-0088` (support-agent-rework-queue) with the enveloping language *"support agents must review generated responses before sending."* The DPO observed *"this reads as an intention, not an operating condition — fourth instance of the pattern we've been tracking."* Decision `DEC-2026-0097`: *signed off with conditions — Condition 1: FRIA owner to revise the measure section once the pattern analysis (ACT-2026-0132) is complete, by 2026-12-15; Condition 2: no new FRIA to be presented for sign-off from 2026-11-16 onwards until the measure-section operating-condition expectation is clarified. `ACT-2026-0141` assigned.*
- **Agenda item 7 — incident and monitoring roll-up.** `INC-2026-0184` closure endorsed; the trust-site update covered in Lab 01 was directed at `DEC-2026-0098`.
- **Agenda item 8 — policy and standard work in flight.** Analyst noted that the class-4 memo (`ACT-2026-0132`) is in preparation and will land on the 2026-11-16 council pre-read as agenda item 8.
- **Agenda item 10 — escalation register.** `ESC-2026-0234` opened — the vendor review of `VND-2026-0019` (first noted at the August council as `ESC-2026-0220`) has not progressed; the vendor-supplied model-card still does not describe the operating conditions under which the vendor's safety-evaluation results hold. The analyst noted this is the same substantive gap (operating-condition language) that the FRIA pattern exposes; the council agreed with the connection and directed the analyst to include the vendor-review observation in the class-4 memo as a parallel pattern instance. `ACT-2026-0143` assigned.

### B. What the memo is (and is not)

The class-4 memo is a short analyst-authored document — chapter 09 is explicit on the memo's shape. The memo is *not* a policy draft, a standard draft, or a council pre-read item in its own right; it is the *originating artefact* that proposes a policy-work item for `senior-ai-governance-architect` and `head-of-ai-governance` to take forward. The memo is also *not* a reopening of any of the four prior council decisions; those decisions stand on the record. The memo *reads* those decisions for a shared pattern and proposes policy-work against that pattern.

The owning roles — `senior-ai-governance-architect` for policy-work scoping, `head-of-ai-governance` for council-tier endorsement — set the policy direction from the memo. The analyst's voice stops at *recommendation*; it does not pre-empt the owning roles' decision.

## Steps

### Step 1 — Scaffold the file (5 min)

Create the working folder and file.

```bash
mkdir -p ~/aicg-labs/mod-110-lab-02
cd ~/aicg-labs/mod-110-lab-02
touch class-4-memo.md
```

Open `class-4-memo.md` and lay in the header. Chapter 09's memo shape sits under a standard header the analyst uses for every class-4 escalation.

```markdown
# Class-4 Recurring-Pattern Memo — [Pattern Name]

Memo ID:             ESC-2026-<sequence> (class-4; recurring pattern → policy-work)
Prepared by:         [analyst name] — 2026-11-08
Prepared for:        senior-ai-governance-architect (owning role, policy-work scoping);
                     head-of-ai-governance (owning role, council-tier endorsement)
Copied to:           AI governance council (standing-agenda item 8, 2026-11-16 meeting)
Recurrence count:    [N instances; promotion threshold per chapter 09 is three]
Status:              first-cut; not a policy draft; proposes a policy-work item
Underlying pins:     DEC-2026-0066; DEC-2026-0073; DEC-2026-0088; DEC-2026-0097;
                     ACT-2026-0119; ACT-2026-0132; ACT-2026-0141; ACT-2026-0143;
                     ESC-2026-0220; ESC-2026-0234; EXC-2026-0034; EXC-2026-0041.
Related artefacts:   FRIA-2026-0049 (HR-tooling-Phase-2); FRIA-2026-0054
                     (Writing-Assistant-EU); FRIA-2026-0059 (customer-support-
                     copilot-Phase-3); RISK-2026-0117 (content-moderation-Phase-1);
                     VND-2026-0019 vendor-review record.
Not a policy draft:  This memo proposes a policy-work item; the owning roles
                     scope and draft any policy, standard, or guidance change
                     that follows.
```

Set the *recurrence count* field to the true number of instances the four minute summaries expose; the memo's promotion is already in motion (`ACT-2026-0132` was assigned at the third recurrence in September, consistent with chapter 09's rule), so the memo lands at *fourth recurrence or beyond*, with the memo as the artefact promised at the September promotion.

### Step 2 — Name the pattern precisely (15 min)

The memo's first substantive section is the pattern name and a one-paragraph statement of what the pattern *is*. The name is what every subsequent council pre-read will refer back to, so it must be specific enough to identify the pattern and general enough to cover every instance the memo lists.

Compose a `## Pattern` section. The pattern, read from the four minute summaries, is: *impact assessments (and, at least once, a residual-risk acceptance and a vendor-model-card review) are being signed off against **enveloping measures** whose **operating conditions** are not specified in a form that an operational control can test.* The measure reads as a user's or operator's intention (*"human-review-of-every-output-before-filing"*, *"panel chair confirms each shortlist entry has been read"*, *"support agents must review generated responses"*), not as an operating condition the control is verifying. The control passes on the process side (the human or the panel confirms); the outcome, where tested, fails more often than the measure's rhetorical envelope would predict.

Write the pattern in two or three sentences. Resist the temptation to list every instance in the pattern statement itself — the instance list lives in Step 3. The pattern statement names the *shape* of the recurring problem at the systemic-condition altitude.

A worked draft of the paragraph (compose your own wording; the substance should match):

> *The enterprise's impact assessments and, in parallel, its residual-risk acceptances and its vendor-model-card reviews are repeatedly signing off against enveloping human-oversight measures stated as intentions rather than as operating conditions. A measure phrased as "the panel will read the shortlist" or "support agents will review generated responses" is not testable against operations; the control the measure anchors passes on process confirmation (the panel confirms; the agent clicks the review button) while the outcome the measure was supposed to envelop fails in a non-zero fraction of cases. The gap between the measure's intentional phrasing and an operating condition the control can test is where incidents (`INC-2026-0184`) and residual-risk overruns (`RISK-2026-0117`) emerge.*

### Step 3 — Cite the instances by minute reference and artefact ID (10 min)

Compose an `## Instances` section as a bulleted or numbered list. Each instance cites the council minute's decision ID and the underlying artefact ID; no instance is listed by description alone. The chapter-09 promotion rule's *instance-count on the register after promotion* discipline requires that the running instance-count is derivable from the memo.

Draft the list. The fixed input in Section A exposes at least four instances:

1. **2026-07-21 (`DEC-2026-0066`) — FRIA-2026-0049 on INV-2026-0128 (HR-tooling-Phase-2).** FRIA returned for edits because the *measure* section cited a control whose operating condition was unspecified (what happens if the panel accepts the shortlist without reading it). Resolved at the following council with a measure-section revision (`DEC-2026-0073`) that two members still noted treated the panel chair's confirmation as a proxy for the panel's reading.
2. **2026-08-18 (`DEC-2026-0073`, Condition 2 → `ACT-2026-0119`) — FRIA-2026-0049 sign-off.** The legal delegate's note at this council — *"the control statement treats the panel chair's confirmation as a proxy for the panel's reading"* — is the first naming of the pattern as such. Condition 2 assigned the analyst the tracking.
3. **2026-09-21 (`DEC-2026-0088`, `ACT-2026-0132`) — FRIA-2026-0054 on INV-2026-0137 (Writing-Assistant-EU).** The third recurrence, which triggered the promotion (per chapter 09's rule: second recurrence notes in the pre-read for information; third recurrence promotes to class-4). The fairness SME's observation — *"this is the third FRIA this quarter where the measure reads as an intention rather than a condition"* — is the recognition on the record.
4. **2026-10-19 (`DEC-2026-0097`, `ACT-2026-0141`) — FRIA-2026-0059 on INV-2026-0142 (customer-support-copilot-Phase-3).** Fourth recurrence. The council directed that no new FRIA be presented for sign-off from the 2026-11-16 meeting onwards until the operating-condition expectation is clarified.
5. **Parallel instance: 2026-08-18 → 2026-10-19 (`ESC-2026-0220` → `ESC-2026-0234`, `ACT-2026-0143`) — VND-2026-0019 vendor-model-card review.** The vendor-supplied model-card does not describe the operating conditions under which the vendor's safety-evaluation results hold. The council at 2026-10-19 agreed the vendor-review observation is the same substantive gap and directed the analyst to include it in this memo.
6. **Related instance: 2026-07-21 → 2026-09-21 (`EXC-2026-0034` → `EXC-2026-0041`) — two standard-level exceptions to the model-approval standard's *mandatory human-oversight-measure-with-named-operating-condition* clause from two separate business lines (low-risk marketing-copy tool and HR-technology candidate-communication tool).** The recurring-exception pattern was explicitly noted at the 2026-09-21 council — *"a recurring exception pattern against the same clause suggests the clause may be misspecified"* — and `EXC-2026-0041` was deferred pending the pattern analysis this memo represents.

### Step 4 — Identify the common cause (15 min)

Compose a `## Common cause` section. Chapter 09's memo shape calls for the common cause at the *systemic-condition altitude*, not at the individual-incident altitude.

The analyst's reading from the four instances:

- The enterprise's FRIA methodology does not currently specify a form for the *measure* section's operating condition. The methodology (last updated 2025-12-01) states that measures should be *"human-oversighted"* and *"operationally feasible"* but does not require the measure to be phrased as an operating condition a control can test.
- The enterprise's model-approval standard's *mandatory human-oversight-measure-with-named-operating-condition* clause (added 2026-06; `DEC-2026-0051` on the model-approval standard v2.0 ratification) *does* require operating-condition language, but the standard's clause is not reflected in the FRIA methodology — the FRIA owners write the *measure* section against the FRIA methodology, not against the model-approval standard's clause.
- Two business lines independently filed standard-level exceptions to the model-approval standard's clause (`EXC-2026-0034`, `EXC-2026-0041`), consistent with the clause being misspecified or inconsistent with the FRIA methodology the enterprise's FRIA owners already follow.
- The vendor-review observation (`ESC-2026-0220`, `ESC-2026-0234`) extends the pattern beyond the enterprise's own FRIAs: a vendor's model-card documents measures the vendor is responsible for, with the same intentional-rather-than-operating-condition phrasing; the vendor-review standard does not currently require operating-condition language on vendor-supplied model-card measures.

State the common cause as two or three sentences at the systemic-condition altitude. A worked draft of the paragraph:

> *The enterprise's FRIA methodology and the enterprise's third-party AI vendor review standard do not require the **measure** section's human-oversight language to be stated as an operating condition that an operational control can test. The enterprise's model-approval standard **does** carry such a requirement but is inconsistent with the FRIA methodology the FRIA owners already follow, producing a standard clause that attracts recurring exceptions rather than enforcement. The gap between the intentional phrasing the FRIA methodology permits and the operating-condition phrasing the model-approval standard requires is the shared root cause of all six instances this memo cites.*

### Step 5 — Quantify the operational cost (10 min)

Compose an `## Operational cost` section. Chapter 09 asks the memo to name *the operational cost of continuing to handle them one-at-a-time* — the specific demand on the enterprise if the pattern continues without a policy-work resolution.

Honest costs the memo can name from the fixed input:

- **Each new instance consumes a council cycle.** The pattern has already consumed four full council cycles (July, August, September, October 2026) and two more are already queued (the November memo discussion and the December FRIA-2026-0059 revision); at the enterprise's one-hour council slot, this is roughly six hours of council time plus the preparation and follow-through cadence (per `mod-110` chapter 04, M − 14 through M + 5 per cycle, so roughly 20 analyst-hours per cycle for pre-read and minute work × six cycles, before counting contributor hours). The pattern is bottom-of-queue displacing other governance work.
- **The pattern is affecting operational decisions.** The 2026-10-19 council directed that *no new FRIA be presented for sign-off from 2026-11-16 onwards until the operating-condition expectation is clarified.* That is a direct and material impact on the enterprise's AI governance operation; new AI systems in `mod-102` intake are currently blocked at the `mod-105` FRIA sign-off step pending the policy-work this memo proposes.
- **The pattern is compounding at the vendor surface.** The vendor-review observation (`ESC-2026-0234`, open) is tracking the same gap on a third-party model-card, which the enterprise cannot resolve unilaterally — the enterprise will need to raise the operating-condition expectation with the vendor contractually, extending the pattern's operational cost into the contract-renewal cycle.
- **Recurring exceptions mask the pattern's prevalence.** Each exception filed (`EXC-2026-0034`, `EXC-2026-0041`) is presented at the council as a one-off; without the pattern analysis this memo carries, the exceptions would have been granted individually without the council recognising the shared root cause. Chapter 06 is explicit that *policy-exception requests recur for the same section → the section is misspecified in the policy and needs re-drafting rather than repeated exception-granting*.

Write the cost paragraph. Numbers should be honest estimates grounded in the fixed input; do not invent costs the fixed input does not support (e.g., no legal-exposure estimate; no customer-impact dollar figure; no regulator-risk score — none of those is in the fixed input).

### Step 6 — Propose the policy-work item (15 min)

Compose a `## Proposed policy-work item` section. Chapter 09 and chapter 06 together fix the shape: the memo proposes which of the four canonical first-cut drafts the policy-work targets, or names that the target is a different artefact (a policy-section revision, a standard-section revision, a methodology update, a training update, a tooling configuration, a role-clarity statement); the memo also carries the analyst's rough scope estimate.

A worked draft (analyst reads the pattern as a *methodology + standard-section reconciliation* problem spanning two owning documents):

> *The analyst proposes a coordinated two-document policy-work item:*
>
> *1. **Revision to the FRIA methodology** (`mod-105` chapter — not one of the four canonical first-cut drafts from `mod-110` chapter 06, but the enterprise's FRIA-methodology document the FRIA owners work against). The revision requires the measure section's human-oversight language to be stated as an operating condition that is testable by an operational control, with worked examples. The analyst's rough scope estimate: 2–3 weeks of `senior-ai-governance-architect` time plus cross-functional consultation (DPO, legal, business-line FRIA owners), routed through the chapter-06 four-phase chain; the first-cut draft can be originated by the analyst if the architect directs, but the methodology's owner (`senior-ai-governance-architect`) is the more usual author.*
>
> *2. **Reconciling revision to the model-approval standard** (the second canonical first-cut draft under `mod-110` chapter 06). The standard's *mandatory human-oversight-measure-with-named-operating-condition* clause is retained but re-worded to reference the revised FRIA methodology; the two recurring exceptions (`EXC-2026-0034`, `EXC-2026-0041`) are closed on the standard-revision ratification, with the exception register's history preserved per chapter 05's frozen-after-ratification rule. Rough scope estimate: 1–2 weeks of `senior-ai-governance-architect` time plus the usual consultation and ratification cadence.*
>
> *3. **Parallel update to the third-party AI vendor review standard** (the third canonical first-cut draft under `mod-110` chapter 06). The standard's vendor-supplied-artefacts requirements list is extended to require that vendor-supplied model-card measures be stated as operating conditions, with the fallback that where the vendor cannot, the enterprise's own operational control must carry the operating-condition statement. Rough scope estimate: 1 week of `senior-ai-governance-architect` time plus consultation with `procurement` and `legal` on the contract-clause implications for `VND-2026-0019` and similar vendor contracts.*
>
> *Total rough scope estimate for the coordinated policy-work: 4–6 weeks of `senior-ai-governance-architect` time plus the usual consultation and ratification cadence; the three artefacts ratify together so the FRIA methodology, the model-approval standard, and the third-party AI vendor review standard carry consistent operating-condition expectations.*

Chapter 09 is explicit that the memo *names the proposed policy-work with a rough scope*; the owning roles — `senior-ai-governance-architect` and `head-of-ai-governance` — scope definitively from there. The analyst does not commit the architect to the estimates; the analyst offers them as *rough* so the owning roles can agree, counter, or re-scope.

### Step 7 — Write the recommendation (10 min)

Compose a `## Recommendation` section. Chapter 09 asks the memo to end on *recommendation, not decision*. The recommendation names what the memo asks the owning roles to do at the 2026-11-16 council and, if endorsed, in the weeks after.

A worked draft:

> *The analyst recommends the 2026-11-16 AI governance council endorse the coordinated policy-work described in the previous section — the FRIA methodology revision, the model-approval standard reconciliation, and the third-party AI vendor review standard extension — with `senior-ai-governance-architect` scoping and routing per the chapter-06 four-phase chain and a target ratification date for the three artefacts of 2027-Q1. The analyst further recommends that the two deferred standard-level exceptions (`EXC-2026-0034`, `EXC-2026-0041`) remain deferred until the model-approval standard revision ratifies, rather than being individually re-reviewed, so that the exception register's instance count reflects the pattern's resolution path. The analyst will carry the running instance-count on the escalation register per chapter 09's instance-count-after-promotion discipline and will report instance-count status at each council cycle until the three artefacts ratify.*
>
> *This memo does not propose that the council decide the policy-work scope on 2026-11-16; the council's endorsement opens the policy-work routing, and `senior-ai-governance-architect` and `head-of-ai-governance` will take the scoping decisions from there.*

**Discipline checks before you stop writing this section.**

- *The recommendation is a recommendation.* The memo asks the council to *endorse* and the owning roles to *scope and route*; it does not pre-empt the architect's scoping call or the head of governance's ratification call. If the recommendation reads *"the council should adopt the revised FRIA methodology on 2026-11-16"* — strike. The council on 2026-11-16 cannot adopt a methodology that has not yet been drafted; it can endorse the policy-work path.
- *The recommendation carries the chapter-09 instance-count discipline.* The analyst commits to tracking the instance-count on the escalation register until the policy-work closes the pattern.
- *The recommendation does not carry a legal, contractual, or executive-committee ask.* The memo's audience is `senior-ai-governance-architect` and `head-of-ai-governance`, with the council as copy; it is not a legal advice request, a contract-renewal scoping memo, or an executive-committee briefing.

### Step 8 — Write the closing `## Analyst limits` block (5 min)

Chapter 09 and the chapter-08 self-check-block pattern together require that the memo names its own limits — what the memo does *not* cover, where the analyst's reading may be incomplete, and what the owning roles may find on deeper review. Add a short `## Analyst limits` block (2–4 sentences).

A worked draft:

> *This memo reads the pattern across four consecutive council cycles and the enterprise's FRIA methodology, model-approval standard, and third-party AI vendor review standard; it does not read the enterprise's broader HR-policy intersections (where the HR-technology business line's exception may reflect an HR-policy constraint the memo has not surfaced). The memo's instance count is anchored on council-minute references and may understate the pattern's prevalence across systems that have not yet reached council sign-off. The memo's rough scope estimates are the analyst's own and are not committed on `senior-ai-governance-architect`'s behalf; the architect may scope the policy-work differently.*

## Expected output

One Markdown file in `~/aicg-labs/mod-110-lab-02/`:

- `class-4-memo.md` — a class-4 pattern-recognition memo of roughly 1,500–2,500 words, with the header populated per Step 1, and with the six substantive sections populated per Steps 2–8: *Pattern*, *Instances*, *Common cause*, *Operational cost*, *Proposed policy-work item*, *Recommendation*, *Analyst limits*. Every instance in the *Instances* section cites the council minute's decision ID and the underlying artefact ID; the *Common cause* section stays at the systemic-condition altitude; the *Operational cost* section carries honest estimates grounded in the fixed input; the *Proposed policy-work item* section names which of the four canonical first-cut drafts the policy-work targets (or names that the target is a different artefact) with a rough scope estimate; the *Recommendation* section ends on recommendation, not decision; the *Analyst limits* block names the memo's limits honestly.

A reviewer should be able to read the memo in fifteen minutes and see every chapter-09 rule applied: the pattern recognised and named precisely at the systemic-condition altitude; the three (or more) instances cited by minute reference and underlying artefact ID; the common cause stated at the systemic-condition altitude; the operational cost quantified honestly; the proposed policy-work item named with a rough scope; the recommendation phrased as a recommendation rather than as a decision; the memo's limits named.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Does the *Pattern* section name the pattern at the systemic-condition altitude rather than at the individual-incident altitude?** If the pattern reads *"FRIA-2026-0054 has a bad measure section"*, it's at the wrong altitude — that is an instance, not a pattern. If it reads *"the enterprise's methodology does not require operating-condition language on measure sections"*, that is the pattern.
2. **Does every instance in the *Instances* section cite the council minute's decision ID and the underlying artefact ID?** An instance named by description alone (*"the HR system from July"*) is a chapter-09 traceability failure.
3. **Is the *Common cause* section stated at the systemic-condition altitude?** No individual-contributor blame (no *"the FRIA owner wrote the measure section carelessly"*); no team-level blame (no *"the HR-technology business line doesn't understand the standard"*). The common cause is about the enterprise's methodology and standards, not about the humans who wrote against them.
4. **Is the *Operational cost* section grounded in the fixed input rather than invented?** Council-cycle count, blocked FRIA sign-offs, open vendor-review escalation, deferred exceptions — these are visible in the minutes. A legal-exposure estimate, a customer-impact dollar figure, or a regulator-risk score are not — strike if they appear.
5. **Does the *Proposed policy-work item* section name which artefact(s) the policy-work targets?** Chapter 09 asks for the specific artefact; a memo that says *"we need better guidance"* without naming which document is a chapter-09 discipline failure.
6. **Is the rough scope estimate honest?** If the estimates read *"this is a quick fix"* or *"a few days"*, scrutinise — ratifying three coordinated artefacts through the chapter-06 four-phase chain is not a few days. If the estimates read *"this will take a year"*, equally scrutinise — the pattern is well-scoped and the policy-work does not require re-architecting the entire policy library.
7. **Does the *Recommendation* section end on recommendation, not decision?** *"The council should adopt the revised methodology on 2026-11-16"* is a decision (and in this case an impossible one — the methodology does not yet exist to adopt). *"The analyst recommends the council endorse the policy-work path, with `senior-ai-governance-architect` scoping from there"* is a recommendation.
8. **Does the *Recommendation* section carry the chapter-09 instance-count discipline?** The analyst commits to tracking the instance-count on the escalation register until the policy-work closes the pattern; if the recommendation does not say so, add it.
9. **Does the *Analyst limits* block name honest limits?** If the block reads *"the analyst has covered everything"*, the block has failed. The lab's four minute summaries do not, for example, reveal the HR-policy intersections or the vendor-contract text; the memo does not pretend to.
10. **Is the memo's recipient list correct?** `senior-ai-governance-architect` and `head-of-ai-governance` as primary; the AI governance council as copy via the 2026-11-16 pre-read's standing-agenda item 8. The memo is not addressed to `legal`, to `communications`, or to the executive committee — chapter 09's class-4 target role is specific.

If any of the ten is *no*, revise the memo before considering the lab done.

## Why this is a lab, not an exercise

The module's four exercises each drill a *different* authoring act. Exercise 01 drills six audience-adapted briefings from a fairness-review note; exercise 02 drills one full council-meeting cycle *including* the identification of a class-4 recurring-pattern signal and the capture of that signal as an action-item; exercise 03 drills the AUP first-cut; exercise 04 drills the certifications portfolio plan. None of the four asks the analyst to compose the class-4 memo itself — the specific chapter-09 artefact that sits between the *recognition* exercise 02 asks for and the *first-cut drafting* exercise 03 asks for. The class-4 memo is where the analyst's *first-cut drafting* voice meets the analyst's *council packaging* voice; it is also the artefact chapter 09 is most explicit about: *the memo may itself land as a standing-agenda item on the next council*. This lab is that specific authoring act, run against four consecutive council cycles whose minutes show the pattern accumulating, so the analyst practises the recognition-recurrence-promotion walk against a fixed baseline and composes the memo at the altitude chapter 09 requires. The failure mode this lab prevents is the analyst who identifies recurring patterns reliably but has never composed the memo that promotes the pattern into policy-work — and who, under pressure of a standing-agenda slot at the next council, ends up shipping a memo that blames an individual FRIA owner, a memo that fails to name which artefact the policy-work targets, a memo that ends on decision rather than recommendation, or a memo that promises the policy-work will ratify in a week without the chapter-06 routing chain.
