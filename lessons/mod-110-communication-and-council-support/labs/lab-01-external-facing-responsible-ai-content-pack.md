# Lab 01 — External-Facing Responsible-AI Content Pack from a Fixed Internal Baseline

**Duration:** 2 hours.
**Grounding chapters:** [07](../07-external-facing-responsible-ai-communication.md), [02](../02-translating-technical-evidence-for-five-audiences.md), [06](../06-first-cut-internal-ai-policies-and-standards.md), [09](../09-delegation-boundary-and-escalation-patterns.md).
**Difficulty:** Core — exercises chapter 07's four external artefact families (trust-site content, published model card, regulator response, Article 50 transparency notice) at the depth the analyst is expected to draft. The module's four exercises each drill a *different* authoring act (exercise 01 drills six audience-adapted briefings from a fairness-review note; exercise 02 drills one full council-meeting cycle; exercise 03 drills the acceptable-use-policy first-cut; exercise 04 drills the certifications portfolio plan). None of them asks the analyst to compose a coordinated *external-facing pack* — the specific chapter-07 artefact family that lives under a stricter vocabulary discipline than internal briefings and under a different review-and-approval chain. This lab is that specific authoring act, run against a fixed internal baseline so the analyst can concentrate on the chapter-07 discipline rather than on re-authoring the underlying internal artefacts.

## Objective

Take a *fixed, pre-assembled* internal baseline — an internal model card, a closed incident record, a residual-risk register entry, and a release-assurance eval summary — and produce a coordinated four-artefact external-facing pack that the analyst would hand to `senior-ai-governance-architect`, `legal`, `communications`, and `head-of-ai-governance` for review and ratification per chapter 07's review-and-approval chain. The pack exercises every chapter-07 rule: external claims never outstrip the internal evidence; the *certified ≠ aligned ≠ implementing ≠ compliant* distinction is applied verbatim; framework names carry versions; metrics are cited with their measurement basis and date; limitations the internal card names are preserved; no comparative claims about competitors; no speculation about future capability; Article 50 transparency notices read as compliance artefacts rather than marketing content; and the delivery-chain header on each file names the reviewers and signer / publisher so the file routes rather than sits.

The deliverables are four Markdown files in `~/aicg-labs/mod-110-lab-01/`:

- `01-trust-site-update.md` — the drafted update to the enterprise's responsible-AI trust-site page covering the system and incident reflected in the baseline.
- `02-external-model-card.md` — the external-published model card derived from the internal model card, reconciled so no external claim outstrips the internal evidence and so no limitation named internally is omitted externally.
- `03-regulator-response.md` — the analyst's first-cut draft response to a specific regulator request-for-information quoted in Section D below.
- `04-article-50-transparency-notice.md` — the user-facing Article 50 transparency notice the enterprise will place on the end-user surface for the system.

A reviewer should be able to read all four in forty-five minutes and see every chapter-07 rule applied: (i) the vocabulary discipline (precise framework names with versions, distinguished verbs of adherence, cited metrics with their basis, named limitations); (ii) the no-external-claim-outstrips-the-internal-evidence discipline; (iii) the review-and-approval chain stated explicitly on each file's header; (iv) Article 50 notice as compliance artefact rather than marketing content; (v) the *do not* patterns avoided — no comparative claims about competitors, no forward-looking capability statements, no stop-and-escalate signals silently fixed.

## Prerequisites

- Chapter 07 read; the four artefact families, the review-and-approval chain, the stop-and-escalate red flags, the public-facing vocabulary discipline (*certified* ≠ *aligned* ≠ *implementing* ≠ *compliant*), and Article 50's transparency obligations fresh in memory.
- Chapter 02 read; the translation-not-summarisation rule (traceability + no unsupported claims) applies to external content just as much as to internal briefings.
- Chapter 06 read; the four-phase routing chain (first-cut draft → architect edits → cross-functional consultation → ratification) applies to external artefacts that the analyst drafts (particularly the trust-site update, where the architect owns the published shape).
- Chapter 09 read; the delegation-boundary rows for external communication — the analyst drafts and factual-reviews; the analyst does *not* sign, publish, speak of record, or respond directly to media. The lab header on each file carries the routing chain explicitly.
- A Markdown editor; no Python, GRC, or vendor tooling required. The baseline in Section D below is a Markdown-only stand-in for what would live in the GRC platform and the enterprise's model-card repository in production.
- Exercise 01 completed, or at minimum skimmed — the translation discipline the analyst used across the five internal audiences carries over to the external audience; the external audience is just *one more* audience under a tighter vocabulary regime.

## The fixed input — a pre-assembled internal baseline

Use *exactly* this baseline. Do not substitute identifiers, dates, versions, or evidence identifiers, and do not re-derive the underlying facts — the fixed state is the point of the lab. Treat the whole block as `pedagogic example — identifiers, numbers, and dates illustrative`.

### A. The enterprise profile

- **Enterprise.** A UK-headquartered mid-sized SaaS provider operating in the UK (primary) and the EU (secondary), with limited US consumer-facing exposure. Legal entity in Ireland for EU-user-facing products. No real-time law-enforcement use cases.
- **Trust-site baseline.** The enterprise maintains a public *Responsible AI* page at `[enterprise-domain]/responsible-ai` with a short *Our AI principles* statement (last updated 2025-10-14), a *How we govern AI* summary (last updated 2026-02-20), a *Published model cards* index (last updated 2026-04-30), and a *Contact* footer with the AI-governance mailbox address. The page does *not* currently list any specific models. Before this lab, the page says the enterprise *"is implementing ISO/IEC 42001:2023"* — the enterprise is not certified.
- **AI governance posture at start of this lab.** The enterprise is in the implementation phase of its ISO/IEC 42001 AIMS; a Stage 1 audit is scheduled for 2027-Q2. The enterprise runs a monthly AI governance council. The enterprise aligns its AI risk management with ISO/IEC 23894:2023 and NIST AI Risk Management Framework 1.0.

