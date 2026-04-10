# Workstream Contract: Devs Artifact Structure Refactor

## Metadata

- Workstream ID: `artifact-structure-refactor`
- Status: `draft`
- Last updated by role: `spec-author`

## Objective

Finalize one clear artifact model for Devs and align the repo-facing docs,
install docs, init guidance, and templates to that model.

## Problem / Context

The repo already leans toward a workstream-based model, but the contract is not
yet explicit enough for a deterministic refactor.

Without one clear contract, the repo risks keeping mixed terminology, unclear
continuity rules, and mismatched install/template outputs.

## Before / After Summary

| Area | Before | After |
|---|---|---|
| Continuity unit | continuity logic is partly mixed between spec, phase, handoff, and workstream | `workstream` is the main continuity and delivery unit |
| Fix loops | rework logic exists but is not stated tightly enough | spec fixes, impl fixes, and verifier fixes stay inside the same workstream while the acceptance target stays the same |
| Formal spec | spec still looks close to a required container | spec is an optional contract layer |
| Spec-less work | allowed in principle, but under-specified | allowed explicitly, with a minimal contract in `state.md` |
| State model | workstream-level direction exists, but needs full contract wording | one living `state.md` per workstream |
| Planned slices | old `Phase 1..N` wording still leaks into the model | specs use `Slice S1..N` for planned slices inside the workstream |
| Repo IDs | relationship between planned slices and the workstream is not fully explicit | `S1..N` are planned slices; `ws-*` is the workstream ID |
| Terminology | `phase` language can collide with execution stages | `stage` is the lifecycle position inside one workstream |
| Artifact ownership | hidden/system and visible/project layers are not fully pinned down | `.devs/` is hidden system layer; `devs/` is visible project artifact layer |

## Clarification Record

### Clarification Coverage Summary

| Domain | Status (`answered|already_decided|deferred|n/a`) | Why This Status Is Acceptable | Notes / Contract Impact |
|---|---|---|---|
| Requested outcome | `answered` | The work is a deterministic docs/template refactor contract | The next session should be able to execute it directly |
| User-visible behavior and flow | `answered` | This changes repo workflow artifacts, not product runtime behavior | Workstream becomes the explicit continuity unit |
| Environment / platform | `answered` | Repo-local markdown and template changes only | No external runtime dependency |
| Hard constraints | `answered` | The user wants a compact, direct contract | Keep the spec short and executable |
| In-scope slice | `answered` | The slice is bounded to artifact model, terminology, and affected repo surfaces | No runtime code changes |
| Out-of-scope items | `answered` | Runtime code and broader workflow redesign are excluded | Keep this refactor structural |
| Success criteria / acceptance bar | `answered` | The output is a single aligned model across docs and templates | No partial mixed model allowed |
| Verification expectations | `answered` | This is a text/template refactor | Text consistency checks are sufficient |
| Ownership / source of truth | `answered` | The note plus this contract define the target model | README/install/templates must follow this contract |
| Integrations / dependencies | `n/a` | No external integration is involved | N/A |
| Edge cases / failure behavior | `answered` | `spec-less workstream` and workstream boundary are the main edge cases | The contract must define both clearly |
| Tradeoffs needing user input | `answered` | The user approved the model direction and requested a compact executable spec | No material decision gaps remain |

### User Escalation Gate

| # | Domain | Question | Why It Matters | Options Presented | Recommended Option | Why Recommended | User Answer / Waiver | Contract Impact |
|---|---|---|---|---|---|---|---|---|
| `UE-1` | continuity unit | What is the main continuity unit: project, spec, or workstream? | This determines where living state belongs | project / spec / workstream | `workstream` | It supports both spec-linked and spec-less work without collapsing continuity into the whole repo | `workstream` | `state.md` belongs to a workstream |
| `UE-2` | boundary rule | Should rework and verifier-returned fixes open a new workstream by default? | This determines continuity boundaries | yes / no, keep same workstream while target is the same | `no, keep same workstream while target is the same` | It preserves truthful continuity and avoids session-log fragmentation | keep same workstream while acceptance target is the same | The contract must define a same-target boundary rule |
| `UE-3` | spec-less work | Can a workstream exist without a formal spec? | This determines whether the model can handle smaller bounded work | no / yes, with minimal contract | `yes, with minimal contract` | It keeps the model usable without making every task heavy | yes, with minimal contract | `state.md` must carry the minimal contract when no spec exists |
| `UE-4` | planned slices vs workstream ID | Should planned spec slices and the workstream ID share one numbering scheme? | This determines how planning maps to living continuity | shared numbering / separate numbering with explicit linkage | `separate numbering with explicit linkage` | Planned slices and living continuity records serve different jobs | separate numbering with explicit linkage | `S1..N` and `ws-*` must stay separate |
| `UE-5` | terminology | Should execution sections in specs keep `phase` language? | This affects repo-wide wording consistency | keep `phase` / use `slice` for planned sections and `stage` for lifecycle position | `use slice for planned sections and stage for lifecycle position` | It removes one major source of ambiguity | use `slice` and `stage` distinctly | The contract must define both terms separately |
| `UE-6` | ownership | Should visible project artifacts be treated like refreshable install-owned scaffolding? | This determines upgrade/install safety | yes / no | `no` | User-owned project artifacts should not be treated like replaceable system files | no | `.devs/` is refreshable system layer; visible `devs/` artifacts are project-owned |

