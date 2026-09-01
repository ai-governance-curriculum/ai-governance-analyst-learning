# Exercise 02 — Incident Record Composition

**Estimated effort:** 2 hours
**Grounding chapters:** [03 — Logging the Incident Against the Risk Register](../03-incident-record-and-register-linkage.md), [04 — Coordinating the Impact-Assessment Update](../04-coordinating-impact-assessment-update.md), [08 — Post-Incident Evidence Packaging for Council and Internal Audit](../08-post-incident-evidence-packaging.md), [09 — Delegation Boundary and Escalation Patterns](../09-delegation-boundary-and-escalation-patterns.md).

## Objective

Compose one worked `INC-<year>-<sequence>` incident record end-to-end for a supplied scenario, populating every field in chapter 03's row schema across the three temporally distinct events (intake, triage, post-mortem), driving the cross-reference block against the artefact set you have carried forward from `mod-102`, `mod-103`, `mod-105`, `mod-107`, and `mod-108`, coordinating the IA / FRIA / DPIA update per chapter 04's walk protocol, and closing the record with a rationale another analyst could pick up cold three quarters later.

The drill's point is not to invent an incident; it is to *operate the record shape* against a plausible scenario with the discipline chapter 03 fixes — the cross-references are IDs and bidirectional, severity is unset at intake, closure requires a rationale, silent gaps are the failure mode downstream artefacts inherit and cannot recover from. After this exercise you should be able to open the GRC platform on any Monday morning, given an intake ticket, and populate the intake-time subset of the record within thirty minutes without pausing to re-derive the shape.

## Prerequisites

- Chapter 03 read; the intake→triage→post-mortem cadence, the `INC-<year>-<sequence>` row shape (identifier and provenance; classification with reclassification history; the cross-reference block; containment and technical detail; governance follow-through; root cause and post-mortem; closure), the intake questionnaire's nine prompts, the cross-reference discipline (IDs not descriptions; bidirectional), and the weekly-roll-up interaction with the escalation register fresh in memory.
- Chapter 04 read; the four questions that decide whether an incident triggers an IA / FRIA / DPIA re-open (Q1 factual basis; Q2 residual materially different; Q3 measure commitment falsified; Q4 protected-group scope), the walk protocol, the sign-off routing.
- Chapter 08 read; the analyst-voice root-cause translation practice; the evidence-pack shape a downstream council or auditor reads.
- Chapter 09 read; the four escalation classes and the file-up threshold.
- Exercise 01's `mod-109-ex-01-incident-taxonomy.md` open if completed — one of that exercise's twelve tickets is the seed for this exercise's worked record. If not completed, the scenario is self-contained below.
- Your `mod-102` inventory rows (MCDA `INV-2026-0088`, MCDA-Benefits `INV-2026-0311`, and any RAG-augmented system you have carried forward — support-copilot, contract-review-assistant, HR-Policy-Bot, or the equivalent), your `mod-103` risk-register entries (`RISK-2026-*`), your `mod-105` impact-assessment corpus entries (`IA-2026-*`, `FRIA-2026-*`, `DPIA-2026-*`) with their *measures* sections, your `mod-107` eval-evidence rows (`EVAL-2026-*`), and your `mod-108` control records (`CTL-2026-*`) with any vendor rows (`VND-2026-*`) open for cross-reference.
- The [EU AI Act consolidated text](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) open for Article 3(49) and Article 73 clock-language verification at the *governance follow-through* section.

## Problem statement

The deliverable is a **single Markdown file, `mod-109-ex-02-incident-record.md`**, containing the worked `INC-<year>-<sequence>` record for the scenario below, plus the parallel artefacts the record's *governance follow-through* fields trigger.

### The scenario (self-contained)

On Friday **2026-09-04** at **14:23 Europe/Berlin**, a customer of the enterprise's contract-review-assistant (`INV-2026-0104`) — a RAG-based assistant used by law firms to draft comparative-clause memos from a curated statutes-and-case-law corpus — sent a support ticket to the enterprise's shared inbox. The customer, a partner at a mid-sized firm, wrote:

> *"We used your tool on Tuesday for a memo we filed on Wednesday. The memo cited a case (Chen v. Halcyon Systems, 2024 WL 8871123) as precedent for our position on limitation-of-liability. Opposing counsel notified us today that the case does not exist. Our filing has been withdrawn; the court has asked for a sanction memo by Monday. We need to know how this happened and what you're going to do about it."*

Inspection by the on-call ML engineer at 16:05 Europe/Berlin confirms:

- The tool retrieved four documents from the statutes-and-case-law corpus for the memo query; none contained the *Chen v. Halcyon* citation. The retrieval index does contain a shard of California appellate opinions but has no entry for the fabricated citation.
- The model's response cites the case with a verbatim quotation and a page number. Both are fabricated. The other three citations in the memo are real and correctly quoted.
- The customer's law firm is subject to the jurisdiction of a US state bar with an active AI-tool-misuse enforcement track; the enforcement bar has publicly noted a pattern of sanction filings against firms using AI tools without disclosure.
- The contract-review-assistant has an EU customer base (approximately 40% of monthly active users). It is not, by the enterprise's current classification, in the EU AI Act's high-risk scope — it is not one of the Annex III use cases, and no legal-diagnostic-support determination has been made.
- The affected system's most recent `EVAL-2026-0119` release-assurance evidence row cites *hallucination rate at 0.6% on the internal reference set of contract-drafting queries*. The reference set does not include comparative-clause memo queries with case-law-precedent asks; the analyst notes this gap on the record.
- The system has a `FRIA-2026-0033` under `mod-105` because the customer base includes several EU firms and the tool's outputs may affect legal advice to natural persons; the FRIA claims *human-review-of-every-output-before-filing* as a *measure*. The customer confirms they read the memo before filing and did not catch the fabricated citation.

The customer's firm has flagged its intent to (a) demand a public statement from the enterprise, (b) pursue an indemnification claim under the enterprise's business terms, and (c) consider a class-action against the enterprise on behalf of similarly-affected firms. Legal has been looped in by the account executive at 16:47 Europe/Berlin.

### Step 1 — Compose the intake-time record (§1)

Author a **§1 Intake-time record (T0 = 2026-09-04 16:52 Europe/Berlin)** section that populates the intake-time subset of the `INC-<year>-<sequence>` fields per chapter 03:

