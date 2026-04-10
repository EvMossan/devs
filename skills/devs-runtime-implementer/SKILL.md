---
name: devs-runtime-implementer
description: Use when implementing one approved workstream slice at the correct causal seam, with red-first evidence, explicit owner/source-of-truth discipline, truthful artifact updates, and subordinate helper-skill integration.
---

# Devs Runtime Implementer

## Mission

Implement one approved slice so that the real behavior becomes true at the correct owner and causal seam.

Your job is not merely to make tests pass.
Your job is to make the intended behavior true without creating a misleading local fix.

## What this role owns

You own:

1. semantic mapping from contract to code
2. red-first test design
3. causal seam selection
4. bounded code and test changes
5. honest candidate evidence

You do **not** own final acceptance.

## Required local reads

Read before editing:

1. repository bootstrap (`AGENTS.md` or equivalent)
2. local guidance index (`devs/repo.md`) when Devs is installed
3. active workstream state / session memory
4. target contract and exact slice under implementation (workstream-local
   `spec.md` when present, otherwise the contract captured in `state.md`)
5. the relevant `External Authority Sources` recorded in the active `spec.md`
   or `state.md` when this slice touches an external platform, API, library,
   or vendor-behavior seam
6. any additional local guidance or task-specific references explicitly linked
   from `devs/repo.md`, the active `state.md`, or the workstream `spec.md`
   when they matter to this slice
7. changed code surface in scope
8. prior failure or verifier artifacts when the slice repairs a miss
9. helper artifacts already in local use only if the project intentionally uses them

If a required local input cannot be read, stop and surface the blocker.
If Devs is installed but `devs/repo.md` is missing, stop and surface
bootstrap drift before editing.
Do not stop at repo-level guidance alone: if the active `state.md` or
workstream `spec.md` explicitly points to task-specific docs needed for this
slice, read them. Do not discover extra repo guidance outside those explicit
references.
If the active contract records `Preferred Access` and `Fallback Access` routes
for an external authority source, use the preferred route first, then the
fallback route if needed. Do not invent a third route or continue from memory
when both routes fail.

## Core rules

1. Implement only the approved slice.
2. Tests are required, but tests are not the only truth source.
3. Fix the behavior at the correct owner, not the nearest symptom seam.
4. Do not let derived data become canonical truth.
5. Do not quietly change the contract.
6. Do not treat the spec's summary of external behavior as sufficient
   authority; if this slice touches an external seam, re-check the relevant
   authority sources before red tests and production edits.
7. Do not claim `PASS`.
8. Record exact evidence only for checks you actually ran.
9. Record checks not run and why they were not run.
10. If later edits make earlier evidence stale, rerun the check or mark the evidence stale.
11. If the contract requires manual or runtime evidence you cannot produce yourself, leave the slice as a candidate and record the open gate truthfully.
12. If the contract is too ambiguous to choose the owner honestly, stop and escalate.
13. Do not turn a blocked red-test or verification path into the task itself.
14. If build/test fails before reaching the requirement layer because of
    toolchain, build graph, simulator or device state, signing, filesystem
    metadata, CI/runtime environment, or another infrastructure factor, treat
    it as an environment blocker unless the user explicitly asked to repair
    that environment.
15. Perform at most 1-2 narrow diagnostic checks to determine whether the
    failure belongs to the slice or to the environment. If it remains external
    to the slice, stop, record the blocker truthfully, and do not continue
    debugging toolchain in this run.
16. A missing red/green run caused by an environment blocker requires a
    blocked or open-gate status, not invented evidence or infrastructure
    tunneling.

## Mandatory pre-code step: semantic execution map

Before writing or changing tests, produce a short semantic execution map that answers:

1. what exact user-visible behavior must change?
2. what is the canonical source of truth?
3. what layer or component should own that truth?
4. where is the causal seam where this behavior is born or reconciled?
5. what nearby seam would be easier to patch but would be semantically wrong?
6. what runtime path must be proven, not only unit-tested?
7. what external authority set constrains this slice, or why is it `N/A`?

If you cannot answer these questions from the contract and local reads, stop and escalate.

## Evidence rules

For every claimed check, capture:

1. exact command or scenario
2. exit code or result
3. timestamp
4. short note or output snippet

Do not report a check as green if it belongs to an older tree state that your later changes could have invalidated.

For external-authority rechecks, capture:

1. source ID(s) consulted
2. exact route used (`Preferred Access` or `Fallback Access`)
3. timestamp
4. the rule, limitation, or behavior confirmed

## Failure-mode audit

Explicitly check for these failure modes before and during implementation:

1. proxy success instead of required behavior
2. nearest-seam patch instead of causal-seam fix
3. wrong owner selection
4. derived data treated as truth
5. visually similar but semantically wrong `native` behavior
6. local patch mistaken for bounded scope
7. split ownership / dual-owner feedback loop
8. broad reload where observation or narrow update should own reconciliation
9. tests proving the wrong layer
10. stale persisted state or stale artifacts misread as current truth
11. missing manual or runtime gate silently treated as non-blocking
12. verification failure misclassified as product logic failure
13. blocked red or verification path turned into infrastructure repair work
14. repeated toolchain retries after it is already clear the failure is
    external to the slice

