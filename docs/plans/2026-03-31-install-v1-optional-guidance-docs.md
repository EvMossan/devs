# Devs Install V1 Optional Guidance Docs Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Replace the current assisted brownfield repo-truth discovery with a minimal v1 install flow that asks only one optional end-of-install question for explicitly provided local guidance docs.

**Architecture:** Simplify the install contract so install no longer scans for commands, approval-sensitive operations, repo classification, or candidate repo standards to auto-curate into `devs/repo.md`. Keep only bootstrap patching, refresh ownership, and fresh-vs-refresh detection. Make `devs/repo.md` contain only explicitly user-provided active guidance docs or a short empty-state note, and never recreate it silently during refresh.

**Tech Stack:** Markdown install contract, install prompts, repo-local skill instructions

---

### Task 1: Rewrite the install contract around one optional docs step

**Files:**
- Modify: `install/init_contract.md`

**Step 1: Remove the obsolete discovery scope from the scan section**

Edit `Target Repo Scan` so it no longer instructs the installer to scan for:
- likely commands
- approval-sensitive operations
- repo mode / project type / technology tags
- repo-local standards or architecture docs to auto-fill `devs/repo.md`

Keep only scan items still needed for bootstrap:
- repo root and working directory
- whether Devs is already installed here
- existing instruction files and local skill folders
- existing `devs/repo.md` for refresh detection

**Step 2: Replace the adaptive questionnaire with the new v1 rule**

Rewrite `Minimal Adaptive Questionnaire` so it has only:
- merge question when patching existing root instruction files is ambiguous
- one optional final question asking whether the user wants to attach local guidance docs now

The docs question should be described as:
- optional
- skippable without blocking install
- explicit-path based
- maintainer-driven rather than repo-discovered

Remove all questionnaire language about:
- confirming canonical commands
- confirming approval-sensitive operations
- rebuilding repo truth from scanned standards docs

**Step 3: Rewrite the `devs/repo.md` blueprint**

Replace the current recommended sections with a minimal v1 structure:
1. `Active Local Guidance`
   - only explicitly user-provided docs
   - each item should be a repo path with a short purpose note when useful

Remove v1 sections that are no longer part of the contract:
- `Repository Profile`
- `Canonical Commands`
- `Approval-Sensitive Operations`
- `Local Standards / Normative Links`
- `Companion Systems In Local Use`
- `Repo-Specific Workflow Notes`

**Step 4: Adjust the install manifest contract**

Update `.devs/install_manifest.json` guidance so it records:
- whether the optional local-guidance question was asked
- whether the user skipped it
- which explicit docs were attached if any
- whether the run was `install` or `refresh`

Do not describe scan notes for candidate docs, command discovery, repo classification, or unresolved brownfield standards review in v1.

**Step 5: Run contract consistency checks**

Run:

```bash
rg -n "Canonical Commands|Approval-Sensitive Operations|Local Standards / Normative Links|likely commands|high-risk operations|repo-local standards" install/init_contract.md
```

Expected:
- no matches for removed v1 concepts inside the active install contract

**Step 6: Commit**

```bash
git add install/init_contract.md
git commit -m "refactor: simplify install contract for v1 guidance docs"
```

### Task 2: Update the public install entrypoints and product wording

**Files:**
- Modify: `install/INSTALL.md`
- Modify: `install/INSTALL_PROMPT.md`
- Modify: `README.md`

**Step 1: Rewrite the entrypoint behavior in `install/INSTALL.md`**

Update the install summary and non-negotiable behavior so the public contract says:
- scan first for bootstrap and advisory profile only
- ask only merge questions when patching is ambiguous
- ask one optional final question about attaching local guidance docs
- allow skipping that docs step with no penalty

Remove public install language that still implies assisted brownfield truth reconstruction for commands, standards, or approval-sensitive operations.

**Step 2: Rewrite the copy-paste install prompt**

Update `install/INSTALL_PROMPT.md` requirements so the prompt now tells the agent to:
- scan before asking questions
- avoid repo-wide discovery of candidate truth docs
- ask at most the merge question plus one optional final docs question
- treat local guidance docs as explicit user-provided inputs only

**Step 3: Narrow the README artifact description**

Update `README.md` where it describes `devs/repo.md` so the wording matches v1:
- confirmed local guidance docs

Avoid broader wording that implies install reconstructs all repo operational truth automatically.

**Step 4: Verify active docs are aligned**

Run:

