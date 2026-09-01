# Exercise 04 — Delegation Boundary Drill

**Estimated effort:** 2 hours
**Grounding chapters:** [10 — Delegation Boundary and Escalation Patterns](../10-delegation-boundary-and-escalation-patterns.md); grounding across [01](../01-analyst-scope-on-eval-and-audit-evidence.md), [05](../05-summarising-eval-evidence-into-a-governance-row.md), [08](../08-benchmarking-internal-artifacts-against-public-references.md), and [09](../09-composing-and-handing-off-the-review-packet.md).

## Objective

Practise the delegation boundary at speed. The drill is scenario-based: given a set of short vignettes describing situations the analyst plausibly encounters during a release-assurance cycle, the deliverable is (a) a *stay-or-hand-off* classification with the role that owns the work, (b) for each scenario that warrants an escalation, a filled-in escalation entry against the appropriate class from chapter 10, and (c) a short *register-of-escalations* projection that the auditor would read alongside the eval and benchmark rows.

The drill's point is that the boundary is not abstract — it is a set of decisions the analyst makes several times a week. Getting the boundary wrong in one direction produces the *silent-launder* failures chapter 10 called out; getting it wrong in the other direction consumes specialist bandwidth on work the analyst should have done. This exercise builds the reflex.

After this exercise you should be able to look at any inbound eval-related question or artefact and, within seconds, name (a) whether it is analyst-tier work or hand-off work, (b) which role owns it if hand-off, and (c) whether an escalation is warranted and of what class.

## Prerequisites

- Chapter 10 read; the full delegation-boundary statement (what the analyst does / does not do), the adjacent-role list, the four escalation classes (1: under-evidenced claim, 2: mis-scoped eval, 3: stale eval, 4: packet-cannot-be-handed-off), and the escalation-register row shape fresh in memory.
- Chapters 01 (role stance preview), 05 (row schema — the row's *escalation-hooks* / *counsel-flag* / *status* fields are where escalation triggers surface), 08 (benchmark row gaps often produce Class-2 or Class-3 triggers), and 09 (packet's section-7 escalation hooks and the *packet-cannot-be-handed-off* Class-4 case) skimmed.
- The exercise-01, exercise-02, and exercise-03 deliverables open — the drill will produce escalation entries that link back to specific rows filed there.
- The adjacent-role list from chapter 10 fresh in memory: `ai-evaluation-engineer`, `model-evaluation-engineer`, `ai-red-team-engineer`, `ai-risk-engineer`, ML / product owner, governance council, `head-of-ai-governance`, counsel / DPO, `incident-response-team`.

## Problem statement

The deliverable is a **single Markdown file, `mod-107-ex-04-delegation-boundary.md`**, containing three parts.

### Part 1 — Scenario triage

The exercise provides ten short vignettes below. For each, produce a triage row with:

- **Scenario ID.** `SCN-01` through `SCN-10`.
- **One-line summary.** Paraphrase the scenario.
- **Analyst-tier or hand-off.** Boolean.
- **If hand-off — receiving role.** From chapter 10's adjacent-role list. `ai-evaluation-engineer` / `ai-red-team-engineer` / `ai-risk-engineer` / ML product owner / governance council / `head-of-ai-governance` / counsel / DPO / `incident-response-team` / other (named).
- **If analyst-tier — the specific analyst-tier verb.** From chapter 10's *ai-governance-analyst does* list. *Read* / *locate* / *summarise* / *link* / *benchmark* / *compose* / *hand off* / *escalate* / *refresh* / *communicate*.
- **Escalation class if any.** Class 1 / 2 / 3 / 4 / none. A scenario may be analyst-tier work *and* an escalation (Class 1/2/3 escalations are analyst-tier work — the analyst files the escalation).
- **Route.** Named owner or role the escalation or hand-off routes to.
- **One-line rationale.** Why the scenario lands where it does. This is the field a reviewer reads to check whether you have internalised the boundary or are guessing.

