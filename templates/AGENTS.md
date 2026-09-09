# AGENTS.md

> The project's root entrypoint for agents and humans. A **map**, not an
> encyclopedia (progressive disclosure). Keep it readable in one sitting. This
> file and the documents it points to are self-contained — do not link out to
> `agent_harness` for operational rules.
>
> Delete guidance lines before use.

## What this project is

<One or two sentences: what it does, for whom. Link the product doc if the
project has one.>

## Where things live

> Fill in only the rows this project actually uses. Use the paths this project
> chose (they need not match any other project's).

| You need | Look in |
| --- | --- |
| Product requirements | `<path or "n/a">` |
| Architecture | `<path or "n/a">` |
| Decisions (ADRs) | `<path or "n/a">` |
| Current status | `<path or "n/a">` |
| Change workflow | `<this file, section below, or docs/WORKFLOW.md>` |
| Verification contract | `<path or section>` |
| Execution plans | `<path or "n/a">` |
| Review workflow | `<path or "n/a">` |

## Source of truth

This repository is the canonical state of the project. Anything needed for future
work must be discoverable here.

## Change workflow

> Inline the core workflow, or keep a local `docs/WORKFLOW.md` and summarize here.
> Core habits: read relevant context first; inspect version-control state;
> smallest coherent change; do not invent missing requirements; no unrelated
> cleanup; keep docs in sync; run the checks; review your own diff; honest
> reporting; do not commit/push unless asked.

Governance is **risk-based**: <state this project's low / medium / high-risk
policy — what needs a plan, what needs independent review, what needs owner
acceptance>.

## Verification

> What the project's verification entry point is and what it runs *today*. It
> grows with real capabilities; it never contains fake or no-op checks. In a Git
> repo, `git diff --check` clean is part of every change.

## Invariants

> The hard rules for this project. Where a rule is meant to be machine-checked,
> state it as a finite contract (an exhaustive allow/deny form), not "if needed".
> Many projects have few or none — do not invent them.
