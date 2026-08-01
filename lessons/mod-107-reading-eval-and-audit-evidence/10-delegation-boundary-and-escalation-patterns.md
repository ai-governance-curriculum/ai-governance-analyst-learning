# Delegation Boundary and Escalation Patterns

## Why this chapter

Chapter 01 previewed the delegation boundary between the analyst and the evaluation-engineering / red-team / risk-engineering roles that produce the evidence. Every chapter since has reinforced it with a *what this is not* section. This chapter makes the boundary explicit and — critically — walks the *escalation* protocol for the cases the boundary alone cannot handle: under-evidenced claims, mis-scoped evals, stale evals, and the small number of situations where the packet chapter 09 works cannot be handed off in good faith.

Escalation is a first-class output of this module. An analyst who silently files an under-evidenced eval into the register and moves on is worse-than-useless: they are laundering a gap into evidence. Escalation is how the analyst surfaces the gap to the accountable role — the ML / product owner, the governance council, or (via the packet) `ai-evaluation-engineer` — with enough structure that the accountable role can act.

## The delegation boundary — full statement

The full statement of who does what in the eval-and-audit-evidence loop:

### `ai-governance-analyst` (this role) does

- **Read** the eval, red-team, audit, system-card, and RSP-family reports.
- **Locate** the three load-bearing claims (residual-risk, threshold-decision rationale, unresolved findings).
- **Summarise** into `EVAL-<year>-<sequence>` and `BENCH-<year>-<sequence>` rows per the chapter 05 schema.
- **Link** to source artefacts and to the register, impact-assessment, regulatory-tracker, control-library, and incident-response artefacts.
- **Benchmark** internal artefacts against public references (vendor system cards, RSPs, Preparedness Frameworks).
- **Compose** the review packet per chapter 09.
- **Hand off** the packet to `ai-evaluation-engineer` for release-assurance sign-off.
- **Escalate** under-evidenced claims, mis-scoped evals, stale evals, and packet-cannot-be-handed-off cases per this chapter.
- **Refresh** the row set on cadence (per-report change log, per-vendor revision, quarterly cross-check).
- **Communicate** the row set and packet outcomes to the governance council per `mod-110`.

### `ai-governance-analyst` does *not*

- **Design or run** the evaluation. Tasks, datasets, solvers, scorers, judges, and eval-run infrastructure are `ai-evaluation-engineer` / `model-evaluation-engineer` scope.
- **Design or run** the red-team engagement. Threat modelling, attack construction, jailbreak methodology, tool-use exploitation, and reproduction verification are `ai-red-team-engineer` scope.
- **Design or run** the risk-quantification study. Quantitative risk modelling, robustness studies, and adversarial-perturbation analyses are `ai-risk-engineer` scope.
- **Interpret novel benchmark metrics.** An unfamiliar metric is recorded verbatim and the eval owner is asked to characterise it. The analyst does not silently guess a meaning.
- **Author the residual-risk-acceptable decision.** The eval owner's threshold-decision rationale is quoted; the accept-or-not call belongs to the accountable model / product owner.
- **Sign off release-assurance.** `ai-evaluation-engineer` signs (with counter-signatures per enterprise policy). The analyst's packet is input to the sign-off, not the sign-off.
- **Author internal policy on release-gating thresholds.** Enterprise policy on what threshold levels release-gate what deployment tiers is `head-of-ai-governance` / `ai-policy` scope; the analyst reads and applies the policy.
- **Represent the enterprise in a regulator engagement.** Regulator-facing eval-evidence packages are prepared with counsel and (per enterprise policy) with `head-of-ai-governance`. The analyst supplies the underlying material; the representation is not the analyst's.

### Adjacent roles the analyst hands off to or receives from

