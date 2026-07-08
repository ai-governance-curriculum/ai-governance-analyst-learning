# The International Values Baseline — OECD, Council of Europe, and UNESCO

## Why this chapter

The NIST AI RMF, ISO/IEC 42001, and the EU AI Act give you the *how*: functions, clauses, tiers, obligations. They do not, on their own, tell an enterprise what it *stands for* — the values statement its Responsible AI policy commits to.

Three international instruments do that work at a level enterprises are expected to *not* undercut:

- The **OECD AI Principles** — the most-cited, adopted 2019 and updated 2024, endorsed by ~50 countries.
- The **Council of Europe Framework Convention on AI, Human Rights, Democracy and the Rule of Law** — the first *legally binding* international treaty on AI, opened for signature September 2024.
- The **UNESCO Recommendation on the Ethics of AI** — adopted by 193 UNESCO member states in November 2021, the broadest international consensus text.

You do not have to memorise every clause of these. You have to know they exist, roughly what they say, and — for the analyst — that they define the *floor* the enterprise's AI policy should sit on top of. When the head of AI governance drafts the enterprise Responsible AI Policy (`mod-110`), one of the sanity checks is: does this policy commit to anything *less* than what OECD, CoE, or UNESCO already committed the country to? If yes, the policy is publicly indefensible.

## OECD AI Principles

