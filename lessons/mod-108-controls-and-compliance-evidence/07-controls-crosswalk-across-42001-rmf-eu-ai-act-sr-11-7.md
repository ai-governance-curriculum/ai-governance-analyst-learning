# The Controls Crosswalk — ISO/IEC 42001, NIST AI RMF, EU AI Act, SR 11-7, and the Internal Catalogue

## Why this chapter

Chapters 02 and 03 fixed the cycle and the report. Chapter 06 fixed the vendor row. Every control tested in the cycle, every vendor row in the register, every finding in the report resolves back to one or more *obligations* — external (a regulator's article, a standard's clause, a supervisory letter) or internal (a policy in the enterprise's catalogue). Without a walking map between them, the analyst re-derives the mapping every quarter and the report degrades into inconsistency between periods.

The walking map is the *controls crosswalk*: a table that lists internal controls against the external frameworks that require them (or against which the enterprise voluntarily aligns), plus the internal-policy reference for each. This chapter fixes the analyst-tier crosswalk shape, walks the five source frameworks the analyst reads columns from, states the hand-off boundary with `senior-ai-governance-architect` (who owns the *master* control library the crosswalk projects), and closes with the walk-discipline that keeps the crosswalk useful rather than decorative.

The distinction is deliberate. The *master control library* is `senior-ai-governance-architect`'s. The *crosswalk* is the analyst's — a projection of the library that answers *for control X, which obligations does it satisfy in each of the frameworks the enterprise cares about?*. Same information, different pivot; the analyst maintains the pivot.

## The analyst-tier crosswalk vs the master control library

Two artefacts, two owners, two purposes. The distinction shows up whenever a reader asks the wrong question at the wrong table.

| | Master control library | Analyst-tier crosswalk |
|---|---|---|
| Owner | `senior-ai-governance-architect` | `ai-governance-analyst` |
| Primary purpose | Enumerate every enterprise control with its wording, owner, cadence, and evidence-class expectations | Walk each control to the external and internal obligations it satisfies |
| Row shape | One row per control (`CTL-<year>-<sequence>`) with full attributes | One row per control with columns pointing to ISO/IEC 42001, NIST AI RMF, EU AI Act, SR 11-7, and the internal policy catalogue |
| Update cadence | On library revision (`senior-ai-governance-architect`-owned change management) | On master-library revision + on regulatory-tracker material-change (`REG-<year>-<sequence>` from `mod-106`) |
| Consumer | Internal audit, external audit, regulator, control owner | Analyst-during-cycle, internal audit for scoping, `mod-106` regulatory tracker for coverage view, vendor-intake for compensating-controls anchoring |
| Failure mode when confused | Analyst edits control statement to "clean up" a crosswalk mismatch | `senior-ai-governance-architect` rewrites master library rows without updating crosswalk pointers |

The analyst never edits the master control library from the crosswalk side. When the crosswalk exposes a gap ("*there is no control in the library that satisfies EU AI Act Article 14 human-oversight for this system*"), the response is *raise the gap to `senior-ai-governance-architect`*, not *invent a control statement*.

## The five column-source frameworks

The analyst-tier crosswalk carries five columns beyond the control-identifier and control-statement columns. Each column sources from a specific framework and each has a specific referent shape.

### Column A — ISO/IEC 42001 clauses

- **Framework.** [ISO/IEC 42001:2023 — Information technology — Artificial intelligence — Management system](https://www.iso.org/standard/81230.html). The AI management system standard published by ISO/IEC JTC 1/SC 42.
- **Referent shape.** Clause number (main clauses 4–10 of the management-system body) and Annex A control identifier (Annex A carries the reference AI-specific controls the enterprise selects from). Example referent format: `ISO/IEC 42001:2023 §7.5.3` for a documented-information clause, `ISO/IEC 42001:2023 Annex A.<identifier>` for a control.
- **Where the analyst gets the mapping.** From the master control library's own `ISO/IEC 42001` column, populated by `senior-ai-governance-architect` when the control was authored. The analyst carries the pointer through; the analyst does not re-derive.
- **Common failure mode.** Citing a body clause when the mapping is to an Annex A control, or vice versa. Fix: use the exact reference syntax; verify against a licensed copy of the standard.
- **Analyst-tier note.** ISO/IEC 42001 is paywalled. The analyst can read the public [abstract](https://www.iso.org/standard/81230.html) and the [SC 42 committee summaries](https://www.iso.org/committee/6794475.html); enterprise use requires a licensed copy for the clause-level detail. Mark specific-clause citations with `<!-- needs-research: -->` where the analyst is working from paraphrase.

<!-- needs-research: ISO/IEC 42001 Annex A structure and control identifiers should be verified against a licensed copy of the standard before an audit-facing citation. The public abstract does not enumerate Annex A. -->

### Column B — NIST AI RMF sub-categories

- **Framework.** [NIST AI Risk Management Framework 1.0 (AI RMF, NIST AI 100-1)](https://www.nist.gov/itl/ai-risk-management-framework), the analyst's foundational reference walked in `mod-101` and `mod-103`. The [Generative AI Profile (NIST AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) supplements the core framework for generative-AI-specific risk actions.
- **Referent shape.** Function + Category + Sub-category (e.g., `MEASURE 2.7`, `GOVERN 1.1`, `MANAGE 4.1`). For generative-AI-specific mappings, `NIST AI 600-1 §<risk-action-identifier>`.
- **Where the analyst gets the mapping.** From the master control library's own `NIST AI RMF` column. The analyst carries the pointer through. Where the control was authored before the Generative AI Profile was published, the analyst raises a *needs-refresh* flag to `senior-ai-governance-architect`.
- **Common failure mode.** Mapping to a Category when the underlying obligation is a Sub-category. Fix: sub-category granularity where the control statement is specific enough to warrant it; category granularity only where the control genuinely spans multiple sub-categories.
- **Analyst-tier note.** The NIST AI RMF is public and downloadable; the Playbook (public) enumerates sub-categories and outcome statements. This is the framework the analyst can cite most freely.

### Column C — EU AI Act obligations

- **Framework.** [Regulation (EU) 2024/1689 — the EU Artificial Intelligence Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj), with the obligations most-frequently crosswalked being those on high-risk AI systems (Chapter III, Articles 8–17 for providers) and general-purpose AI models (Chapter V, Articles 51–55 and following). Deployer obligations (Chapter III Section 3, especially Article 26 for high-risk deployment) and transparency obligations (Article 50) also feature.
- **Referent shape.** `EU AI Act Article <n>` at minimum; `EU AI Act Article <n>(<sub>)` where the sub-paragraph matters. Cite the recital only when the analyst is anchoring the *interpretation* rather than the *obligation*.
- **Where the analyst gets the mapping.** From the master control library, augmented by the `mod-106` regulatory-tracker rows that surfaced each obligation. When the EU AI Act phases in a new obligation (the [phased entry-into-application timeline](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) runs through 2024–2027 with the [AI Act service desk](https://digital-strategy.ec.europa.eu/en/policies/ai-office) supporting), `mod-106` fires the trigger and `senior-ai-governance-architect` re-anchors the control; the analyst re-populates the crosswalk column.
- **Common failure mode.** Citing an article that applies to *providers* on a control whose enterprise role is *deployer*, or vice versa. Fix: name the enterprise's role per system on the crosswalk row so the reader can audit the article choice.
- **Analyst-tier note.** The Act is available in every EU official language on EUR-Lex. Cite the official-journal reference (`OJ L 2024/1689`) once per crosswalk header for the archival record; use article numbers thereafter.

### Column D — SR 11-7 pillars

- **Framework.** [Board of Governors of the Federal Reserve System, SR Letter 11-7 — Guidance on Model Risk Management](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) (April 2011), the US supervisory guidance for model risk management at supervised financial institutions. The OCC issued a parallel guidance ([OCC 2011-12](https://www.occ.treas.gov/news-issuances/bulletins/2011/bulletin-2011-12.html)); the FDIC and NCUA have adopted the framework by reference. For AI systems in financial services, SR 11-7 is often the *first-in* governance frame, with the AI-specific standards layered on top.
- **Referent shape.** *Pillar 1 — Model development, implementation, and use*; *Pillar 2 — Model validation*; *Pillar 3 — Governance, policies, and controls*. Cite the pillar and, where the referent is specific, the sub-topic (e.g., *Pillar 2 — Ongoing monitoring*).
- **Where the analyst gets the mapping.** From the master control library. If the enterprise is not a supervised financial institution, this column may be empty by default — but the pillar language is a widely-adopted mental model even outside financial services, and many enterprises populate the column voluntarily.
- **Common failure mode.** Treating SR 11-7 as an AI-specific framework. It is not — it is a model risk management framework that pre-dates the modern AI-standards wave by a decade. Fix: use the pillar as an organising lens for the analyst's own writing, not as an AI-specific citation.

<!-- needs-research: For enterprises whose deployments touch multiple financial-services regulators (SEC / CFTC in the US, FCA / PRA in the UK, ESMA / EBA in the EU, MAS in Singapore, etc.), the SR 11-7-style guidance under each regulator has evolved. Verify the local supervisory guidance in force before citing SR 11-7 alone. -->

### Column E — Internal policy catalogue

- **Framework.** The enterprise's own policy catalogue — an internal document set that establishes the enterprise's positions on responsible AI, model risk management, data governance, third-party risk, information security, privacy, and any sector-specific policies.
- **Referent shape.** `POL-<year>-<sequence> §<section>` (or the enterprise's local identifier syntax). Every enterprise runs a different catalogue naming; the analyst uses the local convention.
- **Where the analyst gets the mapping.** From the master control library's `Internal policy` column, plus the analyst's cross-check that each cited policy still exists at the cited section (policies are revised more often than control statements; a control that points to `POL-2024-0018 §4` when the policy has been re-published as `POL-2026-0018 §4.2` is a crosswalk error the analyst catches at the next cycle).
- **Common failure mode.** Citing a policy that has been superseded but not yet retired from the catalogue index. Fix: the analyst checks the policy status at cycle time and updates the pointer or raises a `senior-ai-governance-architect` request.

### Optional columns the enterprise may add

- **[NIST AI 600-1](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) Generative AI Profile risk-action identifiers.** Used when the enterprise runs generative-AI systems and wants explicit coverage of GAI-specific risk actions.
- **[ISO/IEC 23894:2023](https://www.iso.org/standard/77304.html) risk-source references.** Used when the enterprise wants to trace which 23894 risk source a control mitigates. Anchored in the analyst-tier risk-source scan-list from `mod-103` chapter 02.
- **Sector-specific overlays.** For financial services: OCC / FRB / ESMA / FCA guidance; for healthcare: [FDA good machine learning practice](https://www.fda.gov/medical-devices/software-medical-device-samd/good-machine-learning-practice-medical-device-development-guiding-principles) principles, HIPAA where personal health information is in scope; for hiring: [NYC Local Law 144](https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page), EEOC guidance; for the public sector: [Canadian Directive on Automated Decision-Making](https://www.tbs-sct.canada.ca/pol/doc-eng.aspx?id=32592) via the AIA.
- **Voluntary framework anchors.** For enterprises tracking the [OECD AI Principles](https://oecd.ai/en/ai-principles), the [Council of Europe Framework Convention on AI](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence), or industry-specific codes.

The analyst extends columns with `senior-ai-governance-architect` agreement — new columns require the master library to have been populated in that dimension too, or the crosswalk column will be uniformly empty.

## The crosswalk row shape

The analyst's crosswalk row schema (eleven columns for the baseline; more if optional columns are enabled):

| # | Column | Content |
|---|---|---|
| 1 | Control ID | `CTL-<year>-<sequence>` |
| 2 | Control statement (short) | The library's control statement, truncated to one line for scan-ability |
| 3 | Enterprise role | *provider*, *deployer*, *provider-and-deployer*, *importer*, *distributor*, *authorised representative* — per system, per EU-AI-Act role and equivalents; may be a list where the control applies across roles |
| 4 | Applies to inventory tiers | Which `mod-102` tier(s) the control applies to (Low / Medium / High / Prohibited-out-of-scope, or the enterprise's local tier language) |
| 5 | ISO/IEC 42001 clause(s) | Column A |
| 6 | NIST AI RMF sub-category(ies) | Column B |
| 7 | EU AI Act article(s) | Column C |
| 8 | SR 11-7 pillar(s) | Column D |
| 9 | Internal policy reference(s) | Column E |
| 10 | Regulatory-tracker anchor | `REG-<year>-<sequence>` identifiers from `mod-106` that fire the update trigger for this row |
| 11 | Last verified against library | Date the analyst last confirmed the mapping matches the master library |

The row does not carry the full control statement, owner, cadence, or evidence-class expectations — those live in the master library. The crosswalk row is a *projection*; the reader who needs the full attributes clicks through the `CTL-<year>-<sequence>` identifier.

## The walk discipline

The crosswalk is only useful if a reader can walk from *any* single referent to the others without re-authoring the mapping. Four walks the analyst practises.

- **Regulation-forward walk.** Given an EU AI Act article, find every internal control that satisfies it and every ISO / NIST / SR-11-7 / policy anchor those controls resolve to. Used when the regulator publishes an implementing act, a delegated act, or a guideline that changes the article's scope; used when internal audit selects a regulator-forward sample.
- **Control-forward walk.** Given a `CTL-<year>-<sequence>` identifier, find every framework obligation the control satisfies. Used when a control fails a test and the analyst needs to name the obligations left uncovered for the escalation.
- **Framework-forward walk.** Given an ISO / NIST / SR-11-7 anchor, find every internal control that references it. Used when the enterprise is preparing for an external audit against that framework and wants a coverage view.
- **Inventory-forward walk.** Given a `mod-102` inventory row, find every control that applies to the system's tier and the framework anchors those controls resolve to. Used when a new system enters production and the analyst assembles the applicable-controls set.

The walks compose. A regulator-forward walk that surfaces a control with no evidence in the last two cycles is a *known-obligation, unevidenced-control* escalation; a control-forward walk that surfaces no framework anchor at all is a *control-may-be-obsolete* escalation.

## When the crosswalk exposes a gap

Four gap classes and their handling.

- **Uncovered obligation gap.** A framework anchor with no internal control pointing at it. The analyst raises a *control-authoring request* to `senior-ai-governance-architect` with the framework citation and the affected `mod-102` inventory rows. The analyst does not draft the control.
- **Uncovered control gap.** An internal control with no framework anchor. May be legitimate (enterprise-specific policy stronger than the frameworks require); may be obsolete (a control retained from an older policy set no longer maps to any current obligation). The analyst flags for `senior-ai-governance-architect` review.
- **Mis-anchored control gap.** A control that cites a framework article the analyst reads as unrelated (or that has been superseded). Common with the EU AI Act as delegated acts and standards are published. The analyst files a *re-anchor request*.
- **Drift gap.** A control whose framework anchor was correct at authoring but has since drifted (framework standard revised, regulatory-tracker material change since the last-verified date). The analyst updates the *last verified* date only when the mapping still holds; where it does not, the analyst files the drift as a *re-anchor request*.

Every gap becomes an escalation-register entry per the four classes in chapter 09. The escalation-register roll-up appears in the control-status report's §5 (chapter 03) and the council briefings' policy agenda (`mod-110`).

## The hand-off boundary with `senior-ai-governance-architect`

Restated for clarity.

- **The analyst maintains the crosswalk.** The crosswalk is the analyst's tangible artefact for this chapter.
- **The `senior-ai-governance-architect` owns the master control library.** Any change to a control statement, wording, owner, cadence, evidence-class expectation, or framework anchor sits with that role.
- **The analyst raises library changes as escalations.** Gap classes above are the trigger set; the escalation register (chapter 09) is the queue.
- **The `senior-ai-governance-architect` implements library changes.** When the change lands, the analyst re-populates the crosswalk column, updates the *last verified* date, and re-runs the affected walk to confirm coverage.

The line is *analyst suggests, architect decides, analyst re-populates*. No shortcuts across the line.

## Cadence

- **On regulatory-tracker material change.** `mod-106` fires a change; the analyst walks the affected framework column; escalations follow.
- **On master-library revision.** `senior-ai-governance-architect` publishes a new / revised control; the analyst updates the crosswalk row(s) and confirms the framework anchors.
- **At each cycle.** During the periodic control-testing cycle (chapter 02), the analyst refreshes the *last verified* date on every touched row and walks any gap that surfaced.
- **On external-audit prep.** When the enterprise is preparing for an external ISO/IEC 42001 audit, a SOC 2 examination, or an independent audit (chapter 08), the framework-forward walk feeds the coverage view the external auditor scopes against.

## Common failure modes

- **Crosswalk edited without master-library edit.** The analyst re-anchors a control on the crosswalk without raising the corresponding library change. Result: crosswalk and library diverge; internal audit finds the difference and both reads are wrong. Fix: the *analyst suggests, architect decides, analyst re-populates* line.
- **Column referent syntax drift.** One row says `EU AI Act 15`; another says `Article 15 EU AI Act`; a third says `AI Act Art 15`. Fix: fix a single syntax convention at the crosswalk header and apply consistently.
- **Cadence-tracked date rot.** *Last verified* dates that have not moved in years while the frameworks have moved substantially. Fix: automate the cadence check against the `mod-106` regulatory-tracker material-change flags.
- **Framework-only coverage view without control-coverage view.** The analyst can show every framework anchor is covered by *at least one* control, but not that every control has a *current* test in the cycle. Fix: two views — coverage forward (chapter 07) and testing forward (chapter 03) — with a compare at report time.
- **Optional columns half-populated.** ISO/IEC 23894 or NIST AI 600-1 column added but only some rows populated. Fix: either populate every applicable row or remove the column; a half-populated column reads as *analyst forgot* rather than *not applicable*.

## What to memorise

- **The crosswalk is analyst-tier; the master control library is `senior-ai-governance-architect`-tier.** The analyst never edits the library from the crosswalk.
- **Five source-framework columns** — ISO/IEC 42001 clauses, NIST AI RMF sub-categories, EU AI Act articles, SR 11-7 pillars, internal policy catalogue references — plus optional overlays.
- **Eleven-column baseline row shape** — the crosswalk is a projection, not a duplicate of the library.
- **Four walks** — regulation-forward, control-forward, framework-forward, inventory-forward — compose to answer every question the auditor, the vendor-management office, and the regulator asks.
- **Four gap classes** — uncovered obligation, uncovered control, mis-anchored control, drift — become escalations, not silent fixes.
- **Cadence is event-driven** — regulatory-tracker changes and master-library revisions trigger the walk; the periodic cycle refreshes the *last verified* stamp.

## Summary

The analyst-tier controls crosswalk is a projection of the master control library onto five external / internal framework columns — ISO/IEC 42001 clauses, NIST AI RMF sub-categories, EU AI Act articles, SR 11-7 pillars, and the internal policy catalogue — plus optional overlays for sector-specific and voluntary references. The eleven-column row shape carries the control identifier, statement short-form, enterprise role, tier applicability, and the five framework anchors with a regulatory-tracker linkage and a last-verified date; it is a projection, not the library. Four walk patterns — regulation-forward, control-forward, framework-forward, inventory-forward — compose to answer every audit, vendor, and regulator question that the report and vendor row from chapters 03 and 06 do not answer directly. Four gap classes — uncovered obligation, uncovered control, mis-anchored control, drift — become escalation-register entries that the `senior-ai-governance-architect` resolves at library level; the analyst re-populates the crosswalk after each change. Chapter 08 turns to the two independent-audit / bias-auditor credential bodies the analyst most commonly encounters when reading vendor-independent-audit reports and enterprise-side external attestations.
