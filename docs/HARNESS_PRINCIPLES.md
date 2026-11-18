# Harness principles

The reusable ideas behind an agent-driven repository. Each was learned the
expensive way — a mostly-autonomous agent going wrong, or a review catching an
ambiguity — and each has a concrete, checkable form.

Principles are split into a **core** set (worth applying to any repository, even
a one-file library) and an **additional** set (adopt the ones that fit — see
[MODULES.md](MODULES.md)). Nothing here is weakened by being "additional"; it is
just not forced on projects that gain nothing from it.

---

## Core principles

### C1. Repository over prompt

**Context that recurs belongs in the repository, not in ever-growing task
prompts.** If an agent needs a fact to do future work, that fact must be
discoverable by reading the repo. Off-repository conversation is not a
dependency.

- Accepted decisions, current constraints, invariants, verifiable requirements,
  and confirmed dead-ends are written down where the project keeps such things.
- "We discussed this in chat" is not a source of truth.
- When the source of truth moves, documentation moves in the *same* change.
- For planned work, refer to the canonical plan when briefing an author or
  reviewer. Stable references keep long requirements usable across sessions.

### C2. Progressive disclosure

**Root instructions route; they do not contain everything.** The root entrypoint
(`AGENTS.md` by convention) is a map: what the project is, where each kind of
information lives, the change workflow, the hard invariants, the verification
rules. Detail lives in linked documents.

- The root file stays short enough to read every session.
- **One document owns each topic.** A rule is stated once and linked, never
  copied into several files — copies drift and then contradict.

### C3. Honest verification

**A green check must correspond to verification that exists and actually ran.**

- Never report a check as passed unless it was executed and observed to pass. If
  it was not run, say so.
- A verification command must not contain no-op steps, always-passing dummy
  tests, empty suites, or "pass with no tests" flags used to look complete.
- A capability that does not exist yet is simply **not in the command yet**. That
  is the correct state, not a gap to paper over.

*(The core change-workflow habits — read context first, inspect Git state, make
the smallest coherent change, do not invent missing requirements, avoid unrelated
cleanup, review your own diff — live in [WORKFLOW.md](WORKFLOW.md).)*

---

## Additional principles

### A1. Executable rules

Prefer the chain **human decision → documented invariant → mechanical check**,
where practical. Write invariants so a check *could* enforce them, even before
the check exists. "Where practical" is real — some invariants stay prose — but a
rule meant to be enforced is written in enforceable shape (see A3). A new check
must correspond to a real stated invariant, not the reverse.

### A2. Stage-aware verification

The repository-level verification command means *everything implemented and
applicable to the current stage* — not everything the finished system will
check. Each stage adds real checks for what it actually built. The target full
hierarchy may be documented as a labelled future shape. See
[VERIFICATION.md](VERIFICATION.md).

### A3. Finite, enforceable contracts

If a rule is meant for mechanical enforcement, express it as a **finite,
unambiguous contract** — an exhaustive allow/deny form, not contextual wording
like "if required" or "where genuinely needed" — unless the checker explicitly
models the exception. A phrase a reviewer or script cannot evaluate the same way
every time is a bug in the rule: give it the finite form, or move it into
advisory prose. Contradictory statements of one contract in different documents
are a blocker.

### A4. Independent review

For high-risk / substantial changes, separate the **author** role from the
**reviewer** role where practical. The reviewer inspects the actual repository
state and diff and reports findings and readiness under the local review
policy. See [REVIEW.md](REVIEW.md) and the
[risk model](WORKFLOW.md#governance-model).

An immutable handoff, when the delivery model supports it, gives the author
and reviewer the same reproducible change to inspect.

---

## Where these came from

Distilled from bootstrapping one project's agent harness, which took several
independent-review rounds before it was accepted. The recurring failure modes,
generalized:

| Failure observed | Principle |
| --- | --- |
| The same rule stated differently in two files, so agents got two answers | C2 — one canonical statement, linked |
| An invariant an automated check could not express ("depend on X only if genuinely required") | A3 — finite contracts |
| A verification command that demanded checks for components not built yet | A2 — stage-aware verification |
| Temptation to add empty/passing test stubs so the command "passes" | C3 — honest verification |
| A plan asserting a change had been made when the file did not contain it | C3 — claims must match repo state |
| A plan treated as done on the author's say-so | A4 + [owner acceptance](WORKFLOW.md#owner-acceptance) |
| Task prompts growing to re-explain the same architecture each time | C1 — repository over prompt |
| A root instruction file trying to hold every detail | C2 — progressive disclosure |