### B. The internal model card (the source external content must not outstrip)

```
INTERNAL-MODEL-CARD-INV-2026-0137 — Writing-Assistant-EU — v3 (2026-10-14)
System:               Writing-Assistant-EU (customer-facing drafting assistant for
                      enterprise SaaS end users)
Inventory row:        INV-2026-0137 (High-tier under the enterprise's tiering
                      methodology; not Annex III under the EU AI Act)
Provider / deployer:  Enterprise is the *deployer* of a third-party foundation
                      model (VND-2026-0019); enterprise is the *provider* of the
                      application wrapper
Jurisdictions:        EU (primary end-user base ~65 % of monthly active users);
                      UK (~30 %); rest-of-world (~5 %)
Deployment surface:   In-product drafting panel; "AI-assisted drafting" label
                      visible on first use; opt-out available per user

Intended use:         Suggest draft text continuations and rephrasing for
                      customer-authored internal documents (reports, meeting
                      notes, internal memos). Not intended for customer-external
                      communication, legal advice, medical advice, or financial
                      advice.

Unintended / out-of-  Legal, medical, or financial drafting; customer-external
scope use:            communication without human review; content creation for
                      regulated-industry filings; use on content categorised as
                      personal data of a special category (Article 9 GDPR)
                      without the user's own lawful-basis assessment.

Training & provenance: Underlying model trained by VND-2026-0019; fine-tuning
                      corpus is enterprise-curated anonymised writing samples
                      (10k documents, provenance documented in corpus register
                      CORP-2026-0004). Retrieval-augmentation disabled.

Release-assurance     EVAL-2026-0441-r3 (release-assurance; sample size 8,400
eval evidence (cited  prompts across 12 task-shapes); baseline:
by ID, not reproduced   - groundedness 0.89 against system-card ≥ 0.85
verbatim here):         - refusal-rate on prohibited-content prompts 0.97
                        - hallucination rate on factual-claim prompts 0.6 %
                        - demographic-parity difference on tone-coaching
                          outputs 0.04 (within the enterprise's ≤ 0.05
                          fairness threshold)
                        - eval date 2026-09-12

Limitations (named    - The model is English-first; non-English output quality
by the internal card):  is measurably lower than English output quality on the
                        same metric suite (quantified in EVAL-2026-0441-r3
                        annex B; groundedness 0.78 on non-English prompts).
                      - The model may produce plausible-sounding but
                        unverified factual claims on any topic requiring
                        citation; the in-product UI flags AI-generated text
                        and advises user review before copying or sharing.
                      - The model is not evaluated for use on personal data of
                        a special category (Article 9 GDPR); users enter such
                        data at their own lawful-basis judgement.

Incident history:     INC-2026-0184 (2026-08-02 to 2026-09-05; closed-with-
                      open-follow-through) — a non-English-prompt-shape
                      increase in hallucinated-citation-style output surfaced
                      through customer-support channel. Guardrail deployed
                      2026-08-11 (citation-must-be-retrievable); customer
                      notification 2026-08-18; FRIA re-opened and signed v2
                      2026-08-28. Residual re-scored high 2026-08-04 → medium
                      2026-09-30 after two clean monitoring periods.

Residual risk:        RISK-2026-0131 residual medium (currently accepted by
                      the system risk-owner; the acceptance was endorsed at
                      the AI governance council 2026-09-21 — minute reference
                      DEC-2026-0088).

FRIA / DPIA:          FRIA-2026-0054 v2 (signed 2026-08-28); DPIA-2026-0019 v3
                      (signed 2026-04-30; not re-opened by INC-2026-0184 —
                      chapter-04 Q1/Q2/Q4 all evaluated no, Q3 triggered FRIA
                      only, DPO consulted).

Governance controls:  CTL-2026-0052 (release-assurance eval before each model
                      update; passing per most-recent quarterly re-test);
                      CTL-2026-0066 (citation-must-be-retrievable guardrail;
                      operating; EV-2026-1144 most-recent evidence);
                      CTL-2026-0081 (user-review-prompt on first-use;
                      operating; EV-2026-1150).

External model card   Not currently published externally; the enterprise has
publication status:   elected to publish one from this lab onward, per
                      head-of-ai-governance direction at council 2026-10-19.
```

### C. The incident the trust-site update must reference

The incident `INC-2026-0184` (named in the model card above) is closed; its evidence pack is complete. The council endorsed, at the 2026-10-19 meeting, that the enterprise would reference the incident on the trust site in a factual, limitation-naming shape as part of the enterprise's responsible-AI transparency posture. The analyst's job in this lab is to draft that trust-site update.

The council direction, minuted at DEC-2026-0098 (2026-10-19), reads: *"The council directs management to update the Responsible AI page to (i) list the Writing-Assistant-EU system by category and name, (ii) reference the published model card for the system, (iii) factually describe the enterprise's response to the August 2026 non-English-prompt hallucination surface, (iv) reflect the enterprise's current ISO/IEC 42001 implementation status (no claim of certification), and (v) route through the trust-site review-and-approval chain per chapter 07 before publication."*

