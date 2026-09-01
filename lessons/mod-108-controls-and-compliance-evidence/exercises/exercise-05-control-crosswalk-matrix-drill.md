# Exercise 05 — Control Crosswalk Matrix Drill

**Estimated effort:** 2 hours
**Grounding chapters:** [07 — The Controls Crosswalk — ISO/IEC 42001, NIST AI RMF, EU AI Act, SR 11-7, and the Internal Catalogue](../07-controls-crosswalk-across-42001-rmf-eu-ai-act-sr-11-7.md), [03 — The Control-Status Report for Internal Audit](../03-control-status-report-for-internal-audit.md), [09 — Delegation Boundary and Escalation Patterns](../09-delegation-boundary-and-escalation-patterns.md).

## Objective

Build the analyst-tier controls crosswalk for the control subset drafted in exercise 01, then walk the four walk patterns (regulation-forward, control-forward, framework-forward, inventory-forward) end to end and file the class-1 library-design-fix escalations any gap surfaces. The drill's point is not to *design* the master control library — that stays `senior-ai-governance-architect` scope — but to *project* the library into the eleven-column crosswalk shape and to demonstrate that the projection lets a reader walk any obligation into every control and back.

After this exercise you should be able to open the crosswalk on any morning and, without pausing to re-derive the mapping, answer: (a) *for regulation X article Y, which of the enterprise's controls satisfy it?* (b) *for control Z, which regulator obligations does it satisfy?* (c) *for external framework F, does the enterprise have coverage?* and (d) *for inventoried system S, which controls apply?*.

## Prerequisites

