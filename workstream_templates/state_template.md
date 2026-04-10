# Workstream State: <Workstream Name>

Use this file as the one living continuity record for a repo workstream.
Keep same-target fix loops inside this file and this workstream.
Open a new workstream only when the target outcome or scope changes materially.
When the workstream needs a larger contract, keep it as sibling `spec.md` in
the same directory.

If there is no formal spec, the minimal contract section below is still
required.
`spec-less` is allowed here, but never `contract-less`.

## Workstream Status

- Workstream ID: `<ws-001-short-name>`
- Overall status: `<draft|in_progress|candidate|blocked|done>`
- Current stage: `<clarify/specify|implement|verify>`
- Latest verdict: `<pending|pass|blocked>`
- Spec file: `<spec.md|none>`
- Current planned slice: `<S1|S2|none>`
- Next role: `<spec-author|runtime-implementer|runtime-verifier|user>`
- Next action: `<single concrete next action>`

## Minimal Contract Snapshot

- Objective: `<value>`
- In scope now: `<value>`
- Out of scope now: `<value>`
- Acceptance target: `<value>`
- External authority recheck requirement: `<required via spec.md#external-authority-sources / state-local external source set / N/A>`
- Source request or link: `<value>`

## Source Links

1. Formal spec artifact: `<spec.md or none>`
2. Clarification artifact: `<clarification.md or none>`
3. Relevant architecture docs: `<path(s) or N/A>`
4. External authority source set: `<spec.md#external-authority-sources / state-local external source set / N/A>`
5. Related failure artifacts: `<path(s) or N/A>`
6. Helper artifacts in use (`plan`, `tasks`, etc.): `<path(s) or N/A>`

## Clarification Status

- Clarification complete: `<yes|no>`
- Contract source: `<clarification.md / spec.md + section anchor / this file>`
- Open user questions: `<none or short list>`
- Explicit deferred decisions: `<none or short list>`

## Current Truth

- Slice summary: `<value>`
- Current scope statement: `<value>`
- Changed surface: `<files or modules in scope>`
- Current blocker or risk: `<value or none>`

## Semantic Execution Map

- User-visible truth to change: `<value or N/A>`
- Canonical owner: `<value or N/A>`
- Causal seam: `<value or N/A>`
- Tempting wrong local patch: `<value or N/A>`
- Runtime path that must be proven: `<value or N/A>`
- External authority seam and source set: `<value or N/A>`

## Evidence Ledger

Allowed status values: `pass`, `fail`, `blocked`, `not_run`.
Keep table cells short and scannable. Put long commands, output snippets, and
nuanced explanations in `Evidence Details`, not inside table cells.

| Evidence ID | Check / Scenario | Status | Timestamp | Summary |
|---|---|---|---|---|
| `EV-01` | `<short label>` | `<status>` | `<timestamp>` | `<one-sentence outcome>` |

## Evidence Details

- `EV-01`: `<exact command, output snippet, nuance, and why it matters>`

## External Authority Evidence

- Source set artifact: `<spec.md#external-authority-sources / state-local external source set / N/A>`
- Implementer authority recheck evidence: `<ledger row(s) / implementer handoff / N/A>`
- Verifier authority audit evidence: `<verifier verdict / ledger row(s) / N/A>`

## Requirement Status Snapshot

Allowed status values: `open`, `candidate_pass`, `pass`, `blocked`,
`not_run`.

| Req-ID | Status | Evidence Ref | Short Note |
|---|---|---|---|
| `REQ-01` | `<status>` | `<EV-01>` | `<short human-readable summary>` |

## Checks Not Run / Pending Evidence

1. `<check or manual gate>` - `<reason>`

## Evidence Consistency / Staleness Audit

1. `<issue or none>`
2. `<what still matches or what must be rerun>`

## Acceptance Gate

- Block category: `<none|semantic_miss|evidence_insufficiency|artifact_inconsistency|contract_gap|ownership_defect|complexity|required_manual_evidence>`
- First fix or external dependency: `<value or none>`
- Acceptance note: `<short truthful summary>`

## Open Issues / Unknowns

1. `<value or none>`

## Verifier Findings

1. `<value or none>`

## Complexity / Refactor Note

- Proportionality verdict: `<none|follow-up|required-before-acceptance>`
- Notes: `<value or none>`

## Next Owner / Next Action

- Next owner: `<spec-author|runtime-implementer|runtime-verifier|user|none>`
- Next action: `<single concrete next action>`