### D. The regulator request-for-information

The enterprise's Irish Data Protection Commission (DPC) contact has, on 2026-11-02, issued a non-binding request-for-information under their informal supervisory practice, with a response due 2026-11-30 (28 calendar days). The RFI, reproduced in full:

> *The Commission is aware, from publicly-available sources, that \[Enterprise\] operates a drafting-assistance AI system available to EU users. The Commission requests a factual description of (a) the system's lawful basis under Article 6 GDPR, (b) whether any solely-automated decision-making under Article 22 GDPR occurs via this system, (c) the enterprise's handling of the user's right to object and the user's right to rectification where the system's output concerns the user, (d) the data-protection impact assessment position on the system (DPIA identifier, version, and signature date), and (e) any incidents involving personal data of EU users since the system became available that the enterprise has not already notified under Article 33 GDPR.*
>
> *This request is informal and non-binding; no supervisory finding is implied. A response by \[2026-11-30\] will be treated as timely.*

The RFI is *not* an EU AI Act Article 73 serious-incident notification; it is a GDPR supervisory inquiry and routes through the enterprise's standard data-protection response chain (`legal`, `data-protection-officer`, `head-of-ai-governance` approver, accountable executive signer).

### E. The user-facing surface the Article 50 notice must cover

`Writing-Assistant-EU` sits inside the enterprise's SaaS product. On first use, the user sees a drafting-panel modal. The Article 50 transparency obligation that applies is the *interaction-is-with-an-AI-system* disclosure under Article 50(1) (for providers of AI systems directly interacting with natural persons), and — because the model's output is synthetic text — the labelling obligation under Article 50(4) (for deployers of generative-AI systems producing synthetic content). The enterprise is the *deployer* of the underlying foundation model (per the model card) and the *provider* of the application wrapper. The analyst's Article 50 draft covers both the interaction-is-with-an-AI disclosure (surfaced in the drafting-panel modal) and the synthetic-content labelling (surfaced on AI-generated text segments in the drafting UI). <!-- needs-research: Article 50 obligations and their sub-provision mapping to provider vs deployer are being clarified in Commission guidance and secondary legislation; confirm current state before drafting production notices. -->

## Steps

### Step 1 — Scaffold the four files (10 min)

Create the working folder and files.

```bash
mkdir -p ~/aicg-labs/mod-110-lab-01
cd ~/aicg-labs/mod-110-lab-01
touch 01-trust-site-update.md 02-external-model-card.md 03-regulator-response.md 04-article-50-transparency-notice.md
```

For each file, lay in the common review-chain header at the top. The header makes the delegation boundary load-bearing on the file itself; chapter 09's routing-chain discipline means no external artefact ships without the header populated.

```markdown
# [Artefact name]

Artefact:           [trust-site update / external model card / regulator response / Article 50 notice]
Draft version:      0.1 (first-cut, analyst-authored)
Author:             [analyst name] — 2026-11-08
Underlying pin:     INTERNAL-MODEL-CARD-INV-2026-0137 v3 (2026-10-14);
                    INC-2026-0184 (closed-with-open-follow-through);
                    RISK-2026-0131 residual medium (DEC-2026-0088, 2026-09-21);
                    FRIA-2026-0054 v2 (2026-08-28); DPIA-2026-0019 v3 (2026-04-30);
                    EVAL-2026-0441-r3 (2026-09-12).
Reviewers required: [per artefact — populate per chapter 07's review-and-approval chain]
Signer / publisher: [per artefact — populate per chapter 07's review-and-approval chain]
Not for public      Until signer / publisher has approved and the publication
circulation:        route is open per chapter 07.
```

The four files share this header shape; the *reviewers required* and *signer / publisher* fields differ per artefact.

### Step 2 — Compose `01-trust-site-update.md` (30 min)

The trust-site update's review-and-approval chain, per chapter 07, is: analyst drafts and factual-reviews → `senior-ai-governance-architect`, `legal`, `communications`, `head-of-ai-governance` review → `communications` publishes. Populate the header fields accordingly. Then draft the update's content.

The update must cover the five items the council directed at `DEC-2026-0098` and no more. Draft it as a Markdown-rendered replacement for the current *How we govern AI* summary block plus an addition to the *Published model cards* index. Suggested shape:

```markdown
## How we govern AI

[Enterprise] operates an AI governance programme aligned with ISO/IEC 42001:2023
(AI management system), ISO/IEC 38507:2022 (governance implications of AI use),
ISO/IEC 23894:2023 (AI risk management), and the NIST AI Risk Management
Framework 1.0. The enterprise is currently implementing its ISO/IEC 42001 AI
management system; a Stage 1 audit by an accredited certification body is
scheduled for 2027-Q2. The enterprise is not currently certified against
ISO/IEC 42001.

[Enterprise] runs a monthly AI governance council chaired by the enterprise's
head of AI governance, with legal, privacy (including the data protection
officer), security, business-line, and responsible-AI representatives. The
council reviews new AI systems entering the enterprise's inventory, residual-
risk acceptances above the enterprise's council-attention threshold, impact-
assessment sign-offs, incident summaries, and the enterprise's regulatory
posture.

## Our published model cards

[Enterprise] publishes model cards for its customer-facing AI systems where the
enterprise has elected to do so under its public-transparency posture. The
model cards published below are derived from the enterprise's internal model
cards and reconciled against the enterprise's internal evaluation evidence.

### Writing-Assistant-EU (customer-facing drafting assistant)

Writing-Assistant-EU is a drafting-assistance system available to [Enterprise]
customers in the European Union, the United Kingdom, and selected other
regions. It suggests draft text continuations and rephrasing for customer-
authored internal documents. Full description: [link to
02-external-model-card.md].

In August 2026, [Enterprise] identified, through its customer-support channel,
an increase in the rate of plausible-sounding but unverified factual claims
produced by the system on prompts in languages other than English. [Enterprise]
investigated under its AI-incident response process, deployed a mitigation on
2026-08-11 that requires citations produced by the system to be traceable to
a retrieved source, notified the affected customer segment on 2026-08-18, and
re-opened its fundamental-rights impact assessment on the system (signed
2026-08-28). [Enterprise]'s continuous monitoring shows the system's
performance on non-English prompts returned within the enterprise's internal
threshold in September 2026; the system's non-English output remains lower
in quality than its English output, and the published model card names this
limitation.

Contact for AI-governance questions: [AI-governance mailbox address].
```

