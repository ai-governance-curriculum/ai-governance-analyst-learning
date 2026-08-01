# Voluntary Codes — The EU AI Office General-Purpose AI Code of Practice

## Why this chapter

The tracker holds *regulations* — instruments that carry legal obligation. But an analyst also needs to read and understand *voluntary codes* — instruments that do not carry direct legal obligation but that anticipate regulator expectations, signal the enterprise's compliance posture to counterparties, or provide a safe harbour that the analyst's counsel can rely on when a new obligation lands.

The load-bearing example of an AI voluntary code is the [EU AI Office General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice). Published under Article 56 of the AI Act, it is the voluntary compliance route the AI Office maintains for providers of general-purpose AI (GPAI) models — the code is not the regulation, but adherence to it creates a presumption of compliance with the corresponding Article 53 and Article 55 obligations for GPAI-model providers.

This chapter walks the GPAI Code of Practice as the anchor example: what a voluntary code *is*, how the code interacts with the underlying regulation, what the tracker records about a voluntary code, and how the analyst reads a voluntary code as anticipatory intelligence for what the enforcing authority will want to see. The chapter treats the GPAI code as the specific case; the reading pattern generalises to other voluntary codes (industry codes of conduct, NIST profiles that vendors adopt voluntarily, sector-specific codes maintained by trade associations, and so on).

## What a voluntary code is

A voluntary code is an instrument to which:

- **Adherence is not compelled by law.** An entity that chooses not to adhere does not, by that fact alone, violate any law.
- **Adherence is documented.** The code has signatories, adopters, or endorsers — a public list — or an in-scope declaration that the enterprise adopts.
- **Adherence produces evidence.** Adopters commit to specific obligations that they will document, publish, or attest to; that evidence is what the enterprise's counterparties, regulators, or auditors read.

Voluntary codes exist for two structural reasons:

- **Anticipating regulation.** A well-crafted voluntary code articulates what practitioners collectively believe the enforcing authority will want to see. Adopting the code early positions the enterprise to be *already-compliant* when the regulator's expectations are codified.
- **Filling a gap.** Some obligations do not lend themselves to formal regulation — the technical detail moves too fast, or the appropriate scope is trans-jurisdictional. A voluntary code can codify shared practice without the regulatory-instrument overhead.

The GPAI Code of Practice is the former — it articulates the AI Office's expectations for the Chapter V obligations on providers of GPAI models, ahead of any Commission delegated act that might codify the same requirements.

## The GPAI Code of Practice — what it is and how it interacts with the AI Act

