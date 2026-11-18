# Prompts

Role briefs for recurring agent tasks. Each brief: (1) sets the role, (2) tells
the agent to read the **project's own** authoritative docs, (3) adds only
behavior specific to that task. They do not restate workflow, review, or
verification policy — that lives in the project's repository after bootstrap.

| Prompt | Role | When |
| --- | --- | --- |
| [bootstrap-project.md](bootstrap-project.md) | Bootstrapper | Once, to stand up a project's harness from `agent_harness`. |
| [implement-change.md](implement-change.md) | Author | To carry out a change, sized to its risk tier. |
| [review-change.md](review-change.md) | Independent reviewer | When project policy calls for independent review of a change. |
| [close-work.md](close-work.md) | Closer | Housekeeping after review and (if configured) owner acceptance. |

Use the review brief where the project calls for independent review. Adapt
wording to the project and keep the intent. `bootstrap-project.md` is the only one
that reads `agent_harness` — the rest run inside a self-contained project and
never need it.
