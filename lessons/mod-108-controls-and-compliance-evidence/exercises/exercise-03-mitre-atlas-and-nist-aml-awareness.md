# Exercise 03 — MITRE ATLAS and NIST AML Awareness Drill

**Estimated effort:** 2 hours
**Grounding chapters:** [05 — MITRE ATLAS, NIST AI 100-2, and Google SAIF](../05-mitre-atlas-nist-ai-100-2-and-google-saif.md), [04 — OWASP LLM Top 10 and the Analyst-Tier Taxonomy](../04-owasp-llm-top-10-and-analyst-tier-taxonomy.md), [09 — Delegation Boundary and Escalation Patterns](../09-delegation-boundary-and-escalation-patterns.md).

## Objective

Practise reading across the four AI/LLM security-threat references — OWASP LLM Top 10 (primary filing), NIST AI 100-2 (attack-class taxonomy), MITRE ATLAS (adversary tactics and techniques), and Google SAIF (defence-programme areas) — at the *recognition depth* the analyst-tier role calls for. The drill is scenario-based: given a batch of security-linked artefacts drawn from red-team engagement reports, incident tickets, vendor notices, and control-test findings, the deliverable is (a) a per-artefact reference-set table naming the four tags where each applies, (b) an anchoring on chapter 05's seven top categories, (c) a *recognition-vs-exploitation* boundary check that names when the analyst would stop and hand off, and (d) a defender-side control-anchoring pass that maps each finding to a SAIF element the enterprise's control library would carry.

The drill's point is that the four references do different work. OWASP names the risk; NIST AI 100-2 names the attack; ATLAS names the technique; SAIF names the defence-programme area. The analyst carries whatever the source artefact names and does not manufacture the missing ones. Getting the composition right on paper is what makes the crosswalk (chapter 07) and the control-status report (chapter 03) hang together.

After this exercise you should be able to look at any inbound security-linked artefact and, within a minute, name the OWASP primary tag, the NIST AI 100-2 attack-class family, the ATLAS technique identifier if the source artefact names one, the SAIF defence-programme element the corresponding control should anchor to, the top-category from chapter 05's seven, and the recognition-vs-exploitation boundary line the analyst does not cross.

## Prerequisites

