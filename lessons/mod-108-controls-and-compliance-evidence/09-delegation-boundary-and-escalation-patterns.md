# Delegation Boundary and Escalation Patterns

## Why this chapter

Chapters 01–08 defined the analyst's outputs (the control-status report, the vendor-risk-register row set, the crosswalk), the tagging conventions, and the reading practices. This closing chapter states the full delegation-boundary map operationalised across those outputs and defines the four escalation classes the analyst uses when work outgrows the analyst's scope.

The delegation boundary is not a soft preference. In every earlier chapter, the analyst's job stopped at a specific handoff — the master control library at `senior-ai-governance-architect`, the security exploit at `ai-infra-security`, the contract at `procurement` / `legal`, the operating-effectiveness opinion at `internal-audit`, the accredited certification at the external body. Cross those lines silently and the enterprise's assurance posture degrades: `senior-ai-governance-architect` loses visibility of library changes that were made without them; `ai-infra-security` misses findings that were closed without them; `internal-audit` reads a report that already contains an opinion; `legal` finds out at renewal that a term was accepted informally. The escalation register — the queue this chapter fixes — is the mechanism that makes the boundary auditable.

## The full delegation-boundary map

The preview from chapter 01, stated in full and cross-referenced to the chapters where each row was operationalised.

| Artefact / action | Owner | Analyst's role | Chapter reference |
|---|---|---|---|
| Master control library — content, wording, cadence, evidence-class expectations | `senior-ai-governance-architect` | Reads the library, tests against it, raises library-level gaps as escalations | 01, 02, 03, 07 |
| Periodic control test — scoping, pulling, attaching, flagging stale | `ai-governance-analyst` | Owns | 02 |
| Control-status report | `ai-governance-analyst` | Owns; pre-issuance review with `senior-ai-governance-architect`; issues to `internal-audit` | 03 |
| Internal-audit opinion on operating effectiveness | `internal-audit` | Supplies the report; does not opine | 03 |
| Security threat analysis, exploit reproduction, pentest, mitigation code | `ai-infra-security` | Recognises the category (OWASP, ATLAS technique, AI 100-2 family, SAIF area); tags; files; routes | 04, 05 |
| Red-team engagement (execution) | `ai-red-team-engineer` | Reads the report; carries ATLAS identifiers forward; does not construct payloads | 05 |
| Application-security review (LLM05 output-handling class) | `application-security` | Files finding; routes; does not evaluate mitigation code | 04 |
| Third-party AI vendor / model / dataset intake reading | `ai-governance-analyst` | Owns the vendor row | 06 |
| Contract negotiation and DPA redlining | `procurement` / `legal` | Supplies the row; does not sign or redline | 06 |
| DPA acceptance for personal-data processing | `data-protection-officer` | Escalates on personal-data or special-category triggers | 06 |
| Analyst-tier controls crosswalk | `ai-governance-analyst` | Owns; projections only; does not edit the master library | 07 |
| Master-library revision on gap or drift | `senior-ai-governance-architect` | Raises the gap; re-populates the crosswalk after the revision lands | 07 |
| External accredited certification (ISO/IEC 42001, SOC 2, other) | External accredited body, enterprise led by `head-of-ai-governance` / `senior-ai-governance-architect` | Supplies documentation; does not audit the enterprise's own systems | 08 |
| Independent audit (ForHumanity-linked, BABL-linked, other) | External auditor | Reads the report; records auditor + credential + criteria + opinion; escalates exceptions | 08 |
| Independent audit commissioning | `head-of-ai-governance` / `senior-ai-governance-architect` (with `procurement`) | Supports scoping; does not sign engagement letter | 08 |
| Statutory bias-audit publication (Local Law 144 and analogues) | Enterprise executive per statute; supported by `legal` | Records the audit + publication URL as evidence on the control test | 08 |
| Post-incident control re-test | `ai-governance-analyst` (on trigger from `mod-109`) | Owns; the trigger is the incident, not the cycle date | 09 (of this module); `mod-109` |

The line pattern is consistent: the analyst reads, tags, files, tests, rows, reports, and hands off. The analyst does not author library statements, exploit, negotiate, sign, opine, or audit the enterprise's own systems.

## The four escalation classes

Every artefact this module produces can generate an escalation. Four classes cover the field; the analyst files under whichever fits, with the same rationale-plus-requested-action-plus-target-date shape.

