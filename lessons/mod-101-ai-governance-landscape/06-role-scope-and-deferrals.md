# Role Scope and Deferrals — What Stays on the Analyst Desk

## Why this chapter

The single most common failure mode for a new AI governance analyst is *scope creep* — quietly taking on work that belongs to the senior AI governance architect, the head of AI governance, an evaluation engineer, an AI risk engineer, an AI infra security engineer, or legal counsel. It happens because the analyst is closest to the intake, closest to the register, closest to the artefact — and stakeholders will hand things over.

Scope creep produces two bad outcomes:

1. **Silent methodology risk.** An analyst-tier answer to a harm-model question, or a fairness-methodology question, or a cross-jurisdiction reconciliation question, is often *wrong* in ways the analyst cannot see. The right owner has domain skills the analyst does not.
2. **Career drift.** An analyst who has spent six months quietly doing architect work has neither *architect on the resume* nor *analyst-tier depth* — the analyst has been doing the wrong altitude of work.

The right posture is the opposite: hold the analyst boundary confidently, route escalations quickly, and let the register speak. This chapter is the deferral map you use to do that.

## What this role owns

At level 15 in the Governance family, the analyst owns:

- **AI use-case intake and triage.** Populating the intake questionnaire, tagging the tier, routing to the risk owner.
- **Model / AI system inventory maintenance.** Keeping the row in sync with the ML registry, filing gaps.
- **First-draft AI risk assessment authoring.** Walking a new system through NIST AI RMF MAP, overlaying ISO 23894 risk sources and the GenAI Profile risks.
- **Impact-assessment authoring.** Algorithmic Impact Assessment (Canadian AIA shape), Fundamental Rights Impact Assessment (EU AI Act Article 27), Data Protection Impact Assessment (GDPR Article 35), and sector-specific impact assessments.
- **Model card, system card, and datasheet authoring** from ML-team inputs.
- **Cross-jurisdiction regulatory tracking.** Rolling watch across EU, US federal, US state, UK, Canada, and sector regulators.
- **Reading eval / red-team / audit evidence into the governance record.** Not authoring the evaluations — reading their outputs into a governance-record summary.
- **Control-tracking and evidence-collection cycles.** Running periodic control tests, pulling evidence, producing analyst-tier control-status reports.
- **Third-party AI vendor review** with an AI-specific due-diligence questionnaire.
- **AI incident response at the analyst tier.** Logging the incident, cross-referencing the inventory row, packaging post-incident evidence.
- **Continuous-monitoring interpretation** and post-market surveillance summary filing.
- **Stakeholder communication and council support.** Pre-read decks, one-pagers, decision logs, minutes for the AI governance council.
- **Drafting internal AI policies and standards under senior guidance.** First-cut acceptable-use policy, model-approval standard, third-party vendor standard, GenAI employee guidance.

That is the roster. Everything below is *not* on it.

## What defers upward

**To the Senior AI Governance Architect** (next-up in the Governance ladder):

- **Control-library architecture.** The master control library that ISO 42001, NIST AI RMF, EU AI Act, SR 11-7, and internal policy are crosswalked into. Analyst maintains the crosswalk row-by-row; architect designs the taxonomy.
- **Policy taxonomy.** How the Responsible AI Policy, model-approval standard, vendor standard, acceptable-use policy, and GenAI guidance fit together as a stack. Analyst drafts inside the stack; architect *designs* the stack.
- **Cross-jurisdiction reconciliation.** When EU AI Act Article 27 FRIA, Canada Directive AIA, GDPR Article 35 DPIA, and a sector overlay all pull on the same use case, the reconciliation of which artefact takes precedence and which fields are shared is architect scope.
- **Quantitative risk methodology.** Frequency-and-severity models, monetised risk claims, and portfolio-level risk aggregation.

**To the Head of AI Governance** / **Chief AI Officer** (executive):

- **Board reporting.** The board sees a curated view — not the register.
- **Budget.** Program budget, tooling budget, headcount.
- **Regulator interface.** External engagement with the EU AI Office, US federal agencies (FTC, EEOC, FDA, CFPB), state AGs, and sector regulators. Analysts prepare read-outs; leadership speaks.
- **Enterprise-wide risk appetite.** The statement of how much AI risk the enterprise will accept in return for how much value.
- **Public communications about AI policy.** Press releases, blog posts, testimony.

## What defers sideways

**To the AI Evaluation Engineer** (peer, Governance family, level 25):

- **Release-assurance methodology.** Whether an evaluation battery is *sufficient* to release. The analyst summarises the eval report; the AI evaluation engineer signs off on the release.
- **Audit-trail methodology.** The design of the evidence chain a regulator or independent auditor can walk. The analyst files evidence into the chain; the engineer designs the chain.
- **Regulator-facing evidence packaging** beyond the analyst-tier summary.

**To the AI Risk Engineer** (peer, ML Engineering ladder, level 30):

- **Harm-model design.** What the harm surface looks like, which failure modes matter, and how to characterise them. The analyst files risks that the harm model surfaces; the risk engineer *designs* the harm model.
- **Alignment-risk methodology.** Deep alignment work — reward-model shaping, RLHF failure modes, spec gaming.
- **Red-team data generation.** The datasets, prompts, and adversarial scenarios red-teamers exercise. The analyst reads the red-team report; the risk engineer designs the exercise.

