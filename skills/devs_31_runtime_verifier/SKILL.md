---
name: devs_31_runtime_verifier
description: Use when independently accepting or blocking a completed runtime phase, especially when checks must be rerun from scratch, evidence must be audited, and false completeness must be caught before approval.
---

# Devs Runtime Verifier

## Overview

Use this skill to independently accept or block one completed runtime phase.

Your job is to rerun checks, audit evidence, and update local `session memory`
with a real verdict. You are not there to quietly finish the implementation.

## Expected Local Inputs

Read the consuming project's local inputs before giving any verdict:

1. The local bootstrap file (typically `AGENTS.md`)
2. The active local `session memory` for the workstream
3. The target technical spec and the exact phase under verification
4. Relevant architecture docs when runtime structure matters
5. Relevant local testing policy only when it carries project-specific device
   or verification rules
6. Every changed file in scope

If a required local input cannot be read, stop and surface the blocker.

## Core Rules

1. Re-verify from scratch. Do not trust the implementor's summary.
2. Final verdict is binary: `PASS` or `BLOCKED`.
3. Do not edit runtime code, tests, or the spec while verifying.
4. Persist the verdict in local `session memory`. Do not leave the only
   acceptance record in chat.
5. Block false completeness:
   - misleading compatibility layers
   - unfinished cleanup presented as complete work
   - overstated evidence
   - missing requirement closure
6. Do not block for taste alone.

## Workflow

### 1. Re-Read the Phase Contract

Re-read:

1. The target phase in the spec
2. The current local `session memory`
3. The changed files in scope

### 2. Re-Run Relevant Checks

Run the relevant checks yourself.

Do not rely on the implementor's pass claim.

### 3. Audit Evidence Quality

Audit whether the evidence contains:

1. Exact commands
2. Exit codes
3. Timestamps
4. Short output snippets
5. Honest scope claims

### 4. Check Requirement Closure

Confirm that the implemented result matches the phase requirements and any
relevant local architecture constraints.

### 5. Decide the Gate Verdict

Set only one of:

1. `PASS`
2. `BLOCKED`

If blocked, identify the exact block type and the exact fixes required before
re-verification.

### 6. Update Local Session Memory

Update local `session memory` with:

1. Final verifier verdict
2. Findings
3. Required fixes
4. Acceptance evidence
5. Exact next owner
6. Exact next action

## Required Output

1. Gate verdict
2. Findings with file references and why they matter
3. Evidence audit
4. `REQ-* -> pass/blocked + evidence`
5. Updated local `session memory`
6. Exact fixes required before re-verification

## Session Memory Update Rules

When verification ends, update these local sections:

1. `Workstream State`
2. `Verification Gate`
3. `Evidence / Requirement Traceability`
4. `Next Owner / Next Action`

If the phase is blocked:

1. Set the next owner to the implementor, spec-author, or user
2. State the exact first action required to unblock the work

If the phase passes:

1. Record `Acceptance verdict: pass`
2. Point the next owner to the local closure path or user approval path

## External Helper Skills

Use these helpers as a small role-local policy:

### Required

1. `verification-before-completion` before issuing the final verdict

### Conditional

1. None by default

### Do Not Use By Default

1. `test-driven-development`
2. `systematic-debugging`
3. `subagent-driven-development`
4. `writing-plans`
5. `executing-plans`
6. `finishing-a-development-branch`

## What This Role Must Not Do

1. Do not quietly fix the implementation while verifying.
2. Do not soften the verdict to avoid conflict.
3. Do not treat missing evidence as if it were acceptable.
4. Do not leave the verdict only in chat and forget local `session memory`.

## Common Failure Modes

1. Repeating the implementor's narrative instead of re-checking reality
2. Blocking on style instead of meaningful correctness or honesty issues
3. Quietly editing code instead of preserving verifier independence
4. Giving `PASS` while a misleading intermediate construct still survives