**Discipline checks before you stop writing this file.**

- *Precise framework names with versions.* ISO/IEC 42001:2023, not *ISO 42001*. ISO/IEC 38507:2022, not *ISO 38507*. NIST AI Risk Management Framework 1.0, not *the NIST framework*. On first mention of the EU AI Act, the full name would appear — not required in *this* update because the EU AI Act isn't directly referenced, but note the pattern.
- *Verbs of adherence.* *Implementing* for the ISO/IEC 42001 AIMS; *aligned with* for the three standards and the framework; *not currently certified*. Do not use *compliant* anywhere; do not use *certified* without an accredited certificate.
- *No comparative claims.* Nothing of the shape *"better than [competitor]"*; nothing of the shape *"the industry standard is …"*.
- *No forward-looking capability statements.* The Stage-1-audit-in-2027-Q2 line is a scheduled event, not a capability claim; acceptable. No *"will soon be certified"* — strike if it appears.
- *Named limitation.* The non-English quality limitation from the internal model card appears in the trust-site paragraph on `Writing-Assistant-EU`; the external card expands on it.
- *No silent inflation of the incident.* The trust-site description tracks the incident record and the FRIA re-open; it does not claim more than the record supports and does not rename the incident.
- *Cross-reference.* The *published model cards* index links to `02-external-model-card.md`; the trust-site page does not reproduce the model-card content in the index.

### Step 3 — Compose `02-external-model-card.md` (30 min)

The external model card's review-and-approval chain, per chapter 07, is: analyst drafts and factual-reviews → internal model-card owner (per `mod-105`), `senior-ai-governance-architect`, `legal` (because the deployment is customer-facing and the FRIA has been re-opened in the past 12 months), `communications` (for tone) review → `senior-ai-governance-architect` publishes (or the enterprise's model-card publication authority). Populate the header fields.

The external card must be derivable from the internal model card above *without outstripping it*. The content shape below is the analyst's reconciliation of the internal card for an external audience — the internal-only fields (`INV-` row, `CTL-` identifiers, `EV-` evidence identifiers, internal team names, incident-register identifiers) are translated into external-appropriate language (the system's category, published metric summary, external-appropriate scope-of-use description).

```markdown
# Writing-Assistant-EU — Model Card

Published by: [Enterprise]
Published:    2026-11-08 (version 1.0)
Supersedes:   not applicable (first external publication)
Next review:  within 12 months of publication or on material change, whichever
              is sooner

## About this system

Writing-Assistant-EU is a drafting-assistance AI system that suggests draft text
continuations and rephrasing for text the user is authoring. It is available
to [Enterprise] customers inside [Enterprise]'s SaaS product in a drafting-
panel surface. The system is intended for use on the customer's own internal
documents — reports, meeting notes, internal memos, and similar.

## What this system is not for

Writing-Assistant-EU is not evaluated for and is not intended for:

- Producing legal, medical, or financial advice.
- Producing content that will reach customers, regulators, or a public audience
  without human review.
- Producing content for regulated-industry filings or similar high-stakes
  external communication.
- Processing personal data of a special category (Article 9 GDPR) — users
  entering such data into the system do so at their own lawful-basis
  judgement.

## How the system works

The system is built on a third-party foundation model, fine-tuned by
[Enterprise] on an anonymised corpus of [Enterprise]-curated writing samples.
The system does not currently use retrieval-augmentation; outputs are
produced from the user's prompt and the fine-tuned model's parameters alone.

## Evaluation evidence

The system is evaluated against [Enterprise]'s release-assurance evaluation
suite before each model update and quarterly on an ongoing basis. The most-
recent release-assurance evaluation, conducted 2026-09-12 on a sample of
8,400 prompts across 12 task shapes, recorded:

- Groundedness: 0.89 (against the published target ≥ 0.85).
- Refusal rate on prompts the system is expected to refuse: 0.97.
- Hallucination rate on prompts requiring a factual claim: 0.6 %.
- Demographic-parity difference on tone-coaching outputs across segment
  pairings evaluated: 0.04 (within [Enterprise]'s internal fairness
  threshold ≤ 0.05).

## Named limitations

- **Language variation.** The system's English output quality is measurably
  higher than its non-English output quality on the same evaluation suite.
  As of the 2026-09-12 evaluation, non-English groundedness was 0.78
  compared to 0.89 overall.
- **Factual claims requiring citation.** The system may produce plausible-
  sounding but unverified factual claims on any topic requiring citation.
  The in-product user interface flags system-generated text and advises
  user review before the user copies or shares that text.
- **Scope of evaluation.** The system is not evaluated for use on personal
  data of a special category (Article 9 GDPR). Users entering such data
  make their own lawful-basis judgement at the point of use.

## Incident history visible to users

In August 2026, [Enterprise] identified, through its customer-support
channel, an increase in the rate of plausible-sounding but unverified
factual claims produced by the system on prompts in languages other than
English. [Enterprise] investigated, deployed a mitigation on 2026-08-11
(a requirement that citations produced by the system be traceable to a
retrieved source), notified the affected customer segment on 2026-08-18,
and re-opened the system's fundamental-rights impact assessment (signed
2026-08-28). Continuous monitoring shows the system's non-English
performance returned within [Enterprise]'s internal threshold during
September 2026. The named language-variation limitation above describes
the current state.

## Oversight

Writing-Assistant-EU is governed by [Enterprise]'s AI governance programme,
which operates an AI management system [Enterprise] is implementing against
ISO/IEC 42001:2023 (Stage 1 audit scheduled for 2027-Q2 against an
accredited certification body; the enterprise is not currently certified).
The programme is aligned with ISO/IEC 38507:2022, ISO/IEC 23894:2023, and
NIST AI Risk Management Framework 1.0.

## Contact

AI-governance questions, including questions about this model card or
requests to exercise rights under applicable data protection law: [AI-
governance mailbox address]. For data-protection enquiries specifically,
[Enterprise]'s data protection officer: [DPO contact].

Document references (internal-only; not published): INV-2026-0137;
INTERNAL-MODEL-CARD-INV-2026-0137 v3 (2026-10-14); EVAL-2026-0441-r3
(2026-09-12); FRIA-2026-0054 v2 (2026-08-28); DPIA-2026-0019 v3
(2026-04-30); RISK-2026-0131; DEC-2026-0088 (2026-09-21); INC-2026-0184.
```

