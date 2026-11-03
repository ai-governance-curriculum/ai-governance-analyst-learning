# Quiz 01 — Frameworks, Standards, and Values Baselines

**Format:** 10 multiple-choice questions, one correct answer each.
**Grounding chapters:** [01](../01-nist-ai-rmf-four-functions.md), [02](../02-genai-profile-twelve-risks.md), [03](../03-iso-iec-42001-clause-walkthrough.md), [04](../04-eu-ai-act-risk-tiers-and-annex-iii.md), [05](../05-international-values-baseline.md), [06](../06-role-scope-and-deferrals.md).
**Rules:** Open-book against the chapters themselves (the point is fluency, not blind recall). Closed-book against anything else.

---

## Questions

### 1. When the four NIST AI RMF functions fire

Which description best captures the lifecycle rhythm of GOVERN, MAP, MEASURE, and MANAGE?

- A. GOVERN fires only at intake; MAP continues continuously once a system is live.
- B. MAP fires once at design time; GOVERN replaces it when the system goes live.
- C. GOVERN is continuous and predates any single system; MAP, MEASURE, and MANAGE cycle through the AI lifecycle, with the outputs of each feeding the next.
- D. All four fire only at material-change events; between changes they are inactive.

### 2. The trustworthy-AI characteristics

An analyst is drafting an impact assessment and wants to cite the RMF's set of trustworthy-AI characteristics. How many are there and how does the framework rank them?

- A. Five, ordered by severity of harm.
- B. Seven, unranked properties the system is checked against — different domains foreground different ones.
- C. Twelve, aligned one-to-one with the NIST AI 600-1 generative-AI risks.
- D. Four, each matching one of the four RMF functions.

### 3. The three near-universal defaults from the GenAI Profile

Chapter 02 names three generative-AI risks that an analyst should list as *default candidates* on virtually every generative-AI intake. Which trio?

- A. Confabulation; Harmful Bias or Homogenization; Intellectual Property.
- B. Value Chain and Component Integration; Data Privacy; Information Security.
- C. CBRN Information or Capabilities; Dangerous, Violent, or Hateful Content; Obscene, Degrading, and/or Abusive Content.
- D. Environmental Impacts; Information Integrity; Human-AI Configuration.

### 4. Matching a GenAI risk to a canonical use case

An intake proposes an LLM-generated summary of a patient's chart, displayed to a clinician in an EHR sidebar. Which of the twelve generative-AI risks does chapter 02 use *this exact shape of use case* to illustrate?

- A. CBRN Information or Capabilities.
- B. Environmental Impacts.
- C. Human-AI Configuration.
- D. Obscene, Degrading, and/or Abusive Content.

### 5. Why ISO/IEC 42001 layers onto an existing ISMS

Why does ISO/IEC 42001:2023 layer cleanly onto an existing ISO/IEC 27001 ISMS instead of requiring a parallel governance rhythm?

- A. ISO 42001 is a strict superset of ISO 27001 and silently inherits its Annex A controls.
- B. ISO 42001 formally replaces ISO 27001 at Clauses 4–10 once an AIMS is in place.
- C. Both standards share the Annex L / Harmonised Structure, so top-level clause numbering, language, and the audit / management-review rhythm match.
- D. ISO 42001 is a non-certifiable framework and therefore has nothing to reconcile at the clause level.

### 6. What ISO/IEC 42001 adds that ISO/IEC 27001 does not have

Chapter 03 lists additions ISO/IEC 42001 brings to the management-system machinery that ISO/IEC 27001 has no direct equivalent for. Which of the following is one of them?

- A. The Statement of Applicability.
- B. The Clause 10 corrective-action machinery.
- C. The AI impact assessment as a peer to risk assessment, anchored in Clauses 6 and 8.
- D. The internal-audit-and-management-review rhythm at Clause 9.

### 7. Tier-tagging an emergency-dispatch assistant

A product manager submits an intake for an LLM that listens to live 911 calls and suggests severity codes to the human dispatcher. Using the chapter 04 tagging heuristic, how should the analyst tag it?

- A. Minimal — the system is "assistive" because a human dispatcher still decides.
- B. Limited risk — only an Article 50 transparency disclosure is required.
- C. Unacceptable — Article 5 prohibits any AI used in emergency services.
- D. High risk under Annex III (area 5 — access to essential services, which includes emergency-service dispatch).

### 8. Spotting an Article 5 prohibition

Which of the following practices is *prohibited* under EU AI Act Article 5 as described in chapter 04?

- A. Credit scoring used as one input into a loan-underwriting decision.
- B. Emotion inference deployed in workplaces and educational institutions, outside narrow medical and safety exceptions.
- C. An internal retrieval-augmented LLM assistant answering agent-facing questions from a knowledge base.
- D. A general-purpose AI model made available to downstream developers via API.

