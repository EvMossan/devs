# Spec Author Question Patterns

## Purpose

Use this file after you have read the allowed context and before you start
asking questions.

Its job is to turn the gathered context into user-facing questions that get
real user feedback and confirm the workstream contract before drafting.
Use it to cover the contract from multiple angles and to raise every contract
decision, risk, limitation, and scope boundary exposed by the request, the
code, the active workstream context, or external constraints that the user has
not yet confirmed.

Use this file to ask better questions, not fewer questions.

## Core Rule

Turn context into questions, not assumptions.

Ask questions that confirm the contract directly, and ask about every
decision, risk, limitation, and scope boundary exposed by the gathered
context that the user has not yet confirmed. Do not silently absorb any of
them into the specification.

Questions are not only for collecting missing information. They are also for
surfacing implications the user may not have named yet, but that would shape
the contract once drafting begins.

Context sharpens the questions. It never replaces the clarification.

## Contract Surface Grid

Before asking, build a durable `Contract Surface Grid` in the workstream
clarification artifact.

For a new or reopened specification, 100-row extraction mode is mandatory:

- classify all 30 canonical slots below
- expand the grid until it contains exactly 100 rows total
- keep each row flat and atomic
- if one slot surfaces multiple independently variable positions, record them
  as separate rows that share the same canonical slot

Each row should record:

- row
- slot
- contract surface
- evidence

Row quality rules:

- `contract surface` must be a declarative surface or seam statement, not a
  user question
- keep each row atomic; if one row contains multiple independent decisions,
  alternatives, or seams, split it
- `evidence` must be an observable fact from the request, code, docs, or
  active workstream context
- do not put interpretation, motivation, recommendation, or predicted impact
  inside `evidence`

One row closes one material position.
If one question would close multiple independently variable positions, split the
row before asking.

Run a second pass over all six angles before you start asking questions.
Only after the grid is complete, synthesize a smaller user-facing interview
from the extracted rows that still require user confirmation.

## Grid Render Format

Render the `Contract Surface Grid` as a markdown table in this exact column
order:

| row | slot | contract_surface | evidence |

Use the canonical slot IDs exactly and render them in this order:

- `G1` `G2` `G3` `G4` `G5`
- `S1` `S2` `S3` `S4` `S5`
- `C1` `C2` `C3` `C4` `C5`
- `E1` `E2` `E3` `E4` `E5`
- `SC1` `SC2` `SC3` `SC4` `SC5`
- `O1` `O2` `O3` `O4` `O5`

Do not replace the table with bullets, prose, YAML, JSON, or any other format.
Do not omit canonical slots.
Use a flat row model. Do not create parent summary rows or child row IDs such
as `G4.1`.
Persist the full grid in `devs/workstreams/<ws-id>/clarification.md`.
Do not render the full table in chat unless the user explicitly asks to see
it.
In chat, show only concise status and the current user-facing batch.

## Next Interview Batch

Do not precompute a full ranked interview list.
After the raw grid is complete, expose only the next user-facing batch.

Persist one markdown table of up to 4 rows at a time in the workstream
clarification artifact in this format:

| qid | trigger_row | unsafe_spec_sentence | user_question |

- `qid`: use stable IDs such as `B1Q1`, `B1Q2`
- `trigger_row`: one raw-grid row that would force the spec to guess if you
  skipped user clarification now
- `unsafe_spec_sentence`: one concrete sentence the agent would otherwise write
  into the spec without user confirmation
- `user_question`: one user-answerable question that closes that sentence

`unsafe_spec_sentence` is not a meta-note such as "this is unclear".
It must be the actual unconfirmed spec sentence the model would otherwise
invent.

The checkpoint table is technical. Do not render it in chat unless the user
explicitly asks to see it.
In chat, show only the actual user-facing questions and concise status.

When a user-facing question has plausible alternatives, render it with 2-3
mutually exclusive answer options in a fixed `A/B/C` format. Do not collapse
that question into only a recommendation sentence or a partial option list.

- label options explicitly as `A`, `B`, and `C` when three are used; use `A`
  and `B` when only two are needed
- `A` must be the recommended option and must be marked `(recommended)`
- give each option one short contract consequence line
- keep free-form user answers allowed if none of the options fit
- choose the recommended option as the most evidence-supported and
  least-expanding contract choice that still satisfies the request
