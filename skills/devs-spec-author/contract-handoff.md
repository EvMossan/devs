# Spec Author Contract and Handoff

Use this file after clarification is visible in repo artifacts and before
handing off to the next Devs role.

## Clarification Artifact Rule

The clarification interview must be visible in repo artifacts, not only in
chat and not only in session memory.

The primary technical clarification artifact is
`devs/workstreams/<ws-id>/clarification.md`.

At minimum, preserve:

1. closure status for each material contract position
2. the material questions or decisions actually raised
3. the explanatory `Decision Brief` or a short summary of it for each
   context-heavy question block
4. the delivery mode used for each block when user input was required
5. the options presented when a real decision existed
6. the practical consequence of each option when a real decision existed
7. the recommended option and why it was recommended
8. user answers or explicit waivers
9. contract impacts of those answers
10. material positions already fixed by the provided context
11. explicit unknowns or deferred positions, including where they will be
    closed later
12. named spec-author decisions and why they were owned here

If no user clarification was needed, record a short closure summary instead.
Name what fixed the positions and why no new user input was needed.
Do not dump raw scoring tables or noisy internal rubric details into the spec.
Keep only a compact operational echo in session memory or state when needed.

## Drafting Workflow

1. Build the closure record first.
2. Reframe the request:
   - what is broken or missing
   - why it matters
   - what this bounded slice will change now
3. Read runtime reality before prescribing change:
   - current owners
   - source-of-truth boundaries
   - write or reconciliation seams
   - coupling seams
   - prior failed attempts or verifier findings
4. Publish the exact markdown-table `Contract Surface Grid` required by
   `./question-patterns.md` into the workstream clarification artifact.
5. Synthesize the user-facing clarification interview only from grid rows that
   still require user confirmation.
6. Continue classifying and closing material positions until the contract can
   stand on its own.
7. Only then write the formal spec.

A material position is one that changes behavior, scope, priority,
verification, ownership, or integration boundary.
A `Contract Surface Grid` row must record: row, slot, contract surface, and
evidence.
For a new or reopened specification, the `Contract Surface Grid` must classify
all 30 canonical slots and reach exactly 100 rows before drafting.
If a material position remains open and cannot safely be deferred, do not
finalize the contract.

## Contract Format

If the local project has an explicitly linked stricter template, follow that
format exactly.

If no stricter local template is explicitly in force, use the repo's default
templates as the source of truth:

- `.devs/templates/spec_template.md`
- `.devs/templates/state_template.md`
- `.devs/templates/clarification_template.md`

Repository artifacts must remain in English unless the local project says
otherwise.

For a new or reopened specification run under `devs-spec-author`, completion
requires a formal `devs/specs/<spec-id>/spec.md`.
`spec-less` is not a valid final output for this role.

## Handoff Self-Check

Before finalizing, confirm:

1. the implementer could choose the correct causal seam from this document
2. the verifier knows what would count as a semantic miss
3. all important requirements have a proving path
4. the slice is still stage-sized
5. the clarification artifact is complete enough that the next session does not
   reconstruct the interview from chat
6. no section depends on hidden chat memory
7. every context-heavy decision had a sufficient visible `Decision Brief`
8. each escalated question was user-answerable without reading code
9. each option's practical consequence was clear
10. architecture completeness did not masquerade as user-clarification
    completeness
11. a zero-question path still left a visible closure summary in the contract

## Helper Policy

External helpers may sharpen this role without displacing the Devs contract.

Rules:

1. Devs remains the governing contract and artifact system.
2. Helpers may accelerate exploration or scaffolding.
3. Final contract authorship, clarification logging, and next-owner routing
   remain this role's responsibility.
4. Do not let helper-generated artifacts silently become the source of truth.
5. Do not let a helper replace the `Clarification Record`, unknown inventory,
   or `User Decisions Log`.
6. `writing-plans` is appropriate only after the contract is explicit enough
   that a plan cannot silently change scope.

## Output Requirements

Return:

1. workstream identification
2. clarification summary
3. open questions, or a closure summary explaining why no new user
   clarification was needed
4. formal spec path
5. contract summary
6. requirement and verification summary
7. next owner and exact next action

## Session Memory Update

Update the local workstream state with:

1. clarification artifact path
2. contract path
3. key user answers
4. clarification outcome summary, including fixed-by-context decisions and any
   named spec-author decisions
5. owner or source-of-truth decisions
6. semantic hazards
7. open deferred decisions
8. next owner and next action

## Common Failure Modes

1. treating a discussion as if it were already a contract
2. leaving clarification history only in chat
3. treating strong docs as permission to guess
4. treating strong docs as a reason to reopen already-fixed decisions
5. confusing `program decided` with `spec decided`
6. asking implementation trivia the user cannot answer productively
7. leaving ownership implicit when implementation depends on it
8. writing vague verification such as `test manually`
9. omitting negative cases or rejected patterns
10. creating a slice too large for one honest implementation cycle
11. using internal architecture language without building a user-facing bridge
12. treating a zero-question path as permission to skip visible closure
13. starting branch, workstream, artifact, or spec prose before the visible
    checkpoint and needed clarification blocks
14. letting global `spec-less` policy override the required `spec.md` output of
    `devs-spec-author`
15. asking the user to choose between formal spec and `spec-less` output while
    this role is active
