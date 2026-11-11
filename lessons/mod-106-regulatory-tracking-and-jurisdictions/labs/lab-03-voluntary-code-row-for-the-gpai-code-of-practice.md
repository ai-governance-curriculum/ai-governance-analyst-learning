# Lab 03 — Voluntary-Code Tracker Row for the GPAI Code of Practice

**Duration:** 90 minutes.
**Grounding chapters:** [09](../09-voluntary-codes-gpai-code-of-practice.md), [01](../01-rolling-regulatory-tracker-method.md), [02](../02-eu-stack-ai-act-gdpr-coe.md); AIGP tagging per [08](../08-iapp-aigp-shared-vocabulary.md); routing per [10](../10-regulatory-change-note-routing.md).
**Difficulty:** Core — exercises chapter 09's voluntary-code reading pattern and the tracker treatment of a code the enterprise is a *deployer* under rather than a provider, which the module's five exercises do not directly drill.

## Objective

Take a *fixed, pre-assembled* stub tracker row and inventory context — `REG-2026-EU-010` as a half-populated row for the EU AI Office General-Purpose AI Code of Practice, and two inventory rows that are *deployers* of in-scope GPAI models rather than providers of them — and author a complete voluntary-code tracker row per chapter 09's framing. The row carries every column from chapter 01's schema, the AIGP tag from chapter 08, and a *notes for counsel* field with the adherence trade-off framing chapter 09 insists is routed to the governance owner and general counsel rather than decided by the analyst. Pair the row with a short `adherence-framing-memo.md` that writes up the trade-off for the governance owner in the chapter 09 *adopt / do not adopt* shape, and reserve a change-note identifier for the day the AI Office publishes a Code revision.

The lab's point is the specific case most enterprises face — being a *deployer* of a GPAI model whose provider has adhered to the Code — which chapter 09 explicitly calls out and which none of the module's exercises drill. The analyst-tier action is not *should we sign the Code*; it is *how do we read the provider's Code adherence documentation and route it into our Article 26 deployer obligations and our vendor-review evidence*.

## Prerequisites

- All ten chapters read; chapter 09's three-chapter structure of the Code (transparency, copyright, safety-and-security), Article 56's presumption-of-compliance framing, and the five-step analyst-tier reading pattern fresh in memory.
- Chapter 02 fresh for Article 51's systemic-risk designation, Article 53 and Article 55 provider obligations, and Chapter V's 2 August 2025 effective date.
- A markdown editor; no Python or GRC-platform tooling required.
- Exercises 01 and 05 completed, or at minimum skimmed, so the tracker schema and change-note shape are familiar.

## The fixed input

Use *exactly* this stub and inventory context. Do not substitute identifiers or pre-populate the empty fields. Identifiers are illustrative; treat the block as `pedagogic example — numbers and dates illustrative`.

### A. The stub tracker row

```
REG-2026-EU-010 — EU AI Office General-Purpose AI Code of Practice
  Jurisdiction:    EU
  Instrument:      (to populate)
  Short name:      EU GPAI Code of Practice
  Scope trigger:   (to populate)
  Role:            (to populate — enterprise is primarily a deployer of
                   in-scope GPAI models; the row carries both the provider-
                   facing scope trigger and a note on the deployer-facing
                   secondary read)
  Status:          (to populate)
  Effective date:  (to populate)
  Enforcement:     (to populate)
  Affected inv:    (to populate)
  Related obl:     REG-2026-EU-002 (AI Act Article 6 + Annex III),
                   REG-2026-EU-005 (Chapter V GPAI)
  AIGP tag:        (to populate)
  Last verified:   (to populate)
  Primary src:     (to populate)
  Notes:           (to populate — adherence trade-off framing)
```

### B. The inventory context

