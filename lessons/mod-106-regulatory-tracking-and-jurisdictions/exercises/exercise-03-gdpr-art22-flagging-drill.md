# Exercise 03 — GDPR Article 22 Flagging Drill

**Estimated effort:** 2 hours
**Grounding chapter:** [07 — Privacy Laws and the Flagging Discipline — GDPR Article 22, GDPR Article 35, CCPA/CPRA, and HIPAA](../07-privacy-law-flagging-discipline.md)

## Objective

Practise the analyst-tier flagging discipline for GDPR Article 22 across a set of small, deliberately-ambiguous inventory-row scenarios. Produce a flag block per scenario that names the inventory row, applies the three Article 22 tests (solely automated, legal effects, similarly significant effects) with a defensible read on each, and routes the question to the DPO — without crossing into a legal conclusion the analyst is not qualified to reach.

After this exercise you should be able to open a new intake questionnaire, read the system's decision-shape in five minutes, and produce a flag block that either raises Article 22 correctly or explains — with the tests cited — why the flag is not raised.

## Prerequisites

- Chapter 07 read; the three Article 22 tests, the WP 251 rev.01 *meaningful human involvement* threshold, the Article 22(2) exemption bases, and the *question, not conclusion* discipline fresh in memory.
- The [GDPR consolidated text](https://gdpr-info.eu/) open — you will cite Article 22 sub-paragraphs by number and Article 9 (special-category data) where relevant.
- The [Article 29 Working Party WP 251 rev.01 — Guidelines on Automated individual decision-making and Profiling](https://ec.europa.eu/newsroom/article29/items/612053) open — you will cite the meaningful-human-involvement framing verbatim.
- Chapter 07's example flag block (the MCDA-Benefits `INV-2026-0088` block near the end of the chapter) open as a shape reference — your outputs match that structure.
- The inventory rows from `mod-102` chapter 03 and the register entries from `mod-103` chapter 02 for context on the shape of the *counsel questions* field the flag lives in.

## Problem statement

The deliverable is one Markdown document — `mod-106-ex-03-article-22-flag-set.md` — containing **five** flag blocks, one per scenario below, plus a **cover section** at the head and a **reflection section** at the tail.

### The five scenarios

For each scenario, treat the description as the intake questionnaire you have received. The scenarios are deliberately ambiguous or under-specified in specific ways; your flag block acknowledges what is unclear and asks the DPO the right questions rather than filling in the gap yourself.

Feel free to invent inventory-row identifiers of the form `INV-2026-EX03-<01..05>` and system names that are clearly illustrative. Do not re-use MCDA / MCDA-Benefits for these scenarios; you want fresh systems that force fresh reading.

1. **Scenario 1 — Instant online loan decisioning for consumer credit under €5,000.** A retail-bank subsidiary deploys a model that produces an *approve / decline / refer to underwriter* output on consumer-credit applications up to €5,000. Roughly 60% of applications are auto-approved and roughly 15% are auto-declined without a human touching the file; the remaining 25% are referred to an underwriter who reviews the file and issues the final decision. The system is used for EU-resident applicants across four member states.

2. **Scenario 2 — Insurance premium tiering.** A life-insurance product uses an ML pricing engine to generate a *tier 1 / tier 2 / tier 3 / decline* premium band from the applicant's health questionnaire, medical-history extracts, and lifestyle data. The output is written to the customer's quote and displayed as *your indicative premium*; the applicant then completes an in-branch or telesales conversation with a human agent who explains the tier and offers a policy at the priced rate. The agent has no authority to change the tier.

3. **Scenario 3 — HR shortlist ranker for internal promotion candidates.** An enterprise deploys a model that ranks internal candidates for a promotion opportunity by projected fit against the target role. The hiring manager receives a ranked list; per stated policy the manager reads the top five files and interviews at least three. The final promotion decision is the manager's, ratified by the HR business partner. The tool is used across EU offices for EU-resident employees.

4. **Scenario 4 — Content moderation autonomous action on a social platform.** A user-generated-content platform deploys a moderation model that, at high confidence thresholds, autonomously removes posts and — on repeated violations — temporarily restricts a user's ability to post. A subset of removals are queued for human review, but the initial action (remove-and-restrict) happens automatically. The platform serves EU-resident users.

5. **Scenario 5 — Public-sector eligibility recommender with mandatory human sign-off.** A public housing authority deploys a model that recommends *eligible / ineligible / hold for further information* on rental-subsidy applications. Per statutory requirement, no eligibility decision is finalised without a caseworker reviewing the file and countersigning; the caseworker sees the model's recommendation, the underlying inputs, and the reasoning. Caseworker acceptance rate of the model's recommendation is approximately 82% based on the pilot evaluation. The authority operates in one EU member state.

### The flag-block structure — required for every scenario

Each flag block has the structure from chapter 07, extended for the drill:

- **Inventory row and system name.** `INV-2026-EX03-<n>` (`[illustrative-system-name]`). One-sentence recap of the deployment.
- **Test 1 — solely automated.** Your analyst-tier read on whether the decision is *solely* automated in the WP 251 sense. Explicitly cite what would make human involvement *meaningful* rather than rubber-stamp for this system, and state which side of that line the described workflow appears to sit. If the description is under-specified in a load-bearing way (e.g., in scenario 3 the *reads the top five files* policy is not the same as *modifies the ranking*), name the ambiguity.
- **Test 2 — legal effects.** Whether the decision produces legal effects. Cite the WP 251 examples where they help (cancellation of contract, denial of benefit, etc.).
- **Test 3 — similarly significant effects.** Whether the decision similarly significantly affects the person even in the absence of legal effect. Consider access-to-service, pricing-to-exclusion, reputational-impact.
- **Analyst-tier read.** Two-of-three-yes triggers the flag. State the count and — if the flag is raised — the counsel question. If the flag is *not* raised, state which test failed and why, so the reasoning is auditable.
- **Article 22(4) special-category-data check.** If special-category data (Article 9) is in scope, note it explicitly and raise the tighter Article 22(4) prohibition, which limits solely-automated decisions on special-category data to explicit consent or substantial public interest.
- **Counsel question — the flag itself.** The exact one-paragraph flag as it would sit in the inventory row's *counsel questions* field. Structured per chapter 07's model paragraph — inventory row, three-test outcomes, request for opinion, deployment date placeholder, and the *this flag does not constitute an analyst legal opinion* disclaimer.
- **Downstream artefact triggers.** If the flag is raised, name the specific downstream reviews the analyst also opens — an Article 35 DPIA under `mod-105` chapter 04's discipline (if not already open), a residual-risk revisit in the register, a review-triggers update in the canonical document, and the change-note ID reservation for the eventual DPO opinion returning.

### The cover section

At the head of the document, a short (five-to-ten-line) block:

- Document identifier, version, date, author.
- One paragraph on the drill's purpose and the *question, not conclusion* discipline.
- A single-line reminder that these are practice scenarios; nothing in this document is legal advice, and no scenario refers to a real deployment.

### The reflection section

At the tail of the document, a short (half-page) reflection:

- **Which scenario was hardest to flag correctly, and why.** Meaningful human involvement in scenario 3 (HR shortlist) is a common trap; the pricing engine in scenario 2 is another; you will discover others as you write.
- **What you would ask on the intake questionnaire next time** to disambiguate any load-bearing ambiguity you had to flag as *under-specified* in a scenario.
- **Which of the five scenarios you would additionally send to the DPO even if the strict two-of-three test does not fire** — the *when in doubt, flag* posture is defensible, but every flag consumes DPO time; state your default and defend it.

## Requirements

- **Every flag block applies all three tests explicitly.** Skipping the test with a *this is obviously not solely automated* is not the discipline; the discipline is to say *test 1 — solely automated — [read]; test 2 — legal effects — [read]; test 3 — similarly significant effects — [read]*, in that order, every time.
- **Every flag block cites WP 251 verbatim or by-reference on the meaningful-human-involvement threshold.** Rubber-stamp acceptance is not meaningful; a human whose role and training let them and — where warranted — do modify the outcome is meaningful. Name the standard and apply it.
- **Every flag block resolves the two-of-three count explicitly and names the outcome.** *Flag raised — two of three tests plausibly land yes* or *flag not raised — test 1 clearly negative on meaningful-human-review evidence*. Silent-on-outcome flag blocks are not deliverable.
- **Every flag is written as a question, not a conclusion.** *Requesting DPO opinion on whether Article 22 is engaged* — correct. *This system violates Article 22* — wrong and a career-limiting move; the analyst does not opine on statutory violation.
- **Every flag names the inventory row and cites the trigger.** No *this system might be a problem* language. `INV-2026-EX03-<n>` and the specific test outcomes.
- **Every raised flag names the downstream artefact triggers.** A flag that stops at *requesting DPO opinion* leaves the impact-assessment corpus stale; the analyst also opens the DPIA if not already open, updates the review-triggers list, and reserves the change-note ID.
- **Scenario 4 requires an explicit stop-and-think.** Autonomous content moderation is a rich Article 22 area and often engages the platform's Digital Services Act obligations as well; name the DSA cross-reference and route to counsel with the DPO — this is a *both* flag, not either.
- **Scenario 5 requires the meaningful-human-review test taken seriously.** A statutory-requirement countersignature is on stronger ground than an internal-policy caseworker review; state your read on the countersignature evidence, note the 82% acceptance-rate figure and what it implies about *effective* human review vs *nominal* human review, and defer the meaningful-involvement determination to the DPO.
- **No fabricated statutory sections, WP 251 quotations, or DPO opinions.** Every citation traces to the primary text; where a specific fact is unknown (e.g., which member state the housing authority operates in, the exact underwriter-referral rules on the loan decisioning) the flag names the ambiguity and asks the DPO the right question.

## Starter guidance

- Draft one flag block end-to-end before moving to the next. The pattern is repetitive on purpose — the muscle memory is what makes the discipline durable — but if you author all five test-1 sections, then all five test-2 sections, and so on, you will drift between scenarios and produce inconsistent-shape flag blocks.
- The scenario 1 loan-decisioning case is the archetypal Article 22 hit: solely automated on 75% of applications by construction, legal effects clear (denial of consumer credit), similarly significant effects clear. Two of three easily; three of three straightforwardly. Draft this one first to warm up.
- The scenario 2 insurance case is the *pricing-engine-with-human-in-the-workflow* trap. The human agent presents the price but has no authority to change the tier — is that meaningful involvement? WP 251 says the involvement must be able to modify the outcome to be meaningful; a human with no authority is a rubber stamp. Draft your read and cite the standard.
- The scenario 3 HR case is where the *meaningful review* threshold gets its full workout. A ranked list *substantially assists or replaces* the manager's discretionary decision-making — the NYC LL 144 framing, quoted from chapter 04, is a useful frame here — but Article 22's *solely* test is stricter. State whether the described managerial workflow crosses into *solely automated* under WP 251; note that the answer depends on evidence of the manager's actual review behaviour, not the written policy.
- The scenario 4 content-moderation case has two active hooks (Article 22 and the DSA). Do not conflate them in the flag block; the Article 22 flag stays on the WP 251 shape and adds a note that a parallel DSA-Article-14 or Article-27 question exists and is routed to counsel separately.
- The scenario 5 public-sector case is where the *meaningful review* standard is at its strongest — a statutorily-required countersignature, a caseworker seeing full inputs and reasoning — and where the *82% acceptance rate* nonetheless prompts the DPO to ask whether the review is in practice as substantive as it is in policy. Flag the question; do not answer it.
- Every flag block should be short. Four short paragraphs plus the counsel-question paragraph. The reader (the DPO) is time-constrained and the flag needs to be scannable in under a minute.

## Acceptance criteria

- `mod-106-ex-03-article-22-flag-set.md` with a cover section, five flag blocks (one per scenario), and a reflection section.
- Every flag block applies all three tests explicitly, cites WP 251 on meaningful human involvement, resolves the two-of-three count explicitly, and — if raised — reserves the downstream-artefact triggers.
- Every flag block is written as a question with the *this flag does not constitute an analyst legal opinion* disclaimer.
- Scenario 4's flag block includes a DSA cross-reference note routed to counsel in parallel.
- Scenario 5's flag block treats the statutory-countersignature and the 82% acceptance-rate evidence honestly and defers the *meaningful* determination to the DPO.
- The reflection section names the hardest scenario, the intake-questionnaire additions that would help, and the analyst's default flag-vs-do-not-flag posture with justification.
- No fabricated citations, no fabricated DPO opinions, no fabricated statutory language.

## Stretch goals

- **A pair-review round.** Swap your flag set with a colleague on the same track (or, solo, put the drill down for a day and re-read it fresh). For each flag block, note where the paired reader would push back on the test read; incorporate the pushback as a revision or an explicit *analyst held to original read because …* note.
- **A CCPA/CPRA-and-ADMT companion flag per scenario.** Where the scenario would also engage California-resident data subjects, write a short parallel flag applying the CPPA ADMT regulation shape from chapter 07. The pattern is the same (question not conclusion; name the inventory row; cite the trigger) with a different regulator counterpart.
- **An enterprise flag template.** Extract the shape common across your five flag blocks into a reusable `mod-106-ex-03-article-22-flag-template.md` template with prompts (`[analyst's read on solely-automated]`, `[analyst's read on legal effects]`, etc.). The template is what a colleague copies to write their first flag; you validate it works by re-authoring one of your five blocks from the template alone.
- **A meaningful-human-review evidence checklist.** For a system where you flagged *plausibly meaningful review, deferred to DPO*, list the specific evidence artefacts (training records, sampled-file reviews, override-rate statistics, decision-modification logs) that would convert *plausibly meaningful* into *demonstrably meaningful*. This is what the analyst asks for on the next revision of the intake questionnaire.
- **A cross-reference against the FRIA scoping filter.** For any scenario that is also an AI Act high-risk deployer case (scenarios 1, 3, and 5 are the strongest candidates), note the Article 27 FRIA scoping-filter outcome in a footnote to the flag block. This crosses back into `mod-105` chapter 03 and reinforces the shared-template discipline.

## Deliverables

- `mod-106-ex-03-article-22-flag-set.md` — the five-flag-block drill with cover and reflection sections.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference flag block per scenario in the shape above. Yours will differ in the specific test-read language and in the exact counsel questions raised. What should not differ is (a) every flag block applies all three tests explicitly, (b) WP 251 is cited on meaningful human involvement, (c) the two-of-three count is resolved explicitly, (d) every flag is written as a question, (e) downstream artefact triggers are reserved on raised flags, and (f) the scenario 4 DSA cross-reference and the scenario 5 statutory-countersignature nuance are both handled honestly. A short, disciplined flag block that correctly asks the DPO one specific question beats a paragraph of *this system probably violates GDPR* — the second is not a flag, it is an assertion the analyst is not qualified to make.