### Explicit Unknowns / Deferred Decisions

| # | Unknown / Deferred Item | Why Safe to Defer | Owner | Revisit Trigger |
|---|---|---|---|---|
| `UD-1` | `devs/workstreams/INDEX.md` remains optional in v1 | It is not needed to define the core model | `runtime-implementer` | Only if implementation discovers a real navigation need |

## User Decisions Log

### Lead Decisions

| # | Decision | Rationale | Impact |
|---|---|---|---|
| `LD-1` | Keep hidden Devs system files separate from visible project artifacts | System-owned files should not be mixed with active work records | Use `.devs/` for hidden system files |
| `LD-2` | Keep visible Devs artifacts under one visible `devs/` folder | This keeps project-facing artifacts grouped and readable | Store specs and workstreams under `devs/` |
| `LD-3` | Use one living `state.md` per workstream | Continuity should stay operational and bounded | Reject project-wide state and default per-session state files |
| `LD-4` | Keep same-target fix loops inside one workstream | Rework should not create fake new continuity units | A new workstream is opened only when target outcome or scope changes materially |
| `LD-5` | Allow `spec-less workstream`, but require a minimal contract | Smaller work should remain supported without becoming vague | `state.md` must carry the minimal contract when no formal spec exists |
| `LD-6` | Keep planned `S1..N` separate from the workstream `ws-*` ID | Planning slices and living workstream records are different artifacts | Link them in metadata, not shared numbering |
| `LD-7` | Use `stage` for lifecycle position inside a workstream | `phase` wording collides with the new workstream model | Templates and docs should use `clarify/specify`, `implement`, `verify` as stages |
| `LD-8` | Treat visible project artifacts as project-owned, not refresh-owned | Install/refresh logic should not silently replace living project artifacts | `.devs/` may be refreshable; visible `devs/` artifacts are not installer scaffolding |

## Existing Reality

1. Current owner(s): `draft design discussion on local branch`
2. Current source(s) of truth: `docs/notes/workstream_artifact_model.md` plus this contract
3. Current write / reconciliation seam(s): `README, install docs, init guidance, templates`
4. Known coupling or prior failures: `older multi-file handoff patterns became noisy; older repo-facing docs still reflect pre-refactor wording`

## In Scope

1. Finalize the artifact model for `.devs/`, `devs/repo.md`, and
   `devs/workstreams/`
2. Finalize `workstream` as the main continuity and delivery unit
3. Finalize the same-target boundary rule for fix loops inside one workstream
4. Finalize the rule that one workstream gets one living `state.md`
5. Finalize the rule that `spec-less workstream` is allowed but must carry a
   minimal contract in `state.md`
6. Finalize the distinction between planned `Slice S1..N` and the
   workstream ID such as `ws-001`
7. Finalize `stage` as the lifecycle position inside one workstream
8. Update `README.md`
9. Update `install/INSTALL.md`
10. Update `install/INSTALL_PROMPT.md`
11. Update `install/init_contract.md`
12. Update `skills/init_repo/SKILL.md`
13. Update `workstream_templates/spec_template.md`
14. Update `workstream_templates/state_template.md`

## Out of Scope

1. Runtime code changes
2. Session-log or archive history design beyond the one-current-state model
3. New workflow features outside the artifact and terminology refactor
4. Mandatory escalation rules from `spec-less` work into formal spec

## User-Visible Behavior Contract

1. Devs should present one clear visible location for project artifacts under
   `devs/`.
2. Devs should keep hidden system-owned files under `.devs/`.
3. `workstream` should be described as the main continuity and delivery unit.
4. A workstream should include spec fixes, implementation fixes, and
   verifier-returned fixes as long as the acceptance target is still the same.
5. A new workstream should be opened only when the target outcome or scope
   changes materially.
