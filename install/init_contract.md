# Devs Bootstrap Contract

## Purpose

Install or refresh Devs in the current repository in a way that is:

1. low-friction on first run
2. safe around existing bootstrap files
3. self-contained for future Devs work after installation
4. clear about Devs-owned files vs repo-owned files
5. consistent with the workstream-based artifact model

Self-contained means the target repo can run future Devs work from repo-local
bootstrap files, hidden support templates, repo-local role skills, and
project-owned Devs artifacts.
It does **not** require a local mirror of the source installer internals.

## Artifact Model

Use this model consistently:

1. `.devs/` = hidden Devs system layer
2. `devs/README.md` = visible Devs-managed artifact map
3. `devs/repo.md` = visible repo-owned index of local guidance docs
4. `devs/specs/` = formal contract layer
5. `devs/workstreams/` = living continuity layer

The main continuity and delivery unit is the `workstream`.

Rules:

1. same-target fix loops stay inside the same workstream
2. open a new workstream only when the target outcome or scope changes
   materially
3. one workstream gets one living `state.md`
4. a formal spec is optional
5. `spec-less workstream` is allowed, but not contract-less
6. if no formal spec exists, the minimal contract must live in `state.md`
7. specs may plan `Slice S1..N` inside a workstream
8. planned `S1..N` and workstream IDs such as `ws-*` stay distinct
9. `stage` means the lifecycle position inside one workstream

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
7. Copy the current authoritative support templates verbatim from the source
   repo into the target repo.
8. Install repo-local skills for both Claude and Codex by default so the target
   repo is ready regardless of which tool the next session uses.
9. Do not install Superpowers or Spec Kit by default.
10. Do not infer repo truth from repo contents during install.
11. Do not start feature work after install or refresh. Stop after bootstrap.
12. If an existing repo instruction file cannot be patched safely, ask the user
    how to merge it instead of overwriting it.
13. Do not require or reference a source-level `install/templates/` directory.
14. Do not generate `devs/bootstrap/*` mirror files in the target repo by
    default.
15. A Devs GitHub repo URL, git URL, or raw install URL is **source context**,
    not a package-install request. Do not default to `submodule vs vendored
    repo copy` questions unless the user explicitly asks for that packaging
    model.
16. `.devs/**`, `devs/README.md`, and repo-local Devs role skills are
    Devs-owned and refresh-managed.
17. `devs/repo.md`, `devs/specs/**`, and `devs/workstreams/**` are repo-owned.
18. Do not fall back to a project-wide state file or a per-session state model.
19. If Devs is already installed, treat the run as a refresh, not a blind
    reinstall.
20. Refresh Devs-owned support files directly, patch shared bootstrap files
    minimally, preserve repo-owned files, and never overwrite an existing
    `devs/repo.md` during a normal refresh.
21. Do not report refresh `pass` unless every required bootstrap target is
    present and synchronized.

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
   role skills, and support templates
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

### Support templates

7. `workstream_templates/spec_template.md`
8. `workstream_templates/state_template.md`

If any required source file above is missing, stop with a bootstrap blocker.

## Target Repo Scan

Before asking questions, scan the target repo only for bootstrap state:

1. git root and current working directory
2. whether Devs is already installed here
3. existing `AGENTS.md`, `CLAUDE.md`, `.claude/`, `.agents/`, `devs/`,
   `.devs/`, and other root instruction files relevant to safe patching
4. existing `devs/repo.md` if Devs is already installed

## Minimal Adaptive Questionnaire

Ask the user one concise question block **only** for unresolved merge points.

### Ask only when needed

1. Existing root instruction files were found and safe patching is ambiguous.
   Ask how to merge:
   - `patch existing`
   - `import / shim where possible`
   - `proposal only`

### Fresh-install optional docs step

On fresh install only, after bootstrap decisions are otherwise resolved, ask one
optional final question unless the user already answered it:

- whether they want to attach local guidance docs now
- if yes, ask for explicit repo paths or a short explanation of what to attach
- if no, continue without blocking install

On refresh:

- do not ask this question during normal refresh
- preserve `devs/repo.md` unchanged
- if `devs/repo.md` is missing, stop and surface bootstrap drift

### Question rules

1. Ask in one concise block.
2. Keep the local-guidance step optional and skippable.
3. Do not present repo-discovered candidate docs.
4. Do not ask about commands, approval-sensitive operations, or inferred repo
   standards.
5. Do not ask questions that do not change install output.

## Files to Generate or Patch in the Target Repo

### Always-loaded adapter files

1. `AGENTS.md`
2. `CLAUDE.md`