### 9. Positioning the international values instruments

Chapter 05 positions OECD, Council of Europe, and UNESCO instruments as the international values baseline. Which of the following claims matches what chapter 05 actually says?

- A. The OECD AI Principles are the first legally binding international treaty on AI.
- B. The UNESCO Recommendation on the Ethics of AI is a treaty ratified by 193 member states.
- C. The Council of Europe Framework Convention on AI is the first *legally binding* international treaty on AI, opened for signature in September 2024.
- D. All three instruments are legally binding on their signatory states and preempt the EU AI Act.

### 10. Routing a release sign-off request

A PM asks in Slack: *"The agentic customer-support pilot's eval report is in — can you sign off that it's safe to turn on for external customers next Monday?"* Chapter 06 says the analyst's correct response is:

- A. Read the eval, form a judgement, and reply yes or no — the analyst is closest to the register, so the sign-off belongs here.
- B. Decline entirely and tell the PM to resubmit the request as a ticket in a different queue.
- C. Summarise the eval report into the governance record (findings above/below threshold, residual-risk claim, open questions) and route the sign-off request to the AI Evaluation Engineer, noting the routing in the register.
- D. Escalate to legal counsel for a statutory opinion before taking any other action.

---

## Answer key

| # | Answer | Why |
|---|---|---|
| 1 | **C** | Chapter 01 opens with the explicit claim that GOVERN sits alongside the other three as a *continuous* function that "never stops running," while MAP, MEASURE, and MANAGE "cycle through the AI lifecycle, with the outputs of each feeding the next." (See chapter 01, "The four functions at a glance.") |
| 2 | **B** | Chapter 01's "Trustworthy AI characteristics" section lists seven and states they "are not weighted or ordered; they are properties you check the system against" — different domains put different ones first. |
| 3 | **B** | Chapter 02 names Value Chain and Component Integration, Data Privacy, and Information Security as the three that "show up on virtually every enterprise generative-AI intake" and advises treating them as *default candidates*. |
| 4 | **C** | Chapter 02's table of the twelve risks pairs Human-AI Configuration with the plausible internal use case "Clinician decision-support summary in an EHR sidebar." The risk is about over-reliance, anthropomorphism, and unclear handoff — exactly the EHR-sidebar shape. |
| 5 | **C** | Chapter 03's "Annex L 'High-Level Structure'" section explains that modern ISO management-system standards share the same top-level clause skeleton (formerly Annex L / Annex SL), which is why 42001 inherits the audit rhythm of an existing 27001 ISMS. |
| 6 | **C** | Chapter 03's "Where ISO 42001 adds new machinery" section explicitly calls out the AI impact assessment (Clauses 6 and 8) as a peer to risk assessment with no direct ISMS analogue; it also calls out Annex A AI-specific controls. The SoA, Clause 10, and Clause 9 rhythm all have direct 27001 counterparts, so A, B, and D are wrong. |
| 7 | **D** | Chapter 04's Annex III list names "Access to and enjoyment of essential private services and essential public services and benefits — … emergency-service dispatch" as area 5. The tagging heuristic routes any intended-purpose match in an Annex III area to **high-risk (Annex III route)**. A human-in-the-loop does not demote the tier at analyst level. |
| 8 | **B** | Chapter 04's "What Article 5 prohibits" section lists "Emotion inference in workplaces and educational institutions (with medical / safety exceptions)" as a prohibited practice. Credit scoring, internal RAG, and GPAI-provider releases are not Article 5 prohibitions (they are high / minimal / GPAI tier concerns). |
| 9 | **C** | Chapter 05 characterises the Council of Europe Framework Convention on AI as "the **first legally binding international treaty on AI**," adopted May 2024 and opened for signature in Vilnius on 5 September 2024. UNESCO is a non-binding recommendation; OECD is non-binding intergovernmental principles. |
| 10 | **C** | Chapter 06's "Concrete example — a plausible mis-scope" works through exactly this PM ask and names the right response: the analyst summarises the eval into the governance record and routes the sign-off to the AI Evaluation Engineer. Chapter 06 flags option A as the canonical scope-creep failure that produces "silent methodology risk." |

## Scoring

- **9–10 correct:** Fluent — ready to tag intake under this module's frameworks on day one of production work.
- **7–8 correct:** Solid. Re-read the chapters anchoring any missed questions; patch the gap before `mod-102` intake work starts leaning on this fluency.
- **5–6 correct:** Partial. Re-read chapters 01, 03, and 04 end-to-end — these three carry the most downstream weight.
- **≤4 correct:** Re-read the module. The downstream modules assume this material at recall speed, not at look-up speed.
