# Composing and Handing Off the Review Packet

## Why this chapter

Chapters 02–08 built the artefacts: internal eval rows (chapters 02–05), vendor system-card rows (chapter 06), vendor RSP disclosure rows (chapter 07), and benchmark rows with gap lists (chapter 08). This chapter turns them into a single, hand-off-ready packet that `ai-evaluation-engineer` uses as input to the release-assurance sign-off decision.

The packet is the analyst's second tangible output of this module (the first being the rows themselves). It is not a memo, not a summary email, and not a slide deck. It is a versioned, cited, structured deliverable filed into the governance repository, referenced from the release-assurance workflow, and handed across a role boundary with a clear expectation of what the receiver will do with it.

## What the packet is (and is not)

The review packet is:

- **A per-release-decision artefact.** One packet per system per release gate. A monthly re-cut of the same MCDA packet for the same release window is one packet with version history, not four independent packets.
- **A composition of existing rows.** The packet does not re-author the underlying rows; it references them and adds a synthesis layer.
- **A hand-off document.** Its audience is `ai-evaluation-engineer` (primary), the model / product owner (secondary), and — through them — the release-assurance workflow's downstream consumers (release manager, principal engineer, governance council for council-relevant releases).
- **Auditable.** A packet from six months ago must be readable and reproducible from the referenced rows.

The packet is **not**:

- The release-assurance sign-off itself. Sign-off is `ai-evaluation-engineer` scope with (per enterprise policy) further counter-signatures.
- A restatement of the eval reports. The reports are cited; not re-summarised.
- The analyst's opinion on whether the system should ship. The analyst's role is to package the evidence and surface the gaps; the ship / no-ship call is the accountable role's.
- A one-off document. Every release cycle produces a packet; every material change to a system in-cycle produces a packet update.

## The packet structure

The analyst-tier packet has these sections. Structure matches the shape `ai-evaluation-engineer` expects for release-assurance input:

### Header

- **Packet identifier.** `PACKET-<year>-<sequence>`, stable, never re-used.
- **System.** Inventory row (`INV-<year>-<sequence>`) with one-line description.
- **Release gate.** The named release gate this packet supports (e.g., *MCDA v3.7 GA release, target 2026-09-15*).
- **Packet version and date.** Version identifier and packet publication date.
- **Analyst / preparer.** Named person.
- **Recipient.** Named `ai-evaluation-engineer` for release-assurance sign-off.
- **Escalation flag.** Boolean plus one-line hook — is there any content in the packet requiring escalation per chapter 10?

### 1 — The analyst-tier summary

One page. The synthesis the receiver reads first. Structured as:

- **Residual-risk claim (rolled up).** One or two sentences that consolidate the residual-risk claims from every internal `EVAL-<year>-<sequence>` row cited. Where two rows produce residual-risk claims that partially conflict (a safety eval says the system is above threshold; a red-team says the system has an open Medium-severity finding), the packet states both and does not silently resolve the tension.
- **Threshold-decision rationale (rolled up).** Which internal thresholds and which vendor thresholds have been met, which have not, and against what named references. Cross-reference each to the underlying row.
- **Unresolved findings (rolled up).** The union of every unresolved-findings list across the cited rows, deduplicated, with severity, owner, and target closure date on each item.
- **Benchmark gap list.** The gap list from the paired `BENCH-<year>-<sequence>` row (chapter 08), with severity and target closure date on each item.
- **Analyst's assessment of packet completeness.** One paragraph: does the packet's evidence cover the full risk surface for this system's use case? If not, what is missing? This paragraph is not a ship / no-ship recommendation; it is a completeness statement.

### 2 — The evidence table

A structured table listing every row the packet cites. Columns: row ID, report type, report title, report date, residual-risk one-liner, threshold-decision status, unresolved-finding count, link. Sorted by report date descending.

The evidence table is the receiver's index into the underlying material. It exists so `ai-evaluation-engineer` can walk any specific row without hunting for it.

### 3 — The benchmark row and gap list

