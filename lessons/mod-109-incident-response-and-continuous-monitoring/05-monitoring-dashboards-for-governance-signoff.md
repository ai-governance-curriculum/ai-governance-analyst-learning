# Reading Continuous-Monitoring Dashboards for Governance Sign-off

## Why this chapter

Chapters 02–04 walked what happens when an incident lands. Continuous monitoring is what runs in between — the standing observation of a deployed AI system's operating behaviour so that a drift, quality, safety, or cost signal is caught before it becomes an incident, or, when it does become one, so that the incident record cites a specific dashboard state as the surface of report.

The analyst's role in the monitoring stack is *reading*, not *designing*. The metrics on the dashboards, the thresholds that fire the alerts, the sampling rules that populate the panels, and the alerting integrations that page the on-call are all designed by `ai-eval-engineer` and operated by `ai-infra-mlops`. The analyst reads what those roles have built at a level sufficient to interpret it for governance sign-off — the *monitoring-reading note* that says the affected system's operating state is (or is not) consistent with the current impact assessment, register-entry residual claim, and system-card publication, and that names anything that has escalated.

This chapter fixes the four panel families the analyst reads (drift, quality, safety, cost), the analyst-tier reading depth per family, the monitoring-reading note shape, and the deferral rules to `ai-eval-engineer` and `ai-infra-mlops` on questions the analyst is not qualified to answer.

## The four panel families

Continuous monitoring for AI systems is organised — across vendors, open-source tools, and internal platforms — around four panel families. The specific metrics, the thresholds, and the visualisations vary by task and tool; the four families are stable and are the taxonomy the analyst reads against.

### 1. Drift

*Drift* is a change in the statistical distribution of the model's inputs, outputs, or the ground-truth signal against which the model is evaluated. The four analyst-tier subclasses:

