# Devs Agent-Native Install / Refresh

Use this file as the single bootstrap entrypoint when an agent installs or
refreshes Devs inside another repository.

Definitions:

- **Target repo** = the repository the agent is currently working in.
- **Source repo** = the Devs repository that contains this file.

The install or refresh should feel native:

1. scan bootstrap state first
2. ask only merge questions when patching is ambiguous and, on fresh install
   only, one optional final docs question
3. create or patch the target bootstrap files
4. install the current Devs work-role skills and support templates locally
5. stop after bootstrap

## Required read order

Before writing anything in the target repo:

1. read `install/init_contract.md`
2. read `skills/init_repo/SKILL.md`
3. read `skills/spec_author/SKILL.md`
4. read `skills/runtime_implementer/SKILL.md`
5. read `skills/runtime_verifier/SKILL.md`
6. read `workstream_templates/spec_template.md`
7. read `workstream_templates/state_template.md`
8. scan the target repo

If a required source file cannot be found, stop and report the blocker.

## Current authoritative source paths

In the current Devs repository, the authoritative install inputs are:

1. `install/INSTALL.md`
2. `install/init_contract.md`
3. `skills/init_repo/SKILL.md`
4. `skills/spec_author/SKILL.md`
5. `skills/runtime_implementer/SKILL.md`
6. `skills/runtime_verifier/SKILL.md`
7. `workstream_templates/spec_template.md`
8. `workstream_templates/state_template.md`

Do not assume a source-level `install/templates/` directory exists.
Do not block on it.
This install version uses the blueprints in `install/init_contract.md` instead of
source bootstrap templates.

## Source-repo interpretation rule

If the user provides a GitHub repo URL, git URL, or raw `install/INSTALL.md`
URL for Devs, treat it as **source context only**.

That means:

1. resolve the install entrypoint inside that source repo
2. read the source files from that repo
3. generate or patch bootstrap files in the current target repo

It does **not** mean:

1. add the Devs repo as a git submodule
2. vendor the whole Devs repo into the target repo
3. ask `submodule vs copied repo files` as the first install decision

Unless the user explicitly asks for submodule-based reuse, default to
**generated target files + copied repo-local skills/templates**, not repo
embedding.

## Non-negotiable behavior

1. Treat the current repo as the target repo.
2. Treat the repository containing this file as the source repo.
3. Do not rewrite the current Devs role skills during install.
   Copy the authoritative source versions verbatim into the target repo.
4. Install the repo-local work roles by default:
   - `devs_spec_author`
   - `devs_runtime_implementer`
   - `devs_runtime_verifier`
5. Do not install or generate `devs_init_repo` inside the target repo unless the
   user explicitly asks for local refresh tooling.
6. Do not create a local mirror of installer internals such as
   `devs/bootstrap/*` unless the user explicitly asks for it.
7. Do not start feature work after install or refresh.
8. Do not install Superpowers or Spec Kit by default.
9. Keep `AGENTS.md` short, broadly applicable, and workstream-centered.
   When patching an existing file, prefer one Devs-managed marker block instead
   of freeform whole-file editing.
10. Keep `CLAUDE.md` as a thin shim over `AGENTS.md`.
11. Prefer patching existing root instruction files over blind overwrite.
12. Keep the install simple. Do not infer repo truth from repo contents.
13. `.devs/` is the hidden Devs system layer.
14. `devs/` is the visible project artifact layer.
15. `devs/README.md` is Devs-managed and may be refreshed directly.
16. `devs/repo.md` is a repo-owned index of local guidance docs and must not be
    overwritten during normal refresh.
17. Visible `devs/specs/` and `devs/workstreams/` artifacts are project-owned.
18. `workstream` is the main continuity and delivery unit.
19. Same-target fix loops stay inside one workstream.
20. A formal spec is optional, but `spec-less` never means contract-less.
21. If the target repo already has Devs installed, treat this run as a refresh:
    refresh hidden/system support files and repo-local Devs role skills, patch
    shared bootstrap files minimally, preserve repo-owned visible work
    artifacts, and never overwrite an existing `devs/repo.md` during a normal
    refresh.
22. Do not discover commands, candidate docs, or other repo truth to populate
    `devs/repo.md`.

## What this install writes by default

1. `AGENTS.md`
2. `CLAUDE.md`
3. `devs/repo.md`
4. `.devs/install_manifest.json`
5. `.devs/templates/spec_template.md`
6. `.devs/templates/state_template.md`
7. `devs/README.md`
8. `devs/specs/`
9. `devs/workstreams/`
10. `.claude/skills/devs_spec_author/SKILL.md`
11. `.claude/skills/devs_runtime_implementer/SKILL.md`
12. `.claude/skills/devs_runtime_verifier/SKILL.md`
13. `.agents/skills/devs_spec_author/SKILL.md`
14. `.agents/skills/devs_runtime_implementer/SKILL.md`
15. `.agents/skills/devs_runtime_verifier/SKILL.md`

The target repo should describe the artifact model consistently:

- `.devs/` = hidden system support files
- `devs/README.md` = Devs-managed artifact map
- `devs/repo.md` = repo-owned index of local guidance docs
- `devs/specs/` = formal contract layer
- `devs/workstreams/` = living continuity layer
- specs may plan `Slice S1..N` inside a workstream
- repo workstreams use `ws-*`
- `stage` means lifecycle position inside one workstream

One workstream gets one living `state.md`.
That `state.md` carries the minimal contract whenever the workstream has no
formal spec.

## Refresh behavior

If the target repo already has Devs installed, treat the run as refresh, not
blind reinstall.

Refresh should:

1. refresh Devs-managed hidden support files and repo-local Devs role skills
2. patch shared bootstrap files minimally
   - `AGENTS.md` should be updated through the Devs-managed marker block when
     that model is in use
3. preserve repo-owned visible work artifacts and local guidance docs
4. not ask the fresh-install docs question during normal refresh
5. never overwrite an existing `devs/repo.md` during a normal refresh
6. fail the refresh audit if any required bootstrap target remains stale

The exact refresh ownership rules live in `install/init_contract.md`.

## Execution summary

Follow the algorithm in `install/init_contract.md`.

At the end, report:

1. install mode
2. local guidance status (`attached`, `skipped`, or `preserved unchanged`)
3. questions asked and answers
4. files written
5. files patched
6. unresolved issues or manual follow-ups
7. the exact next suggested prompt for the first real workstream or next
   Devs-role action