```
INV-2026-ASSIST-01 — InternalRAG (internal knowledge-base assistant)
  Owner:          IT Platform
  Tier tag:       Tier 2
  GPAI exposure:  Deploys Vendor-V foundation model (GPAI). Vendor-V has
                  publicly adhered to the GPAI Code of Practice; its Code
                  adherence documentation is on the vendor's trust page.

INV-2026-MKTG-11 — MCDA (marketing copy draft assistant)
  Owner:          Marketing Ops
  Tier tag:       Tier 2
  GPAI exposure:  Deploys Vendor-W foundation model (GPAI). Vendor-W has
                  not adhered to the Code; its own-compliance posture is
                  cited in its vendor-review artefact.

INV-2026-CLIN-05 — PathTriage (authorised AI/ML-enabled SaMD device)
  Owner:          Pathology Service Line
  Tier tag:       Tier 1 (high)
  GPAI exposure:  None — purpose-built narrow-task model; no GPAI
                  component.
```

### C. The today-date for the authoring

Treat today as **2026-11-11**.

## Steps

### Step 1 — Scaffold the working folder (5 min)

Create the working folder and files.

```bash
mkdir -p ~/aicg-labs/mod-106-lab-03
cd ~/aicg-labs/mod-106-lab-03
touch tracker-row.md adherence-framing-memo.md change-note-reservation.md
```

Open `tracker-row.md` and reproduce the stub row block from block A verbatim at the top so the reviewer can see the starting state; author the populated row below it.

### Step 2 — Populate the *instrument* and *primary-source URLs* columns (10 min)

Open chapter 09's "The GPAI Code of Practice — what it is and how it interacts with the AI Act" sub-section. The chapter names:

- The AI Office code-of-practice page as the canonical landing page.
- The *Final General-Purpose AI Code of Practice — AI Office* publication (July 2025) as the specific published instrument.
- The AI Act Chapter V, Articles 51–56, as the underlying regulation.
- Article 56 as the specific article that establishes adherence as contributing to a presumption of compliance.

Populate:

- *Instrument.* `Final General-Purpose AI Code of Practice — EU AI Office (July 2025), published under Article 56 of Regulation (EU) 2024/1689`.
- *Primary src.* `https://digital-strategy.ec.europa.eu/en/library/final-general-purpose-ai-code-practice` (code landing page per chapter 09); plus `https://eur-lex.europa.eu/eli/reg/2024/1689/oj` for the Chapter V reference.
- Add a `<!-- needs-research: verify the current published version of the Code, any periodic updates, and the current adherent list at digital-strategy.ec.europa.eu/en/policies/ai-code-practice before citing to an audience per chapter 09 needs-research marker -->` marker in the notes column.

Record the populated fields in `tracker-row.md`.

### Step 3 — Populate the *scope trigger* and *role* columns (10 min)

Chapter 09 is explicit that the Code's scope is *provider of a general-purpose AI model* — Article 3(63) definition, with Article 51 overlaying the systemic-risk designation. Chapter 09 is equally explicit that most enterprises are *deployers* rather than providers, and that the row's affected-inventory-row list is often empty on the provider side.

Populate:

- *Scope trigger.* `Enterprise is a provider of a general-purpose AI model as defined at Article 3(63), with Article 51 designation applying the safety-and-security chapter to systemic-risk-model providers. Secondary read: enterprise is a deployer of an in-scope GPAI model; the provider's Code adherence documentation is an input to the enterprise's Article 26 deployer obligations and to the vendor-review artefact per mod-105 chapter 06.`
- *Role.* `Provider of GPAI model (primary scope); deployer of in-scope GPAI model (secondary, affects vendor-review evidence rather than direct Code obligation).`

The two-shape framing is the chapter 09 move — the enterprise may be *out of direct scope* for the Code (because it is not a GPAI provider) and still *affected* by the Code's existence (because its deployed vendor's adherence informs the vendor-review evidence). A row that collapses to a single-role framing misses the secondary read.

### Step 4 — Populate the *status* and *effective date* columns (5 min)