### Hidden Devs system layer

3. `.devs/install_manifest.json`
4. `.devs/templates/spec_template.md`
5. `.devs/templates/state_template.md`

### Visible Devs-managed artifact layer

6. `devs/README.md`

### Visible repo-owned artifact layer

7. `devs/repo.md`
8. `devs/specs/`
9. `devs/workstreams/`

### Repo-local Claude skills

10. `.claude/skills/devs_spec_author/SKILL.md`
11. `.claude/skills/devs_runtime_implementer/SKILL.md`
12. `.claude/skills/devs_runtime_verifier/SKILL.md`

### Repo-local Codex skills

13. `.agents/skills/devs_spec_author/SKILL.md`
14. `.agents/skills/devs_runtime_implementer/SKILL.md`
15. `.agents/skills/devs_runtime_verifier/SKILL.md`

## File Writing Rules

### `AGENTS.md`

If no root `AGENTS.md` exists:
- create it from the blueprint below

If a root `AGENTS.md` already exists:
- preserve existing project truth
- patch it through one Devs-managed block rather than replacing it wholesale
- if patching would be ambiguous or destructive, ask the merge question

#### Managed patch rule

When patching an existing `AGENTS.md`, use one managed block with exact markers:

```md
<!-- DEVS:BOOTSTRAP:START -->
...Devs-managed bootstrap content...
<!-- DEVS:BOOTSTRAP:END -->
```

Rules:

1. if the markers already exist, update only the content inside them
2. do not rewrite unrelated repo-owned sections outside the markers
3. if no markers exist yet, add one Devs-managed block in a safe location rather
   than attempting a freeform whole-file rewrite
4. if no safe insertion point exists, stop and ask the merge question

#### `AGENTS.md` blueprint

Keep it short.

Recommended sections:

1. `Mission`
   - one short paragraph on why Devs is installed here
2. `Working Model`
   - `clarify -> specify -> implement -> verify`
   - `workstream` is the main continuity and delivery unit
   - a workstream is the full loop for one target outcome
   - repo artifacts, not chat memory, hold the contract and state
3. `Local Devs Files`
   - point to `devs/README.md`
   - point to `devs/repo.md`
   - point to `devs/specs/` and `devs/workstreams/`
4. `Context Loading`
   - read `AGENTS.md` first
   - when entering Devs operational work, read `devs/README.md`
   - then read `devs/repo.md` for any repo-specific guidance docs Devs should
     read
   - for a specific workstream, read the relevant `state.md`
   - if that `state.md` links a formal spec and contract details matter, read
     the linked `spec.md`
5. `Role Routing`
   - when to use `devs_spec_author`
   - when to use `devs_runtime_implementer`
   - when to use `devs_runtime_verifier`
6. `Core Guardrails`
   - no implementation before a bounded workstream contract exists
   - `spec-less` is allowed, but not contract-less
   - same-target fix loops stay inside one workstream
   - implementation does not self-approve
   - report checks not run
   - keep changes bounded to the current slice

For fresh installs, the generated Devs bootstrap content may be wrapped in the
same managed markers to make later refreshes deterministic.

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

### `devs/repo.md`

Create this file on fresh install.

During refresh:

1. if `devs/repo.md` already exists, preserve it
2. if `devs/repo.md` is missing and Devs is otherwise installed, stop and surface
   bootstrap drift instead of guessing

Rules:

1. keep repo-owned guidance only
2. include only docs the user explicitly attached
3. prefer repo-relative paths and short purpose notes over prose
4. do not put install history, source refs, refresh mechanics, or inferred repo
   facts here
5. do not let refresh overwrite this file during normal operation

Recommended sections:

1. `Active Local Guidance`
   - repo-owned docs Devs should treat as active local guidance
   - each item may include a short purpose note when useful

If no local guidance docs were attached during install, create the file with a
short note that none were attached yet and that maintainers can add paths
later.

### `.devs/install_manifest.json`

Record:

1. source repo URL or local path
2. source ref if known
3. source entrypoint used
4. install timestamp
5. install mode (`install` or `refresh`)
6. local guidance status:
   - `attached`
   - `skipped`
   - `preserved unchanged`
7. explicit local guidance docs attached, if any
8. questions asked and answers
9. files written and patched
10. notable warnings or unresolved issues

### Hidden support templates

Copy current authoritative support templates from the source repo:

- `workstream_templates/spec_template.md` -> `.devs/templates/spec_template.md`
- `workstream_templates/state_template.md` -> `.devs/templates/state_template.md`

