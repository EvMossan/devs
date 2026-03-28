---
name: devs_init_repo
version: v1.1
description: Use when installing Devs into the current repository or refreshing an existing Devs install. Scan first, ask only unresolved questions, create or patch the repo-local bootstrap and workstream scaffolding, install the current Devs work-role skills for Claude and Codex, and stop before feature work begins.
---

# Devs Init Repo

## Mission

Install or refresh Devs in the current repository so future sessions can use a
repo-local Devs bootstrap, repo-local workstream templates, and repo-local
Devs work-role skills without relying on one long chat.

## Required reads

Before writing or patching anything:

1. `install/init_contract.md` from the source Devs repo
2. `skills/spec_author/SKILL.md` from the source Devs repo
3. `skills/runtime_implementor/SKILL.md` from the source Devs repo
4. `skills/runtime_verifier/SKILL.md` from the source Devs repo
5. `workstream_templates/spec_template.md` from the source Devs repo
6. `workstream_templates/state_template.md` from the source Devs repo
7. target repo root instruction files if they already exist
8. target repo manifests and top-level structure

If a required input cannot be read, stop and surface the blocker.

## Core rules

1. Scan first, ask second.
2. Ask only the minimum unresolved questions.
3. Keep `AGENTS.md` short and broadly applicable.
4. Keep `CLAUDE.md` as a thin shim over `AGENTS.md`.
5. Copy the current authoritative work-role skills and workstream templates
   verbatim. Do not redesign them during install.
6. Install repo-local work-role skills for both Claude and Codex by default.
7. Do not install Superpowers or Spec Kit by default.
8. Do not require or look for `install/templates/*`.
9. Do not create `devs/bootstrap/*` mirror files unless the user explicitly
   asks for local installer copies.
10. A GitHub repo URL for Devs is source context, not a submodule/vendoring
    request, unless the user explicitly asks for that packaging model.
11. Stop after installation. Do not start feature work.

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
2. `skills/spec_author/SKILL.md`
3. `skills/runtime_implementor/SKILL.md`
4. `skills/runtime_verifier/SKILL.md`
5. `workstream_templates/spec_template.md`
6. `workstream_templates/state_template.md`

Do not substitute guessed source paths if these exist.

### 3. Scan the target repo

Determine:

1. repo mode
2. primary project type
3. technology tags
4. likely setup / build / test / lint / typecheck commands
5. existing agent instruction files
6. existing companion systems
7. high-risk operations that should require approval

### 4. Ask the adaptive question block

Use the minimal questionnaire from `install/init_contract.md`.

Ask only when something remains unresolved after the scan.

Typical reasons to ask:

1. existing root instruction files cannot be patched safely
2. canonical commands remain ambiguous
3. approval-sensitive operations remain unclear
4. repo mode or primary type would be misleading if guessed

Ask in one concise block.
Do not ask deep implementation trivia.
Do not ask questions that do not change install output.

### 5. Write or patch target bootstrap files

Create or patch:

1. `AGENTS.md`
2. `CLAUDE.md`
3. `devs/project.md`
4. `devs/install_manifest.json`
5. `workstreams/README.md`
6. `workstreams/_templates/spec.md`
7. `workstreams/_templates/workstream.md`

Use the blueprints in `install/init_contract.md` for generated files.
Do not block on missing source bootstrap templates.

### 6. Install local work-role skills

Copy the current source role skills into:

- `.claude/skills/devs_spec_author/SKILL.md`
- `.claude/skills/devs_runtime_implementor/SKILL.md`
- `.claude/skills/devs_runtime_verifier/SKILL.md`
- `.agents/skills/devs_spec_author/SKILL.md`
- `.agents/skills/devs_runtime_implementor/SKILL.md`
- `.agents/skills/devs_runtime_verifier/SKILL.md`

Do not install `devs_init_repo` into the target repo unless the user explicitly
asks for local refresh tooling.

### 7. Stop and report

Return:

1. repo classification
2. questions asked and answers
3. files written
4. files patched
5. unresolved issues
6. the exact next suggested prompt for the first real workstream

## Output requirements

Your final install report must include:

1. target repo mode
2. primary project type
3. technology tags
4. files written
5. files patched
6. checks or decisions still pending
7. next suggested prompt

## Common failure modes to avoid

1. asking too many questions before scanning the repo
2. blocking on a non-existent `install/templates/` source folder
3. overwriting existing root instruction files blindly
4. rewriting the current role skills during install
5. asking `submodule vs copied repo files` when the user only supplied Devs as a
   remote source repo
6. copying installer internals into the target repo without a user request
7. leaving the target repo dependent on the source repo for everyday Devs work
8. starting real feature work before bootstrap is complete