- Chapter 05 read; the four references (OWASP LLM Top 10, MITRE ATLAS, NIST AI 100-2e2025, Google SAIF), the four AI 100-2 attack-class families (evasion, poisoning, privacy, abuse), the ATLAS tactics-and-techniques matrix shape, the SAIF six elements, and the seven top categories the analyst must recognise (prompt injection, data exfiltration, model theft, membership inference, adversarial evasion, supply-chain compromise, guardrail bypass) fresh in memory.
- Chapter 04 read; the OWASP LLM Top 10 2025 items and sub-variants.
- Chapter 09 read; the recognition-vs-exploitation boundary and the class-2 security-route escalation shape.
- The [MITRE ATLAS matrix](https://atlas.mitre.org/matrices/ATLAS) and the [ATLAS case studies](https://atlas.mitre.org/studies) open for the current tactic-and-technique identifiers. Confirm the identifier and title at read time — ATLAS is a living matrix.
- The [NIST AI 100-2e2025 report](https://csrc.nist.gov/pubs/ai/100/2/e2025/final) abstract open, and the report itself if you have desk access; the exercise's citations reference the four families and note edition specifically.
- The [Google Secure AI Framework (SAIF)](https://safety.google/cybersecurity-advancements/saif/) page open for the current six-element wording. SAIF has been revised over time; confirm the current wording at read time.
- The exercise-02 deliverable open — several of the drill's scenarios extend scenarios you already tagged with OWASP identifiers, and this exercise adds the second, third, and fourth tags on top.

## Problem statement

The deliverable is a **single Markdown file, `mod-108-ex-03-atlas-nist-saif.md`**, containing five parts.

### Part 1 — The reference-set table

The drill provides ten short artefact scenarios below. For each, produce a reference-set row with:

- **Artefact ID.** `SEC-A01` through `SEC-A10`.
- **One-line summary.** Paraphrase the artefact in one sentence.
- **Source artefact class.** Where the artefact comes from — red-team engagement report, incident ticket, vendor security advisory, control-test finding, monitoring alert, eval-report finding.
- **Primary OWASP LLM 2025 tag.** Version-cited per chapter 04's rule.
- **NIST AI 100-2e2025 attack-class family.** *Evasion*, *poisoning*, *privacy*, or *abuse*, with a one-line rationale referencing the family's definition from chapter 05.
- **NIST AI 100-2e2025 sub-class.** Where the source artefact or the family's definition names a sub-class (e.g., *black-box evasion — targeted*, *training-data poisoning — backdoor*, *privacy — membership inference*, *abuse — content-generation misuse*), state it. Where the source does not name a sub-class, mark *sub-class not named by source*.
- **ATLAS technique identifier.** *Only where the source artefact names one*. If the source names *AML.T0051 LLM Prompt Injection*, carry it verbatim. Otherwise, mark *not-named-in-source*; do not manufacture.
- **ATLAS tactic anchor.** From the current [ATLAS matrix](https://atlas.mitre.org/matrices/ATLAS) — the analyst is allowed to name the *tactic* (higher-level column) even when the source does not name a specific technique, because tactics group findings by adversary phase. Chapter 05's *use the tactic name for grouping* discipline governs.
- **SAIF element anchor.** Which of SAIF's six elements the corresponding *control* (defender side) sits under. State the element name as SAIF publishes it.
- **Chapter-05 top-category.** Which of the seven top categories (prompt injection, data exfiltration, model theft, membership inference, adversarial evasion, supply-chain compromise, guardrail bypass) the finding sits under.

The ten scenarios:

- **SEC-A01.** A red-team engagement report on MCDA (`INV-2026-0088`) tests a jailbreak variant that circumvents the guardrail-classifier by wrapping the adversarial instruction in a base64-encoded payload embedded in a retrieved document. The report cites `AML.T0051 LLM Prompt Injection` and `AML.T0054 LLM Jailbreak`, and classifies the technique against the *ML Model Access* tactic column. The system prompt was not disclosed; the model produced a policy-violating output. No live customer traffic was affected — the engagement ran against an isolated evaluation endpoint.
- **SEC-A02.** A vendor security advisory from a foundation-model provider notes that a specific membership-inference query pattern can, at scale, reveal whether a specific training corpus contained a particular record. The advisory notes NIST AI 100-2e2025's *privacy attacks — membership inference* family and recommends rate-limiting inference to slow the attack. The enterprise uses the model through the vendor's enterprise API tier.
- **SEC-A03.** An incident ticket on the contract-review-assistant (`INV-2026-0104`) reports that a customer's competitor made ~50,000 short queries over a two-week period, each designed to elicit representative outputs across a specific corpus category. The pattern is consistent with a model-extraction / model-theft campaign. The infra-team believes the API keys were legitimate (the competitor was a real paying customer during that window).
- **SEC-A04.** A control-test finding from the quarterly cycle notes that the training-data provenance for the enterprise's Llama fine-tune (`INV-2026-0122`) cannot be re-verified — the upstream Hugging Face mirror was compromised (the SEC-03 finding from exercise 02), and the fine-tune has been running in production since. No behavioural anomaly has been observed, but the analyst files the *supply-chain* finding as a class-2 escalation.
- **SEC-A05.** A red-team engagement report on the agentic MCDA variant (`INV-2026-0409`) demonstrates that the agent can be induced to call the *send-email* tool by supplying the destination address inside the user prompt, without triggering the human-in-the-loop confirmation the design-review had committed to. The report cites `AML.T0057 LLM Plugin Compromise` and the *Impact* tactic column.
- **SEC-A06.** An eval-report finding on MCDA-Benefits shows a specific demographic-slice-triggered underperformance whose vector is a known keyword pattern in user input. The eval author notes that the trigger appears to be a *backdoor* introduced by a fine-tuning dataset slice contributed by a third-party labelling vendor. The affected inputs are ~0.1% of the eval corpus.
- **SEC-A07.** A monitoring alert on the HR-Policy-Bot (`INV-2026-0128`) shows that a specific series of adversarial prompts consistently pushed the model to output PII fragments the model appears to have memorised from training data. The scenario extends SEC-02 from exercise 02.
- **SEC-A08.** A vendor advisory from a self-hosted-model publisher (e.g., a Mistral or DeepSeek-family release) notes that a specific supply-chain compromise on a widely used tokenizer-adjacent library affects any deployment that pulled the affected dependency version between two dates. The enterprise's ML platform team confirms MCDA-lite (`INV-2026-0122`) pulled the affected version and has been running it in production.
- **SEC-A09.** A red-team engagement report on the RAG-augmented contract-review-assistant (`INV-2026-0104`) shows an *embedding-inversion* attack that reconstructs partial source-document text from vector-store entries. The report cites `AML.T0043 Craft Adversarial Data` and *Exfiltration* tactic. Some of the reconstructed content is confidential customer contract text.
- **SEC-A10.** A council-member email asks the analyst to *"look at whether we might be vulnerable to LLM-abuse attacks like generating phishing content"*. The council member attaches an OWASP blog post but does not attach any internal artefact.

### Part 2 — Anchor on chapter 05's seven top categories

Below the Part-1 table, add a **§2 Seven-category anchor** section. For each of chapter 05's seven top categories (prompt injection, data exfiltration, model theft, membership inference, adversarial evasion, supply-chain compromise, guardrail bypass), list the SEC-A* rows that fall under it, and note whether each row is a *primary* or *secondary* fit. Chapter 05's summary table (top-category × OWASP × AI 100-2 × ATLAS × SAIF) is the reference; the exercise applies it to the ten scenarios.

Where a scenario touches two categories (e.g., SEC-A05 touches guardrail-bypass and excessive-agency; SEC-A03 touches model-theft with a data-exfiltration overlap), note both with the primary named first. Where a scenario does not fit any of the seven, name it explicitly — chapter 05 was clear that not every finding belongs in the seven, and the analyst records the finding as *outside AI 100-2 taxonomy* per the rule.

### Part 3 — Recognition-vs-exploitation boundary check

Below the seven-category anchor, add a **§3 Boundary check** section. For each SEC-A* row, name the specific analyst-tier verb from chapter 05's *recognition depth vs exploitation depth* discussion:

- **Recognition-depth verbs.** *Tag*, *file*, *route*, *carry forward the source's identifier*, *cite the AI 100-2 family*, *anchor the control to a SAIF element*.
- **Exploitation-depth verbs the analyst does *not* do.** *Reproduce the exploit*, *construct a new payload*, *derive an ATLAS identifier from scratch*, *evaluate mitigation code*, *set severity*.

For each row, name the *last analyst-tier verb* — what the analyst does — and the *first hand-off verb* — what the analyst hands off. Cite the receiving role by name (`ai-infra-security`, `ai-red-team-engineer`, `application-security`, `data-protection-officer`, `procurement`, `senior-ai-governance-architect`, `head-of-ai-governance`, `incident-response-team`, per chapters 05, 09).

SEC-A01, SEC-A05, and SEC-A09 test the *ATLAS identifier* rule especially: the source artefact names the identifier; the analyst carries it forward and does not derive. SEC-A02 tests the *NIST AI 100-2 sub-class* rule: the vendor advisory names the sub-class explicitly; the analyst carries it forward. SEC-A10 tests the *do not tag speculatively* rule from chapter 04 and the *recognition-depth verb* discipline from chapter 05 — the analyst opens a scoping request; the analyst does not tag the finding as an AI 100-2 abuse-family attack in the absence of an internal artefact.

### Part 4 — Defender-side control-anchoring pass

Below the boundary check, add a **§4 Defender-side anchor** section. For each SEC-A* row that would drive a control-library change (whether a new control, a re-worded control, or a re-anchored control), name the SAIF element the control should anchor to and the class-1 library-design-fix escalation the analyst would file per chapter 09.

- SEC-A01, SEC-A05, and SEC-A09 all point at controls in the *Adapt controls to adjust mitigations and create faster feedback loops for AI deployment* SAIF element. SEC-A04 and SEC-A08 point at *Expand strong security foundations to the AI ecosystem* and *Harmonise platform-level controls*. SEC-A03 points at *Expand strong security foundations* (rate-limiting, anomaly detection). SEC-A02 and SEC-A07 point at *Expand strong security foundations* and *Contextualise AI system risks in surrounding business processes*. SEC-A06 points at *Adapt controls* and *Contextualise risks*.
- For each escalation, populate the class-1 fields from chapter 09: rationale, requested library change (owner-reassignment, cadence change, evidence-class change, or new control scope), affected inventory identifiers, blast radius.

The exercise's point at this part is that the OWASP tag files the *finding*; the SAIF anchor drives the *control* — and the class-1 escalation is the bridge between the two.

### Part 5 — Recurring-pattern roll-up

Below the defender-side anchor, add a **§5 Recurring-pattern roll-up** section. Identify any two-or-more SEC-A* rows that share an OWASP tag, an AI 100-2 family, an ATLAS tactic, or a SAIF element. For each pattern, state the chapter-09 escalation-owning role and the recommended library-level policy work.

Chapter 09's *pattern language for library-level policy work* section named four patterns explicitly:

- Three same-control library-design-fix escalations in a rolling year.
- Recurrent LLM01 findings across multiple systems.
- Multiple vendor rows where the DPA position is negotiated post-signature.
- Council-decision escalations resolving with *no decision*.

The ten-row batch above will exhibit variants of the first two patterns. The roll-up is what the analyst brings to the council briefing per `mod-110`.

## Requirements

- **All ten scenarios are populated in Part 1.** Every row has ID, summary, source artefact class, primary OWASP tag (version-cited), NIST AI 100-2 family + sub-class (with *sub-class not named by source* where applicable), ATLAS technique identifier (only where the source names one; else *not-named-in-source*), ATLAS tactic anchor, SAIF element anchor, chapter-05 top-category.
- **ATLAS technique identifiers are only carried forward where the source names them.** *Not manufactured.* Chapter 05 was explicit — SEC-A01, SEC-A05, SEC-A09 carry named identifiers; SEC-A02, SEC-A03, SEC-A04, SEC-A06, SEC-A07, SEC-A08, SEC-A10 do not have named identifiers and are marked accordingly.
- **NIST AI 100-2 citations are edition-cited.** *AI 100-2e2025 — Evasion*, not *AI 100-2 — Evasion*. Chapter 05 was explicit that edition matters.
- **SAIF element wording matches the current published list.** The six elements are named as SAIF publishes them; the exercise's summary above uses commonly cited phrasings and should be verified at read time.
- **Chapter-05 top-category assignments are correct.** SEC-A01 = prompt injection (primary) + guardrail bypass (secondary). SEC-A02, SEC-A07 = membership inference / data exfiltration crossings. SEC-A03 = model theft (primary) + data exfiltration overlap. SEC-A04, SEC-A08 = supply-chain compromise. SEC-A05 = guardrail bypass + agent-abuse variant. SEC-A06 = adversarial evasion + poisoning-family overlap. SEC-A09 = data exfiltration + adversarial evasion overlap. SEC-A10 = *speculative — no artefact* per chapter 05's rule that the analyst does not manufacture the category.
- **Part 2 seven-category anchor accounts for all ten rows** with primary/secondary noted where the row touches two.
- **Part 3 boundary check names the last analyst-tier verb and the first hand-off verb per row.** No row is *analyst does everything* and no row is *analyst does nothing*.
- **Part 4 SAIF-anchored escalations use the chapter-09 class-1 template.** Rationale, requested change, affected inventory identifiers, blast radius.
- **Part 5 recurring-pattern roll-up identifies at least one pattern across the ten rows** and cites chapter 09's pattern language.
- **No manufactured identifiers.** No fake ATLAS techniques, no fabricated CVE / CWE / MITRE ATT&CK IDs, no invented AI 100-2 sub-classes.
- **No severity or exploitability assignments.** Chapter 04 and chapter 05's *do not use the tag as a severity claim* rule and the *severity is `ai-infra-security`'s call* boundary govern.

## Starter guidance

- Part 1 is a mechanical read-across. Start with the OWASP primary tag (which you may have from exercise 02 for SEC-A01 through SEC-A07 depending on scenario mapping), then walk to the AI 100-2 family, then to the ATLAS technique (only if the source names it), then to the SAIF element. Chapter 05's summary table is the mechanical guide.
- The temptation on Part 1 is to *guess* an ATLAS identifier that fits. Do not. Chapter 05 was explicit — the analyst carries forward what the source names, and asks the security team when in doubt. A row that carries *AML.T00XX (analyst guess)* is worse than a row that carries *not-named-in-source — ask ai-infra-security*.
- SEC-A02 tests the *NIST AI 100-2 sub-class discipline* — the vendor advisory names *membership inference*; the analyst carries the sub-class forward verbatim rather than paraphrasing to a family-level *privacy attack*.
- SEC-A03 is *model theft* — chapter 05's seven-category anchor names it. The OWASP mapping is LLM10 via the model-extraction sub-variant; the AI 100-2 family is *privacy* (model theft is an AI 100-2 privacy-family attack in the report's terminology).
- SEC-A05 tests both guardrail-bypass and the excessive-agency composition — chapter 04's LLM06 tag applies at the OWASP layer; the AI 100-2 family is *abuse* or *evasion* depending on how you read the sub-class; the ATLAS technique the source names is `AML.T0057 LLM Plugin Compromise`. The SAIF anchor is *Adapt controls* because the control that fails is the human-in-the-loop confirmation the design-review committed to.
- SEC-A06 is the *deliberate poisoning* case that separates from SEC-04 in exercise 02. Here the eval author has evidence of a backdoor trigger from a labelling-vendor dataset slice; the AI 100-2 family is *poisoning* explicitly and the ATLAS tactic anchor is *Resource Development / Initial Access* (per chapter 05's mapping).
- SEC-A08 is the *self-hosted-supply-chain* case. Chapter 05 was explicit that supply-chain compromise crosses OWASP LLM03 and AI 100-2 poisoning (when the vector is training-time) or supply-chain (when the vector is deployment-dependency). Note the vector explicitly.
- SEC-A09 is the *embedding-inversion* case. Chapter 05's LLM08 anchor at the OWASP layer; the AI 100-2 family is *privacy* (data reconstruction sub-class); the ATLAS technique the source names is `AML.T0043 Craft Adversarial Data`; the SAIF anchor is *Contextualise AI system risks in surrounding business processes* because the reconstruction risk depends on what the vector store contains (customer contract text).
- SEC-A10 is the *council-forwarded blog post* — the analyst does *not* tag it. Chapter 04's *do not tag speculatively* rule and chapter 05's *the analyst does not manufacture* discipline apply. The correct response is to file a scoping request to `ai-red-team-engineer` or `ai-infra-security` and note in Part 3 that the *first hand-off verb* is *open scoping request*; there is no primary OWASP tag on this row.
- Part 4's escalations are class-1 library-design-fix escalations, not class-2 security-route escalations. Part 3's routing decisions are class-2. Do not confuse the two — chapter 09's class definitions govern.
- Part 5's recurring-pattern roll-up is the shape the analyst brings into a council briefing. Two or more SEC-A rows sharing an OWASP tag is a pattern; two or more sharing an ATLAS tactic is a pattern; two or more sharing a SAIF element is a pattern. State the pattern honestly; do not force a pattern that is not present in the batch.

## Acceptance criteria

- `mod-108-ex-03-atlas-nist-saif.md` filed with §1 reference-set table (all ten scenarios), §2 seven-category anchor, §3 boundary check, §4 defender-side anchor with class-1 escalations, §5 recurring-pattern roll-up.
- Every §1 row has all nine columns populated per the schema above.
- ATLAS technique identifiers appear only on SEC-A01 (`AML.T0051`, `AML.T0054`), SEC-A05 (`AML.T0057`), and SEC-A09 (`AML.T0043`) — the three scenarios whose source artefact names the identifier. All other rows carry *not-named-in-source*.
- NIST AI 100-2 citations are edition-cited (`AI 100-2e2025 — <family>`).
- SEC-A02's row cites *AI 100-2e2025 — Privacy attacks — Membership inference*; SEC-A03 cites *AI 100-2e2025 — Privacy attacks — Model extraction / model theft*; SEC-A04 cites *AI 100-2e2025 — Poisoning* (when the vector is training-time) with the supply-chain crossing noted; SEC-A05 cites *AI 100-2e2025 — Abuse* (agentic-tool-abuse sub-class) or *Evasion* per how the source reads.
- §2 anchors every SEC-A row against the seven top categories with primary/secondary noted; SEC-A10 is anchored as *speculative — no artefact*.
- §3 names the last analyst-tier verb and the first hand-off verb per row; SEC-A10's first hand-off verb is *open scoping request*, not *tag and route*.
- §4 SAIF-anchored escalations use the chapter-09 class-1 template with all fields populated.
- §5 identifies at least one recurring pattern; the load-bearing candidates are (a) LLM01-family prompt-injection findings across multiple systems (SEC-A01, SEC-A05, SEC-A07 — variants of the same guardrail-architecture gap) and (b) supply-chain findings (SEC-A04, SEC-A08).
- No manufactured identifiers, no severity assignments, no fabricated CVE/CWE labels.
- SAIF element wording matches the current published SAIF list (verified at read time).

## Stretch goals

- **A cross-reference to a red-team-engagement scoping request.** For SEC-A10 specifically, draft the scoping request the analyst sends to `ai-red-team-engineer` asking for an internal LLM-abuse evaluation of the enterprise's systems most likely to be misused for phishing-content generation. The request cites the OWASP list's abuse-adjacent items (LLM09 misinformation crosses here), the AI 100-2 abuse family, and the enterprise's customer-facing systems the assessment should scope against.
- **A SAIF-coverage map.** After §5, add a `## SAIF-coverage map` block that lists the six SAIF elements and, per element, the SEC-A* rows that would drive a control-library change against that element. This is the artefact `senior-ai-governance-architect` would read to see coverage of the enterprise's control library against SAIF; it exercises chapter 07's crosswalk in the *analyst-tier subset* direction.
- **A four-tag composition cheatsheet.** Extract chapter 05's summary table (top-category × OWASP × AI 100-2 × ATLAS × SAIF) into a standalone reference (e.g., `mod-108-ex-03-taxonomy-cheatsheet.md`) that the analyst pins next to their desk. The exercise's real value shows the day the cheatsheet lands on a new analyst's onboarding materials.
- **A NIST AI 100-2 edition-drift note.** Compare the NIST AI 100-2e2023 and AI 100-2e2025 abstract-level content (from NIST's own release notes) and identify at least two areas where the taxonomy shifted between editions. Chapter 05's *the report has been revised* discipline applies — cite the edition every time and re-verify attack-class names between editions.
- **A recognition-vs-exploitation-boundary card.** For your own reference (and for the next analyst you onboard), extract chapter 05's *recognition depth vs exploitation depth* discussion into a one-page reference card, tightened against the scenarios you triaged. This is the artefact the analyst pins next to their desk; the drill's real value shows the day the card starts to look worn.

## Deliverables

- `mod-108-ex-03-atlas-nist-saif.md` — §1 reference-set table, §2 seven-category anchor, §3 boundary check, §4 defender-side anchor, §5 recurring-pattern roll-up, plus any stretch sections.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference table for the ten scenarios with the four-tag composition per row, and one reference set of class-1 escalations per SAIF element. Your table will match on the load-bearing calls (ATLAS identifiers only where the source names them; edition-cited AI 100-2; NIST family assignments per chapter 05; the SAIF anchors per the summary table; the seven-top-category anchors; SEC-A10 not tagged). The narrower calls — the specific SAIF-element wording (SAIF revises), the specific sub-class within a family, the specific escalation rationale — will differ per your enterprise's structure. What should not differ is (a) all ten rows populated per the schema, (b) no manufactured ATLAS identifiers, (c) edition-cited AI 100-2 references, (d) SEC-A10 held as speculative rather than tagged, (e) the class-1-versus-class-2 escalation distinction from chapter 09 applied correctly, and (f) at least one recurring pattern identified in §5. A tight read that carries source-named identifiers forward without invention beats a longer read that guesses techniques and inflates the tag set.
