# Exercise 03 — Review Packet Composition

**Estimated effort:** 2 hours
**Grounding chapters:** [09 — Composing and Handing Off the Review Packet](../09-composing-and-handing-off-the-review-packet.md); prerequisites in [05 — Summarising Eval Evidence into a Governance-Record Row](../05-summarising-eval-evidence-into-a-governance-row.md) and [08 — Benchmarking Internal Artifacts Against Public References](../08-benchmarking-internal-artifacts-against-public-references.md).

## Objective

Compose the review packet for a specific release gate on a specific system, using the eval rows filed in exercise 01, the vendor rows and benchmark row filed in exercise 02, and any adjacent artefacts from earlier modules (`RSK-`, `IA-`, `REG-`, `CTRL-`). The packet is the analyst's second tangible output of the module — the first being the rows themselves — and is the artefact `ai-evaluation-engineer` uses as primary input to the release-assurance sign-off decision. Its correctness is measured not by how much it says but by whether a receiver who has never opened your rows before can walk from the packet's summary to any underlying piece of evidence in one hop.

After this exercise you should be able to sit down with a heterogeneous stack of eval rows on a system approaching a release gate and produce a defensible, hand-off-ready packet within an hour.

## Prerequisites

- Chapter 09 read; the eight packet sections and the six-step hand-off protocol fresh in memory.
- Chapters 05 and 08 skimmed; the row schema and the benchmark axes open in adjacent tabs.
- Exercise 01's `mod-107-ex-01-eval-rows.md` open — the packet will cite at least two of those rows.
- Exercise 02's `mod-107-ex-02-vendor-benchmark.md` open — the packet will cite both vendor rows and the benchmark row.
- Inventory row (`INV-<year>-<sequence>`) for the system under packet — pick MCDA (`INV-2026-0088`), MCDA-Benefits (`INV-2026-0311` or your equivalent), or the same system used in exercise 02 Part 3 (whichever gives the packet the fullest evidence base).
- Register (`mod-103`) entries, impact-assessment corpus (`mod-105`) entries, regulatory-tracker (`mod-106`) rows, and control-library (`mod-108` — provisional; the module has not been authored yet, so cite by `CTRL-<year>-<sequence>` identifier and note the provisional status) rows that the packet's linkage section will reference.
- A named release gate: pick or invent a specific one. For MCDA: *MCDA v3.7 GA release, target 2026-09-15*. For MCDA-Benefits: *MCDA-Benefits pilot expansion to Colorado deployment, target 2026-10-01*. The named gate anchors the packet's header and shape.

## Problem statement

The deliverable is a **single Markdown file, `mod-107-ex-03-review-packet.md`**, structured as the packet chapter 09 fixes.

### Step 1 — Choose the packet's system and release gate

Populate the packet's header block with:

- **Packet identifier.** `PACKET-2026-EX03-01` (stable; parallels the `PACKET-<year>-<sequence>` convention).
- **System.** The inventory row (`INV-<year>-<sequence>`) and a one-line description.
- **Release gate.** The named release gate; make it specific enough that a reader can identify what deploy or ship decision is being supported (a version identifier, a jurisdiction, an audience expansion — whichever shape fits your enterprise).
- **Packet version and date.** For the exercise, publish as *v1, [today's date]*. Chapter 09's *superseding vs revising* discipline applies if you re-cut mid-exercise.
- **Analyst / preparer.** Named (yours or the role for the exercise).
- **Recipient.** Named `ai-evaluation-engineer` for release-assurance sign-off.
- **Escalation flag.** Boolean plus one-line hook.

### Step 2 — Populate all eight packet sections

Chapter 09's eight sections, in order. Each is required. Under-populating any section is a hand-off failure — the pre-hand-off completeness checklist walks against exactly these.

- **Section 1 — Analyst-tier summary.** One page. Rolled-up residual-risk claim, rolled-up threshold-decision rationale, rolled-up unresolved-findings list, the benchmark gap list, and the analyst's assessment of packet completeness. Chapter 09's discipline: *tensions between rows are stated, not resolved*. If exercise 01's safety-eval row says *above threshold* and the red-team row has an open Medium-severity finding, both are stated.
- **Section 2 — Evidence table.** A structured table listing every cited row: row ID, report type, report title, report date, residual-risk one-liner, threshold-decision status, unresolved-finding count, link. Sorted by report date descending. Populated from exercises 01 and 02.
- **Section 3 — Benchmark row and gap list.** The `BENCH-<year>-<sequence>` row from exercise 02 inline. Every gap itemised — gap ID, description, severity, owner, target closure date, current status.
- **Section 4 — Cross-artefact linkages.** Foreign-key list of every artefact the packet depends on or feeds. At minimum: the inventory row (`INV-`), register entries (`RSK-`), impact-assessment corpus entries (`IA-`), regulatory-tracker rows (`REG-`), control-library entries (`CTRL-`) with a provisional-status note, and any prior packets for the same system.
- **Section 5 — Provenance and reproducibility.** Governance-repository path, row-set commit / version pin, source-artefact snapshot references for public references, and the enumerated refresh triggers.
- **Section 6 — Open follow-ups for `ai-evaluation-engineer`.** A short list of specific questions or asks — usually where an eval configuration warrants receiver review, where receiver technical judgment is needed on an unfamiliar metric, or where the benchmark's Axis-1 or Axis-4 gap requires new eval scoping. Not a punch list of demands; a hand-off note.
- **Section 7 — Escalation hooks.** For any content that requires escalation per chapter 10 (under-evidenced claim, mis-scoped eval, stale eval, packet-cannot-be-handed-off), an inline escalation entry. If there are no escalations, the section explicitly reads *no escalations open at time of hand-off*.
- **Section 8 — Change log.** Version history of the packet itself. For v1, reads *initial packet*. If you re-cut mid-exercise into v2, the delta between versions is enumerated.

### Step 3 — Walk the pre-hand-off completeness checklist

Chapter 09's eleven-check pre-hand-off completeness checklist, walked explicitly at the bottom of the packet as a `## Pre-hand-off completeness check` block. Each check reads *pass* / *pass-with-note [note]* / *fail [reason and remediation]*. The checklist stays in the packet as a record of the analyst's own diligence — auditors read this the same way they read the escalation register.

### Step 4 — Author a short *hand-off protocol log*

At the very end of the packet, a short `## Hand-off protocol` block that walks the six steps chapter 09 fixed (pre-hand-off completeness check → hand-off notification → receiver acknowledgement → receiver review → sign-off decision → post-decision packet closure). For the exercise, populate:

- Steps 1 (completeness check) with an explicit *done, see above* reference.
- Step 2 (hand-off notification) with a mock notification message the analyst would send — packet ID, release-gate name, target sign-off date, escalation flag, link to the packet.
- Steps 3–6 are named as *awaiting* with the expected next-state noted.

The point of the log is not to fake the round-trip. It is to ensure the analyst knows the protocol and would not fall into chapter 09's *silent-file-in-repo hand-off* failure mode.

## Requirements

- **All eight packet sections are populated.** A packet missing any section is not a hand-off-ready packet.
- **The packet is a composition, not a re-authoring.** Chapter 09's discipline. Rows are cited by identifier and linked; their residual-risk / threshold-decision / unresolved-findings content is quoted or referenced, not re-written.
- **The analyst-tier summary contains all four rolled-up elements.** Residual-risk claim, threshold-decision rationale, unresolved-findings, benchmark gap list. A summary missing any element is chapter 09's *summary-only packet* failure mode inverted.
- **Tensions between rows are stated, not resolved.** If exercise 01's safety-eval and red-team rows produce partially-conflicting residual-risk claims, the summary states both. If exercise 02's benchmark surfaces a gap that qualifies but does not block release, the summary says so — an optimistic packet is a broken packet per chapter 09.
- **The evidence table lists every cited row.** Every row cited in the summary or the benchmark appears in the table; every row in the table is cited somewhere else in the packet.
- **Cross-artefact linkages are populated with real identifiers.** No `TBD`s in section 4. Where a downstream artefact does not yet exist (control library is `mod-108` scope; the module has not been authored), the row is cited by the identifier the enterprise would use and flagged with a `<!-- pending-mod-108 -->` marker.
- **Provenance pins a specific row-set version.** A commit hash, a repository tag, or an equivalent version pin — chapter 09's discipline is that a packet from six months ago must be reproducible.
- **Vendor artefact snapshots are referenced.** Live URL plus snapshot / archived URL for the vendor system card and the RSP disclosure (per exercise 02's requirement and chapter 06's *deprecated-card trap*).
- **Refresh triggers are enumerated.** Under what conditions the packet must be re-cut — new eval filed, existing row status transitions to *evidence-stale*, benchmark row's next-benchmark-due date passes, vendor artefact revised, release-gate slips.
- **The follow-ups for `ai-evaluation-engineer` are specific.** *Please advise on scoping the Q4 hallucination eval per Axis 1 gap `BENCH-GAP-2026-EX02-01`* is a follow-up; *please review* is not.
- **The escalation hooks section is honest.** If the underlying rows carry any Class-1 / Class-2 / Class-3 trigger flagged in exercise 01, the packet's escalation hooks section records the trigger and the current disposition. If no escalation is open, the section explicitly reads *no escalations open at time of hand-off*.
- **The pre-hand-off completeness checklist is walked in the packet.** Each of chapter 09's eleven checks is enumerated with a pass / pass-with-note / fail disposition.
- **No cited stale row is silent.** Every cited row's row status (from exercise 01) is honoured; a cited row with status *evidence-stale* is called out explicitly in the packet, per chapter 09.
- **The hand-off protocol log ends the packet.** Six steps, with steps 1–2 authored and steps 3–6 named as *awaiting*.
- **No fabricated content.** All rows cited exist in your exercise 01 / exercise 02 files. Where a linked artefact from an earlier module does not exist (the control library, incident-response entries), the row is cited by identifier and flagged provisional; the analyst does not manufacture the artefact's content.

## Starter guidance

- Populate the header block first, then the evidence table (section 2). The evidence table is the packet's index; once it is done, section 1's summary can be written directly against it and every other section pulls from it. Chapter 09's shape becomes mechanical once the table is in place.
- The analyst-tier summary is the section a busy receiver reads first. Write it last, once the other sections are in place — a summary written before the underlying material is complete will hide gaps the material actually contains. One page is the guide; three paragraphs is often enough.
- The *rolled-up* discipline for the summary is deliberate. Do not simply concatenate the individual residual-risk claims from each cited row; synthesise them. Where the safety-eval row says *96.4% overall safe-answer rate, protected-class 89.0%* and the red-team row says *protected-class analogy-prompt closed under system-prompt v1.8; competitor-disparagement open Medium*, the summary's residual-risk claim is one paragraph that names both the strong-and-weak safety-eval result and the red-team's status of the highest-severity issue.
- Section 4's cross-artefact linkages are the section most commonly under-populated. Walk each artefact family in `mod-102` → `mod-108` explicitly: inventory row, register entries, fairness-review note if the system has one from `mod-104`, impact-assessment entries, regulatory-tracker rows for every jurisdiction the system attaches to, control-library entries with the pending-`mod-108` marker, and any prior packets for the same system. Chapter 09 fixed this list.
- Section 5's row-set commit pin can be a placeholder for the exercise (`git rev-parse HEAD` output at the time of writing, or `commit-<placeholder>`), but the *shape* is real — the packet's reproducibility depends on this being a stable, retrievable pin.
- Section 6 is where the analyst-to-receiver relationship shows. If exercise 01's Inspect-style row used a same-family judge (Claude Opus judging Claude Sonnet), the follow-up should ask the receiver whether that warrants a companion eval with a different-family judge. If exercise 02's benchmark surfaced an Axis-4 gap where the vendor's only external evaluator was named but the enterprise has no independent line of evidence, the follow-up asks the receiver's view on scoping an internal or contracted engagement.
- Chapter 09's *waiting-on-escalation packet* failure mode is worth reading before you write section 7. The correct pattern is *hand off the packet with the escalation entry inline, and let the parallel escalation proceed*. Only the rare Class-4 (packet-cannot-be-handed-off, exercise 04) actually holds the packet.
- The pre-hand-off completeness checklist is not a rubber stamp — walk it honestly. If a check fails, the packet's disposition is *held for remediation* and the packet is not handed off until the remediation is done. For the exercise, if you encounter a legitimate fail on a check, remediate it in the packet before the checklist block records *pass*.
- The hand-off notification message in the hand-off protocol log should be short and structured — packet ID, release-gate name, target sign-off date, escalation flag, link. The enterprise's actual channel (Jira ticket, GRC-platform workflow, Slack message) is out of scope; the message content is what the exercise is testing.

## Acceptance criteria

- `mod-107-ex-03-review-packet.md` filed with a complete packet header and all eight sections (analyst summary, evidence table, benchmark row and gap list, cross-artefact linkages, provenance, follow-ups for `ai-evaluation-engineer`, escalation hooks, change log).
- The analyst-tier summary contains all four rolled-up elements and states any tensions between cited rows without resolving them in the analyst's preferred direction.
- The evidence table lists every cited row with the columns chapter 09 fixed.
- The benchmark row is inline with an itemised gap list carrying ID / severity / owner / target closure date on every gap.
- Cross-artefact linkages are populated with real identifiers from exercises 01 and 02 and from earlier modules (`INV-`, `RSK-`, `IA-`, `REG-`, `CTRL-` with pending-`mod-108` marker, prior packets).
- Provenance pins a specific row-set version and enumerates refresh triggers.
- Vendor artefact snapshot references are captured (live URL plus snapshot).
- Follow-ups for `ai-evaluation-engineer` are specific and named against exercise-01 / exercise-02 row IDs where relevant.
- Escalation hooks section is honest — either lists any open triggers or explicitly reads *no escalations open at time of hand-off*.
- Pre-hand-off completeness checklist walked in the packet, with an explicit pass / pass-with-note / fail disposition per check.
- Hand-off protocol log at the bottom, with steps 1–2 authored and steps 3–6 named as *awaiting*.
- No fabricated content — all rows cited exist in exercise 01 / exercise 02 or in earlier-module artefacts; provisional artefacts flagged as such.

## Stretch goals

- **A v2 re-cut of the packet.** Simulate a mid-release update — a new red-team finding closes overnight, a vendor RSP revision lands, a control-library entry moves from provisional to real. Re-cut the packet as v2, populating the change log (section 8) with the delta since v1 and updating the summary, evidence table, and benchmark accordingly. Chapter 09's *superseding vs revising* discipline applies — same packet ID, new version.
- **A packet for the paired system.** Compose a second packet for the *other* system (whichever of MCDA / MCDA-Benefits you did not use above). This exercises the multi-system packet-flow chapter 09 fixed and gives the analyst practice at maintaining continuity across a portfolio.
- **A council-briefing hook block.** Append a short `## Council-briefing hook` block after section 8 that names the two or three items from the packet that would land in a governance-council briefing per `mod-110`. This wires the packet to the council-facing communication surface `mod-110` will build.
- **A regulator-facing view.** Produce a filtered projection of the packet that would be shared with a regulator or external auditor (removing any internal-only fields, redacting sensitive per-slice numbers if any, and keeping the residual-risk claim, threshold-decision rationale, unresolved-findings list, benchmark gap list, and named external evaluators). Chapter 09 did not fix this projection because it is out of analyst-tier scope for release-assurance; but it is directly useful for `mod-108` and `mod-110`.
- **A hand-off protocol dry-run with a colleague.** If you have a colleague (an `ai-evaluation-engineer` in real life or a track-mate playing the role), walk the six-step protocol against them. Capture the round-trip questions in the hand-off protocol log and update the packet against them. This is the most valuable stretch because it surfaces the *questions-you-did-not-anticipate* class of gap the checklist cannot catch on its own.

## Deliverables

- `mod-107-ex-03-review-packet.md` — a complete review packet with all eight sections, a pre-hand-off completeness checklist, and a hand-off protocol log.
- Optional stretch artefacts named clearly.

## Notes on evaluation

The paired solutions repo works one reference packet shaped around MCDA v3.7 GA release, citing the illustrative rows chapters 02, 04, 05, and 08 use throughout. Yours will differ in the system, the release gate, and the specific rows cited from exercises 01 and 02. What should not differ is (a) all eight sections are populated, (b) the analyst summary rolls up all four elements and states tensions honestly, (c) the evidence table lists every cited row and every row in the table is cited elsewhere, (d) cross-artefact linkages are populated with real identifiers rather than `TBD`, (e) provenance pins a row-set version and enumerates refresh triggers, (f) the completeness checklist is walked in the packet, and (g) the hand-off protocol log names the six steps. A packet that meets these seven conditions is one an `ai-evaluation-engineer` could actually use as release-assurance sign-off input; a longer packet that leaves any of them under-populated is not.
