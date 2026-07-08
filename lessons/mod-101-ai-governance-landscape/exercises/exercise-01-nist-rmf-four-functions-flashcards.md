# Exercise 01 — NIST RMF Four Functions Flashcards

**Estimated effort:** 2 hours
**Grounding chapters:** [01 — NIST AI RMF 1.0](../01-nist-ai-rmf-four-functions.md), [02 — GenAI Profile](../02-genai-profile-twelve-risks.md)

## Objective

Build a personal flashcard set that lets you recite the four NIST AI RMF functions, their categories, and their intent from cold. The goal is not to *memorise the framework document*. The goal is to build *recall fluency* deep enough that in an intake meeting, when someone says "we should probably file this against MAP-5", you can answer *without opening the PDF*.

## Prerequisites

- Chapter 01 read.
- A flashcard tool of your choice: [Anki](https://apps.ankiweb.net/), [Mochi](https://mochi.cards/), a Notion database, or index cards. Whichever you will actually revisit.
- The [NIST AI RMF 1.0 PDF](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) and the [Playbook](https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook) open.

## Problem statement

You will build ~50 flashcards covering:

1. **The four functions.** Front: function name. Back: one-line intent + count of categories under it + when it fires in the lifecycle.
2. **The seven trustworthy-AI characteristics.** Front: characteristic. Back: one-line intent + the RMF function most closely associated + one example failure mode.
3. **The nineteen top-level categories** (GOVERN 1–6, MAP 1–5, MEASURE 1–4, MANAGE 1–4). Front: category identifier (e.g., "MAP 2"). Back: one-line intent.
4. **Six representative subcategories** you choose from the Playbook — pick the ones most likely to be cited in your target sector (finance / healthcare / general enterprise). Front: subcategory identifier. Back: intent + one Playbook-suggested action + one transparency question.

## Requirements

- **Every card front is short** (≤ 8 words) so you cannot leak the answer.
- **Every card back cites the framework by function-and-category** (e.g., "GOVERN 1.1 — RMF §5.1").
- **No fabricated subcategory content.** If you cannot find the Playbook's suggested actions for a subcategory, write a `<!-- needs-research: -->` note in the card back and skip it in the review deck.
- **Cards are exportable** — commit them as a `.csv`, `.tsv`, `.md`, or an Anki `.apkg` in your workspace so you can revisit or share.
- **A short reflection note** — after your first full review pass, write 3–5 sentences on which cards you got wrong the first time and why. This is the metadata that lets a coach or a peer help you.

## Starter guidance

- Do not try to cover every subcategory. Nineteen categories + six chosen subcategories is a *studyable* deck. Fifty subcategories is not.
- Use the Playbook's own phrasing where possible; do not paraphrase into your own vague words. If the Playbook says "prioritize", do not soften to "consider".
- If you are building this for a specific target sector, pick subcategories that show up in that sector's regulatory overlay. For finance, MAP 4 (third-party data) and MANAGE 3 (third-party risks) are safe picks; for healthcare, MEASURE 2 (validity and reliability) shows up in Good ML Practice.
- Include cards on the trustworthy-AI characteristics *by name and by count*. Interviewers ask "how many characteristics does the RMF define?" and expect "seven".

## Acceptance criteria

- Deck contains cards for **all 4 functions**, **all 7 trustworthy-AI characteristics**, **all 19 top-level categories**, and **6 chosen subcategories** — 36 to 40 cards minimum.
- Every card back cites its source location (framework section or Playbook URL).
- The deck runs cleanly in your chosen tool (imports without errors, if using Anki / Mochi).
- Reflection note is present and honest.
- No card back contains fabricated content — every claim is either sourced from the framework / Playbook or explicitly marked `needs-research`.

## Stretch goals

- Add cards for the **12 GenAI Profile risks** (front: risk name; back: one-line intent + one plausible internal use case + one RMF subcategory to attach the register entry to).
- Add cards that quiz you on the **ISO/IEC 42001 ↔ NIST RMF touchpoints** — e.g., "Which RMF function most closely corresponds to ISO/IEC 42001 Clause 6 planning?" (Answer: MAP + parts of GOVERN.)
- Add cards distinguishing **RMF vs 42001 vs EU AI Act** as instruments — voluntary framework vs certifiable standard vs regulation. Interviewers ask this.
- Publish the deck as a shared study resource for your peers, with a short README on how you organised it.

## Deliverables

- `mod-101-ex-01-flashcards.{csv|tsv|md|apkg}` in your workspace.
- `mod-101-ex-01-reflection.md` — the 3–5 sentence reflection note.

## Notes on evaluation

There is no "grader" for a flashcard deck — the deliverable is the deck plus your reflection. In the paired solutions repo, the reference deck illustrates one defensible cut of the material; your own deck should differ from it in subcategory choice and phrasing (that is the point of building your own).