**Reconciliation checks before you stop writing this file.**

- *No external claim outstrips the internal evidence.* Every number on the external card appears in the internal card's EVAL section, at the same value, with the same date.
- *No limitation the internal card names is omitted externally.* The English-first quality gap, the factual-claim-citation limitation, and the Article-9-not-evaluated limitation all appear.
- *Internal-only identifiers kept internal.* The *document references* block names them for the analyst's own reconciliation record and for the internal reviewer; those identifiers are *not* part of the published card's user-visible content (treat the *document references* block as a draft-review annex to be removed at publication, or flagged *internal reviewer only*).
- *Vocabulary discipline.* Same as the trust-site update — *implementing* / *aligned* / *not currently certified* throughout.
- *Mitchell-et-al. and Hugging Face model-card conventions.* The shape above is consistent with them; the analyst does not need to name them in the body of the published card but may cite them in the review-notes annex.

### Step 4 — Compose `03-regulator-response.md` (25 min)

The regulator response's review-and-approval chain, per chapter 07, is: analyst drafts and fact-checks → `legal`, `head-of-ai-governance`, subject-matter contributors (in this case `data-protection-officer`) review → accountable executive named for the DPC and the Irish entity signs and submits. Populate the header fields.

The regulator response is a first-cut, for internal review. The analyst's content covers (a) through (e) of the RFI, each factually and each cited to the underlying artefact by ID. The analyst does *not* take the lawful-basis position (that is the DPO's call); the analyst *names* the position the DPIA records. The analyst does *not* interpret Article 22 for the DPC's benefit; the analyst *describes* whether and how the system engages Article 22.

