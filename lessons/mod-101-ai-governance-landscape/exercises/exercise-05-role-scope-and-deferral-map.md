# Exercise 05 — Role Scope and Deferral Map

**Estimated effort:** 2 hours
**Grounding chapter:** [06 — Role scope and deferrals](../06-role-scope-and-deferrals.md)

## Objective

Take a batch of realistic **incoming asks** — the kind that land on the analyst desk from a product manager, a data scientist, a lawyer, a security engineer, or the head of governance — and produce, for each one, an explicit routing decision: *own it, co-own it, decline and route it, or block and escalate.* Along the way, build the personal desk-side **deferral map** you will lean on for the rest of the year.

The point is not to become skilled at saying no. The point is to know, ahead of time, *which desk each ask belongs on*, so you can accept the work that is genuinely yours and route the rest inside a day rather than quietly absorbing it and drifting off-altitude.

## Prerequisites

- Chapter 06 read.
- The track-level [`JOB_REQUIREMENTS.md`](../../../JOB_REQUIREMENTS.md) and [`CURRICULUM.md`](../../../CURRICULUM.md) open — they list the owned scope and the up / sideways / out-of-family defers this exercise assumes.
- Optional but useful: your employer's actual RACI chart for the AI governance program (if one exists). This exercise works as a general drill without it.

## Problem statement

Author a single markdown file, `mod-101-ex-05-deferral-map.md`, containing four sections.

### Section 1 — Your desk-side deferral map

Reproduce the ownership map from chapter 06 in your own words — not as a copy of the tables in the chapter, but as a **one-page** reference you would keep pinned to your desk. It should contain:

- **Owned scope.** A bullet list of the analyst-tier deliverables you accept without escalation. Keep it to 10–14 items; the chapter lists roughly that many.
- **Up-defers.** For each upward role (Senior AI Governance Architect; Head of AI Governance / CAIO), 2–4 concrete examples of asks that go there.
- **Sideways-defers.** For each peer role (AI Evaluation Engineer; AI Risk Engineer; AI Eval Engineer on the AI Engineering ladder; Model Evaluation Engineer on the ML Engineering ladder; AI Infra Security), 1–3 concrete examples.
- **Out-of-family defers.** For legal counsel and general privacy engineering, 1–3 concrete examples each.
- **Two boundary-holding heuristics** stated in your own words — the two the chapter calls out (*cite framework, don't invent methodology*; *summarise evidence, don't authorise release*) plus, optionally, one you invent.

This is the artefact you will actually use. Optimise for scannability, not exhaustiveness.

### Section 2 — Routing the incoming asks

Below are **fifteen incoming asks**, phrased the way they would arrive in a Slack DM, a ticket, or a hallway conversation. Copy them into your working file and produce, for each, a routing row.

#### The incoming asks