Chapter 09 says the Code was finalised in July 2025 ahead of the 2 August 2025 Chapter V effective date, and the AI Office has indicated a periodic review cadence. The row's status field is a voluntary-code shape, not an *in force* shape.

Populate:

- *Status.* `Voluntary code — published July 2025. Adherence contributes to the Article 56 presumption of compliance with corresponding Article 53 / Article 55 obligations; non-adherence is not a violation.`
- *Effective date.* `Published July 2025; underlying AI Act Chapter V obligations (Article 53 — all GPAI providers; Article 55 — systemic-risk-model providers) applied from 2 August 2025.`

### Step 5 — Populate the *enforcement* column (5 min)

Chapter 09 is explicit that adherence is voluntary; the AI Office maintains the Code and the adherent list. Enforcement of the underlying obligations (not of the Code itself) runs at Union level through the AI Office with Member State supervisory-authority participation per Article 88.

Populate:

- *Enforcement.* `Code adherence is voluntary; AI Office maintains the Code and the adherent list. Underlying Article 53 (all GPAI providers) and Article 55 (systemic-risk-model providers) obligations are enforced by the AI Office at Union level, with Member State supervisory-authority participation per Article 88.`

### Step 6 — Populate the *affected inventory rows* column (10 min)

Walk block B. For each inventory row, decide whether the row inherits the GPAI Code tracker row.

- `INV-2026-ASSIST-01` (InternalRAG). Enterprise is a *deployer* of Vendor-V (a GPAI provider that has adhered to the Code). Direct Code obligation on the enterprise: none. Secondary effect: Vendor-V's Code adherence documentation feeds the enterprise's vendor-review artefact and its Article 26 deployer-obligation evidence. Record *affected (secondary read) — vendor adherent*.
- `INV-2026-MKTG-11` (MCDA). Enterprise is a *deployer* of Vendor-W (a GPAI provider that has not adhered to the Code). Direct Code obligation on the enterprise: none. Secondary effect: Vendor-W's absence of Code adherence means the vendor-review artefact must carry the vendor's own-compliance-posture evidence rather than a Code-adherence citation. Record *affected (secondary read) — vendor not adherent; vendor-review relies on own-compliance posture*.
- `INV-2026-CLIN-05` (PathTriage). No GPAI component. Record *not affected — no GPAI component in this system*.

The populated column:

```
Affected inv:
  INV-2026-ASSIST-01 — secondary read; Vendor-V is Code-adherent; vendor-review
                       artefact cites Code adherence as Article 26 deployer-
                       obligation input.
  INV-2026-MKTG-11   — secondary read; Vendor-W is not Code-adherent;
                       vendor-review relies on vendor own-compliance evidence.
  INV-2026-CLIN-05   — not affected (no GPAI component).
  No direct scope    — enterprise is not a GPAI provider; the direct-scope
                       affected-inventory-row list is empty by design per chapter
                       09's typical-enterprise-deployer framing.
```

### Step 7 — Populate the *AIGP tag* and *last verified* columns (5 min)

Chapter 09 names the AIGP tag as `Domain 4 (existing and emerging AI laws and standards); secondary Domain 5 (AI development life cycle) for the safety-and-security chapter`. Populate exactly that; the primary domain is first per chapter 08's tagging pattern.

Populate:

- *AIGP tag.* `D4 primary; D5 secondary (safety-and-security chapter).`
- *Last verified.* `2026-11-11` with the needs-research marker from step 2 carried as the honest-uncertainty companion.

### Step 8 — Populate the *notes for counsel* column with the adherence trade-off framing (10 min)

Chapter 09's "The trade-off — why the enterprise may or may not adopt" sub-section names:

- *Adopt when.* Code articulates practice the enterprise is already doing at scale; enterprise wants to signal compliance posture to customers / sovereigns / investors; Code's evidentiary weight materially reduces exposure.
- *Do not adopt (yet) when.* Code is still in a settling phase; Code covers practice areas the enterprise does not do at scale; counsel prefers direct-to-regulation evidence over code-mediated presumption.

