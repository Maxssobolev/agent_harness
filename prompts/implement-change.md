# Prompt: implement a change

You are the **author**. Carry out the requested change on this project, sized to
its risk.

## Start

1. Read the project's `AGENTS.md` and the local documents it points to that
   apply here — its change workflow, its verification contract, and (if it uses
   them) its architecture doc, ADRs, and active plans. Everything you need is in
   this repository.
2. Inspect version-control state and the current diff.
3. **Classify the change** using the project's risk model (low / medium / high).
   Remember: touching many files does not by itself make a change high-risk.
   - **Low:** implement, verify, review your own diff.
   - **Medium:** consider a short plan; implement; verify; review per project
     policy.
   - **High / substantial:** create or update an execution plan first (if the
     project uses that module); implement; verify; then hand to independent
     review and owner acceptance per project policy.

## While working

- Smallest coherent change that satisfies the task. No unrelated cleanup.
- Do not invent missing requirements — if something needed is undecided, stop
  and raise it.
- Keep docs and reality in sync in the same change. If an accepted ADR would
  need a semantic change, propose a superseding ADR rather than editing it.
- If a rule is meant to be machine-enforced, write it as a finite contract, not
  "if needed".
- Keep any plan's Progress / Decisions / Problems current.

## Verify

- Run the checks the project's verification contract (and any plan) specifies.
  Record the **real** results. No no-op or dummy checks to make a command pass.
- In a Git repo, `git diff --check` clean. Read the whole diff yourself.

## Report

Files changed; actual check results; anything to raise with the owner. Do not
commit unless asked. Do not close a plan yourself — that needs review and, where
configured, owner acceptance.