```bash
rg -n "local standards|Canonical Commands|approval-sensitive|adaptive questionnaire|brownfield" README.md install/INSTALL.md install/INSTALL_PROMPT.md
```

Expected:
- no stale wording that contradicts the new v1 install flow

**Step 5: Commit**

```bash
git add README.md install/INSTALL.md install/INSTALL_PROMPT.md
git commit -m "docs: align install entrypoints with v1 guidance-docs flow"
```

### Task 3: Rewrite the repo init skill to match the new contract

**Files:**
- Modify: `skills/init_repo/SKILL.md`

**Step 1: Simplify the scan responsibilities**

Update the scan step so it covers only:
- advisory profile inputs
- bootstrap patching inputs
- refresh detection inputs

Remove skill instructions that tell the installer to discover:
- likely commands
- approval-sensitive operations
- repo-local standards that should stay discoverable through `devs/repo.md`

**Step 2: Replace the question flow**

Update `Workflow` step 4 so it instructs:
- ask the merge question only when root-file patching is ambiguous
- after install decisions are otherwise resolved, ask one optional final question about attaching local guidance docs
- accept skip cleanly
- never force the user to review repo-wide discovered candidates

**Step 3: Update the write step for `devs/repo.md`**

Change the repo-truth write guidance so the installer writes:
- advisory profile fields from scan
- active local guidance docs only when the user explicitly provided them

Remove any language about truthfully rebuilding broader repo standards during first install.

**Step 4: Verify the skill does not reintroduce removed logic**

Run:

```bash
rg -n "commands remain ambiguous|approval-sensitive|repo-local standards|rebuilding devs/repo.md" skills/init_repo/SKILL.md
```

Expected:
- no matches for the removed v1 questionnaire/discovery model

**Step 5: Commit**

```bash
git add skills/init_repo/SKILL.md
git commit -m "refactor: simplify init skill for v1 optional guidance docs"
```

### Task 4: Run a final consistency sweep for the whole install surface

**Files:**
- Modify if needed: `README.md`
- Modify if needed: `install/INSTALL.md`
- Modify if needed: `install/INSTALL_PROMPT.md`
- Modify if needed: `install/init_contract.md`
- Modify if needed: `skills/init_repo/SKILL.md`

**Step 1: Search for stale contract language across the active install surface**

Run:

```bash
rg -n "Canonical Commands|Approval-Sensitive Operations|Local Standards / Normative Links|high-risk operations|likely commands|active guidance docs useful for devs/repo.md" README.md install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/init_repo/SKILL.md
```

Expected:
- only the new v1 guidance-docs model remains

**Step 2: Search for the new docs-step wording**

Run:

```bash
rg -n "optional final question|local guidance docs|attach local guidance" README.md install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/init_repo/SKILL.md
```

Expected:
- each active install surface describes the same one-question model

**Step 3: Manually review the happy paths**

Review the changed text and confirm these scenarios are both truthfully described:
1. greenfield install with no extra docs provided
2. install where the user explicitly attaches one or more local guidance docs

Confirm neither scenario requires:
- repo-wide docs review
- candidate shortlist review
- commands confirmation
- brownfield migration logic

**Step 4: Commit**

```bash
git add README.md install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/init_repo/SKILL.md
git commit -m "docs: finalize v1 optional guidance-docs install flow"
```

### Task 5: Validate the behavior manually before broader rollout

**Files:**
- No file changes required unless a drift is found

**Step 1: Dry-run the greenfield path mentally against the new contract**

Check that the new flow can complete with:
- zero repo guidance docs
- no extra install questions unless merge handling is ambiguous

Expected:
- `devs/repo.md` still gets written with advisory profile only

**Step 2: Dry-run the maintainer-attached-docs path**

Check that the new flow can complete when the user provides exact file paths for local guidance docs.

Expected:
- only explicitly provided docs appear in `devs/repo.md`
- no repo discovery step is needed to propose candidates

**Step 3: Block rollout on any remaining ambiguity**

If any active file still implies:
- migration behavior
- inferred repo truth
- repo-wide candidate discovery

return to the relevant task and fix it before implementation is declared complete.

**Step 4: Final commit**

```bash
git add README.md install/INSTALL.md install/INSTALL_PROMPT.md install/init_contract.md skills/init_repo/SKILL.md docs/plans/2026-03-31-install-v1-optional-guidance-docs.md
git commit -m "docs: add implementation plan for v1 install simplification"
```
