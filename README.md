# agent_harness

A small, reusable, **project-agnostic engineering system** for agent-driven
software projects: the generic parts of a repository that let mostly-autonomous
coding agents (and humans) do reliable work from the repository alone.

It is a **starter you copy from**, not a framework and not a runtime. You pick
the parts a given project needs, copy them into that project, and adapt them.
After that the project owns its harness and never refers back here.

## Dependencies

The harness has **no runtime, package-manager, or application-framework
dependencies**. It is plain Markdown. It assumes a **Git repository** for the
documented workflow (`git status`, diff review, `git diff --check`). Any
`AGENTS.md`-style instruction files are a **tooling convention**, not an
application dependency, and are themselves optional per project.

There is no CLI and V1 does not add one.

## Shape: minimal core + optional modules

**Required V1 core — every initialized project has:**

- a root **`AGENTS.md`** — the portable/default repository-instruction
  convention (never optional);
- a **change workflow**;
- a **verification contract** (project-native).

For a small project the workflow and verification contract MAY be short sections
**inside `AGENTS.md`** — they do not need their own files. So the minimal valid
project harness is a single file:

```text
AGENTS.md   — repository navigation/context + a lightweight change workflow
            + real project-native verification instructions
```

**Optional modules** — add only when the project benefits: PRODUCT doc,
ARCHITECTURE doc, PROJECT_STATUS, ADR workflow, execution plans,
independent-review workflow, owner/maintainer acceptance gate, vendor/tool
adapters such as `CLAUDE.md`, and **dedicated `WORKFLOW` / `VERIFICATION` files**
(when embedding those core capabilities in `AGENTS.md` gets unwieldy). See
[`docs/MODULES.md`](docs/MODULES.md) and the principles in
[`docs/HARNESS_PRINCIPLES.md`](docs/HARNESS_PRINCIPLES.md).

Governance is **risk-based, not file-count based** (see `docs/WORKFLOW.md`): a
change that touches many files is not automatically "big"; risk, ambiguity,
architectural breadth, reversibility, and system impact are what decide how much
process a change gets.

## How a project uses it

```text
agent_harness  ──bootstrap: pick modules, copy + adapt──▶  new project repository
                                                                 │
                                                                 ▼
                            the project's own AGENTS.md + docs are its source of truth
                                                                 │
                                                                 ▼
                          agents and humans work from the project repo alone
```

**Self-contained result.** Bootstrap copies every operational rule a project's
chosen workflow needs *into the project*. After bootstrap, ordinary work never
reads this repository, its docs, its prompts, or a link back to it. Acceptance
check for a bootstrap: *if `agent_harness` were deleted, could agents keep
developing the project using only its own repository?* — the answer must be
**yes**. See [`prompts/bootstrap-project.md`](prompts/bootstrap-project.md).

References back to `agent_harness` are allowed only as optional
attribution/background, never as a required part of a workflow.

## Repository layout

```text
AGENTS.md                 how to work on THIS repository

docs/                     authoritative generic statements (also the source bootstrap copies from)
  HARNESS_PRINCIPLES.md   the reusable ideas; core subset marked
  WORKFLOW.md             core change workflow + risk-based governance model
  VERIFICATION.md         what a verification command may mean (environment-neutral)
  REVIEW.md               the independent-review workflow (a module)
  MODULES.md              catalog: core vs optional modules, and how to choose

templates/                per-artifact skeletons a project copies and then owns
  README.md               which template belongs to which module; suggested paths
  AGENTS.md               project root entrypoint
  PRODUCT.md  ARCHITECTURE.md  PROJECT_STATUS.md
  ADR.md  adr-index.md
  EXEC_PLAN.md  exec-plan-index.md

prompts/                  role briefs for recurring agent tasks
  README.md
  bootstrap-project.md    one-time: stand up a project's harness
  implement-change.md     author role
  review-change.md        independent-reviewer role
  close-work.md           closure housekeeping
```

## V1 scope and dogfooding

V1 is deliberately minimal. The harness's own lifecycle (execution plans,
independent review, owner acceptance) is **not applied retroactively** to this
initial creation — that lifecycle did not exist while V1 was being written.
Dogfooding begins with the first substantial post-V1 change. See
[`AGENTS.md`](AGENTS.md).
