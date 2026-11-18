# Verification

What a verification command may mean, and how it grows. Stack- and
environment-neutral: the harness assumes a Git repository for the documented
workflow, and nothing else.

## The contract

A project SHOULD have **one repository-level verification entry point**, named
and implemented in whatever is native to its stack (a `Makefile` target, a
script, a task runner, a language's test command — the harness does not care
which, and requires none in particular).

**It runs all verification that is actually implemented and applicable to the
current state of the repository — and nothing else.**

- It grows as real capabilities land. Each stage adds real checks for what that
  stage actually built.
- **If the project has CI**, CI runs the same entry point, so CI gains new
  checks automatically. Projects without CI simply run it locally.
- A capability that does not exist yet is **not in the command yet**. Correct,
  not a hole to fill.

## Not allowed (core)

Never, to make the command "pass" or look complete:

- no-op steps;
- always-passing dummy tests;
- empty test suites;
- "pass with no tests" / "allow empty" flags;
- checks for components that do not exist.

A green run must correspond to verification that exists and ran.

## Honest reporting (core)

- Report a check as passed only if you ran it and saw it pass.
- If you did not run it, say so and why.
- Distinguish "passed", "failed (output …)", "skipped (reason)", and "not
  applicable yet".
- In a Git repository, `git diff --check` clean is part of every change.

### Retries

When a check passes on retry, report the initial failure, the evidence or
known cause, any targeted investigation performed, and the successful retry.
Preserve both outcomes. Distinguish failures in the implementation or tests
(including deterministic test failures) from transient external or
infrastructure failures and timeouts or resource limits when evidence
supports that distinction. Leave the cause unresolved when the evidence is
inconclusive.

## Claims audit

Before the final implementation handoff and again before closing substantial
work, check the changed and directly related documentation and report against
the repository and verification evidence. Confirm that claims about planned
and implemented work, current and next stages, test counts, command names,
file paths, workflow and job terminology, dependencies, completion, and review
status match what can be established. Correct stale claims and record the
outcome and any unresolved discrepancies. Inspection is sufficient and the
scope should match the project and change.

## Closure verification

Before delivery, inspect the contents of the closure changes, including new
files, for accidentally included secrets, tokens, and credentials. When
committing, check the staged content that will actually be committed. A clean
result from a limited pattern scan gives no guarantee that the changes are
free of secrets. If you find a potential secret, stop delivery until it is
resolved. In the report, identify the affected location without exposing the
suspected value.

## Stage-aware growth

Document the intended full verification hierarchy as a **labelled target** —
cheapest / most-local first — and mark, per level, which stage introduces it.
Until a level's subject exists, it is not in the command.

A generic hierarchy to adapt (add, remove, or rename levels to fit the project
and its stack):

```text
targeted checks       checks for the code under change                 (ongoing)
      ↓
static analysis       whatever the stack offers (types, lint, vet, …)  (from first code)
      ↓
structural checks     module/boundary/ownership contracts, if any      (if the project has them)
      ↓
build                 each build target produces its artifact          (if the project builds)
      ↓
component checks      validation of each subsystem as it is built      (per subsystem)
      ↓
integration           cross-component flows                            (once >1 component exists)
```

## Machine-enforced contracts

If an invariant is meant to be enforced by one of these checks, write it as a
finite, unambiguous contract (see [HARNESS_PRINCIPLES.md](HARNESS_PRINCIPLES.md)
A3). Example of the *shape*, not the content:

```text
# internal-dependency allowlist — every internal import must match a row
core     → []
feature  → [core]
app      → [core, feature]
```

Anything not on a row fails. Contextual exceptions ("may import X if needed") do
not belong in an enforced contract unless the checker explicitly models them.

Many projects have no such contract, and that is fine — do not invent module
boundaries to have something to enforce.
