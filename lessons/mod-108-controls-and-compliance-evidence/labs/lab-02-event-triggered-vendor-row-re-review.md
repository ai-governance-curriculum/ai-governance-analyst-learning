# Lab 02 — Event-Triggered Vendor-Row Re-Review on a Certification Lapse and a New Sub-Processor

**Duration:** 2 hours.
**Grounding chapters:** [06](../06-third-party-ai-vendor-and-model-intake.md), [08](../08-independent-audit-and-bias-auditor-credentialing-forhumanity-and-babl-ai.md), [09](../09-delegation-boundary-and-escalation-patterns.md).
**Difficulty:** Core — exercises the chapter-06 twenty-two-column `VND-<year>-<sequence>` row shape and the ten-step intake sequence, the chapter-08 ForHumanity / BABL AI / ISO/IEC 42001 / IAF-accreditation discipline, and the chapter-09 Class-3 vendor / contract escalation shape against a pre-assembled vendor-row snapshot where two events (an ISO/IEC 42001 certification lapse *and* a new sub-processor in an un-approved jurisdiction) have fired between the annual re-review cadence. Exercise 04 authors fresh vendor rows from the public evidence sweep onward; this lab exercises the *event-triggered re-review* — the specific workflow that runs between annual cadences when a vendor-side event (certification lapse, new sub-processor, DPA change, breach notice, model-version change) fires the re-review rule from chapter 06's cadence discipline.

## Objective

Take a *fixed, pre-assembled* vendor-row snapshot — one `VND-<year>-<sequence>` row filed in the prior annual cycle, with two deliberately-induced events that have fired since — and run the event-triggered re-review. Refresh the twenty-two-column row against the public and private evidence states the lab provides, update the residual-risk paragraph, redraft the inheritance decision if the evidence state no longer supports the prior decision, and file the chapter-9 Class-3 escalation to `procurement` / `legal` / `data-protection-officer` with the correct routings. Close by cross-referencing the re-review into the `CTL-2026-0352` vendor-DPA-currency control-test row (from the paired `mod-108` lab-01 fixture — the two labs are consistent at the vendor + DPA layer by design, and the artefacts produced in this lab are what a mid-cycle sweep would consume on the control side).

The deliverable is three Markdown files in `~/aicg-labs/mod-108-lab-02/`:

- `vendor-row-refresh.md` — the refresh walk log, one sub-section per changed column.
- `vnd-2026-0044-refreshed.md` — the refreshed vendor row in the chapter-6 twenty-two-column shape, superseding the prior row with a stable pointer-back.
- `escalation-register.md` — the `ESC-<year>-<sequence>` Class-3 entries authored from the re-review, projected into the chapter-9 register shape.

A reviewer should be able to read all three in twenty minutes and see every column refreshed, every event explicitly accounted for, the residual-risk paragraph updated honestly, the inheritance decision re-drawn where the evidence calls for it, and every escalation routed per the chapter-9 Class-3 template.

## Prerequisites

