---
name: devs-init-repo
description: Use when installing Devs into the current repository or refreshing an existing Devs install. Scan first, ask only unresolved questions, create or patch the repo-local bootstrap, hidden `.devs/` support files, visible `devs/` artifact layer, install the current Devs work-role skill bundles for Claude and Codex, and stop before feature work begins.
---

# Devs Init Repo

## Mission

Install or refresh Devs in the current repository so future sessions can use a
repo-local Devs bootstrap, hidden support files under `.devs/`, visible work
artifacts under `devs/`, and repo-local Devs work-role skill bundles without relying
on one long chat.

## Required reads

Before writing or patching anything:

1. `install/init_contract.md` from the source Devs repo
2. `skills/devs-spec-author/SKILL.md` from the source Devs repo
3. `skills/devs-runtime-implementer/SKILL.md` from the source Devs repo
4. `skills/devs-runtime-verifier/SKILL.md` from the source Devs repo
5. `workstream_templates/spec_template.md` from the source Devs repo
6. `workstream_templates/state_template.md` from the source Devs repo
7. target repo root instruction files if they already exist
8. target repo manifests and top-level structure

If a required input cannot be read, stop and surface the blocker.
Treat each role skill bundle directory as the authoritative source unit during
install or refresh, not only its `SKILL.md`.

## Core rules

1. Scan first, ask second.
2. Ask only the minimum unresolved questions.
3. Keep `AGENTS.md` short and broadly applicable.
   When patching an existing file, prefer one Devs-managed marker block rather
   than freeform whole-file rewrites.
4. Keep `CLAUDE.md` as a thin shim over `AGENTS.md`.
5. Synchronize the current authoritative work-role skill bundles and support
   templates from source without redesigning them during install.
6. Install repo-local work-role skill bundles for both Claude and Codex by default.
7. Do not install Superpowers or Spec Kit by default.
8. Do not require or look for `install/templates/*`.
9. Do not create `devs/bootstrap/*` mirror files unless the user explicitly
   asks for local installer copies.
10. A GitHub repo URL for Devs is source context, not a submodule/vendoring
    request, unless the user explicitly asks for that packaging model.
11. `.devs/` is the hidden system layer.
12. `devs/` is the visible project artifact layer.
13. `devs/README.md` is Devs-managed and refreshable.
14. `devs/repo.md`, `devs/specs/`, and `devs/workstreams/` are repo-owned.
15. `workstream` is the main continuity and delivery unit.
16. Same-target fix loops stay inside one workstream.
17. A formal spec is optional, but `spec-less` never means contract-less.
18. Specs use planned `Slice S1..N` inside a workstream, while repo workstreams use `ws-*`.
19. `stage` means lifecycle position inside one workstream.
20. Do not infer repo truth from repo contents during install.
21. Stop after installation. Do not start feature work.

## Workflow

### 1. Determine source and target

1. The current repo is the target.
2. The Devs repo containing the install files is the source.
3. If only a raw URL was provided, infer the source repo root from it.
4. If a GitHub repo URL was provided, resolve `install/INSTALL.md` inside that
   source repo and continue. Do not stop to ask `submodule vs copy repo files`
   unless the user explicitly asked for repo embedding.

### 2. Read the exact source inputs

Read these exact source paths:

1. `install/init_contract.md`
2. `skills/devs-spec-author/`
3. `skills/devs-runtime-implementer/`
4. `skills/devs-runtime-verifier/`
5. `workstream_templates/spec_template.md`
6. `workstream_templates/state_template.md`

Read `SKILL.md` from each role skill bundle before writing, and treat any
sibling bundle files as authoritative install inputs. Do not substitute guessed
source paths if these exist. After install or refresh, each managed target role
skill directory must match the current source bundle file set and contents
exactly.

### 3. Scan the target repo

Determine:

1. whether Devs is already installed here
2. existing root instruction files and local skill folders
3. existing `devs/repo.md` when Devs is already installed

### 4. Ask the adaptive question block

Use the minimal questionnaire from `install/init_contract.md`.

Ask only when something remains unresolved after the scan.

Typical reasons to ask:

1. existing root instruction files cannot be patched safely
2. on fresh install, after bootstrap decisions are resolved, you need to ask
   the optional final question about attaching local guidance docs now

Ask in one concise block.
Do not ask deep implementation trivia.
Do not ask questions that do not change install output.
Do not present repo-discovered candidate docs.
Do not ask the local-guidance question during normal refresh.

### 5. Write or patch target bootstrap files

Create or patch:

1. `AGENTS.md`
2. `CLAUDE.md`
3. `devs/repo.md`
4. `.devs/install_manifest.json`
5. `.devs/templates/spec_template.md`
6. `.devs/templates/state_template.md`
7. `devs/README.md`
8. `devs/specs/`
9. `devs/workstreams/`

Use the blueprints in `install/init_contract.md` for generated files.
Do not block on missing source bootstrap templates.
Do not present visible `devs/` artifacts as installer-owned scaffolding.
If the target repo already has Devs installed, treat this run as a refresh:
apply the refresh ownership rules from `install/init_contract.md` rather than a
blind reinstall.
Use the managed patch rule for `AGENTS.md` whenever the target file already
exists.

### 6. Install local work-role skill bundles

Synchronize the current source role skill bundles into:

- `.claude/skills/devs-spec-author/`
- `.claude/skills/devs-runtime-implementer/`
- `.claude/skills/devs-runtime-verifier/`
- `.agents/skills/devs-spec-author/`
- `.agents/skills/devs-runtime-implementer/`
- `.agents/skills/devs-runtime-verifier/`

Do not install `devs-init-repo` into the target repo unless the user explicitly
asks for local refresh tooling.
For managed target role skill directories, make the file set and file contents
match the current source bundles exactly, including removing files that are no
longer present in the source bundles.

### 7. Stop and report

Return:

1. install mode
2. local guidance status (`attached`, `skipped`, or `preserved unchanged`)
3. questions asked and answers
4. files written
5. files patched
6. unresolved issues
7. the exact next suggested prompt for the first real workstream

## Output requirements

Your final install report must include:

1. install mode
2. local guidance status (`attached`, `skipped`, or `preserved unchanged`)
3. files written
4. files patched
5. checks or decisions still pending
6. next suggested prompt

## Common failure modes to avoid

1. asking too many questions before scanning the repo
2. blocking on a non-existent `install/templates/` source folder
3. overwriting existing root instruction files blindly
4. rewriting the current role skill bundles during install
5. asking `submodule vs copied repo files` when the user only supplied Devs as a
   remote source repo
6. copying installer internals into the target repo without a user request
7. leaving the target repo dependent on the source repo for everyday Devs work
8. starting real feature work before bootstrap is complete
9. treating visible `devs/` artifacts as refresh-owned support files
10. letting `spec-less` turn into `contract-less`
11. overwriting an existing `devs/repo.md` during refresh
12. asking the user to review repo-wide discovered docs
