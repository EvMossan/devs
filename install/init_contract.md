# Devs Bootstrap Contract

## Purpose

Install Devs into the current repository in a way that is:

1. low-friction on first run
2. adaptive to the target project
3. self-contained for future Devs work after installation
4. clean about what is always loaded vs on-demand
5. generic across software repositories instead of tuned only for mobile

Self-contained means the target repo can run future Devs workstreams from local
bootstrap files, local workstream templates, and repo-local role skills.
It does **not** require a local mirror of the source installer internals.

## Non-Negotiable Rules

1. The install flow is agent-native. The agent should do the work.
2. Scan the target repo before asking questions.
3. Ask only the minimum unresolved questions in one concise block.
4. Keep `AGENTS.md` short, broad, and always-loaded.
5. Keep `CLAUDE.md` as a thin shim that imports `AGENTS.md`.
6. Copy the current authoritative Devs work-role skills verbatim from the
   source repo into the target repo:
   - `devs_spec_author`
   - `devs_runtime_implementer`
   - `devs_runtime_verifier`
7. Copy the current authoritative workstream templates verbatim from the
   source repo into the target repo.
8. Install repo-local skills for both Claude and Codex by default so the target
   repo is ready regardless of which tool the next session uses.
9. Do not install Superpowers or Spec Kit by default.
10. Detect existing companion systems and record them in `devs/project.md`.
11. Do not start feature work after install. Stop after bootstrap.
12. If an existing repo instruction file cannot be patched safely, ask the user
    how to merge it instead of overwriting it.
13. Do not require or reference a source-level `install/templates/` directory.
14. Do not generate `devs/bootstrap/*` mirror files in the target repo by
    default.
15. Repo classification is advisory metadata only. It must not fork the Devs
    role workflow into separate mobile/backend/data-only processes.

## Source Repo Discovery

The installer must determine the source repo path or URL first.

Acceptable source forms:

1. local path to a Devs checkout
2. git URL to the Devs repository
3. raw URL pointing directly at `install/INSTALL.md`

If only a raw URL is provided, infer the source repository root from that URL.

## Current Authoritative Source Paths

Use these exact source paths in the current Devs repo:

### Install files

1. `install/INSTALL.md`
2. `install/init_contract.md`

### Role skills

3. `skills/init_repo/SKILL.md`
4. `skills/spec_author/SKILL.md`
5. `skills/runtime_implementer/SKILL.md`
6. `skills/runtime_verifier/SKILL.md`

### Workstream templates

7. `workstream_templates/spec_template.md`
8. `workstream_templates/state_template.md`

If any required source file above is missing, stop with a bootstrap blocker.

## Target Repo Scan

Before asking questions, scan the target repo for:

1. git root and current working directory
2. empty/new vs existing/brownfield state
3. likely commands:
   - setup / install
   - build
   - test
   - lint
   - typecheck
4. package / workspace signals:
   - manifest files
   - lockfiles
   - project roots
   - monorepo markers
5. existing `AGENTS.md`, `CLAUDE.md`, `.claude/`, `.agents/`, `.specify/`,
   `docs/`, `.codex/`, and other process or agent instruction files
6. existing companion systems such as Superpowers or Spec Kit
7. obvious high-risk operations:
   - deploy
   - infrastructure apply
   - production migrations
   - destructive data changes
8. repo language / framework signals useful for `devs/project.md`

## Advisory Classification Model

Use the simplest truthful classification that fits the target repo.

### Repo mode

1. `greenfield`
2. `brownfield`
3. `mixed`

### Primary project type

Use one advisory value:

1. `application`
2. `service`
3. `library`
4. `mobile`
5. `data`
6. `infra`
7. `monorepo`
8. `generic`

### Technology tags

Also record a short list of observed tags, for example:

- `swift`
- `ios`
- `python`
- `typescript`
- `node`
- `terraform`
- `postgres`
- `react`
- `monorepo`

These tags are descriptive only.
They help fill `devs/project.md`.
They do not change the Devs role model.

## Minimal Adaptive Questionnaire

Ask the user one concise question block **only** for unresolved points.

### Ask only when needed

1. Existing root instruction files were found and safe patching is ambiguous.
   Ask how to merge:
   - `patch existing`
   - `import / shim where possible`
   - `proposal only`
2. Canonical commands remain ambiguous after scanning.
   Ask to confirm or correct:
   - setup / install
   - build
   - test
   - lint
   - typecheck
3. Approval-sensitive operations are unclear.
   Ask which operations always require explicit human approval.
4. Repo mode or primary project type is genuinely unclear and would make
   `devs/project.md` misleading if guessed.

### Question rules

1. Ask in one concise block.
2. Prefer explicit options over open-ended questions.
3. Do not ask deep implementation trivia.
4. Do not ask questions that do not change install output.
5. If the scan is already clear enough, ask nothing and proceed.

## Files to Generate or Patch in the Target Repo

### Always-loaded adapter files

1. `AGENTS.md`
2. `CLAUDE.md`

### Extended repo profile

3. `devs/project.md`
4. `devs/install_manifest.json`

### Workstream scaffolding

5. `workstreams/README.md`
6. `workstreams/_templates/spec.md`
7. `workstreams/_templates/workstream.md`

### Repo-local Claude skills

8. `.claude/skills/devs_spec_author/SKILL.md`
9. `.claude/skills/devs_runtime_implementer/SKILL.md`
10. `.claude/skills/devs_runtime_verifier/SKILL.md`

### Repo-local Codex skills

11. `.agents/skills/devs_spec_author/SKILL.md`
12. `.agents/skills/devs_runtime_implementer/SKILL.md`
13. `.agents/skills/devs_runtime_verifier/SKILL.md`

## File Writing Rules

### `AGENTS.md`

