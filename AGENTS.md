# AGENTS.md

How to work on **the `agent_harness` repository itself**. A map — follow the
links for detail. (There is no separate `CLAUDE.md` here; this file is the whole
entrypoint. Per-agent adapter files are optional — see
[`docs/MODULES.md`](docs/MODULES.md).)

`agent_harness` produces a reusable harness that other projects copy parts of and
then own. Nothing here is meant to be pasted wholesale into a project.

## Where things live

| You need | Look in |
| --- | --- |
| The reusable ideas; which are core | [docs/HARNESS_PRINCIPLES.md](docs/HARNESS_PRINCIPLES.md) |
| Core change workflow + risk-based governance | [docs/WORKFLOW.md](docs/WORKFLOW.md) |
| What a verification command may mean | [docs/VERIFICATION.md](docs/VERIFICATION.md) |
| The independent-review workflow (a module) | [docs/REVIEW.md](docs/REVIEW.md) |
| Core vs optional modules, and how to choose | [docs/MODULES.md](docs/MODULES.md) |
| Per-artifact skeletons projects copy | [templates/README.md](templates/README.md) |
| Role briefs for recurring agent tasks | [prompts/README.md](prompts/README.md) |
| Human-facing overview and dependency wording | [README.md](README.md) |

## Rules for changing this repository

The core workflow in [docs/WORKFLOW.md](docs/WORKFLOW.md) applies here too. In
addition:

1. **Keep it generic.** Do not encode any one project's product, architecture,
   technology, vendor, or naming as a rule of the harness. A concrete project may
   appear only as a brief illustrative example, never as a requirement.
2. **Keep it small.** Add a document or template only when it earns its place;
   prefer extending an existing one. Every added rule needs one authoritative
   owner document (progressive disclosure — see the principles doc).
3. **Do not restate long policies in prompts or templates.** Prompts set a role
   and point at the project's own local docs. Templates carry structure plus
   short reminders, not whole policies.
4. **No runtime.** No package manager, dependencies, build, framework, or CLI.
   Plain Markdown.
5. **Honest verification.** Never claim a check ran or passed unless you ran it
   and saw the result. `git diff --check` clean.
6. **Review the full `git diff` yourself** before reporting; report the real
   results of the checks you ran.
7. Do not `git commit` or `git push` unless the owner asks.

## Governance for this repo

Use the risk model in [docs/WORKFLOW.md](docs/WORKFLOW.md#governance-model). A
restructure, a new/removed principle, or a change to the bootstrap contract is
**high risk**: write an execution plan (from
[templates/EXEC_PLAN.md](templates/EXEC_PLAN.md), under `docs/exec-plans/active/`
— create that directory when first needed), have it independently reviewed
([docs/REVIEW.md](docs/REVIEW.md)), and get explicit owner acceptance before it
closes. Typo/wording fixes are low risk: just make them.

**V1 exemption.** The initial creation of V1 is not governed by this lifecycle —
the lifecycle did not exist yet. Dogfooding starts with the first substantial
post-V1 change.

## Verification for this repo

No build or test suite; V1 adds none. Verification here is: inspect every changed
file; validate relative Markdown links; scan for secrets; scan for project- or
vendor-specific assumptions that leaked into generic rules; confirm no
runtime/dependency was introduced; `git diff --check`; `git status`; read the
full diff.
