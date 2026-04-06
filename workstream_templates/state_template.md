# Workstream State: <Workstream Name>

Use this file as the one living continuity record for a repo workstream.
Keep same-target fix loops inside this file and this workstream.
Open a new workstream only when the target outcome or scope changes materially.

If there is no formal spec, the minimal contract section below is still
required.
`spec-less` is allowed here, but never `contract-less`.

## Workstream Status

- Workstream ID: `<ws-001-short-name>`
- Overall status: `<draft|in_progress|candidate|blocked|done>`
- Current stage: `<clarify/specify|implement|verify>`
- Latest verdict: `<pending|pass|blocked>`
- Linked spec: `<devs/specs/<spec-id>/spec.md or none>`
- Current spec slice: `<S1|S2|none>`
- Next role: `<spec-author|runtime-implementer|runtime-verifier|user>`
- Next action: `<single concrete next action>`

## Minimal Contract Snapshot

- Objective: `<value>`
- In scope now: `<value>`
- Out of scope now: `<value>`
- Acceptance target: `<value>`
- Source request or link: `<value>`

## Source Links

1. Formal spec: `<path or none>`
2. Clarification artifact: `<path or none>`
3. Relevant architecture docs: `<path(s) or N/A>`
4. Related failure artifacts: `<path(s) or N/A>`
5. Helper artifacts in use (`plan`, `tasks`, etc.): `<path(s) or N/A>`

## Clarification Status

- Clarification complete: `<yes|no>`
- Contract source: `<clarification path / spec path + section anchor / this file>`
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

## Evidence Ledger

| Check / Scenario | Status (`pass|fail|blocked|not_run`) | Timestamp | Evidence / Note |
|---|---|---|---|
| `<command or scenario>` | `<status>` | `<timestamp>` | `<note>` |

## Requirement Status Snapshot

| Req-ID | Status (`open|candidate_pass|pass|blocked|not_run`) | Latest Evidence |
|---|---|---|
| `<REQ-01>` | `<status>` | `<evidence>` |

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
