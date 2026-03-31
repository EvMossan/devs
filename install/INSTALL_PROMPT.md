# Devs Install Prompt

These are copy-paste prompts for installation and refresh.

## Canonical install prompt

Install Devs in this repository from this bootstrap entrypoint:

`https://raw.githubusercontent.com/<OWNER>/<REPO>/<REF>/install/INSTALL.md`

Requirements:

1. Treat the current repository as the target repo.
2. Treat the referenced Devs repository as the source repo.
3. Read `install/INSTALL.md`, then follow `install/init_contract.md`.
4. Use the current authoritative source paths in the Devs repo:
   - `skills/init_repo/SKILL.md`
   - `skills/spec_author/SKILL.md`
   - `skills/runtime_implementer/SKILL.md`
   - `skills/runtime_verifier/SKILL.md`
   - `workstream_templates/spec_template.md`
   - `workstream_templates/state_template.md`
5. Scan this repo only for bootstrap state before asking questions.
6. Ask only merge questions when patching is ambiguous. On fresh install only,
   ask one optional final question about local guidance docs.
7. Create or patch the target bootstrap files, repo-local Devs skills, hidden
   `.devs/` support files, and visible `devs/` artifact directories.
8. Do not expect a source-level `install/templates/` directory.
9. Do not create `devs/bootstrap/*` mirror files in the target repo.
10. Do not treat the Devs source repo as a dependency, submodule, or vendored
    repo copy.
11. Stop after install or refresh. Do not start feature work.
12. Use `.devs/` as the hidden system layer and `devs/` as the visible project
    artifact layer.
13. Keep `devs/repo.md`, `devs/specs/`, and `devs/workstreams/` repo-owned, and
    keep `devs/README.md` Devs-managed.
14. Treat `workstream` as the main continuity and delivery unit.
15. Allow `spec-less workstream`, but require its minimal contract to live in
    `state.md`.
16. Do not discover commands, candidate docs, or inferred repo standards to
    populate `devs/repo.md`.
17. If Devs is already installed here, treat this run as a refresh: refresh
    Devs-managed support files and role skills, patch shared bootstrap files
    minimally, preserve repo-owned visible artifacts, and never overwrite an existing
    `devs/repo.md` during a normal refresh.

## Canonical refresh prompt

Refresh the existing Devs install in this repository using this source:

`https://raw.githubusercontent.com/<OWNER>/<REPO>/<REF>/install/INSTALL.md`

Requirements:

1. Treat the current repository as the target repo.
2. Treat the referenced Devs repository as the source repo.
3. Read `install/INSTALL.md`, then follow `install/init_contract.md`.
4. Detect the existing Devs install first, then run refresh rather than a blind
   reinstall.
5. Refresh hidden Devs support files and repo-local Devs role skills from the
   current source version.
6. Patch `AGENTS.md` through the Devs-managed marker block when present, and
   patch `CLAUDE.md` plus `devs/README.md` minimally.
7. Preserve `devs/repo.md`, `devs/specs/`, `devs/workstreams/`, and any
   local guidance docs already in use.
8. Do not ask the optional local-guidance question during normal refresh.
9. If `devs/repo.md` is missing, stop and report bootstrap drift instead of
   recreating it.
10. Run an exact refresh audit and do not report `pass` if a required bootstrap
    target remains stale.
11. Stop after refresh and report exactly which files were updated or patched.

## Alternate source forms

Use the same install or refresh requirements above, but swap only the source
form:

### GitHub repo URL

`https://github.com/<OWNER>/<REPO>`

Special note:

- Treat that GitHub repository as the Devs **source repo only**.
- Do not ask whether to add it as a submodule or copy the whole repo unless I
  explicitly request that packaging model.

### Local path

`<PATH_TO_DEVS_REPO>/install/INSTALL.md`

## Minimal install outcome

A successful install should leave the target repo with:

1. `AGENTS.md`
2. `CLAUDE.md`
3. `devs/repo.md`
4. `.devs/install_manifest.json`
5. `.devs/templates/spec_template.md`
6. `.devs/templates/state_template.md`
7. `devs/README.md`
8. `devs/specs/`
9. `devs/workstreams/`
10. repo-local Devs work roles for Claude and Codex

The resulting repo should describe one model consistently:

- `.devs/` holds only Devs-managed internal support files
- `devs/repo.md` holds a repo-owned index of local guidance docs
- `devs/README.md` is the Devs-managed artifact map
- `workstream` is the main continuity and delivery unit
- same-target fix loops stay inside one workstream
- one workstream gets one living `state.md`
- a formal spec is optional
- `spec-less` is allowed, but not contract-less
- specs may plan `Slice S1..N` inside a workstream
- repo workstreams use `ws-*`
- `stage` means lifecycle position inside one workstream

## Stability note

When possible, pin `<REF>` to a tag or commit instead of a moving branch.
