# Monitoring-Signal Escalation Patterns

## Why this chapter

Chapter 05 fixed the analyst's reading discipline on the four panel families and the monitoring-reading note. This chapter walks the escalation half of the loop: given the reading, when does a signal warrant escalation, to which specialist role, on what timeline, and captured on what record.

The escalation half matters because reading without escalation is a governance failure. A drift metric that has been trending toward the threshold for three months and been read as *approaching threshold* every month, without an escalation ever filed, is a record that lets the incident happen and then documents that the enterprise saw it coming. The escalation is what turns a *reading* into an *action item* that a specialist role picks up.

Three specialist roles receive the majority of monitoring escalations at the analyst tier: `ai-risk-engineer` for model-behaviour signals; `ai-infra-security` for security-adjacent signals; `head-of-ai-governance` for enterprise-level or council-decision-worthy signals. Chapter 09 walks the full delegation map; this chapter fixes the *when* — the escalation-trigger tables per panel family — and the shape of the escalation record itself.

## The escalation-record shape

Monitoring escalations use the same `ESC-<year>-<sequence>` register the module inherits from `mod-108` chapter 09. The shape is identical; three fields are populated specifically for monitoring-source escalations.

| Field | Content specific to monitoring source |
|---|---|
| Trigger source | The `MON-<year>-<month>-<inv-id>` reading note that surfaced the signal, or the alert-fire event ID if the signal was alert-driven |
| Panel family + specific panel | *drift* / *quality* / *safety* / *cost* + the specific panel URL and metric that carries the signal |
| Panel state cited | The metric value, the threshold, the trend across periods, and the segment (if a per-segment threshold applies) |
| Rationale | Why the signal warrants escalation (what it implies about the referenced assessments, register, or eval-evidence baselines) |
| Requested action | What the analyst asks the escalation owner to do (a re-eval, a threshold review, a fresh disaggregated analysis, a guardrail retune, a containment action, a council decision) |
| Escalation owner | `ai-risk-engineer` / `ai-infra-security` / `head-of-ai-governance` / other |
| Target date | When the analyst expects an acknowledgement and when a substantive response |
| Status | *open* / *in-progress* / *resolved* / *withdrawn* — inherited from `mod-108` chapter 09 |
| Resolution note | The specialist's action, the resulting artefact identifier (new eval, new threshold, new incident record, council-minute reference) |
| Roll-up reference | The monitoring-reading note (`MON-<year>-<month>-<inv-id>`) that carries this escalation into its *governance interpretation* section, and the control-status report (`CSR-<year>-<period>`) that carries it into `mod-108` §5 |

## Escalation triggers per panel family

The threshold-crossing rules and the escalation classes per panel family. Every trigger table has three columns: *what the analyst reads*, *what warrants an escalation*, and *the escalation owner and class*. Class refers to the four classes chapter 09 defines: *Class A — model-behaviour route to `ai-risk-engineer`*, *Class B — security route to `ai-infra-security`*, *Class C — infrastructure / monitoring redesign route to `ai-infra-mlops`*, and *Class D — enterprise-level or council-decision route to `head-of-ai-governance`*.

### Drift panel

| Reading | Escalation trigger | Owner / class |
|---|---|---|
| Any drift metric crosses the alert threshold `ai-eval-engineer` set | Escalate on the first period of confirmed crossing | Class A (`ai-risk-engineer`); ask: re-eval on current-distribution samples and residual-risk re-open evaluation |
| Any per-segment drift metric where the segment was named in a FRIA / DPIA crosses the segment-specific threshold | Escalate on the first period of confirmed crossing | Class A + Class D (`head-of-ai-governance` copied because segment-drift on a FRIA-cited segment is fundamental-rights-adjacent); ask: disaggregated re-eval + FRIA re-open trigger evaluation (chapter 04) |
| Drift metric trending toward the threshold for two consecutive periods without crossing | Escalate as *approaching threshold* on the second consecutive period | Class A; ask: fresh reference-distribution sample and threshold review |
| Silent absence of drift metrics on a system whose IA / FRIA cited *drift monitoring* as a measure | File as a `mod-108` control-testing finding; escalate to `senior-ai-governance-architect` for library-level fix | Class C-and-`mod-108` combined |

### Quality panel

