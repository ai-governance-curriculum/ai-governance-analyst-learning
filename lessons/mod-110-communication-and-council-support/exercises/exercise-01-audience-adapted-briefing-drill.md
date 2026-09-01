# Exercise 01 — Audience-Adapted Briefing Drill

**Estimated effort:** 2 hours
**Grounding chapters:** [01 — The Analyst's Scope on Communication and Council Support](../01-analyst-scope-on-communication-and-council-support.md), [02 — Translating Technical Evidence for Five Audiences](../02-translating-technical-evidence-for-five-audiences.md), [03 — ISO/IEC 38507 and Board-Level Governance-Body Vocabulary](../03-iso-iec-38507-and-board-level-vocabulary.md), [09 — Delegation Boundary and Escalation Patterns](../09-delegation-boundary-and-escalation-patterns.md).

## Objective

Practise the *translate* verb — the first analyst-tier action per chapter 01 — at speed. The drill is single-source: one underlying technical artefact (a fairness-review note on MCDA-Benefits), and six audience-adapted briefings drawn from it — legal, privacy, security, product, executive committee, and board / governance body. The deliverable exercises the translation-not-summarisation rule (chapter 02), the per-audience vocabulary and depth constraints (chapter 02 matrix), the ISO/IEC 38507 governance-body vocabulary (chapter 03), and the delegation-boundary reminders (chapter 09) — *the analyst drafts; the analyst does not deliver executive or board briefings directly*.

The drill's point is that translation is a *filing decision* about audience, decision, and depth — not a *rewriting* exercise. The same substantive claim (a demographic-parity finding on a benefits-decision model) must appear in each briefing without drift; the vocabulary, the length, the depth, and the delivery channel change per audience. Getting the substantive claim consistent across six briefings is the discipline that separates translation from marketing.

After this exercise you should be able to take a single technical artefact and produce six audience-adapted briefings that each open with the audience's decision, cite the artefact by ID for every claim, and respect each audience's vocabulary and length constraints — without inventing claims the artefact does not support.

## Prerequisites

- Chapter 01 read; the analyst-tier verbs (translate, package, record, draft, factual-review, escalate) and the three tangible outputs (audience-adapted briefing, council packet, first-cut policy / standard draft) fresh in memory.
- Chapter 02 read; the five-audience matrix (legal, privacy, security, product, executive committee), the length / vocabulary / depth / cross-references / delivery-channel constraints per audience, the translation-not-summarisation rule (traceability + no unsupported claims), and the routing dependency per audience fresh in memory.
- Chapter 03 read; the ISO/IEC 38507 governance-body-vs-management distinction, the *evaluate / direct / monitor* spine, the AI-specific considerations vocabulary (autonomy, opacity, data use, cultural / behavioural change, third-party dependence), the board-vs-board-committee-vs-council altitude difference.
- Chapter 09 read; the delegation-boundary rows for translation and briefing — the analyst drafts every briefing; the analyst delivers the legal, privacy, security, and product briefings directly; the analyst does *not* deliver the executive-committee or board briefing (chapter 09's *the analyst never* column).
- The MCDA-Benefits system row (`INV-2026-0311` or the equivalent from your `mod-102` work) open — the drill's underlying artefact operates on this system. If your `mod-102` work used different placeholders, substitute yours throughout.

## Problem statement

The deliverable is **one Markdown file per audience, six files in total**, all located in a folder `mod-110-ex-01-briefings/`:

- `01-legal.md`
- `02-privacy.md`
- `03-security.md`
- `04-product.md`
- `05-executive-committee.md`
- `06-board.md`

Each briefing translates the same underlying artefact — a fairness-review note on MCDA-Benefits — into the receiving audience's language, at the audience's length, at the audience's depth, over the audience's delivery channel. A seventh file, `00-source-artefact.md`, holds the source artefact the six briefings translate from.

### The source artefact

Compose `00-source-artefact.md` to carry the underlying fairness-review note the six briefings translate. This file is *not* audience-adapted; it is the technical artefact `ai-eval-engineer` and `ai-risk-engineer` would have handed the analyst. Use the following facts (the drill supplies them so every candidate translates the same claim):

- **Artefact ID.** `EVAL-2026-0273` — fairness-review report on `INV-2026-0311` (MCDA-Benefits).
- **System.** MCDA-Benefits, the enterprise's model-assisted benefits-eligibility decision system. Operates in the UK (`mod-102` inventory row). Registered as high-risk under the enterprise's tiering methodology (mirrors EU AI Act Annex III point 5(a) on public-benefits eligibility).
- **Reviewer.** `ai-eval-engineer` [named delegate], with `ai-risk-engineer` [named delegate] co-signing on the residual-risk implications.
- **Review date.** 2026-08-24.
- **Data.** Six months of production traffic (2026-02-01 to 2026-07-31), 214,308 decisioned applications.
- **Findings.**
  1. **Demographic-parity difference (protected characteristic: applicant postcode segmented to the *rural-postcode-north* segment vs the enterprise's population baseline).** Approval rate: 61.4 % for the rural-postcode-north segment; 74.2 % population baseline. Difference: 12.8 percentage points (95 % CI [10.9, 14.7]). Outside the enterprise's fairness threshold (≤ 8 pp per the enterprise's `mod-104` fairness-review methodology).
  2. **Equal-opportunity difference (true-positive-rate parity on the same segment).** TPR: 0.83 for rural-postcode-north vs 0.91 baseline. Difference: 0.08 (95 % CI [0.06, 0.10]). Outside the enterprise's fairness threshold (≤ 0.05).
  3. **Root-cause hypothesis.** The retrieval features driving the model include a *distance-to-nearest-service-centre* variable that correlates with the rural-postcode-north segment and is not adjusted for.
  4. **Second finding.** A subset of overturns (61 of 214,308 decisions across the six months) surfaced through the manual re-review escalation path — of those, 43 came from the rural-postcode-north segment, disproportionate to the segment's share of the traffic.
- **Impact-assessment cross-reference.** `FRIA-2026-0044` on MCDA-Benefits — currently signed off; the fairness-review finding above the enterprise's threshold triggers a re-open per `mod-105` chapter 05's re-open protocol.
- **Register cross-reference.** `RISK-2026-0104` — the register entry for MCDA-Benefits' fairness-related residual. Residual currently accepted at 4×3 = 12 on the enterprise's 5×5 matrix; the fairness-review finding likely re-scores to a higher residual.
- **Control cross-reference.** `CTL-2026-0031` — the fairness-monitoring control on MCDA-Benefits, currently *tested this quarter, evidence current*.
- **Regulator-tracker cross-reference.** `TRK-2026-0018` — EU AI Act Annex III point 5(a) obligation row (with the enterprise's UK-post-Brexit-assimilation position noted); `TRK-2026-0022` — UK Equality Act 2010 indirect-discrimination obligation.
- **Vendor cross-reference.** `VND-2026-0007` — the third-party feature-store vendor whose distance-to-service-centre variable is the retrieval feature implicated in finding 3.
- **Recommended actions per the reviewer.**
  - Re-open `FRIA-2026-0044` per `mod-105` chapter 05.
  - Re-score `RISK-2026-0104` on the register; the current 4×3 acceptance is unlikely to survive the re-score.
  - Open an `INC-2026-<sequence>` per `mod-109` chapter 02 class 4 (biased-outcome escalation) — the manual-re-review finding crosses the class-4 threshold on the enterprise's incident taxonomy.
  - Route to `ai-eval-engineer` for a feature-reweighting or feature-removal proposal; route to `ai-risk-engineer` for the residual re-scoring; route to `data-protection-officer` for the Article 22 automated-decision review; route to `legal` for the Equality Act indirect-discrimination review.
  - Present at the next AI governance council meeting for a residual-risk-acceptance decision above threshold.

Compose the source artefact concisely (roughly one page); the six briefings are the substantive deliverable. If any figure above conflicts with your `mod-104` work, substitute yours and note the substitution at the top of the source file.

### The six audience-adapted briefings

For each audience, produce a Markdown file with the following common header at the top:

```
Audience: [audience name]
Delivery channel: [per chapter 02]
Delivered by: [who — analyst directly / analyst drafts, X delivers]
Underlying artefact: EVAL-2026-0273 (fairness-review report on INV-2026-0311, MCDA-Benefits)
Related artefacts: FRIA-2026-0044, RISK-2026-0104, CTL-2026-0031, TRK-2026-0018, TRK-2026-0022, VND-2026-0007
Author: [analyst name]
Date drafted: [YYYY-MM-DD]
Length: [word or page count, per chapter 02 constraint]
```

Then the substantive body per the audience's constraints (below).

#### 01-legal.md

- **Length.** One to three pages (per chapter 02).
- **Vocabulary anchor.** Statutes and articles. At minimum, name the UK Equality Act 2010 (indirect discrimination — s.19), GDPR Article 22 (solely automated decision-making producing legal or similarly significant effects on the individual), and — where the UK-post-Brexit-assimilation-of-EU-AI-Act position warrants it — the equivalent EU AI Act Article 27 FRIA obligation and Annex III point 5(a) high-risk classification the enterprise's tiering mirrors.
- **Depth of technical detail.** Just enough to make the exposure legible. Metric tables go into an annex; the body carries the exposure characterisation.
- **Structure.**
  - Opening sentence naming the exposure characterisation (e.g., *"EVAL-2026-0273 identifies a potential UK Equality Act 2010 indirect-discrimination exposure on MCDA-Benefits with respect to the rural-postcode-north segment."*).
  - The finding stated in legal-adjacent language.
  - The cited statutory / regulatory / contract-clause anchors.
  - The exposure characterisation the legal audience is being asked to open a case file on (or the *no known legal anchor* note, if that were the case).
  - The recommended legal next steps at analyst-tier depth (a case file, a review of prior similar incidents, a coordination with the DPO on Article 22).
  - Cross-reference block by artefact ID.
  - Annex — the metric table from the source artefact.
- **Do not.** Interpret the statute (chapter 09 boundary: legal takes the position; the analyst names the exposure). Do not claim the model *is* discriminatory (the finding is a demographic-parity difference above threshold; whether that constitutes *indirect discrimination* under s.19 is legal's call). Do not omit the confidence interval on the metrics.

#### 02-privacy.md

- **Length.** One to two pages plus a lawful-basis / data-flow annex.
- **Vocabulary anchor.** GDPR articles (5(1)(a) fairness principle, 5(1)(d) accuracy, 6 lawful basis, 22 automated decision-making with legal or similarly significant effects, 25 data protection by design, 35 DPIA). The enterprise's DPIA methodology. UK GDPR post-Brexit assimilation.
- **Depth of technical detail.** Data-flow and processing detail — what personal data is processed, where the retrieval feature (`distance-to-nearest-service-centre`) is sourced from (vendor `VND-2026-0007`), whether the feature is a proxy for personal data of a special category (e.g., religion, ethnic origin) where rural-postcode-north correlates with such a category, and the DPIA re-open trigger.
- **Structure.**
  - Opening sentence naming the DPIA re-open trigger and the Article 22 review question.
  - The finding stated in privacy language.
  - Article-by-article translation of the finding (5(1)(a), 22, 25).
  - The vendor-flow implication (`VND-2026-0007` — is the distance-to-service-centre feature covered in the vendor's DPA, and does the DPA include a fairness-review clause?).
  - Cross-reference to `FRIA-2026-0044` (currently signed off; re-open triggered) and to any adjacent DPIA.
  - Data-flow annex.
- **Do not.** Take the lawful-basis position (the DPO takes it; the analyst names the question). Do not conflate the fairness finding with a data-quality finding — they are distinct GDPR concerns.

#### 03-security.md

- **Length.** One to two pages, with a mitigation-tracking annex.
- **Vocabulary anchor.** Chapter 02 identified OWASP LLM Top 10, MITRE ATLAS, NIST AI 100-2, Google SAIF as the security-audience anchors. On a fairness finding the direct security-taxonomy anchor is subtler than on a jailbreak or a prompt-injection — the finding may not map to a specific OWASP LLM Top 10 entry (which is LLM-application-focused). Use the MITRE ATLAS *ML Model Access* / *ML Attack Staging* categories where the vendor-supplied feature is an attack surface (`VND-2026-0007`); use NIST AI 100-2e2025's *abuse* attack class where the biased-outcome finding may be exploited or amplified; note explicitly if no security-taxonomy mapping applies and the finding is a fairness-and-risk finding routed *for information* to security rather than as a mitigation ticket. Chapter 02 was explicit that a briefing without a legal-anchor writes *no known legal anchor*; the same discipline applies here — *no known security-taxonomy anchor; routed for information* is a valid brief.
- **Structure.**
  - Opening sentence naming the security question (is this a threat class security needs to open a mitigation ticket on, or is it a fairness-and-risk finding routed to security for awareness?).
  - The finding stated in security-taxonomy language (or the *no-known-taxonomy-anchor* note).
  - The vendor-feature-store surface (`VND-2026-0007`) as an attack-adjacent question.
  - The escalation call (mitigation ticket / awareness note / red-team scoping request).
  - Cross-reference block.
- **Do not.** Force a mapping to an OWASP LLM Top 10 entry where the finding does not fit. Do not open a mitigation ticket on the analyst's own authority — the security engineer named for MCDA-Benefits opens the ticket if warranted.

#### 04-product.md

- **Length.** One page, with a launch-gate recommendation.
- **Vocabulary anchor.** Product-team language — the feature name, the customer segment, the launch gate, the roadmap milestone, the mitigation. Framework citations minimal in the body.
- **Depth of technical detail.** Just enough to make the launch-gate call defensible.
- **Structure.**
  - Opening sentence naming the launch-gate call. MCDA-Benefits is already in production, so the call is about *ongoing operating status* rather than a fresh launch — the analyst frames the equivalent gate (continue operating / continue with conditions / pause / roll back).
  - The finding stated in product-team language.
  - The mitigation surface (feature-reweighting or feature-removal proposal per the reviewer's recommendation) with rough turnaround.
  - The council-decision path (the residual-risk re-score will land at the AI governance council; product owner named as a contributor to the pre-read).
  - Cross-reference block.
- **Do not.** Make the operating-status call in place of the product owner and `head-of-ai-governance`. Do not treat the fairness finding as a *feature-request delay* — it is a governance finding first.

#### 05-executive-committee.md

- **Length.** Half a page to one page (per chapter 02).
- **Vocabulary anchor.** The enterprise's own strategic-priority language. Portfolio-level metrics (customer trust, regulatory posture, competitive position, the enterprise's public-facing responsible-AI posture). Framework citations in a footnote, not the body.
- **Delivery.** Drafted by the analyst; delivered by `head-of-ai-governance` (chapter 09 boundary). Header names the delivery role explicitly.
- **Structure.**
  - Opening sentence naming the portfolio-level implication (a high-risk system in production has a fairness finding above the enterprise's threshold; the AI governance council will decide the residual re-acceptance at its next meeting; the item may escalate to board oversight if the residual re-score crosses the board-attention threshold).
  - One paragraph of context (management's response — the FRIA re-open, the risk re-score, the incident opened, the specialist-role routing).
  - The executive-committee decision surface (there is not usually a decision the executive committee takes on this item directly; the item is *for awareness* pending the council's decision).
  - Cross-reference block.
- **Do not.** Write more than one page. Do not include the eval metric table in the body (annex or footnote at most). Do not deliver directly to the executive committee (chapter 09 boundary).

#### 06-board.md

- **Length.** One page (per chapter 03; boards read short packs).
- **Vocabulary anchor.** ISO/IEC 38507 governance-body vocabulary. The *evaluate / direct / monitor* spine. The AI-specific considerations (autonomy, opacity, data use, cultural / behavioural change, third-party dependence) where they apply.
- **Delivery.** Drafted by the analyst, reviewed by `senior-ai-governance-architect` and `legal`, delivered by `head-of-ai-governance` (chapter 09). Header names all three.
- **Structure per chapter 03's worked skeleton.**
  1. **What management is asking the board to evaluate.** *"Management (via the AI governance council) is reviewing the residual-risk acceptance on MCDA-Benefits following a fairness finding above the enterprise's threshold. The board is asked to evaluate management's response, not to take a system-level decision."*
  2. **What management is asking the board to direct.** *Option A — endorse management's approach (FRIA re-open, risk re-score, incident opened, specialist-role routing, council decision at next meeting). Option B — require management to return to the board at the next quarterly touch-point with an update. Option C — [where warranted] escalate the item to a board committee (audit / risk / technology) for deeper review.*
  3. **What management is asking the board to monitor.** *The AI governance council's decision on the residual re-acceptance (minute reference to be provided at the next quarterly update); the FRIA re-open outcome; the incident record's post-mortem.*
  4. **AI-specific considerations (ISO/IEC 38507).** Autonomy (MCDA-Benefits makes decisions that reach applicants without a human in the loop on the default path; the manual re-review path exists as the human-oversight backstop); opacity (the finding was surfaced by systematic fairness review, not by inspection of the model's internals — chapter 03's opacity vocabulary); data use (the implicated feature is sourced from `VND-2026-0007`); cultural / behavioural change (management notes the operations manager's Slack thread signal that manual re-reviewers are picking up shifts); third-party dependence (the vendor whose feature-store carries the implicated variable).
  5. **Prior-record cross-references.** Prior board / council decisions on MCDA-Benefits (typical prior decisions on the system's original tier-1 sign-off, FRIA sign-off, and the residual acceptance — cited by minute reference or *TBD-<meeting-date>* if not yet available in your worked artefacts).
  6. **Cross-references (footnote / annex).** `EVAL-2026-0273`, `FRIA-2026-0044`, `RISK-2026-0104`, `INV-2026-0311`, `TRK-2026-0018`, `TRK-2026-0022`, `VND-2026-0007`, and — once opened — the incident record ID.
- **Do not.** Write more than one page. Do not use council-level operational language; use governance-body vocabulary throughout. Do not cite framework text verbatim in the body (footnote / annex only). Do not attribute a decision to *the enterprise* or *we* — every material claim is attributable to either the board (past decisions, endorsed appetite, ratified policies) or management (current operations, ongoing work, upcoming asks). Do not deliver directly to the board (chapter 09 boundary).

## Requirements

- **All six briefings plus the source artefact are filed as separate Markdown files** in `mod-110-ex-01-briefings/` with the specified names.
- **The source artefact is identical for all six briefings.** No briefing introduces a claim the source artefact does not support. If a briefing needs a claim the source does not carry, the briefing names the gap and routes it, per chapter 02's *no claims the artefact does not support* rule.
- **Every substantive claim in every briefing cites the artefact ID(s) it derives from.** No claim without a citation.
- **The demographic-parity number, the equal-opportunity number, and the confidence intervals appear in every briefing in some form** — headline number in the body plus full metric table in the annex where the audience's length permits. Chapter 02 was explicit that summarisation that drops the uncertainty is a failure mode.
- **The legal briefing names at least two statutes with article numbers.** UK Equality Act 2010 s.19 and GDPR Article 22 at minimum. *No known legal anchor* is not the right answer for this artefact.
- **The privacy briefing names the DPIA re-open trigger explicitly** and names the article path (Article 22 review, Article 5(1)(a) fairness, Article 35 DPIA) — but does not take the DPO's lawful-basis position.
- **The security briefing acknowledges the ambiguous security-taxonomy mapping.** A forced mapping to *OWASP LLM01 — Prompt Injection* on a fairness finding is a chapter-02 failure mode. *No known security-taxonomy anchor; routed for information* or the ATLAS / NIST-AI-100-2 nearest-anchor with the reasoning is acceptable.
- **The product briefing frames the call as *ongoing operating status* (not a fresh launch),** with the mitigation surface and the council-decision path both named.
- **The executive-committee briefing fits on one page.** The delivery-by field names `head-of-ai-governance`, not the analyst. The briefing is for awareness pending the council's decision — a decision from the executive committee itself is not the ask.
- **The board briefing uses ISO/IEC 38507's *evaluate / direct / monitor* spine.** All five sections present (evaluate, direct, monitor, AI-specific considerations, prior-record cross-references). Every material claim is attributable to either the board or management explicitly. The briefing fits on one page.
- **No briefing takes a role's decision in that role's place.** Legal takes the legal position; the DPO takes the lawful-basis position; the security engineer opens the mitigation ticket; the product owner takes the operating-status call; the council decides the residual re-acceptance; the board decides the appetite. The analyst names the question and characterises the artefact.
- **The delivery-channel field is set correctly per chapter 02 and 09.** Legal / privacy / security / product briefings delivered by the analyst directly to the receiving role or its tracker. Executive-committee briefing delivered by `head-of-ai-governance`. Board briefing delivered by `head-of-ai-governance` after `senior-ai-governance-architect` and `legal` reviews.
- **No fabricated statute citations, no fabricated case law, no fabricated regulator bulletins.** Chapter 02 was explicit: the analyst does not extend the finding beyond what the artefact supports. Cite statutes that exist; do not invent enforcement precedent.

## Starter guidance

- Compose the source artefact first, then the six briefings. Write the source once and refer to it while drafting the six; do not compose the source in parallel with the briefings — it drifts.
- For each briefing, before writing the first sentence, write two lines at the top of your drafting scratch-pad: *(a) the audience's decision on this item is [X]; (b) the vocabulary anchor is [Y].* Chapter 02 was explicit that the briefing's structure follows the decision.
- Draft the legal briefing first. It anchors the language legal will use back to the analyst; if the legal briefing gets the statute-and-article mapping right, the privacy briefing (Article 22) and the board briefing (regulatory posture in the AI-specific-considerations block) become easier.
- Draft the board briefing last. It is the hardest — the governance-body-vs-management vocabulary discipline is where most drafts break down. Chapter 03 was explicit that every material claim is attributable to either the board or management; run the draft through that filter as a final pass.
- For the security briefing, do not force a taxonomy mapping. Chapter 02's *no known legal anchor* pattern applies here — *no known OWASP-LLM-Top-10 anchor; the nearest ATLAS-adjacent category is [X] but the finding is a fairness-and-risk finding first; routed to security for awareness* is a legitimate briefing.
- For the product briefing, remember that MCDA-Benefits is *already in production*. The launch-gate vocabulary from chapter 02 needs to be adapted to an operating-status vocabulary — the equivalent decision is *continue operating / continue with conditions / pause / roll back*, not *approve for launch*.
- For the executive-committee briefing, keep the framework alphabet soup out of the body. Chapter 02 was explicit that citations go in an annex or footnote; the body is in the enterprise's language.
- For the board briefing, chapter 03 was explicit: every claim is attributable to *the board* or *management*, and management asks for one of *evaluate / direct / monitor*. If your draft has a claim attributable to neither, the sentence is unfinished; complete it or delete it.
- The delivery-channel discipline is a chapter-09 boundary. Executive-committee and board briefings are delivered by `head-of-ai-governance`; the analyst drafts. Putting the analyst's name in the *Delivered by* field on the executive or board briefing is off-side.
- The metric table (demographic-parity number, TPR number, CIs, sample size) should appear in every briefing at some depth — headline in body, or annex with the full table — but the depth varies per audience. Legal and privacy carry it in an annex; security carries the vendor-feature-surface framing in the body; product carries the mitigation-timeline framing in the body; the executive committee reads a portfolio-level sentence with the metrics in a footnote; the board reads the ISO/IEC 38507-vocabulary framing with the metrics behind the referenced artefact ID.
- Cite `mod-102` (inventory), `mod-103` (register), `mod-104` (fairness methodology), `mod-105` (FRIA), `mod-106` (tracker), `mod-108` (control, vendor), and `mod-109` (incident, PMS) IDs by placeholder where you do not have specific IDs from your own prior work. Consistent placeholders across the six briefings are what allow the reader to see the same finding across audiences.

## Acceptance criteria

- Seven files filed in `mod-110-ex-01-briefings/`: `00-source-artefact.md`, `01-legal.md`, `02-privacy.md`, `03-security.md`, `04-product.md`, `05-executive-committee.md`, `06-board.md`.
- The source artefact carries the finding's substance (demographic-parity difference, TPR difference, root-cause hypothesis, second finding, cross-references, recommended actions) at roughly one page.
- Every briefing carries the common header (audience, delivery channel, delivered by, underlying artefact, related artefacts, author, date drafted, length).
- Every briefing opens with the audience's decision or read-for question in the first sentence.
- Every substantive claim in every briefing cites an artefact ID.
- The metric numbers appear consistently across all six briefings (no drift).
- Legal briefing: 1–3 pages, names UK Equality Act 2010 s.19 and GDPR Article 22 at minimum, exposure characterisation in the body, metric table in the annex, does not interpret the statute.
- Privacy briefing: 1–2 pages plus data-flow annex, names the DPIA re-open trigger, names Articles 22 / 5(1)(a) / 35 at minimum, does not take the lawful-basis position, addresses the vendor `VND-2026-0007` DPA question.
- Security briefing: 1–2 pages, acknowledges the ambiguous taxonomy mapping honestly, does not force an OWASP LLM Top 10 mapping, names the ATLAS-nearest-anchor if one is warranted, does not open a mitigation ticket on the analyst's authority.
- Product briefing: 1 page, frames the call as ongoing operating status, names the mitigation surface and the council-decision path, does not take the operating-status call in place of the product owner.
- Executive-committee briefing: ≤ 1 page, portfolio-level framing, framework citations in a footnote at most, delivery-by field names `head-of-ai-governance`, no decision from the executive committee itself is the ask.
- Board briefing: ≤ 1 page, ISO/IEC 38507 *evaluate / direct / monitor* spine present with all five sections, every material claim attributable to *the board* or *management* explicitly, AI-specific considerations (autonomy, opacity, data use, cultural / behavioural change, third-party dependence) named in the standard's own words where they apply, delivery-by field names `head-of-ai-governance` (with `senior-ai-governance-architect` and `legal` as reviewers), no framework alphabet soup in the body.
- No briefing takes a role's decision in that role's place. No fabricated statutes, case law, or regulator bulletins.

## Stretch goals

- **The regulator-inquiry hypothetical.** Draft a seventh file, `07-regulator-inquiry-hypothetical.md`, imagining that six months from now the UK Equality and Human Rights Commission opens an inquiry into MCDA-Benefits' rural-postcode-north segment outcomes. Compose the analyst's first-cut response draft per chapter 07's regulator-response discipline — the analyst drafts and factual-checks; the accountable executive signs and submits. Do not submit; the exercise is a drafting drill. Chapter 09's class-3 escalation applies from the moment the regulator inquiry lands.
- **The trust-site update draft.** Draft an `08-trust-site-update.md` file — the analyst-contributed first-cut of the update to the enterprise's responsible-AI trust-site page reflecting the FRIA-re-open outcome (assume: the re-open concludes that the enterprise re-scores the residual to unacceptable, removes the distance-to-service-centre feature, and re-launches with a documented mitigation). Apply chapter 07's external-facing vocabulary discipline (precise framework names with versions, *aligned* not *compliant*, cited metrics with basis, named limitations). Route by chapter 07's review-and-approval chain (drafted / factual-reviewed / signed by whom).
- **The pre-read one-pager sibling.** Draft a `09-pre-read-one-pager.md` file — a chapter 04 one-pager for the AI governance council meeting where the residual-risk re-acceptance on `RISK-2026-0104` will be decided. The pre-read is a sibling artefact to the six briefings; the analyst who has translated the finding for six audiences will have the vocabulary needed for the council pre-read at the ready. This stretch goal is the natural bridge to exercise 02.
- **The vocabulary-drift audit.** After all six briefings are drafted, compose a `10-vocabulary-drift-audit.md` file — a 200–400 word analyst's-own note listing (a) the substantive claim as it appears in the source artefact, (b) how the claim is worded in each of the six briefings, (c) any drift in the wording, and (d) the fix. Chapter 02's translation-not-summarisation rule is a discipline; auditing your own drift is how the discipline gets internalised.
- **The delegation-boundary contact log.** Compose an `11-boundary-contact-log.md` file listing every role your briefings hand the artefact to (legal delegate, DPO, security engineer, product owner, `head-of-ai-governance`, chair of the AI governance council, `senior-ai-governance-architect`, accountable executive for board delivery) with the specific hand-off — *what* the analyst hands, *when*, and the expected turnaround. Chapter 09 was explicit that the delegation boundary is load-bearing; the log is how the analyst tracks it.

## Deliverables

- `mod-110-ex-01-briefings/` folder containing:
  - `00-source-artefact.md`
  - `01-legal.md`
  - `02-privacy.md`
  - `03-security.md`
  - `04-product.md`
  - `05-executive-committee.md`
  - `06-board.md`
- Optional stretch files (`07-` through `11-`) named clearly.

## Notes on evaluation

The paired solutions repo works one reference source artefact and one reference set of six briefings. The load-bearing calls your draft is expected to match: (a) the demographic-parity and TPR numbers with their CIs appearing consistently across all six briefings; (b) the legal briefing anchoring on UK Equality Act 2010 s.19 and GDPR Article 22; (c) the privacy briefing naming the DPIA re-open trigger and *not* taking the DPO's lawful-basis position; (d) the security briefing acknowledging the ambiguous taxonomy mapping rather than forcing OWASP LLM01; (e) the product briefing framing operating-status rather than launch-gate; (f) the executive-committee briefing at ≤ 1 page delivered by `head-of-ai-governance`; (g) the board briefing at ≤ 1 page using ISO/IEC 38507's *evaluate / direct / monitor* spine and the AI-specific-considerations vocabulary, delivered by `head-of-ai-governance` after `senior-ai-governance-architect` and `legal` reviews. The narrower calls — specific mitigation-timeline estimates, specific council-meeting dates, specific board-committee routing — will differ per your enterprise's structure. What should not differ is: (i) traceability to the source artefact for every claim, (ii) no unsupported claims added beyond the source, (iii) no role's decision taken in that role's place, (iv) the delivery-by discipline on the executive-committee and board briefings, (v) the ISO/IEC 38507 vocabulary on the board briefing. A tight six-briefing set that gets the vocabulary right beats a longer set that drifts the substantive claim across the six or that has the analyst delivering the board briefing directly.
