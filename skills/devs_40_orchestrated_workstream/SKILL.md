---
name: devs_40_orchestrated_workstream
description: Use when running one workstream through a controller-managed clarify-specify-implement-verify loop with fresh subagents, persistent artifacts, and minimal user orchestration overhead.
---

# Devs Orchestrated Workstream

## Overview

Use this skill when one user session should act as the controller for one
bounded workstream.

This is an additive prototype mode. It does not replace the existing manual
`spec-author`, `runtime-implementor`, or `runtime-verifier` skills.

## Read First

Before starting the workstream, read:

1. The local bootstrap file for the active repository, typically `AGENTS.md`
2. `orchestration/orchestrated_v1/protocol.md`
3. `orchestration/orchestrated_v1/controller.md`
4. `orchestration/orchestrated_v1/templates/spec.md`
5. `orchestration/orchestrated_v1/templates/workstream.md`

Read the role prompt files only when you are about to launch that phase:

1. `orchestration/orchestrated_v1/roles/clarifier.md`
2. `orchestration/orchestrated_v1/roles/implementor.md`
3. `orchestration/orchestrated_v1/roles/verifier.md`

## What This Skill Owns

The controller owns:

1. Creating `workstreams/<slug>/spec.md`
2. Creating `workstreams/<slug>/workstream.md`
3. Keeping the workstream state current between phases
4. Launching fresh subagents for clarification, implementation, and
   verification
5. Asking the user only at genuine decision gates
6. Stopping when the workstream passes, needs user escalation, or hits an
   external blocker

## Core Rules

1. One active workstream per controller run.
2. Keep the user-facing flow simple.
3. Use a fresh subagent for each clarification, implementation, and
   verification phase.
4. Give each subagent only the current task brief, the relevant artifact
   paths, and the matching role prompt.
5. The controller updates `workstream.md`. Subagents do not own the state
   file.
6. Do not move into implementation before the spec is explicit enough and the
   user has approved it.
7. Do not let the verifier quietly edit the implementation.
8. If verification finds a spec problem, stop the runtime loop and return to
   clarification or user approval.

## Minimal Workflow

1. Turn the user request into a workstream slug.
2. Create `workstreams/<slug>/` and initialize `spec.md` plus `workstream.md`
   from the templates if they do not exist.
3. Run clarification and specification.
4. Present the spec summary and ask for approval.
5. Launch a fresh implementor subagent for the approved slice.
6. Update the workstream artifact from the implementation result.
7. Launch a fresh verifier subagent.
8. If blocked, route to the next bounded fix or spec repair step.
9. If passed, close the workstream with a final summary and the saved state.

## User Interaction Points

The user should normally interact only to:

1. Answer clarification questions
2. Approve or reject the drafted spec
3. Perform manual checks when verification requires them
4. Approve the final result or pause the workstream

## Required Output

At every controller checkpoint, report:

1. Current phase
2. Workstream slug
3. Artifact paths
4. What changed in the saved state
5. The next automated step or the exact user decision needed

