# Prompt: close out a piece of work

You are doing **closure housekeeping** for a completed change or execution plan.
Do this only when the project's policy for that work is satisfied — typically:
implemented, verified, independently reviewed with no open blockers, and (where
the project configures an owner-acceptance gate) explicitly accepted by the
owner/maintainer. If a required step is missing, stop.

## Do (skip steps for modules this project does not use)

1. **If the project uses execution plans:** update the plan to record, factually,
   the final review verdict, the acceptance (and date, if there is a gate), the
   final state, and the real verification results; add a **Result** section that
   *links* the documents this work produced or changed rather than restating
   them. Then move/mark it completed per the project's convention and update the
   plan index.
2. **If the project uses a status doc:** update it as a **snapshot** — current
   milestone, current state, next step. Do **not** append this task to a growing
   history list; the completed plan, Git history, and any changelog are the
   history.
3. **Do not start the next piece of work.** No new plan, no scaffolding, no
   dependencies.

## Verify

Inspect every changed file. Validate relative Markdown links (especially after
any move). Scan for secrets. `git diff --check`. `git status`. Review the full
diff. Confirm the status doc reads as a current snapshot, not a changelog, and
that no application code or dependency was introduced.

## Commit

Only if the owner asked: stage the intended changes, review the staged diff once
more, make exactly one commit with the message the owner specified, do not amend
earlier commits, do not push unless told to, then report `git status` and
`git log -1 --oneline`.