The [GPAI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice) was finalised through a multi-stakeholder drafting process convened by the AI Office and involving GPAI-model providers, deployers, civil society, academic experts, and Member State observers. The [final version was published by the AI Office](https://digital-strategy.ec.europa.eu/en/library/final-general-purpose-ai-code-practice) in July 2025, ahead of the 2 August 2025 date on which Chapter V obligations applied.

<!-- needs-research: verify the current published version of the GPAI Code of Practice at the [AI Office code-of-practice page](https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice), including any updates, the list of signatories or adherents at date of tracker refresh, and the operational text of the code's chapters (transparency, copyright, and safety-and-security-for-systemic-risk-model chapters). The AI Office indicated a periodic review cadence. -->

The Code is organised into three chapters that map to the underlying AI Act obligations:

- **Transparency chapter.** Maps to Article 53(1)(a) and (b) — the obligation on GPAI providers to draw up and maintain technical documentation of the model and to provide information to downstream deployers. The chapter operationalises what the technical documentation and downstream-provider information should contain, in a common template shape.
- **Copyright chapter.** Maps to Article 53(1)(c) and (d) — the obligation to put in place a policy to comply with EU copyright law and to publish a sufficiently detailed summary of training-data content. The chapter operationalises the training-data-summary template and the copyright-policy expectations.
- **Safety and security chapter.** Applies to providers of GPAI models with systemic risk (Article 51 designation). Maps to Article 55 — additional obligations on providers of GPAI with systemic risk, including model evaluation, adversarial testing, tracking and reporting serious incidents, and cybersecurity protection. The chapter operationalises the safety-and-security framework a systemic-risk-model provider maintains.

Chapter V of the AI Act (Articles 51–56) applies from 2 August 2025. The Code of Practice's role, per Article 56(1) and (5), is that adherence *contributes to demonstrating compliance*. An adopter can be presumed to comply with the corresponding obligations to the extent it complies with the Code. A non-adopter is not presumed non-compliant — it just carries a heavier evidentiary burden of showing that its own compliance approach meets Article 53 or Article 55 obligations directly.

## How the tracker treats the Code of Practice

The tracker holds the Code as a row in the sector-agnostic *EU* branch, alongside the AI Act rows from chapter 02:

- **Row.** `REG-2026-EU-010` — EU AI Office GPAI Code of Practice.
- **Status.** *Voluntary code — published July 2025. Applies alongside Article 53 (all GPAI providers) and Article 55 (systemic-risk-model providers) obligations that took effect 2 August 2025.*
- **Instrument.** [Final GPAI Code of Practice — AI Office](https://digital-strategy.ec.europa.eu/en/library/final-general-purpose-ai-code-practice).
- **Scope trigger.** Enterprise is a provider of a general-purpose AI model (as defined at Article 3(63) and elaborated at Article 51 for systemic-risk designation).
- **Role.** Provider of GPAI model.
- **Enforcement authority.** Adherence is voluntary; the AI Office maintains the code and its adopter list. Underlying Article 53 and Article 55 obligations are enforced by the AI Office at Union level with Member State supervisory-authority participation per Article 88.
- **Affected inventory rows.** The enterprise's GPAI-model inventory rows, if any. Where the enterprise is not a GPAI-model provider — the typical enterprise-analyst case, since most enterprises are GPAI-model *deployers* rather than *providers* — the row's affected-inventory-rows list is empty and the analyst notes *no in-scope systems; retained for horizon-scan and for deployer-side reading (a provider's Code adherence informs the deployer's Article 26 obligations)*.
- **Related obligations.** `REG-2026-EU-002` (AI Act Article 6 + Annex III), `REG-2026-EU-005` (Chapter V GPAI base row).
- **AIGP body-of-knowledge tag.** Domain 4 (existing and emerging AI laws and standards); secondary Domain 5 (AI development life cycle) for the safety-and-security chapter.
- **Last-verified date.** Refreshed on monthly deep read; check the AI Office page for updates or an updated adopter list.
- **Notes for counsel.** *Adherence decision — routed to AI governance owner and general counsel. Where the enterprise is a deployer of an in-scope model, read the model provider's Code adherence documentation as an input to the enterprise's Article 26 deployer obligations and to the enterprise's vendor-review evidence (`mod-105` chapter 06's vendor-supplement pattern).*

## How the analyst reads a voluntary code

The Code is a document, not a database. The analyst-tier reading pattern:

1. **Read the underlying regulation first.** The Code operationalises Article 53 and Article 55; without a working grasp of those articles, the Code reads as arbitrary. `mod-105` chapter 03 walks Article 27; the same reading discipline applies to Chapter V.
2. **Read the Code by chapter, matched to the operational area.** Transparency chapter is read by the analyst / documentation lead / model card team. Copyright chapter is read by the analyst / IP counsel / data-governance lead. Safety and security chapter is read by the analyst / ML safety lead / CISO — most enterprises do not have systemic-risk-designated models, so the safety chapter is often only skimmed.
3. **Extract the operational templates.** The Code's transparency chapter includes template shapes for the technical documentation and downstream-deployer information; the copyright chapter includes a template for the training-data summary. The analyst records the templates in the enterprise governance-artefact library and — where the enterprise adopts the Code — populates them for the specific model.
4. **Note the drift risks.** The Code is periodically revised; the analyst's tracker row includes the version of the Code that was current at the enterprise's adherence decision, and the monthly deep read compares the current AI Office publication to the version-of-record.
5. **Do not opine on adherence.** The decision to adopt the Code is a business-and-legal decision — the analyst frames the trade-off (compliance evidentiary weight vs adherence overhead) and routes to the governance owner and general counsel.

## Other voluntary codes the analyst tracks

The GPAI Code is the anchor example. Other voluntary codes the tracker may carry as separate rows depending on the enterprise's shape:

- **[US Voluntary AI Commitments](https://www.whitehouse.gov/briefing-room/statements-releases/2023/07/21/fact-sheet-biden-harris-administration-secures-voluntary-commitments-from-leading-artificial-intelligence-companies-to-manage-the-risks-posed-by-ai/)** — commitments made by leading US AI companies in 2023 on safety, security, and trust. Non-binding; adherence is public. Historical significance — the US EO stack has changed since (chapter 03) and the commitments' role has shifted; verify current relevance.
- **[Frontier Model Forum](https://www.frontiermodelforum.org/)** commitments — voluntary industry body of leading frontier-model developers with published commitments on safety practice.
- **[Partnership on AI](https://partnershiponai.org/)** codes and shared practices — trans-industry commitments on specific practice areas (deepfake provenance, synthetic-media disclosure).
- **NIST Generative AI Profile as a voluntary adoption** — the [NIST AI 600-1 GenAI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) is a framework, not a code, but many enterprises adopt it voluntarily as a self-attested standard.
- **[C2PA (Coalition for Content Provenance and Authenticity)](https://c2pa.org/)** technical standard adoption — voluntary industry standard for content provenance, adopted by media platforms and content-generation tools.
- **Sector-specific industry codes** — pharmaceutical trade-association AI codes, financial-services industry AI codes, insurance industry AI codes as they emerge.

Each is a row in the tracker with the same field shape as the GPAI Code — voluntary status, scope trigger, role, enforcement (typically self-attested with public documentation), affected inventory rows, and the anticipation-of-regulation note that lets the analyst read the code as advance intelligence.

## The trade-off — why the enterprise may or may not adopt

The adherence decision is a governance-owner + counsel decision. Analyst-tier framing of the trade-off:

**Adopt when:**
- The Code articulates practice the enterprise is already doing at scale — adherence is a modest overhead on top of existing evidence and produces external-facing recognition.
- The enterprise wants to signal *this is our compliance posture* to enterprise customers, sovereign buyers, or investors.
- The Code's evidentiary weight in an enforcement or supervisory-review posture materially reduces exposure — the AI Act Article 53/55 presumption from Code adherence is a specific case.

**Do not adopt (yet) when:**
- The Code is still in a settling phase — early revisions may reshape obligations and re-set the enterprise's evidentiary posture.
- The Code covers practice areas the enterprise does not do at scale — adherence would create a discovery risk on gaps unrelated to the enterprise's actual operations.
- The enterprise's counsel prefers direct-to-regulation compliance evidence over a code-mediated presumption, on the grounds that the code's revision cycle introduces its own compliance overhead.

The analyst does not decide. The analyst notes the trade-off, the Code's current stability, and the enterprise's operational fit, and routes to the governance owner and counsel.

## Where the voluntary-codes tracking stops for the analyst

- **Not the enterprise's adherence decision.** The analyst frames; counsel and the governance owner decide.
- **Not a substitute for reading the underlying regulation.** The Code is a lens on the regulation; the regulation is the obligation.
- **Not a marketing claim.** The tracker records whether the enterprise has adopted; whether the enterprise *advertises* adoption externally is a marketing-and-communications decision.
- **Not a legal opinion on the presumption of compliance.** Article 56(5)'s presumption is a legal question — the analyst records that the Code exists and that adherence contributes to compliance evidence; counsel opines on the strength of the presumption in the enterprise's specific case.

## What to memorise

- **Voluntary codes are anticipatory intelligence.** They articulate what practitioners collectively believe the enforcing authority will want to see; adopting the code early positions the enterprise to be already-compliant.
- **The GPAI Code of Practice is the AI Office's voluntary compliance route for Article 53 and Article 55.** Three chapters — transparency, copyright, and safety-and-security-for-systemic-risk-models. Adherence contributes to Article 56 presumption of compliance.
- **The tracker treats a voluntary code as a row with the same field shape as a regulation row.** Status is *voluntary code*; the affected-inventory-rows list may be empty for the typical enterprise deployer.
- **Read the underlying regulation first, then the code.** The Code operationalises the regulation; without the regulation, the Code is arbitrary.
- **The adherence decision is not the analyst's.** Frame the trade-off, route to the governance owner and counsel.
- **Other voluntary instruments — Frontier Model Forum, NIST profiles adopted voluntarily, C2PA, sector-specific industry codes — get the same tracker-row treatment.**

## Summary

Voluntary codes are the anticipatory-intelligence layer of the regulatory landscape — instruments that do not carry direct legal obligation but that articulate what practitioners collectively believe the enforcing authority will want to see. The EU AI Office GPAI Code of Practice is the anchor example: three chapters (transparency, copyright, safety and security) that operationalise the Article 53 and Article 55 obligations on providers of general-purpose AI models, with Article 56 establishing that adherence contributes to a presumption of compliance. The tracker treats the Code as a row with the same field shape as a regulation row, tagged with the AIGP body-of-knowledge domain, refreshed monthly, and routed to the governance owner and general counsel for the adherence decision. The reading pattern generalises: voluntary codes are read by chapter, matched to enterprise operational areas, and their templates are extracted to the enterprise's governance-artefact library. Chapter 10 closes the module with the regulatory-change-note that turns any tracker update — regulation or voluntary code — into routed action across the affected system owners.
