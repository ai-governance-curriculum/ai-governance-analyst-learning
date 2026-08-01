# The Analyst's Scope on Controls and Compliance Evidence

## Why this chapter

By this point in the track the analyst has authored inventory rows (`mod-102`), risk-register entries with mitigations (`mod-103`), fairness-review notes (`mod-104`), an impact-assessment corpus with a *measures* section (`mod-105`), regulator-tracker rows that name the obligations behind the *measures* (`mod-106`), and evaluation-evidence rows that cite the reports behind the *measures* actually working (`mod-107`).

Every one of those artefacts asserts that the enterprise *does* something. This module is the discipline that answers the question every internal auditor, external auditor, and regulator asks next: *show me the evidence you did it, and show me it was current at the time*.

That evidence lives in *controls*. A control is an enterprise-committed activity that mitigates a risk or satisfies an obligation. The AI system's risk register named the mitigations; the impact assessment named the measures; the eval-evidence row cited the reports. The control catalogue is where those get consolidated into a testable operating record — *description of the activity, owner, cadence, evidence of last execution, next test date* — so the enterprise can prove operating effectiveness rather than just design intent.

Designing that catalogue is not analyst-tier work. **Running the periodic test cycle** against it, **pulling** the evidence artefacts, **attaching** them to the GRC-platform control records, **flagging** the stale ones, and **producing** the control-status report internal audit reads *is*. This chapter fixes that scope, previews the delegation map that the rest of the module lives inside, and lists the vocabulary the analyst needs before chapters 02–09.

## What the analyst does with controls and compliance evidence

The analyst-tier verbs, in order:

1. **Reads** the control library the `senior-ai-governance-architect` has already published — the master list of controls, their required evidence types, and their test cadence per control class.
2. **Runs** the periodic control-testing cycle against the subset in scope for the current quarter, half, or year (whichever cadence the enterprise operates on).
3. **Pulls** the evidence artefacts — config exports, log samples, eval-report links, sign-off records, screenshots, interview notes — from the ML / infra / product owners named on each control record.
4. **Attaches** each artefact to the GRC-platform control record with a stable identifier, a *last verified* date, and a link to the source artefact.
5. **Flags** stale evidence — evidence older than the control's re-test window — and opens a follow-up with the named owner.
6. **Tags** each security-linked record with the OWASP LLM Top 10 / MITRE ATLAS / NIST AI 100-2 / SAIF category the threat sits under (chapters 04 and 05).
7. **Composes** the control-status report — the summary an internal auditor can review cold — and hands it to `internal-audit` for the quarterly / half-yearly / annual review (chapter 03).
8. **Escalates** the control gaps that need library-level treatment (a control that keeps failing, a control that no longer maps to any regulation, a control the enterprise has silently stopped operating) to `senior-ai-governance-architect` and the governance council (chapter 09).
9. **Runs**, in parallel, the third-party AI vendor / model / dataset intake cycle — reviewing model cards, sub-processor lists, DPAs, ISO/IEC 42001 certification letters, independent audit reports — and produces a vendor-risk-register row per third-party dependency (chapter 06).
10. **Maintains** the analyst-tier controls crosswalk — ISO/IEC 42001, NIST AI RMF, EU AI Act, SR 11-7, internal policy catalogue — so a downstream reader can walk from any single control to the obligations it satisfies and back (chapter 07).

None of these verbs *authors the master control library*. That distinction is the module's spine.

## What the analyst does not do

The analyst does not:

- **Design or version the master control library.** Choosing which controls exist, their wording, their cadence, and their required evidence class is `senior-ai-governance-architect` scope. The analyst runs the cycle against the library that role has published; the analyst does not silently add, remove, or re-word controls.
- **Author the security exploit, the pentest, or the mitigation code.** Recognising the *category* of an AI/LLM security threat is analyst-tier (chapters 04 and 05); reproducing the attack, running the pentest, writing the guardrail, or evaluating the exploit code is `ai-infra-security` scope.
- **Sign the vendor contract or approve the DPA.** Reading the vendor's model card, sub-processor list, DPA, ISO/IEC 42001 certification letter, and independent audit report to populate the vendor-risk-register row is analyst-tier (chapter 06). Negotiating the contract, redlining the DPA, and signing anything is `procurement` and `legal` scope.
- **Issue the internal-audit opinion.** Composing the control-status report is analyst-tier (chapter 03). Issuing an internal-audit opinion on whether controls are operating effectively is `internal-audit` scope. The analyst produces the input; `internal-audit` produces the opinion.
- **Certify controls against an external framework.** The enterprise's certification against ISO/IEC 42001, SOC 2, or an accredited independent audit is out of scope — those engagements are led by an external accredited body (chapter 08). The analyst's crosswalk (chapter 07) is an *internal* mapping artefact, not a certification statement.

