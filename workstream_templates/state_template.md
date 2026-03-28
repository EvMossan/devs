# Workstream State: <Workstream Name>

## Workstream Status

- Workstream ID: `<slug>`
- Overall status: `<draft|in_progress|candidate|blocked|done>`
- Current phase: `<clarify/specify|implement|verify>`
- Latest verdict: `<pending|pass|blocked>`
- Next role: `<spec-author|runtime-implementor|runtime-verifier|user>`
- Next action: `<single concrete next action>`

## Source Links

1. Contract: `<path>`
2. Relevant architecture docs: `<path(s) or N/A>`
3. Related failure artifacts: `<path(s) or N/A>`
4. Helper artifacts in use (`plan`, `tasks`, etc.): `<path(s) or N/A>`

## Clarification Status

- Clarification complete: `<yes|no>`
- Contract clarification record: `<spec path + section anchor>`
- Open user questions: `<none or short list>`
- Explicit deferred decisions: `<none or short list>`

## Current Slice

- Slice summary: `<value>`
- In scope now: `<value>`
- Out of scope now: `<value>`
- Changed surface: `<files or modules in scope>`

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

- Next owner: `<spec-author|runtime-implementor|runtime-verifier|user|none>`
- Next action: `<single concrete next action>`
