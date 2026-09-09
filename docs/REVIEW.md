# Independent review

*(Module. The recommended default for high-risk / substantial agent-driven work;
project-configurable — see [WORKFLOW.md](WORKFLOW.md#governance-model).)*

The reviewer is a **separate role** from the author (a different agent session,
or a person). Its job is to catch, before the change is accepted, what the
author's own report would miss.

## Ground rule

**Review the repository, not the report.** Read the actual version-control state,
the full diff (staged and unstaged), and the current contents of the affected
files. Treat the author's summary as a set of claims to verify. If the author
says "X was done", confirm X is in the files.

## What to check

Scope it to the change and its stated acceptance criteria, plus:

- **Correctness** — does the diff actually achieve the goal and meet each
  acceptance criterion?
- **Consistency** — does any statement contradict another document in the repo?
  A rule stated two ways is a finding.
- **Enforceability** — are rules meant to be machine-checked written as finite,
  unambiguous contracts (no "if needed" a check cannot evaluate)?
- **Honest verification** — every check reported as passed: real, and plausibly
  run? Any no-op / dummy / empty checks?
- **Claims vs reality** — dated notes, "added/updated/moved", status lines: do
  the files bear them out?
- **Scope & safety** — unrequested cleanup, new runtime/dependencies, secrets.

## Findings

Triage every finding into exactly one level:

| Level | Meaning |
| --- | --- |
| **Blocker** | Must be fixed before the change proceeds. Wrong, contradictory, unenforceable-as-written, or unsafe. |
| **Important** | Should be fixed. Not strictly blocking, but leaving it causes avoidable trouble. |
| **Minor** | Worth fixing. Cosmetic, wording, small inconsistency. |

One problem per finding: location, what is wrong, the minimal fix.

## Verdict

```text
Verdict: REQUEST CHANGES | APPROVE

Blockers:   - <where> — <what> — <minimal fix>
Important:  - ...
Minor:      - ...

Readiness: READY | NOT READY — <one line>
```

"Not ready" whenever a blocker is open. Note findings you checked and found
correct as-is.

## Iteration

The author addresses findings and re-runs verification. The reviewer re-checks
**against the updated repository**, not against the author's list of changes.
Repeat until no blockers remain, then hand to the owner-acceptance step if the
project configures one ([WORKFLOW.md](WORKFLOW.md#owner-acceptance)).

Record each review round and its verdict wherever the project logs the work
(e.g. the execution plan), factually — including findings that were correct
as-is.