If no root `AGENTS.md` exists:
- create it from the blueprint below

If a root `AGENTS.md` already exists:
- preserve existing project truth
- patch it minimally with Devs sections rather than replacing it wholesale
- if patching would be ambiguous or destructive, ask the merge question

#### `AGENTS.md` blueprint

Keep it short.

Recommended sections:

1. `Mission`
   - one short paragraph on why Devs is installed here
2. `Working Model`
   - `clarify -> specify -> implement -> verify`
   - one bounded workstream at a time
   - repo artifacts, not chat memory, hold the contract and state
3. `Local Devs Files`
   - point to `devs/project.md`
   - point to `workstreams/`
4. `Role Routing`
   - when to use `devs_spec_author`
   - when to use `devs_runtime_implementer`
   - when to use `devs_runtime_verifier`
5. `Core Guardrails`
   - no implementation before a bounded workstream contract exists
   - implementation does not self-approve
   - report checks not run
   - keep changes bounded to the current slice

Do **not** turn `AGENTS.md` into a second long workflow manual.
Do **not** duplicate the full skill content there.

### `CLAUDE.md`

If no root `CLAUDE.md` exists:
- create it as exactly:

```md
@AGENTS.md
```

If a root `CLAUDE.md` already exists:
- preserve existing Claude-specific guidance where possible
- ensure it imports `@AGENTS.md` if that is safe
- if the file already carries a valid import or equivalent shared bootstrap, do
  not duplicate it

### `devs/project.md`

Create this file directly from the blueprint below.
No source-level template file is required.

#### `devs/project.md` blueprint

Keep operational facts only.

Recommended sections:

1. `Repo Snapshot`
   - repo mode
   - primary project type
   - technology tags
2. `Important Paths`
   - key app / service / package roots
3. `Canonical Commands`
   - setup / install
   - build
   - test
   - lint
   - typecheck
4. `Human Approval Required`
   - operations that always require explicit approval
5. `Existing Agent / Process Systems`
   - existing `AGENTS.md`, `CLAUDE.md`, `.claude/`, `.agents/`, `.specify/`,
     Superpowers, Spec Kit, other notable systems
6. `Install Notes`
   - merge choices
   - warnings
   - unresolved follow-ups

Rules:

1. prefer concrete commands and paths over prose
2. remove or mark irrelevant subsections as `N/A`
3. keep it repo-specific and readable
4. do not copy generic Devs theory here

### `devs/install_manifest.json`

Record:

1. source repo URL or local path
2. source ref if known
3. source entrypoint path
4. install timestamp
5. target repo mode
6. target primary project type
7. technology tags
8. questions asked and answers
9. files written
10. files patched
11. notable warnings or unresolved issues

Suggested top-level keys:

- `installed_at`
- `source`
- `target`
- `questions`
- `files_written`
- `files_patched`
- `warnings`

### `workstreams/`

Copy current authoritative workstream templates from the source repo:

- `workstream_templates/spec_template.md` -> `workstreams/_templates/spec.md`
- `workstream_templates/state_template.md` -> `workstreams/_templates/workstream.md`

Create `workstreams/README.md` directly from the blueprint below.

#### `workstreams/README.md` blueprint

Recommended contents:

1. what belongs in this folder
2. how to start a new bounded workstream
3. how to use the two templates
4. naming guidance:
   - choose descriptive names
   - keep contract and state paired
5. reminder that verification is a separate role

This file should explain the local workstream convention only.
It should not restate all Devs theory.

### Role skills

Copy these source skill files verbatim into both tool directories:

- `skills/spec_author/SKILL.md`
- `skills/runtime_implementer/SKILL.md`
- `skills/runtime_verifier/SKILL.md`

Map them to:

- `.claude/skills/devs_spec_author/SKILL.md`
- `.claude/skills/devs_runtime_implementer/SKILL.md`
- `.claude/skills/devs_runtime_verifier/SKILL.md`
- `.agents/skills/devs_spec_author/SKILL.md`
- `.agents/skills/devs_runtime_implementer/SKILL.md`
- `.agents/skills/devs_runtime_verifier/SKILL.md`

Do not rewrite the role content during install.

### Existing local skills

Do not delete unrelated project skills in `.claude/skills` or `.agents/skills`.

For local `devs_*` skill directories:
- overwrite the three installed work roles with the current source versions
- record the refresh in `devs/install_manifest.json`

## Companion Systems

Do not install or scaffold these by default:

1. Superpowers
2. Spec Kit

But if they already exist locally:

1. detect them
2. record them in `devs/project.md`
3. keep Devs as the governing workstream contract unless the repo explicitly
   says otherwise

## Success Criteria

The install is complete only when:

1. the target repo has a short root `AGENTS.md`
2. the target repo has a root `CLAUDE.md` shim
3. the target repo has `devs/project.md`
4. the target repo has `devs/install_manifest.json`
5. the target repo has `workstreams/README.md`
6. the target repo has local workstream templates
7. the target repo has repo-local Devs work roles for both Claude and Codex
8. the install did not require a source-level `install/templates/` directory
9. the install did not silently create `devs/bootstrap/*` mirror files
10. the agent has not silently started feature work

## Final Output Contract

After installation, report:

1. target repo mode
2. target primary project type
3. technology tags
4. questions asked and answers
5. files written
6. files patched
7. unresolved or manual follow-up items
8. the exact next suggested prompt to start the first real workstream

Also remind the user that future sessions can use the repo-local Devs work-role
skills directly.

## Suggested First Next Prompt

The installer should usually suggest a prompt in this shape:

`Use devs_spec_author to define the first workstream for: <user goal>.`

Tool-specific invocation hints:

- Claude Code: `/devs_spec_author`
- Codex: `$devs_spec_author`

Do not run that next prompt automatically.
