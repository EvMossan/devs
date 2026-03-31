# Devs Install V1 Guidance Contract Cleanup Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Remove the remaining ambiguities in the simplified v1 install flow so optional local guidance docs are handled only where intended, and all Devs roles follow the same explicit-guidance contract.

**Architecture:** Keep the current v1 bootstrap model, but tighten three seams: fresh install vs refresh behavior, role-level guidance discovery rules, and shared terminology. The target state is: install may only attach guidance docs when explicitly provided, refresh never silently edits `devs/repo.md`, and runtime/spec roles only read repo-specific instruction docs when those docs are explicitly referenced by bootstrap or workstream artifacts.

**Tech Stack:** Markdown install contract, install prompts, repo-local role skill instructions

---

### Task 1: Separate fresh-install docs attachment from refresh behavior

**Files:**
- Modify: `install/init_contract.md`
- Modify: `install/INSTALL.md`
- Modify: `install/INSTALL_PROMPT.md`
- Modify: `skills/init_repo/SKILL.md`

**Step 1: Tighten the contract in `install/init_contract.md`**

Update the `Minimal Adaptive Questionnaire` and `Final optional docs step` sections so they say exactly:
- the optional local-guidance question belongs to fresh install only
- on refresh, do not ask that question by default
- on refresh, preserve `devs/repo.md` exactly as repo-owned content
- if `devs/repo.md` is missing during refresh, stop with bootstrap drift

Do not leave wording that could be read as:
- “ask one optional docs question on every run”
- “refresh may attach or replace docs as part of normal bootstrap”

**Step 2: Mirror the same rule in `install/INSTALL.md`**

Rewrite the high-level flow and refresh section so they clearly distinguish:
- fresh install: optional final docs question may be asked
- refresh: no docs question unless the user explicitly asked to update local guidance

Also update the execution summary so the report wording no longer implies the same docs outcome field always applies equally to install and refresh. Prefer wording like:
- fresh install: `attached` or `skipped`
- refresh: `preserved unchanged` unless explicitly asked otherwise

**Step 3: Mirror the same rule in `install/INSTALL_PROMPT.md`**

Update the canonical install prompt and canonical refresh prompt so:
- the install prompt says the optional final docs question applies on fresh install
- the refresh prompt does not imply any docs attachment step
- the refresh prompt explicitly says not to modify `devs/repo.md` during normal refresh

**Step 4: Align `skills/init_repo/SKILL.md`**

Change the workflow text so the installer skill says:
- merge question only when patching is ambiguous
- optional docs question only on fresh install
- refresh preserves `devs/repo.md` and does not ask for new docs unless the user explicitly requests that

Update report wording there as well so install and refresh outcomes are not collapsed into one muddy status field.

**Step 5: Verify no install/refresh ambiguity remains**

Run:

```bash
rg -n "optional final|local guidance docs|refresh" install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/init_repo/SKILL.md
```

Expected:
- fresh install wording and refresh wording are clearly distinct
- no active text implies the docs question is part of normal refresh

**Step 6: Commit**

```bash
git add install/init_contract.md install/INSTALL.md install/INSTALL_PROMPT.md skills/init_repo/SKILL.md
git commit -m "docs: separate fresh install docs step from refresh"
```

### Task 2: Enforce explicit-guidance-only reads in Devs roles

**Files:**
- Modify: `skills/spec_author/SKILL.md`

**Step 1: Fix the direct-discovery leak in `skills/spec_author/SKILL.md`**

Rewrite `Required local reads` so the spec author no longer independently reads:
- `project-local authoring standard, if present`
- `relevant architecture contracts`

Replace that with an explicit-source rule such as:
- read repo-specific guidance docs only when they are explicitly referenced by `AGENTS.md`, `devs/repo.md`, the active workstream `state.md`, or the linked `spec.md`

The goal is to forbid spec-author from rediscovering repo policy from arbitrary files in the tree.

`skills/runtime_implementer/SKILL.md` and `skills/runtime_verifier/SKILL.md`
were reviewed already and are acceptable for v1 because they only read
repo-specific guidance docs when those docs are linked from `devs/repo.md`.
Do not expand this task to those files unless a later terminology-only cleanup
needs it.