```markdown
# [Enterprise] — Response to Irish Data Protection Commission
# Request for Information of 2026-11-02

Prepared by:   [Enterprise] AI Governance (analyst draft; routing for legal,
               DPO, and head-of-AI-governance review)
Draft date:    2026-11-08
Due date:      2026-11-30 (28 calendar days from the Commission's request)
Signer:        [Accountable executive — Irish entity, e.g., General Counsel or
               named C-level, per Enterprise's regulator-communication protocol]

[Enterprise] appreciates the Commission's informal request of 2026-11-02 and
provides the following factual response in respect of its drafting-assistance
AI system (Writing-Assistant-EU). The response refers to the system's internal
documentation on file at [Enterprise]; copies are available to the Commission
on request.

## (a) Lawful basis under Article 6 GDPR

Writing-Assistant-EU operates on the user's own authored text within the
[Enterprise] SaaS product. [Enterprise]'s data protection impact assessment
on file (DPIA-2026-0019 v3, signed 2026-04-30) records the lawful basis for
the processing involved in operating the system and the enterprise's
balancing assessment. The lawful basis for the system as recorded in that
assessment is [LEGAL / DPO TO CONFIRM BEFORE SUBMISSION — the analyst draft
names the DPIA by ID rather than taking the Article 6 position in the draft
itself].

## (b) Article 22 GDPR — solely automated decision-making

Writing-Assistant-EU produces draft text for the user; the system's output
is a suggestion that the user accepts, edits, or rejects before any further
use the user makes of it. The system does not take decisions concerning the
user or any data subject; the system's output is not applied automatically
to any downstream process in [Enterprise]'s SaaS product. Accordingly,
Article 22 GDPR does not attach to the operation of this system in its
current deployment. This position is recorded in DPIA-2026-0019 v3.

## (c) Right to object and right to rectification

Where a user's interaction with Writing-Assistant-EU involves personal data
of the user, [Enterprise]'s rights-of-data-subjects workflow applies as it
does for the enterprise's other processing of user data. Rights can be
exercised via [Enterprise]'s standard data-subjects portal at [URL] or
by contacting [Enterprise]'s data protection officer at [DPO contact].

Where a specific right-of-rectification request concerns the content of
the system's output (i.e., the user asks for correction of text the
system produced about them), the user may request rectification by the
same route; [Enterprise]'s process is to consider such requests and, where
they engage personal-data accuracy under Article 5(1)(d) GDPR, to action
them in accordance with the DPO's review.

## (d) Data protection impact assessment on the system

- Identifier: DPIA-2026-0019.
- Current version: v3.
- Current version signature date: 2026-04-30.
- Re-opened following the August 2026 incident described in (e)? No —
  the incident did not trigger a DPIA re-open on [Enterprise]'s chapter-04
  walk (Q1 falsified claim: no; Q2 un-enumerated population: no; Q3
  un-considered harm class: yes, but the chapter-04 walk routed that
  re-open to the FRIA, not the DPIA; Q4 inoperative measure: no). The
  DPO was consulted on this determination and the consultation is
  recorded on the incident record.
- Related fundamental-rights impact assessment: FRIA-2026-0054, v2
  signed 2026-08-28, specifically re-opened following the August 2026
  incident.

## (e) Incidents involving EU users' personal data since the system became available

[Enterprise] has one recorded AI-incident on the system since the system
became available to EU users: INC-2026-0184 (opened 2026-08-02; closed
with open follow-through 2026-09-05). The incident concerned a rate of
plausible-sounding but unverified factual claims produced by the system
on prompts in languages other than English. [Enterprise] assessed the
incident against Article 33 GDPR notification criteria and did not
notify under Article 33 because the incident did not constitute a
personal-data breach within the meaning of Article 4(12) GDPR
(no confidentiality, integrity, or availability compromise of personal
data was identified). [LEGAL AND DPO TO CONFIRM BEFORE SUBMISSION.]

[Enterprise]'s AI-incident response included, in summary, deployment of
a citation-must-be-retrievable guardrail on 2026-08-11, customer
notification on 2026-08-18, and the FRIA-2026-0054 v2 sign-off on
2026-08-28. Continuous monitoring indicates the issue has been
addressed within [Enterprise]'s internal performance thresholds.

## Contact

Named point-of-contact for this response: [accountable executive and
signer] via [Enterprise]'s regulator-communication channel. All further
substantive communication on this matter should be addressed to the
signer; [Enterprise]'s AI governance analyst is not the regulator contact
of record for this matter (chapter 09 boundary).

## Document references (internal-only; not part of the response submitted)

- Internal model card: INTERNAL-MODEL-CARD-INV-2026-0137 v3 (2026-10-14)
- Inventory row: INV-2026-0137
- Incident record: INC-2026-0184 (closed-with-open-follow-through)
- DPIA: DPIA-2026-0019 v3 (2026-04-30)
- FRIA: FRIA-2026-0054 v2 (2026-08-28)
- Residual-risk register entry: RISK-2026-0131 (medium; endorsed at
  council 2026-09-21, DEC-2026-0088)
- Release-assurance evaluation: EVAL-2026-0441-r3 (2026-09-12)
```

**Discipline checks before you stop writing this file.**

- *Analyst does not take the legal position.* Section (a) names the DPIA by ID rather than stating the Article-6 basis; sections (b) and (e) describe the position the internal records support and flag *legal / DPO to confirm before submission*; the analyst's first-cut makes the DPO's / legal's final sign-off path clear.
- *Analyst does not sign or submit.* The header names the accountable executive as signer; the body closes with the named point-of-contact being that signer, not the analyst.
- *Deadline discipline.* The due date (2026-11-30) is in the header and visible to every reviewer.
- *Every factual claim traces to an artefact ID.* DPIA, FRIA, incident record, eval-evidence, council decision — all cited.
- *The response does not offer substantive communication beyond what was asked.* The analyst does not add commentary on the system's broader safety posture, does not respond to questions the Commission did not ask, and does not open a side-channel conversation.

### Step 5 — Compose `04-article-50-transparency-notice.md` (15 min)