For the lab's fixed input the enterprise is *not* a GPAI provider on any of the three inventory rows, so the direct-adherence question does not arise. The analyst-tier note:

```
Notes for counsel:
  Enterprise is not a GPAI provider on any current inventory row; direct Code
  adherence decision not open. Secondary reads apply on INV-2026-ASSIST-01 and
  INV-2026-MKTG-11 — vendor-review evidence cites Vendor-V's Code adherence and
  Vendor-W's own-compliance posture respectively. Flag to vendor-review lead to
  confirm the Code-adherence citation on INV-2026-ASSIST-01 is a current
  version. Adherence trade-off framing deferred to governance owner and general
  counsel at the point the enterprise first considers deploying a GPAI model
  under its own branding (which would flip the role to provider) or developing a
  GPAI model in-house.
```

The note is a *question routed to the governance owner and counsel* framed in the chapter 07 pattern — not an opinion on whether the enterprise should sign. Chapter 09 is explicit: *the adherence decision is not the analyst's*.

### Step 9 — Author the adherence-framing memo (15 min)

Open `adherence-framing-memo.md` and author a short memo (roughly 500 words) for the governance owner. Structure:

- **Header.** Title (`GPAI Code of Practice — adherence framing — 2026-11-11`); author (analyst role); recipient (governance owner, general counsel copied); cross-reference to `REG-2026-EU-010`.
- **Current state.** One paragraph: enterprise is not a GPAI provider on any current inventory row; the Code applies to providers; the enterprise is a deployer of two in-scope models with differing vendor Code-adherence status.
- **Why the framing still matters.** Two or three sentences: if the enterprise develops a GPAI model in-house or begins exposing a GPAI model under its own branding, the role flips to provider and the Code's direct scope attaches. The framing is prepared in advance so the decision — when it arises — is not authored under time pressure.
- **Adopt-when considerations.** Three bullets from chapter 09's *adopt when* list, each phrased as a *question for the governance owner*: are the Code's articulated practices already what the enterprise does; is signalling compliance posture a current enterprise objective; does the Article 56 presumption's evidentiary weight materially matter to the enterprise's exposure.
- **Do-not-adopt-yet considerations.** Three bullets from chapter 09's *do not adopt* list, same question shape: is the Code's text settled; do the Code's practice areas overlap the enterprise's actual operations; does counsel prefer direct-to-regulation evidence.
- **Analyst role boundary.** One sentence: the analyst frames; counsel and the governance owner decide. The memo is not an advocacy document.

### Step 10 — Reserve the change-note identifier (10 min)

Open `change-note-reservation.md`. Chapter 09 says the Code is periodically revised; chapter 10 says a regulatory-change note is the artefact that converts a tracker update into routed action. Reserve a change-note identifier for the next AI Office publication of a revised Code so that when the publication lands the analyst is not improvising the identifier.

Write:

```markdown
# Change-note reservation — GPAI Code of Practice

Reserved identifier: CN-2026-LAB03-01
Reserved for:        AI Office publication of a revised GPAI Code of Practice
                     or an update to the adherent list that materially shifts
                     the enterprise's vendor-review evidence on
                     INV-2026-ASSIST-01 or INV-2026-MKTG-11.
Fired by:            Monthly deep-read scan of
                     https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice
                     per the chapter 09 reading pattern step 4 (note drift risks
                     and compare current AI Office publication to the version
                     of record).
Routing (anticipated):
  Primary — vendor-review lead and the owners of INV-2026-ASSIST-01
            (IT Platform) and INV-2026-MKTG-11 (Marketing Ops).
  Secondary — governance owner (who owns the Code-adherence decision if the
              enterprise's role flips to provider in future) and risk-register
              owner.
  Tertiary — general counsel (on the interpretation of any changed Article 56
             presumption language or any adherent-list update that affects a
             vendor citation in the enterprise's evidence).
```