- **`ai-evaluation-engineer`** — produces internal eval reports; receives the review packet; performs release-assurance sign-off.
- **`model-evaluation-engineer`** — near-synonym in many enterprise structures; produces model-specific evaluations.
- **`ai-red-team-engineer`** — produces red-team engagement reports; receives escalation on emerging attack patterns the analyst notices during reading.
- **`ai-risk-engineer`** — produces internal risk-quantification and robustness studies; the analyst reads.
- **ML / product owner** — accountable role for the system; receives escalation on under-evidenced claims, mis-scoped evals, and stale evals on their system.
- **Governance council** — receives escalation for cross-system patterns, systemic evidence gaps, and threshold-policy questions. Also receives regular briefings per `mod-110`.
- **`head-of-ai-governance`** — accountable role for the analyst's function; receives escalation on packet-cannot-be-handed-off cases and on repeated systemic gaps.
- **Counsel / DPO** — receives escalation on legal / regulatory / privacy questions the analyst has flagged in the row's *counsel-flag* field.
- **`incident-response-team`** — receives escalation on any red-team finding that is being actively exploited or that has a live consumer harm attached.

## The four escalation classes

The analyst-tier escalation protocol organises around four escalation classes. Each has a definition, a trigger, a route, and a template.

### Class 1 — Under-evidenced claim

**Definition.** A residual-risk claim in the report is not supported by the evidence the report cites, or the threshold-decision rationale is absent, or the unresolved-findings list is missing.

**Trigger examples.**

- Report says *safety is acceptable* without naming a threshold.
- Report claims low residual risk based on an aggregate that hides a category-specific failure.
- Report cites a scorer whose calibration is undocumented and whose bias direction is not addressed.
- Report presents a *no findings* conclusion from a red-team engagement whose methodology section describes an under-powered exercise.
- Vendor system card cites an external evaluator without a linkable reference to the collaboration.

**Route.** To the eval owner (author of the internal report) or the ML / product owner (for vendor artefacts). Copy `ai-evaluation-engineer` for internal reports. Copy the governance council if the under-evidence pattern recurs across systems.