- Identifier and provenance block (Incident ID as `INC-2026-XXXX`; opened date; opened by; surface of report; source-of-report link with a placeholder URL).
- Classification block (AI-specific class per chapter 02; classical incident cross-reference *none for now*; external-corpus reference — the AIID has clusters on hallucinated legal citations, note the *closest-match* shape without inventing an identifier).
- Cross-reference block (Affected `INV-<year>-<sequence>` inventory row; empty or *TBD-at-triage* for `RISK`, `IA`/`FRIA`/`DPIA`, `EVAL`, `CTL`, `VND`, `PMS` at intake — populate with the specific IDs from your `mod-102`–`mod-108` corpus).
- Containment and technical detail block (Severity *unset*; availability state *available — under-monitoring*; containment actions *none-yet-at-T0*; duration of impact *2026-09-01 through 2026-09-04* per the customer's use; users / systems affected *one-firm-confirmed; unknown-others-at-risk*).
- Governance follow-through block (IA / FRIA / DPIA re-open status *evaluate-at-triage*; register-entry residual re-open status *evaluate-at-triage*; system-card / model-card update status *evaluate-at-triage*; customer / user notification status *drafted-by-legal-in-flight*; regulator notification status *not-triggered — non-Annex-III but Article 3(49)(c) fundamental-rights evaluation open*; control re-test status *evaluate-at-triage*; escalation register entries *none-yet-at-T0*).
- Root cause and post-mortem block (*post-mortem pending*).

Include the answers the intake questionnaire produced from the customer (via the account executive), rendered in the reporting party's voice.

Do not fabricate details the scenario did not provide. If the record needs a field you cannot honestly populate (a specific `EVAL-2026-*` identifier, a named risk owner, a GRC-platform ticket URL), use `TBD-<reason>` per chapter 03's discipline.

### Step 2 — Compose the triage-time update (§2)

Author a **§2 Triage-time update (T0 + 3 days = 2026-09-07 16:00 Europe/Berlin)** section that updates the record after the primary-route specialist has picked it up. Assume:

- `ai-eval-engineer` (metric owner) has confirmed the class as *class 5 — hallucination-driven harm* per chapter 02, with a secondary *class 1 — model regression* flag suspected pending re-eval on the current model version against a comparative-clause-memo reference set (currently under construction).
- Severity landed at *SEV-2 (high — external-customer harm confirmed; legal exposure open)* per the enterprise's ML incident-severity scale.
- Containment actions taken since T0: (a) the retrieval index was audited for any *Chen v. Halcyon* references (none found; the citation is a pure model confabulation); (b) a *legal-citation-must-be-retrieved* guardrail was deployed to the production system at 2026-09-06 19:14 Europe/Berlin, blocking any response that cites a case not present in the retrieved documents; (c) a customer-communication template was drafted by `legal` for outreach to all customers with active tool usage in the same jurisdiction cluster.
- The user-affected estimate is refined to *one-firm-confirmed harm; 12 firms with similar comparative-clause-memo query patterns in the same 30-day window; expansion in progress*.

Update the fields the triage event changed, log the reclassification history per chapter 03's *silent overwrites are a fail* rule, and drive the IA / FRIA / DPIA evaluation per chapter 04's four questions:

- **Q1 factual basis.** Does the incident change any factual claim in the FRIA's context or scope sections?
- **Q2 residual materially different.** Does the incident change the residual-risk claim materially?
- **Q3 measure commitment falsified.** Did the incident falsify the *human-review-of-every-output-before-filing* measure? The customer says they read the memo — does that count?
- **Q4 protected-group scope.** Is the harm concentrated on a protected group?

Record the answers with rationale on the *IA / FRIA / DPIA re-open status* field. If the answer is *triggered*, name the assessment-owner from your `mod-105` corpus and the walk-protocol timeline (chapter 04). If *not-triggered*, name the rationale.

### Step 3 — Compose the post-mortem-time completion (§3)

Author a **§3 Post-mortem-time completion (T0 + 21 days = 2026-09-25 12:00 Europe/Berlin)** section that completes the record after the engineering team's post-mortem lands. Assume:

- The post-mortem is filed as `PM-2026-0044` in the engineering team's wiki (use a placeholder URL).
- Root cause per the post-mortem: the model produced a confabulated citation because the prompt template asked for *"the most relevant precedent"* without requiring the citation to be traceable to a retrieved document, and the retrieval-augmented-generation configuration did not enforce a citation-provenance check at generation time. Contributing factors named: evaluation gap (the reference set did not include comparative-clause-memo queries), prompt-template drift (the *"most relevant precedent"* language was added by a product-manager-driven prompt edit in Q2 2026 without a corresponding eval), guardrail gap (no *citation-must-be-retrieved* guardrail was in place before this incident).
- Corrective actions per the post-mortem: (a) the *citation-must-be-retrieved* guardrail deployed at triage becomes permanent; (b) the prompt template is reverted to a *"only cite precedents present in the retrieved documents"* form; (c) the internal reference set is extended with comparative-clause-memo queries; (d) a customer-communication programme is launched with a system-card update.
- Preventive actions per the post-mortem: (a) a *prompt-template-change-requires-eval* control is added to the master control library; (b) a *citation-provenance-check* pattern is added to the RAG-application scaffold used by future systems.
- The re-eval on the current model version against the extended reference set completes; the *class 1 model regression* secondary is *not-confirmed* — the current model is no worse than the release-assurance baseline on the extended set. The class-1 secondary is closed on the reclassification history.

Populate the *root cause and post-mortem* block per chapter 03's schema. Translate the post-mortem's root cause into analyst-voice governance vocabulary per chapter 08's translation practice (three-to-five sentences, no jargon, cites the falsified assumption, names the systemic contributing factors, avoids blame).

Update the *governance follow-through* fields to their post-mortem-time status:

- IA / FRIA / DPIA re-open status — per your Step 2 evaluation, either *update-completed* (with FRIA version bump and IA reference update) or *deferred-with-rationale*.
- Register-entry residual re-open status — the `RISK-2026-*` entry whose residual-risk claim rested on the *human-review-of-every-output* assumption needs re-scoring; drive the re-scoring per `mod-103` chapter 05 and record the outcome.
- System-card / model-card update status — the affected system's system card, if published, needs a note on the *legal-citation-provenance-guarantee* the guardrail now enforces; drive per `mod-105` chapter 05.
- Customer / user notification status — per `legal` template, mark *sent* on a specific date for the affected firm and *sent-general* on a specific date for the wider customer base.
- Regulator notification status — the analyst's Article 3(49) evaluation: does the harm plausibly implicate (a) death or serious harm to health / (b) critical-infrastructure disruption / (c) fundamental-rights infringement / (d) serious harm to property or the environment? The affected system is not in Annex III scope, so Article 73 does not attach directly — record the *not-applicable-current-scope-but-flag-for-scope-review* rationale.
- Control re-test status — the *prompt-template-change-requires-eval* control does not yet exist; the analyst opens a `mod-108` library-design-fix escalation to `senior-ai-governance-architect` per chapter 09 class 1. The *citation-must-be-retrieved* guardrail is a new control that needs to be added to the master library and tested next cycle.
- Escalation register entries — file the class-1 library-design-fix escalation and, if the pattern of prompt-template edits without eval is broader than this one system, a class-4 governance-council decision escalation per chapter 09.

### Step 4 — Compose the closure block (§4)

Author a **§4 Closure (T0 + 45 days = 2026-10-19)** section that closes the record. Populate the closure block per chapter 03:

- Status — *closed-with-open-follow-through* if any corrective / preventive action is still in flight; *closed* only if every action is complete or explicitly deferred with rationale.
- Closed date; closed by.
- Closure rationale — one paragraph naming what was resolved, what was deferred, and why closure is appropriate. Chapter 03 was explicit: silent closure is a fail; the rationale is mandatory.
- Post-closure re-open history — empty at closure; the record has a re-open field that populates if the class-4 escalation surfaces a systemic pattern later.

The point of §4 is the discipline chapter 03 fixed: closure is not the same as *the containment worked and everyone went home*. Closure is the analyst's assertion that every follow-through item has completed or is on a tracked open track, that the register / IA / system-card updates have landed, and that the record is safe for downstream reference without a docent.

### Step 5 — Draft the parallel artefacts (§5)

Below the closure block, add a **§5 Parallel artefacts** section listing every artefact the record's *governance follow-through* fields triggered, each with a placeholder identifier and a one-line summary. At minimum:

- The FRIA update record — `FRIA-2026-0033-r2` with the *human-review-of-every-output* measure re-scoped and a new *citation-provenance-guardrail* measure added.
- The register-entry re-score record — `RISK-2026-0079-rescore-2026-10-08` (or the specific entry from your corpus) with the residual re-scored from *medium* to *high* pending the guardrail's operating evidence, then re-scored to *medium* after two consecutive months of clean guardrail-fire evidence.
- The system-card update — `system-card-INV-2026-0104-v3` with the new provenance guarantee published.
- The customer-notification records — the individual-firm notification (dated 2026-09-08 per `legal`) and the general-customer notification (dated 2026-09-14 per `legal`).
- The `mod-108` library-design-fix escalation — `ESC-2026-EX02-0001` under chapter 09 class 1, addressed to `senior-ai-governance-architect`, requesting the *prompt-template-change-requires-eval* control be authored into the master library.
- The `mod-108` control re-test — `CTL-2026-*-post-incident-retest` for the *human-review-of-every-output* control that the incident called into question; the re-test evidence (the customer's own confirmation that they read the memo) is compatible with the control passing on the process side even though the outcome failed; the analyst records the *control-passes-but-outcome-failed* pattern for chapter 09 as evidence that the control library itself needs re-design.
- The `mod-107` eval-evidence row for the extended reference set — `EVAL-2026-0119-r2` — with the new comparative-clause-memo queries and the current-model baseline.

Each parallel artefact is named with the analyst's coordinating verb (chapter 04's *coordinates*) and the named owner from your corpus.

## Requirements

- **Every field of chapter 03's row schema is populated** at its appropriate stage (intake / triage / post-mortem / closure). Fields the analyst cannot yet populate at intake are marked *unset* (severity) or *TBD-<reason>*; blank fields are not permitted.
- **Cross-references are IDs, not descriptions.** *Affected `INV-2026-0104`* is a cross-reference. *Affected the contract-review-assistant* is not. Every cross-referenced artefact is an ID from your `mod-102`–`mod-108` corpus; where you have not carried a specific ID forward, use a documented placeholder (`RISK-2026-XXXX` with an inline note) rather than a description.
- **Cross-references are bidirectional in narrative.** The record names the affected `INV-2026-0104`, and §5 confirms the analyst has written the `INC-2026-XXXX` identifier back to the inventory row's incident history field. Chapter 03 was explicit that bidirectional linkage is the analyst's responsibility if the GRC platform does not enforce it.
- **The intake-time record has severity *unset*.** Chapter 03 was explicit: intake severity is unset; the specialist's triage severity is what lands. A §1 that reads *severity: SEV-2* is off-side.
- **The reclassification history logs any class change with actor and date.** The scenario's *class 1 model regression secondary suspected at triage; not-confirmed at post-mortem* trajectory produces two entries.
- **The intake questionnaire's answers are in the reporting party's voice.** The customer's law-firm partner is not fluent in *class 5 hallucination-driven harm* vocabulary. The questionnaire captures what the partner said; the classification is the analyst's separate action.
- **The IA / FRIA / DPIA evaluation cites chapter 04's four questions.** Q1 factual basis, Q2 residual materially different, Q3 measure commitment falsified, Q4 protected-group scope. The evaluation is done at triage per chapter 04's *not-triggered by default is a fail* rule.
- **Q3 gets the load-bearing analysis on this scenario.** The FRIA's *human-review-of-every-output-before-filing* measure was met on the process — the customer read the memo — but the measure was not sufficient to catch the fabricated citation. Chapter 04 was explicit that a *technically-met-but-outcome-failed* measure is a re-open trigger; the record's evaluation must state this and coordinate the update.
- **The Article 73 evaluation on the record is complete.** The system is not in Annex III scope, so Article 73 does not attach — but the analyst records the walk of the four Article 3(49) outcome classes on the *regulator notification status* field with the *not-applicable-current-scope-but-flag-for-scope-review* rationale. Silent *not-applicable* is off-side.
- **The root-cause translation into analyst voice is three-to-five sentences.** Chapter 08 was explicit: no jargon, cite the falsified assumption, name the systemic contributing factors, avoid blame. The technical root cause stays in the post-mortem; the analyst's translation is what the council reads.
- **The closure rationale is a paragraph, not a sentence.** Chapter 03 was explicit: silent closure is a fail; a one-sentence closure that reads *"all actions complete; closing"* is silent closure with extra words.
- **The parallel artefacts in §5 are named per the analyst's coordinating verb.** *`legal` authors the customer notification; analyst tracks completion and records the date on the record's `customer notification status` field* is a coordinating statement. *analyst writes the notification* is off-side — chapter 01 and chapter 04 were both explicit that the analyst does not draft the update.
- **The `mod-108` escalation-register class assignment cites chapter 09's four classes.** *ESC-2026-EX02-0001 under class 1 library-design-fix* is complete; *ESC-2026-EX02-0001 under escalation* is incomplete.
- **No fabricated facts beyond the scenario.** If the analyst needs a specific `AIID Incident nnn` identifier, note the *closest-match* shape without inventing the number. If the analyst needs a specific state-bar enforcement citation, describe the shape and mark `<!-- illustrative — not from a real system -->`. Chapter 03 was explicit: the record is the audit surface; fabricated content in an audit surface is a fail.

## Starter guidance

- Do §1 first, then Step 2 without editing §1. Chapter 03's discipline is that intake is a distinct temporal event; the intake-time record is not retroactively updated with what the triage learned. Every triage update lives in §2 with its own timestamp and actor.
- The IA / FRIA / DPIA evaluation is the analyst's most consequential single action on this record. Chapter 04's four questions are the walk. Do not skip Q3 — the *technically-met-but-outcome-failed* measure is the load-bearing insight the scenario is engineered around.
- The Article 73 evaluation is not a *check the box* action. The affected system is not Annex III today, but the enterprise's scope-review process may add it (the customer base is 40% EU; the tool affects legal advice; the state-bar enforcement pattern is a fundamental-rights signal in a US context and would land as (c) *fundamental-rights infringement* if the system were in Annex III scope). The record's *regulator notification status* field carries this walk and its rationale.
- The analyst-voice root-cause translation is the artefact chapter 08 walks in full. Prefer *"the enterprise's assurance model claimed human review would catch fabricated citations; the assurance model did not envelop the case where a user with sound reading habits does not spot a plausible-looking fabrication in text they otherwise trust"* over *"the customer failed to catch the hallucination"*. The former names the systemic gap; the latter is blame.
- The parallel artefacts in §5 are the connective tissue chapter 03 called out. Do not skip the `mod-108` control re-test with the *control-passes-but-outcome-failed* pattern — that pattern is the escalation-register spine's meat and drives the class-1 library-design-fix.
- Where your `mod-102`–`mod-108` corpus has a specific ID you can carry forward for the cross-references (a specific `RISK` entry, a specific `FRIA` corpus row, a specific `EVAL` row), use it; the drill's value multiplies when the record threads through the artefacts you have already produced. Where you do not have a specific ID, use a documented placeholder rather than a made-up ID.
- Time-zone discipline matters on this record. The customer, the on-call engineer, and the analyst may be in different zones; the record's timestamps are stamped in the analyst's local zone with the original observer's zone in parentheses. The Article 73 clock (if it attached) is calendar days from the moment a person acting for the provider first learned of the incident; the analyst's *T0* on the record must match the first-awareness event, not the record-open action.

## Acceptance criteria

- `mod-109-ex-02-incident-record.md` filed with §1 intake-time record, §2 triage-time update, §3 post-mortem-time completion, §4 closure block, §5 parallel artefacts.
- §1 populates every intake-time field per chapter 03's schema; severity is *unset*; cross-reference block names `INV-2026-0104` and the placeholders for `RISK`, `FRIA-2026-0033`, `EVAL-2026-0119`, and any `CTL` / `VND` / `PMS` cross-references; the intake questionnaire's answers are in the customer's voice.
- §2 logs the reclassification history for the *class 1 secondary suspected* entry; sets severity to *SEV-2*; records the containment actions with timestamps; drives chapter 04's four-question evaluation with rationale on the *IA / FRIA / DPIA re-open status* field; names the FRIA owner and walk-protocol timeline if *triggered*.
- §3 lands the post-mortem identifier and link; carries the analyst-voice root-cause translation in three-to-five sentences per chapter 08; populates every *governance follow-through* field per its post-mortem-time status; opens the `mod-108` library-design-fix escalation and the control re-test.
- §4 closes with *closed-with-open-follow-through* (if any preventive action is still on the two-quarter track), a full paragraph closure rationale, and empty re-open history.
- §5 names every parallel artefact — FRIA update, register re-score, system-card update, customer notifications (individual and general), library-design-fix escalation, control re-test, extended eval-evidence row — with placeholder identifiers and the coordinating owner.
- No severity assigned at intake; no cross-references written as descriptions; no fabricated AIID / state-bar / regulator identifiers; the Article 73 walk is complete on the *regulator notification status* field.

## Stretch goals

- **A cross-reference-integrity check.** After §5, add a short *cross-reference-integrity check* that walks every ID named anywhere in the record (`INV`, `RISK`, `IA`/`FRIA`/`DPIA`, `EVAL`, `CTL`, `VND`, `ESC`, `PM`, system-card) and confirms each resolves to a live artefact in your corpus (or a documented placeholder). This is the `mod-108` control chapter 03 called out — *sample a set of `INC-*` records and confirm every ID they name resolves to a live artefact* — run as a self-test on the drill's record.
- **A weekly-roll-up entry.** Draft the weekly-roll-up entry the analyst would produce for the week of 2026-09-04 to 2026-09-11 that summarises the record's state at end-of-week (intake and triage complete; post-mortem in flight; FRIA update in flight; class-1 library-design-fix escalation open). Chapter 03 was explicit: the analyst runs a weekly roll-up against the escalation register.
- **A pattern-recognition note.** Draft a short pattern-recognition note the analyst would send to `head-of-ai-governance` if this incident is the second class-5 hallucination-driven-harm incident against a RAG-based tool in the enterprise's corpus within a rolling quarter. Chapter 03 and chapter 09 were both explicit: repeated incidents of the same class against the same system-family are policy work, not fresh incidents. The note names the pattern, cites the two incident records, and requests a council standing agenda item.
- **A council briefing preview.** Draft the two-slide preview a council briefing on this incident would land on (chapter 08's evidence-pack shape reduced to the council-tier surface). Slide 1: what happened, in one paragraph, in analyst voice. Slide 2: the systemic finding (the *technically-met-but-outcome-failed* human-review measure) and the requested council decision (endorse the library-design-fix escalation and the prompt-template-change-requires-eval control authoring).
- **A DPIA cross-check.** Even though this system is not Annex III, some of the affected data (the customer's memo, the retrieved statutes-and-case-law corpus) may involve personal data. Walk the `mod-105` DPIA question set for this scenario and record whether a DPIA was in force, whether it should have been, and whether the incident triggers one to be authored. This exercises the *DPO copy* discipline chapter 04 called out.

## Deliverables

- `mod-109-ex-02-incident-record.md` — §1 intake-time record, §2 triage-time update, §3 post-mortem-time completion, §4 closure block, §5 parallel artefacts, plus any stretch sections.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference record threaded through the MCDA / contract-review-assistant / MCDA-Benefits inventory the track uses, with one FRIA re-open trajectory (*human-review-of-every-output* measure re-scoped), one register re-score (`RISK-2026-*` residual bumped high then re-scored medium after two clean months), one system-card update, one class-1 library-design-fix escalation, and one *control-passes-but-outcome-failed* re-test note. Yours will differ in the specific IDs threaded through (per your `mod-102`–`mod-108` corpus), the specific timeline dates (per your local time zone and enterprise cadence), the specific coordinating-owner names, and the specific closure-rationale wording. What should not differ is (a) every chapter-03 field populated at its stage with severity unset at intake, (b) the reclassification history logged, (c) chapter 04's four-question walk on the FRIA re-open with Q3 as the load-bearing question, (d) the analyst-voice root-cause translation in three-to-five sentences per chapter 08, (e) the Article 73 walk on the *regulator notification status* field with the *not-applicable-current-scope-but-flag-for-scope-review* rationale, (f) the full parallel-artefacts list in §5, and (g) no fabricated identifiers beyond the scenario. A tight record that another analyst could pick up cold three quarters later beats a longer record that reads as narrative and leaves the operational specifics to the reader's imagination.