| Reading | Escalation trigger | Owner / class |
|---|---|---|
| Any quality metric drops below the release-assurance baseline the current eval-evidence row set | Escalate on the first period of confirmed drop | Class A; ask: fresh eval and model-regression incident-record evaluation (chapter 02 class 1) |
| RAG groundedness drops below the FRIA / IA-cited threshold | Escalate on the first period of confirmed drop | Class A + Class D; ask: fresh eval, retrieval-index provenance check, IA re-open trigger evaluation |
| Quality metric drops in a specific segment while overall metric is stable | Escalate on the first period of confirmed disaggregated drop | Class A + Class D; ask: disaggregated re-eval, biased-outcome-escalation incident-record evaluation (chapter 02 class 4) |
| Human-review overturn rate rises above baseline | Escalate on the first period of confirmed rise; consider as a leading indicator | Class A; ask: overturn-cause analysis and quality-metric review |
| User-feedback (thumbs-down) rate spikes | Escalate on any period where the spike exceeds 3× the trailing 12-month median | Class A + product owner copied; ask: root-cause analysis and complaint-driven biased-outcome-escalation evaluation |

### Safety panel

| Reading | Escalation trigger | Owner / class |
|---|---|---|
| Guardrail-classifier fire-rate spikes above baseline | Escalate on any period where the spike exceeds 3× the trailing 12-month median | Class B; ask: attack-pattern investigation and jailbreak / prompt-injection incident-record evaluation |
| Guardrail-classifier fire-rate drops below baseline | Escalate on any period of confirmed drop (may indicate silent guardrail bypass or classifier failure) | Class B + Class C; ask: guardrail-classifier health check and end-to-end refusal-test on the internal jailbreak-attempt corpus |
| Refusal-appropriateness drops (over-refusal or under-refusal detected) | Escalate on the first period of confirmed drop | Class A + Class B; ask: refusal-appropriateness re-eval and classifier retune review |
| Tool-call authorisation-failure rate spikes | Escalate on any period where the spike exceeds 3× the trailing 12-month median | Class B + `application-security` copied; ask: scope-violation analysis and prompt-injection incident-record evaluation |
| User-reported unsafe-content rate spikes | Escalate on any period where the spike exceeds 3× the trailing 12-month median | Class B + product owner + trust-and-safety copied; ask: unsafe-content triage and system-card claim review |
| Trust-and-safety escalation-volume threshold breach | Escalate on any period where the escalation volume exceeds the trust-and-safety team's defined threshold | Class B + Class D; ask: joint review with head-of-ai-governance |

### Cost panel

| Reading | Escalation trigger | Owner / class |
|---|---|---|
| Unexplained cost spike (any period) | Escalate on the second consecutive period without correlation-to-a-known-driver | Class C (`ai-infra-mlops`); ask: cost-attribution analysis |
| Cost spike correlated with guardrail-fire-rate spike or quality drop | Escalate immediately (do not wait for a second period) | Cross-cut: Class B (security) if safety metrics are involved; Class A (model-behaviour) if quality is involved; ask: correlated incident-record evaluation |
| Cost drop unexplained (may indicate silent model-version downgrade or caching-layer bug) | Escalate on the second consecutive period without correlation-to-a-known-driver | Class C + Class A; ask: model-version provenance check |
| Provider-mix change unexplained (new provider appearing in the panel that the vendor register does not know about) | Escalate immediately | Class C + `mod-108` chapter 06 vendor-intake; ask: fresh vendor intake for the un-registered provider |

## The 3× median rule

A common threshold across the tables above is *exceeds 3× the trailing 12-month median*. The rule is a starting-point heuristic, not a policy: it is calibrated to be sensitive enough to catch material anomalies while not paging on every small spike. `ai-eval-engineer` and `ai-infra-mlops` may set enterprise-specific thresholds that override the heuristic; the analyst uses their thresholds where set and the heuristic where not.

The heuristic assumes a system with roughly stable steady-state metrics and a 12-month operating history. New systems (less than 12 months in operation) use a shorter reference window and a more permissive spike threshold; the analyst asks `ai-eval-engineer` to sanction the choice per system.

## Cross-panel escalation

Chapter 05's cross-panel reading rules produce escalations that are not attributable to a single panel family. The two most common patterns:

- **Coordinated-attack shape.** Safety fire-rate up + cost up + quality down + drift stable. Escalate as *coordinated-attack signal in progress* — Class B, immediate, with `ai-infra-security` primary and `head-of-ai-governance` copied for enterprise-level context. Do not wait for confirmation of intent; the pattern is diagnostic enough to warrant same-day acknowledgement.
- **Silent-model-downgrade shape.** Cost down + quality down + safety stable + drift stable. Escalate as *silent-model-version-change signal* — Class C primary (provenance investigation) and Class A copied (residual-risk re-open on the register entry if the change is confirmed).

Cross-panel escalations file under the panel that carries the strongest signal, with the additional owners copied. The rationale field on the escalation record cites the specific cross-panel reading.

## What warrants a Class D escalation to `head-of-ai-governance`

Not every monitoring escalation reaches `head-of-ai-governance`. The rule of thumb: Class D applies when the signal has implications the specialists on Classes A / B / C cannot resolve alone.

- **Fundamental-rights-adjacent signals.** Segment-specific drift or quality drops on segments named in a FRIA; biased-outcome-escalation signals of any magnitude that reach the trust-and-safety threshold; regulator-facing signals (a signal that appears likely to trigger an Article 73 notification per chapter 07).
- **Cross-system pattern signals.** The same panel-family signal shape appearing on three or more inventory rows within the same reading period; a pattern of monitoring escalations that suggests an enterprise-wide policy or platform issue.
- **Council-agenda signals.** Signals that the analyst assesses would benefit from council awareness at the next standing meeting, either because they inform a pending policy decision or because they represent a material change in the enterprise's assurance posture.
- **Executive-communication signals.** Signals that may require executive communication to customers, partners, regulators, or the board.

The analyst files Class D by copying `head-of-ai-governance` on the escalation record and — for council-agenda signals — by adding the escalation to the standing council briefing per `mod-110`.

## Escalation timeline discipline

Each class has a default acknowledgement and response timeline the analyst uses at filing.

| Class | Acknowledgement | Substantive response |
|---|---|---|
| A (`ai-risk-engineer`) | 3 working days | 10 working days |
| B (`ai-infra-security`) — immediate-severity | Same day | 5 working days |
| B (`ai-infra-security`) — routine | 3 working days | 10 working days |
| C (`ai-infra-mlops`) | 3 working days | 15 working days |
| D (`head-of-ai-governance`) | 5 working days | At next standing council meeting or 15 working days, whichever is earlier |

Non-response by the acknowledgement date follows chapter 09's blocked-resolution rule: the analyst re-issues with the target date restated and copies the owner's manager; the second non-response escalates as a fresh Class D entry.

## Interaction with incident records

Monitoring escalations often turn into incident records — and vice versa. Two operational rules for the interaction:

- **Escalation → incident.** When the specialist's substantive response confirms an AI-specific effect (chapter 02's six classes), the analyst opens the incident record and cross-references the escalation. The escalation record's status flips to *resolved with incident record `INC-<year>-<sequence>` opened*.
- **Incident → escalation.** When the incident record's post-mortem identifies a monitoring gap (the incident should have been surfaced by the dashboards but was not), the analyst files a Class C escalation for the monitoring redesign and a `mod-108` control-testing finding for the missing panel.

The two records are always cross-referenced; a monitoring escalation with a resolution-note pointer to an incident record and no reverse pointer is a data-integrity failure.

## Cadence-driven vs alert-driven escalations

The analyst produces two flavours of escalation record.

- **Cadence-driven.** The escalation is filed as part of the monthly monitoring-reading note, based on the analyst's reading of the dashboards. Most Class A escalations come from cadence-driven reading (the trend is what the analyst caught; the alert may not have fired).
- **Alert-driven.** The escalation is filed in response to an alert-fire event that paged the on-call or opened a ticket. Most Class B escalations start as alert-driven.

The two flavours use the same record shape. The distinction matters for the `mod-108` control-testing view: cadence-driven escalations demonstrate *reading is being done*; alert-driven escalations demonstrate *alerting is being triggered*; the absence of one flavour or the other over multiple periods is a signal to `mod-108`.

## When *not* to escalate

Not every panel wobble is an escalation. The filter:

- **Known transient.** A metric moves during a scheduled event the analyst knows about (a planned model-version cutover, a scheduled retrieval-index refresh, a scheduled traffic-mix change) and returns to baseline within the expected window. Record the observation on the monitoring-reading note; do not escalate.
- **Within-noise variation.** A metric moves within its known noise band; the movement is not sustained across periods. Record the observation on the monitoring-reading note if the movement is worth calling out; do not escalate.
- **Already-escalated pattern.** The signal has already been filed as an open escalation in a prior period. Update the existing escalation record with the current-period state; do not open a new one.
- **Signal without follow-through capacity.** The escalation is filed to satisfy the reading discipline, but the analyst knows the specialist role cannot act on it (the specialist is unstaffed, the tool is being retired, the system is in end-of-life). File as a `mod-108` control-testing finding — the *specialist coverage exists to receive monitoring escalations* control — and route to `senior-ai-governance-architect` for library-level intervention.

## Common failure modes

- **Escalations that never file.** The analyst reads the panels, notes the signal in the monitoring-reading note, and never opens the escalation record. The specialist role never picks it up. Fix: the note's *what escalated (if anything)* section is mandatory; empty means the analyst asserts *nothing warranted an escalation this period*, not *I did not file*.
- **Class miss.** The analyst files a Class A escalation on a signal that has clear security implications and should have been Class B. Fix: chapter §"Escalation triggers per panel family" gives the class per trigger; the analyst files the class the table names.
- **Overuse of Class D.** Every escalation carries `head-of-ai-governance` as a copy, diluting the executive's queue. Fix: Class D is for the four situations in §"What warrants a Class D escalation"; other classes do not automatically copy the head.
- **Under-use of Class D on fundamental-rights signals.** Segment-specific fairness signals file as Class A without the Class D copy; the enterprise's exposure on protected-class outcomes is invisible to the executive. Fix: FRIA-cited-segment signals always add Class D.
- **Escalations that resolve without an artefact.** The specialist responds informally (an email, a chat message) and the analyst closes the escalation without the resolution-note artefact identifier. Fix: `mod-108` chapter 09's rule — verbal commitments do not close escalations. The specialist's action must produce a follow-through artefact (a new eval identifier, a new incident record, a new control record, a council-minute reference), and the identifier lands on the escalation.
- **Cadence-driven escalations displacing alert-driven ones.** The analyst files heavily on the monthly cadence but does not receive alert-driven pages because the on-call rotation is not routing them. Fix: raise the alerting-integration gap to `ai-infra-mlops` as a Class C.

## What to memorise

- **Four escalation classes:** A (`ai-risk-engineer`), B (`ai-infra-security`), C (`ai-infra-mlops`), D (`head-of-ai-governance`).
- **Trigger tables per panel family** in §"Escalation triggers per panel family" — the analyst files under whichever the specific signal matches.
- **The 3× median rule** is the analyst's default for spike detection; `ai-eval-engineer` / `ai-infra-mlops` may set an enterprise-specific override.
- **Cross-panel escalations file under the strongest-signal panel and copy the other affected classes.**
- **Class D applies on fundamental-rights, cross-system pattern, council-agenda, or executive-communication signals** — not on every escalation.
- **Escalation timelines have per-class defaults;** non-response follows `mod-108` chapter 09's blocked-resolution rule.
- **Escalation-incident interaction is bidirectional.** Escalations that confirm an AI-specific effect open incident records; incidents that expose a monitoring gap open Class C escalations.

## Summary

Reading without escalation is a governance failure. The analyst files monitoring-source escalations against the `ESC-<year>-<sequence>` register under four classes — A (`ai-risk-engineer`), B (`ai-infra-security`), C (`ai-infra-mlops`), D (`head-of-ai-governance`) — with a trigger table per panel family that specifies the threshold-crossing and spike rules. Cross-panel escalations file under the strongest-signal panel with the other affected classes copied. Class D applies specifically on fundamental-rights, cross-system-pattern, council-agenda, or executive-communication signals. Escalation and incident records are bidirectionally cross-referenced. Chapter 07 turns to the EU AI Act post-market surveillance summary — the periodic artefact that carries this module's monitoring reading and incident recording into the regulator-facing form the Act requires for high-risk systems.