6. A formal spec should be optional.
7. A `spec-less workstream` should still require a minimal contract in
   `state.md`: objective, in-scope now, out-of-scope now, acceptance target,
   and source request or source link.
8. Specs should describe planned execution slices as `Slice S1`, `S2`,
   `S3`, and so on inside the workstream.
9. Planned `S1..N` slices and the workstream ID such as `ws-*` should be kept
   distinct and linked explicitly rather than merged into one numbering
   scheme.
10. `stage` should describe the lifecycle position inside one workstream, for
    example `clarify/specify`, `implement`, `verify`.
11. A fresh Devs install or repo init flow should create and describe the new
    artifact model consistently.
12. Install and refresh logic should not treat visible project artifacts as
    replaceable system scaffolding.

## Success Criteria / Acceptance Criteria

1. The repository has one approved target model for hidden system files,
   visible specs, and visible workstream state.
2. The model clearly states that `workstream` is the continuity unit.
3. The model clearly states that one workstream gets one living `state.md`.
4. The model clearly states the same-target boundary rule for internal fix
   loops.
5. The model clearly supports `spec-less workstream`.
6. The model clearly states the minimal contract required for a `spec-less
   workstream`.
7. The model clearly states that one spec may define several planned slices.
8. The model clearly separates planned `S1..N` from the workstream `ws-*` ID.
9. The model clearly separates `stage` terminology from planned slice
   terminology.
10. The model clearly states that `.devs/` is the hidden system layer and
    `devs/` is the visible project artifact layer.
11. The implementation slice is concrete enough to update the named files
    without reopening design questions.
12. README, install docs, init guidance, and templates can all be aligned to
    the same model from this contract alone.

## Non-Negotiable Rules

1. Do not use one project-wide `state` file as the default Devs continuity
   model.
2. Do not create one new state file per session as the default Devs continuity
   model.
3. Do not open a new workstream just because the verifier returned fixes or the
   same acceptance target needs another pass.
4. Treat `workstream` as the main continuity and delivery unit.
5. Allow a workstream to exist without a formal spec.
6. Do not allow `spec-less` to mean `contract-less`.
7. Use `slice` language in specs for planned execution slices.
8. Use `stage` for lifecycle position inside one workstream.
9. Do not collapse planned `S1..N` and the workstream `ws-*` ID into one numbering model.
10. Keep hidden Devs system files separate from visible project artifacts.
11. Treat `.devs/` as system-owned and potentially refreshable.
12. Do not treat visible `devs/` artifacts as refresh-owned scaffolding.
13. Keep README, install outputs, local repo docs, and templates aligned to
    one artifact model.

## Owner / Source-of-Truth Map

| Concern | Canonical Owner | Write / Reconcile Seam | Derived Surfaces | Notes |
|---|---|---|---|---|
| hidden Devs system files | `.devs/` | install / refresh logic | internal Devs support files | System-owned and refreshable |
| larger contracts | `devs/workstreams/<ws-id>/spec.md` | spec authoring and repo-facing docs | later slice planning | One spec may define several planned slices inside the same workstream |
| continuity between sessions | `devs/workstreams/` | workstream state updates and templates | next-session startup context | One living `state.md` per workstream |

## Semantic Hazards and Tempting Wrong Fixes

1. Treating the spec as the only valid continuity unit
2. Treating verifier-returned fixes as an automatic reason to open a new
   workstream
3. Treating `spec-less workstream` as permission to skip a contract
4. Treating `S1..N` and `ws-*` as one numbering system
5. Replacing `phase` with `slice` everywhere while forgetting that
   lifecycle stages still need a distinct term
6. Treating visible project artifacts as if install/refresh logic can recreate
   them freely

## Rejected Implementation Patterns

1. `one project-wide state file` - it grows too large and mixes independent
   work
2. `one new state file per session by default` - it creates noisy continuity
   and pushes the system back toward a session log
3. `forcing all workstreams to belong to a spec` - it breaks valid spec-less
   work
4. `spec-less means no explicit objective or acceptance target` - it recreates
   vague chat-only work
5. `shared numbering for planned slices and the workstream ID` - it hides the
   difference between planning and living continuity
6. `updating repo docs but leaving install/init/templates on the old model` -
   it leaves the repo internally inconsistent
7. `treating visible artifacts as installer-owned refresh output` - it makes
   living project records unsafe

## Verification Plan

### Automated Checks

1. `rg -n "\\bPhase\\b|state/handoff|project-wide state" README.md install skills workstream_templates docs/notes`
2. `rg -n "workstream|state\\.md|devs/specs|devs/workstreams|\\.devs/" README.md install skills workstream_templates docs/notes`

### Manual / Runtime Checks