**Template (row's *escalation-hooks* field or standalone note):**

> *Escalation Class 1 — under-evidenced claim.*
>
> *Row: `EVAL-<year>-<sequence>` — [report title]. Claim: [the residual-risk or threshold claim, verbatim]. Evidence gap: [what is missing]. Question to eval owner: [specific ask]. Route: [named owner]. Requested resolution date: [date]. Impact on packet `PACKET-<year>-<sequence>`: [none / addendum required / hand-off deferred].*

The row's status transitions to *escalated* and remains there until the owner responds. If the owner cannot provide the missing evidence within the requested window, the escalation itself becomes a governance-council item.

### Class 2 — Mis-scoped eval

**Definition.** The eval measured what it measured cleanly, but the scope does not match the deployed system's use case, model version, deployment surface, or risk categories.

**Trigger examples.**

- Safety eval was run on `claude-3-5-sonnet-20240620` but the deployment uses `claude-3-5-sonnet-20241022`.
- Safety eval was run at temperature=0 but deployment runs at temperature=0.7.
- Safety eval was run without tool use but deployment enables function calling.
- RAG-triad eval used a retrieval index version that predates the currently-deployed index.
- Red-team engagement scope explicitly excluded prompt-injection-via-retrieved-context, which is the deployment's dominant risk category per the impact assessment.
- Fairness-review categories from `mod-104` include protected characteristics the eval did not test against.

**Route.** To the eval owner and to the ML / product owner. The eval owner may re-scope; the ML / product owner may need to update the deployment or accept a re-eval before proceeding.

**Template:**

> *Escalation Class 2 — mis-scoped eval.*
>
> *Row: `EVAL-<year>-<sequence>` — [report title]. Scope as reported: [scope, verbatim]. Scope required for the deployed system: [what the deployment needs]. Divergence: [named divergence — e.g., model version drift, solver configuration mismatch, category not covered]. Options: (a) re-run eval against the deployed configuration; (b) narrow the deployment to match the eval's scope; (c) accept the divergence with a documented risk-treatment note. Route: [named owner]. Requested resolution date: [date].*

The row's status transitions to *escalated*. The packet chapter 09 works either references the escalation inline (the packet is handed off with the escalation open) or defers hand-off (rare — see the *packet-cannot-be-handed-off* section below).

### Class 3 — Stale eval

**Definition.** The report is beyond its own refresh cadence, or the system it evaluated has materially changed since the report ran, or a downstream artefact (regulatory tracker, impact assessment) has changed in a way that would invalidate the residual-risk claim.

**Trigger examples.**

- Report is past its next-due date and no refresh has been scheduled.
- System version, system prompt version, or tool inventory has changed since the eval.
- Retrieval index has been refreshed since the RAG-triad eval.
- Vendor has released a new base-model version and the deployment has moved to it.
- Regulatory tracker (`mod-106`) has picked up a new obligation (Colorado AI Act consumer-notice change, EU AI Act guidance) that would change the risk framing.
- A related eval has been superseded (e.g., a new red-team engagement finds a category of vulnerability the older safety eval did not test for).

**Route.** To the eval owner (to schedule the refresh) and to the ML / product owner (to accept the interim risk of a stale eval or to trigger a system change that would defer the release gate). Copy `ai-evaluation-engineer` for internal reports.

**Template:**

> *Escalation Class 3 — stale eval.*
>
> *Row: `EVAL-<year>-<sequence>` — [report title]. Last-verified: [date]. Refresh cadence: [cadence]. Staleness trigger: [what changed]. Impact on residual-risk claim: [what the analyst reads the impact as — verbatim from the report where possible]. Refresh options: (a) re-run at [target date]; (b) accept interim risk with documented risk-treatment note through [target date]; (c) narrow deployment scope until refresh completes. Route: [named owner]. Requested resolution date: [date].*

The row's status transitions to *evidence-stale* and (if the impact is material) *escalated*. Packet hand-off proceeds with the escalation inline; release-assurance sign-off may be conditional on the resolution.

### Class 4 — Packet-cannot-be-handed-off

**Definition.** The rare case where the analyst has walked the pre-hand-off completeness check and the packet is not defensible for hand-off — the evidence gap is material, the escalation cannot be closed in the release window, and handing the packet off would mean asking `ai-evaluation-engineer` to sign off on an incomplete evidence base.

**Trigger examples.**

- No internal safety eval exists for the system's dominant risk category and the vendor's system card does not cover the category either.
- The most recent eval on the system was run against a system version that has since undergone a Critical-severity red-team finding that has not been mitigated.
- The vendor has revised its RSP / Preparedness Framework in a way that would re-classify the model at a higher tier than the enterprise's controls are prepared for, and the enterprise has not made the corresponding control update.
- The system's use case has changed since the last impact assessment and the eval evidence base has not caught up.

**Route.** Escalation goes to `head-of-ai-governance` and to the governance council. `ai-evaluation-engineer` is notified that the packet is being held. The ML / product owner is notified that the release gate is at risk. Counsel is copied if there is a regulatory dimension.

**Template:**

> *Escalation Class 4 — packet-cannot-be-handed-off.*
>
> *System: `INV-<year>-<sequence>`. Release gate: [name and target date]. Reason: [structured description of the evidence gap that prevents hand-off]. Required resolution: [what would need to change for the packet to be handed off]. Owners: [named]. Estimated resolution effort: [rough]. Recommendation: [analyst's recommendation — defer release, narrow release scope, accept documented residual risk with council sign-off, or seek executive-tier decision]. Route: `head-of-ai-governance`, governance council.*

The packet enters *held* status. This is a serious escalation and should be uncommon; if it becomes common the enterprise has a broader eval-programme maturity issue that `head-of-ai-governance` and `ai-evaluation-engineer` need to jointly address.

## Escalation is a first-class output, not a failure mode

The most important discipline in this chapter: **filing an escalation is not a mark against the analyst.** It is the analyst doing the job correctly. An analyst who never files an escalation is not producing perfect evidence packages — they are producing packages with silent gaps.

The failure modes the escalation protocol prevents:

- **The silent-launder.** Analyst reads an under-evidenced claim, fills the row's residual-risk field with the report's language, and moves on. The row becomes evidence for a claim the report did not actually support.
- **The version-drift silence.** Analyst reads an eval on an older model version, fills the row against the deployed version without noting the drift, and moves on. The row now attests something the eval did not measure.
- **The stale-refresh silence.** Analyst passes a row's next-verified date, updates the last-verified field to the current date, and moves on without re-reading the report or checking the system. The row now claims currency without evidence of currency.
- **The packet-shipped-anyway silence.** Analyst has doubts about the evidence base but hands the packet off anyway, on the theory that `ai-evaluation-engineer` will catch anything the analyst missed. Sign-off is now happening on evidence the analyst themselves does not trust.

Each of these is worse than filing an escalation. The escalation protocol exists so the analyst can name the gap explicitly and route it to the accountable owner, rather than absorbing the gap into a filed row that then propagates through the register, the impact assessment, the control library, and the release-assurance sign-off as if it were evidence.

## Recurring-escalation patterns feed policy work

Single escalations resolve individually. Patterns of escalation feed structural work:

- **Repeated Class 1 escalations against a specific team or eval type** suggest the team's report-authoring template is under-specified. Feedback to `ai-evaluation-engineer` or `head-of-ai-governance` on template tightening is warranted.
- **Repeated Class 2 escalations on model-version drift** suggest the enterprise's eval-refresh trigger policy is under-specified. Feedback to internal-policy owners.
- **Repeated Class 3 escalations on stale RAG-triad evals** suggest the RAG-eval cadence policy is not matched to the retrieval-index refresh cadence. Feedback to the retrieval-platform owner and to internal-policy owners.
- **Repeated Class 4 packet-holds** suggest structural under-investment in internal eval capacity. Feedback to `head-of-ai-governance` and to the governance council.

The analyst-tier discipline: file the individual escalation; over the quarter, look at the pattern; roll the pattern up to the council briefing per `mod-110`.

## The register of escalations

Escalations are themselves tracked — one row per escalation, with:

- **Escalation ID.** `ESC-<year>-<sequence>`.
- **Class.** 1 / 2 / 3 / 4.
- **Source row.** Foreign key to the `EVAL-<year>-<sequence>` or `BENCH-<year>-<sequence>` row.
- **Filed date.** When the escalation was raised.
- **Route.** Who it was routed to.
- **Status.** *open* / *awaiting owner response* / *resolved* / *superseded* / *escalated further*.
- **Resolution.** What was done (or not done) and when.
- **Impact on packet.** Which packet(s) were affected and how.

The escalation register is a first-class artefact alongside the eval rows and benchmark rows. Auditors read it to check the enterprise's response to identified evidence gaps.

## What to memorise

- **The analyst reads and summarises; specialists produce.** The delegation boundary is fixed.
- **Four escalation classes** — under-evidenced claim, mis-scoped eval, stale eval, packet-cannot-be-handed-off.
- **Each class has a route.** Class 1/2/3 route to eval owner and product owner; Class 4 routes to `head-of-ai-governance` and the governance council.
- **Filing an escalation is doing the job correctly.** Silence is the failure mode.
- **Patterns of escalation feed policy work.** Individual escalations resolve individually; patterns rolled up to the council drive structural improvement.
- **The escalation register is a first-class artefact.** Discoverable, cited, aged.

## Summary

The delegation boundary between the analyst and the evaluation-engineering / red-team / risk-engineering roles is the module's spine. The analyst reads, summarises, benchmarks, packages, and hands off. Specialists design, run, and interpret the evaluations themselves. The escalation protocol — Class 1 under-evidenced, Class 2 mis-scoped, Class 3 stale, Class 4 packet-cannot-be-handed-off — is how the analyst surfaces evidence gaps to the accountable owners without silently absorbing them into filed rows. Escalations feed into an escalation register that auditors read, and recurring patterns roll into governance-council briefings per `mod-110`. The module closes here; the analyst who has internalised the row schema, the packet composition, the delegation boundary, and the escalation protocol is ready to run eval-evidence work end-to-end for the enterprise's inventory.