- Chapters 06, 08, and 09 read; the six vendor-evidence artefact classes (model card, sub-processor list, DPA, ISO/IEC 42001 certification letter, adjacent attestations + independent audit report, security questionnaire response), the twenty-two-column `VND-<year>-<sequence>` row schema, the ten-step intake sequence, the three inheritance decisions (*inherit*, *inherit-with-compensating-controls*, *do-not-inherit*), the four independent-audit shapes (management-system certification; assurance engagement; independent audit of algorithmic systems; bias audit), the IAF Multilateral Recognition Arrangement, the chapter-6 common failure modes (trust-portal drift; certification-letter theatre; DPA fresh-in-file, stale-in-fact; model card is a marketing page; sub-processor list without geographic detail; inheritance decision without residual-risk paragraph; missing compensating-controls anchor; vendor rows that never re-review), and the chapter-9 Class-3 escalation template fresh in memory.
- A Markdown editor; no Python or vendor-portal access required — the snapshot below is a Markdown-only stand-in for what would live in the vendor-management platform in production.
- Exercise 04 completed, or at minimum skimmed, so the twenty-two-column schema and the ten-step intake order are familiar. This lab starts at step 10 of a prior intake (the annual re-review that would be next) and runs the *event-triggered* path, which re-enters at step 3 (public evidence sweep) rather than running the full ten-step cycle.
- The paired `mod-108` lab-01 completed, or at minimum skimmed, is helpful but not required — the `VND-2026-0044` identifier in that lab's fixture is the same vendor referenced here, so the two labs compose into a single consistent picture of the vendor-plus-control cross-link.
- The [IAF Members list](https://iaf.nu/en/iaf-members/), the [OpenAI Trust Portal](https://trust.openai.com/), the [Anthropic Trust Center](https://trust.anthropic.com/), and the [Cloud Security Alliance CAIQ reference](https://cloudsecurityalliance.org/artifacts/consensus-assessments-initiative-questionnaire-v4/) are useful to have open as public-evidence sources; the fixture below does not depend on them but references their shape.

## The fixed input — a deliberately-event-triggered vendor-row snapshot

Use *exactly* this snapshot. Do not substitute identifiers, dates, vendor or jurisdiction names, or report titles, and do not pre-correct the drift — the drift is the point of the lab. Each field is reproduced only at the level a re-reviewer reads from. Treat the whole block as `pedagogic example — vendor names, identifiers, and dates illustrative; do not reuse in audit-facing artefacts without verifying against the real vendor's current state`.

### A. The prior-year vendor row (as filed 2026-02-10)

```
VND-2026-0044 — [hosted-foundation-model-vendor-X]
  Dependency class:         hosted-foundation-model
  Named artefact:            [hosted-foundation-model-vendor-X] Model family M via
                             enterprise API tier
  Enterprise integration:    INV-2026-0088 (MCDA), INV-2026-0091 (support-chat-
                             copilot), INV-2026-0104 (contract-review-assistant);
                             API endpoint via enterprise-managed proxy
  Data classification:       public, internal, confidential (no personal data by
                             contract; no restricted; no special-category); DPO
                             sign-off on scope recorded on original intake
  Contract owner:            procurement-lead@
  Technical owner:           ml-platform-lead@

  Model card:                URL + v2025-10 + summary: intended-use covers general
                             text generation, out-of-scope covers un-grounded
                             medical/legal advice, known-limitations cover
                             hallucination, over-refusal, jailbreak resilience;
                             vendor publishes per-release safety-evaluation
                             coverage.
  Sub-processor list:        URL + snapshot 2026-01-15; nine named sub-processors
                             across US-East, US-West, EU-Frankfurt, EU-Amsterdam,
                             Singapore, Tokyo; all within the enterprise's
                             approved data-transfer footprint; vendor commits to
                             14-day notification on new sub-processors.
  DPA:                       Version v2025-11-01; SCCs (2021 EU standard) as
                             transfer mechanism; audit right: on 30 days' notice,
                             once per 12 months; sub-processor terms incorporated
                             by reference to the trust-site list.
  ISO/IEC 42001 certif.:     Body [IAF-signatory certification body Z]; scope: the
                             named enterprise API tier only; effective 2025-04-01;
                             expiry 2028-04-01; no qualifications.
  Adjacent attestations:     ISO/IEC 27001 (body A; effective 2024-09; valid);
                             SOC 2 Type II (body B; FY2025 report; covers security,
                             availability, confidentiality).
  Independent audit:         Not applicable — vendor has not commissioned an
                             independent audit of AI systems; relies on the
                             ISO/IEC 42001 certification and the SOC 2 report.
  Security questionnaire:    CAIQ v4.0.3; vendor's pre-filled response dated
                             2025-12-05; no inconsistencies with items 1-5.
  OWASP / ATLAS / 100-2 /    LLM02:2025 — Sensitive Information Disclosure (vendor
    SAIF tags:               publishes known-limitation on training-data leakage
                             under adversarial prompting; not a current finding,
                             just a vendor-side acknowledged limitation).

  Residual-risk assessment:  The vendor's management system is ISO/IEC 42001
                             certified by an IAF-accredited body with a scope that
                             covers the exact tier the enterprise consumes; the
                             DPA reflects the current transfer mechanism; the sub-
                             processor list is complete and in-footprint; the
                             security posture is externally attested at a current
                             SOC 2 Type II level; the model card is Mitchell-
                             shaped with stated intended-use and known-
                             limitations. Residual risk is low on the governance-
                             posture dimension and medium on the model-behaviour
                             dimension (jailbreak resilience, hallucination under
                             grounding gap) — the latter is addressed by
                             enterprise-side compensating controls (CTL-2026-0341
                             guardrails; CTL-2026-0344 RAG eval; CTL-2026-0355
                             release-assurance sign-off).

  Inheritance decision:      inherit-with-compensating-controls.
  Compensating controls:     CTL-2026-0341, CTL-2026-0344, CTL-2026-0355,
                             CTL-2026-0352.
  Re-review cadence:         Annual + on-event (vendor breach, DPA change, new
                             sub-processor, certification lapse, model-version
                             change).
  Last reviewed:             2026-02-10.
  Next review:               2027-02-10 or on-event.
  Analyst note:              Baseline intake; vendor is a key dependency for
                             three High-tier systems; event-triggered re-review
                             rule is especially load-bearing here.
```

### B. Related artefact identifiers

```
INV-2026-0088    MCDA                                        Tier: High
INV-2026-0091    support-chat-copilot                        Tier: Medium
INV-2026-0104    contract-review-assistant                   Tier: High
CTL-2026-0341    Jailbreak-classifier + human-review queue
CTL-2026-0344    MCDA-Benefits RAG groundedness
CTL-2026-0352    Vendor DPA currency (the cross-link to lab-01)
CTL-2026-0355    High-tier release-assurance sign-off
POL-2026-0022 §3 Enterprise data-transfer-footprint policy
REG-2026-EU-001  EU AI Act
REG-2026-EU-002  GDPR (processor obligations under Article 28)
ESC-2026-LAB01-11 Class-3 escalation on CTL-2026-0352 + VND-2026-0044
                 (filed in lab-01; this lab's escalation entries compose with it)
```

### C. What has changed in the year since the row was filed

Treat today as **2026-11-14**. The following events are known to have occurred since the row was filed on 2026-02-10. Some are reflected in the row above; some are *not*. The re-reviewer's job is to notice which is which.

1. **Certification body Z** — the IAF-signatory body that issued `[hosted-foundation-model-vendor-X]`'s ISO/IEC 42001 certificate — was suspended by its national accreditation authority on 2026-09-02 for 90 days pending review of its AI-management-system assessment methodology. The vendor's certificate remains *dated through 2028-04-01* on the vendor's trust site, but the certifying body's accreditation is suspended as of the lab date. The vendor has not publicly commented; the trust site still displays the certificate.
2. **Sub-processor list** — snapshot 2026-10-28 (from the vendor's trust site) lists ten named sub-processors; the tenth is a new addition on 2026-10-22, located in Jurisdiction Y, which is *outside* the enterprise's approved data-transfer footprint per `POL-2026-0022 §3`. The vendor met its 14-day notification obligation via the trust-site update; the enterprise's vendor-management-office intake-notification process did not fire.
3. **DPA** — unchanged since 2025-11-01; the transfer mechanism (SCCs 2021) does not reference Jurisdiction Y as an approved recipient-country category.
4. **Model card** — refreshed by the vendor on 2026-08-15; the refresh added safety-evaluation coverage for an agentic tool-use capability the vendor has released on the API tier. The known-limitations catalogue is expanded (indirect-prompt-injection resilience added; tool-call authorisation known-limitation added). No breaking changes to the existing evaluated capabilities.
5. **Security questionnaire** — the vendor published a refreshed CAIQ v4.0.3 response on 2026-09-10 with no material changes; however, the questionnaire response still cites the same ISO/IEC 42001 certificate (see event 1) without reference to the certifying-body accreditation status.
6. **Independent audit** — the vendor published a bias-audit report on 2026-07-20, commissioned from a BABL-trained auditor, against ForHumanity's audit criteria set for AEDT-adjacent high-risk domains, scope covering the hiring-adjacent use of Model M. The audit opinion is *qualified* with two exceptions tied to disaggregated performance on language-pair subsets; management response commits to mitigation on both.
7. **Breach notices / incidents** — none in the current year.
8. **Model-version change** — the vendor rotated Model M's identifier from `vendor-X/model-M-2025-10` to `vendor-X/model-M-2026-08` on 2026-08-15 alongside the model-card refresh. MCDA, support-chat-copilot, and contract-review-assistant deployments were migrated by the ML platform team on 2026-09-01 after re-running release-assurance against the new identifier.

## Steps

### Step 1 — Scaffold the refresh log and the row-superseding structure (10 min)

Create the working folder and files.

```bash
mkdir -p ~/aicg-labs/mod-108-lab-02
cd ~/aicg-labs/mod-108-lab-02
touch vendor-row-refresh.md vnd-2026-0044-refreshed.md escalation-register.md
```

Open `vendor-row-refresh.md` and lay in the structure up front.

```markdown
# VND-2026-0044 event-triggered re-review — 2026-11-14

Reviewer:       <your-name>
Review date:    2026-11-14
Prior row:      VND-2026-0044 filed 2026-02-10
Trigger set:    certification-body accreditation suspended (event 1);
                new sub-processor outside approved footprint (event 2);
                vendor model card refreshed (event 4);
                vendor model-version rotated (event 8);
                vendor bias-audit published (event 6).

## Pre-review event list (from Section C)

## Column-by-column refresh

### Column 9 — Model card
### Column 10 — Sub-processor list
### Column 11 — DPA
### Column 12 — ISO/IEC 42001 certification
### Column 13 — Adjacent attestations
### Column 14 — Independent audit report
### Column 15 — Security questionnaire
### Column 16 — OWASP / ATLAS / 100-2 / SAIF tags
### Column 17 — Residual-risk assessment
### Column 18 — Inheritance decision
### Column 19 — Compensating controls
### Column 20 — Re-review cadence
### Column 21 — Last reviewed / Next review
### Column 22 — Analyst note

## Escalations authored from this re-review

## Cross-link to the control side (CTL-2026-0352 + lab-01 escalation)

## Re-review verdict

## Pre-close completeness check
```

Open `vnd-2026-0044-refreshed.md` and copy the twenty-two-column shape from chapter 06 as the target skeleton; this is the row that supersedes the 2026-02-10 row on issue.

Open `escalation-register.md` and lay in the entry-plus-table skeleton.

### Step 2 — Walk the trigger set and confirm the re-entry point (10 min)

Chapter 06 §"The pull sequence" names the ten-step intake. The *annual* re-review runs the full ten steps. The *event-triggered* re-review re-enters at step 3 (public evidence sweep) when the trigger is a public-side event and runs through steps 4–10. The reviewer explicitly records which events fired from the Section-C change list and which step each event re-enters at.

Populate the `## Pre-review event list (from Section C)` section with a one-line-per-event block:

- *Event 1 — certifying-body accreditation suspended 2026-09-02; re-enters at step 4 (private evidence request) for the vendor's response plus step 3 (IAF portal re-verification) for the accreditation status.*
- *Event 2 — new sub-processor in Jurisdiction Y 2026-10-22, outside approved footprint; re-enters at step 2 (data classification and DPA scope) plus step 5 (consistency check between the trust-site update and the DPA text).*
- *Event 4 — model card refreshed 2026-08-15; re-enters at step 3 (public evidence sweep).*
- *Event 6 — vendor bias-audit published 2026-07-20 with qualified opinion and two exceptions; re-enters at step 3 (public evidence sweep) plus step 5 (consistency check with the vendor's representations in the security questionnaire).*
- *Event 8 — model-version rotation 2026-08-15; re-enters at step 1 (enterprise intake row confirmation) to re-verify the `INV-<year>-<sequence>` systems' current deployment state.*

The purpose of listing these up front is that the step-7 residual-risk draft and the step-8 inheritance decision require the full event set to be visible — a partial list is where the chapter-6 *inheritance decision without residual-risk paragraph* failure mode lands.

### Step 3 — Refresh columns 9–16 (the evidence-column refresh) (20 min)

Walk the six vendor-evidence artefact classes against the current evidence state. For each, record the *before* (from the 2026-02-10 row) and the *after* (from the current evidence) on the per-column sub-section in `vendor-row-refresh.md`, and populate the corresponding cell on `vnd-2026-0044-refreshed.md`.

- **Column 9 — Model card.** Before: URL + v2025-10; after: URL + v2026-08-15 + summary updated to include agentic tool-use capability and expanded known-limitations catalogue (indirect-prompt-injection resilience; tool-call authorisation). Include the vendor's known-limitation list so that enterprise-side compensating controls can map against each; note the agentic tool-use capability as a *new deployment surface* for downstream crosswalk re-anchoring (chapter 07 — may trigger a `senior-ai-governance-architect` review on LLM06 Excessive-Agency control coverage if the enterprise has enabled the capability).
- **Column 10 — Sub-processor list.** Before: nine sub-processors in-footprint, snapshot 2026-01-15; after: ten sub-processors, snapshot 2026-10-28, tenth in Jurisdiction Y *outside* the enterprise's approved footprint. Record both the snapshot date and the list length delta; name the Jurisdiction Y sub-processor explicitly with its listed function (per the vendor's trust-site naming — the lab's fixture does not name the function, so record *function not specified on trust site* and add a follow-up request to the vendor's account team).
- **Column 11 — DPA.** Before: v2025-11-01, SCCs 2021, audit right on 30 days' notice, sub-processor terms incorporated by reference; after: unchanged on vendor side but *stale-in-fact* per chapter 06's named failure mode — the current sub-processor list references Jurisdiction Y, which the DPA's transfer-mechanism language does not. Record the DPA as unchanged *in text* but flagged as *stale-in-fact* on the column; the finding is the DPA-to-trust-site divergence, not a DPA content change.
- **Column 12 — ISO/IEC 42001 certification.** Before: Body Z, IAF-accredited, scope covers the enterprise API tier, effective 2025-04-01, expiry 2028-04-01; after: certificate still dated through 2028-04-01 but *certifying body's accreditation is suspended for 90 days from 2026-09-02* — the certificate is *in a pending state*, not *valid* and not *expired*. The vendor has not commented. This is the chapter-6 *certification-letter theatre* adjacent failure mode — the certificate looks valid on the trust site but the *IAF-signatory status* behind it is suspended. Record the raw facts on the column and flag the certification as *provisional — body accreditation suspended; awaiting vendor statement and / or IAF re-instatement*. Do *not* downgrade to *not-certified* without running the chapter-8 Class-3 escalation first.
- **Column 13 — Adjacent attestations.** Before: ISO/IEC 27001 (body A; 2024-09; valid), SOC 2 Type II (body B; FY2025); after: unchanged. Record explicitly to show the reviewer walked the column rather than silently carrying forward (chapter 06 *bare attachments are not evidence* discipline applies to the walk, not just the attachment).
- **Column 14 — Independent audit report.** Before: not applicable — vendor had not commissioned an independent audit; after: vendor commissioned a bias-audit report on 2026-07-20 against ForHumanity's AEDT-adjacent criteria set, by a BABL-trained auditor, scope covering hiring-adjacent use of Model M, opinion *qualified* with two exceptions on language-pair performance disaggregation and a management response committing to mitigation on both. Record (a) auditor identity; (b) BABL training credential as *credentialing* (not a certification body in the IAF sense per chapter 08); (c) ForHumanity criteria set as the *criteria origin* (distinct field — do not conflate with the credential); (d) scope (hiring-adjacent use of Model M, *not* the general-purpose API tier the enterprise uses); (e) period; (f) opinion (*qualified*); (g) two exceptions with management response status. Important: the audit scope is *hiring-adjacent* — the enterprise does *not* use Model M for AEDT in NYC hiring on the current integrations (`INV-2026-0088` MCDA is marketing-copy; `INV-2026-0091` support-chat; `INV-2026-0104` contract-review); record the audit as *informative but out-of-scope for the enterprise's current deployment* so a downstream reader does not over-interpret the inheritance implications.
- **Column 15 — Security questionnaire.** Before: CAIQ v4.0.3, 2025-12-05 response, no inconsistencies; after: refreshed response 2026-09-10 with no material changes — but the response still cites the ISO/IEC 42001 certificate as *valid* without reference to the certifying-body accreditation suspension. This is a chapter-6 *consistency-check-vs-vendor-published-artefacts* finding: the questionnaire asserts certification status that the trust-site certificate itself may no longer substantiate. Record and open a follow-up with the vendor to clarify.
- **Column 16 — OWASP / ATLAS / 100-2 / SAIF tags.** Before: LLM02:2025 (vendor-side known-limitation on training-data leakage under adversarial prompting); after: add LLM06:2025 (Excessive Agency — the new agentic tool-use capability is a known-limitation surface the vendor has acknowledged in the refreshed card, and the enterprise's compensating-controls set needs to cover tool-set / permission / autonomy per chapter 04). Carry the AI 100-2 attack-class family citation for each (Privacy for LLM02; Evasion + Abuse for LLM06 depending on exploit path). ATLAS technique identifiers: record only if the source artefact names any; the vendor's refreshed card does not, so do not manufacture.

### Step 4 — Draft the residual-risk paragraph (column 17) (15 min)

Chapter 06 §"The pull sequence" step 6 names the residual-risk paragraph as the gating draft before the inheritance decision. Do not skip to step 7 (compensating controls) or step 8 (inheritance decision) before the paragraph is written.

Open the `### Column 17 — Residual-risk assessment` sub-section and draft the paragraph. The paragraph should name the three dimensions the 2026-02-10 paragraph did (governance-posture, model-behaviour, data-flow) plus the new dimensions the events have introduced (certification posture; sub-processor jurisdictional posture; deployment-surface expansion to agentic tool-use). A plausible draft:

> *Residual risk has moved materially on three dimensions since the 2026-02-10 baseline. **Certification posture** has degraded from *IAF-accredited certifying body* to *pending IAF-accredited body* following the 2026-09-02 suspension of certifying body Z's national accreditation; the certificate itself is dated through 2028-04-01 and the vendor has not commented, so the certification's evidentiary weight is provisional pending vendor statement and / or IAF re-instatement — the enterprise cannot treat the certificate as current-tier assurance until that resolves. **Sub-processor jurisdictional posture** has degraded from *all sub-processors in approved footprint* to *nine of ten in approved footprint, one in Jurisdiction Y outside footprint per `POL-2026-0022 §3`*; the DPA (v2025-11-01) does not reference Jurisdiction Y as an approved recipient-country category, so the data-flow posture is now *potentially non-compliant with the enterprise's own transfer-mechanism policy* pending a DPA re-negotiation or a vendor-side removal of the Jurisdiction Y sub-processor. **Deployment-surface** has expanded from *text generation only* to *text generation plus agentic tool-use*; the vendor has acknowledged this in the refreshed 2026-08-15 model card with new known-limitations (indirect-prompt-injection resilience; tool-call authorisation) — the enterprise does not currently consume the agentic capability on any of the three integrated systems, so the surface expansion is *latent* rather than *active*. Model-behaviour dimension (jailbreak resilience, hallucination under grounding gap) is unchanged, and the enterprise's compensating controls (`CTL-2026-0341`, `CTL-2026-0344`, `CTL-2026-0355`) continue to address it; the vendor's bias-audit report (2026-07-20, qualified opinion, hiring-adjacent scope) is informative but scope-out-of-enterprise-use and does not directly affect the inheritance decision for the current integrations.*

The paragraph is deliberately long on purpose — chapter 06 names a *missing residual-risk paragraph* as a named failure mode, and a one-sentence hedge is functionally the same miss.

### Step 5 — Redraft the inheritance decision and compensating controls (column 18 + 19) (15 min)

With the residual-risk paragraph in hand, draft columns 18 and 19. The 2026-02-10 row read *inherit-with-compensating-controls* — the question is whether the current evidence state still supports that, supports a move to *do-not-inherit* until specific gaps close, or supports a scope-narrowing that keeps *inherit-with-compensating-controls* but names the pause-conditions.

A plausible redraft:

- **Column 18 — Inheritance decision.** *inherit-with-compensating-controls — with pause-conditions*. The pause-conditions are the two gating resolutions: (a) vendor statement on the certifying-body suspension and / or IAF re-instatement of body Z; and (b) DPA re-negotiation to reflect Jurisdiction Y, or vendor-side removal of the Jurisdiction Y sub-processor. If either resolution lands adversely (vendor declines to comment on the suspension, or vendor refuses DPA re-negotiation), the decision moves to *do-not-inherit* and the enterprise pauses net-new use of Model M pending executive decision. The baseline enterprise-side compensating controls (chapter 04's LLM01 / LLM06 / LLM07 surfaces; chapter 05's SAIF *Expand strong security foundations* + *Adapt controls* elements) continue to carry the model-behaviour-dimension residual.
- **Column 19 — Compensating controls.** Carry `CTL-2026-0341`, `CTL-2026-0344`, `CTL-2026-0355`, and `CTL-2026-0352` (the DPA-currency control itself). Add a *proposed new control* flag to `senior-ai-governance-architect` for coverage of the agentic tool-use surface if the enterprise moves to enable it — do *not* draft the new control statement (chapter 07's *analyst suggests, architect decides* line; a Class-1 escalation is the correct shape for the suggestion).

Record both columns on the refresh log and on the refreshed row.

### Step 6 — Set cadence, dates, and the superseding pointer (column 20–22) (10 min)

Open `vnd-2026-0044-refreshed.md` and populate the remaining columns.

- **Column 20 — Re-review cadence.** Annual + on-event. The event-triggered re-review itself resets the next-cadence date; add an explicit *60-day follow-up on each pause-condition* so the row doesn't drift into *never re-reviewed* if the pause-conditions stall (chapter 06 *vendor rows that never re-review* failure mode).
- **Column 21 — Last reviewed / Next review.** Last reviewed: 2026-11-14. Next review: 2027-01-13 (60-day pause-condition follow-up) or on resolution of either pause-condition, whichever is sooner; full annual re-review at 2027-02-10 regardless.
- **Column 22 — Analyst note.** One paragraph. Record the event list, the pause-conditions, the cross-link to `CTL-2026-0352` and `ESC-2026-LAB01-11`, and the *do-not-inherit fallback* language so a future reviewer picking up the row knows the conditional structure of the decision.

On the refreshed-row file, record the row's supersession pointer up front (chapter 06 *the row supersedes any earlier vendor row for the same vendor + named-artefact combination* discipline):

```
VND-2026-0044 (refreshed 2026-11-14)
  Supersedes:   VND-2026-0044 (filed 2026-02-10; closed on supersession)
  Reason:       Event-triggered re-review per chapter 06 cadence; five events
                (1, 2, 4, 6, 8 from the lab's Section C) fired between the
                annual cadence dates.
```

The prior row is *closed with a pointer to the new one*; the refreshed row is the record the vendor-management office and `CTL-2026-0352` now cite.

### Step 7 — Author the Class-3 escalation entries (20 min)

Open `escalation-register.md`. The re-review generates two full Class-3 entries and one Class-1 entry; author each with the chapter-9 per-class template. One of the entries (on the DPA + sub-processor) composes with `ESC-2026-LAB01-11` from the paired lab-01 — the two entries share a target but file to different artefacts (lab-01's is routed through the control-cycle side; this lab's is routed through the vendor-management side; both reference the same `VND-2026-0044` fact set).

- **`ESC-2026-LAB02-01` — Class 3 vendor / contract action on the certifying-body accreditation suspension.** Rationale: `VND-2026-0044`'s ISO/IEC 42001 certificate is dated through 2028-04-01 but the issuing body's national accreditation is suspended 2026-09-02 for 90 days; the certificate's evidentiary weight as an IAF-signatory-body-issued attestation is provisional until IAF re-instates or the vendor migrates to another IAF-signatory body. The vendor's refreshed CAIQ response still cites the certificate without reference to the suspension — a consistency-check finding. Route to `procurement` and `data-protection-officer` (the DPA references the certification as an assurance anchor); copy `senior-ai-governance-architect` for the control-library implications; copy `ai-infra-security` for the security-posture angle. Requested action: *obtain a vendor statement on the certifying-body status; request a current IAF portal confirmation on body Z's accreditation state at resolution; evaluate whether the enterprise should treat the certification as valid in the interim*. Target: 2026-12-15 (acknowledgement); 2027-01-13 (statement). Impact on inheritance decision: if the vendor declines to comment or the suspension extends past the 90-day window without re-instatement, the inheritance decision moves to *do-not-inherit* pending executive sign-off.
- **`ESC-2026-LAB02-02` — Class 3 vendor / contract action on the Jurisdiction Y sub-processor and the DPA divergence.** Rationale: `VND-2026-0044`'s 2026-10-28 sub-processor list adds a new sub-processor in Jurisdiction Y (outside `POL-2026-0022 §3` approved footprint); the DPA (v2025-11-01) does not reference Jurisdiction Y as an approved recipient-country category; the enterprise is relying on a transfer mechanism that does not extend to the new sub-processor's jurisdiction. Route to `procurement`, `legal`, and `data-protection-officer`; copy `ai-infra-security` for the security questionnaire follow-up; copy the technical owner for context. Requested action: *(a) re-negotiate DPA to reflect Jurisdiction Y with the appropriate transfer-mechanism language, or (b) request vendor-side removal of the Jurisdiction Y sub-processor, or (c) carve out an enterprise-side pause on use of Model M across the three integrated systems pending resolution — the accountable executive selects the option*. Target: 2026-11-28. Note the explicit *requested* language on the pause (chapter 09 *analyst does not pause unilaterally*). Cross-link to `ESC-2026-LAB01-11` from the paired lab's control-side filing. Impact on inheritance decision: see `ESC-2026-LAB02-01` — compounding pause-conditions.
- **`ESC-2026-LAB02-03` — Class 1 library-design fix on the agentic-tool-use deployment surface.** Rationale: the vendor's refreshed 2026-08-15 model card introduces a new agentic tool-use capability on the API tier that the enterprise currently does not consume but is likely to enable on at least one integrated system in the next six months (per the MCDA roadmap; the specific plan is not in-scope for this lab but is a known forthcoming item). The enterprise's control library carries LLM01 / LLM07 surfaces on `CTL-2026-0341` but no LLM06 Excessive-Agency control covering tool-set / permission / autonomy for a vendor-delivered agentic surface. Route to `senior-ai-governance-architect` with the vendor's model-card known-limitations attached as the evidence base. Requested action: *library-level review of LLM06 coverage against the vendor's acknowledged agentic known-limitations; if a new control is needed, draft and ship on the master-library change-management workflow; the analyst re-populates the crosswalk column once the control lands*. Target: 2026-12-19 (library review scoping); 2027-01-30 (new control, if any, drafted). The analyst does not draft the control statement (chapter 07 *analyst suggests, architect decides* line).

### Step 8 — Project into the register table (5 min)

Below the entries in `escalation-register.md`, project them into the chapter-9 register-table shape.

```markdown
## Register table

| ID | Class | Source | Filed | Route | Status | Resolution | Impact on row and report |
|---|---|---|---|---|---|---|---|
| ESC-2026-LAB02-01 | 3 | VND-2026-0044 cert body accreditation suspended | 2026-11-14 | procurement; data-protection-officer; senior-ai-governance-architect cc; ai-infra-security cc | open — awaiting vendor statement | — | inheritance decision pause-condition (a); moves to do-not-inherit on adverse resolution |
| ESC-2026-LAB02-02 | 3 | VND-2026-0044 new sub-processor in Jurisdiction Y | 2026-11-14 | procurement; legal; data-protection-officer; ai-infra-security cc; technical owner cc | open — awaiting owner action | — | inheritance decision pause-condition (b); composes with ESC-2026-LAB01-11 |
| ESC-2026-LAB02-03 | 1 | VND-2026-0044 agentic tool-use surface | 2026-11-14 | senior-ai-governance-architect | open — awaiting architect scoping | — | no immediate change to row; drives library work for forthcoming MCDA enable |
```

### Step 9 — Compose the cross-link, the verdict, and the completeness check (5 min)

Open `## Cross-link to the control side (CTL-2026-0352 + lab-01 escalation)` in `vendor-row-refresh.md`. Record that the vendor-side `ESC-2026-LAB02-02` composes with `ESC-2026-LAB01-11` (the control-side escalation filed in the paired lab) — the two entries are separate files-of-record because they route to different artefacts (one to the vendor-management office, one to the control-status report §5) but share the underlying fact set and the same target date. The refreshed `VND-2026-0044` row and the refreshed `CTL-2026-0352` row cite each other; a resolution to either escalation closes the vendor-side column 11 and the control-side column 15 in one pass.

Open `## Re-review verdict`. Four or five sentences:

*Event-triggered re-review ran 2026-11-14 against `VND-2026-0044`. Five Section-C events fired since the 2026-02-10 baseline (certifying-body accreditation suspension; new sub-processor in Jurisdiction Y; model-card refresh with new agentic tool-use capability; vendor bias-audit publication with qualified opinion; model-version rotation). Twelve columns refreshed on the row, the inheritance decision moved from *inherit-with-compensating-controls* to *inherit-with-compensating-controls — with pause-conditions*, and two Class-3 escalations filed to `procurement` + `data-protection-officer` + `legal` plus one Class-1 escalation to `senior-ai-governance-architect` on the agentic-tool-use library gap. The refreshed row supersedes the 2026-02-10 row on issue; the next review is 2027-01-13 (60-day pause-condition follow-up) or on earlier resolution of either pause-condition, with the full annual re-review at 2027-02-10 regardless. The vendor's bias-audit report, while out-of-scope for current enterprise deployment, is recorded on column 14 with criteria origin (ForHumanity) and auditor credentialing (BABL-trained) as distinct fields per chapter 08. No Class-4 governance-council escalation was warranted on this re-review — the pause-conditions are specific and resolvable; the inheritance decision remains the analyst-plus-vendor-management scope.*

Open `## Pre-close completeness check` and walk the row against the following four checks before closing:

1. **Every event in Section C is accounted for in the refresh log, with the re-entry step named for each.** Five events on the pre-review list; each named on a column sub-section and / or on an escalation. Confirm pass.
2. **Columns 17 (residual-risk paragraph), 18 (inheritance decision), and 19 (compensating controls) are populated in that order — not with 18 before 17.** The paragraph comes first (chapter 06 step 6 before step 8); 18 names the pause-conditions explicitly; 19 names at least one `CTL-<year>-<sequence>` per compensating-claim plus the Class-1 escalation for a new control. Confirm pass.
3. **Column 12's certification is recorded as *provisional — body accreditation suspended*, not silently as *valid*.** Chapter 06 *certification-letter theatre* adjacent failure mode; chapter 08 IAF-accreditation discipline. Confirm pass.
4. **Column 14's independent audit is recorded with criteria origin (ForHumanity criteria set + version) and auditor credentialing (BABL-trained) as distinct fields.** Chapter 08 named failure mode *conflating criteria with credential*. Confirm pass.

If any of the four is "no", revise *that artefact* before considering the lab done.

## Expected output

Three Markdown files in `~/aicg-labs/mod-108-lab-02/`:

- `vendor-row-refresh.md` — one refresh log with (a) a pre-review event list from Section C with re-entry steps named; (b) twelve column-by-column refresh sub-sections (columns 9–16 for evidence refresh; 17 for residual-risk draft; 18 for inheritance decision; 19 for compensating controls; 20–22 for cadence, dates, and analyst note) with before / after values; (c) a cross-link block to the paired `CTL-2026-0352` and `ESC-2026-LAB01-11`; (d) a re-review verdict; (e) a pre-close completeness check.
- `vnd-2026-0044-refreshed.md` — the full twenty-two-column refreshed row in the chapter-6 shape, with a supersession-pointer header naming the closed prior row.
- `escalation-register.md` — three full chapter-9 escalation entries (two Class-3 and one Class-1) with per-class template fields, plus the chapter-9 register-table projection beneath.

Total length: roughly 2,500–3,500 words across the three files. A reviewer should be able to read all three in twenty minutes and see every event walked, every column refreshed honestly, the residual-risk paragraph drafted before the inheritance decision, and every escalation routed per the chapter-9 Class-3 (or Class-1) template.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Did column 12 (ISO/IEC 42001 certification) read *provisional — body accreditation suspended*, not silently as *valid*?** Chapter 06's *certification-letter theatre* adjacent failure mode plus chapter 08's IAF-accreditation discipline together drive this; a reviewer who carries forward *valid* because the certificate date still reads 2028-04-01 has conflated the certificate with the IAF-signatory status that underwrites it.
2. **Did the residual-risk paragraph land *before* the inheritance decision?** Chapter 06 names *inheritance decision without residual-risk paragraph* as a specific failure mode; the walk-order matters — step 6 before step 8, always.
3. **Did the inheritance decision name the pause-conditions explicitly, not as "watch-items"?** *Inherit-with-compensating-controls — with pause-conditions* is a legitimate chapter-6 variant; *inherit-with-compensating-controls* without pause-conditions on a vendor whose evidence is provisional is the chapter-6 *missing compensating-controls anchor* failure mode in disguise.
4. **Did column 14 (independent audit) record criteria origin (ForHumanity) and auditor credentialing (BABL-trained) as distinct fields?** Chapter 08 named failure mode. A single field that reads *audit by ForHumanity / BABL* conflates the criteria set with the credential; a downstream reader cannot then tell whether the auditor was trained by one body and audited against the other's criteria, which is in fact exactly what happened here.
5. **Did `ESC-2026-LAB02-02` cross-link to `ESC-2026-LAB01-11` from the paired lab?** The two entries share the fact set but route to different artefacts; a reviewer who files one without cross-linking the other has lost the connective-tissue the chapter-9 register is supposed to carry.
6. **Did the Class-1 library-design fix on the agentic-tool-use surface route to `senior-ai-governance-architect` *without* a drafted control statement?** The lab's agentic-tool-use surface is a library gap — the analyst raises it with the model-card known-limitations attached; the analyst does not draft the LLM06 control statement. Chapter 07's *analyst suggests, architect decides* line is explicit.
7. **Did the refreshed row supersede the 2026-02-10 row with an explicit pointer, rather than overwrite it in place?** Chapter 06 *the row supersedes any earlier vendor row for the same vendor + named-artefact combination*; overwriting in place loses the audit trail.

If any of the seven is "no", revise *that artefact* before considering the lab done.

## Why this is a lab, not an exercise

The module's five exercises each drill *authoring from scratch* — exercise 04 in particular drills authoring fresh vendor rows from the ten-step intake sequence starting at step 1 (enterprise intake row) through step 10 (cadence). None of them asks the analyst to run the *event-triggered* re-review path — which enters at step 3 (public evidence sweep) or step 4 (private evidence request) rather than step 1, runs through twelve column refreshes with before / after walks, and produces a *superseding* row rather than a *new* one. This lab is that path. The failure mode it prevents is the analyst who can author a fresh vendor row from a clean sheet but has never once refreshed an existing row where the certification posture, the sub-processor posture, and the deployment surface all moved between annual cadences, and has never once held the chapter-6 step-6-before-step-8 ordering discipline under pressure from the inheritance-decision question. It also exercises the specific chapter-8 ForHumanity-vs-BABL distinction that only lands when the artefact being read is a bias-audit *by a BABL-trained auditor against ForHumanity criteria* — the exact shape the chapter calls out as a named *criteria-vs-credential conflation* failure mode.
