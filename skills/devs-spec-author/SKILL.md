---
name: devs-spec-author
description: Use when writing a new Devs specification, or reopening one in a way that changes the workstream contract, and the contract must be clarified with the user before drafting.
---

# Devs Spec Author

## Overview

Take a new or reopened specification request and turn it into a clear Devs
contract before any drafting begins.
When this role is active for a new or reopened specification, the run must end
with a formal `devs/specs/<spec-id>/spec.md`.

Core principle: every specification begins with direct user questions and real
user feedback. Zero-question path is invalid for a new specification.

Use the available context to ask better questions, not to skip clarification.
If the request, the allowed context, the existing code, or external
constraints expose a contract decision, risk, limitation, or scope boundary
that the user has not confirmed yet, bring it to the user as a question
instead of silently absorbing it into the specification.

## When to Use

- A new specification is being created for a workstream, feature, or product.
- An existing specification is being reopened in a way that changes the
  contract.
- The contract must be confirmed with the user in the context of the whole
  workstream, not just the immediate task.
- Important decisions about scope, boundaries, expectations, constraints, or
  success criteria are still not confirmed with the user.
- Starting to draft now would force the model to fill gaps on its own.

## Do not use when:

- The user wants only a text-level update to an already accepted
  specification, and no contract decision is changing.

## Core Pattern

Before drafting:

1. Read only the allowed context: the user request and user-provided context;
   `AGENTS.md`, `devs/repo.md`, the active `state.md`, the linked `spec.md`,
   and only the local guidance explicitly linked from that chain. If platform,
   API, or library constraints affect what can be specified, read the
   corresponding official documentation too.
2. If the request changes an existing system, read the relevant existing code
   before you write questions or define the contract.
3. Build the full technical clarification trail before you word the
   questions. For a new or reopened specification, persist the `Contract
   Surface Grid` in `devs/workstreams/<ws-id>/clarification.md` using the repo
   template. Classify all 30 canonical slots from `./question-patterns.md`
   and expand the grid until it reaches exactly 100 rows before drafting.
   Render the grid there as the required markdown table from
   `./question-patterns.md`, not as bullets or prose.
4. Treat each touched owner, integration seam, lifecycle trigger, data
   boundary, and stateful interaction contract as a separate candidate
   position. Do not collapse independently variable positions into one broad
   question.
5. Turn the gathered context into explicit user questions about the
   specification and the workstream contract, including every contract
   decision, risk, limitation, and scope boundary surfaced by that context,
   even if the user has not named them yet.
6. Synthesize a user-facing clarification interview only from grid rows that
   still require user confirmation. You may combine multiple rows into one
   question block only if each underlying row remains separately visible and
   closable in the grid after the answer.
7. Ask the synthesized clarification questions in normal chat and get the
   user’s answers before drafting.
8. Restate the confirmed contract in chat, then draft the formal spec from it.

## Quick Reference

- Use `./question-patterns.md` before you ask questions.
- Questions are mandatory for a new specification. Zero-question path is invalid.
- Ask in normal chat. Do not hide questions or their rationale in reasoning.
- Ask about the whole workstream contract, not only the immediate task.
- Use context to sharpen questions, not to replace user feedback.
- Raise every contract decision, risk, limitation, and scope boundary surfaced
  by the request, the allowed context, the code you read for this task, or the
  official documentation you read for this task.
- During clarification, bias toward surfacing more user-answerable contract
  questions, not fewer; under-questioning is riskier than over-questioning.
- For a new or reopened specification, 100-row extraction mode is mandatory
  before drafting.
- This role is for formal spec authoring. It does not complete as a state-only
  or `spec-less` output.
- Do not ask the user to choose between formal spec and `spec-less` output
  while this role is active.
- Persist the full technical clarification trail in
  `devs/workstreams/<ws-id>/clarification.md`.
- Keep the full `Contract Surface Grid` and `Drafting Gate` out of chat unless
  the user explicitly asks to see them.
- In chat, show only concise status, the current user-facing batch, and the
  final contract restatement.
- Distinguish an active user-facing flow from a latent route or type seam in
  code. Do not describe a latent seam as an active flow unless the code proves
  it.
- One grid row closes one material position. If one question would still leave
  multiple independently variable positions open, split the grid row first.
- The user interview is not the raw grid. Extract broadly, then synthesize a
  smaller clarification set from rows that still need user confirmation.
- Keep questions user-answerable. Translate code-level or architecture-level
  findings into decisions the user can actually confirm.
- Restate the confirmed contract in chat before drafting.
- Use the repo's default templates from `.devs/templates/` unless stricter
  linked local templates are in force.
- Use `./contract-handoff.md` for clarification logging, contract handoff, and
  next-owner routing.

## Additional References

- `./question-patterns.md`
  Use it when turning gathered context into user-facing questions.
- `./contract-handoff.md`
  Use it when turning confirmed answers into a durable contract, handoff, and
  next-owner state.
- `.devs/templates/spec_template.md`
  Default spec template when no stricter linked local template is in force.
- `.devs/templates/state_template.md`
  Default state template when no stricter linked local template is in force.
- `.devs/templates/clarification_template.md`
  Default clarification template for the full technical clarification trail.

## Common Mistakes

- Optimizing for fewer questions
- Treating context as permission to guess instead of asking the user.
- Treating strong context as permission to skip questions.
- Asking fewer questions because the situation feels clear enough.
- Asking questions only about the immediate task and missing the wider
  workstream contract.
- Asking vague questions that do not lead to a real contract decision.
- Asking code-level or architecture-level questions when the real issue is
  scope, behavior, constraints, or success criteria.
- Asking for answers the user cannot reasonably give without reading code or
  internal architecture.
- Hiding questions or their rationale inside reasoning instead of normal chat.
- Turning confirmed answers into an incomplete contract before drafting.
- Ending a new or reopened spec-author run without a formal
  `devs/specs/<spec-id>/spec.md`.
- Starting spec prose before the confirmed contract has been restated in chat.
