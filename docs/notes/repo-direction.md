# Devs Product Direction Notes

## Status

Draft
Date: 2026-03-20

## Purpose

This document captures the current internal product direction discussed during
design exploration.

It is not the user-facing repository introduction.

## Current Product Shape

Current draft position:

1. `Devs` is not only a skill pack
2. `Devs` is not a full project management suite
3. `Devs` is a repo-native workstream protocol layer

The goal is to make AI software delivery more structured without requiring a
custom IDE or a heavy external control plane.

## Core Delivery Loop

The core delivery loop remains:

1. clarify and specify the work
2. implement the approved contract
3. verify the result independently

This loop is expected to run through explicit hand-offs between sessions rather
than through one long chat.

## Workstream Model

The primary user-facing unit is a `workstream`.

A workstream carries:

1. clarified intent
2. specification state
3. current phase
4. session memory and hand-off state
5. next owner
6. next action

This workstream framing is currently stronger than a skill-first or chat-first
model.

## Session Boundaries

One important draft principle is:

1. one delivery phase per session

The intent is not to "solve" limited LLM context completely.

The intent is to create a disciplined workflow inside context-limited systems
by:

1. bounding each phase
2. saving explicit state
3. making hand-offs visible
4. reducing hidden carry-over between phases

## Clarification Phase

Clarification is considered a major differentiator.

The system should not move directly from a vague request to implementation.

Instead, it should help the user turn vague intent into a spec-ready contract
through structured questioning.

Open design question:

1. how fixed or adaptive the clarification interview should be

## Hidden Artifacts

The system should create and update important artifacts under the hood.

These artifacts are necessary, not accidental.

They are part of how `Devs` preserves continuity and auditability across
sessions.

At the same time, users should not be forced to manually manage those artifacts
during normal use.

## Handoff Ritual

An important current idea is that each completed phase should:

1. save the relevant state
2. record the next owner
3. record the next action
4. produce the next-session prompt

This is currently one of the strongest candidate UX mechanisms for turning a
methodology into a repeatable technical workflow.

## Honest Product Promise

The current honest promise is closer to this:

`Devs helps keep AI-assisted work structured, bounded, and auditable across sessions.`

It should not promise to fully solve LLM context limits or memory problems.

## Open Questions

The biggest unresolved questions currently include:

1. what the first-run experience should be after installation
2. whether project bootstrap is a separate flow or the first workstream
3. how strongly the protocol should block same-session phase continuation
4. what the minimal required workstream artifacts should be
5. how much of the methodology can be enforced technically versus procedurally
