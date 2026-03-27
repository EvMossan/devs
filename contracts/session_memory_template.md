# Session Memory Template

Use one `session memory` file per active workstream.

Purpose:

1. Preserve long-term state across sessions
2. Provide role-to-role communication
3. Keep the next session from reconstructing context from chat history

Naming rules:

1. Use descriptive workstream names
2. Do not use dates as the primary name
3. Do not use active sequential numbering

Examples:

1. `spec78-phase3-health-goals-ui.md`
2. `spec78-health-goals-ui.md`
3. `process-session-conveyor-refactor.md`
4. `topic-product-direction.md`

Role update rules:

1. `spec-author` updates scope, decisions, user answers, and next owner
2. `runtime-implementor` updates implementation progress, evidence, and leaves
   acceptance pending
3. `runtime-verifier` records verdict, findings, required fixes, and next owner

Required sections:

1. `Workstream State`
2. `Source Links`
3. `Decisions / User Answers`
4. `Implementation Update`
5. `Verification Gate`
6. `Evidence / Requirement Traceability`
7. `Next Owner / Next Action`

Optional sections:

1. `Clarifying Questions`
2. `Known Risks / Follow-ups`
3. `Checks Not Run`
4. `Declared Deviations`
5. `Notes for Next Session`

Template:

```md
# Session Memory: <Workstream Name>

## Workstream State

- Overall status: `<draft|in_progress|candidate|blocked|done>`
- Current role: `<spec-author|runtime-implementor|runtime-verifier|user>`
- Branch: `<branch-name or N/A>`
- Base commit/tag: `<commit-hash-or-tag or N/A>`
- Acceptance verdict: `<pending|pass|blocked>`

## Source Links

1. Bootstrap: `<path>`
2. Primary spec: `<path>`
3. Architecture/product docs: `<path(s) or N/A>`
4. Related artifacts: `<path(s) or N/A>`

## Decisions / User Answers

1. `<decision or answer>`

## Implementation Update

1. Scope touched: `<what changed or N/A>`
2. Files changed: `<path list or N/A>`
3. Summary of work: `<short summary or N/A>`
4. Open issues/blockers: `<none or list>`

## Verification Gate

1. Latest verifier verdict: `<pending|pass|blocked>`
2. Block type: `<none|implementation|spec|external>`
3. Findings: `<none or list>`
4. Required fixes before re-verification: `<none or list>`

## Evidence / Requirement Traceability

1. `<Req-ID or work item>` - `<status>` - `<evidence>`

## Next Owner / Next Action

1. Next owner: `<spec-author|runtime-implementor|runtime-verifier|user|none>`
2. Next action: `<single concrete next action>`

## Clarifying Questions

1. `<question and answer or N/A>`

## Known Risks / Follow-ups

1. `<risk or N/A>`

## Checks Not Run

1. `<check and reason or N/A>`

## Declared Deviations

1. `<deviation or N/A>`

## Notes for Next Session

1. `<important context that must not be lost>`
```