Chapter 09 returns to this boundary in operational detail. The point at this stage: the analyst is a *cycle runner and reporter*, not a *library designer* and not an *auditor*.

## The two tangible outputs

Everything in this module reduces to two artefacts:

1. **The control-status report.** A periodic (typically quarterly) report that lists every control in scope for the period, the test results, the evidence artefacts, the stale-evidence flags, and the escalation queue. Internal audit reads it as the primary input to the periodic assurance opinion. Chapter 03 is the shape.
2. **The vendor-risk-register row set.** A row per third-party AI vendor / model / dataset the enterprise depends on, with the six vendor-evidence artefacts summarised, a residual-risk assessment, an inheritance decision, and a re-review date. The vendor-management office reads it as the primary input to renewal / off-boarding decisions. Chapter 06 is the shape.

Everything else — the OWASP tagging (chapter 04), the ATLAS / NIST AI 100-2 / SAIF recognition (chapter 05), the controls crosswalk (chapter 07), the ForHumanity / BABL AI credentialing awareness (chapter 08) — is instrumental to producing those two artefacts correctly.

## Where this module sits in the arc

- **Inputs.** The `senior-ai-governance-architect`-published master control library; the enterprise's inventory (`mod-102`); the enterprise's risk register with mitigations (`mod-103`); the enterprise's fairness-review notes (`mod-104`); the enterprise's impact-assessment corpus with the *measures* sections (`mod-105`); the enterprise's regulatory tracker (`mod-106`); the enterprise's eval-evidence rows (`mod-107`); the ML / infra / product teams' running system-of-record evidence (configs, logs, sign-off records); each third-party AI vendor's publicly available evidence (model card, sub-processor list, DPA extract, certification letter, audit report) plus their security-questionnaire responses.
- **Outputs.** A control-status report per period; a set of stale-evidence flags with named owners and follow-up dates; a vendor-risk-register row per third-party dependency; an analyst-tier controls crosswalk; an escalation register of the control gaps the `senior-ai-governance-architect` and the governance council need to act on.
- **Downstream consumers.** `mod-109` reads the control-status report as the first artefact when reconstructing what was in place at the time of an incident. `mod-110` reads the report summary and the escalation register into council briefings and into the policy-work agenda. `internal-audit` reads the full report as the input to the periodic assurance opinion. `procurement` / `legal` / vendor-management-office read the vendor-risk-register rows to inform contract renewal and off-boarding decisions.

## The vocabulary the analyst needs

- **Control.** An enterprise-committed activity that mitigates a specific risk or satisfies a specific obligation. Named ("`CTL-2026-0341 — Model input length is capped at 8000 tokens for all customer-facing endpoints`"), owned (a named person or team), evidenced (an artefact that shows the control operated in a given period), and cadenced (how often the operation is re-tested).
- **Control library.** The enterprise's master list of controls. Maintained by `senior-ai-governance-architect`. The analyst reads it, tests against it, and flags issues — the analyst does not silently edit it.
- **Control test.** One periodic pass at proving a control operated as designed. A test is *pass* (evidence present, current, and consistent with the control statement), *fail* (evidence missing, stale, or inconsistent), *deviation* (evidence present but shows the control operated differently than described), or *not-tested-in-period* (control was out of scope for the period; test deferred). Chapter 03 fixes the language.
- **Evidence artefact.** The concrete thing that shows the control operated. Chapter 02 walks the six classes: config export, log sample, eval-report link, sign-off record, screenshot, interview note. Each control record names the class it expects.
- **Stale evidence.** Evidence older than the control's re-test window. A control tested annually with evidence dated 400 days ago is stale; a control tested quarterly with evidence dated 100 days ago is stale. Chapter 02 fixes the flag rules.
- **Operating effectiveness.** The auditor's-language phrase for *the control not only exists on paper but actually operated in the period under review*. The control-status report supplies the evidence that supports this determination; `internal-audit` makes the determination.
- **Compensating control.** A different control that reduces the same risk when the primary control cannot be operated. The enterprise's control library — not the analyst — designates the compensating control per primary. The analyst records that a compensating control was invoked in the period; the analyst does not invent one.
- **Third-party AI vendor / model / dataset.** Any external supplier the enterprise's AI systems depend on — a hosted model provider (OpenAI, Anthropic, Google, Azure OpenAI, AWS Bedrock, Mistral), a self-hosted model taken from a public source (a Hugging Face weight file, a Meta Llama release, a Mistral release), a labelled or unlabelled dataset (a licensed data provider, a public dataset governed by a licence), or a tooling / evaluator vendor (a bias-audit vendor, a red-team vendor, a monitoring vendor). Chapter 06 walks the intake and row shape.
- **Vendor-risk-register row.** The analyst's tangible output per vendor. Chapter 06 fixes the row schema.
- **Controls crosswalk.** A mapping table that lists internal controls against the external frameworks that require them. Chapter 07 walks the analyst-tier subset (ISO/IEC 42001 clauses, NIST AI RMF sub-categories, EU AI Act obligations, SR 11-7 pillars, internal policy catalogue references).
- **Independent audit.** An external, accredited auditor's engagement that examines the enterprise's controls against a named framework and issues an opinion. ISO/IEC 42001 certification is one shape; a ForHumanity independent audit is another. Chapter 08 covers the two credential bodies the analyst encounters most.

