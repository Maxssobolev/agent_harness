# Execution plans

> Module: exec-plans. The project's authoritative statement of its plan lifecycle
> and its numbering/concurrency convention. Link here from elsewhere.
>
> Delete guidance lines before use.

## Lifecycle

```text
draft ─▶ in progress ─▶ (implement + verify + review per policy)
                     ─▶ (owner acceptance, if configured) ─▶ completed
```

A completed plan is kept as the record of that work.

## This project's convention

> Choose one and state it. Examples:
>
> - Small single-owner project: one active plan at a time; single sequential
>   series `0001-slug`, `0002-slug`, …
> - Monorepo / multi-team: scoped IDs (e.g. `web-2024-11-auth`), team/component
>   prefixes, multiple concurrent active plans allowed.
>
> There is no universal `WIP=1` and no universal single stream — this section is
> where the project decides.

**Convention:** <state it here>

## Index

| Plan | Status | Outcome (when completed) |
| --- | --- | --- |
| <id> | <in progress / completed YYYY-MM-DD> | <one line> |
