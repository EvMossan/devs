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
16. A Devs GitHub repo URL, git URL, or raw install URL is **source context**,
    not a package-install request. Do not default to `submodule vs vendored
    repo copy` questions unless the user explicitly asks for that packaging
    model.

## Source Repo Discovery

The installer must determine the source repo path or URL first.

Acceptable source forms:

1. local path to a Devs checkout
2. git URL to the Devs repository
3. raw URL pointing directly at `install/INSTALL.md`

If only a raw URL is provided, infer the source repository root from that URL.

## Source URL Interpretation

When the user gives a GitHub repo URL or git URL for Devs:

1. treat that repo as the authoritative **source** of install instructions,
   skill files, and workstream templates
2. resolve `install/INSTALL.md` inside that repo
3. generate or patch files in the current target repo

Do not ask whether the whole Devs repo should be added to the target repo as a
submodule or copied into the tree unless the user explicitly requests that
installation model.

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
- if safe patching is ambiguous, ask the merge question

### `devs/project.md`

Create from the blueprint below and fill only the sections that are actually
useful.

Rules:

1. keep operational facts only
2. prefer concrete commands and paths over prose
3. record detected companion systems
4. record merge / patch decisions made during install
5. keep repo classification advisory and concise
6. include only the repo-type notes that are actually relevant

Recommended sections:

1. `Repository Profile`
   - repo mode
   - primary project type
   - technology tags
2. `Canonical Commands`
   - setup / install
   - build
   - test
   - lint
   - typecheck
3. `Approval-Sensitive Operations`
4. `Detected Companion Systems`
5. `Instruction File Notes`
6. `Workstream Notes`
   - where workstream contracts and state live
7. `Open Install Warnings`
   - only if needed

### `devs/install_manifest.json`

Record:

1. source repo URL or local path
2. source ref if known
3. source entrypoint used
4. install timestamp
5. target repo mode
6. primary project type
7. technology tags
8. questions asked and answers
9. files written and patched
10. notable warnings or unresolved issues

### `workstreams/`

Copy current authoritative workstream templates from the source repo:

- `workstream_templates/spec_template.md` -> `workstreams/_templates/spec.md`
- `workstream_templates/state_template.md` -> `workstreams/_templates/workstream.md`

Create `workstreams/README.md` from the blueprint below.

#### `workstreams/README.md` blueprint

Keep it short.

Recommended sections:

1. `Purpose`
   - Devs stores the current workstream contract and state here
2. `Templates`
   - `workstreams/_templates/spec.md`
   - `workstreams/_templates/workstream.md`
3. `Suggested Flow`
   - spec author writes a bounded contract
   - implementer executes one approved slice
   - verifier decides pass or blocked
4. `Naming`
   - descriptive workstream names
   - keep one current contract and one current state file per workstream where possible

### Role skills

Copy each authoritative work-role skill file verbatim into both:

- `.claude/skills/<skill-name>/SKILL.md`
- `.agents/skills/<skill-name>/SKILL.md`

Install these by default:

- `devs_spec_author`
- `devs_runtime_implementer`
- `devs_runtime_verifier`

Do not install `devs_init_repo` into the target repo unless the user explicitly
asks for repo-local refresh tooling.

### Existing local skills

Do not delete unrelated project skills in `.claude/skills` or `.agents/skills`.

For local `devs_*` role skills:
- overwrite them with the source versions from this install
- record the refresh in `devs/install_manifest.json`

## Companion Systems

Do not install or scaffold these by default:

1. Superpowers
2. Spec Kit

But if they already exist locally:

1. detect them
2. record them in `devs/project.md`
3. keep Devs as the governing contract and workstream system unless the repo
   explicitly says otherwise

## Execution Mode Default

For v1 installs, the default is:

- `manual_roles`

The installer may record other local preferences in `devs/project.md`, but it
does not need to scaffold controller/orchestrator files in this version.

## Success Criteria

The install is complete only when:

1. the target repo has a short root `AGENTS.md`
2. the target repo has a root `CLAUDE.md` shim
3. the target repo has `devs/project.md`
4. the target repo has `workstreams/README.md`
5. the target repo has local workstream templates
6. the target repo has repo-local Devs skills for both Claude and Codex
7. `devs/install_manifest.json` truthfully records what happened
8. the agent has not silently started feature work

## Final Output Contract

After installation, report:

1. target repo mode
2. primary project type
3. technology tags
4. files written
5. files patched
6. any unresolved or manual follow-up items
7. the exact next suggested prompt to start the first real workstream

Also remind the user that future sessions can use the repo-local role skills
directly.