The ten scenarios:

- **SCN-01.** An internal safety-eval report on MCDA lands in your inbox. The residual-risk narrative reads *the model refuses correctly in the vast majority of scenarios*, no threshold is cited, no per-slice breakdown appears in the aggregate section, and the scorer is described as *LLM-as-judge*.
- **SCN-02.** The ML product owner for MCDA asks you to re-score the internal safety-eval's dataset using a different judge model because they suspect the current judge is biased.
- **SCN-03.** A vendor releases a new base-model version (`anthropic/claude-3-5-sonnet-20250401`) with a paired system-card revision and an RSP framework update. MCDA is currently deployed on `anthropic/claude-3-5-sonnet-20241022`. The MCDA product owner says the deployment will migrate to the new version within two weeks. The current safety-eval row is against the previous model version.
- **SCN-04.** During benchmarking (chapter 08 Axis 4), you notice the vendor's card names UK AISI as a collaborator on autonomy evaluations for the model MCDA uses. The enterprise has no internal or contracted autonomy evaluation for MCDA. MCDA has no tool use enabled and no agentic surface today, but the roadmap adds function-calling in Q4.
- **SCN-05.** An eval report on MCDA-Benefits reports a fairness metric the analyst has not seen before — an `equalised-groundedness-rate` that reads as some kind of RAG-triad × protected-class disaggregation but is not explained in the report or in any documentation.
- **SCN-06.** A red-team engagement on MCDA finds a Critical-severity finding. The engagement lead says the finding is under active exploitation in a related production system — a real user has triggered a similar failure in the last 24 hours.
- **SCN-07.** The RAG-triad eval row for the HR-Policy-Bot has a `last-verified` date of 2026-03-15. The current date is 2026-09-01. The retrieval index has been refreshed twice in the interim; the system-prompt has changed once.
- **SCN-08.** `ai-evaluation-engineer` sends back the review packet you handed off, asking for the analyst's *view on whether the residual-risk claim in `EVAL-2026-088` is actually acceptable given the protected-class-generalisation category-specific miss*.
- **SCN-09.** During benchmarking, you notice that the enterprise's control library has no control at the tier the vendor's RSP commits to for the model MCDA uses. The vendor commits to hardened weight-access controls at the tier; the enterprise deploys the model via API without hardened controls on the API keys the vendor requires.
- **SCN-10.** You are composing a review packet for a system whose only internal eval is a fairness-review note (`mod-104`) that predates the current deployment configuration. The vendor's system card does not cover the deployment's dominant risk category, and no red-team engagement has been scoped. The release gate is in 10 days.

### Part 2 — Escalation entries

For each scenario in Part 1 whose *escalation class* is 1 / 2 / 3 / 4, produce a full escalation entry against the chapter-10 template for that class. The template is reproduced in chapter 10 sections *Class 1* through *Class 4*; use it verbatim as the field structure.

Each escalation entry carries:

- **Escalation ID.** `ESC-2026-EX04-<seq>`.
- **Class.** 1 / 2 / 3 / 4.
- **Source row.** Foreign key to the relevant `EVAL-<year>-<sequence>` or `BENCH-<year>-<sequence>` row from exercises 01–02 (or, where the scenario surfaces without a filed row yet, note *no row yet — escalation triggers row creation*).
- **Filed date.** For the exercise, today's date.
- **Route.** Per chapter 10's per-class routing (Class 1/2/3 to eval owner and product owner; Class 4 to `head-of-ai-governance` and governance council).
- **Class-specific template fields.** For Class 1: the claim quoted verbatim, the evidence gap, the question to the eval owner, the requested resolution date, the impact on the packet. For Class 2: scope-as-reported, scope-required, divergence, options (a/b/c), route, requested resolution date. For Class 3: last-verified, refresh cadence, staleness trigger, impact on residual-risk claim, refresh options, route, requested resolution date. For Class 4: system, release gate, reason, required resolution, owners, estimated resolution effort, recommendation, route.
- **Status.** For the exercise, *open*.
- **Impact on packet.** Which `PACKET-<year>-<sequence>` is affected and how.

