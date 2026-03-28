# Workstream Contract: <Workstream Name>

## Metadata

- Workstream ID: `<slug>`
- Status: `draft`
- Last updated by role: `<spec-author|runtime-implementer|runtime-verifier>`

## Objective

State the concrete outcome this workstream should produce.

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

If no material clarification was needed, still include one row stating that no material clarification was required.

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

1. Contract artifact: `<this file path>`
2. Workstream state artifact: `<path>`
3. Manual evidence artifact: `<path or N/A>`

## Requirement Traceability

| Req-ID | Requirement | Acceptance Evidence |
|---|---|---|
| `REQ-01` | `<requirement>` | `<command / artifact / scenario>` |

## Next Bounded Implementation Slice

State the exact slice that should be built now.

## Clarifying Questions for Implementer

1. `<question or None — requirements are fully specified>`

## Verifier Focal Points

1. `<what the verifier should challenge hardest>`

## Next Role / Next Action

- Next role: `runtime-implementer`
- Next action: `<single concrete next action>`