The reservation is a tracker-hygiene move — chapter 09's reading pattern closes with *note the drift risks* and chapter 10's discipline closes with *route the change-note* when a drift materialises. Reserving the identifier now is the dot-the-i that keeps the next month's deep read smooth.

### Step 11 — Self-check (5 min)

Walk the three files top-to-bottom and verify:

- Every column of `REG-2026-EU-010` is populated. No `(to populate)` remains. One `<!-- needs-research: -->` marker is open against the AI Office code-of-practice page per chapter 09's needs-research marker.
- The *scope trigger* and *role* columns carry both the primary (provider) and secondary (deployer of in-scope model) reads. A row with only the provider-shape scope trigger misses the chapter 09 deployer-side framing.
- The *affected inventory rows* column resolves to specific outcomes for the three rows in block B, with the *not affected* answer for the non-GPAI row cited explicitly.
- The *notes for counsel* field frames the trade-off as a *question routed to the governance owner and counsel* per chapter 09's *not the analyst's decision* framing. A note that opines *we should sign the Code* is a failure of the discipline.
- The memo is a *framing* document, not a recommendation. Each adopt / do-not-adopt consideration is phrased as a question for the governance owner.
- The change-note reservation names the fired-by scan (chapter 09 reading pattern step 4) and the anticipated routing per chapter 10's primary / secondary / tertiary pattern.

## Expected output

Three markdown files in `~/aicg-labs/mod-106-lab-03/`:

- `tracker-row.md` — stub at the top, populated row underneath; every column filled; one needs-research marker.
- `adherence-framing-memo.md` — ~500 words, header plus six sections per step 9.
- `change-note-reservation.md` — short reservation note with fired-by scan and anticipated routing.

Total length: roughly 1,200–1,800 words across the three files.

## Checkpoint

A mentor, peer, or self-review walk. Answer honestly:

1. **Does the *scope trigger* carry both the primary (provider) and the secondary (deployer of in-scope model) read?** Chapter 09 is explicit that most enterprises are deployers; a row that collapses to the provider scope misses the typical-enterprise case the chapter addresses.
2. **Does the *notes for counsel* field frame the adherence trade-off as a question, not an opinion?** Chapter 09 is explicit: the decision is not the analyst's. A note that recommends adoption or non-adoption is the discipline failing.
3. **Did every uncertain fact carry a `<!-- needs-research: -->` marker?** Chapter 09 names the AI Office code-of-practice page as the verification target for the current Code version and adherent list; markers over guesses.
4. **Does the memo respect the analyst's role boundary?** The memo is a framing document for the governance owner. If a sentence asserts a specific recommendation, the memo has crossed from framing into advocacy.
5. **Is the change-note identifier reserved rather than invented?** Chapter 09 + chapter 10 integration means the analyst anticipates the next Code revision by reserving the identifier now; waiting until the revision lands to invent one is the operational mistake the reservation prevents.

If any of the five is "no", revise *that artefact* before considering the lab done.

## Why this is a lab, not an exercise

The module's five exercises drill the tracker schema (ex 01), crosswalks against the EU and US-state stacks (ex 02), Article 22 flagging (ex 03), the sector overlays (ex 04), and the change-note shape against two scenarios (ex 05). None of them walks a voluntary-code row in the specific case that fits most enterprises — being a deployer of an in-scope GPAI model whose provider has (or has not) adhered to the Code. Chapter 09's integration muscle is the ability to read a voluntary code as *anticipatory intelligence* that shapes the enterprise's vendor-review evidence and its Article 26 deployer-obligation posture without the analyst crossing into the adherence decision itself. This lab exercises exactly that muscle; the failure mode it prevents is the analyst who reads chapter 09 and either (a) collapses the Code row to a provider-shape scope the enterprise is not actually in, or (b) authors a *we should sign* recommendation that is not the analyst's to make.