1. *PM, in Slack:* "Can you take a look at the new agentic customer-support pilot's eval report and let me know if we're safe to turn it on for external customers next Monday?"
2. *Head of AI Governance, in a 1:1:* "Draft the first-cut Responsible AI Policy for the enterprise — I'll edit and take it to the exec review."
3. *Data scientist, in a ticket:* "Please tier this new intake against the EU AI Act and cite the article — it's a résumé-screening tool for internal recruiting."
4. *Senior AI Governance Architect, in email:* "I'm designing the cross-jurisdiction reconciliation for how FRIA / DPIA / Canadian AIA / a sector overlay stack on the same intake. Would you own the design end-to-end so I can focus on the enterprise control library?"
5. *Legal counsel, in Teams:* "We need a legal opinion on whether GDPR Article 22 applies to our new loan-underwriting decision assistant. Can you write it up?"
6. *AI Eval Engineer, in Slack:* "The new bias-eval battery is running clean; do you want to sign off on the release?"
7. *Security engineer, in a ticket:* "OWASP LLM Top 10 finding on prompt injection came back on the RAG assistant. Can you triage the fix and land the mitigation?"
8. *PM, in Slack:* "Please open a register entry for the new marketing-copy generator, tag the tiering, and note which impact assessment(s) will apply."
9. *Head of AI Governance, in a DM:* "The board pack this quarter needs a monetised view of AI risk across the portfolio. Can you build the model and present it?"
10. *Vendor manager, in email:* "New SOC 2 and pen-test report arrived from our foundation-model vendor. Please read it into the vendor record and flag anything material."
11. *PM, in a project channel:* "We had a hallucination incident on the internal knowledge-base assistant yesterday — a user got a wrong policy citation. Please log it and open the incident."
12. *AI Risk Engineer, in Slack:* "For the new agentic pipeline, I want to spin up a red-team exercise. Can you scope the harm model and draft the adversarial-prompt dataset?"
13. *PM, in Slack:* "Colorado just passed a new AI-hiring rule — what does it mean for our current résumé pilot, and do we need to change anything?"
14. *Privacy engineer, in a DM:* "The new clinical-note summariser touches PHI. Can you own the full HIPAA implementation review — controls, BAAs, MRAs, all of it?"
15. *Head of AI Governance, in email:* "Please prepare the quarterly council pre-read: portfolio status, open MANAGE-1 items above threshold, regulatory-watch summary, and a one-slide 'what needs a decision this meeting'."

#### For each ask, produce a row

| Column | Content |
|---|---|
| # | 1–15 |
| Verdict | one of: `own it`, `co-own with X`, `decline and route to X`, `block and escalate` |
| Route (if applicable) | Named role (e.g., "Senior AI Governance Architect", "AI Evaluation Engineer", "legal counsel") |
| Analyst-tier hand-off | What the analyst does **before** handing off — the summary, the framework-cited register entry, the intake questionnaire, the packaged evidence, the meeting minutes, etc. Never "nothing." |
| Rationale | 1–2 sentences on **which boundary** this ask sits on. Cite the ownership map by role name. |
| Boundary-holding heuristic used | The chapter names two; add your own if it helps. |

The verdict should reflect chapter 06's ownership map without embellishment. Some asks are clearly owned; some are clearly deferred; a few are meant to be genuinely ambiguous (co-owned, or "own the summary, route the decision"). Do not resolve every row to a clean owned / not-owned tag — the exercise rewards honest ambiguity where the chapter permits it.

### Section 3 — A near-miss self-assessment

Pick **two** asks from Section 2 that you can imagine yourself accepting in-scope even though the chapter says they should defer. For each, write:

- The ask.
- The verdict you would have given six months ago, before this module.
- The verdict you would give now.
- The **failure mode** the wrong verdict would produce (silent methodology risk, career drift, wrong-altitude decision made without the right authority, missed escalation to legal, etc.).
- One **early-warning signal** — the sentence a stakeholder might say that should tip you off that you are about to over-accept.

The point of this section is not self-flagellation. It is to name, in advance, the exact shape of the mistake you are most likely to make, so you can catch it.

### Section 4 — Reflection

5–8 sentences answering:

- Which category of ask are you most tempted to accept even when the chapter says defer? (Common honest answers: legal-opinion-shaped asks; release-sign-off asks; harm-model-shaped asks.)
- Which defer role in the ownership map do you understand *least*? Which one would you shadow for a week if you could?
- Is there a category of ask that appears in the fifteen above that the chapter's ownership map does not cleanly cover? If so, name it — that is the kind of gap you file back to the senior architect for a RACI update.

## Requirements

- Every verdict in Section 2 names a specific role from the ownership map — no "someone else" or "the team."
- Every routing row has a non-empty analyst-tier hand-off. The rule is: even when you decline the ask, you leave the next person a running head-start (a register entry, a summary, a packaged report, a meeting minute).
- Every rationale cites the ownership map by role name (e.g., "This is release-sign-off — belongs to the AI Evaluation Engineer per chapter 06").
- The desk-side deferral map (Section 1) fits **on one page** in a normal editor at readable font. If it does not fit, cut items — this is a reference, not a manual.
- No fabricated org-chart roles. If your target enterprise's RACI differs from the ownership map in chapter 06, name the delta explicitly in Section 4 rather than silently rewriting the chapter's map.