- Chapter 07 read; the analyst-tier vs master-library distinction, the five column-source frameworks (ISO/IEC 42001 clauses, NIST AI RMF sub-categories, EU AI Act articles, SR 11-7 pillars, internal policy catalogue), the eleven-column baseline row shape, the four walk patterns, the four gap classes (uncovered obligation, uncovered control, mis-anchored control, drift), and the *analyst suggests, architect decides, analyst re-populates* line fresh in memory.
- Chapter 03 read; the twenty-column `CTL-<year>-<sequence>-<test-N>` row schema, particularly column 18 (framework crosswalk).
- Chapter 09 read; the class-1 library-design-fix escalation shape.
- The exercise-01 deliverable (`mod-108-ex-01-control-cycle-runbook.md`) open — the eight to twelve controls in exercise-01 §1 are the crosswalk row set.
- The `mod-106` regulatory-tracker rows for the EU AI Act, Colorado AI Act, NYC Local Law 144, and any sector overlay relevant to the MCDA / MCDA-Benefits pair open — the crosswalk's regulatory-tracker-anchor column (column 10) references these.
- The [ISO/IEC 42001 abstract](https://www.iso.org/standard/81230.html) and the [ISO/IEC JTC 1/SC 42 committee page](https://www.iso.org/committee/6794475.html) open for ISO/IEC 42001 clause structure; the [NIST AI Risk Management Framework 1.0](https://www.nist.gov/itl/ai-risk-management-framework), the [Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook), and the [Generative AI Profile (AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) open for the sub-category vocabulary; the [EU AI Act consolidated text (Regulation (EU) 2024/1689)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj) open for article citations; the [SR Letter 11-7](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) and the [OCC 2011-12 bulletin](https://www.occ.treas.gov/news-issuances/bulletins/2011/bulletin-2011-12.html) open for the pillar language.

## Problem statement

The deliverable is a **single Markdown file, `mod-108-ex-05-crosswalk-matrix.md`**, containing four parts. Use the controls from exercise-01 §1 as the row set; if you did not complete exercise 01, use a plausible eight-to-twelve-control subset per exercise 01's Step 1 rubric.

### Part 1 — The crosswalk matrix

Populate the eleven-column crosswalk from chapter 07 for every control in the exercise-01 §1 row set. Columns:

1. Control ID (`CTL-2026-<sequence>`)
2. Control statement (short-form; one line)
3. Enterprise role (*provider*, *deployer*, *provider-and-deployer*, or the applicable EU AI Act role; may be a list)
4. Applies to inventory tiers (Low / Medium / High / Prohibited-out-of-scope, or the local tier language)
5. ISO/IEC 42001 clause(s)
6. NIST AI RMF sub-category(ies)
7. EU AI Act article(s)
8. SR 11-7 pillar(s)
9. Internal policy reference(s) (`POL-<year>-<sequence>` with the local syntax)
10. Regulatory-tracker anchor (`REG-<year>-<sequence>` from `mod-106`)
11. Last verified against library (date the analyst last confirmed the mapping)

Populate each column per chapter 07's per-column guidance:

- **ISO/IEC 42001 clause(s).** Cite specific clauses of the management-system body (4–10) and Annex A control identifiers where they apply. The Annex A structure is paywalled; mark specific Annex A identifiers with `<!-- needs-research: verify Annex A identifier against licensed copy of ISO/IEC 42001:2023 -->` where you are working from paraphrase.
- **NIST AI RMF sub-category(ies).** Cite Function + Category + Sub-category (e.g., `MEASURE 2.7`, `GOVERN 1.1`, `MANAGE 4.1`). For generative-AI-specific mappings, `NIST AI 600-1 §<risk-action-identifier>`. Sub-category granularity where the control statement is specific enough.
- **EU AI Act article(s).** Cite article numbers, sub-paragraphs where the sub-paragraph matters, and the enterprise's role (provider vs deployer) explicitly. The high-risk provider obligations sit in Articles 8–17 and 43; the deployer obligation sits in Article 26; the transparency obligation in Article 50; general-purpose AI model obligations in Articles 51–55.
- **SR 11-7 pillar(s).** *Pillar 1 — Model development, implementation, and use*; *Pillar 2 — Model validation*; *Pillar 3 — Governance, policies, and controls*. Where the enterprise is not a supervised financial institution, this column may be *not-applicable* — but the pillar language is useful even outside financial services.
- **Internal policy reference(s).** Use bracket placeholders (`POL-2026-<sequence> §<section>`) if you cannot honestly cite the enterprise's own policy catalogue; do not invent policy content.
- **Regulatory-tracker anchor.** Link to the `REG-<year>-<sequence>` rows from `mod-106` that fire the update trigger for the row.

Include at least one row per each of these control categories from exercise 01: input/guardrail, fairness/disparate-impact, release-assurance sign-off, impact-assessment, vendor-artefact/supply-chain, eval-cadence, security-linked. This ensures the crosswalk exercises the full spread of framework anchors — the fairness row will map heavily to `MEASURE 2.11` / EU AI Act Article 10; the vendor row will map to Article 25 or Article 26 depending on role; the security-linked row will map to Article 15; the eval-cadence row will map to Article 9 and to NIST `MEASURE 2.7`; and so on.

### Part 2 — The four walks

Below the matrix, author a **§2 Four walks** section. For each walk, demonstrate the walk with a specific example:

- **§2.1 Regulation-forward walk.** Pick one EU AI Act article present in Column 7 of your matrix (Article 9, Article 15, or Article 26 are typical). Walk from the article to every control in the matrix that references it, then to the other framework anchors those controls resolve to (ISO/IEC 42001, NIST AI RMF, SR 11-7, internal policy). State the walk as a numbered chain the reader can retrace.
- **§2.2 Control-forward walk.** Pick one `CTL-<year>-<sequence>` identifier from your matrix (a control whose row has *fail* or *deviation* verdict from exercise 01 is ideal; otherwise pick a control that resolves to at least three framework anchors). Walk from the control to every obligation it satisfies and every affected inventory-row identifier. State the walk as a numbered chain.
- **§2.3 Framework-forward walk.** Pick one framework (ISO/IEC 42001 or NIST AI RMF is typical). Walk from the framework's structure to every control in the matrix that references it, and identify which subset of the framework's structure is *not covered* by any control in the matrix. Chapter 07's *uncovered obligation gap* is what this walk surfaces.
- **§2.4 Inventory-forward walk.** Pick MCDA (`INV-2026-0088`) or MCDA-Benefits (`INV-2026-0311` or equivalent). Walk from the inventory row to every control in the matrix that applies to the system's tier, and every framework anchor those controls resolve to. State the walk as a numbered chain.

Each walk is one short numbered list; the four together are what makes the crosswalk useful rather than decorative.

### Part 3 — Gap analysis

Below the four walks, author a **§3 Gap analysis** section. For each of chapter 07's four gap classes, identify any gap the matrix or the walks surface:

- **Uncovered obligation gap.** A framework anchor with no internal control pointing at it. Examples the batch will typically surface: EU AI Act Article 14 (human oversight) if no exercise-01 control names human oversight; EU AI Act Article 11 (technical documentation) if none of the controls covers the deployment-lifecycle technical documentation; NIST AI RMF `GOVERN 5.1` if no control names the AI-governance-council decision-record chain.
- **Uncovered control gap.** An internal control with no framework anchor. Examples the batch will typically surface: an enterprise-specific control on internal-brand-safety or an internal review committee that no external framework requires.
- **Mis-anchored control gap.** A control that cites a framework article the analyst reads as unrelated (or that has been superseded). Common with the EU AI Act as delegated acts and standards are published.
- **Drift gap.** A control whose framework anchor was correct at authoring but has since drifted. Common when `mod-106` regulatory-tracker rows have registered a material change since the last-verified date.

For each gap, author the class-1 library-design-fix escalation per chapter 09's row shape (rationale + requested action + escalation owner + target date + status). Chapter 07 was explicit that gaps become escalations, not silent fixes.

### Part 4 — The pre-issuance-review agenda

Below the gap analysis, author a **§4 Pre-issuance-review agenda** section. This is the artefact the analyst sends `senior-ai-governance-architect` before the crosswalk (and the control-status report from exercise 01 §4) reach internal audit. Author the agenda as:

- **Crosswalk maturity summary.** Rows in scope, framework anchors populated, framework anchors marked *not-applicable*, `<!-- needs-research: -->` markers outstanding, last-verified dates that need refresh.
- **Gap classes surfaced.** Roll-up per class from §3.
- **Class-1 escalation queue.** Full list of the class-1 escalations from §3, with rationale, requested action, and target-date proposal.
- **Optional-column recommendations.** Whether the enterprise should enable any of the optional columns chapter 07 named (NIST AI 600-1 risk-action identifiers, ISO/IEC 23894 risk-source references, sector-specific overlays, voluntary framework anchors) based on the batch you crosswalked.
- **Ask of `senior-ai-governance-architect`.** One-paragraph explicit ask — accept / defer / redirect on each gap-class item, sign-off on the crosswalk maturity summary, and confirmation of the target-date proposals.

## Requirements

- **The crosswalk matrix populates all eleven columns for every control** from exercise-01 §1. At minimum eight rows; up to twelve if exercise 01 authored twelve. Missing columns are populated with *not-applicable* (with a one-line reason) rather than blank.
- **Framework citations are specific referents, not bare framework names.** *NIST AI RMF MEASURE 2.7*, *EU AI Act Article 15(3)*, *ISO/IEC 42001:2023 §<clause>*, *SR 11-7 Pillar 2 — Ongoing monitoring*, *POL-2026-<sequence> §<section>*. Bare *NIST* or *EU AI Act* are not citations.
- **Enterprise role is stated in column 3 per system, not per enterprise.** Where MCDA is a *deployer* of a vendor foundation model and *provider* of the customer-facing wrap, the row states both.
- **Column 4 tier applicability matches the master library's tier language.** Do not invent a tier scheme the enterprise does not use.
- **Column 11 last-verified date is populated with a specific date.** The date is either today (for a fresh row) or the last cycle's date (if this is a mid-cycle projection); *recent* is not a date.
- **The four walks each produce a numbered chain.** A walk that is a paragraph without a chain reads as *analyst asserted the mapping rather than demonstrating it*.
- **The framework-forward walk (§2.3) identifies at least one framework-structure element not covered.** Chapter 07 was explicit that the framework-forward walk exists to surface uncovered obligations. A walk that finds full coverage of every framework element is either the world's most complete library or a walk that missed the gaps.
- **Gap analysis (§3) uses chapter 07's four gap classes.** Each gap is classified as uncovered-obligation / uncovered-control / mis-anchored / drift. A gap that does not fit one of the four is not a gap chapter 07 recognises; either refine the classification or note the row as a chapter-07-language-extension request.
- **Class-1 escalations use the chapter-09 template.** Rationale + requested library change + affected inventory and framework anchors + escalation owner (`senior-ai-governance-architect`) + target date + status.
- **Pre-issuance-review agenda (§4) has an explicit ask.** *Please review* is not an ask; *please confirm the class-1 queue is accepted and confirm the target dates* is.
- **No silent library edits.** The exercise does not permit the analyst to rewrite a control statement to close a gap; the class-1 escalation is the record of the requested change. Chapter 07's *analyst suggests, architect decides, analyst re-populates* discipline is the load-bearing rule.
- **No fabricated regulatory articles or ISO clauses.** Where an ISO/IEC 42001 Annex A control identifier is not verifiable from the public abstract, mark `<!-- needs-research: -->`; do not invent an identifier. Where a NIST sub-category is uncertain, cross-check against the Playbook; do not invent.

## Starter guidance

- Start with the NIST AI RMF column. It is the framework the analyst can cite most freely (public and specific), and it will populate for almost every control. Use it as the *anchor* column and populate other columns against it.
- The ISO/IEC 42001 column is the trap. The main clauses (4–10) are structural — *Context of the organisation*, *Leadership*, *Planning*, *Support*, *Operation*, *Performance evaluation*, *Improvement*. Most operational controls will cite Clause 8 (Operation) and Clause 9 (Performance evaluation), with specific Annex A control identifiers pending verification against a licensed copy of the standard. Mark uncertain Annex A citations with `<!-- needs-research: -->`.
- The EU AI Act column depends on the enterprise's role. If the enterprise deploys hosted foundation models via API to build a customer-facing high-risk AI system, the enterprise is both *provider* (of the customer-facing high-risk system, per Article 25 responsibilities of the high-value-chain provider) and *deployer* (of the underlying general-purpose AI model). The article citations differ per role — column 3 (enterprise role) is what the reader uses to audit the article choice.
- The SR 11-7 column is likely *not-applicable* if the enterprise is not a supervised financial institution; but if the enterprise operates in financial services, the pillar language is useful even outside the strict scope. Do not force the column; note *not-applicable — non-financial-services deployment* honestly where applicable.
- The regulation-forward walk (§2.1) usually reveals more coverage than expected — most controls that satisfy Article 15 (accuracy, robustness, cybersecurity) also touch Article 9 (risk management) and Article 12 (record-keeping). Walk the chain fully; do not stop at the first hop.
- The framework-forward walk (§2.3) is where chapter 07's *uncovered obligation gap* discipline shows up. Walk every high-risk-provider-obligation article and check the matrix's Column 7 for coverage; the articles that appear zero or one times across the eight-to-twelve-control matrix are almost certainly under-covered.
- Gap analysis (§3) is not fault-finding on `senior-ai-governance-architect` — chapter 07 was explicit that the crosswalk is a discovery tool. The gap classes are the format; the escalations are the record. The architect owns the resolution.
- The pre-issuance-review agenda (§4) is what makes the exercise-01 report and the exercise-05 crosswalk hang together. Both artefacts land at `senior-ai-governance-architect` before internal audit; the agenda is what the analyst brings to the shared review meeting.
- Do not skip §3 or §4. Chapter 07 was explicit that the crosswalk without the gap analysis is a decorative table; the gap analysis without the pre-issuance-review agenda is an escalation queue with no interlocutor.

## Acceptance criteria

- `mod-108-ex-05-crosswalk-matrix.md` filed with §1 crosswalk matrix (all eleven columns for every control from exercise-01 §1), §2 four walks, §3 gap analysis with class-1 escalations, §4 pre-issuance-review agenda.
- All eleven columns populated for every row; *not-applicable* used with reason rather than blank.
- Framework citations are specific referents. NIST AI RMF sub-category granularity; EU AI Act article-and-sub-paragraph; ISO/IEC 42001 clause and (where verifiable) Annex A identifier with `<!-- needs-research: -->` markers where paraphrased; SR 11-7 pillar and sub-topic; internal policy reference with local syntax.
- Enterprise role stated per row; last-verified date is a specific date.
- All four walks are numbered chains, not paragraphs.
- Framework-forward walk identifies at least one uncovered framework element.
- Gap analysis classifies every surfaced gap as one of chapter 07's four classes.
- Class-1 escalations use the chapter-09 template with all fields populated.
- Pre-issuance-review agenda has crosswalk maturity summary, gap-class roll-up, class-1 escalation queue, optional-column recommendations, and an explicit ask of `senior-ai-governance-architect`.
- No silent library edits; no fabricated citations; `<!-- needs-research: -->` markers used honestly where paraphrasing paywalled or uncertain sources.

## Stretch goals

- **A NIST AI 600-1 optional column.** Enable the [NIST AI 600-1 Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) risk-action optional column chapter 07 named, and populate it for every generative-AI-specific control in the matrix. This exercises the *optional columns* discipline and demonstrates the crosswalk's extensibility.
- **A sector-overlay optional column.** Pick one sector overlay per the enterprise's actual deployment (financial services: OCC / FRB guidance; healthcare: FDA good machine learning practice; hiring: NYC Local Law 144, EEOC guidance; public sector: Canadian Directive on Automated Decision-Making). Populate the column for every affected control and confirm the *analyst extends with `senior-ai-governance-architect` agreement* discipline is satisfied — i.e., the master library has been populated in that dimension too, or the column will be uniformly empty.
- **A cross-referenced update to exercise-01 §3 rows.** For every row in exercise-01 §3, update column 18 (framework crosswalk) with the specific citations from the crosswalk matrix built in this exercise. This closes the loop between the two exercises and demonstrates that the crosswalk is a *shared* artefact between the control-status report and the crosswalk matrix.
- **A crosswalk-vs-testing-coverage compare.** Author a short table that pivots the crosswalk (framework anchors covered by *at least one* control) against the exercise-01 §3 rows (controls actually tested in the period). Rows where the framework anchor is covered by a control that was *not tested this period* are visible as *unconfirmed coverage*; chapter 07's *framework-only coverage view without control-coverage view* failure mode is what this table catches.
- **A drift-monitoring cadence proposal.** After §4, add a short `## Drift monitoring` block proposing a cadence and a set of triggers for the *last verified* date. Chapter 07 was explicit that automation against `mod-106` regulatory-tracker material-change flags is what keeps the crosswalk from rotting. State the automation shape and the manual-check-frequency the analyst commits to.

## Deliverables

- `mod-108-ex-05-crosswalk-matrix.md` — §1 crosswalk matrix, §2 four walks, §3 gap analysis, §4 pre-issuance-review agenda, plus any stretch sections.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference crosswalk built against a ten-control exercise-01 subset covering the seven category minimum, with all eleven columns populated (with `<!-- needs-research: -->` markers on ISO/IEC 42001 Annex A identifiers), the four walks demonstrated on Article 15 (regulation-forward), a security-linked control (control-forward), NIST AI RMF (framework-forward), and MCDA-Benefits (inventory-forward), a gap analysis identifying four uncovered-obligation gaps (Articles 14 human-oversight, 11 technical documentation, `GOVERN 5.1` decision-record chain, and one drift on Article 26 from a `mod-106` material change), and a pre-issuance-review agenda that reads as one page. Yours will differ in the specific controls chosen, the specific framework citations, the specific gaps surfaced, and the specific escalations opened. What should not differ is (a) all eleven columns populated for every control, (b) specific-referent framework citations, (c) four walks as numbered chains, (d) at least one uncovered framework element in the framework-forward walk, (e) every gap classified against chapter 07's four gap classes, (f) class-1 escalations using the chapter-09 template, and (g) an explicit ask of `senior-ai-governance-architect` in §4. A tight crosswalk that walks cleanly beats a longer crosswalk whose citations blur the specific-referent discipline.