1. Re-read the updated files and confirm they all express the same artifact
   model
2. Confirm the same-target boundary rule is stated consistently
3. Confirm `spec-less workstream` is allowed everywhere but never contract-less
4. Confirm `S1..N`, `ws-*`, and `stage` are separated cleanly
5. Confirm visible project artifacts are never described as refresh-owned

### Evidence Artifacts

1. Contract artifact:
   `docs/notes/devs_artifact_structure_refactor_spec.md`
2. Design note artifact:
   `docs/notes/workstream_artifact_model.md`
3. Changed repo-facing artifacts:
   `README.md`, `install/INSTALL.md`, `install/INSTALL_PROMPT.md`,
   `install/init_contract.md`, `skills/init_repo/SKILL.md`,
   `workstream_templates/spec_template.md`,
   `workstream_templates/state_template.md`

## Requirement Traceability

| Req-ID | Requirement | Acceptance Evidence |
|---|---|---|
| `REQ-01` | Hidden system files live separately from visible project artifacts | Sections `Before / After Summary`, `User-Visible Behavior Contract`, `Owner / Source-of-Truth Map` |
| `REQ-02` | `workstream` is the main continuity and delivery unit | Sections `User Escalation Gate`, `User-Visible Behavior Contract`, `Non-Negotiable Rules` |
| `REQ-03` | One workstream gets one living `state.md` | Sections `Lead Decisions`, `Success Criteria`, `Non-Negotiable Rules` |
| `REQ-04` | Same-target fix loops stay inside one workstream | Sections `User Escalation Gate`, `User-Visible Behavior Contract`, `Success Criteria` |
| `REQ-05` | A workstream may exist without a formal spec | Sections `User Escalation Gate`, `User-Visible Behavior Contract`, `Non-Negotiable Rules` |
| `REQ-06` | A `spec-less workstream` still requires a minimal contract in `state.md` | Sections `User Escalation Gate`, `User-Visible Behavior Contract`, `Success Criteria` |
| `REQ-07` | One spec may define several planned slices | Sections `Before / After Summary`, `User-Visible Behavior Contract`, `Owner / Source-of-Truth Map` |
| `REQ-08` | Specs use `Slice S1..N` for planned slices inside the workstream | Sections `Before / After Summary`, `User-Visible Behavior Contract`, `Non-Negotiable Rules` |
| `REQ-09` | Planned `S1..N` and the workstream `ws-*` ID remain distinct | Sections `User Escalation Gate`, `User-Visible Behavior Contract`, `Non-Negotiable Rules` |
| `REQ-10` | `stage` is the lifecycle position inside one workstream | Sections `User Escalation Gate`, `User-Visible Behavior Contract`, `Non-Negotiable Rules` |
| `REQ-11` | Visible project artifacts are not treated as refresh-owned scaffolding | Sections `User Escalation Gate`, `User-Visible Behavior Contract`, `Non-Negotiable Rules`, `Owner / Source-of-Truth Map` |
| `REQ-12` | README, install docs, init guidance, and templates all align to the same model | Sections `In Scope`, `Success Criteria`, `Next Bounded Implementation Slice` |

## Next Bounded Implementation Slice

Update the named repo-facing files so they all describe and scaffold the same
model:

1. `README.md` - explain `workstream` as the main continuity and delivery unit
2. `install/INSTALL.md` - describe the target artifact model for installation
3. `install/INSTALL_PROMPT.md` - align install prompt wording to the same
   model
4. `install/init_contract.md` - align repo bootstrap contract to the same
   model
5. `skills/init_repo/SKILL.md` - align repo-init guidance to the same model
6. `workstream_templates/spec_template.md` - represent planned slices as
   `S1..N`
7. `workstream_templates/state_template.md` - represent one living workstream
   state, including the minimal contract needed for `spec-less` work

## Clarifying Questions for Implementer

None — requirements are fully specified. Keep `devs/workstreams/INDEX.md`
optional unless implementation discovers a concrete need for it.

## Verifier Focal Points

1. Check that the contract does not accidentally force all work through specs
2. Check that the contract does not collapse continuity back into a project-wide
   or per-session state model
3. Check that same-target fix loops stay inside one workstream everywhere
4. Check that `spec-less workstream` is supported everywhere but never
   contract-less
5. Check that `S1..N`, `ws-*`, and `stage` are used consistently and distinctly
6. Check that install/init/template changes do not describe visible project
   artifacts as refresh-owned scaffolding

## Next Role / Next Action

- Next role: `runtime-implementer`
- Next action: `Update the named repo-facing docs and templates so they all match this workstream-based artifact model without reopening design questions.`
