# Prompt: bootstrap a project's harness

You are standing up the agent harness for a **project repository**. One-time
task. The result must be **fully self-contained**: after this, ordinary work on
the project must not need `agent_harness`, its docs, its prompts, or any link
back to it.

## Inputs from the owner (ask if missing — do not invent)

- Project name and a one-paragraph description.
- Repository shape: single small package / library / CLI, monorepo, or
  multi-team repo.
- Decisions already made (technology, structure, constraints) and hard external
  constraints.
- Which agents will actually work on this repo (Claude, Codex, others, humans
  only).
- Desired governance intensity (how much process for high-risk changes).

## Steps

1. **Inspect the target repo** (`git status`, file listing, existing content).
   Assume nothing that is not present.
2. **Establish the V1 core** (always): a root `AGENTS.md`, a change workflow, and
   a verification contract. For a small project the workflow and verification
   contract are short sections **inside `AGENTS.md`** — the minimal valid harness
   is a single `AGENTS.md`. Then **select optional modules** from
   [../docs/MODULES.md](../docs/MODULES.md) only where the project genuinely
   benefits. Do not add `PRODUCT`, `ARCHITECTURE`, `ADR`, `PROJECT_STATUS`,
   execution plans, independent review, an acceptance gate, or dedicated
   workflow/verification files just to have them.
3. **Choose document locations** that fit the repo shape (root files for a small
   repo; a `docs/` tree or per-package docs for a monorepo/multi-team repo).
4. **Copy and adapt every operational rule the project's chosen setup uses, as
   local project-owned content.** Always local: `AGENTS.md`, the change workflow,
   and the verification contract (the last two may be sections of `AGENTS.md`, or
   separate files if that module is selected). Local only if selected: the
   review workflow, the owner-acceptance gate, and recurring
   author/reviewer/closure instructions (as local prompt files or a
   `CONTRIBUTING`/workflow section). Adapt generic wording to this project. **Do
   not** leave any operational rule as "see `agent_harness`".
5. **Agent entrypoints:** always create the root `AGENTS.md` (from
   [../templates/AGENTS.md](../templates/AGENTS.md)). Create a per-agent adapter
   (`CLAUDE.md`, `CODEX.md`, …) **only** for agents actually used; each is a thin
   file that defers to `AGENTS.md` plus agent-specific notes. No vendor adapter
   is mandatory.
6. **Record chosen module set and document locations in `AGENTS.md`** so agents
   can discover them.
7. **Record only what is decided.** Everything open goes in the status doc (if
   used) or `AGENTS.md` open-questions.
8. **Do not build the application.** No package manager, dependencies, framework,
   or code unless the owner explicitly asks and it is captured in a plan.
9. Strip guidance lines from every copied template.

## Verify

- Inspect every file created. Validate all relative Markdown links. Scan for
  secrets. `git diff --check`. Review the full `git diff`.
- **Reference scan:** grep the initialized project for operational references
  back to `agent_harness` (name, paths, links). Any that are part of a workflow
  are a defect — replace with local content. Attribution/background mentions are
  allowed if clearly optional.
- **Self-contained acceptance check — answer explicitly:** *If the
  `agent_harness` repository were deleted now, could agents continue normal
  development using only this project repository?* The answer must be **YES**. If
  not, find what is still missing and copy it in.

## Report

Modules selected and why; document locations chosen; files created; decisions
encoded; open questions; verification results including the reference-scan and
the self-contained acceptance answer. Do not commit unless the owner asks.
