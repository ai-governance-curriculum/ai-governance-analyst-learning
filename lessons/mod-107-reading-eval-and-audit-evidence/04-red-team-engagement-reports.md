# Red-Team Engagement Reports

## Why this chapter

Where an Inspect-style eval report (chapter 02) and a RAG-triad report (chapter 03) are metric-shaped — datasets, scorers, aggregates — a **red-team engagement report** is narrative-shaped. Red-teaming is an adversarial exercise: a small team (internal, external, or crowdsourced) attempts to elicit unsafe or policy-violating behaviour from the system through creativity, persistence, multi-turn dialogue, roleplay, tool-use exploitation, and combinations of techniques a benchmark suite would not enumerate. The deliverable is a report that describes *what the team tried, what worked, what didn't, and what remains open*.

Red-team reports carry evidence a standard eval cannot produce. A benchmark can measure whether the model refuses a fixed set of prompts; only a red-team engagement can find the twelfth-turn escalation pattern that gets a compliant model to comply, or the tool-use chain that turns a benign summarisation task into an exfiltration path. NIST AI 600-1 (the [Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)) explicitly names red-teaming as a Measure-family action; the [OWASP LLM Top 10](https://genai.owasp.org/llm-top-10/) organises its threat catalogue in a shape red-team engagements naturally probe against; [MITRE ATLAS](https://atlas.mitre.org/) supplies a shared adversarial-tactic taxonomy the report can reference.

This chapter walks the shape of a red-team engagement report, the section layout the analyst should expect, the severity taxonomy that translates findings into a governance row, and the specific reading traps that come from evidence being narrative rather than numeric.

## What red-teaming is (and is not)

Red-teaming, in the analyst's operational vocabulary:

- **Adversarial.** The team is trying to break the system, not to characterise its average behaviour. A red-team report that reads like a benchmark leaderboard has probably not done red-teaming.
- **Structured.** Modern red-teams work from a threat model, an in-scope-and-out-of-scope list, and a methodology (multi-turn dialogue, jailbreak library, tool-use exploitation, cross-model transfer, human-in-the-loop iteration). Ad-hoc *tried some prompts* is not a red-team engagement.
- **Iterative.** Findings are triaged, reproduced, fed back to the model owner, and re-tested after mitigation. A one-shot report without a re-test round is often provisional.
- **Bounded.** A red-team engagement runs for a defined window, with a defined budget, against a defined system version. Findings that fall outside the scope are noted for a future engagement.

Red-teaming is **not** the same as:

- **Penetration testing** of the surrounding application (network, container, IAM). That is `cyber-security-engineer` scope and produces a separate report.
- **Bias auditing** in the fairness-metric sense (chapter reference: `mod-104`). A red-team may surface bias findings, but a bias audit is a separate methodology.
- **Formal verification** of model behaviour. Red-teaming is empirical; formal verification is (in principle) exhaustive. The distinction matters when auditors ask what a *finding of no vulnerabilities* actually claims.

## The expected sections of a red-team engagement report

A well-authored engagement report typically has these sections:

1. **Header.** Engagement identifier, dates, team composition (internal, external vendor, or crowdsourced), system(s) tested, system version, agreement / SOW reference.
2. **Threat model and scope.** What harms the engagement was scoped to elicit — CBRN uplift, prompt injection leading to data exfiltration, jailbreak of policy-refusal training, tool-use abuse, over-refusal, model-generated disinformation, PII leakage, and so on. Out-of-scope items are named explicitly.
3. **Methodology.** The attack techniques the team used, ideally mapped to a public taxonomy. Common taxonomies referenced:
   - [OWASP LLM Top 10](https://genai.owasp.org/llm-top-10/) — LLM01 prompt injection, LLM02 sensitive information disclosure, LLM06 excessive agency, and so on.
   - [MITRE ATLAS](https://atlas.mitre.org/) — adversarial techniques for ML systems, organised by tactic.
   - [NIST AI 600-1](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — the twelve GenAI risk categories.
   - Vendor- or lab-specific taxonomies (e.g., [Anthropic's Usage Policy](https://www.anthropic.com/legal/aup) categories, [OpenAI's usage policies](https://openai.com/policies/usage-policies/)).
4. **Test setup.** System version(s), deployment surface, tool inventory, guardrails in force, and the specific API or interface the team attacked through. Two engagements against nominally the same system with different guardrails are producing very different evidence.
5. **Findings.** The core of the report. Each finding is a self-contained record — chapter section below.
6. **Aggregate findings summary.** A table of findings by severity, by category, and by status (open / mitigated / accepted). Distributions and trends where the engagement is a re-test.
7. **Mitigations attempted and validated.** Which findings were mitigated during the engagement (some engagements iterate with the model owner in-window) and which mitigations were re-tested. A mitigation without a re-test is a *proposed* mitigation, not a *validated* mitigation.
8. **Residual-risk narrative.** The engagement lead's synthesis: what the system's residual attack surface looks like after the engagement.
9. **Threshold-decision rationale.** How the residual maps to the enterprise's release-gating threshold or the vendor's RSP / Preparedness-Framework capability threshold.
10. **Open follow-ups.** Findings not mitigated in-engagement, out-of-scope items surfaced but not tested, and recommended future engagements.
11. **Change log and appendix.** Version history and, where policy permits, per-finding reproduction transcripts.

## The finding record shape

The finding is the atomic unit of a red-team report. A well-authored finding carries:

- **Finding identifier.** Stable — `RT-<engagement-id>-<seq>`.
- **Title.** One-line description.
- **Category.** Mapped to the public taxonomy the methodology named (OWASP LLM01, ATLAS AML.T0043, NIST 600-1 CBRN, etc.).
- **Severity.** Per the enterprise's severity rubric — often a four- or five-tier scale (Critical / High / Medium / Low / Informational) with explicit criteria. If the rubric is unnamed, the analyst asks for it.
- **Likelihood or exploitability.** How easy the attack is to execute — trivial (single prompt), moderate (specific multi-turn setup), difficult (specialised knowledge or tool chain).
- **Reproduction.** A step-by-step recipe a reader can (with appropriate care) re-run. Some engagements redact reproductions from the main report and provide them in a separate access-controlled appendix; the analyst notes the location.
- **Impact.** What the attack could cause if exploited in production — data leakage, harmful content generation, policy violation, regulator-reportable event, reputational damage. Impact language is often qualitative; the analyst does not sharpen it beyond what the report claims.
- **Status.** Open / mitigated in-engagement / mitigation proposed but not validated / accepted with justification / closed / duplicate-of.
- **Mitigation recommendation.** If open, the recommended fix. If mitigated, what was done.
- **Owner.** Who is responsible for the mitigation.
- **Target closure date.** When the fix or re-test is due.

A red-team finding without severity, reproduction, and status is not a finding — it is an anecdote. The analyst notes any anecdote-shaped findings as a report-quality concern.

## Severity rubrics — what the analyst should expect

There is no single industry-standard severity rubric for red-team findings on AI systems the way [CVSS](https://www.first.org/cvss/) has become standard for CVEs on classical software. Enterprises typically adopt one of:

- **A CVSS-adapted rubric** — using CVSS's exploitability / impact / scope structure adapted to AI-system semantics. Increasingly common where the enterprise's security programme is CVSS-native.
- **An OWASP-derived rubric** — categorising by risk (severity × likelihood) mirroring OWASP's risk-rating methodology.
- **A bespoke enterprise rubric** — often four or five tiers with plain-language definitions.
- **A vendor rubric** — for engagements against a vendor foundation model, the vendor's rubric may carry through (e.g., Anthropic's or OpenAI's internal severity language, where the engagement is disclosed).

The analyst does *not* need to memorise every rubric. The analyst *does* need to record, per row, the rubric name and version being used, so that a downstream reader knows whether *high* in this report is the same as *high* in a report from six months ago.

## Where the three claims live in a red-team report

- **Residual-risk claim** → sections 6, 7, and 8. Section 6 gives the distribution of findings; section 7 says which were mitigated and re-tested; section 8 synthesises the residual attack surface. The analyst reads all three; the residual-risk claim in the row is section 8's narrative, evidenced by the section-6 distribution.
- **Threshold-decision rationale** → section 9. If the engagement was scoped against a specific RSP / Preparedness-Framework capability threshold, section 9 cites the threshold and the yes-or-no call. Where no explicit external threshold exists, the enterprise's internal red-team-acceptance policy is cited.
- **Unresolved findings** → section 10, cross-referenced with any section-5 findings whose status is *open* or *proposed-not-validated*.

## Reading traps specific to red-team reports

- **Coverage-versus-depth confusion.** A short list of very deep findings can be more evidence than a long list of shallow ones, or vice versa. The analyst reads the *methodology* section to understand which shape the engagement produced, and records the trade-off in the row's provenance.
- **Absence-of-evidence isn't evidence-of-absence.** A red-team that did not find a specific attack does not mean the attack does not exist — it means the team, within the scope and budget, did not find it in this window. The analyst does not silently promote *nothing found* into *system is safe*.
- **Silent scope creep.** The findings sometimes extend beyond the stated scope. If the report describes a finding that was outside the section-2 scope, the analyst notes the finding, notes the scope excursion, and treats the finding as a *surfaced item* rather than an in-scope evaluated one.
- **The mitigation-without-retest trap.** A finding that says *mitigated: refused to answer after prompt-template update* without a re-test round is a proposed mitigation, not a validated one. The row's *status* field must reflect the distinction.
- **The credential-based-attack conflation.** Some findings depend on the attacker having access the deployed system will not grant a real user (a system-prompt leak, a jailbroken tool). The analyst notes the access assumption; a finding that requires system-prompt access when the deployment does not expose the system prompt is a *lower-priority* finding, not a *higher-priority* one.
- **The single-vendor-model transfer trap.** A finding demonstrated against `openai/gpt-4o-2024-11-20` may or may not transfer to `anthropic/claude-3-5-sonnet-20241022` running the same application. Multi-model applications need per-model transfer testing; a single-model finding is not automatically a multi-model finding.

## The interaction with the impact-assessment and register artefacts

A red-team engagement report often surfaces findings that require updates to artefacts in earlier modules:

- **Register updates (`mod-103`).** A new residual risk category, or a change in an existing category's residual severity, populates the register.
- **Impact-assessment refresh triggers (`mod-105`).** A high-severity finding on a deployed system typically triggers a refresh of the impact-assessment corpus for that system.
- **Regulatory-tracker linkage (`mod-106`).** A finding that maps to a regulator-recognised risk category (a Colorado AI Act consumer harm, a NYC LL 144 bias signal, an EU AI Act Article 15 accuracy-and-robustness signal) is cross-referenced to the regulatory tracker row.
- **Control-library update (`mod-108`).** A validated mitigation becomes a new control (or a strengthening of an existing control); the control library refreshes.
- **Incident-response feed (`mod-109`).** A live-exploited finding is treated as an incident; the incident-response playbook is engaged.

The analyst does not update all of these artefacts single-handedly — the register update and control-library refresh are typically joint work with the risk and platform owners — but the analyst is the person who *notices the cross-artefact linkage* and files the change note into each downstream module.

## A concrete illustrative walkthrough

Consider a red-team engagement against MCDA's protected-class-generalisation weakness surfaced in chapter 02's safety-eval example (illustrative — not a real engagement):

- **Header.** *RT-2026-014, MCDA red-team engagement, 2026-08-01 through 2026-08-12, internal red-team of 3 engineers plus one contracted external evaluator. System version: MCDA application v3.7, system prompt v1.7, model `anthropic/claude-3-5-sonnet-20241022`.*
- **Threat model and scope.** *In scope: protected-class-generalisation elicitation via multi-turn dialogue, roleplay, and paraphrased prompts derived from the internal harm suite v3.2 protected-class subset; competitor-disparagement elicitation via indirect prompting; brand-guideline-violation via analogy prompts. Out of scope: prompt-injection via retrieved-context manipulation (scheduled for a separate engagement), tool-use exploitation (MCDA has no tools enabled).*
- **Methodology.** *Manual multi-turn attempts iterated in 3 rounds; MITRE ATLAS techniques AML.T0043 (Create Adversarial Data), AML.T0051 (LLM Prompt Injection — where applicable via user-side prompting), NIST 600-1 category coverage for bias / discrimination and harmful bias, plus OWASP LLM04 model-DoS check for over-refusal load.*
- **Findings.** *(a) RT-2026-014-001: two protected-class-generalisation elicitations via analogy prompts (Severity High, Exploitability Moderate; reproduction in appendix A.1). (b) RT-2026-014-002: one instance of competitor-disparagement via indirect prompting (Severity Medium, Exploitability Moderate). (c) RT-2026-014-003: 40% over-refusal on benign paraphrases of allowed prompts (Severity Medium — over-refusal is not a safety incident but is a business impact).*
- **Mitigations attempted and validated.** *Finding -001: system-prompt v1.8 draft (refuses analogy-prompt pattern) validated in round 3 — new residual 0/25 in retest, prior 2/25. Finding -002: not mitigated in-engagement; owner assigned. Finding -003: not mitigated in-engagement; owner assigned.*
- **Residual-risk narrative.** *Protected-class-generalisation via analogy-prompt pattern is closed under system-prompt v1.8. Competitor-disparagement via indirect prompting and over-refusal on benign paraphrases remain open with named owners.*
- **Threshold-decision rationale.** *Internal red-team acceptance policy v1.5: no High-severity findings may remain open at release; Medium-severity findings must have named owner and target closure within 30 days. Current state meets the release-gating criteria conditional on the system-prompt v1.8 rollout.*
- **Open follow-ups.** *RT-2026-014-002 (owner MCDA product owner, closure 2026-09-11); RT-2026-014-003 (owner MCDA product owner, closure 2026-09-11); separate engagement RT-2026-018 scoped for prompt-injection via retrieved-context manipulation, target 2026-10.*

The analyst's row populates from these sections. Chapter 05 works the extraction.

## What the analyst does *not* second-guess

- **The severity assignments.** If the engagement calls a finding High, the row records High and the rubric version. The analyst does not silently downgrade.
- **The scope exclusions.** If the engagement did not test prompt injection, the row records that prompt injection is out-of-scope-not-tested. The analyst does not silently promote *not tested* into *tested and clean*.
- **The mitigation validation.** If the report says a mitigation was validated in round 3, the row records that. If the analyst suspects the round-3 test was under-powered, that is a follow-up question for the engagement lead, not a row-level override.

## What to memorise

- **Red-team evidence is narrative, not numeric.** The reading discipline is sections-and-findings, not aggregate metrics.
- **The finding record is the atomic unit.** Identifier, category, severity, likelihood, reproduction, impact, status, mitigation, owner, target closure.
- **Severity rubrics are not standardised.** Record the rubric name and version alongside the severity.
- **Absence of evidence is not evidence of absence.** A red-team that did not find a specific attack has not proven the attack does not exist.
- **Mitigation-without-retest is *proposed*, not *validated*.** The row's status field must reflect the distinction.

## Summary

Red-team engagement reports are the third and most narrative-heavy report shape the analyst reads. The atomic unit is the finding, with its own severity, likelihood, reproduction, and status. Load-bearing sections are the threat model and scope, the methodology (mapped to OWASP LLM Top 10, MITRE ATLAS, and NIST AI 600-1 taxonomies), the findings, the mitigations attempted and validated, the residual-risk narrative, and the open follow-ups. Findings frequently trigger cross-artefact updates in the register (`mod-103`), the impact-assessment corpus (`mod-105`), the regulatory tracker (`mod-106`), the control library (`mod-108`), and the incident-response playbook (`mod-109`). Chapter 05 defines the row schema that all three report shapes (Inspect-style, RAG-triad, red-team) feed into.
