# The Control-Testing Cycle and Evidence-Artefact Shape

## Why this chapter

Chapter 01 fixed the scope: the analyst runs the periodic control-testing cycle against the master control library `senior-ai-governance-architect` has published. This chapter answers the operational questions inside that scope: *what is a cycle, how often does it run, what evidence artefacts count, how are they pulled from the ML / infra / product owners, how are they attached, and when does evidence go stale*.

The answers are not exotic — a control cycle is a project-management workflow that any well-run compliance function has been operating for decades. What is AI-specific is the *evidence-artefact shape*. AI controls do not primarily produce ticket-audit trails and change-management approvals; they produce config exports (guardrail thresholds, refusal-training checkpoints, deployment flags), log samples (jailbreak-attempt hits, human-review-queue rows, output-filter matches), eval-report links (fairness eval, red-team engagement, RAG-triad eval, capability eval), sign-off records (release-assurance sign-off, DPIA acceptance, governance-council decision), screenshots (GRC dashboard tile, monitoring-panel state), and interview notes (walk-through with the model owner). This chapter fixes those six classes and the flag rules that trigger a re-test.

## The control-testing cycle at a glance

A cycle has four phases; the analyst repeats them per period.

- **Scope.** From the master control library, select the subset of controls in scope for this period. The scoping rule per control is *cadence + last-tested date + last-changed date + risk-tier of the systems the control applies to*. A quarterly control last tested more than 90 days ago is in scope; a control last changed since the last test is in scope regardless of cadence; a control on any High-tier system (per `mod-102` tiering) is in scope every period as a default. `senior-ai-governance-architect` fixes the cadence per control; the analyst applies the scoping rule.
- **Pull.** For each in-scope control, request the evidence from the named owner. Chapter 02 fixes the six evidence-artefact classes and the pull protocol.
- **Attach and test.** Record the evidence in the GRC-platform control record with a stable evidence-artefact identifier, a *last verified* date, a source-artefact link, and the test verdict (pass / fail / deviation / not-tested-in-period).
- **Report and flag.** Roll the tested set into the control-status report (chapter 03). Open a follow-up per stale-evidence flag or per failed / deviation test. Escalate the library-level gaps to `senior-ai-governance-architect` per the classes in chapter 09.

The cycle is not a spreadsheet exercise — the enterprise runs it in a GRC platform (`mod-102` chapter 04 walked the analyst-tier tour). The analyst-tier discipline is the *pull protocol* and the *stale-evidence flag rules*; the platform records the state.

## The six evidence-artefact classes

The analyst attaches one or more of these artefact types to each control test. Each control record in the master library names the class it expects.

### 1. Config export

A machine-parseable dump of the current configuration of a control-relevant knob — a guardrail threshold, a refusal-training checkpoint identifier, a deployment flag, a rate limit, a model-version pin, an allowlist / blocklist, an environment-variable-driven system prompt, a router policy.

- **Typical control types.** *Model-input length is capped at 8000 tokens*; *system prompt matches the approved v3.2 template*; *jailbreak-classifier threshold is set to 0.85 on production traffic*; *only model versions in the approved-list may be routed*.
- **Where it lives.** The infra team's GitOps repo, the deployment-platform export, the service's `/config` endpoint, the internal admin UI.
- **How to pull.** Ask the infra owner for a diff or export of the relevant knob against the value the control expects. A config export must include a *time-of-export* stamp; without it, the analyst cannot show the config was current at the test time.
- **Failure mode to watch for.** A config export dated three months old for a knob that lives in a repo where any commit could have changed the value in between. Ask for a fresh export.

### 2. Log sample

A representative slice of run-time output that shows the control operated on real traffic. Not the full log — a *sample*, with the sampling window and sampling rule named.

- **Typical control types.** *Human-review queue is invoked whenever the confidence score drops below 0.6*; *output filter blocks prompts matching the PII regex set*; *jailbreak-classifier fires and returns the refusal message on the internal jailbreak-attempt corpus*; *tool-call authorisation check runs on every agentic action*.
- **Where it lives.** The observability platform, the model-monitoring vendor, the internal data warehouse's log tables.
- **How to pull.** Request a sample with a *time window* (e.g., the last 30 days) and a *sampling rule* (e.g., 1000 records uniformly sampled from the population; all records where the control fired; all records where the control failed). A log sample without both is not evidence.
- **Failure mode to watch for.** A log sample of *only records where the control fired* being read as *proof the control fires on all inputs where it should*. That reading is a form of survivorship bias. Ask for a sample of *inputs where the control should have fired but did not*, if the log platform can produce it; otherwise annotate the limitation on the control record.

