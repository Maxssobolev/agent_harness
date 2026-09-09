# ARCHITECTURE

> Module: architecture-doc. A high-level description of how the system is built —
> **not** an implementation plan and **not** a decision log.
>
> **Every section below is optional.** Include a section only if the project
> actually has that structure. A flat single-package library or CLI may keep
> just *System overview* and nothing else — do not invent components, package
> boundaries, ownership, or a dependency graph where none are useful.
>
> Delete guidance lines and unused sections before use.

## System overview  *(useful when applicable)*

<One short paragraph: the overall shape — a single binary, a library, a service,
a few packages, a pipeline. Enough for a newcomer to orient.>

## Components  *(optional)*

> Only if there is more than one meaningful part. List them and what each is
> responsible for.

| Component | Responsibility |
| --- | --- |
| <name> | <what it does> |

## Component ownership  *(optional)*

> Only if it matters that a given type/contract/responsibility lives in exactly
> one place. State the unique owner per contract.

## Dependency rules  *(optional)*

> Only if the project constrains how parts may depend on each other. **If a
> project has machine-enforced component/package boundaries, document them as
> finite contracts** — an exhaustive allowlist, no contextual exceptions:

```text
core     → []
feature  → [core]
app      → [core, feature]
```

> Name the check that enforces this and from when (see the verification doc). If
> nothing enforces boundaries, omit this section.

## Deployment / runtime architecture  *(optional)*

<Where it runs, what talks to what at runtime, external services, data stores.
Omit for a library or a local tool.>

## Data / state  *(optional)*

<Where authoritative state lives; what is immutable; what is derived and must be
rebuildable.>

## What is enforced mechanically  *(optional)*

<Which invariants above a check enforces today, and which are still prose. Keep
this honest.>