For scenarios where *no escalation* is warranted, no Part-2 entry is needed — but Part 1's rationale field must be honest about *why* no escalation applies (often because the work is a specialist's to receive, not the analyst's to file).

### Part 3 — Escalation-register projection

At the bottom of the file, a short `## Escalation register` block that projects the Part-2 escalation entries into the chapter-10 escalation-register shape:

- **Escalation ID.**
- **Class.**
- **Source row.**
- **Filed date.**
- **Route.**
- **Status.**
- **Resolution.** Populated for the exercise as *awaiting owner response* for all rows.
- **Impact on packet.**

This projection is the artefact auditors read. It is the *register of escalations* chapter 10 fixed as a first-class artefact alongside the eval rows and benchmark rows.

## Requirements

- **All ten scenarios are triaged.** Each with the full triage-row field set — analyst-tier vs hand-off, receiving role or analyst-tier verb, escalation class if any, route, one-line rationale.
- **Every hand-off names a specific role from chapter 10's adjacent-role list.** `Someone else` is not a valid receiving role.
- **Every analyst-tier scenario names a specific verb from chapter 10's *does* list.** *Read* / *locate* / *summarise* / *link* / *benchmark* / *compose* / *hand off* / *escalate* / *refresh* / *communicate*.
- **Escalation classes are correctly assigned.** Chapter 10's definitions govern: Class 1 is under-evidenced (the claim is not supported by the evidence cited); Class 2 is mis-scoped (the eval measured cleanly but the scope does not match the deployment); Class 3 is stale (report is beyond refresh cadence or system has drifted); Class 4 is packet-cannot-be-handed-off (rare — evidence gap is material and cannot be closed in the release window).
- **Escalations are routed per the class-specific routing.** Class 1/2/3 route to eval owner and product owner (with `ai-evaluation-engineer` copied on internal reports and the governance council copied on recurring patterns). Class 4 routes to `head-of-ai-governance` and the governance council.
- **Every escalation entry uses the chapter-10 template.** Class-specific fields populated per template — no free-text escalation entries.
- **Every escalation entry links to a source row.** Where the row does not exist yet, the entry notes *no row yet — escalation triggers row creation* and the entry is treated as itself the trigger for a row.
- **Where a scenario has both an internal and an external route (e.g., SCN-06 with an incident-response overlay), both routes are recorded** — chapter 10's adjacent-role list includes `incident-response-team` for exactly this case.
- **Where a scenario is analyst-tier work but also is a hand-off in an adjacent sense (SCN-08 is *ai-evaluation-engineer sending a question back to the analyst*), the response is a hand-off in the *reverse* direction and requires an analyst-tier action to respond** — chapter 10's discipline is explicit that *the analyst does not author the residual-risk-acceptable decision*. The response to SCN-08 is *not* an analyst-tier opinion on whether the risk is acceptable; it is a re-hand-off with additional context or a routing to the accountable role.
- **No scenario is answered with *escalate* alone.** Escalation is a class of analyst-tier work; the entry still requires the class, the route, and the template fields.
- **The escalation-register projection is populated** for every scenario that produced an escalation.
- **No fabricated escalations.** Where a scenario legitimately does not warrant an escalation, the triage row says so with the rationale. Chapter 10 was explicit that filing an escalation is doing the job correctly *when the trigger is real* — filing one when the trigger is not real is a different kind of noise.

## Starter guidance