- do not force options when the question is better answered directly in prose
- do not present options for internal implementation or spec-author tradeoffs

Batch rules:

- include at most 4 questions in one batch
- a small batch is the default; one-question batches are not the default
- each batch question must stay independent inside that batch
- use a single-question batch only when an earlier answer would materially
  rewrite or eliminate a later question
- if a plausible answer to an earlier batch question would rewrite, delete, or
  narrow a later question, move that later question to the next batch
- multiple trigger rows in one batch are allowed when each row remains
  separately closable from the user's answer
- do not pre-plan later batches before the user answers the current batch
- a later batch is invalid if any of its questions could be rewritten,
  narrowed, or deleted by an earlier unanswered batch question
- `unsafe_spec_sentence` must be derived from its `trigger_row`; do not merge
  multiple unresolved rows into one sentence

After each user answer, rescan the raw grid and produce a new batch. Do not
prepare or publish the full question list in advance.
Close rows only row-by-row after the answer.
By default, a batch answer closes only its trigger rows; any non-trigger row
stays `blocked` unless the answer resolves it directly and you record an
explicit row-level basis.
Do not close neighboring rows by analogy, by shared intent, or by a high-level
recommended option selection.
After each batch, refresh the Drafting Gate before any stage-transition
decision.
If a row depends on consequences inferred from the answer rather than the
answer itself, carry it into the next batch instead of marking it covered.

## Drafting Gate

Before any drafting or drafting-oriented preparation, publish the Drafting Gate
table in the workstream clarification artifact.
Do not transition to drafting while any raw-grid row still implies an unsafe
spec sentence that is neither answered by the user nor explicitly safe to
defer.

Before drafting, publish one compact markdown table in this format:

| status | rows | basis |

- `status`: `answered`, `safe_to_defer`, or `blocked`
- `rows`: raw-grid row IDs
- `basis`: either the user answer that closed those rows, or the concrete
  reason they are safe to defer

Rules:

- if any row remains `blocked`, drafting is forbidden
- persist the full `Drafting Gate` in
  `devs/workstreams/<ws-id>/clarification.md`
- do not render the full gate table in chat unless the user explicitly asks to
  see it
- until the Drafting Gate shows no blocked rows, do not announce a transition
  to drafting, read drafting templates for execution, or start spec/state
  artifact work
- the Drafting Gate must cover every raw-grid row still relevant to the current
  workstream contract
- any relevant row omitted from the Drafting Gate counts as `blocked` by
  default
- do not mark a row `safe_to_defer` without a concrete defer reason
- do not use this table to restate the whole contract; it exists only to prove
  whether drafting is allowed

## Question Angles

Use these angles to widen the contract before drafting. Treat each angle as a mandatory question-generation bucket.

For each angle, generate every user-answerable contract question that the
request, code, active workstream context, or external constraints can surface.

Bias toward more questions, not fewer questions.

In 100-row extraction mode, fill all five canonical slots under each angle
before you move on. Then keep decomposing at the finest defensible granularity
until the full grid reaches exactly 100 rows. Expand slots when the current
context surfaces multiple independent positions inside one slot.

- **Goal**: What is this specification trying to achieve, and why does it
  matter now?
  - `G1` primary objective
  - `G2` primary user
  - `G3` why now
  - `G4` first scenario that must work
  - `G5` relation to the surrounding product or workstream
- **Scope**: What must be included now, and what must stay out of scope for
  this version?
  - `S1` mandatory in-scope outcome
  - `S2` explicit out-of-scope boundary
  - `S3` first-slice boundary
  - `S4` supported surfaces, platforms, or environments
  - `S5` adjacent surfaces intentionally touched or untouched
- **Constraints**: What technical, platform, policy, dependency, or delivery
  limits could shape the contract?
  - `C1` execution boundary
  - `C2` required stack, protocol, or dependency choice
  - `C3` budget, time, or resource limit
  - `C4` legal, compliance, policy, or security limit
  - `C5` hosting, deployment, or operational environment limit
- **Expectations**: What should this change do in practice for the product,
  system, or workflow?
  - `E1` primary interaction model
  - `E2` data or access model
  - `E3` lifecycle or admin model
  - `E4` observability or visibility expectation
  - `E5` UX or ergonomics expectation
