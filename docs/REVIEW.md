# Independent review

*(Module. The recommended default for high-risk / substantial agent-driven work;
project-configurable — see [WORKFLOW.md](WORKFLOW.md#governance-model).)*

The reviewer is a **separate role** from the author (a different agent session,
or a person). Its job is to catch, before the change is accepted, what the
author's own report would miss.

## Ground rule

**Review the repository, not the report.** Inspect the actual version-control
state, the diff in scope, and the affected files at the review target. Treat
the author's summary as claims to verify.

## Review target

- **Immutable revisions.** For high-risk work, prefer an exact Base SHA and
  Head SHA when the project's [delivery model](WORKFLOW.md#delivery-contract)
  permits it. Confirm that the reviewed HEAD matches the intended Head SHA
  before reviewing. Compare those revisions (`git diff <base-sha> <head-sha>`)
  and inspect file contents at that head. Run any reviewer checks in a clean
  checkout of the same revision. Local commits are sufficient.
- **Local changes.** A project can choose to review staged changes, unstaged
  changes, or the full worktree. Agree on the base, files, and states in scope.
  A full worktree review includes staged and unstaged changes and any untracked
  files belonging to the change. Identify the state inspected and re-establish
  it if the changes move during review.

## What to check

In a comprehensive review, inspect the full change against its stated goal
and acceptance criteria. Also check:

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
| **Blocker** | A defect that defeats a required outcome, breaks a governing contract, or makes the change unsafe. |
| **Important** | A material problem with correctness, reliability, or maintainability that falls short of Blocker severity. |
| **Minor** | Worth fixing. Cosmetic, wording, small inconsistency. |

One problem per finding: location, what is wrong, the minimal fix.

## Readiness and verdict

A project adopting independent review states its readiness gate in its local
policy. Examples include zero open Blockers, zero open Blockers and zero open
Important findings, or another explicit rule. Severity describes each finding.
The local gate determines the readiness verdict.

Use the project's gate for both the verdict and the readiness line:

```text
Verdict: REQUEST CHANGES | APPROVE

Blockers:   - <where> — <what> — <minimal fix>
Important:  - ...
Minor:      - ...

Readiness: READY | NOT READY — <one line>
```

If the gate is unspecified, report the findings and mark the verdict and
readiness as undetermined pending local policy.

Report the exact reviewed HEAD for an immutable target, the diff scope
(including Base and Head SHAs for a revision range), and the verification
state. State which checks you ran, what other evidence you inspected, and
what remains unverified. Note findings you checked and found correct as-is.

## Iteration

The author addresses findings and reruns verification. The reviewer checks the
updated repository and applies the local readiness gate again. When the gate
is met, hand off for owner acceptance if the project configures it
([WORKFLOW.md](WORKFLOW.md#owner-acceptance)).

Record each review round and its verdict wherever the project logs the work
(e.g. the execution plan), factually — including findings that were correct
as-is.

### Narrow follow-up review

Use a narrow follow-up only when a comprehensive review established the
previous scope, remaining findings are explicit, and the exact fix diff is
available, narrow, and free of unrelated changes. Compare the last reviewed
state with the new target. For immutable revisions, use the previous reviewed
Head SHA and the new Head SHA to capture the whole fix diff.

Recheck the original findings, the exact fix diff, regressions the diff could
introduce, and the required verification. Name the original findings in the
review output, record their disposition, and apply the gate to all open
findings, including any carried over. Rely on the established review for the
rest of the scope. Return to comprehensive review if the fix scope materially
expanded or the prerequisites cannot be established.
