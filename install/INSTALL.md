# Devs Agent-Native Install

Use this file as the single bootstrap entrypoint when an agent installs Devs
into another repository.

Definitions:

- **Target repo** = the repository the agent is currently working in.
- **Source repo** = the Devs repository that contains this file.

The install should feel native:

1. scan first
2. ask only the minimum unresolved questions
3. create or patch the target bootstrap files
4. install the current Devs workstream skills and templates locally
5. stop after installation

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
7. Do not start feature work after install.
8. Do not install Superpowers or Spec Kit by default.
   If they already exist locally, detect and record them.
9. Keep `AGENTS.md` short, broadly applicable, and workstream-centered.
10. Keep `CLAUDE.md` as a thin shim over `AGENTS.md`.
11. Prefer patching existing root instruction files over blind overwrite.
12. Keep the install generic. Repo classification is advisory metadata, not a
    workflow fork.

## What this install writes by default

1. `AGENTS.md`
2. `CLAUDE.md`
3. `devs/project.md`
4. `devs/install_manifest.json`
5. `workstreams/README.md`
6. `workstreams/_templates/spec.md`
7. `workstreams/_templates/workstream.md`
8. `.claude/skills/devs_spec_author/SKILL.md`
9. `.claude/skills/devs_runtime_implementer/SKILL.md`
10. `.claude/skills/devs_runtime_verifier/SKILL.md`
11. `.agents/skills/devs_spec_author/SKILL.md`
12. `.agents/skills/devs_runtime_implementer/SKILL.md`
13. `.agents/skills/devs_runtime_verifier/SKILL.md`

## Execution summary

Follow the algorithm in `install/init_contract.md`.

At the end, report:

1. target repo mode
2. advisory project classification and technology tags
3. questions asked and answers
4. files written
5. files patched
6. unresolved issues or manual follow-ups
7. the exact next suggested prompt for the first real workstream