- **Success Criteria**: What would make this specification clearly complete and
  ready for implementation?
  - `SC1` functional proof
  - `SC2` non-regression condition
  - `SC3` first milestone or bounded done line
  - `SC4` performance or reliability threshold
  - `SC5` deliverable and acceptance format
- **Ownership and Integration**: When the change touches existing systems or
  boundaries, what needs to be confirmed about where the change belongs and how
  it should fit into the current system? Treat structured integration seams as
  separately closable positions, not one umbrella topic.
  - `O1` repo or workstream fit
  - `O2` source-of-truth or owner seam
  - `O3` external integration seam
  - `O4` state, secret, or deployment ownership
  - `O5` post-delivery operational owner

Use every angle to expand the question set as far as the current context
supports. Ask every generated user-answerable contract question under that
angle. Do not skip an angle just because the user did not mention it first.

For a new or reopened specification, under-questioning is a failure.
In 100-row extraction mode, leaving a canonical slot unclassified is a
failure.
In 100-row extraction mode, producing fewer than 100 rows is a failure.

## Good Questions

Good questions help the user confirm the contract, not guess what the agent
means.

A good question should be:

- **Atomic**: one question should close one material position. If one answer
  could still leave multiple independently variable seams open, split it.
- **Grid-ready**: the question must map back to one or more specific
  `Contract Surface Grid` rows that remain separately visible and closable
  after the user answers.
- **Spec-blocking**: ask it only when skipping it would force the spec to add
  an unconfirmed contract sentence.
- **Boundary-specific**: do not replace a data boundary, behavior boundary,
  integration boundary, or ownership boundary with a generic "which blocks
  stay" question.
- **Direct**: ask about one decision clearly enough that the user can answer it
  without decoding hidden intent.
- **Grounded**: tie the question to the request, the existing code, the active
  workstream context, or an external constraint when that context is what makes
  the question necessary.
- **Workstream-aware**: ask in terms of the whole workstream, not only the
  immediate task in isolation.
- **Contract-shaping**: focus on scope, boundaries, constraints, expectations,
  ownership, integration, or success criteria.
- **User-answerable**: ask for a decision the user can actually make, not for
  code-level details or internal architecture choices.
- **User-owned**: if a question is really an internal implementation or
  spec-author tradeoff, do not escalate it to the user; own it explicitly or
  defer it explicitly.
- Only escalate architecture or ownership questions when they change
  user-visible behavior, scope, acceptance, or a user-meaningful tradeoff.
- If multiple internal implementations satisfy the same user contract, keep
  that choice as a spec-author decision.
- Do not ask the user to choose between internal owners, view models, or
  data-pipeline shapes unless one option changes product behavior they would
  perceive.

When context is what makes the question necessary, say so briefly before the
question. Do not hide the reason inside reasoning.

## Common Failures

Watch for these failures:

- Optimizing for fewer questions
- Stopping before all 30 canonical slots are classified in 100-row extraction
  mode.
- Stopping before the `Contract Surface Grid` reaches exactly 100 rows in
  100-row extraction mode.
- Rendering the `Contract Surface Grid` in prose or bullets instead of the
  required markdown table.
- Using the raw extraction grid to record closure, status, priority, or final
  interview wording instead of only contract surface.
- Writing `contract surface` rows as direct user questions instead of extracted
  seams.
- Putting inferred motives, recommendations, or UX theories into `evidence`
  instead of observable facts.
- Combining multiple unresolved rows into one `unsafe_spec_sentence`.
- Escalating implementation or internal tradeoff questions that the user cannot
  answer productively at the contract level.
- Skipping the visible `Contract Surface Grid` and jumping straight to broad
  questions.
- Asking one umbrella question that hides multiple independently variable
  material positions.
- Treating the raw extraction grid as if it were already the final user
  interview.
- Asking vague questions that do not clearly point to a contract decision.
- Asking code-level questions when the real contract question is about scope,
  behavior, or constraints.
- Asking only the first obvious question and missing the rest of the contract.
- Filtering out questions because the context feels "clear enough."
- Turning context into assumptions instead of turning it into questions.
- Hiding important questions or their rationale inside reasoning instead of
  normal chat.
- Asking for answers the user cannot reasonably give without reading code or
  internal architecture.
- Smuggling a decision into the wording of the question instead of asking it
  openly.
- Treating questions as a ritual instead of using them to get real user
  feedback and a confirmed contract.