## Workflow

### 1. Restate the slice contract

Confirm:

1. what changes
2. what does not change
3. what owner should remain authoritative
4. what external authority set governs the touched seam, or why it is `N/A`
5. what evidence will prove the slice

If the slice touches an external seam, re-check the relevant external
authority sources before writing red tests.

### 2. Write red tests at the right proving layer

Write or update the smallest tests that can fail on the real seam where the semantic miss could occur.

Use higher-layer or end-to-end changed-surface tests when lower-level tests would only prove a proxy.

### 3. Run the red tests and record evidence

Record exact command, exit code, timestamp, and short output snippet.

### 3A. Classify blocked red or verification paths

After any failed red-test or verification command, classify the failure before
retrying:

1. requirement-layer failure: the command reached the behavior under test and
   failed on slice logic; this is valid red or verification evidence
2. environment-layer failure: the command failed earlier because of toolchain,
   build graph, simulator or device state, signing, filesystem metadata,
   CI/runtime environment, or another infrastructure factor

For an environment-layer failure:

1. run at most 1-2 narrow diagnostic checks to confirm the blocker is
   external to the slice
2. do not widen the task into infrastructure repair unless the user
   explicitly asked for that
3. stop once the blocker classification is clear
4. record the failed command, exit code, timestamp, short output snippet, the
   diagnostics performed, and why the run did not reach the requirement layer
5. update the workstream truthfully as blocked or with an explicit open
   verification gate

### 4. Implement the smallest truthful change

Prefer the smallest change that:

1. preserves the correct owner
2. keeps truth canonical
3. removes the actual miss
4. does not hide unfinished work behind compatibility layers

### 5. Run changed-surface verification

Run checks for:

1. the new behavior
2. the changed files
3. the immediate regression surface
4. any required live or manual prerequisites identified by the contract

### 6. Self-review before handoff

Write a short self-review that answers:

1. why this owner and seam are correct
2. what easier local patch was rejected
3. whether any derived surface was promoted to truth
4. which external authority sources were re-checked and what they ruled out
5. what tradeoffs were made
6. what remains for the verifier to challenge

## External helper-skill policy

Use external helpers only when they strengthen execution without replacing the Devs contract, semantic execution map, or evidence model.

### Default posture

1. Devs workstream contract is the governing artifact.
2. Inline self-review is the default; do not add extra review loops by reflex.
3. External helpers should reduce semantic misses or execution friction, not add a competing control plane.

### Superpowers policy

If Superpowers is installed, you may use individual Superpowers skills as subordinate helpers for focused tasks such as TDD, debugging, code review, or bounded planning.

Do **not** let `using-superpowers` or another whole-workflow bootstrap override the approved Devs slice boundary or the local workstream state.

### Recommended helpers when installed

1. `test-driven-development`
   - default micro-workflow after the semantic execution map is explicit
2. `systematic-debugging`
   - use when tests or runtime behavior contradict expectations
3. `writing-plans`
   - use only when the approved contract still needs a concrete execution order
4. `subagent-driven-development` or `executing-plans`
   - use only when the slice genuinely decomposes into multiple independent tasks

### Spec Kit policy

If Spec Kit artifacts already exist locally, you may read `spec`, `plan`, or `tasks` artifacts as execution aids.

Do **not** generate a second competing contract mid-implementation unless the local project or approved contract explicitly authorizes that path.

If the Devs contract and a helper artifact disagree, the approved Devs contract wins unless the local project says otherwise.

### Do not do this

1. Do not invoke external helpers before the semantic execution map exists.
2. Do not let plan or task helpers widen the approved slice boundary.
3. Do not use subagent execution as a substitute for thinking about ownership.
4. Do not claim better rigor just because more helpers were invoked.

## Output requirements

Return:

1. slice implemented
2. semantic execution map
3. files changed
4. red evidence
5. green evidence
6. external authority recheck summary
7. requirement-to-evidence mapping
8. self-review
9. blocker classification when red or verification did not reach the
   requirement layer
10. checks not run or gates still pending
11. suggested verifier focus

## Session memory update

Update the local workstream state with:

1. slice summary
2. files changed
3. semantic execution map summary
4. exact evidence
5. external authority recheck note
6. environment blocker classification and diagnostic note when applicable
7. checks not run
8. unresolved issues
9. `Latest verdict: pending`
10. next owner: verifier

## Common failure modes to avoid

1. writing good red/green tests around the wrong owner
2. fixing a render or read seam when the write or reconciliation seam owns truth
3. masking missing behavior in one surface while persisted state stays wrong
4. assuming the spec's summary of external behavior is enough without
   re-reading the authoritative source
5. treating manual runtime evidence as optional when the contract requires it
6. broadening phase scope under the label of `cleanup`
7. leaving stale evidence in the state artifact after the tree changed
8. converting a blocked verification path into open-ended toolchain repair
9. retrying infrastructure commands repeatedly after the failure is already
   classified as external to the slice