The full paired `BENCH-<year>-<sequence>` row from chapter 08, with each gap itemised — gap ID, description, severity, owner, target closure date, current status. Gaps that have closed since the last packet version are marked *closed as of [date]* and retained for continuity.

### 4 — Cross-artefact linkages

Foreign-key list of every artefact the packet's rows depend on or feed:

- Inventory rows (`INV-<year>-<sequence>`).
- Register entries (`RSK-<year>-<sequence>`) — from `mod-103`.
- Fairness-review notes — from `mod-104`.
- Impact-assessment corpus entries (`IA-<year>-<sequence>`) — from `mod-105`.
- Regulatory-tracker rows (`REG-<year>-<sequence>`) — from `mod-106`.
- Controls (`CTRL-<year>-<sequence>`) — from `mod-108`.
- Prior packets for the same system (`PACKET-<year>-<sequence>`) — for continuity.

The receiver uses this section to verify that the packet is embedded in the broader governance corpus and is not a standalone piece of evidence.

### 5 — Provenance and reproducibility

- **Governance-repository location** — path to the packet and the underlying rows.
- **Row-set frozen at.** A commit / version pin of the row set as it stood when the packet was cut. If a row changes after the packet is cut, the packet is superseded; a new version is issued.
- **Source-artefact snapshot references.** For public references (vendor system cards, vendor RSPs), the snapshot / archived URL alongside the live URL — vendor URLs move.
- **Refresh triggers.** Under what conditions the packet must be re-cut (new eval row filed; existing row status transitions to *evidence-stale*; benchmark row's next-benchmark-due date passes; vendor artefact revised).

### 6 — Open follow-ups for `ai-evaluation-engineer`

A short list of specific questions or asks for the receiver — usually where an internal eval configuration warrants review, where the receiver's technical judgment is needed on an unfamiliar metric, or where the benchmark's Axis-1 or Axis-4 gap requires new eval scoping. Not a punch list of demands; a hand-off note.

### 7 — Escalation hooks

For any content that requires escalation per chapter 10 (under-evidenced claim, mis-scoped eval, stale eval), the packet includes an inline escalation entry — what the escalation is, who it's routed to, current status. The packet does not delay hand-off waiting for the escalation to close; the two proceed in parallel.

### 8 — Change log

Version history of the packet itself — what changed between v1 and v2, which rows were added, which gaps closed, which new findings surfaced.

## The hand-off protocol

The packet does not become evidence for release-assurance sign-off by being filed. It becomes evidence by being *handed off* under a protocol that both roles recognise. The analyst-tier hand-off protocol:

1. **Pre-hand-off completeness check.** The analyst walks the packet against a checklist (below). Any incomplete field is either filled or explicitly flagged as *acknowledged incomplete with reason [X]*. Empty fields go to the receiver as gaps, not as accidents.
2. **Hand-off notification.** The analyst notifies `ai-evaluation-engineer` (via whatever channel the enterprise uses — Jira ticket, GRC-platform workflow, structured Slack message with a link) that the packet is ready. The notification carries the packet ID, the release-gate name, the target sign-off date, and any escalation flag.
3. **Receiver acknowledgement.** `ai-evaluation-engineer` acknowledges receipt (again via the enterprise's channel of record). Acknowledgement records the receiver, the acknowledgement date, and confirms the release gate.
4. **Receiver review.** `ai-evaluation-engineer` performs the release-assurance review using the packet as its primary input, drawing on the packet's evidence table to walk any specific row. During review, the receiver may return questions to the analyst; these round-trips are recorded on the packet.
5. **Sign-off decision.** `ai-evaluation-engineer` (with counter-signatures per enterprise policy) records the release-assurance decision as its own artefact, cross-linked back to the packet ID. The analyst is copied on the decision record but does not co-sign.
6. **Post-decision packet closure.** The packet's row status transitions to *sign-off-recorded* (if approved), *sign-off-conditional* (if approved with conditions the analyst must track), or *sign-off-declined* (if the release-assurance decision is *do not ship at this gate*). Each transition is recorded on the packet.

The protocol is deliberately explicit. A hand-off that happens by silent-file-in-a-repository is not a hand-off; it is a gamble that the receiver will find it.

## The pre-hand-off completeness checklist

Before notification, the analyst walks the packet against this checklist. Any *no* is either fixed or explicitly flagged:

- Every cited row has a stable identifier, a source-artefact link, and a last-verified date within its refresh cadence.
- The analyst-tier summary contains the four rolled-up elements (residual-risk claim, threshold-decision rationale, unresolved-findings, benchmark gap list).
- The evidence table is complete: every row the summary references is in the table, and every row in the table is cited in the summary or in the benchmark.
- The benchmark row is cited and its gap list is inline in the packet.
- The cross-artefact linkage section is populated — no untracked dependencies.
- The provenance section names the governance-repository location and pins the row-set at a specific commit / version.
- The refresh triggers are enumerated.
- The escalation-hooks section either lists any escalations in flight or explicitly reads *no escalations*.
- The change log is populated (or, for v1, reads *initial packet*).
- No cited row's *row status* is *evidence-stale* or *escalated* without being explicitly acknowledged in the packet.
- The recipient is named; the release-gate name is precise; the target sign-off date is populated.

An eleven-check pass. A missed check is a hand-off failure the analyst catches, not one the receiver has to.

## The packet in the multi-system context

Enterprises with more than a handful of AI systems will produce many packets per quarter. The analyst-tier discipline for the multi-system context:

- **One packet per release gate.** Multi-system rollups (e.g., *all Q3 releases*) may be produced by `ai-evaluation-engineer` or by the governance council for their own consumption; the analyst produces per-system per-gate packets.
- **Packet identifiers are stable across versions.** Version v1, v2, v3 of a packet all share the packet ID; the version identifier disambiguates. Never re-use packet IDs.
- **Continuity across packets.** For a system that has had prior packets, section 4 (cross-artefact linkages) lists the prior packets and section 8 (change log) summarises what changed since the most recent prior packet.
- **Superseding vs revising.** A packet is *revised* while the release gate is open (adding evidence, closing gaps, incorporating updates). A packet is *superseded* when the release gate closes and a new gate opens; the new gate gets a new packet.
- **Retirement.** When a system is decommissioned or its release cycle ends, the associated packets transition to *retired* status and remain read-only in the governance repository for the audit-retention window.

## Failure modes

- **The summary-only packet.** The analyst writes a strong summary and omits the evidence table, benchmark row, and cross-artefact linkage sections. The receiver has no path to walk the underlying material. The packet is filed but is not evidence.
- **The evidence-dump packet.** The analyst references twelve rows without a summary or a benchmark synthesis. The receiver is left to construct the synthesis themselves; the hand-off degenerates into the receiver re-doing the analyst's work.
- **The optimistic-summary packet.** The summary resolves tensions between conflicting rows in the analyst's preferred direction (a safety eval passes, a red-team finding is open; the summary says *safety controls in place*). The receiver has to unpick the summary to find the tension. Truthful packets state tensions; optimistic ones hide them.
- **The stale-row packet.** The packet cites a row whose row status is *evidence-stale* and does not acknowledge the staleness. When the receiver notices, trust in the packet collapses. Every cited stale row is called out explicitly.
- **The waiting-on-escalation packet.** The analyst delays packet hand-off until an in-flight escalation resolves. Meanwhile the release gate approaches. The correct pattern: hand off the packet with the escalation entry inline, and let the parallel escalation proceed. Chapter 10 covers when a packet cannot be handed off at all (rare).
- **The silent-file-in-repo hand-off.** The analyst files the packet without notification. The receiver never sees it. No release-assurance sign-off happens; the release either slips or ships without evidence.

## A worked packet — MCDA v3.7 GA release

Bringing forward the MCDA illustrative examples from chapters 05 and 08:

- **Header.** *PACKET-2026-114, MCDA (`INV-2026-0088`), release gate: MCDA v3.7 GA target 2026-09-15, packet v2, published 2026-08-25, analyst: [name], recipient: [ai-evaluation-engineer], escalation flag: no.*
- **Section 1 — Analyst summary.** *MCDA v3.7 is deployed on `anthropic/claude-3-5-sonnet-20241022` with system prompt v1.8. Internal safety eval `EVAL-2026-088` reports 96.4% safe-answer rate overall (above the internal 95% threshold). Red-team engagement `EVAL-2026-091` closed the protected-class-generalisation High-severity finding under system-prompt v1.8; two Medium-severity findings remain open with owners and closure dates within the release window. Benchmark `BENCH-2026-014` against the paired vendor system card and RSP disclosure identifies two gaps: hallucination coverage (scheduled for Q4) and customer-visible AI-disclosure marker (closure 2026-09-30). Packet is complete in the sense that all applicable internal evals have been filed; the hallucination coverage gap is acknowledged and does not block the current release per the internal release-gating policy.*
- **Section 2 — Evidence table.** Row list — `EVAL-2026-088` (safety-eval, 2026-07-14), `EVAL-2026-091` (red-team, 2026-08-15), `EVAL-2026-102` (vendor-system-card for `claude-3-5-sonnet-20241022`), `EVAL-2026-103` (vendor-rsp-disclosure), `BENCH-2026-014` (benchmark).
- **Section 3 — Benchmark row and gap list.** `BENCH-2026-014` full row inline. Gaps: `BENCH-GAP-2026-014-01` (hallucination coverage, Med, owner `ai-evaluation-engineer`, target 2026-Q4); `BENCH-GAP-2026-014-02` (AI-disclosure marker, Med, owner MCDA product owner, target 2026-09-30).
- **Section 4 — Cross-artefact linkages.** `INV-2026-0088`; `RSK-2026-0088-04`, `RSK-2026-0088-07`; `IA-2026-0088`; `REG-2026-US-STATE-003` (Colorado AI Act), `REG-2026-US-STATE-005` (NYC LL 144); `CTRL-2026-042`; prior packet `PACKET-2026-096` (MCDA v3.6 release).
- **Section 5 — Provenance.** Governance-repository path; row-set pinned at commit `abc1234`; vendor artefact snapshots archived at `[path]`; refresh triggers: new eval filed, benchmark next-due 2026-11-01, vendor RSP revision.
- **Section 6 — Follow-ups for `ai-evaluation-engineer`.** *(a) Please advise on scoping and dataset selection for the Q4 hallucination-under-grounding eval for MCDA (Axis 1 gap). (b) The safety-eval judge model is same-family (Claude Opus judging Claude Sonnet); interested in your view on whether that warrants a companion eval with a different-family judge for calibration.*
- **Section 7 — Escalation hooks.** *None open.*
- **Section 8 — Change log.** *v1 (2026-08-20): initial packet with `EVAL-2026-088` and vendor rows. v2 (2026-08-25): added `EVAL-2026-091` (red-team completed), added `BENCH-2026-014`, updated summary and evidence table.*

The packet is filed, `ai-evaluation-engineer` is notified, acknowledgement is recorded, and the release-assurance review begins.

## What to memorise

- **One packet per system per release gate.** Versioned across the release cycle; superseded when the gate closes.
- **The packet is a composition, not a re-authoring.** It cites the rows, adds the summary and benchmark, and hands off.
- **The eight sections** — header, analyst summary, evidence table, benchmark row, cross-artefact linkages, provenance, follow-ups, escalation hooks, change log.
- **The hand-off protocol is explicit** — pre-check, notify, acknowledge, review, sign-off, closure.
- **Tensions between rows are stated, not resolved.** An optimistic packet is a broken packet.
- **Every cited stale row is called out.** Silent staleness is a hand-off failure.

## Summary

The review packet is the analyst's hand-off artefact. It composes the internal `EVAL-<year>-<sequence>` rows, the paired vendor-card and RSP rows, and the benchmark row with gap list into a per-release-gate deliverable that `ai-evaluation-engineer` uses as primary input to release-assurance sign-off. Its eight sections structure the composition; the hand-off protocol structures the exchange between roles. The packet is auditable, versioned, and pinned to a specific row-set commit so that a reader six months later can walk the evidence. Chapter 10 closes the module with the delegation boundary the packet crosses and the escalation protocol for the cases the packet cannot cross the boundary on its own.
