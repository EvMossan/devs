# Formal Spec: <Spec Name>

Use this template for a formal spec when the workstream needs a larger
contract.
This file lives inside `devs/workstreams/<ws-id>/spec.md`.
A workstream may also run without a formal spec, but it must still keep a
minimal contract in `state.md`.

## Metadata

- Workstream ID: `<ws-001-short-name>`
- Status: `<draft|active|done|superseded>`
- Last updated by role: `<spec-author|runtime-implementer|runtime-verifier>`

## Objective

State the concrete outcome this spec should make possible.

## Problem / Context

Explain the problem being solved, why it matters, and any essential background.

## Clarification Record

### Clarification Coverage Summary

Allowed status values: `answered`, `already_decided`, `deferred`, `n/a`.
Keep table cells short and scannable. Put longer rationale and contract nuance
in `Clarification Coverage Details`.

| Domain | Status | Short Basis | Detail Ref |
|---|---|---|---|
| Requested outcome | `<status>` | `<short reason>` | `<CC-01 or none>` |
| User-visible behavior and flow | `<status>` | `<short reason>` | `<CC-02 or none>` |
| Environment / platform | `<status>` | `<short reason>` | `<CC-03 or none>` |
| Hard constraints | `<status>` | `<short reason>` | `<CC-04 or none>` |
| In-scope slice | `<status>` | `<short reason>` | `<CC-05 or none>` |
| Out-of-scope items | `<status>` | `<short reason>` | `<CC-06 or none>` |
| Success criteria / acceptance bar | `<status>` | `<short reason>` | `<CC-07 or none>` |
| Verification expectations | `<status>` | `<short reason>` | `<CC-08 or none>` |
| Ownership / source of truth | `<status>` | `<short reason>` | `<CC-09 or none>` |
| Integrations / dependencies | `<status>` | `<short reason>` | `<CC-10 or none>` |
| External authority / vendor constraints | `<status>` | `<short reason>` | `<CC-11 or none>` |
| Edge cases / failure behavior | `<status>` | `<short reason>` | `<CC-12 or none>` |
| Tradeoffs needing user input | `<status>` | `<short reason>` | `<CC-13 or none>` |

### Clarification Coverage Details

- `CC-01`: `<longer rationale and contract impact>`
- `CC-02`: `<longer rationale and contract impact>`

### User Escalation Gate

Allowed decision modes: `options_presented`, `user_waived`, `not_needed`.
Keep table cells short and scannable. Put long option text, rationale, and
answer nuance in `User Escalation Details`.

| # | Domain | Short Question | Decision Mode | Detail Ref | Contract Impact |
|---|---|---|---|---|---|
| `UE-1` | `<domain>` | `<short user-facing question>` | `<mode>` | `<UE-1 or none>` | `<short impact>` |

If no material clarification was needed, still include one row stating that no
material clarification was required.

### User Escalation Details

- `UE-1`: `Why it matters`: `<longer reason>` `Options`: `<options>` `Recommended`: `<recommended>` `Why`: `<why recommended>` `Answer / waiver`: `<answer>`

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

## External Authority Sources

Record every external authority that constrains this workstream's contract.
If no external platform, API, library, or vendor-behavior seam is in scope,
state `N/A`.
Determine this from the workstream contract, planned requirements, acceptance
rules, validation rules, compatibility promises, and runtime semantics, not
only from touched file type.
`N/A` is allowed only when the spec explicitly explains why the workstream
contract does not depend on any external validation rule, protocol default,
platform behavior, or vendor-defined semantics.
Preserve any material qualifiers, API-specific defaults, omitted-setting
branches, opt-out paths, version constraints, or other behavior-changing
conditions from the canonical source. Do not compress them away.

| Source ID | Concern / Seam | Canonical Source | Preferred Access | Fallback Access | Version / Date Anchor | Authority Rule | Applies to Req-ID(s) |
|---|---|---|---|---|---|---|---|
| `EXT-1` | `<seam>` | `<source>` | `<MCP:... / Web:... / RepoMirror:... / N/A>` | `<Web:... / RepoMirror:... / N/A>` | `<version/date or N/A>` | `<constraint confirmed from the source>` | `<REQ-01>` |

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
2. If this workstream touches an external platform, API, library, or
   vendor-behavior seam, `External Authority Sources` is mandatory.
   `spec-author` must define the source set and access routes, preserve this
   law at equal or stronger force than the active template, and keep all
   material qualifiers from the canonical source. `runtime-implementer` must
   independently re-check the relevant sources before red tests and production
   code. `runtime-verifier` must independently re-check the relevant sources
   before verdict. If no such seam exists, record `N/A`.
3. This `spec.md` lives inside the same workstream as `state.md` and
   `clarification.md`.
4. Specs plan work as `Slice S1..N` inside the workstream.
5. Planned `S1..N` and workstream IDs such as `ws-*` stay distinct.
6. `stage` means lifecycle position inside the workstream.
7. `spec-less` is allowed elsewhere in the repo, but never contract-less.

## Planned Slices

Add one block per planned slice.
Use `Slice S1`, `Slice S2`, and so on here.
A slice is a planned unit inside the workstream, not a separate workstream.
Do not replace these planned IDs with the workstream ID such as `ws-001`.
When execution starts, record the active slice explicitly in the
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

Verification commands must be slice-bounded.
Do not prescribe a whole suite, bundle, or broad test target as an acceptance
rerun when it contains known unrelated checks, pre-existing failures, or
mixed-scope coverage.
Prefer the narrowest command that can prove the requirement truthfully.
If a broader regression surface is still required, name it explicitly as
regression coverage, not as the primary proving command for one requirement.

### Automated Checks

1. `<command or changed-surface check>`

### Manual / Runtime Checks

1. `<scenario or N/A>`

### Evidence Artifacts

1. Spec artifact: `spec.md`
2. Workstream state artifact: `state.md`
3. External authority source set: `spec.md#external-authority-sources`
4. Implementer authority recheck evidence: `<state.md ledger entry / implementer handoff / N/A>`
5. Verifier authority audit evidence: `<verifier verdict / state.md / N/A>`
6. Manual evidence artifact: `<path or N/A>`

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
2. `If an external seam exists, include an independent authority-audit focal point covering the recorded source set, timing law, and fidelity of the implemented rule.`

## Next Role / Next Action

- Next role: `runtime-implementer`
- Next action: `<continue this workstream on the next planned slice>`