### Class 1 — Library-design fix needed

- **Trigger.** A control that repeatedly fails or deviates for a structural reason (evidence class not produceable at the enterprise; statement ambiguous; owner unassigned; cadence unrealistic; test un-runnable at scale without a sampling rule the library does not specify). A crosswalk gap (uncovered obligation, uncovered control, mis-anchored control, drift).
- **Owner of the escalation.** `senior-ai-governance-architect`.
- **What the analyst supplies.** The rationale (which control, which structural reason, evidence of the recurrence), the requested library change (typically re-wording, cadence-change, or owner-reassignment; the analyst does not propose the wording), and the affected inventory and framework anchors so the architect can see the blast radius.
- **What the analyst does not do.** Rewrite the control statement. Re-anchor the framework citations on their own initiative. Silently drop the control from the next-period scope.
- **Example.** *Control CTL-2026-0341 (jailbreak-classifier fires on ≥ 0.85) has deviated in two consecutive quarters due to the log-sample platform being unable to produce the should-have-fired-but-did-not subset. Requesting library-level review of the control's evidence-class expectation and, if the platform cannot be extended, a re-statement toward an evidence class that can be produced.*

### Class 2 — Security route to `ai-infra-security`

- **Trigger.** A security-linked finding surfaced through control testing, an incident, a red-team engagement report, a vendor notice, or a monitoring alert.
- **Owner of the escalation.** `ai-infra-security`, with the ML / infra / product owner copied.
- **What the analyst supplies.** The OWASP LLM 2025 tag (chapter 04); the AI 100-2 attack-class citation if applicable; the ATLAS technique identifier if the source artefact names one; the affected `INV-<year>-<sequence>` systems; the evidence artefact link.
- **What the analyst does not do.** Set severity. Reproduce the exploit. Draft the mitigation code. Close the finding based on their own assessment.
- **Example.** *Red-team engagement RE-2026-0018 identified a prompt-injection variant against INV-2026-0091 (support-chat-copilot). Tagged LLM01:2025 — Prompt Injection (indirect variant); AI 100-2e2025 — Evasion; ATLAS AML.T0051 per the RE report. Routing to `ai-infra-security` for triage and severity; ML platform owner copied.*

### Class 3 — Vendor / contract action