- Walk each scenario twice before writing anything. On the first pass, ask *whose work is this, if not mine?* On the second pass, ask *if it is mine, is any part of it a first-class escalation?* Chapter 10 was explicit that many analyst-tier scenarios include an escalation as one of their outputs.
- The *scorer is described as LLM-as-judge* line in SCN-01 is a specific trap chapter 02 called out — a scorer without a named judge model and a documented judge prompt is under-specified. Combined with the missing threshold and the missing per-slice breakdown, SCN-01 is a straightforward Class-1 escalation with three named evidence gaps.
- SCN-02 is where the *does not* list matters. The analyst does not re-run the eval's scorer with a different judge — that is `ai-evaluation-engineer` scope. The analyst may *ask* the eval owner to characterise the judge choice (a follow-up in the packet) or to run a companion eval with a different-family judge (a request for future scoping), but the re-scoring itself is not analyst-tier work. The scenario is a hand-off to `ai-evaluation-engineer`.
- SCN-03 is the archetypal Class-2 escalation. Model-version drift on a scheduled deployment change. The route is to the eval owner (to schedule a re-run of the safety eval against the new model version) and to the ML product owner (to accept the interim risk of an eval running against the previous version or to defer the deployment migration until the eval catches up).
- SCN-04 is a benchmark Axis-4 gap that surfaces from *external-evaluator alignment*. The scenario also carries a *roadmap change* — MCDA is adding function-calling in Q4. The analyst's response has both a benchmark row gap (present state) and a change-note for the impact assessment (future state). Chapter 08 fixed the gap-list output; chapter 10 fixes the escalation route.
- SCN-05 is where chapter 10's *does not interpret novel benchmark metrics* discipline applies. The analyst records the metric verbatim and asks the eval owner to characterise it. The response is a Class-1 escalation (the metric's meaning is under-specified in the report) routed to the eval owner, not an analyst-tier interpretation of what the metric might mean.
- SCN-06 combines a red-team finding with a live incident. Chapter 10's adjacent-role list includes `incident-response-team`; the escalation has two routes — the finding itself to `ai-red-team-engineer` and the ML product owner for the finding's disposition, and the live-exploit signal to the `incident-response-team` for the incident-response playbook engagement.
- SCN-07 is a Class-3 stale-eval escalation. The RAG-triad row's index-version and system-prompt drift both trigger. The route is to the eval owner (to schedule the refresh) and to the ML product owner (to decide whether to accept interim risk or to gate the deployment until the refresh completes).
- SCN-08 is where the *what the analyst does not do* list is load-bearing. The analyst does not author the residual-risk-acceptable decision. The response to `ai-evaluation-engineer`'s question is *not* an opinion on whether the risk is acceptable — it is either additional context (quoted from the source report, from the impact assessment, from the threshold policy) that helps `ai-evaluation-engineer` decide, or a re-routing to the ML product owner (accountable role) or the governance council (policy question).
- SCN-09 is a Class-2 mis-scope with a control-library implication — the enterprise's controls are below the vendor's RSP tier. The route is to the ML product owner (to update the deployment to meet the vendor tier) and to `head-of-ai-governance` (for the control-library policy question). If the enterprise cannot bring controls up to the vendor tier in the release window, this may escalate further to Class 4.
- SCN-10 is the archetypal Class-4 packet-cannot-be-handed-off scenario. Fairness-review-note-only evidence, no vendor coverage of the dominant risk category, no red-team, ten-day release gate. The route is `head-of-ai-governance` and the governance council; `ai-evaluation-engineer` is notified that the packet is being held. Chapter 10 was explicit that Class 4 should be uncommon; if a scenario looks like Class 4 on the first pass, re-read it to check that Classes 1/2/3 with an inline escalation would not suffice.

## Acceptance criteria