## Starter guidance

- Do Section 1 last. You will produce a better one-page map after you have walked the fifteen asks in Section 2 and felt where the boundaries actually bite.
- When you get to a "co-own" verdict in Section 2, be honest about the split. A useful pattern: *"I own the summary and the register entry; the AI Evaluation Engineer owns the release decision."* That is a co-own with a clean boundary.
- Ask 1 (release sign-off request from a PM) and ask 6 (AI Eval Engineer offering you the sign-off) are the two most common analyst traps in the wild. They will show up in your first month of production work.
- Ask 5 (legal opinion) is a *hard* decline. Analysts do not write legal opinions even when the answer looks obvious. If you find yourself tempted, name the specific statute you would be interpreting — that is usually enough to reset.
- Ask 9 (monetised board-facing risk view) is a mixture: the analyst can prepare the underlying data pack and portfolio summary, but the *model* and the *presentation* belong to the senior architect and head of governance respectively. Split it.
- Ask 14 (full HIPAA implementation review) is a classic scope-creep invite — HIPAA depth belongs to privacy engineering. The analyst owns the AI-specific overlays (see `mod-105` and `mod-106`), not the underlying implementation review.
- For asks that involve reading an external report into the governance record (10, 11), remember that reading the report *is* on the analyst desk. Signing off on what the report *concludes* is not.

## Acceptance criteria

- File `mod-101-ex-05-deferral-map.md` present in your workspace.
- Section 1 (one-page deferral map) present, scannable, and consistent with chapter 06.
- Section 2 has all 15 asks routed, each with a verdict, a route (or blank if `own it`), an analyst-tier hand-off, a rationale citing the ownership map, and a named boundary-holding heuristic.
- Section 3 has two near-miss self-assessments with an early-warning signal each.
- Section 4 reflection is present, honest, and specific — it names at least one temptation you personally have and at least one role you would shadow.
- No fabricated org roles. Any local RACI delta is called out in Section 4.

## Stretch goals

- Add a **sixteenth ask of your own**, chosen because it sits on a boundary the fifteen above do not cleanly hit. Route it. This is a good candidate for peer review.
- Add a **"time-to-route" target** in Section 1 — e.g., *"if I have not routed a clearly out-of-scope ask within one business day, that is itself a signal I am about to absorb it."* This becomes an ops KPI you can measure yourself against.
- Add a **routing template** — a short markdown snippet you would paste into a Slack response when declining an ask, with placeholders for the ask, the correct owner, the analyst-tier hand-off, and the reason. This is a legitimately reusable artefact.
- Cross-reference each verdict in Section 2 to a specific chapter of this track (e.g., "release sign-off → not covered here; belongs to a track for AI Evaluation Engineers"). This exposes the seams between roles that a good analyst learns to name aloud.
- Draft a **RACI-delta memo** for your employer — a one-pager naming any place the chapter 06 ownership map does not fit your local org, with a proposed resolution. Share it with your manager or the senior architect if the environment supports it.

## Deliverables

- `mod-101-ex-05-deferral-map.md`.

## Notes on evaluation

The reference solution in the paired `ai-governance-analyst-solutions` repository shows one defensible cut through the fifteen asks. On most rows the verdict will match; on the ambiguous ones (1, 6, 9, 10, 12, 13) the *shape* of the reasoning matters more than the exact verdict. The rubric is: (a) the desk-side map is genuinely one page and matches the chapter; (b) every routing row names a real role, a real hand-off, and a real rationale; (c) the near-miss self-assessment names a failure mode with teeth; (d) the reflection is honest and specific enough that a mentor could act on it.