## The delegation map — preview

Chapter 09 states this in full; here is the preview.

| Artefact / action | Role that owns | Role that supports |
|---|---|---|
| Master control library — content, wording, cadence, evidence-class expectations | `senior-ai-governance-architect` | `ai-governance-analyst` (raises library-level gaps) |
| Periodic control test — pulling evidence, attaching, flagging stale | `ai-governance-analyst` | ML / infra / product control owners |
| Control-status report for internal audit | `ai-governance-analyst` | `senior-ai-governance-architect` (reviews before hand-off), `internal-audit` (consumes) |
| Internal-audit opinion on operating effectiveness | `internal-audit` | `ai-governance-analyst` (supplies the report) |
| AI/LLM security threat analysis, exploit reproduction, pentest, mitigation code | `ai-infra-security` | `ai-governance-analyst` (files and routes the record) |
| Third-party AI vendor / model / dataset intake — reading published evidence, populating the vendor row | `ai-governance-analyst` | `procurement` / `legal` (contract, DPA), `ai-infra-security` (security questionnaire) |
| Vendor contract negotiation, DPA redlining, signature | `procurement` / `legal` | `ai-governance-analyst` (supplies the row) |
| Analyst-tier controls crosswalk (ISO/IEC 42001, NIST AI RMF, EU AI Act, SR 11-7, internal catalogue) | `ai-governance-analyst` | `senior-ai-governance-architect` (owns the master library it references) |
| External independent-audit engagement (ISO/IEC 42001 certification, ForHumanity independent audit, SOC 2, etc.) | Accredited external body | `head-of-ai-governance` / `senior-ai-governance-architect` (leads on the enterprise side); `ai-governance-analyst` (supplies the artefacts) |

The row in the middle — *control-status report for internal audit* — is the analyst's headline output. The row a few lines below — *vendor-risk-register row* — is the second. Everything else supports one of those two.

## What to memorise

- **The analyst runs the control cycle; `senior-ai-governance-architect` designs the library.** Testing, evidence-pulling, tagging, flagging, reporting, escalating are analyst-tier. Adding, removing, or re-wording controls is not.
- **The two tangible outputs are the control-status report and the vendor-risk-register row set.** Everything else in this module is instrumental to producing those correctly.
- **AI/LLM security recognition is filing depth, not exploit depth.** The analyst recognises the OWASP LLM Top 10 / MITRE ATLAS / NIST AI 100-2 / SAIF categories well enough to route a record; the analyst does not reproduce the attack.
- **Vendor intake reads published evidence into a row; procurement and legal own the contract.** The analyst's job stops at the row.
- **The controls crosswalk is an analyst-tier subset, not the master library.** The crosswalk table is a walk aid; the master library is `senior-ai-governance-architect`'s.

## Summary

This module turns the *the enterprise says it does X* signal that runs through every earlier module into the *the enterprise has evidence it did X in the period under review* artefact set that internal audit, external audit, and the vendor-management office rely on. The analyst is a cycle runner and reporter, not a library designer and not an auditor. The two headline outputs are the control-status report (chapter 03) and the vendor-risk-register row set (chapter 06). The horizontal disciplines the cycle depends on are the AI/LLM security taxonomy recognition (chapters 04 and 05), the controls crosswalk maintenance (chapter 07), and the independent-audit credentialing awareness (chapter 08). Chapters 02, 03, and 06 fix the row and report shapes; chapter 09 states the delegation boundary and the escalation classes; the exercises operationalise each into a runbook the analyst can execute on Monday morning.