- **Trigger.** A vendor-intake finding that requires action outside the analyst's scope — a new sub-processor added in a jurisdiction outside the enterprise's approved footprint, a DPA that requires re-negotiation, a certification lapse, a security-questionnaire response that contradicts the vendor's published evidence, a personal-data processing purpose not covered by the current contract.
- **Owner of the escalation.** Contract owner (`procurement` / `legal`), with `data-protection-officer` copied where personal data is in scope, `ai-infra-security` copied where security is in scope, and the technical owner copied for context.
- **What the analyst supplies.** The vendor row identifier (`VND-<year>-<sequence>`), the specific column that surfaced the finding, the vendor-side evidence (URL, snapshot date, response document), and the requested action ("*re-negotiate DPA to reflect new sub-processor jurisdiction*"; "*request current ISO/IEC 42001 certification letter*"; "*pause new use of vendor artefact pending resolution*").
- **What the analyst does not do.** Redline the DPA. Negotiate a term. Sign anything. Pause vendor use unilaterally without executive sign-off — the request is *requested pause*, and the accountable executive decides.
- **Example.** *VND-2026-0044 (Vendor X's hosted-model service) sub-processor list snapshot 2026-05-12 lists a new sub-processor in Jurisdiction Y, outside the enterprise's approved data-transfer footprint. DPA does not reference Jurisdiction Y. Routing to `procurement` and `data-protection-officer` for DPA re-review; requested action: pause net-new use of INV-2026-0091 (support-chat-copilot) pending resolution.*

### Class 4 — Governance-council decision

- **Trigger.** A finding whose resolution requires a decision the analyst, `senior-ai-governance-architect`, `ai-infra-security`, or `procurement` cannot make alone — a residual-risk acceptance beyond a named threshold, an enterprise-wide policy change, a control-library re-design that affects multiple business units, an incident whose remediation crosses functional lines.
- **Owner of the escalation.** The governance council, with `head-of-ai-governance` as convener.
- **What the analyst supplies.** The full context (which finding, which artefacts, which affected systems, which chapters of the module lead to the escalation), the requested decision, and the recommendation from `senior-ai-governance-architect` (obtained during the pre-issuance review — chapter 03).
- **What the analyst does not do.** Take the decision. Withdraw the escalation because a downstream team promised remediation. Downgrade the class to a lower one to avoid the council slot.
- **Example.** *Three separate control failures across INV-2026-0088, INV-2026-0091, and INV-2026-0104 in the current quarter map to a shared root cause in the enterprise's guardrail-classifier release cadence. The pattern requires a decision on whether to pause new high-tier deployments pending a classifier re-architecture. Escalating to the governance council for decision at the next meeting; `senior-ai-governance-architect` recommends option B (pause net-new high-tier deployments; existing systems continue with heightened monitoring).*

## The escalation register

The register is the persistent record of the four classes. Every entry carries the same shape.

| Column | Content |
|---|---|
| Escalation ID | `ESC-<year>-<sequence>` |
| Filed date | The analyst's action date |
| Class | 1, 2, 3, or 4 |
| Trigger source | Chapter / artefact that surfaced it — control test ID, vendor row ID, incident ID, crosswalk gap |
| Affected systems / vendors | `INV-<year>-<sequence>` and `VND-<year>-<sequence>` identifiers |
| Rationale | One paragraph — why this needs escalation, evidence of recurrence, blast radius |
| Requested action | What the analyst asks the escalation owner to do |
| Escalation owner | Role or named person |
| Target date | When the analyst expects an answer |
| Status | *open*, *in-progress*, *resolved*, *withdrawn* |
| Resolution note | What was decided; the resolving artefact identifier; the resulting library / control / vendor changes |
| Roll-up reference | The control-status report (`CSR-<year>-<period>`) that carried this escalation into §5 |

The register lives in the GRC platform; the roll-up view (open escalations per class per period) feeds the control-status report §5 (chapter 03) and the council briefings (`mod-110`).

## The pattern language for library-level policy work

Repeated escalations of the same class against the same control, control family, or vendor pattern become *policy work* — a signal that library design, vendor-management policy, or enterprise-wide practice needs revision beyond a single fix. The analyst does not do the policy work but does surface the pattern.

- **Three same-control library-design-fix escalations in a rolling year.** Pattern: this control keeps not working as-worded. Recommend to `senior-ai-governance-architect` that the control be re-scoped or removed.
- **Recurrent LLM01 findings across multiple systems.** Pattern: enterprise-wide guardrail architecture is not keeping pace. Recommend to `senior-ai-governance-architect` and `ai-infra-security` that a platform-level guardrail solution be evaluated.
- **Multiple vendor rows where the DPA position is negotiated post-signature.** Pattern: procurement's model DPA is not carrying enough AI-specific coverage. Recommend to `procurement` and `legal` a model-DPA revision.
- **Council-decision escalations resolving with *no decision*.** Pattern: the council is under-resourced for the volume of AI decisions. Recommend to `head-of-ai-governance` that decision-rights be delegated or that the council cadence increase.

These are pattern-recognitions, not policy proposals. The analyst raises the pattern; the roles that own the underlying artefact set the policy.

## When to file up rather than across

Not every difficulty is an escalation. A first-instance control failure with a clear owner and a clear follow-up path is a *finding* on the control-status report, not an escalation. The threshold for opening an escalation register entry is one of:

- The issue recurs across two or more periods without resolution.
- The issue requires action from a role other than the finding's control owner.
- The issue is not resolvable within the current control-cycle window.
- The issue affects multiple systems, multiple vendors, or multiple frameworks.
- The issue exposes a gap in the master library, the crosswalk, or the vendor-intake process itself.

Otherwise: file as a finding on the control-status report §4 with the follow-up action and owner (chapter 03), and re-test at the next scoped date.

## When to escalate around a blocked resolution

The escalation owner may not act. The analyst does not silently absorb the block.

- **Escalation owner does not respond by the target date.** The analyst re-issues with the target date restated and copies the owner's manager. If the second request is not answered, the analyst raises the block itself as a class-4 (governance-council decision) escalation with the original escalation attached.
- **Escalation owner declines with rationale.** The analyst records the declination on the escalation entry (*status: withdrawn — declined by owner: rationale*) and, where the finding still merits action, considers whether the case belongs at a higher class or a different owner. Declination is a legitimate outcome; silent withdrawal is not.
- **Escalation owner declines without rationale.** The analyst asks for the rationale; failing that, raises to the owner's manager. Silent decline without rationale is a governance failure the analyst does not accept.

## Cross-module escalation flow

The escalation register does not live in isolation. Findings that arise from `mod-108` control testing may originate in adjacent modules and flow back to them.

- **`mod-103` — risk register.** A control-status finding may indicate a register-entry residual-risk claim is no longer defensible. The analyst opens a *residual-risk re-open* request against the register entry with the finding attached.
- **`mod-105` — impact-assessment corpus.** A control-status finding tied to a *measure* named in an impact assessment triggers a review-trigger on the assessment (per `mod-105` chapter 08's walk discipline).
- **`mod-106` — regulatory tracker.** A crosswalk drift often surfaces when the tracker registers a material change; the escalation flows back to the tracker for confirmation of the obligation's current shape.
- **`mod-107` — eval-evidence rows.** A control that cites an eval-evidence row that has itself gone stale triggers a re-run request to `ai-evaluation-engineer` (per `mod-107` chapter 09's hand-off).
- **`mod-109` — incident response and continuous monitoring.** An incident triggers a control re-test outside the periodic cycle; the incident's post-mortem may generate class-1 or class-4 escalations that feed back to this module's register.
- **`mod-110` — communication and council support.** The roll-up of open escalations feeds the council briefings' policy-work agenda.

The register is the connective tissue. Escalation IDs (`ESC-<year>-<sequence>`) referenced from other modules' artefacts let a reader walk the full path from a single finding to the policy work it drove.

## Common failure modes

- **Silent library edits.** The analyst tightens a control statement to make the test pass and does not tell `senior-ai-governance-architect`. Fix: the library edit is the escalation; the test result reflects the library as it stood at test time.
- **Escalations that resolve as *the team promised to fix it*.** The escalation is closed on a verbal commitment with no dated artefact. Fix: resolution requires a resolving artefact identifier — a library-change identifier, a security ticket, a contract amendment, a council-minute reference. Verbal commitments do not close escalations.
- **Class-4 escalations that never reach the council.** The analyst files a class-4 but the roll-up view lists it as class-2. Fix: the class is the analyst's determination at filing; downgrades require a `senior-ai-governance-architect` co-sign on the register entry.
- **Registers that grow without triage.** Open escalations accumulate quarter over quarter with no resolution or withdrawal. Fix: the control-status report §5 lists open escalations by age; the council reads this and prompts closure.
- **Escalations that duplicate the control-status report §4 findings.** The analyst files an escalation for every finding, defeating the finding-vs-escalation distinction. Fix: apply the threshold set above.

## What to memorise

- **The delegation map is fifteen rows.** The analyst reads, tags, files, tests, rows, reports, and hands off — nothing more, nothing less.
- **Four escalation classes** — library-design fix, security route, vendor / contract action, governance-council decision.
- **The escalation register is a persistent record** with a consistent row shape; the roll-up feeds §5 of the control-status report and the council briefings.
- **File-up threshold.** Recurrence across periods, out-of-scope-for-current-window, cross-role, cross-system, or exposing a process gap. Otherwise it is a finding, not an escalation.
- **Blocked resolutions escalate to the owner's manager, then to class 4.** Silent absorption is not an option.
- **Cross-module flow** goes through the register: escalation IDs are the walking path from finding to policy work.

## Summary

This chapter closes the module by stating the full delegation-boundary map operationalised across every earlier chapter and defining the four escalation classes — library-design fix, security route, vendor / contract action, governance-council decision — the analyst uses when work outgrows the analyst's scope. The escalation register is the persistent audit-facing record; the roll-up feeds the control-status report and the council briefings; escalation IDs are the walking path when a finding grows into policy work. The analyst reads, tags, files, tests, rows, reports, and hands off. The specialists — `senior-ai-governance-architect` at the master library, `ai-infra-security` at the exploit, `procurement` / `legal` at the contract, `internal-audit` at the opinion, external accredited bodies at certification — own the artefacts they own. The module ends where the enterprise's assurance posture rests: on the two artefacts the analyst produces (the control-status report and the vendor-risk-register row set) and on the register of escalations that connects the analyst's cycle to every other role's work.
