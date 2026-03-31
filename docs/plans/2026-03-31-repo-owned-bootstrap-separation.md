# Repo-Owned Bootstrap Separation Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Replace the mixed-ownership repo-truth model with a repo-owned `devs/repo.md` model while preserving deterministic install and refresh behavior.

**Architecture:** Split Devs artifacts into two hard ownership domains. Keep `.devs/**`, generated `devs/README.md`, and repo-local Devs role skills fully Devs-managed and refreshable; move repo-local operational truth to `devs/repo.md`, which refresh must never overwrite after first creation or migration.

**Tech Stack:** Markdown contracts, install prompts, repo-local role skills

---

### Task 1: Rewrite the artifact model and routing contract

**Files:**
- Modify: `/Users/jj/Documents/Projects/devs/README.md`
- Modify: `/Users/jj/Documents/Projects/devs/install/INSTALL.md`
- Modify: `/Users/jj/Documents/Projects/devs/install/INSTALL_PROMPT.md`

**Step 1: Replace old mixed-ownership references with `devs/repo.md`**

Update the public-facing docs so the visible repo-owned file becomes `devs/repo.md` and `.devs/` is described as internal support only.

**Step 2: Update the read chain**

Describe the new route as:

```text
AGENTS.md -> devs/README.md -> devs/repo.md -> state.md -> spec.md
```

**Step 3: Update refresh wording**

Refresh must say it updates Devs-owned files, preserves repo-owned visible artifacts, and never overwrites `devs/repo.md`.

**Step 4: Verify wording consistency**

Run:

```bash
rg -n "\.devs/project\.md|devs/repo\.md|Refresh" README.md install/INSTALL.md install/INSTALL_PROMPT.md
```

Expected: public docs refer to `devs/repo.md` as repo-owned truth and no stale install guidance remains.

### Task 2: Replace the install contract and file blueprints

**Files:**
- Modify: `/Users/jj/Documents/Projects/devs/install/init_contract.md`

**Step 1: Replace the artifact model**

Update the contract so:

- `.devs/` is internal / Devs-managed only
- `devs/repo.md` is repo-owned operational truth
- `devs/README.md` is Devs-managed artifact map

**Step 2: Remove the old mixed-ownership blueprint**

Delete the old blueprint and add a new `devs/repo.md` blueprint that contains:

- canonical commands
- approval-sensitive operations
- local standards / policies / contracts
- repo-specific workflow notes only when needed

**Step 3: Add migration rules**

Specify that refresh on an old repo:

1. extracts repo-local truth from the explicit repo-owned source
2. writes `devs/repo.md`
3. stops mixing repo truth into Devs-managed files

**Step 4: Tighten refresh ownership and audit**

Define:

- Devs-managed refreshable files
- repo-owned preserved files
- exact refresh audit checklist required before `pass`

**Step 5: Verify contract consistency**

Run:

```bash
rg -n "\.devs/project\.md|devs/repo\.md|patch minimally|audit|migration" install/init_contract.md
```

Expected: the contract uses the new ownership model throughout.

### Task 3: Update the init role and work roles

**Files:**
- Modify: `/Users/jj/Documents/Projects/devs/skills/init_repo/SKILL.md`
- Modify: `/Users/jj/Documents/Projects/devs/skills/spec_author/SKILL.md`
- Modify: `/Users/jj/Documents/Projects/devs/skills/runtime_implementer/SKILL.md`
- Modify: `/Users/jj/Documents/Projects/devs/skills/runtime_verifier/SKILL.md`

**Step 1: Update required reads**

Every role that previously read the old repo-truth layer must read `devs/repo.md` instead.

**Step 2: Update bootstrap drift behavior**

If Devs is installed but `devs/repo.md` is missing, roles must stop and surface bootstrap drift.

**Step 3: Update init behavior**

The init skill must:

- create `devs/repo.md` on fresh install
- preserve existing `devs/repo.md` during normal refresh
- stop with bootstrap drift if `devs/repo.md` is unexpectedly missing

**Step 4: Verify skill consistency**

Run:

```bash
rg -n "\.devs/project\.md|devs/repo\.md|bootstrap drift" skills/init_repo/SKILL.md skills/spec_author/SKILL.md skills/runtime_implementer/SKILL.md skills/runtime_verifier/SKILL.md
```

Expected: all roles reference `devs/repo.md` and no stale requirement remains.

### Task 4: Validate the repo-owned architecture

**Files:**
- Modify if needed: `/Users/jj/Documents/Projects/devs/README.md`
- Modify if needed: `/Users/jj/Documents/Projects/devs/install/init_contract.md`
- Modify if needed: `/Users/jj/Documents/Projects/devs/skills/init_repo/SKILL.md`

**Step 1: Run text-level verification**

Run:

```bash
git diff --check
```

Expected: no patch formatting issues.

**Step 2: Run contract-level grep checks**

Run:

```bash
rg -n "\.devs/project\.md" README.md install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/*.md
```

Expected: no stale live references remain in the active install contract.

**Step 3: Re-read the update model**

Check that the final docs still support:

1. fresh install
2. refresh on a current repo
3. repeated refresh without repo-local drift

**Step 4: Commit**

```bash
git add README.md install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/init_repo/SKILL.md skills/spec_author/SKILL.md skills/runtime_implementer/SKILL.md skills/runtime_verifier/SKILL.md docs/plans/2026-03-31-repo-owned-bootstrap-separation.md
git commit -m "refactor: separate repo-owned bootstrap truth"
```