- `mod-107-ex-04-delegation-boundary.md` with all three parts.
- Part 1: ten triage rows, one per scenario, each with analyst-tier-vs-hand-off, receiving role or analyst-tier verb, escalation class if any, route, and one-line rationale.
- Part 2: full escalation entries against the chapter-10 templates for every scenario whose triage assigned an escalation class. Class-specific template fields populated in full.
- Part 3: an escalation-register projection at the bottom of the file, rendering the Part-2 entries into the chapter-10 escalation-register shape.
- Every hand-off names a specific role from chapter 10's adjacent-role list.
- Every analyst-tier scenario names a specific verb from chapter 10's *does* list.
- Every escalation entry links to a source row (or notes *no row yet — escalation triggers row creation*) and uses the correct class-specific template.
- SCN-06's dual-route (finding + incident-response) is recorded correctly.
- SCN-08's response is not an analyst-tier opinion on risk acceptability; it is additional context or a re-routing.
- SCN-10 is treated as a Class-4 packet-hold with the correct routing.
- No scenario is answered with *escalate* alone; no scenario is answered with *ask someone else*.
- The escalation-register projection is populated for every escalation.

## Stretch goals

- **A recurring-pattern roll-up.** After Part 3, add a short `## Recurring patterns` block that names any two-or-more escalations that share a root cause — a specific team producing under-specified reports (repeated Class 1), a specific eval type not refreshing on cadence (repeated Class 3), a specific model-version-drift pattern (repeated Class 2). Chapter 10's *recurring-escalation patterns feed policy work* section fixed the shape; the roll-up is the artefact that would feed a `mod-110` council briefing.
- **A refined delegation-boundary card.** For your own reference (and for the next analyst you onboard), extract chapter 10's *does / does not* lists into a one-page reference card, tightened against the scenarios you triaged. This is the artefact the analyst pins next to their desk; the drill's real value shows the day the card starts to look worn.
- **A response-to-`ai-evaluation-engineer` template.** For SCN-08 specifically, draft the response the analyst sends when a receiver asks for a risk-acceptability view the analyst is not scoped to author. The template distinguishes *here is additional context from the source materials* from *this is a question for the ML product owner / governance council* from *this would benefit from a companion eval scoped by you or `ai-risk-engineer`*. This template lives in the analyst's toolbox and is used for every similar future question.
- **A Class-4 avoidance retrospective.** For SCN-10 specifically, walk backwards: at what points earlier in the release cycle could the enterprise have caught the evidence gap before it reached the ten-day-to-gate deadline? Which artefact (inventory, register, impact assessment, tracker, prior eval row) was the earliest chance to notice? This retrospective is the shape that, rolled up over the quarter, drives structural improvement in the enterprise's eval-programme maturity — chapter 10 was explicit that repeated Class 4 escalations suggest structural under-investment.
- **A cross-referenced update to exercise 03's review packet.** If any of the Part-2 escalations attach to rows cited in your exercise-03 packet, update the packet's section 7 (escalation hooks) with the Part-2 entries and update section 1 (analyst summary) to state any tensions the escalations create. This closes the loop between the packet composition and the escalation protocol; the packet is only defensible when its escalation hooks reflect the escalation register.

## Deliverables

- `mod-107-ex-04-delegation-boundary.md` — Part-1 scenario triage, Part-2 escalation entries, Part-3 escalation-register projection.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference triage of the ten scenarios above and one reference set of escalation entries. Your triage will match on the load-bearing calls (SCN-01 = Class 1, SCN-03 = Class 2, SCN-06 dual-routed with incident-response, SCN-07 = Class 3, SCN-08 not an analyst opinion, SCN-10 = Class 4). The narrower calls — the specific route names, the specific requested resolution dates, the specific one-line rationales — will differ per your enterprise's structure. What should not differ is (a) all ten scenarios triaged with the full row field set, (b) escalation classes correctly assigned per chapter 10 definitions, (c) escalations routed per the class-specific routing, (d) chapter-10 templates used verbatim as the escalation-entry structure, (e) SCN-08 not answered with an analyst opinion on risk acceptability, and (f) the escalation-register projection populated. A short-and-honest triage that gets the load-bearing calls right beats a longer triage that classifies every scenario as Class-1 or misses SCN-10's Class-4 shape.