**To the AI Eval Engineer** (peer, AI Engineering family, level 30):

- **AI-application evaluation methodology depth.** Building the eval harness, choosing metrics, statistical rigour on eval results.

**To the Model Evaluation Engineer** (peer, ML Engineering family, level 30):

- **Benchmark construction** and **statistical methodology** on model evaluations.

**To the AI Infra Security engineer** (level 35):

- **Deep ML/AI security.** The analyst is aware of the OWASP LLM Top 10, MITRE ATLAS, and NIST AI 100-2 taxonomies enough to file a security-linked record and route to the security team. Everything downstream of that — threat modelling of the model, red-teaming the inference infrastructure, incident response for a live attack — is security scope.

**To legal counsel** (out-of-family):

- **Statutory interpretation** and **legal opinion**. The analyst reads GDPR / CCPA / HIPAA / the EU AI Act at a paralegal level. When the answer to "does this obligation apply?" is not obvious, or when the enterprise's answer will be tested externally, it goes to counsel.

**To general privacy engineering** (out-of-family):

- **Depth in GDPR / CCPA / HIPAA / PIPEDA implementation** beyond the AI-specific overlays. AI risk assessments will name a personal-data flag and route to the privacy team.

## Boundary-holding heuristics

You are on the right side of the boundary when:

- You cite the framework and its subcategory in the register entry rather than inventing methodology.
- You name the risk owner (product, ML, security, legal, privacy) and route with a proposed action rather than owning the mitigation yourself.
- You summarise an evaluation report into the governance record rather than critiquing its methodology.
- You draft an artefact from a template rather than designing the template.
- You escalate boundary cases to the right peer or up-role rather than answering them silently.

You are on the wrong side of the boundary when:

- You are designing the enterprise's control library from scratch.
- You are reconciling how EU AI Act Article 27 FRIA, GDPR Article 35 DPIA, and a Canadian AIA overlap without an architect involved.
- You are producing a monetised risk claim to be shown to executives.
- You are giving a legal opinion — even implicitly — on whether an obligation applies.
- You are designing an eval methodology or an adversarial-testing scenario.
- You are drafting board-facing communication without leadership sign-off.

## Practical routing table

Use this as a mental cheat-sheet when triaging incoming work.

| Incoming ask | Where it goes |
|---|---|
| "Tier this new intake against the EU AI Act." | Analyst (this role). |
| "Author the FRIA first draft." | Analyst. |
| "Design the AIA-FRIA-DPIA-sector reconciliation for the enterprise." | Senior AI Governance Architect. |
| "Rewrite the enterprise Responsible AI Policy." | Head of AI Governance drives; Senior Architect drafts; analyst supports. |
| "Score this risk quantitatively for a board pack." | Senior Architect (quantitative methodology); Head of Governance signs off. |
| "Read the vendor SOC 2 + red-team report into the vendor record." | Analyst. |
| "Sign off that the model is safe to release." | AI Evaluation Engineer. |
| "Design the harm model for a new agentic system." | AI Risk Engineer. |
| "Build the eval harness for this LLM app." | AI Eval Engineer. |
| "Give a legal opinion on whether GDPR Article 22 applies." | Legal counsel. |
| "Interpret the OWASP LLM Top 10 finding on this system and recommend a fix." | AI Infra Security. |
| "Log an incident against the register." | Analyst. |
| "Present the AI risk portfolio to the audit committee." | Head of AI Governance / CAIO. |

## Concrete example — a plausible mis-scope

A product manager asks: *"Can you review the eval report for the new agentic customer-support system and let us know if it's safe to release?"*

Wrong response (in-scope creep): read the eval report, form a judgement, tell the PM yes or no. This gives the PM a *release decision from an analyst*, which is the wrong altitude and produces silent methodology risk.

Right response (analyst-tier): summarise the eval report into the governance record — findings above threshold, findings below threshold, residual-risk claim, open questions. Route the release-sign-off request to the AI Evaluation Engineer with the summary attached. Note the routing in the register.

The PM gets an answer within the day; the AI Evaluation Engineer owns the *sign-off*; the analyst owns the *summary* and the *route*. Everyone stays at the right altitude.

## What to memorise

- The **owned scope** of this role — the fourteen items in the "owns" list.
- The three **up-defers** (architect, head of governance, CAIO).
- The five **sideways defers** (evaluation engineer, risk engineer, eval engineer, model evaluation engineer, infra security).
- The two **out-of-family defers** (legal counsel, general privacy engineering).
- The two boundary-holding heuristics: *cite framework, don't invent methodology*; *summarise evidence, don't authorise release*.

## Summary

The analyst owns the operational altitude of the governance program: intake, inventory, first-draft assessments, impact assessments, model / system / dataset cards, control-tracking cycles, regulatory tracking, evidence-reading, analyst-tier incident response, council support, and policy drafts under senior guidance. Everything upward of that — architecture, taxonomy, cross-jurisdiction reconciliation, board reporting, regulator interface, harm-model design, release sign-off, statutory interpretation — defers. Route cleanly, cite explicitly, and let the register speak.
