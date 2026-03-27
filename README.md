# Devs Project Design

> Draft: `Devs` is an early open-source draft of an agentic development
> workflow. This repository currently contains the core process design, skills,
> and orchestration primitives. Installation and repository bootstrap guidance
> are still being developed.

## What Devs Is

`Devs` gives AI-assisted development a simple workflow:

`clarify -> specify -> implement -> verify`

It is a repo-native workstream protocol for structured software delivery.

## Why It Exists

AI coding often starts with one vague request in one long chat.

That usually leads to:

1. missing requirements
2. hidden assumptions
3. scope drift
4. messy context
5. weak verification

`Devs` is a draft attempt to make that workflow more disciplined.

Instead of starting with direct implementation, `Devs` starts by clarifying
the work, turning it into a contract, and carrying that contract through
implementation and independent verification.

## How It Works

`Devs` treats each piece of work as a `workstream`.

A workstream moves through a simple loop:

1. start one workstream
2. clarify the request before coding
3. produce a usable specification
4. implement in a fresh session
5. verify in a fresh session
6. continue the work from saved state in the next session

## What Devs Stores Under The Hood

`Devs` relies on persistent artifacts so work can continue across chats without
depending on chat history alone.

These draft artifact types include:

1. project foundation documents
2. technical specifications
3. session memory and hand-off records
4. verification evidence

Users should not need to manage these artifacts manually every time.

## Draft Principles

The current draft principles are:

1. one workstream at a time
2. one delivery phase per session
3. no implementation before clarification and specification
4. implementation does not self-approve final completion
5. verification is independent
6. each phase leaves a persistent hand-off artifact
7. each completed phase should produce the next-session prompt

## Draft Status

This repository is still a design draft.

The current direction is clear, but several parts are still open:

1. bootstrap flow for new projects
2. brownfield onboarding for existing repositories
3. exact workstream file layout
4. clarification interview format
5. strength of same-session blocking between phases
