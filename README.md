# Devs

A simple workflow for AI-assisted development that does not rely on one long chat, vague scope, or self-approved code.

**Status:** early draft. The core process is here. The installation story is not.

If you've used coding agents for real work, you know the pattern.
You ask for a feature.
The model writes something plausible.
Important decisions stay in chat.
The same session that wrote the code says it's done.
Later you find the missing requirements, scope drift, and fake completion.

Devs is an attempt to stop that.

It forces the work through a short loop:

`clarify -> specify -> implement -> verify`

The point is not ceremony.
The point is to stop guessing.

## The actual problem

Most agent workflows fail in the same boring ways:

- the request is vague
- the contract never gets written down
- context turns to soup inside one giant session
- the model quietly expands scope
- `looks done` gets confused with `was checked`

Devs adds structure where AI work usually turns sloppy.

## What Devs is

Devs is not an IDE.
It is not a project management suite.
It is not an autonomous team in a box.

It is a way to run AI-assisted work inside a repo so that:

- the task gets clarified before code starts
- the agreement lives in files, not only in chat
- implementation stays bounded
- verification is independent
- the next session can continue without starting from zero

Each piece of work becomes a workstream.
That workstream gets a spec, a state/handoff file, a current owner, and a next action.

## This is not vibe coding

Vibe coding is good at getting you to `something exists`.

It is much worse at keeping scope honest, preserving decisions, and proving that a change actually works.

Devs is for the moment when speed is no longer the main problem and trust is.

## The loop

### Clarify
Ask the missing questions first.
Turn a vague request into a real target.

### Specify
Write the contract.
What is in scope.
What is out of scope.
How we will know it is done.

### Implement
Build only the approved slice.
Use tests first.
Leave evidence behind.
Do not self-approve.

### Verify
Check the result in a fresh context.
Re-run the relevant checks.
Return a real verdict: `PASS` or `BLOCKED`.

## Why split the roles?

Because the same context that wrote the code is usually too forgiving when it reviews it.

So Devs separates the jobs:

- a spec author defines the contract
- an implementor builds the slice
- a verifier checks the claim

The handoff carries the baton between them.
It keeps the current state, evidence, findings, next owner, and next action in the repo instead of burying them in chat history.

## What is in this repo now

This repository is still a draft, but the shape is already visible.

You will find:

- the core `clarify -> specify -> implement -> verify` workflow
- role-separated skills for spec work, implementation, and verification
- an orchestration/controller prototype
- repo artifacts for specs and workstream state
- the longer thesis behind the project

You will not find a fully finished product yet.
Some important parts are still open:

- bootstrap and installation
- brownfield onboarding
- stronger technical enforcement
- final public UX

## Who this is for

Use Devs if AI helps you start fast but keeps making the finish messy.

Skip it if you are happy doing everything in one long chat and do not care much about specs, handoffs, or independent verification.

## Read next

Start with:

- `README.md`
- `docs/notes/process_programming_thesis.md`

Then read the orchestration docs and role prompts if you want the operational details.