The Article 50 notice's review-and-approval chain, per chapter 07 and chapter 06's routing-chain overlay: analyst drafts → `legal` (for article interpretation), `data-protection-officer` (for privacy-adjacent framing), `senior-ai-governance-architect` (for consistency with the enterprise's other Article 50 notices if any exist), `head-of-ai-governance` review → `communications` (for placement) publishes. Populate the header fields.

The notice is a *compliance artefact*, not marketing content. It is short, factual, in the language of the affected individual's jurisdiction (English and — for a notice surfaced to EU users — translated into the relevant member-state languages as the enterprise's privacy-notice practice already does; the analyst's first-cut is the English source text), and readily accessible on the user-facing surface.

The notice covers two Article 50 obligations:

- **Interaction-is-with-an-AI-system disclosure (Article 50(1))** — surfaced in the drafting-panel modal on first use.
- **Synthetic-content labelling (Article 50(4))** — surfaced on AI-generated text segments in the drafting UI.

A worked draft:

```markdown
# Article 50 Transparency Notice — Writing-Assistant-EU

Notice version: 1.0 (2026-11-08)
Surfaces covered: (1) drafting-panel first-use modal (interaction disclosure);
                  (2) in-UI label on system-generated text segments (synthetic
                  content labelling)
Jurisdictions:    EU (notice issued in English as source; translations to
                  member-state languages per [Enterprise]'s standard privacy-
                  notice translation practice, routed to communications);
                  UK (notice issued in English);
                  rest-of-world (notice issued in English).
Owner:            [Enterprise] AI Governance (analyst draft; routing for
                  legal, DPO, senior-architect, head-of-AI-governance review).

## (1) Interaction-with-an-AI-system disclosure (drafting-panel first-use modal)

Writing-Assistant-EU is an artificial-intelligence system. The drafting
suggestions you receive from it are produced by an AI model. You can continue
using the drafting assistant, stop using it at any time, or opt out of AI-
assisted drafting in your account settings.

If you would like more information about this system, including the system's
intended uses, limitations, and the oversight [Enterprise] applies to it, our
published model card is available at [link to published model card].

## (2) Synthetic-content labelling (in-UI label on AI-generated text segments)

Text produced by Writing-Assistant-EU is marked as AI-generated in the
drafting panel until you edit it. Please review AI-generated text before
copying, saving, or sharing it outside the drafting panel.

## Contact

Questions about this notice or about Writing-Assistant-EU: [AI-governance
mailbox address]. Data-protection-specific enquiries: [data protection
officer contact].
```

**Discipline checks before you stop writing this file.**

- *Compliance artefact, not marketing content.* No *"the most advanced …"*, no *"state-of-the-art"*, no competitive framing. The notice says what the system is and how to know more.
- *Short and factual.* The user reads it once and moves on.
- *Jurisdictional language.* The notice is the English source text; the header names the translation path for EU member-state languages via the enterprise's existing privacy-notice workflow, so the Article-50 notice inherits that workflow rather than creating a parallel one.
- *Covered the two Article-50 obligations applicable to this deployment.* Interaction disclosure and synthetic-content labelling. Emotion-recognition and biometric-categorisation notices do not apply (the system does neither).
- *The user's route to further information.* The published model card and the AI-governance / DPO contacts are named.

### Step 6 — Cross-file reconciliation walk (10 min)

Open all four files side by side. Walk the following cross-file checks:

- **Every number appears identically across files that cite it.** The 0.89 groundedness, the 0.78 non-English groundedness, the 0.97 refusal rate, the 0.6 % hallucination rate, the 0.04 demographic-parity difference, and the dates (2026-08-11 guardrail deployment; 2026-08-18 customer notification; 2026-08-28 FRIA sign-off) all appear, where cited, at the same value in every file.
- **Every framework name carries the same version in every file.** ISO/IEC 42001:2023; ISO/IEC 38507:2022; ISO/IEC 23894:2023; NIST AI Risk Management Framework 1.0.
- **Every verb of adherence is used identically.** *Implementing* the ISO/IEC 42001 AIMS; *aligned with* the standards and the framework; *not currently certified*.
- **No file over-claims relative to the internal model card.** Scan the external model card first; then scan the trust-site update; then the regulator response and the Article 50 notice. Any claim present in an external file that is not supported by the internal baseline is a reconciliation error — fix it in the external file, not by stretching the internal baseline.
- **No file omits a limitation the internal card names.** The non-English quality gap appears in the external model card and in the trust-site update; the factual-claim-citation limitation and the Article-9-not-evaluated limitation appear in the external model card. None is quietly dropped.
- **Every file's header carries the review-and-approval chain and the signer / publisher.** No external file ships from the analyst's own account; chapter 07's chain is visible on each file.

Add a short `## Cross-file reconciliation self-check` block at the bottom of `01-trust-site-update.md` noting that the four files have been reconciled and listing the checks above as completed. The block is the analyst's discipline; it does not ship with the trust-site update at publication.

### Step 7 — Stop-and-escalate self-check (5 min)

Chapter 07 names five *stop-and-escalate* red flags. Walk each one against the pack as composed:

1. **A material mis-statement in an already-published external artefact.** None here — the trust-site update is a first-cut draft, not a mis-statement correction. If drafting had surfaced a prior-published trust-site claim that was factually wrong, the analyst would pause and route to `legal` and `head-of-ai-governance` before incorporating the correction.
2. **A regulator inquiry without a legal review path.** The regulator response in file 3 has the review chain populated in its header and the body is flagged *LEGAL AND DPO TO CONFIRM BEFORE SUBMISSION* on the two substantive legal determinations (Article 6 lawful basis; Article 33 personal-data-breach assessment). The analyst does not submit before those confirmations.
3. **A press or media inquiry directed to the analyst.** Not applicable to this lab; if it arose, the analyst would route to `communications` without responding substantively.
4. **A whistleblower or worker report received externally.** Not applicable to this lab; if it arose, the analyst would route to the enterprise's whistleblower channel.
5. **Any request to publish before the review chain is complete.** The *Not for public circulation* line in the header on each file is the standing answer. If a well-meaning contributor asks *"can we get this up today?"*, the answer is no (chapter 09 class 2 — the analyst declines; the chair or ratifier backs the decline if needed).

Note the walk at the bottom of `01-trust-site-update.md` under a `## Stop-and-escalate self-check` block. The block is the analyst's own discipline and does not ship.

## Expected output

Four Markdown files in `~/aicg-labs/mod-110-lab-01/`:

- `01-trust-site-update.md` — a trust-site update covering the five items the council directed at `DEC-2026-0098`, with the chapter-07 vocabulary discipline applied end-to-end and the review-and-approval chain populated in the header. Length roughly 400–600 words plus the two self-check blocks.
- `02-external-model-card.md` — a Mitchell-et-al.-shaped external model card derived from the internal model card without over-claiming and without dropping limitations, with the review-and-approval chain populated in the header. Length roughly 700–900 words plus an internal-only *document references* annex clearly marked *not for publication*.
- `03-regulator-response.md` — a first-cut regulator response answering (a) through (e) of the DPC RFI with every factual claim traced to an artefact ID, with the Article-6 and Article-33 determinations flagged *legal and DPO to confirm before submission*, and with the accountable executive named as signer. Length roughly 600–900 words.
- `04-article-50-transparency-notice.md` — a user-facing Article 50 notice covering the interaction-disclosure and synthetic-content-labelling obligations in short, factual, compliance-artefact language, with the review-and-approval chain populated in the header. Length roughly 200–300 words.

Total across the four files: roughly 2,000–3,000 words (plus the two self-check blocks on file 1). A reviewer should be able to read all four in forty-five minutes and see every chapter-07 rule applied: the vocabulary discipline (precise framework names with versions, distinguished verbs of adherence, cited metrics with their basis, named limitations); the no-external-claim-outstrips-the-internal-evidence discipline; the review-and-approval chain on every file's header; Article 50 notice as compliance artefact; the stop-and-escalate self-check completed; the regulator response flagging the two legal determinations rather than taking them; the analyst named as draft author and *not* as signer or publisher on any file.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Does every number in the external pack appear in the internal baseline at the same value?** Scan file 2 first; then files 1 and 3. A number in an external file not traceable to the internal baseline is a chapter-07 *no-external-claim-outstrips-the-internal-evidence* failure.
2. **Does the external pack omit any limitation the internal model card names?** The English-first quality gap, the factual-claim-citation limitation, and the Article-9-not-evaluated limitation. Each should appear at least in the external model card; the English-first gap should also appear on the trust-site update's `Writing-Assistant-EU` paragraph.
3. **Is every framework named with its version, every time?** *ISO/IEC 42001:2023* / *ISO/IEC 38507:2022* / *ISO/IEC 23894:2023* / *NIST AI Risk Management Framework 1.0*. *ISO 42001* on its own is an undisciplined usage; *ISO/IEC 42001* without the year is still off-side.
4. **Is every verb of adherence used precisely?** *Implementing* for the AIMS; *aligned with* for the standards and the framework; *not currently certified*. *Compliant with* should not appear anywhere outside a direct quotation of a statute the regulator response is addressing.
5. **Does the regulator response avoid taking the DPO's or legal's substantive position?** Section (a) names the DPIA by ID rather than stating the Article-6 basis; sections (b) and (e) describe the position the internal records support and flag *legal and DPO to confirm before submission*. If the analyst's draft takes the Article-22 position or the Article-33 position on legal's behalf, revise.
6. **Does the Article 50 notice read as a compliance artefact rather than marketing content?** Short, factual, no superlatives, no competitive framing. If the notice reads like a product-launch blurb, revise.
7. **Does every file's header name the signer / publisher as someone other than the analyst?** `Communications` publishes the trust-site update; `senior-ai-governance-architect` publishes the external model card; the accountable executive signs the regulator response; `communications` places the Article 50 notice. If any file's header names the analyst as signer or publisher, revise.
8. **Does the trust-site update stay inside the council direction at `DEC-2026-0098`?** The five items the council named are covered; nothing beyond those items is added. If the analyst's draft extends into content the council did not direct (e.g., a new statement on the enterprise's AI principles), revise.
9. **Does the pack's language anywhere make a comparative claim about competitors, or a forward-looking capability statement?** *"Better than"* / *"the industry standard"* / *"will soon"* — each is a chapter-07 failure mode. Strike.
10. **Does the pack contain a stop-and-escalate signal the analyst silently handled instead of escalating?** The stop-and-escalate self-check block on file 1 names the five signals. If any applies and the analyst handled it on-desk rather than escalating, revise (and escalate).

