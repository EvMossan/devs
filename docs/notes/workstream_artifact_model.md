# Devs Workstream Artifact Model

## Status

Draft
Date: 2026-03-29

## Purpose

This note captures the current draft model for how Devs stores project
artifacts.

It is a working design note, not yet a final public contract.

## Core Idea

The primary execution unit in Devs is a `workstream`.

A workstream is one bounded line of work that runs from request to completion,
including any internal loops such as:

1. clarify updates
2. spec fixes
3. implementation fixes
4. repeat verification

The loops do not create a new workstream. They happen inside the same
workstream until that work reaches a truthful end state.

A new workstream should be opened only when the target outcome changes in a
material way.

Rework, spec correction, and verifier-returned fixes stay inside the same
workstream as long as the acceptance target is still the same.

## Artifact Model

Devs uses three layers:

1. hidden system files
2. visible specification artifacts
3. visible workstream state artifacts

### Hidden System Layer

Hidden Devs files live under `.devs/`.

This folder is for Devs-owned, install-owned, or refreshable system files such
as:

1. install metadata
2. project profile metadata
3. future Devs support templates
4. future Devs support config or bootstrap files

This folder is not for active engineering work records.

### Visible Project Artifact Layer

Visible Devs project artifacts live under `devs/`.

Current draft structure:

```text
devs/
├── README.md
├── specs/
│   └── <spec-id>/
│       └── spec.md
└── workstreams/
    ├── INDEX.md
    └── <workstream-id-slug>/
        └── state.md
```

## Specs

`specs/` stores larger contracts.

One spec may define multiple planned slices.

A spec changes relatively rarely compared with a workstream state file.

Not every workstream needs a formal spec.

The spec should use `slice` language instead of `phase` language.

Current draft direction:

1. specs should describe planned execution slices as `Slice S1`, `Slice S2`,
   and so on
2. this internal spec numbering is separate from workstream IDs such as
   `ws-001`
3. a slice is a planned unit inside the workstream, not a separate workstream

## Workstreams

`workstreams/` stores the active continuity layer between sessions.

Each workstream gets one living `state.md`.

That file is the current memory for that workstream:

1. current scope
2. current truth
3. evidence status
4. next owner
5. next action

Current draft rule:

1. one workstream gets one current `state.md`
2. not one state file for the whole project
3. not one new state file per session by default

## Relationship Between Spec and Workstream

The workstream is the continuity unit.

The spec is optional.

When present, the spec is the formal contract for that workstream.

That means:

1. one workstream can exist without a formal spec
2. every state file must belong to a workstream
3. not every workstream must belong to a spec
4. one formal spec may belong to one workstream
5. a workstream may link to one current spec slice or to none
6. one formal spec may plan several slices inside the same workstream

## Spec-less Workstreams

If a workstream does not have a formal spec, it still needs a minimal contract
inside `state.md`.

That minimum should capture:

1. objective
2. in-scope now
3. out-of-scope now
4. success signal or acceptance target
5. source request or source link

If that minimal contract stops being enough, the workstream should be promoted
to a formal spec.

## Update Rule for `state.md`

`state.md` should be updated when the workstream truth changes in a meaningful
way, for example:

1. a workstream is opened
2. scope or contract is clarified
3. an implementation slice completes
4. verification records a verdict
5. a blocker changes the next action
6. ownership changes

The file should stay short and operational. It is not intended to become a full
session log.

It should record current truth, not a session-by-session diary.

## Naming Direction

Current naming direction:

1. specs use a spec-oriented ID such as `001-day-freshness`
2. workstreams use a workstream-oriented ID such as
   `ws-001-home-chat-refresh`
3. specs should label planned execution slices as `S1`, `S2`, `S3`
4. a slice is a planned unit inside the workstream, not a separate
   continuity unit
5. linkage between spec slices and the current workstream state should be
   recorded in metadata, not forced into one shared numbering scheme
6. `stage` should describe the current lifecycle position inside one
   workstream, for example `clarify/specify`, `implement`, `verify`
7. `stage` and planned spec slices are different concepts and should not
   share one numbering model

## Current Draft Summary

The current draft model is:

1. `.devs/` for hidden Devs system files
2. `devs/specs/` for larger contracts
3. `devs/workstreams/` for living continuity between sessions
4. one living `state.md` per workstream
5. workstream as the main execution and memory unit
6. spec-less work is allowed, but not contract-less work
7. planned `S1..N` slices in specs are not the same thing as workstream IDs
