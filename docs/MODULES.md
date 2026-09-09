# Core and modules

The harness is a minimal **core** plus **optional modules**. Bootstrap selects
the modules a project actually benefits from and copies their materials into the
project. Nothing forces full governance onto a small library or CLI.

## Core (always)

Every initialized project has these, however small the project.

| Core piece | What it means | Generic source |
| --- | --- | --- |
| **Root `AGENTS.md`** | The portable/default repository-instruction entrypoint. **Not optional.** Maps the repo: what it is, where things live, and — for a small project — the workflow and verification contract inline. | [templates/AGENTS.md](../templates/AGENTS.md) |
| **A change workflow** | The read-context / inspect-VCS-state / smallest-coherent-change / don't-invent-requirements / no-unrelated-cleanup / review-your-own-diff / honest-reporting habits. A **capability**, not necessarily a file — may be a section of `AGENTS.md`. | [WORKFLOW.md](WORKFLOW.md#core-change-workflow-every-project) |
| **A verification contract** | One project-native entry point; stage-aware; honest; no fake/no-op checks. A **capability**, not necessarily a file — may be a section of `AGENTS.md`. | [VERIFICATION.md](VERIFICATION.md) |
| Principles C1–C3 (repository over prompt; progressive disclosure; honest verification) | The ideas the above rest on. | [HARNESS_PRINCIPLES.md](HARNESS_PRINCIPLES.md) |
| Risk-based governance model | How much process a change gets is decided by risk, not file count. | [WORKFLOW.md](WORKFLOW.md#governance-model) |

**The minimal valid project harness is a single file** — a filled-in `AGENTS.md`
containing repository navigation/context, a lightweight change workflow, and real
project-native verification instructions. Everything below is optional.

## Optional modules

Pick what fits. Each row: what it adds, when it is worth it, what to copy.

| Module | Adds | Worth it when | Copy |
| --- | --- | --- | --- |
| **product-doc** | A stable statement of what the project is for | The "why/what" is non-obvious or shared across people | [templates/PRODUCT.md](../templates/PRODUCT.md) |
| **architecture-doc** | A high-level architecture doc with *conditional* sections | There is real structure worth writing down (services, packages, a pipeline, deployment topology) | [templates/ARCHITECTURE.md](../templates/ARCHITECTURE.md) |
| **adr** | A decision log + the immutability policy | Decisions need to be traceable and stable over time | [templates/ADR.md](../templates/ADR.md), [templates/adr-index.md](../templates/adr-index.md) |
| **project-status** | A short current-state snapshot | Work spans sessions/people and "where are we" is asked often | [templates/PROJECT_STATUS.md](../templates/PROJECT_STATUS.md) |
| **exec-plans** | Execution-plan format + lifecycle | The project runs high-risk or multi-session work | [templates/EXEC_PLAN.md](../templates/EXEC_PLAN.md), [templates/exec-plan-index.md](../templates/exec-plan-index.md) |
| **independent-review** | The separate author/reviewer workflow | High-risk agent-driven changes; correctness matters more than speed | [REVIEW.md](REVIEW.md) |
| **owner-acceptance** | An explicit sign-off gate before work closes | Multiple stakeholders, or an owner who must approve outcomes | [WORKFLOW.md](WORKFLOW.md#owner-acceptance) |
| **dedicated workflow / verification files** | Separate `docs/WORKFLOW.md` / `docs/VERIFICATION.md` instead of sections inside `AGENTS.md` (the workflow and verification contract themselves are core — this row is only about giving them their own files) | Embedding them makes `AGENTS.md` too long to read in one sitting | [WORKFLOW.md](WORKFLOW.md), [VERIFICATION.md](VERIFICATION.md) |
| **agent-entrypoints** | Per-agent adapter files (`CLAUDE.md`, `CODEX.md`, …) that defer to `AGENTS.md` | The project is worked by an agent whose tooling reads its own filename | no template — see the note below (a few lines) |

Notes:

- **Root `AGENTS.md` is core, not a module** (see the core table). The *workflow*
  and *verification contract* are core capabilities too; only a *separate file*
  for either is optional, because their content may live inside `AGENTS.md`.
- **No vendor-specific entrypoint is mandatory.** Add `CLAUDE.md` / `CODEX.md` /
  etc. only for agents actually used on the project. Each is a thin adapter — one
  or two lines pointing at (or, if the tool supports includes, importing)
  `AGENTS.md` as the primary instructions, plus only the notes specific to that
  agent. It never restates project rules.
- Modules compose: `exec-plans` + `independent-review` + `owner-acceptance`
  together give the strict lifecycle; any subset is valid.
- Document layout is project-choice. The template README lists *suggested* paths;
  bootstrap picks paths that suit a single-package repo, a monorepo, or a
  multi-team repo, and records the chosen locations in the project's `AGENTS.md`.
