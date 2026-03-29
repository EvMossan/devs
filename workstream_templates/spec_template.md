# Formal Spec: <Spec Name>

Use this template for a formal spec when the work needs a larger contract.
A workstream may also run without a formal spec, but it must still keep a
minimal contract in `devs/workstreams/<ws-id>/state.md`.

## Metadata

- Spec ID: `<001-short-name>`
- Status: `<draft|active|done|superseded>`
- Last updated by role: `<spec-author|runtime-implementer|runtime-verifier>`
- Linked workstream: `<ws-001-... or TBD>`

## Objective

State the concrete outcome this spec should make possible.

## Problem / Context

Explain the problem being solved, why it matters, and any essential background.

## Clarification Record

### Clarification Coverage Summary

| Domain | Status (`answered|already_decided|deferred|n/a`) | Why This Status Is Acceptable | Notes / Contract Impact |
|---|---|---|---|
| Requested outcome | `<status>` | `<why>` | `<notes>` |
| User-visible behavior and flow | `<status>` | `<why>` | `<notes>` |
| Environment / platform | `<status>` | `<why>` | `<notes>` |
| Hard constraints | `<status>` | `<why>` | `<notes>` |
| In-scope slice | `<status>` | `<why>` | `<notes>` |
| Out-of-scope items | `<status>` | `<why>` | `<notes>` |
| Success criteria / acceptance bar | `<status>` | `<why>` | `<notes>` |
| Verification expectations | `<status>` | `<why>` | `<notes>` |
| Ownership / source of truth | `<status>` | `<why>` | `<notes>` |
| Integrations / dependencies | `<status>` | `<why>` | `<notes>` |
| Edge cases / failure behavior | `<status>` | `<why>` | `<notes>` |
| Tradeoffs needing user input | `<status>` | `<why>` | `<notes>` |

### User Escalation Gate

| # | Domain | Question | Why It Matters | Options Presented | Recommended Option | Why Recommended | User Answer / Waiver | Contract Impact |
|---|---|---|---|---|---|---|---|---|
| `UE-1` | `<domain>` | `<question>` | `<why>` | `<options>` | `<recommended>` | `<why recommended>` | `<answer>` | `<impact>` |

If no material clarification was needed, still include one row stating that no
material clarification was required.

### Explicit Unknowns / Deferred Decisions

| # | Unknown / Deferred Item | Why Safe to Defer | Owner | Revisit Trigger |
|---|---|---|---|---|
| `UD-1` | `<item or none>` | `<reason>` | `<owner>` | `<trigger>` |

## User Decisions Log

### Lead Decisions

| # | Decision | Rationale | Impact |
|---|---|---|---|
| `LD-1` | `<decision or none>` | `<why>` | `<impact>` |

If no lead decisions were needed, state that explicitly in the first row.

## Existing Reality

1. Current owner(s): `<value>`
2. Current source(s) of truth: `<value>`
3. Current write / reconciliation seam(s): `<value>`
4. Known coupling or prior failures: `<value or none>`

## In Scope

1. `<bounded item>`

## Out of Scope

1. `<explicitly excluded item>`

## User-Visible Behavior Contract

1. `<behavior that must become true>`

## Success Criteria / Acceptance Criteria

1. `<what must be true for this slice to count as complete>`
2. `<what would still count as blocked or incomplete>`

## Non-Negotiable Rules

1. `<rule>`
2. Specs plan work as `Slice S1..N` inside the workstream.
3. Planned `S1..N` and workstream IDs such as `ws-*` stay distinct.
4. `stage` means lifecycle position inside the workstream.
5. `spec-less` is allowed elsewhere in the repo, but never contract-less.

## Planned Slices

Add one block per planned slice.
Use `Slice S1`, `Slice S2`, and so on here.
A slice is a planned unit inside the workstream, not a separate workstream.
Do not replace these planned IDs with the workstream ID such as `ws-001`.
When execution starts, record the active slice explicitly in the linked
workstream state.

### Slice S1: <Planned Slice Name>

- Objective: `<value>`
- In scope: `<value>`
- Out of scope: `<value>`
- Acceptance target: `<value>`
- Notes: `<value or none>`

### Slice S2: <Planned Slice Name or remove section>

- Objective: `<value>`
- In scope: `<value>`
- Out of scope: `<value>`
- Acceptance target: `<value>`
- Notes: `<value or none>`

## Owner / Source-of-Truth Map

| Concern | Canonical Owner | Write / Reconcile Seam | Derived Surfaces | Notes |
|---|---|---|---|---|
| `<behavior/data>` | `<owner>` | `<seam>` | `<derived surfaces>` | `<notes>` |

## Semantic Hazards and Tempting Wrong Fixes

1. `<wrong-but-plausible implementation pattern>`
2. `<why it would look right but still be wrong>`

## Rejected Implementation Patterns

1. `<pattern>` - `<why rejected>`

## Verification Plan

### Automated Checks

1. `<command or changed-surface check>`

### Manual / Runtime Checks

1. `<scenario or N/A>`

### Evidence Artifacts

1. Spec artifact: `<this file path>`
2. Workstream state artifact: `<path or TBD>`
3. Manual evidence artifact: `<path or N/A>`

## Requirement Traceability

| Req-ID | Requirement | Acceptance Evidence |
|---|---|---|
| `REQ-01` | `<requirement>` | `<command / artifact / scenario>` |

## Next Bounded Implementation Slice

State which planned `Slice S1..N` should start now inside the linked
workstream.

## Clarifying Questions for Implementer

1. `<question or None — requirements are fully specified>`

## Verifier Focal Points

1. `<what the verifier should challenge hardest>`

## Next Role / Next Action

- Next role: `runtime-implementer`
- Next action: `<continue the linked workstream on the next planned slice>`