These are hidden Devs support files.
They are not the visible project artifacts themselves.

### `devs/README.md`

Create from the blueprint below.

Keep it short.

Recommended sections:

1. `Purpose`
   - `devs/` stores visible project-facing Devs artifacts
2. `Structure`
   - `devs/repo.md` stores a repo-owned index of local guidance docs
   - `devs/specs/` stores formal specs
   - `devs/workstreams/` stores repo workstreams
3. `Ownership`
   - `devs/README.md` is Devs-managed
   - `devs/repo.md` is repo-owned
   - `devs/specs/` and `devs/workstreams/` are repo-owned
4. `Workstream Rules`
   - `workstream` is the main continuity and delivery unit
   - a workstream is the full loop for one target outcome
   - same-target fix loops stay inside one workstream
   - one workstream gets one living `state.md`
   - a formal spec is optional
   - `spec-less` is allowed, but not contract-less
   - the minimal contract for spec-less work lives in `state.md`
5. `Artifact Roles`
   - `AGENTS.md` routes the agent to the right context
   - `devs/README.md` explains the Devs artifact map
   - `devs/repo.md` lists local guidance docs Devs should read
   - `state.md` is the living truth for one workstream
   - `spec.md` is the formal contract for that workstream when present
   - role skills define how each role should work
6. `How To Read This`
   - start with `AGENTS.md`
   - read `devs/README.md` when doing Devs operational work
   - read `devs/repo.md` for any local guidance docs Devs should read
   - read the relevant workstream `state.md` before acting
   - read the linked `spec.md` when the state points to one and contract details
     matter
7. `Naming`
   - specs may plan `Slice S1..N`
   - a slice is a planned unit inside the workstream, not a separate workstream
   - repo workstreams use `ws-*`
   - `stage` means the lifecycle position inside one workstream

Do not describe `devs/README.md` as repo-owned.
It is visible but Devs-managed.

### Visible artifact directories

Ensure these directories exist:

- `devs/specs/`
- `devs/workstreams/`

Do not pre-create fake active work artifacts just to fill the directories.

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
- record the refresh in `.devs/install_manifest.json`

## Refresh Ownership Rules

When the target repo already has Devs installed:

1. refresh directly:
   - `.devs/install_manifest.json`
   - `.devs/templates/*`
   - `devs/README.md`
   - `.claude/skills/devs_*`
   - `.agents/skills/devs_*`
2. patch minimally:
   - `AGENTS.md` inside the managed marker block
   - `CLAUDE.md`
3. never recreate during normal refresh:
   - if `devs/repo.md` is missing, stop and surface bootstrap drift
4. preserve as repo-owned:
   - `devs/repo.md` once it exists
   - `devs/specs/**`
   - `devs/workstreams/**`
   - local guidance docs the user attached intentionally

## Exact Refresh Audit

Refresh cannot report `pass` unless all of these are true:

1. `AGENTS.md` routes through `devs/README.md` and `devs/repo.md`
   and the Devs-managed bootstrap block is present and current
2. `CLAUDE.md` imports `@AGENTS.md` or an equivalent shared bootstrap safely
3. `devs/README.md` describes `devs/repo.md` as repo-owned active local
   guidance docs
4. `devs/repo.md` exists
5. hidden support templates match the authoritative source
6. repo-local Devs role skills for both Claude and Codex match the
   authoritative source
7. the install manifest records the optional local-guidance decision and all
   files written or patched

If any item above is false, the refresh must report a blocker or pending follow-up,
not `pass`.

## Success Criteria

The install is complete only when:

1. the target repo has a short root `AGENTS.md`
2. the target repo has a root `CLAUDE.md` shim
3. the target repo has `devs/repo.md`
4. the target repo has `.devs/install_manifest.json`
5. the target repo has hidden Devs support templates in `.devs/templates/`
6. the target repo has `devs/README.md`
7. the target repo has visible `devs/specs/` and `devs/workstreams/`
8. the target repo has repo-local Devs skills for both Claude and Codex
9. `devs/repo.md` contains only explicitly attached local guidance docs or a
   short empty-state note
10. the artifact model is described consistently across root guidance, local
    Devs files, and role skills
11. the agent has not silently started feature work

## Final Output Contract

After installation or refresh, report:

1. install mode
2. local guidance status:
   - `attached`
   - `skipped`
   - `preserved unchanged`
3. questions asked and answers
4. files written
5. files patched
6. any unresolved or manual follow-up items
7. the exact next suggested prompt to start the first real workstream or next
   Devs-role action

Also remind the user that future sessions can use the repo-local role skills
directly.
