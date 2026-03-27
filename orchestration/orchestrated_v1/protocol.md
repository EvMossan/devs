# Orchestrated V1 Protocol

## Purpose

`orchestrated_v1` is a controller-managed execution mode for one bounded
workstream.

It keeps the Devs core loop intact:

`clarify -> specify -> implement -> verify`

The difference is that a single controller session owns the workflow and uses
fresh subagents for the role-specific phases.

## Scope

This protocol is for:

1. One workstream at a time
2. One active specification artifact
3. One controller-owned state artifact
4. Fresh role separation without requiring the user to manually manage new
   sessions

This protocol is not for:

1. Parallel swarms
2. Multi-workstream portfolio management
3. Automatic brownfield migration
4. Long unattended runs with no user approval gates

## Required Runtime Artifacts

Every orchestrated workstream must persist:

1. `workstreams/<slug>/spec.md`
2. `workstreams/<slug>/workstream.md`

`spec.md` is the contract.

`workstream.md` is the controller-owned operational state and handoff record.

## Controller Ownership

The controller owns:

1. Workstream directory creation
2. Artifact initialization
3. State updates between phases
4. User decision gates
5. Launching fresh subagents with bounded context
6. Deciding whether the next move is implementation, verification, spec
   repair, user action, or stop

Subagents may edit code and tests when their role allows it, but they do not
own the persistent state file.

## Human Decision Gates

The controller must involve the user at these points:

1. Clarification answers
2. Specification approval before implementation
3. Manual verification steps when needed
4. Final result acceptance, pause, or re-scope

## Subagent Boundaries

Every role subagent must be fresh.

Each subagent should receive only:

1. The current task brief
2. The exact artifact paths
3. The relevant role prompt
4. Any changed file paths or commands needed for the phase

When the runtime supports it, prefer fresh subagents with minimal passed
context instead of forking the full controller session by default.

Avoid passing the full narrative history when the saved artifacts already hold
the required state.

## Loop Rules

1. Clarification can loop until the spec is good enough to approve.
2. Implementation can loop only from a verifier finding or a clear user
   change request.
3. Verification returns only `PASS` or `BLOCKED`.
4. `BLOCKED` due to implementation issues returns to implementation.
5. `BLOCKED` due to missing or broken contract returns to clarification or
   explicit user approval.
6. External blockers stop the loop and become the next user-visible action.

## Prototype Stop Conditions

The controller stops when:

1. Verification returns `PASS`
2. The user declines the spec or result
3. The workstream needs user input that cannot be inferred safely
4. The workstream hits an external blocker
5. The workstream expands beyond one bounded slice
