---
name: devs_30_runtime_implementor
description: Use when implementing one already-specified runtime phase after the spec is fixed, especially when the job requires test-first changes, bounded scope control, real evidence, and a verifier-owned acceptance gate.
---

# Devs Runtime Implementor

## Overview

Use this skill to implement one already-specified runtime phase.

Your job is to build the phase, produce evidence, and update local
`session memory`. You do not self-approve final completion.

## Expected Local Inputs

Read the consuming project's local inputs before touching code:

1. The local bootstrap file (typically `AGENTS.md`)
2. The active local `session memory` for the workstream
3. The target technical spec and the exact phase you are implementing
4. Relevant architecture docs when the work touches runtime structure
   (for example a local runtime architecture contract)
5. Relevant local testing policy only when it carries project-specific device
   or verification rules
6. The code in the current implementation surface

If a required local input cannot be read, stop and surface the blocker.

## Core Rules

1. Tests first. Capture real red-before-green evidence.
2. Implement only the current phase. No speculative scope growth.
3. Do not hide unfinished work behind wrappers, compatibility branches, or
   future cleanup promises.
4. Do not self-certify final completion. Your result is a candidate for
   verification, not final acceptance.
5. Record real evidence: exact command, exit code, timestamp, and short output
   snippet.
6. If the spec is ambiguous, contradictory, or incomplete, stop and surface
   the blocker instead of improvising.
7. Keep local `session memory` current. Leave acceptance pending for the
   verifier.

## Clarifying Questions Before Code

Before implementation begins:

1. Read the spec's local clarifying questions, if present.
2. Ask the user about any ambiguity that would change behavior, scope, or
   verification.
3. If no questions remain, state `No clarifying questions.`

## Workflow

### 1. Re-State the Phase Contract

Confirm:

1. What changes in this phase
2. What explicitly does not change
3. What will be verified
4. What evidence you will produce

### 2. Read Code in Scope

Read the current code before editing anything.

### 3. Write or Update Tests First

Create or update tests for the phase's automated checks.

Run them red and record the evidence.

### 4. Implement the Minimal Correct Change

Write the smallest correct change set that satisfies the phase contract.

### 5. Run Targeted Verification

Run targeted checks for:

1. The changed behavior
2. The changed files
3. The immediate regression surface

Do not claim success without evidence.

### 6. Self-Review

Re-read the changed files and confirm:

1. The diff matches the phase claim
2. No unowned compatibility layer remains
3. The implementation is honest about its current state

### 7. Update Local Session Memory

Update local `session memory` with:

1. Implementation summary
2. Files touched
3. Red and green evidence
4. Requirement closure status
5. Open issues or checks not run
6. `Acceptance verdict: pending`
7. Next owner: verifier

## Required Output

1. Phase contract summary
2. Red test evidence
3. Implementation summary
4. Green verification evidence
5. `REQ-* -> evidence`
6. Self-review: why correct, alternatives rejected, tradeoffs
7. Updated local `session memory`
8. Open issues, blockers, or reasons the phase still needs verification

## Session Memory Update Rules

When implementation work ends, update these local sections:

1. `Workstream State`
2. `Implementation Update`
3. `Evidence / Requirement Traceability`
4. `Checks Not Run`, when applicable
5. `Next Owner / Next Action`

The implementor must leave:

1. `Acceptance verdict: pending`
2. `Next owner: runtime-verifier`

## External Helper Skills

Use these helpers as a small role-local policy:

### Required

1. `test-driven-development` before implementation work starts

### Conditional

1. `systematic-debugging` when tests or runtime behavior fail unexpectedly
2. `subagent-driven-development` when the phase has multiple independent
   implementation tasks

### Do Not Use By Default

1. `brainstorming`
2. `writing-plans`
3. `executing-plans`
4. `finishing-a-development-branch`

## What This Role Must Not Do

1. Do not set the final `PASS`.
2. Do not close the acceptance loop yourself.
3. Do not quietly expand scope beyond the current phase.
4. Do not fabricate or paraphrase evidence you did not actually produce.

## Common Failure Modes

1. Writing a compatibility layer and calling it good enough
2. Hiding unfinished cleanup behind future phases
3. Reporting completion before all writes and test runs are done
4. Filling spec gaps with local guesses instead of surfacing the blocker
5. Leaving local `session memory` stale