**Step 2: Add one explicit guardrail in `skills/spec_author/SKILL.md`**

Add or sharpen a rule saying the spec author must not expand repo-local guidance by discovering additional policy docs beyond the explicit guidance chain.

This should make the anti-drift policy obvious even if someone skips the install docs and reads only the role skill.

**Step 3: Verify no role still allows silent repo guidance discovery**

Run:

```bash
rg -n "authoring standard, if present|relevant architecture contracts|repo-local guidance index|guidance docs" skills/spec_author/SKILL.md skills/runtime_implementer/SKILL.md skills/runtime_verifier/SKILL.md
```

Expected:
- `spec_author` no longer instructs direct discovery from arbitrary repo docs
- `runtime_implementer` and `runtime_verifier` still stay on the explicit
  `devs/repo.md`-linked guidance model

**Step 4: Commit**

```bash
git add skills/spec_author/SKILL.md
git commit -m "docs: align spec author to explicit guidance reads"
```

### Task 3: Unify terminology for `devs/repo.md`

**Files:**
- Modify: `README.md`
- Modify: `install/INSTALL.md`
- Modify: `install/INSTALL_PROMPT.md`
- Modify: `install/init_contract.md`
- Modify if needed: `skills/init_repo/SKILL.md`
- Modify if needed: `skills/spec_author/SKILL.md`
- Modify if needed: `skills/runtime_implementer/SKILL.md`
- Modify if needed: `skills/runtime_verifier/SKILL.md`

**Step 1: Choose one canonical term**

Use this rule across the active surface:
- section title may remain `Active Local Guidance`
- prose should consistently say `local guidance docs`

Avoid mixing in alternative phrases like:
- `active local guidance for Devs`
- `repo-owned guidance docs`
- `user-maintained guidance docs`
- `local guidance for Devs`

**Step 2: Normalize install/docs prose**

Update the install files and `README.md` so they describe `devs/repo.md` consistently as:
- a repo-owned index of local guidance docs Devs should read

Do not keep mixed descriptions that alternate between “guidance”, “docs”, and “active local guidance” without a clear distinction.

**Step 3: Normalize role-skill prose if needed**

If role files currently use different nouns for the same thing, normalize them to the same `local guidance docs` language.

**Step 4: Verify terminology consistency**

Run:

```bash
rg -n "active local guidance for Devs|repo-owned guidance docs|user-maintained guidance docs|local guidance docs" README.md install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/init_repo/SKILL.md skills/spec_author/SKILL.md skills/runtime_implementer/SKILL.md skills/runtime_verifier/SKILL.md
```

Expected:
- the remaining active term is `local guidance docs`
- the section title `Active Local Guidance` may remain where it names the section itself

**Step 5: Commit**

```bash
git add README.md install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/init_repo/SKILL.md skills/spec_author/SKILL.md skills/runtime_implementer/SKILL.md skills/runtime_verifier/SKILL.md
git commit -m "docs: unify local guidance terminology"
```

### Task 4: Run a final contract sweep

**Files:**
- Modify if needed: all files above

**Step 1: Search for stale install ambiguity**

Run:

```bash
rg -n "optional final|fresh install|refresh|attached or skipped|preserved unchanged" install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/init_repo/SKILL.md
```

Expected:
- the docs step is clearly scoped to fresh install
- refresh behavior is clearly preserve-only by default

**Step 2: Search for stale discovery language**

Run:

```bash
rg -n "authoring standard, if present|relevant architecture contracts|discover(ed)? candidate docs|infer repo truth" install/init_contract.md skills/init_repo/SKILL.md skills/spec_author/SKILL.md skills/runtime_implementer/SKILL.md skills/runtime_verifier/SKILL.md
```

Expected:
- no role or install file instructs silent repo guidance discovery

**Step 3: Run diff hygiene**

Run:

```bash
git diff --check
```

Expected:
- no whitespace or conflict-marker issues

**Step 4: Commit**

```bash
git add README.md install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/init_repo/SKILL.md skills/spec_author/SKILL.md skills/runtime_implementer/SKILL.md skills/runtime_verifier/SKILL.md docs/plans/2026-03-31-install-v1-guidance-contract-cleanup.md
git commit -m "docs: add cleanup plan for install v1 guidance contract"
```