- **Data drift** — the input distribution has shifted (a new customer segment, a new product line, a seasonal pattern, a change in upstream data quality).
- **Concept drift** — the input-to-label relationship has shifted (customer preferences have changed; regulatory definitions have changed; the world's ground truth is different).
- **Label drift** — the distribution of the target has shifted (a fraud-rate change, a class-imbalance change).
- **Prediction drift** — the distribution of the model's outputs has shifted, which may be a lagging indicator of any of the above.

The typical panels: population-stability index (PSI) or Kullback-Leibler divergence between reference and current distributions per feature; per-class prediction rate over time; embedding-drift score for text-input systems; per-segment PSI where the segments were named in the FRIA / IA.

**Analyst-tier reading depth.** The analyst reads whether the drift metric is inside or outside the alert threshold `ai-eval-engineer` set; whether the metric is trending toward the threshold; whether the metric has crossed a segment threshold that the FRIA / IA specifically cited; and whether the current dashboard state is consistent with the residual-risk claim on the register. The analyst does not choose the drift metric, tune the threshold, or judge whether the drift is *safe* — those are `ai-eval-engineer` / `ai-risk-engineer` decisions.

### 2. Quality

*Quality* is the composite of task-appropriate accuracy signals that describe how well the model is performing its intended task in production. Metrics are highly task-specific.

- **Classification / regression tasks.** Precision, recall, F1, calibration error against a delayed-ground-truth label; class-conditional accuracy per protected segment.
- **RAG and question-answering tasks.** Groundedness (does the answer follow from the retrieved sources), context recall (did retrieval bring in what was needed), answer relevance, factuality against a benchmark reference. The RAG-triad (context precision, context recall, answer relevance) is one common panelisation.
- **Generative / assistant tasks.** Task-completion rate, refusal-rate on the internal reference set, human-evaluator win-rate against a baseline, refusal-appropriateness rate.
- **Agentic tasks.** Task-completion rate on scripted-task suites, tool-selection accuracy, tool-call success rate, action-authorisation-pass rate.

The typical panels: metric over time with a reference band; per-segment breakdowns; slice-by-slice performance against the eval-evidence baseline; user-feedback signals (thumbs-up / thumbs-down rate, human-review overturn rate, complaint rate).

**Analyst-tier reading depth.** The analyst reads whether the current metric is consistent with the eval-evidence baseline the release-assurance sign-off cited (`mod-107`); whether the metric has crossed a threshold that the IA cited as a *measure* commitment (chapter 04's Q4); and whether the trend suggests an incoming incident. The analyst does not judge whether a specific metric value is *good enough* — the `mod-107` eval-evidence baseline and the IA's *measures* section are the reference points.

### 3. Safety

*Safety* is the composite of guardrail-and-policy-related signals that describe how well the deployed system is enforcing the enterprise's acceptable-use policy, the model provider's usage policy, and the safety training on the base model.

- **Guardrail-classifier signals.** Rate at which the jailbreak classifier fires; rate at which the output filter fires; rate at which the input sanitiser fires; rate at which the topic-classifier routes to refusal.
- **Refusal-rate signals.** Overall refusal-rate; refusal-rate on the internal jailbreak-attempt corpus; refusal-appropriateness rate (are the refusals themselves appropriate, or is the model over-refusing benign inputs).
- **Agent-tool signals.** Tool-call authorisation-failure rate; tool-call scope-violation rate; tool-call-blocked-by-guardrail rate.
- **User-report signals.** User-reported unsafe-content rate; support-ticket rate mentioning safety keywords; trust-and-safety escalation rate.

The typical panels: rate over time, per-guardrail; refusal-appropriateness confusion matrix (true refuse, true respond, false refuse, false respond); trust-and-safety escalation volumes; correlation of guardrail fire-rate with model-version pin.

**Analyst-tier reading depth.** The analyst reads whether the guardrail is firing as expected (fire-rate stable, refusal-appropriateness stable), whether the fire-rate has trended upward (possibly indicating a coordinated attack or a change in traffic mix), whether the refusal-appropriateness has trended downward (over-refusal degrading the customer experience, or under-refusal missing unsafe outputs), and whether the metric is consistent with the system card's published claims and the FRIA's *measures* section. The analyst does not tune the guardrail, retune the classifier threshold, or judge the guardrail's technical adequacy — that is `ai-infra-security` / `ai-eval-engineer` scope.

### 4. Cost

*Cost* is the composite of run-cost signals — inference cost per request, tokens per response, cache-hit rate, tool-call cost, and cost per business outcome. Cost is not a governance signal in itself; it is a *governance-adjacent* signal, because unexplained cost movements are frequently the first observable indication of a quality or safety regression, a change in traffic mix, an unauthorised model use spike, or a provider-side model-version change.

- **Per-request cost.** Cost per API call, tokens per response, cache-hit rate.
- **Per-outcome cost.** Cost per completed task; cost per human-review handoff; cost per resolved support ticket.
- **Traffic mix.** Requests per hour, request volume by segment, provider mix.

The typical panels: cost over time per system; token-count distributions; cache-hit rate; provider-mix stacked-area chart.

**Analyst-tier reading depth.** The analyst reads whether cost is stable (no unexplained spikes or drops), whether cost movements correlate with model-version changes or guardrail retunes on the other panels, and whether cost patterns are consistent with the approved-use scope. An unexplained cost spike is not itself an incident, but it is a signal the analyst reads and, if the spike does not resolve, escalates to `ai-infra-mlops` for investigation. A cost spike that co-occurs with a spike in guardrail-fire-rate and a drop in quality metrics is the shape of a coordinated jailbreak attempt in progress; the analyst reads across panels, not just within.

## Reading across panels

The four panels are individually diagnostic; the cross-panel readings are what turn a signal into a governance interpretation.

- **Drift up + quality down.** The distribution has shifted and the model is not handling the shift. Read: an evaluation gap — the model was evaluated on a distribution it no longer sees. Coordinate with `ai-eval-engineer` for a re-eval on current-distribution samples; consider triggering a model regression incident record (chapter 02 class 1) if the quality drop crosses the incident threshold.
- **Quality down + safety up.** Task performance is degrading and guardrails are firing more. Read: the model may be defaulting to refusal on inputs it now handles poorly. Coordinate with `ai-eval-engineer` to check refusal-appropriateness; consider if user experience is at risk of degradation the IA did not envelop.
- **Safety spike (guardrail fires up) + cost up.** Guardrails firing more, requests using more compute (retries, longer responses, more chained tool calls). Read: possible coordinated attack traffic in progress. Escalate to `ai-infra-security` per chapter 06; open an incident record if the pattern persists.
- **Cost down + quality down.** The system is doing less work per request and the outcomes are worse. Read: possibly a silent model-version downgrade from the provider (they routed to a cheaper checkpoint) or a caching-layer bug. Coordinate with `ai-infra-mlops` for provenance; possible model regression incident (chapter 02 class 1).
- **Cost up + drift up but quality stable.** Requests are using more compute against a shifted distribution and the model is still performing. Read: the platform is compensating (longer chains, more retries) for a shift the model is technically robust to. Not a governance signal on its own; a monitoring-reading-note observation and a flag for the next `ai-eval-engineer` cadence.

Cross-panel reading is the discipline that distinguishes an analyst who reads dashboards competently from one who reads panels in isolation. The analyst does not need to know the equation behind each metric; the analyst does need to read the panels together.

## The monitoring-reading note

The monthly (plus on-trigger) note the analyst composes per live AI system for governance sign-off.

### Header

| Field | Content |
|---|---|
| Note ID | `MON-<year>-<month>-<inv-id>` |
| Reading period | Start and end dates |
| Inventory row | `INV-<year>-<sequence>` |
| Analyst | Named actor |
| Composed on | Date |
| Assessment reference | The current IA / FRIA / DPIA versions the reading is compared against |
| Register reference | The current register entries whose residuals the reading is compared against |
| Eval-evidence reference | The current `EVAL-<year>-<sequence>` release-assurance baseline |
| System-card reference | The published system-card version, if any |

### The four-panel-family reading

For each family, one paragraph:

- **The current state.** *Drift is stable across all monitored features; the PSI on the top three features is 0.05, 0.07, 0.04 respectively, all below the 0.15 alert threshold. Segment PSI on the demographic segments the FRIA cited is 0.06, 0.11, 0.09 — the second segment has trended upward for two consecutive months and is approaching the alert threshold.*
- **What is consistent with the referenced assessments and evaluations.** *Consistent with the current IA-2025-0034 version 4 residual claim; consistent with the release-assurance baseline in EVAL-2025-0088 v2; the segment-two upward trend is not yet inconsistent with the FRIA but is trending toward the FRIA-cited 0.15 fairness-drift threshold and warrants a fresh disaggregated eval within the next reading period.*
- **What escalated (if anything).** *Segment-two drift trend logged as a class-2 monitoring escalation to `ai-risk-engineer` under `ESC-2026-0177` on 2026-07-24; requested fresh disaggregated eval within 15 working days.*
- **Analyst confidence.** *Reading confidence is high on drift and cost panels; medium on quality (the RAG-groundedness metric depends on a benchmark that was last refreshed in Q1 and is due for refresh — flag raised to `ai-eval-engineer`); medium on safety (the guardrail-fire-rate metric is complete but the refusal-appropriateness confusion matrix is not populated for the last week due to a labelling backlog — flag raised to `ai-infra-mlops`).*

### The governance interpretation

One paragraph that summarises whether the system's current operating state warrants continued governance sign-off, warrants a warning, or warrants an escalation:

- *Continued sign-off.* All four panels are consistent with the referenced assessments and evaluations; any drift signals are within threshold and any escalations are open on their own tracks.
- *Warning.* One or more panels have escalated; the enterprise's sign-off remains but with a named observation and a re-review at the next reading period rather than the next scheduled cadence.
- *Escalation.* One or more panels show a state inconsistent with a referenced assessment or evaluation, or one or more escalations have been open beyond their target date; the analyst recommends the governance council read the note at the next standing meeting.

### Attachments

- Screenshots of any panel state cited (each captured with URL, timestamp, environment tag — per `mod-108` chapter 02's evidence-screenshot discipline).
- Escalation IDs opened during the reading period.
- Incident records the reading period surfaced.

## Where the analyst defers and how

The deferral rules are as important as the reading rules. The analyst is not the metric owner, the threshold owner, or the alerting-rule owner.

- **Metric-choice questions.** *Is groundedness the right metric for this RAG task?* → Defer to `ai-eval-engineer`; the analyst reads the metric on the panel and does not second-guess the choice on the monitoring-reading note. If the choice looks wrong (e.g., a groundedness metric that ignores document-provenance) the analyst raises a note-level observation and asks `ai-eval-engineer` for a review; the analyst does not propose the alternative.
- **Threshold-tuning questions.** *Should the PSI threshold be 0.15 or 0.10?* → Defer to `ai-eval-engineer`; the analyst reads the threshold as set. If the threshold looks poorly calibrated (constant alerting or never alerting) the analyst raises the observation; the tuning is not analyst-tier.
- **Alerting-integration questions.** *Should this alert page the on-call or open a ticket?* → Defer to `ai-infra-mlops`; the analyst can flag that the alerting integration missed an alert the analyst caught by reading the dashboard, but the routing rule is `ai-infra-mlops`-owned.
- **Root-cause questions.** *Why did the metric shift?* → Defer to the specialist role per panel family; the analyst does not perform root-cause analysis. The analyst records what shifted and when.
- **Fix questions.** *What should we do about it?* → Defer to the specialist role; the analyst records the specialist's proposed action on the note and tracks the follow-through.

The two things the analyst *does* on the panels themselves:

- **Flags un-readable panels.** A panel that does not label its axes, does not show a threshold, does not indicate its sampling window, or does not have an obvious meaning at analyst reading is a `mod-108` control-testing finding — the control is *dashboards produce readable evidence* and the analyst opens a finding when a panel fails it.
- **Flags missing panels.** A system whose FRIA cites *demographic-parity-across-segment-X* as a measure but whose dashboards do not have a segment-X panel is a `mod-108` control-testing finding — the *measure* commitment has no operating evidence. The analyst opens the finding and escalates to `ai-eval-engineer` / `ai-infra-mlops`.

The tooling landscape here includes vendor platforms (Arize, Fiddler, WhyLabs, Datadog LLM Observability, New Relic AI Monitoring), open-source tools (Evidently, DeepEval, Ragas, TruLens, Phoenix, Langfuse, OpenLLMetry), and internal-built dashboards. The analyst does not need to master any specific tool; the analyst does need to read *whatever* tool the enterprise runs against the four-panel-family taxonomy.

## Monitoring for LLM and agentic systems specifically

Some panels are LLM-specific or agentic-specific and warrant a note.

- **Prompt-drift.** For systems whose behaviour depends heavily on a system prompt, the panel tracking system-prompt-version changes and their correlated behaviour metrics is worth reading — silent system-prompt edits are a common cause of quality regressions.
- **Retrieval-index freshness.** For RAG systems, the panel tracking retrieval-index-last-refreshed and the correlated groundedness metric is worth reading.
- **Chain-length / turn-count.** For agentic systems, the distribution of chain-length or turn-count per task is worth reading — an increasing chain length may indicate the model is struggling to complete tasks or is caught in a retry loop.
- **Tool-call denial rate.** For agentic systems, the rate at which the tool-authorisation layer denied a tool call is worth reading — a spike suggests either the model is trying to escalate scope (safety concern) or the authorisation layer has been mis-configured (change-management concern).
- **Model-version pin state.** For systems that pin a model version, the panel confirming the pin is holding is worth reading — a silent unpin can lag detection for days if the traffic mix has not shifted.

These are LLM-specific reads; the four-panel-family taxonomy still holds (drift, quality, safety, cost), and each of these reads within one of the four families.

## Cadence

The default cadence for the monitoring-reading note is monthly per live AI system, with an ad-hoc note on trigger. Triggers include:

- Any incident on the affected system (the note is composed as part of the incident record's post-mortem section).
- Any threshold breach that the analyst reads even before an alert fires.
- Any change to the system's IA / FRIA / DPIA that changes what the note should compare the reading against.
- Any release of a new model version on the affected system.
- Any assurance-cycle boundary (a quarterly review, an internal-audit engagement, a governance-council briefing preparation).

The cadence itself is enterprise-policy; monthly is a default that fits the four-family reading in roughly 30–90 minutes per system per period. If the enterprise's system count makes a monthly per-system cadence infeasible, the analyst tiers the reading — High-tier systems monthly, Medium-tier systems quarterly, Low-tier systems on-trigger only — with the tiering rule sanctioned by `senior-ai-governance-architect` and recorded on the analyst's escalation register.

## Common failure modes

- **Reading each panel in isolation.** The analyst reads drift as stable, quality as stable, safety as fine, and cost as fine — while missing that all four have moved slightly in a correlated way that indicates a subtle model regression. Fix: the cross-panel reading rules.
- **Trusting the alert instead of reading the panel.** No alert fired, so the analyst does not read the panel. Fix: the note's cadence is *read the panel*, not *read the alerts*. Alerts miss things that reading catches (and vice versa).
- **Reading dashboards the specialist has not signed off as authoritative.** The analyst reads a demo dashboard, a stale mirror, or an ad-hoc panel and takes it as authoritative. Fix: the note names the specific dashboard (URL, version, owner) and the analyst reads only dashboards `ai-eval-engineer` / `ai-infra-mlops` have named as authoritative.
- **Silently updating the note's reference baselines.** The note compares to the current IA / register / eval-evidence baselines, and when those change, the analyst updates the note's *assessment reference* fields without noting what changed. Fix: the note records the assessment / register / eval-evidence reference versions at each period; changes across periods are called out in the *what changed since last period* section.
- **Composing the note without any panel reading.** The note reads *all panels stable* without any specific metric values or panel screenshots. Fix: every panel-family paragraph names at least one specific metric value and cites the panel by URL.
- **Deferring everything.** The note defers every question to the specialists and produces no governance interpretation. Fix: the governance interpretation is the analyst's — the deferrals are on the technical questions (metric choice, threshold, root cause, fix), not on the interpretation for governance sign-off.

## What to memorise

- **Four panel families:** drift, quality, safety, cost. Every metric a live AI system produces reads into one of the four.
- **Analyst-tier reading depth is *read the panel against the referenced assessments, register, and eval-evidence baselines*.** Metric choice, threshold, and fix are specialist scope.
- **Cross-panel reading is the discipline that turns signals into interpretations.** The five combinations in §"Reading across panels" are the common patterns.
- **The monitoring-reading note has a fixed shape:** header, four-family reading, governance interpretation, attachments.
- **Deferral rules are explicit.** Metric, threshold, alerting integration, root cause, and fix questions defer to the specialists. Un-readable and missing panels are flagged as `mod-108` control-testing findings.
- **Default cadence is monthly per live system, on trigger.**

## Summary

Continuous monitoring gives the analyst the surface on which to read the enterprise's live AI systems between incidents. The reading is organised around four panel families — drift, quality, safety, cost — each with a set of standard metrics and each with a specific analyst-tier reading depth that stays inside *read the panel against the referenced assessments, register, and eval-evidence baselines* and defers metric choice, threshold tuning, and root cause to `ai-eval-engineer` / `ai-infra-mlops`. Cross-panel reading — drift-up-quality-down, safety-up-cost-up, and their siblings — is the discipline that turns panel signals into governance interpretations. The monthly monitoring-reading note is the analyst's tangible output: header, four-family reading, governance interpretation, and attachments. Chapter 06 turns to the escalation patterns the note's *governance interpretation* section triggers when a signal warrants one.