### 3. Eval-report link

A stable link to an evaluation, red-team, or audit report already recorded in the `mod-107` eval-evidence row set. The control does not re-run the eval; the control cites the eval as evidence that a claim in the control statement holds.

- **Typical control types.** *The model is evaluated for CBRN-uplift risk each release and residual is below the internal threshold*; *the RAG-quality eval runs on every knowledge-base update and groundedness stays above 0.85*; *the annual red-team engagement completed and every finding is closed or accepted*.
- **Where it lives.** The eval-evidence row set from `mod-107`; the eval owner's repository; the AI Safety Institute engagement report; the vendor's system-card link.
- **How to pull.** Ask the eval owner (per `mod-107`, this is `ai-evaluation-engineer`, `ai-red-team-engineer`, or an external evaluator) for the stable eval-evidence row identifier (`EVAL-<year>-<sequence>`) and reproduce the residual-risk claim, threshold-decision rationale, and unresolved-findings status inline on the control record.
- **Failure mode to watch for.** A link to the eval *repository* rather than to a specific *report version*. Repositories change; the report version at the time of the test is what matters. Cite the version, not the branch.

### 4. Sign-off record

The system-of-record entry that shows a named person or committee approved something on a specific date — a release-assurance sign-off, a DPIA acceptance, a governance-council decision, a model-owner acceptance of residual risk.

- **Typical control types.** *Every High-tier model release has a release-assurance sign-off from `ai-evaluation-engineer`*; *every FRIA has a fundamental-rights sign-off from the governance council*; *every fairness deviation over threshold has a documented risk-owner acceptance*.
- **Where it lives.** The GRC platform, the change-management system, the release-assurance ticket, the governance-council minutes.
- **How to pull.** Ask the sign-off owner for the record identifier, the date, and the signer. If the sign-off is stored as an email thread or a chat exchange, the analyst asks for an export attached to the control record rather than trusting the thread will remain accessible.
- **Failure mode to watch for.** A sign-off record that names the wrong role — a project manager signing something that requires an accountable executive per the enterprise's own policy. The signature is not evidence if the signer was not the accountable party.

### 5. Screenshot

A dated, source-linked capture of a UI state — a GRC-platform dashboard tile, a monitoring-panel view, a customer-facing consent-page rendering, a system-card page render.

- **Typical control types.** *The customer-facing consent page includes the AI-disclosure statement*; *the internal AI-inventory dashboard shows all High-tier systems have a current impact assessment*; *the model-monitoring dashboard shows the drift metric below threshold*.
- **Where it lives.** The UI itself; the analyst captures at test time.
- **How to pull.** Take the screenshot with the URL, the browser clock, and enough surrounding context to identify the view; store the screenshot alongside the control record with the capture-time stamp. A screenshot without a visible URL and timestamp is not evidence.
- **Failure mode to watch for.** A screenshot of a *staging* or *demo* UI mistaken for production. Include the environment tag in the capture whenever the UI shows it.

### 6. Interview note

A dated summary of a walk-through conversation with a control owner — used when the control is a *process* rather than a *knob*, and when no machine-parseable artefact can be pulled directly.

- **Typical control types.** *The ML team performs a pre-release walkthrough of the deployment checklist with the product owner*; *the model-owner reviews the fairness-review note quarterly and signs a comment*; *the on-call handover includes the AI-incident-response checklist*.
- **Where it lives.** The analyst's own notes; the enterprise's knowledge-management system.
- **How to pull.** Schedule a walk-through, record who was present, what was walked, what the control owner produced during the walk, and the analyst's assessment. An interview note *by itself* is the weakest evidence class — where possible, escalate the control to `senior-ai-governance-architect` for redesign so a machine-parseable artefact can be produced next cycle.
- **Failure mode to watch for.** Attaching an interview note as the only evidence for a High-tier control that could produce a config export or log sample instead. The control-status report (chapter 03) should note *evidence-class downgrade* whenever this happens.

