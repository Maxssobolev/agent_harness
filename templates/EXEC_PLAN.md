# <id> — <plan title>

Status: <in progress | completed YYYY-MM-DD>
<one or two lines: where this plan is in its lifecycle; review rounds so far>

> Optional fields
>
> - **Delivery** — <task override from the local delivery contract>
> - **Review gate** — <reference to the local readiness policy, if applicable>

> Module: exec-plans. Working document for one coherent piece of work — usually
> medium/high-risk or multi-session. Written before the work, kept current
> during it, finalized with the real result. Keep it self-contained; do not link
> to `agent_harness`.
>
> Delete guidance lines before use.

## Goal

<The outcome, in one or two sentences.>

## Scope

<What is included.>

## Acceptance criteria

<Checkable conditions for "done" — each verifiable by inspection or a command.>

## Verification

<The exact checks and their actual results, per the local verification
contract. Record the final claims audit at handoff and closure.>

## Progress

<Running log of what actually happened, newest last. Record review rounds and
verdicts factually, including findings that were correct as-is.>

---

> Include the sections below only when they carry real information.

## Context

<Why this work exists now; the state it starts from.>

## Non-goals

<What is explicitly excluded.>

## Constraints

<Rules the work must respect.>

## Requirements

<For a large plan, optionally give requirements stable IDs such as `R1` or
`S6-R1` for task and review references. Follow the local plan workflow for
revisions and supersessions.>

## Implementation steps

<The plan of record. Update as it changes.>

## Decisions made during implementation

<Choices future contributors need to know. Promote anything architectural to an
ADR if the project uses that module.>

## Problems / failed approaches worth preserving

<Dead ends and why they failed.>

## Result

<Filled at closure: final state, the review verdict, owner acceptance if the
project configures that gate, and links to the documents this work produced or
changed.>
