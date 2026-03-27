# Devs

> Draft: `Devs` is an early open-source draft of an agentic development
> workflow. This repository currently contains the core process design, skills,
> and orchestration primitives. Installation and repository bootstrap guidance
> are still being developed.

## What Devs Is

`Devs` gives AI-assisted development a simple workflow:

`clarify -> specify -> implement -> verify`

It is a repo-native workstream protocol for structured software delivery.

## Why It Exists

AI-assisted coding often starts with one vague request in one long chat.

That usually leads to:

1. missing requirements
2. hidden assumptions
3. scope drift
4. messy context
5. weak verification

`Devs` exists to turn work with agents into a more standardized engineering
process.

Instead of relying on improvisation and fragile chat context, `Devs` starts by
clarifying the work, turning it into an explicit contract, and carrying that
contract through implementation and independent verification. It also preserves
enough state that the next session can continue the work cleanly instead of
starting over.

## How It Works

`Devs` treats each piece of work as a `workstream`.

A workstream moves through a simple loop:

1. start one workstream
2. clarify the request before coding
3. produce a usable specification
4. implement in a fresh session
5. verify in a fresh session
6. continue the work from saved state in the next session

## What You Get

`Devs` is designed to make AI-assisted development easier to trust.

It gives you:

1. a clearer path from a vague request to an explicit specification
2. bounded implementation instead of improvising everything in one long chat
3. independent verification instead of self-approved completion
4. persistent state across sessions, so work does not depend on chat history
   alone
5. a workflow that can keep moving forward without starting over every time

## Current Status

`Devs` is still an early draft.

The core workflow is here. Installation, bootstrap, and broader adoption
guidance are still being developed.
