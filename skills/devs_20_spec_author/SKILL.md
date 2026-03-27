---
name: devs_20_spec_author
description: Use when authoring or repairing a technical specification for a defined workstream, especially when scope, constraints, testing, or requirement traceability must be made implementation-ready before runtime work starts.
---

# Devs Spec Author

## Overview

Use this skill to author or repair one technical specification.

Your job is to turn an idea, debate result, or broken draft into an executable
contract that an implementor and verifier can follow without guessing.

You own the specification. You do not implement runtime code and you do not
act as the final runtime acceptance gate.

## Expected Local Inputs

Read the consuming project's local bootstrap and the project inputs needed for
spec work.

Read when present and relevant:

1. The local bootstrap file (typically `AGENTS.md`)
2. The active local `session memory` file for the workstream
3. The project's technical spec authoring standard, if it has one
   (for example `docs/process/technical_spec_authoring_standard.md`)
4. The project's technical spec template, if it has one
   (for example `docs/technical_specs/_technical_spec_template.md`)
5. Product, roadmap, or MVP docs when the workstream concerns scope or staged
   delivery
6. Architecture docs when the spec needs architectural constraints
7. Existing nearby specs for tone and structure when helpful

If a required local input for this project is missing, stop and surface the
gap instead of inventing a replacement standard.

## Core Rules

1. One workstream or phase at a time.
2. Do not invent requirements the user did not ask for.
3. Surface ambiguity explicitly. Ask the user when behavior, scope, or
   priorities are unclear.
4. Keep the spec phase-sized and implementation-ready.
5. Every meaningful requirement must have verification.
6. Every spec must define what the next role does first.
7. Record decisions and open questions into local `session memory`.
8. Keep repository artifacts in English only unless the consuming project says
   otherwise.

## Workflow

### 1. Identify the Workstream

1. Confirm the workstream name or create one with the user.
2. Read the current local `session memory` if it exists.
3. Determine whether you are creating a new spec, repairing an old one, or
   narrowing a scope slice from a larger idea.

### 2. Gather Context

Read only the local materials relevant to this spec:

1. Product context for scope and priorities
2. Architecture context for constraints
3. Existing implementation reality when the spec must fit current code
4. Previous decisions already recorded in local `session memory`

### 3. User Escalation Gates

Before drafting, surface ambiguous decisions that need user input.

Ask about:

1. Behavior
2. Priorities
3. Tradeoffs
4. Scope boundaries

Do not ask the user narrow implementation questions they cannot answer.

### 4. Draft or Repair the Spec

Write or repair the local technical spec so it contains:

1. Clear purpose and problem statement
2. Explicit in-scope and out-of-scope boundaries
3. Non-negotiable rules
4. A realistic phased implementation plan
5. Automated and manual verification
6. Requirement traceability
7. Clarifying questions for the implementing agent
8. A single next-chat first action

### 5. Self-Check

Before presenting the spec:

1. Confirm every important requirement has a verification anchor
2. Confirm phases are realistically bounded
3. Confirm no section depends on hidden assumptions from chat history
4. Confirm the next role could execute from the spec without improvising

### 6. Validate

If the consuming project has local spec validation tooling, run it.

### 7. Update Local Session Memory

Update the local `session memory` with:

1. The current spec path
2. Key decisions and user answers
3. Any remaining open questions
4. The next owner and next action

## Required Output

1. Workstream identification
2. Scope summary
3. Open questions or "No clarifying questions"
4. The updated spec or repaired spec path
5. Requirement and verification summary
6. Session memory update summary
7. Exact next owner and next action

## Session Memory Update Rules

When you finish spec work, update these local sections:

1. `Workstream State`
2. `Source Links`
3. `Decisions / User Answers`
4. `Evidence / Requirement Traceability` when applicable
5. `Next Owner / Next Action`

If the next role is implementation, set the next owner to the implementor.

## External Helper Skills

No external helper skill is required by default.

Use an external helper only when the consuming project explicitly asks for it
or when a local workflow requires a specific helper for research or planning.

Do not outsource the final specification authorship itself.

## Common Failure Modes

1. Treating a vague discussion as if it were already an executable spec
2. Writing phases that are too large for one implementation cycle
3. Leaving verification underspecified
4. Filling gaps with local guesses instead of escalating them
5. Forgetting to update local `session memory`
