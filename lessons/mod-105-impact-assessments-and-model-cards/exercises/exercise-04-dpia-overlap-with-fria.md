# Exercise 04 — DPIA Overlap With the FRIA

**Estimated effort:** 2 hours
**Grounding chapter:** [04 — The Data-Protection Impact Assessment — GDPR Article 35 and Its Overlap With the FRIA](../04-data-protection-impact-assessment-gdpr-article-35.md)

## Objective

Author a first-draft GDPR Article 35 DPIA for the same system for which you authored a FRIA in exercise 03, and build the explicit DPIA / FRIA overlap table that keeps the two artefacts consistent, cross-referenced, and free of duplication. The drill covers the Article 35 trigger, the WP 248 nine-criteria filter, the four required elements, the DPO consultation, the Article 36 prior-consultation flag, and — critically — the mechanical discipline that lets a reader walk from either document to the other without re-reading.

After this exercise you should be able to author a DPIA alongside a FRIA in the same authoring session, produce an overlap table that convinces the DPO and the AI governance owner they do not need to re-write each other's sections, and correctly raise the Article 36 flag when residual risk stays High.

## Prerequisites

- Chapter 04 read; the Article 35 trigger, the WP 248 filter, the four required elements, and the Article 36 mechanic fresh in memory.
- Exercise 03 completed — you have a FRIA on disk for a system that also processes personal data.
- The [GDPR consolidated text](https://gdpr-info.eu/) open — you will cite Article 6, Article 9 (if special-category data is in scope), Article 22 (if automated-decision-making with legal effects is a live concern), Article 30 (RoPA reference), Article 35, and Article 36 by article number.
- The [Article 29 Working Party WP 248 rev.01](https://ec.europa.eu/newsroom/article29/items/611236) open — you will apply the nine-criteria filter and cite the outcome.
- The [EDPB List of processing operations subject to the requirement of a data protection impact assessment](https://www.edpb.europa.eu/our-work-tools/general-guidance/gdpr-guidelines-recommendations-best-practices_en) and the relevant national supervisory-authority list (e.g., [CNIL for France](https://www.cnil.fr/en/deliberations/decision-2018-327), [BfDI for Germany](https://www.bfdi.bund.de/EN/Home/home_node.html), the [ICO for UK-GDPR](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/data-protection-impact-assessments-dpias/)) as jurisdictionally relevant.

## Problem statement

The deliverable is two Markdown files.

### Part 1 — the DPIA first draft

Author `mod-105-ex-04-dpia-<system>-draft.md` for the same system used in exercise 03.

At the head:

- The cross-reference block from chapter 08 (canonical document ID, register entries, FRIA ID, related model card, related datasheet, DPO opinion reference).
- A **DPIA-trigger narrative** — three to six sentences — that applies the Article 35(1) general test, the Article 35(3)(a)/(b)/(c) always-required cases, and the WP 248 nine-criteria filter to your system, cited to the source. This is the analyst's answer to *why does this system need a DPIA*.

Cover every one of the four Article 35(7) required elements, each labelled with the sub-article citation:

- **(a) Systematic description of the envisaged processing operations and the purposes.** From the canonical System description + Data description.
- **(b) Assessment of necessity and proportionality.** Author net-new — this is the most rewritten DPIA section. Answer *why the personal data processing is required to achieve the stated purpose* and *why the processing is limited to what is required*. Cite the Article 6 (and Article 9 where applicable) lawful basis.
- **(c) Assessment of the risks to the rights and freedoms of data subjects.** From the canonical register entries touching personal data; project only the personal-data-relevant subset here (the FRIA covers the broader Charter scope).
- **(d) Measures envisaged to address the risks.** From the canonical Treatment plan. Include the residual claim per risk after mitigation.

Add a **DPO consultation record** — a short block naming the DPO consulted, date, and the DPO's opinion (attached by reference).

Add an **Article 36 prior-consultation determination** — a short block that says *residuals reviewed; no High residuals after mitigation; Article 36 prior consultation not triggered* or *residual RR-XXX-XXXX remains High after mitigation; Article 36 prior consultation triggered; pending supervisory-authority engagement*. Do not skip.

### Part 2 — the DPIA / FRIA overlap table

Author `mod-105-ex-04-dpia-fria-overlap-<system>.md` — a short document (one page) that contains:

- A cross-reference block at the head with the DPIA ID and the FRIA ID.
- The overlap table from chapter 04, populated for your specific system. Rows are concerns (data protection Article 8, non-discrimination Article 21, human oversight, Article 13 provider-info dependency, market-surveillance-authority notification, prior-consultation-with-supervisory-authority, retention and international-transfer, etc.). Columns are *DPIA covers* / *FRIA covers* / *both cover — cited by reference* / *neither covers — flagged*.
- A **duplication-and-drift check.** For each concern where both cover, name the specific section in each document that carries the load-bearing content and specify which is the source-of-truth (i.e., which document is amended first when the underlying fact changes). No overlap row is *both cover with duplicated wording*; that would be a drift-in-waiting.
- A **routing note** — one paragraph on who reviews what: the DPO on the DPIA, the AI governance owner or senior AI governance architect on the FRIA, counsel on both, and the joint-review moment (typically a single meeting) where they reconcile.

## Requirements

- **The DPIA-trigger narrative is applied at the head.** A DPIA does not exist without the trigger answered and cited. If the WP 248 filter yields zero-or-one criteria, the deliverable becomes a trigger-negative memo, not a DPIA.
- **Every Article 35(7) element is present**, in order, with sub-article citations.
- **The necessity-and-proportionality section is genuinely authored.** It is the DPIA's most-often-thin section. Requirement: at least two paragraphs, one on necessity, one on proportionality, each with a cited lawful-basis reference (Article 6(1)(a) consent, (b) contract, (c) legal obligation, (d) vital interests, (e) public task, or (f) legitimate interests; plus Article 9(2) basis if applicable).
- **Every risk in element (c) is scoped to personal-data impact.** The FRIA covers the broader Charter scope; the DPIA does not duplicate. Where a risk in the register engages both data-protection and other Charter rights, the DPIA cites the FRIA for the non-data-protection Charter framing rather than restating.
- **The DPO consultation record carries a date and an opinion reference.** No date or unresolved opinion = not a record.
- **The Article 36 determination is explicit, not implicit.** *Not triggered* is a valid answer; *silent* is not.
- **The overlap table has no *both-covers-with-duplicated-wording* rows.** Every overlap row names the source-of-truth document and lets the other cite by reference.
- **Nothing is fabricated** — no invented supervisory-authority correspondence, no fake DPO name, no fake internal ticket IDs, no made-up national-supervisory-authority-list entry.
- **No unresolved `<!-- needs-research: -->` markers in the DPIA body** — either the fact is researched, or the draft is marked *pending resolution* and the blocker named at the head.

## Starter guidance

- Author the DPIA-trigger narrative first, then the four elements, then the DPO consultation record and Article 36 determination, then the overlap table. Trying to author overlap before you have both artefacts leads to guessing at coverage.
- The necessity-and-proportionality section is where first-draft DPIAs are shallowest. A trick that helps: for necessity, answer *what less-privacy-invasive alternative was considered and why was it rejected*; for proportionality, answer *what specific data field was minimised or dropped and why is the remaining processing sufficient*.
- On the Article 22 flag: if your system's decision, taken by the system alone without meaningful human review, produces legal or similarly significant effects, Article 22 is a live concern and the DPIA cites it explicitly. If your system's decisions all pass through meaningful human review, note that Article 22 is not engaged and cite the FRIA's human-oversight section as evidence.
- The overlap table is easier if you author the FRIA and the DPIA back-to-back in one session. Concerns that appear in both are cross-referenced; concerns that appear only in one are stable. If you author the two documents weeks apart, plan a joint-review moment to build the overlap table.
- Residual High after mitigation is the trigger for the Article 36 flag. Do not tune residuals down to avoid the trigger; if the enterprise cannot mitigate below High, that is the enterprise's honest state and the flag is correct.
- The DPO opinion is attached by reference in the DPIA. The DPO's actual opinion is a live human artefact — for this exercise, treat the reference as a placeholder ID (`DPO-OPN-<system>-<date>`) and note in the retrospective that the actual DPO consultation is out of scope for a solo exercise.

## Acceptance criteria

- `mod-105-ex-04-dpia-<system>-draft.md` with the cross-reference block, DPIA-trigger narrative, four Article 35(7) elements populated with sub-article citations, DPO consultation record, and Article 36 determination.
- The necessity-and-proportionality section carries at least two paragraphs (one on necessity, one on proportionality) and cites the Article 6 (and Article 9 if applicable) lawful basis.
- Every risk in element (c) is scoped to personal-data impact; broader Charter-rights framing is cited to the FRIA.
- `mod-105-ex-04-dpia-fria-overlap-<system>.md` with the cross-reference block, populated overlap table, duplication-and-drift check, and routing note.
- Every overlap row names a source-of-truth document; no duplicated-wording rows.
- No fabricated correspondence, opinions, or supervisory-authority entries.
- No unresolved research markers in the DPIA body.

## Stretch goals

- **A lawful-basis decision worksheet.** For your system, walk each Article 6(1) lawful basis and record why each is or is not the basis you are relying on. The DPIA cites the chosen basis; the worksheet is the reasoning. Add Article 9(2) if applicable.
- **A cross-jurisdictional supervisory-authority scan.** If the enterprise processes personal data across multiple EU member states, list which national supervisory authority is the lead under Article 56 GDPR (one-stop-shop mechanism) and any other supervisory authorities the DPIA needs to be filed with. Route back to `mod-106` where jurisdictional tracking lives.
- **An Article 22 sub-memo.** If Article 22 is live for your system, author a short (one-page) memo on the Article 22(2) exemptions the enterprise is relying on, the Article 22(3) safeguards in place, and the residual data-subject rights (obtain human intervention, express point of view, contest the decision).
- **A DPIA-to-RoPA-to-model-card walk.** Author a short walk showing that the Record of Processing Activities (Article 30) entry, the DPIA, and the model card all cite each other consistently. This is the personal-data slice of the walk discipline from chapter 08.
- **A revocation-of-consent handling note.** If Article 6(1)(a) consent is your lawful basis (rare in AI system contexts), author a short note on the enterprise's mechanism for handling consent withdrawal and its impact on stored inference results.

## Deliverables

- `mod-105-ex-04-dpia-<system>-draft.md` — the DPIA first draft.
- `mod-105-ex-04-dpia-fria-overlap-<system>.md` — the overlap table and routing note.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference draft against the MCDA-Benefits variant used in exercise 03. Yours will differ in the specific lawful-basis reasoning and mitigation content; what should not differ is (a) the DPIA-trigger narrative is applied and cited, (b) all four Article 35(7) elements are present, (c) necessity-and-proportionality is genuinely authored not perfunctory, (d) the Article 36 determination is explicit, (e) the overlap table has a named source-of-truth per row and no duplicated-wording rows. A cleanly-scoped DPIA that correctly triggers the Article 36 flag beats a longer one that quietly avoids the flag by trimming residuals.
