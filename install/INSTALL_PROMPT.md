# Devs Install Prompt

These are copy-paste prompts for the first bootstrap run.

## Best remote install prompt (raw entrypoint)

Install Devs in this repository from this bootstrap entrypoint:

`https://raw.githubusercontent.com/<OWNER>/<REPO>/<REF>/install/INSTALL.md`

Requirements:

1. Treat the current repository as the target repo.
2. Treat the referenced Devs repository as the source repo.
3. Read `install/INSTALL.md`, then follow `install/init_contract.md`.
4. Use the current authoritative source paths in the Devs repo:
   - `skills/init_repo/SKILL.md`
   - `skills/spec_author/SKILL.md`
   - `skills/runtime_implementor/SKILL.md`
   - `skills/runtime_verifier/SKILL.md`
   - `workstream_templates/spec_template.md`
   - `workstream_templates/state_template.md`
5. Scan this repo before asking questions.
6. Ask only the minimum unresolved questions in one concise block.
7. Create or patch the target bootstrap files, repo-local Devs skills, and
   workstream scaffolding.
8. Do not expect a source-level `install/templates/` directory.
9. Do not create `devs/bootstrap/*` mirror files in the target repo.
10. Do not treat the Devs source repo as a dependency, submodule, or vendored
    repo copy.
11. Stop after install. Do not start feature work.

## Alternate remote install prompt (GitHub repo URL)

Install Devs in this repository using this source repo:

`https://github.com/<OWNER>/<REPO>`

Requirements:

1. Treat the current repository as the target repo.
2. Treat that GitHub repository as the Devs **source repo only**.
3. Resolve and read `install/INSTALL.md` from the source repo, then follow
   `install/init_contract.md`.
4. Use the current authoritative source paths in the Devs repo:
   - `skills/init_repo/SKILL.md`
   - `skills/spec_author/SKILL.md`
   - `skills/runtime_implementor/SKILL.md`
   - `skills/runtime_verifier/SKILL.md`
   - `workstream_templates/spec_template.md`
   - `workstream_templates/state_template.md`
5. Scan this repo before asking questions.
6. Ask only the minimum unresolved questions in one concise block.
7. Create or patch the target bootstrap files, repo-local Devs skills, and
   workstream scaffolding.
8. Do not ask whether to add the source repo as a submodule or copy the whole
   repo unless I explicitly request that packaging model.
9. Do not expect a source-level `install/templates/` directory.
10. Do not create `devs/bootstrap/*` mirror files in the target repo.
11. Stop after install. Do not start feature work.

## Recommended local-path install prompt

Install Devs in this repository using this local bootstrap entrypoint:

`<PATH_TO_DEVS_REPO>/install/INSTALL.md`

Requirements:

1. Treat the current repository as the target repo.
2. Treat the local Devs checkout as the source repo.
3. Read `install/INSTALL.md`, then follow `install/init_contract.md`.
4. Use the current authoritative source paths in the Devs repo:
   - `skills/init_repo/SKILL.md`
   - `skills/spec_author/SKILL.md`
   - `skills/runtime_implementor/SKILL.md`
   - `skills/runtime_verifier/SKILL.md`
   - `workstream_templates/spec_template.md`
   - `workstream_templates/state_template.md`
5. Scan this repo before asking questions.
6. Ask only the minimum unresolved questions in one concise block.
7. Create or patch the target bootstrap files, repo-local Devs skills, and
   workstream scaffolding.
8. Do not expect a source-level `install/templates/` directory.
9. Do not create `devs/bootstrap/*` mirror files in the target repo.
10. Stop after install. Do not start feature work.

## Minimal install outcome

A successful v1 install should leave the target repo with:

1. `AGENTS.md`
2. `CLAUDE.md`
3. `devs/project.md`
4. `devs/install_manifest.json`
5. `workstreams/README.md`
6. `workstreams/_templates/spec.md`
7. `workstreams/_templates/workstream.md`
8. repo-local Devs work roles for Claude and Codex

## Stability note

When possible, pin `<REF>` to a tag or commit instead of a moving branch.