The [OECD AI Principles](https://oecd.ai/en/ai-principles) were the first intergovernmental standard on AI, adopted in May 2019 and updated in May 2024. They anchor the [OECD.AI Policy Observatory](https://oecd.ai/) and were the direct scaffold for the [G20 AI Principles (2019)](https://oecd.ai/en/dashboards/countries/G20). They are non-binding — soft law — but function as the default reference the rest of the ecosystem cites back to.

**The five value-based principles**

1. **Inclusive growth, sustainable development and well-being** — AI should benefit people and the planet, reduce inequalities, and be aligned with sustainable-development objectives.
2. **Human rights and democratic values, including fairness and privacy** — AI systems should respect the rule of law, human rights, democratic values, and diversity; include appropriate safeguards; and offer meaningful human oversight when needed.
3. **Transparency and explainability** — Actors should provide meaningful information appropriate to the context so that people can understand and challenge AI outcomes.
4. **Robustness, security and safety** — AI systems should function robustly and securely throughout their life cycle, and risks should be continually assessed and managed.
5. **Accountability** — AI actors should be accountable for the proper functioning of AI systems and for the respect of the above principles, based on their roles and applicable context.

**The five recommendations to governments** — these are directed at states, not enterprises, but they shape the regulatory environment your employer operates in.

1. Investing in AI research and development.
2. Fostering an inclusive AI-enabling ecosystem (data, infrastructure, standards).
3. Shaping an enabling interoperable governance and policy environment.
4. Building human capacity and preparing for labour-market transitions.
5. International co-operation for trustworthy AI.

**Analyst uptake.** The OECD's five value-based principles are the shortest defensible statement of what an enterprise Responsible AI Policy commits to. Most large-enterprise AI policies published in 2024–2026 read as OECD paraphrases with sector-specific overlays.

## Council of Europe Framework Convention on AI

The [Council of Europe Framework Convention on Artificial Intelligence and Human Rights, Democracy and the Rule of Law](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence) — often called the "Framework Convention on AI" or "CETS 225" — was adopted May 2024 and opened for signature in Vilnius on 5 September 2024. It is the **first legally binding international treaty on AI**.

Its scope is public-sector AI activities and, at a minimum, the private-sector activities parties choose to bring in. It does not preempt the EU AI Act; it sits above it as a human-rights baseline.

The Convention obligates parties to ensure AI activities are consistent with:

- **Human dignity and individual autonomy.**
- **Equality and non-discrimination**, including gender equality.
- **Respect for privacy and personal data protection.**
- **Transparency and oversight**, tailored to context.
- **Accountability and responsibility**, with effective remedies.
- **Reliability** of AI systems.
- **Safe innovation**, including controlled testing environments.

It also requires parties to establish risk-and-impact management frameworks, ensure procedural safeguards (documentation, notification, effective remedies), and provide for oversight mechanisms. Analyst uptake: the Convention gives you the *rights baseline* — the enterprise Responsible AI Policy should commit at least to these; anything less will not survive a public-facing review.

<!-- needs-research: verify the current list of signatories and states that have ratified the Framework Convention before citing specific national commitments in any external-facing document; the signatory list has been updating since September 2024. -->

## UNESCO Recommendation on the Ethics of AI

The [UNESCO Recommendation on the Ethics of Artificial Intelligence](https://www.unesco.org/en/artificial-intelligence/recommendation-ethics) was adopted by all 193 UNESCO Member States in November 2021 at the 41st General Conference. It is the broadest international consensus text on AI ethics and — unlike the CoE Convention — is a *recommendation* (not a treaty).

Structurally, the Recommendation is organised into:

- **Values** — respect, protection and promotion of human rights and human dignity; environment and ecosystem flourishing; ensuring diversity and inclusiveness; living in peaceful, just and interconnected societies.
- **Principles** — proportionality and do-no-harm; safety and security; fairness and non-discrimination; sustainability; right to privacy and data protection; human oversight and determination; transparency and explainability; responsibility and accountability; awareness and literacy; multi-stakeholder and adaptive governance and collaboration.
- **Policy Action Areas** — eleven areas including ethical impact assessment, ethical governance and stewardship, data policy, development and international cooperation, environment and ecosystems, gender, culture, education and research, communication and information, economy and labour, health and social well-being.

**Two things worth internalising**

- The Recommendation explicitly puts an **environmental** anchor into the values statement (sustainability, environment and ecosystems). This is the strongest single instrument connecting AI governance to environmental responsibility, and it maps to NIST AI 600-1 risk #5 (Environmental Impacts).
- The Recommendation introduces **Ethical Impact Assessment (EIA)** and **Readiness Assessment Methodology (RAM)** as concrete instruments states are expected to adopt. Enterprise programmes sometimes reuse the EIA scaffold — worth knowing the name.

**Analyst uptake.** UNESCO is where you point when someone asks "what is the *broadest* international consensus we should not undercut?" 193 states agreed to it, which is a fact you can lean on.

## Positioning against enterprise policy

The three instruments sit at different levels. When the head of AI governance drafts the enterprise policy stack (`mod-110`), the analyst's role is to check the stack layers cleanly:

| Layer | Instrument | Binding? | Analyst-tier check |
|---|---|---|---|
| Universal values baseline | UNESCO Recommendation on the Ethics of AI | Recommendation (non-binding on states) | Policy language does not undercut the values or the 10 principles |
| Rights-and-democracy baseline | CoE Framework Convention on AI | Legally binding treaty (once ratified) | Policy commits at least to the rights, procedural safeguards, and oversight required by the Convention |
| Cross-country soft-law consensus | OECD AI Principles | Non-binding intergovernmental principles | Policy paraphrases or exceeds the five value-based principles |
| Domestic regulation | EU AI Act, US Executive Orders, state laws (Colorado SB 24-205, NYC LL 144), sector regs | Legally binding as applicable | Policy commits to comply and names the operating jurisdictions |
| Framework of choice | NIST AI RMF, ISO/IEC 42001 | Voluntary framework / certifiable standard | Policy names the framework and cites subcategory / clause anchors |
| Enterprise-specific commitments | Responsible AI Policy, model-approval standard, third-party AI vendor standard, GenAI employee guidance | Internal | Policy is consistent across the stack and reviewed by the AI governance council |

The failure mode you are guarding against: a Responsible AI Policy that says less than what the country already signed onto is a public-relations and audit liability. The analyst is often the first person to notice.

## Concrete example — sanity-checking a draft AI policy

Suppose you receive a draft Responsible AI Policy for review. Quick pass:

- **Does it commit to fairness / non-discrimination language at least as strong as OECD Principle 2 and UNESCO's fairness-and-non-discrimination principle?** If it caveats fairness with "where feasible and cost-effective", that is a red flag.
- **Does it acknowledge human rights and mention the rule of law?** OECD, CoE, and UNESCO all say so; if the draft omits it, note it.
- **Does it include transparency and explainability?** OECD Principle 3; UNESCO principle; CoE Convention.
- **Does it include environmental impact?** UNESCO does; the enterprise's own sustainability commitments almost certainly do; check the policy aligns.
- **Does it commit to human oversight?** All three do. The EU AI Act Article 14 makes this a legal obligation for high-risk systems.
- **Does it cite the framework(s) the enterprise operates against?** NIST AI RMF and ISO/IEC 42001 are the two most common.

If the draft is silent on any of these, the analyst-tier finding is "gap against the international values baseline — request coverage" and the routing is up to the senior architect or head of governance for policy work (see `mod-110` and the deferral chapter).

## What to memorise

- The three instruments and their character: **OECD (soft-law principles), CoE (binding treaty), UNESCO (broadest recommendation)**.
- The **five OECD value-based principles**.
- The claim that the CoE Framework Convention is the **first legally binding international treaty on AI**.
- The claim that the **UNESCO Recommendation was adopted by all 193 Member States**.
- Where each instrument sits in the enterprise policy stack.

## Summary

OECD, CoE, and UNESCO define the international values baseline that enterprise AI policy is expected to layer over — not undercut. OECD's five principles are the workhorse reference; the CoE Framework Convention is the first legally binding international AI treaty; UNESCO is the broadest consensus and the strongest source for environmental and cultural anchors. The analyst's role is a sanity check: when the enterprise Responsible AI Policy lands for review, its commitments should be at least as strong as what these three instruments already put on paper.
