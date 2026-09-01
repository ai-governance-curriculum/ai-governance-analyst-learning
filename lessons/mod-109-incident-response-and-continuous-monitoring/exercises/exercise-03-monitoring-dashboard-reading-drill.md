# Exercise 03 — Monitoring Dashboard Reading Drill

**Estimated effort:** 2 hours
**Grounding chapters:** [05 — Reading Continuous-Monitoring Dashboards for Governance Sign-off](../05-monitoring-dashboards-for-governance-signoff.md), [06 — Monitoring-Signal Escalation Patterns](../06-monitoring-signal-escalation-patterns.md), [01 — The Analyst's Scope on Incident Response and Continuous Monitoring](../01-analyst-scope-on-incident-response-and-monitoring.md), [09 — Delegation Boundary and Escalation Patterns](../09-delegation-boundary-and-escalation-patterns.md).

## Objective

Practise the analyst-tier *reading* verb on continuous-monitoring dashboards, produce the monthly monitoring-reading note per the shape chapter 05 fixes, exercise the cross-panel reading rules that turn signals into governance interpretations, and open the correct escalations under chapter 06's classes when a signal warrants one.

The drill is dashboard-reading-based: given a set of panel-state snapshots across the four families (drift, quality, safety, cost) for one live AI system across two consecutive reading periods, the deliverable is (a) the monitoring-reading note per chapter 05's shape (header, four-family paragraphs, governance interpretation, attachments), (b) the cross-panel readings that the signals collectively support, (c) the escalations opened under chapter 06's classes, and (d) a short review of dashboards or panels the analyst *cannot* read and the `mod-108` control-testing findings that follow.

The drill's point is that reading is not designing. The analyst does not choose the metric, tune the threshold, or judge whether a specific value is *good enough*; the analyst reads the panel against the referenced assessments, register, and eval-evidence baselines, reads *across* panels to catch what one panel in isolation would miss, and produces the governance-tier interpretation the council or internal auditor needs to sign off (or not). After this exercise you should be able to sit down with any live AI system's dashboards on the last working day of the month and, within 60–90 minutes, produce a monitoring-reading note that another analyst can pick up cold.

## Prerequisites

- Chapter 05 read; the four panel families (drift with the four subclasses; quality with the task-family metrics; safety with the guardrail-plus-refusal-plus-agent-plus-user-report signals; cost with the per-request / per-outcome / traffic-mix signals), the analyst-tier reading depth per family (*read the panel against the referenced assessments, register, and eval-evidence baselines*; defer metric choice, threshold tuning, and root cause), the five cross-panel reading combinations (drift-up + quality-down; quality-down + safety-up; safety-up + cost-up; cost-down + quality-down; cost-up + drift-up but quality-stable), the monitoring-reading note shape (header; four-family paragraphs; governance interpretation with three levels; attachments), and the LLM-specific reads (prompt-drift; retrieval-index freshness; chain-length / turn-count; tool-call denial rate; model-version pin state) fresh in memory.
- Chapter 06 read; the escalation-trigger tables per panel family (drift → `ai-risk-engineer` if segment threshold crossed; quality → `ai-eval-engineer` if eval-evidence baseline diverged; safety → `ai-infra-security` if guardrail-fire-rate spikes with cost-up; cost → `ai-infra-mlops` if unexplained), the escalation-record shape, and the four escalation-class assignments (Class 1 model-behaviour; Class 2 security; Class 4 governance-council).
- Chapter 09 read; the four escalation classes and the file-up threshold (recurrence across periods, cross-role action, cross-window, cross-system, or exposing a process gap).
- Chapter 01 read; the three tangible outputs (incident record, monitoring-reading note, PMS summary) and the delegation-map preview.
- Your `mod-102` inventory row for the system you are reading (MCDA `INV-2026-0088`, MCDA-Benefits `INV-2026-0311`, contract-review-assistant `INV-2026-0104`, or the equivalent from your carried-forward corpus), your `mod-105` FRIA / IA with the *measures* section (the referenced assessment the note compares against), your `mod-103` register entry with the residual-risk claim (the referenced register entry the note compares against), and your `mod-107` release-assurance eval-evidence row (the referenced eval-evidence baseline the note compares against).
- Familiarity with at least one continuous-monitoring platform's panel shape. Chapter 05's tooling landscape includes vendor platforms (Arize, Fiddler, WhyLabs, Datadog LLM Observability, New Relic AI Monitoring), open-source tools (Evidently, DeepEval, Ragas, TruLens, Phoenix, Langfuse, OpenLLMetry), and internal-built dashboards. The analyst does not master any specific tool; the analyst reads whatever tool the enterprise runs. If you have used none, read the [Evidently AI documentation on ML monitoring taxonomies](https://docs.evidentlyai.com/), the [Ragas RAG-triad documentation](https://docs.ragas.io/), and the [OpenLLMetry conventions](https://www.traceloop.com/openllmetry) before starting so the panel-shape references make sense.

## Problem statement

The deliverable is a **single Markdown file, `mod-109-ex-03-monitoring-note.md`**, containing the monitoring-reading note for the system-and-periods scenario below plus the parallel artefacts (escalations, control-testing findings, cross-panel readings) the reading triggers.

### The scenario (self-contained)

The system under reading is your carried-forward RAG-based system (contract-review-assistant `INV-2026-0104` if you completed exercise 02, MCDA `INV-2026-0088` otherwise). The reading periods are **2026-07 (July)** and **2026-08 (August)**. Panel snapshots below are for August; July values are provided for trend comparison.

Referenced artefacts (use your specific IDs from `mod-102`–`mod-108`; the placeholders below are examples):

- Inventory row: `INV-2026-0104` (contract-review-assistant).
- FRIA: `FRIA-2026-0033` version 4, current, with *measures* including *human-review-of-every-output-before-filing* (post-exercise-02) and *citation-provenance-guardrail* (post-exercise-02).
- Register entry: `RISK-2026-0079` with residual *medium* post-2026-10-08 re-score (see exercise 02).
- Release-assurance eval-evidence: `EVAL-2026-0119-r2` with baseline hallucination rate 0.4% on the extended reference set, groundedness 0.87, refusal-rate 0.09 on the internal jailbreak-attempt corpus, task-completion rate 0.83 on scripted-task suites.
- System card: `system-card-INV-2026-0104-v3` published 2026-09-30, claiming groundedness ≥ 0.85 and citation-provenance-guarantee.

**Panel snapshots — August 2026 reading period (compare to July values in brackets).**

**Drift panel (owner: `ai-eval-engineer`; platform: Evidently-on-internal).**

- Feature-level PSI on the top five input features: 0.04 [0.03], 0.06 [0.05], 0.08 [0.07], 0.14 [0.09], 0.11 [0.10]. Alert threshold: 0.15. FRIA-cited segment threshold: 0.15 on any segment named in the FRIA's *scope* section.
- Segment PSI on the two demographic segments the FRIA cites (US-East-Coast-firms, EU-DACH-firms): 0.07 [0.06], 0.13 [0.09]. Second segment upward trend across three consecutive months.
- Embedding-drift score on retrieved-document embeddings: 0.06 [0.05], stable.
- Prediction drift (distribution of *cite-count* per response): 0.09 [0.07], mild upward trend.

**Quality panel (owner: `ai-eval-engineer`; platform: Ragas-on-Langfuse).**

- Groundedness (rolling-30-day): 0.83 [0.86]. Baseline: 0.87 per `EVAL-2026-0119-r2`. System-card claim: ≥ 0.85. **Below system-card claim.**
- Context precision: 0.79 [0.81]. Baseline: 0.82.
- Context recall: 0.85 [0.87]. Baseline: 0.86.
- Answer relevance: 0.88 [0.88]. Stable.
- Hallucination rate (measured per the internal reference set): 0.5% [0.4%]. Baseline: 0.4%. **Slight uptick; still below the 1% incident threshold.**
- Human-review overturn rate (from customer-side workflow telemetry, opt-in): 3.1% [2.4%]. No baseline (this signal is new post-exercise-02); upward trend.

**Safety panel (owner: `ai-infra-security`; platform: Datadog LLM Observability).**

- *Citation-must-be-retrieved* guardrail fire-rate: 0.8% of responses [not-yet-deployed]. Post-exercise-02 guardrail; no baseline; the fire-rate is the metric the guardrail's operating evidence produces.
- Output-filter fire-rate on the acceptable-use-policy classifier: 0.02% [0.02%]. Stable.
- Refusal-rate on the internal jailbreak-attempt corpus: 0.94 [0.93]. Baseline: per `EVAL-2026-0119-r2`, 0.09 refusal on prohibited-use prompts. Note: the two numbers are complements of each other — 0.94 refusal on jailbreak-attempts is *high*; 0.09 refusal on prohibited-use prompts is the specific eval-evidence baseline. Refusal-appropriateness (false-refuse rate on the reference-set benign inputs): 0.03 [0.02], mild uptick.
- Trust-and-safety escalation volume: 2 [0]. Two customer-reported outputs flagged for review this month; both dispositioned as *within policy* on manual review.

**Cost panel (owner: `ai-infra-mlops`; platform: internal FinOps + provider billing feed).**

- Cost per completed memo: $1.42 [$1.31]. Upward 8% month-over-month, no obvious cause named on the panel.
- Tokens per response: 3,150 [2,880]. Upward 9%.
- Cache-hit rate: 0.62 [0.68]. Downward 6 percentage points.
- Provider mix: 100% provider A (unchanged from July).
- Requests per hour distribution: baseline daily pattern, no anomalous spikes.

**LLM-specific reads.**

- Prompt-drift: system prompt last edited 2026-09-08 (exercise-02 corrective action reverting the *"most relevant precedent"* language). No further edits in August period.
- Retrieval-index freshness: last full refresh 2026-08-01. Delta refreshes daily. Retrieval-index-size: +2.1% month-over-month (new statute updates and new appellate opinions added).
- Chain-length / turn-count: mean 3.2 tool calls per memo [2.9]. Distribution has a right-tail extending to 12 tool calls (July max was 8).
- Tool-call denial rate: 0.4% [0.3%]. No specific tool implicated.
- Model-version pin state: pinned to *provider-A-model-v4.7.2*; the pin is holding per the panel.

### Step 1 — Compose the monitoring-reading note header (§1)

Author a **§1 Note header** section that populates every field in chapter 05's header table:

- Note ID (`MON-2026-08-INV-2026-0104` or equivalent per your inventory row).
- Reading period (2026-08-01 through 2026-08-31).
- Inventory row (your `INV-<year>-<sequence>`).
- Analyst (name / placeholder).
- Composed on (the last working day of the period + one, or your equivalent cadence).
- Assessment reference (`FRIA-2026-0033` version 4).
- Register reference (`RISK-2026-0079`, current residual).
- Eval-evidence reference (`EVAL-2026-0119-r2`).
- System-card reference (`system-card-INV-2026-0104-v3` published 2026-09-30 — for the September+ reading; for August only, note the pre-publication state).

If any header field's value has changed since the July reading period, call out the change explicitly under a *what changed since last period* line — chapter 05 was explicit that silent baseline updates are a fail.

### Step 2 — Compose the four-family reading (§2)

Author a **§2 Four-family reading** section with one paragraph per family per chapter 05's shape (current state; consistency with referenced assessments and evaluations; what escalated; analyst confidence).

- **Drift (§2.1).** State the current drift snapshot with specific values. Consistency: is the drift consistent with the FRIA's *scope* claims? The second demographic segment (EU-DACH-firms) has been trending upward for three consecutive months; is it approaching the FRIA-cited 0.15 threshold? Analyst confidence: is any panel un-readable or missing?
- **Quality (§2.2).** State the current quality snapshot. Consistency: is the groundedness value consistent with the system-card claim (0.83 vs 0.85 published)? Is the hallucination-rate uptick consistent with the eval-evidence baseline? Is the human-review overturn rate a signal (there is no baseline yet — this is a new signal post-exercise-02)? Analyst confidence.
- **Safety (§2.3).** State the current safety snapshot. Consistency: the *citation-must-be-retrieved* guardrail is a post-exercise-02 addition; the 0.8% fire-rate is the operating evidence that the FRIA's *citation-provenance-guardrail* measure is operating. The refusal-appropriateness uptick (0.02 → 0.03 on the false-refuse) is a mild signal; is it consistent with the assessment? Analyst confidence.
- **Cost (§2.4).** State the current cost snapshot. Consistency: cost is up (+8% per completed memo), tokens are up (+9%), cache-hit rate is down (6pp). Is this a governance signal on its own? Chapter 05 was explicit that cost is *governance-adjacent* — read across panels before concluding.

### Step 3 — Compose the cross-panel reading (§3)

Author a **§3 Cross-panel reading** section that walks the five cross-panel reading rules from chapter 05 and identifies which — if any — apply to the August snapshot.

The August pattern to read: **drift is mostly stable but one segment is trending; quality is soft (groundedness below system-card claim, hallucination-rate uptick, human-review overturn rate up); safety is stable-plus-new-guardrail-firing; cost is up with cache-hit-rate down.**

Chapter 05's five patterns:

- **Drift up + quality down.** Does it apply? The one-segment drift trend co-occurring with the quality-panel softness may or may not be the pattern. State the reading and the coordination action.
- **Quality down + safety up.** Does it apply? Refusal-appropriateness is up (false-refuse rate 0.02 → 0.03) and quality is down; is the model defaulting to refusal / evasion on inputs it now handles poorly?
- **Safety spike + cost up.** Does it apply? The safety spike is the *citation-must-be-retrieved* guardrail firing (which is by design, not an attack signal); the cost is up but not correlated with a jailbreak-fire spike. State the reading.
- **Cost down + quality down.** Does it apply? Cost is *up*, not down; this pattern does not apply. State it explicitly to demonstrate the walk.
- **Cost up + drift up but quality stable.** Does it apply? Quality is *down*, not stable; this pattern does not apply. State it explicitly.

For any pattern that applies (or partially applies), name the coordination action per chapter 05 (which specialist role gets pinged; what re-eval / investigation is requested; what escalation-register class assignment follows if the coordination does not resolve within the reading period).

The point of §3 is to demonstrate that the analyst is reading *across* panels, not just within. Chapter 05 was explicit: cross-panel reading is the discipline that distinguishes an analyst who reads dashboards competently from one who reads panels in isolation.

### Step 4 — Compose the governance interpretation (§4)

Author a **§4 Governance interpretation** section, one paragraph per chapter 05's three levels:

- *Continued sign-off* — all four panels consistent with the referenced assessments and evaluations; any drift signals within threshold; any escalations open on their own tracks.
- *Warning* — one or more panels have escalated; the enterprise's sign-off remains but with a named observation and a re-review at the next reading period.
- *Escalation* — one or more panels show a state inconsistent with a referenced assessment or evaluation, or one or more escalations have been open beyond their target date.

Pick one of the three and state the rationale in a full paragraph. The August snapshot has multiple soft signals (segment-drift trend, groundedness below system-card claim, cost-up-cache-down); the analyst's interpretation must be honest about which category the system's operating state falls into. The load-bearing question: is the groundedness value below the system-card claim a *warning* (a named observation and a re-review) or an *escalation* (a state inconsistent with a published claim, driving a class-4 governance-council read)?

### Step 5 — Open the escalations (§5)

Author a **§5 Escalations opened this period** section that lists every escalation the reading triggers, per chapter 06's escalation-record shape. At minimum, address:

- The segment-2 (EU-DACH-firms) drift trend approaching the FRIA-cited threshold. Chapter 06 was explicit that a segment threshold cited in the FRIA is a Class 1 (model-behaviour) escalation to `ai-risk-engineer` with a fresh disaggregated eval requested within a chapter-06-specified window.
- The groundedness value below the system-card claim. This is a Class 1 escalation to `ai-eval-engineer` (metric owner) and a candidate Class 4 (governance-council decision) escalation if the pattern of published-claim-versus-current-state divergence persists across two consecutive reading periods.
- The cost-up + cache-hit-rate-down + tokens-up cluster. This is a `ai-infra-mlops` coordination item, not necessarily a Class 2 (security) escalation — chapter 06 was explicit that cost-only signals are governance-adjacent. State the coordination without over-escalating.
- The trust-and-safety escalation-volume tick (0 → 2). Chapter 06's threshold: two isolated dispositioned-within-policy events do not warrant a Class 2 (security) escalation; a trend across three consecutive months would.
- The human-review-overturn-rate trend (2.4% → 3.1%). No baseline yet — the signal is new post-exercise-02. Chapter 06's escalation-trigger for *new-signal-with-no-baseline* is a *baseline-establishment request* to `ai-eval-engineer`, not an incident escalation.

For each escalation, populate chapter 06's row shape (escalation ID `ESC-2026-EX03-*`; class per chapter 09; source panel; source metric value and threshold; requested action; escalation owner; target date; roll-up reference to `mod-108`).

### Step 6 — Flag un-readable and missing panels (§6)

Author a **§6 Un-readable and missing panels** section per chapter 05's two-things-the-analyst-does-on-the-panels-themselves section. For the August scenario, identify:

- Any panel that does not label its axes, does not show a threshold, does not indicate its sampling window, or does not have an obvious meaning at analyst reading — treat as a `mod-108` control-testing finding under the *dashboards produce readable evidence* control.
- Any panel that the FRIA cites as a *measure* but that does not exist — treat as a `mod-108` control-testing finding under the *measure commitments have operating evidence* control.
- Any panel whose data quality the analyst has doubts about (labelling backlog, sampling gap, timestamp drift) — flag with the observation and the coordination request.

The scenario provides one clear missing-panel candidate — the *human-review overturn rate* metric is new and has no baseline yet, but chapter 05's discipline says the *lack of a baseline* is itself a finding to raise to `ai-eval-engineer`. Populate the finding.

### Step 7 — Attach the reading evidence (§7)

Author a **§7 Attachments** section per chapter 05's attachments block:

- Screenshot placeholders for any panel state cited (URL + timestamp + environment tag). Do not fabricate screenshots; describe the panel state and mark `<!-- screenshot placeholder: <panel-URL>-<timestamp>-prod -->` per `mod-108` chapter 02's evidence-screenshot discipline.
- Escalation IDs opened during the reading period (from §5).
- Any incident records the reading period surfaced (per exercise 02, if applicable).

## Requirements

- **Every field of chapter 05's monitoring-reading-note header is populated.** Reference-version fields (assessment, register, eval-evidence, system-card) name specific versions; a *what changed since last period* line calls out any baseline updates.
- **Every panel family (drift, quality, safety, cost) is covered in §2** with the four-paragraph shape from chapter 05 (current state; consistency; what escalated; analyst confidence).
- **Each panel-family paragraph names at least one specific metric value.** Chapter 05 was explicit that *all panels stable* without specific metric values is a common failure mode. *Groundedness at 0.83 rolling-30-day against a baseline of 0.87 and a system-card claim of 0.85* is a reading; *quality is soft* is not.
- **The cross-panel reading in §3 walks all five patterns explicitly.** Patterns that do not apply are stated as *does not apply* with the reasoning, not silently omitted. Chapter 05's discipline is the walk, not just the ones that fired.
- **The governance interpretation in §4 picks one of the three levels** (continued sign-off / warning / escalation) with a full-paragraph rationale. A §4 that reads *"needs monitoring"* without picking a level is off-side.
- **The groundedness-below-system-card-claim analysis lands as at least a *warning* in §4.** Chapter 05 was explicit that inconsistency with a published claim is a *warning* at minimum; if the divergence has persisted for two reading periods it is an *escalation*. The August reading is the first period at 0.83 — the July reading was 0.86 (above the claim). The rationale in §4 must state the *warning-not-escalation* call and set up the *if-August-repeats-in-September-then-escalation* rule.
- **§5 opens at least one Class 1 (model-behaviour) escalation to `ai-risk-engineer`** for the segment-2 drift trend. Chapter 06's escalation-trigger for segment thresholds cited in the FRIA is explicit.
- **§5 opens at least one Class 1 escalation to `ai-eval-engineer`** for the groundedness-below-system-card-claim finding, with a *baseline-establishment request* on the human-review-overturn-rate metric attached.
- **§5 does *not* open a Class 2 (security) escalation for the cost-up cluster.** Chapter 06 was explicit that cost-only signals are governance-adjacent, not security; treating cost as a security escalation is a chapter-05 discipline failure.
- **§6 identifies at least one *dashboards-produce-readable-evidence* finding.** The scenario's *human-review-overturn-rate is new and has no baseline yet* is the trigger; the finding routes to `ai-eval-engineer` for baseline establishment and to the analyst's `mod-108` control-testing findings queue.
- **§7 attachments are placeholders, not fabricated screenshots.** *`<!-- screenshot placeholder: <panel-URL>-<timestamp>-prod -->`* is honest; a fabricated image would be a fail.
- **No metric-choice, threshold-tuning, root-cause, or fix commentary.** Chapter 05's deferral rules are explicit; the note reads the panels, opens the escalations, and coordinates. It does not propose an alternative metric, retune the threshold, diagnose the root cause, or commit to a fix. A note that reads *"the groundedness metric should be replaced with a more sensitive alternative"* is off-side.
- **No fabricated tool names, dashboard URLs, or environment tags.** Use `[Evidently-on-internal]`, `[Ragas-on-Langfuse]`, `[Datadog-LLM-Observability]`, and `[panel-URL-<panel-name>-prod]` as placeholders. Do not invent tool instance names.

## Starter guidance

- Do §2 before §3 before §4. Chapter 05's discipline is that the four-family reading is the input to the cross-panel reading, which is the input to the governance interpretation. Skipping to the interpretation without the reading is a common failure mode.
- The load-bearing metric on the August snapshot is groundedness — 0.83 rolling-30-day against a system-card claim of ≥ 0.85. This is the *inconsistency with a published claim* case chapter 05 called out. Do not soften it; the analyst names the inconsistency and drives the escalation. The escalation is Class 1 to `ai-eval-engineer` (not Class 4 yet — one period of inconsistency triggers a warning-and-escalate-if-repeats pattern; two consecutive periods triggers a council read).
- The segment-2 (EU-DACH-firms) PSI value is 0.13 on a 0.15 threshold — *approaching*, not *crossed*. Chapter 05 was explicit that trending toward a threshold is a reading (not necessarily an escalation); chapter 06 was explicit that a FRIA-cited segment threshold is a Class 1 escalation on approach if the trend is upward for three consecutive months. The three-consecutive-month rule fires on this snapshot; the escalation opens.
- The cost cluster is a coordination item, not a security escalation. Chapter 05 was explicit: *cost-only signals are governance-adjacent, not security.* Read the cost cluster together with the token increase and cache-hit-rate drop and coordinate with `ai-infra-mlops` for the *why* (possibly the extended retrieval index — 2.1% larger — is producing longer contexts, which drives token count up and cache-hit-rate down, and produces slightly softer groundedness because retrieval is bringing in more marginal-relevance chunks). Do not commit to that root cause on the note — you are not the metric owner; coordinate with `ai-eval-engineer` and `ai-infra-mlops` and record their disposition on the next reading period's note.
- The refusal-appropriateness uptick (0.02 → 0.03) is a mild signal that reads *with* the quality softness. Chapter 05's *quality down + safety up* pattern applies partially — quality is down, and one safety sub-signal (false-refuse) is up. State the reading in §3 and coordinate with `ai-eval-engineer` for a refusal-appropriateness deep-check. Do not over-escalate; the false-refuse rate is 3%, not 10%.
- Where the scenario does not name a specific value for a field you would normally populate (e.g., the `ai-eval-engineer` role's specific person), use *TBD-<the-role-name>* or *the-`ai-eval-engineer`-named-owner-per-INV-2026-0104*. Do not invent names.
- The July values in the scenario are provided for trend comparison, not as a full July reading. The drill's deliverable is the August note; the July values are the *last-period* reference the August note compares against per chapter 05's *what changed since last period* discipline.
- If you have used no continuous-monitoring platform, spend 10–15 minutes with the [Evidently AI documentation on ML monitoring reports](https://docs.evidentlyai.com/) and the [Ragas RAG-triad documentation](https://docs.ragas.io/) before starting. The August snapshot's panel-family names (PSI, groundedness, refusal-rate, cost-per-completed-memo) will make more sense once you have seen how the tools present them.

## Acceptance criteria

- `mod-109-ex-03-monitoring-note.md` filed with §1 note header, §2 four-family reading, §3 cross-panel reading, §4 governance interpretation, §5 escalations opened, §6 un-readable and missing panels, §7 attachments.
- §1 header populates every chapter-05 field; reference-version fields name specific versions; a *what changed since last period* line is present.
- §2 covers all four panel families with the four-paragraph shape per chapter 05; each family paragraph names at least one specific metric value.
- §3 walks all five cross-panel patterns explicitly, marking the ones that do not apply as *does not apply* with the reasoning.
- §4 picks one of *continued sign-off* / *warning* / *escalation* with a full-paragraph rationale; the groundedness-below-system-card-claim analysis lands as at least a *warning*.
- §5 opens at least one Class 1 escalation to `ai-risk-engineer` (segment-2 drift), one Class 1 escalation to `ai-eval-engineer` (groundedness gap), one baseline-establishment request (human-review-overturn-rate), and coordinates the cost cluster to `ai-infra-mlops` without opening a Class 2 escalation.
- §6 identifies at least one *dashboards-produce-readable-evidence* finding (the human-review-overturn-rate baseline gap or an equivalent from the snapshot).
- §7 lists placeholder screenshot references (never fabricated images), escalation IDs, and any incident-record cross-references.
- No metric-choice / threshold-tuning / root-cause / fix commentary; no fabricated tool names or dashboard URLs; no severity assignments on escalations (severity is set by the receiving specialist, not by the analyst — chapter 06 was explicit).

## Stretch goals

- **A September projection.** After §7, draft a short *projection* section for what the September reading is likely to surface if the August signals persist: groundedness stays below system-card claim (escalation from Class-1 warning to Class-4 council read), segment-2 drift crosses the 0.15 threshold (Class-1 escalates to fresh disaggregated eval with fixed-time delivery), cost cluster continues without a resolution note from `ai-infra-mlops` (Class-1 model-behaviour or Class-3 vendor-relationship escalation depending on the disposition). This is a private analyst planning artefact; write it as the analyst's own notes to self, not as council-facing text.
- **A tier-boundary check.** The scenario is a monthly reading on a High-tier system by construction. Chapter 05's tiering note calls out that the cadence flexes with the enterprise's system count. Write a paragraph on how the reading would change if the same system were Medium-tier (quarterly cadence) — what signals would be missed, what escalations would land differently, and what the tiering-decision escalation to `senior-ai-governance-architect` would say.
- **A dashboard-authorship request.** For the *human-review-overturn-rate* metric that has no baseline yet, draft a short authorship request to `ai-eval-engineer` per chapter 05's *flag missing panels* discipline. The request names the FRIA measure the metric maps to (the *human-review-of-every-output* measure post-exercise-02), the operating-evidence claim the metric would support, the desired baseline, and the target cadence. The analyst does not author the metric; the request drives the authorship.
- **A cross-panel confusion-matrix.** For the five cross-panel patterns in §3, build a 5×N matrix where columns are the five patterns and rows are the specific signals from the August snapshot; mark each cell with *supports*, *contradicts*, or *neutral*. This is the analyst's private tool; it exposes which combinations of signals point at which patterns and which patterns the current snapshot's evidence is silent on.
- **A note-authoring template.** Extract the note's structure into a reusable template the analyst uses every reading period — header block, four-family paragraph scaffolds, cross-panel walk table, interpretation-decision paragraph, escalation-record scaffold. Save it alongside the note as `mon-note-template.md`. This is the artefact chapter 01 walked as the analyst's *reads the panel* discipline.

## Deliverables

- `mod-109-ex-03-monitoring-note.md` — §1 note header, §2 four-family reading, §3 cross-panel reading, §4 governance interpretation, §5 escalations opened, §6 un-readable and missing panels, §7 attachments, plus any stretch sections.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference monitoring-reading note on the contract-review-assistant / MCDA pair, with the August snapshot's load-bearing calls (groundedness below system-card claim → Class-1 warning to `ai-eval-engineer`; segment-2 drift trend → Class-1 escalation to `ai-risk-engineer` on the three-consecutive-months rule; cost cluster → `ai-infra-mlops` coordination without Class-2; human-review-overturn-rate → baseline-establishment request; refusal-appropriateness uptick → *quality-down-safety-up* partial cross-panel pattern), and a governance-interpretation call of *warning* on the August period with the *escalate-if-repeats-in-September* rule set up. Your note will differ in the specific IDs threaded through (per your `mod-102`–`mod-108` corpus), the specific tool placeholders (per whichever platforms the enterprise you write against uses), the specific analyst-voice wording of the governance interpretation, and the specific coordination-owner names. What should not differ is (a) the four-family reading with specific metric values per family, (b) the full five-pattern cross-panel walk, (c) a governance-interpretation call from the three levels, (d) at least one Class-1 escalation on segment-2 drift and one Class-1 escalation on groundedness, (e) no Class-2 escalation on the cost cluster, (f) a *dashboards-produce-readable-evidence* finding on the baseline-gap metric, and (g) no root-cause or fix commentary. A tight note that reads the panels honestly (including the *warning* call on groundedness) beats a longer note that soft-pedals the inconsistency with the system-card claim.
