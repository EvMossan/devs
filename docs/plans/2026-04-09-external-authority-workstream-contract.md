# External Authority Workstream Contract Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add one shared external-authority contract across workstream specs, state, implementation, and verification.

**Architecture:** Put the authority set in the workstream contract first, then require both implementation and verification to re-check the same recorded sources through explicit preferred and fallback access routes.

**Tech Stack:** Markdown templates, Devs role skills, repository-local verification with `rg`

---

### Task 1: Freeze baseline gaps

**Files:**
- Create: `docs/notes/external-authority-red-green-evidence.md`

**Step 1: Record the RED baseline**

List the missing behaviors in the current templates and skills.

**Step 2: Keep the target concise**

Record only the minimum GREEN contract needed for the refactor.

### Task 2: Update workstream templates

**Files:**
- Modify: `workstream_templates/spec_template.md`
- Modify: `workstream_templates/state_template.md`

**Step 1: Add external authority contract surface**

Add a mandatory spec section and the minimal state fields needed for spec-less work.

**Step 2: Bind the requirement to the workstream contract**

Make the `Non-Negotiable Rules` section require authority recording and rechecks.

### Task 3: Update the three role skills

**Files:**
- Modify: `skills/devs-spec-author/SKILL.md`
- Modify: `skills/devs-runtime-implementer/SKILL.md`
- Modify: `skills/devs-runtime-verifier/SKILL.md`

**Step 1: Make `spec-author` record the source set**

Require authoritative source capture with explicit access routes.

**Step 2: Make `runtime-implementer` re-check before code**

Require pre-code external-authority rechecks and evidence capture.

**Step 3: Make `runtime-verifier` re-check before verdict**

Require independent authority audit before acceptance.

### Task 4: Verify the contract is wired through

**Files:**
- Verify: `workstream_templates/spec_template.md`
- Verify: `workstream_templates/state_template.md`
- Verify: `skills/devs-spec-author/SKILL.md`
- Verify: `skills/devs-runtime-implementer/SKILL.md`
- Verify: `skills/devs-runtime-verifier/SKILL.md`

**Step 1: Search for required contract terms**

Run `rg -n "External Authority Sources|Preferred Access|Fallback Access|external authority" workstream_templates/spec_template.md workstream_templates/state_template.md skills/devs-spec-author/SKILL.md skills/devs-runtime-implementer/SKILL.md skills/devs-runtime-verifier/SKILL.md`

Expected: each target file contains the new contract hooks.

**Step 2: Search for authority recheck duties**

Run `rg -n "re-check|authoritative external|external seam" skills/devs-runtime-implementer/SKILL.md skills/devs-runtime-verifier/SKILL.md skills/devs-spec-author/SKILL.md`

Expected: spec-author records, implementer re-checks before code, verifier re-checks before verdict.