The library specifies the class. The analyst pulls the matching artefact — or explicitly records that the expected class could not be produced and downgraded to a weaker one, which itself is a control gap the report surfaces.

## The pull protocol

The analyst does not send a spreadsheet of asks and hope. The pull protocol is a short, repeatable script per control per period.

- **Request format.** One control per request. Named recipient (the control's owner in the GRC platform), the control identifier, the control statement, the expected evidence class, the required time window, and the deadline (typically five to ten working days before the report is due).
- **Escalation path.** If the owner does not respond by the deadline, the analyst escalates to the owner's manager and to `senior-ai-governance-architect` per the class in chapter 09. Non-response is a control gap in itself; the report says so.
- **Reciprocity.** Where the owner produces evidence outside the requested class ("here's a screenshot instead of the config export"), the analyst records both the delivered class and the expected class. Chapter 03's control-status report language distinguishes *tested with expected evidence class* from *tested with downgraded evidence class*.
- **Provenance.** Every attached artefact has (a) a stable identifier in the GRC platform, (b) a *pulled-from* source link, (c) a *pulled-on* date, (d) a *pulled-by* actor (the analyst), and (e) a *content hash or version pin* where the source could change under the analyst.

The analyst runs the pull protocol per control. In a mature enterprise the pulls parallelise — the same infra owner may service ten controls in one round-trip. The GRC platform's own workflow tooling automates the request-issue-response loop; the analyst reviews the responses rather than typing each one.

## The stale-evidence flag rules

A control test can pass and still leave stale evidence attached to the record. The next-period cycle needs to catch that. The analyst applies four flag rules per control record at cycle start.

- **Cadence-window rule.** Evidence dated older than the control's re-test cadence is stale. Quarterly controls tolerate ≤90 days; half-yearly ≤180 days; annual ≤365 days. The GRC platform trips the flag automatically when the *last verified* date crosses the window.
- **Config-change rule.** Evidence for a config-export control is stale when the underlying config has changed since the *last verified* date, regardless of cadence. A GitOps repo commit that touches the file, a deployment-flag flip, or a system-prompt edit invalidates the evidence.
- **Model-version rule.** Evidence for a control that depends on a specific model version (any control whose statement references "the current production model") is stale when the model version has changed since the *last verified* date. The `mod-102` inventory row's *current version* field is the trigger.
- **Regulatory-obligation-change rule.** Evidence for a control that maps to a regulatory obligation is stale when the obligation has changed since the *last verified* date. The `mod-106` regulator-tracker row's *last material change* field is the trigger. `senior-ai-governance-architect` will re-word the control; the analyst re-tests once the wording is stable.

The analyst does not *decide* the flag rules — they are policy set by `senior-ai-governance-architect`. The analyst *applies* them, opens the follow-up, and includes the stale-evidence roll-up in the control-status report.

## The evidence-artefact record shape

Every evidence attachment records at least the following in the GRC platform. The analyst never attaches a bare file.

| Field | Content | Notes |
|---|---|---|
| Evidence ID | `EV-<year>-<sequence>` | GRC-platform-assigned |
| Control ID | `CTL-<year>-<sequence>` | The control this evidence is attached to |
| Artefact class | One of: config export, log sample, eval-report link, sign-off record, screenshot, interview note | Chapter 02 §"The six evidence-artefact classes" |
| Delivered class vs expected class | *matches* / *downgraded (expected X, delivered Y)* | Chapter 02 §"The pull protocol" |
| Source | Repo URL + commit / dashboard URL + query / eval-evidence row ID / ticket ID / URL + timestamp / knowledge-base article ID | Whatever the pulled artefact was |
| Content pin | Content hash, version tag, or repository commit SHA where source can drift | Not required for immutable eval-evidence rows |
| Time window | For samples: the sampling window; for signatures: the signing date; for configs: the export time; for interviews: the walk-through date | Every artefact has a time window |
| Pulled-on date | The analyst's action date | Distinct from the time window |
| Pulled-by | The analyst | Named actor |
| Analyst note | Free-text — anomalies observed, sample-rule caveats, downgrade rationale | One or two sentences typical |

A GRC platform that cannot store this shape is being asked to hold evidence it cannot audit. Flag to `senior-ai-governance-architect` if the tool does not have the field; do not silently drop the field.

## Cadence in practice

The cadence per control class is set by `senior-ai-governance-architect`; here is the analyst-tier default the library will typically encode.

| Control class | Default cadence | Rationale |
|---|---|---|
| Config export on High-tier system | Quarterly, plus on-change | The knob is small; the change frequency is bounded; a stale config on a High-tier system is expensive |
| Log sample on High-tier system | Quarterly | Sampling every quarter catches drift while remaining bearable to run |
| Eval-report link | Per release (any Medium/High system) plus annual reaffirm | Release cadence dominates; the annual reaffirm catches long-lived systems that release rarely |
| Sign-off record | Per release (release-assurance); annual (council-level sign-offs) | The sign-off is the event; the test is that the record exists at the event |
| Screenshot | Quarterly | Cheap to re-capture; UI drift is real |
| Interview note | Semi-annually | Interview notes are the weakest class; the analyst pushes the library toward a stronger class when possible |

The analyst does not deviate from the library-set cadence without an explicit `senior-ai-governance-architect` sign-off recorded in the escalation register.

## Common failure modes

The failure modes to expect once the cycle is live.

- **Owner turnover.** The control owner has left the enterprise. The analyst files a *non-response — owner unassigned* and escalates to the owner's manager to name a successor. The library needs an owner-assignment update; that update is `senior-ai-governance-architect` scope.
- **Ambiguous control statement.** The control statement is not precise enough to test — *the model is monitored for drift* without naming the metric, threshold, or dashboard. The analyst files a *cannot-test-as-worded* deviation and hands the ambiguity to `senior-ai-governance-architect` for library-level fix. The analyst does not silently interpret and test against a self-selected metric.
- **Missing evidence class.** The library expects a config export; the enterprise never captured the config outside the deploy platform's live UI. The analyst files a *evidence-class not produceable* deviation. The library may need to be re-written toward the artefact class that can be produced.
- **Auto-generated test with no evidence.** A monitoring platform trips the control-passed status without any evidence attached — because someone wired the platform to update the record on schedule regardless. The analyst files a *pass-without-evidence* finding; the platform automation is a library-level design issue.
- **Volume-of-evidence overwhelm.** A control that theoretically requires reviewing every alert (rather than a sample) becomes untestable at scale. The library needs a sampling rule; the analyst files a *sampling-rule-missing* deviation.

Each of these is a normal outcome of the cycle. The control-status report (chapter 03) has a section per failure mode; the escalation register (chapter 09) tracks which ones require `senior-ai-governance-architect` intervention.

## What to memorise

- **The cycle has four phases** — scope, pull, attach-and-test, report-and-flag — and the analyst runs them per period.
- **The six evidence-artefact classes** — config export, log sample, eval-report link, sign-off record, screenshot, interview note — with a class expected per control. Downgrade to a weaker class is a finding, not a normal outcome.
- **The pull protocol is per-control, named-recipient, deadlined, and escalates on non-response.** The GRC platform automates the mechanics; the analyst runs the protocol.
- **Every evidence attachment carries the ten-field record shape.** Bare file attachments are not evidence.
- **The four stale-evidence flag rules** — cadence window, config change, model-version change, regulatory-obligation change — trigger a re-test regardless of the last-tested date.
- **The analyst does not set the cadence.** `senior-ai-governance-architect` sets it; the analyst applies it.

## Summary

The control-testing cycle is a four-phase workflow — scope, pull, attach-and-test, report-and-flag — that the analyst runs per period against the master control library. The AI-specific content of the cycle is the six evidence-artefact classes (config export, log sample, eval-report link, sign-off record, screenshot, interview note) and the four stale-evidence flag rules (cadence window, config change, model-version change, regulatory-obligation change). The pull protocol is per-control, named-recipient, deadlined, and escalates on non-response; the evidence-artefact record shape carries ten mandatory fields so a later auditor can reconstruct what was pulled from where when. Common failure modes — owner turnover, ambiguous control statement, missing evidence class, pass-without-evidence, sampling-rule-missing — are normal outcomes of the cycle that surface as findings, not as reasons to skip the test. Chapter 03 fixes the report shape those findings roll into.
