# External Authority RED/GREEN Evidence

## Scope

Freeze the behavioral contract for external authority handling across
`spec-author`, `runtime-implementer`, `runtime-verifier`, and the workstream
templates.

## RED Baseline

1. `workstream_templates/spec_template.md` had no mandatory section that named
   the external authority set, access route, or fallback route for an external
   seam.
2. `workstream_templates/state_template.md` had no minimal-contract slot for a
   spec-less workstream to record required external authority sources.
3. `skills/devs-runtime-implementer/SKILL.md` required local reads only and did
   not require a pre-code recheck of authoritative external sources.
4. `skills/devs-runtime-verifier/SKILL.md` did not require an independent
   recheck of authoritative external sources before `PASS` or `BLOCKED`.
5. `skills/devs-spec-author/SKILL.md` required official documentation when
   needed, but did not require the resulting authority set and access route to
   be recorded as a durable workstream contract field.
6. The instruction layer did not explicitly forbid weakening a mandatory
   template law during spec authoring.
7. The templates did not distinguish authority inventory from implementer
   recheck evidence and verifier authority audit as separate surfaces.
8. The authority rule slot did not explicitly require material qualifiers,
   API-specific default branches, or opt-out paths to be preserved from the
   source.

### RED Evidence Commands

1. `rg -n "External Authority Sources|Preferred Access|Fallback Access|external authority" workstream_templates/spec_template.md workstream_templates/state_template.md skills/devs-spec-author/SKILL.md skills/devs-runtime-implementer/SKILL.md skills/devs-runtime-verifier/SKILL.md`
2. `rg -n "re-check|authoritative external|external seam|Preferred Access|Fallback Access" skills/devs-spec-author/SKILL.md skills/devs-runtime-implementer/SKILL.md skills/devs-runtime-verifier/SKILL.md`

## GREEN Target

1. `spec.md` templates must carry a mandatory `External Authority Sources`
   section for external seams, with explicit preferred and fallback access
   routes.
2. `state.md` templates must carry enough contract surface to record the same
   requirement when work runs spec-less.
3. `spec-author` must read and record the authoritative source set.
4. `runtime-implementer` must re-check the relevant source set before tests and
   code.
5. `runtime-verifier` must re-check the relevant source set independently
   before acceptance.
6. Mandatory template laws must survive authoring at equal or stronger force.
7. Source inventory, implementer recheck evidence, and verifier authority
   audit must remain separate contract surfaces.
8. External authority summaries must preserve behavior-changing qualifiers from
   the canonical source.

### GREEN Verification

1. `workstream_templates/spec_template.md` now contains `External Authority Sources`,
   explicit `Preferred Access` and `Fallback Access` columns, and a
   non-negotiable workstream rule that binds all three roles to the same
   authority set.
2. `workstream_templates/state_template.md` now carries a minimal-contract
   field plus source-link and semantic-map fields for external authority,
   including spec-less workstreams.
3. `skills/devs-spec-author/SKILL.md` now requires recording the authority set
   and access routes in the active `spec.md`.
4. `skills/devs-runtime-implementer/SKILL.md` now requires pre-code authority
   rechecks and evidence capture.
5. `skills/devs-runtime-verifier/SKILL.md` now requires an independent
   authority audit before acceptance.

### GREEN Verification Commands

1. `rg -n "External Authority Sources|Preferred Access|Fallback Access|external authority" workstream_templates/spec_template.md workstream_templates/state_template.md skills/devs-spec-author/SKILL.md skills/devs-runtime-implementer/SKILL.md skills/devs-runtime-verifier/SKILL.md`
2. `rg -n "re-check|authoritative external|external seam|Preferred Access|Fallback Access" skills/devs-spec-author/SKILL.md skills/devs-runtime-implementer/SKILL.md skills/devs-runtime-verifier/SKILL.md`
