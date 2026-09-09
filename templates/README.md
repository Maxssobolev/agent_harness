# Templates

Per-artifact skeletons. `AGENTS.md` is core — every project gets one. Copy the
rest only for the optional modules the project selects (see
[../docs/MODULES.md](../docs/MODULES.md)). Put each where it suits *this* project,
fill it in, and delete the guidance (`> …` notes, `<…>` placeholders). After that
the project owns them and does not track `agent_harness`.

| Template | Module | Suggested path (project-choice) |
| --- | --- | --- |
| [AGENTS.md](AGENTS.md) | **core — required** | repo root `AGENTS.md` |
| [PRODUCT.md](PRODUCT.md) | product-doc | `PRODUCT.md` or `docs/PRODUCT.md` |
| [ARCHITECTURE.md](ARCHITECTURE.md) | architecture-doc | `ARCHITECTURE.md` or `docs/ARCHITECTURE.md` |
| [PROJECT_STATUS.md](PROJECT_STATUS.md) | project-status | `PROJECT_STATUS.md` or `docs/STATUS.md` |
| [ADR.md](ADR.md) | adr | `docs/adr/NNNN-slug.md` |
| [adr-index.md](adr-index.md) | adr | `docs/adr/README.md` |
| [EXEC_PLAN.md](EXEC_PLAN.md) | exec-plans | `docs/exec-plans/<id>.md` |
| [exec-plan-index.md](exec-plan-index.md) | exec-plans | `docs/exec-plans/README.md` |

Paths are suggestions. A single-package repo may keep everything at the root; a
monorepo may scope docs per package; a multi-team repo may put them under a
`docs/` tree with team subdirectories. **Record the chosen locations in the
project's `AGENTS.md`** so agents can find them.

A project always ends up with a change workflow and a verification contract —
core capabilities — but they may live as sections inside `AGENTS.md`; a separate
`docs/WORKFLOW.md` / `docs/VERIFICATION.md` is optional (add it when embedding
gets unwieldy). The independent-review workflow is an optional module. The
generic text for all three is in [../docs/](../docs/); bootstrap copies whatever
the project adopts into the project and adapts it. Projects do not link back to
`agent_harness` for operational rules.

Keep filled-in templates lean: real structure and content, not rows of `TBD`.