If any of the ten is *no*, revise *that artefact* before considering the lab done.

## Why this is a lab, not an exercise

The module's four exercises each drill a *different* internal-facing authoring act — exercise 01 drills six audience-adapted internal briefings on a fairness finding; exercise 02 drills one council-cycle pack (pre-read, minutes, action-item register); exercise 03 drills the AUP first-cut; exercise 04 drills the certifications portfolio plan. The external-facing authoring work — chapter 07's four artefact families with their stricter vocabulary discipline and distinct review-and-approval chain — appears as a *stretch goal* on exercise 01 (one trust-site update) but is never core-drilled as a coordinated pack. This lab is that specific authoring act: a coordinated trust-site update, external model card, regulator response, and Article 50 transparency notice drafted from a fixed internal baseline, with every chapter-07 rule exercised and every reviewer and signer named on the file. The failure mode this lab prevents is the analyst who can draft a legal briefing, a privacy briefing, a security briefing, a product briefing, and even a board briefing under internal-governance vocabulary but who — when the enterprise asks the analyst to draft the external-facing surface for the same system — over-claims on framework adherence, drops a limitation the internal card names, takes a legal position in a regulator response, writes marketing copy into an Article 50 notice, or ships from the analyst's own account because *"legal review will slow this down."* Chapter 07 is explicit that external-facing drafting is *where the analyst's writing intersects with the enterprise's public-facing risk surface*; this lab is the practice run before that writing lands on `[enterprise-domain]/responsible-ai`.
