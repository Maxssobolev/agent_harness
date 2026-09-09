# Workflow and governance

The generic working agreement for an agent-driven repository. A project adopts
this by **copying the parts it selects into its own repository** and adapting
them — not by linking back here. Projects may tighten *or deliberately simplify*
these defaults, provided the chosen policy is written down locally.

---

## Core change workflow (every project)

Applies to any repository, from a one-file library up.

1. **Read the relevant repository context first** — the root entrypoint, the
   documents it links that apply, any active plan, and the neighbouring code. Do
   not start from memory of a past conversation.
2. **Inspect version-control state** — in a Git repository, `git status` and the
   current diff before making changes.
3. **Make the smallest coherent change** that satisfies the task. No unrelated
   cleanup or refactoring in the same change.
4. **Do not invent missing requirements.** If a requirement is absent, record it
   as an open question and ask — do not guess and proceed.
5. **Keep documentation and reality in sync** in the same change.
6. **Run the checks** the task or the project's verification contract specifies
   (see [VERIFICATION.md](VERIFICATION.md)). Honest verification (C3) is core.
7. **Review the whole diff yourself** before reporting.
8. **Report** the files you changed and the *actual* results of the checks you
   ran.
9. **Do not commit or push** unless the owner/maintainer asks.

---

## Governance model

How much process a change gets is decided by **risk**, not by how many files it
touches. *Multiple files alone do not make a change substantial.*

Assess: risk of harm, ambiguity, architectural breadth, reversibility,
external/system impact, and expected duration/complexity.

### Low risk

Local, reversible, well-understood, no architectural or external impact.

> implement → targeted verification → review your own diff

### Medium risk

Some ambiguity or breadth; still reversible; limited blast radius.

> optional short plan → implement → verification → review appropriate to project
> policy (self-review, a second pair of eyes, or independent review)

### High risk / substantial

Hard to reverse, architecturally broad, security/data/system impact, or a
contract change.

> execution plan → implement → verification → **independent review where project
> policy requires it** → **explicit owner/maintainer acceptance where
> configured**

Independent review ([REVIEW.md](REVIEW.md)) and the
[owner-acceptance gate](#owner-acceptance) are the **recommended defaults for
high-risk agent-driven work**. They are project-configurable: a small
single-owner project may fold "reviewer" and "owner" into one person; a
regulated or multi-team project may require both plus more. Whatever a project
chooses, it states it in its own workflow doc.

---

## Execution plans

*(Module — adopt when the project runs high-risk or multi-session work. A tiny
project may never need one.)*

An execution plan is the working document for one coherent piece of work:
written before it starts, kept current during it, finalized with the real
result.

### Sections

Mandatory: **Goal**, **Scope**, **Acceptance criteria**, **Verification** (with
real results once run), **Progress** (a running log). Add **Context**,
**Non-goals**, **Constraints**, **Implementation steps**, **Decisions made**, and
**Problems / failed approaches** when they carry real information — omit empty
headings. Template: [templates/EXEC_PLAN.md](../templates/EXEC_PLAN.md).

### Lifecycle

```text
draft ─▶ in progress ─▶ (implement + verify + review per policy)
                     ─▶ (owner acceptance, if configured) ─▶ completed
```

A completed plan is retained as the record of that work (this is where "what was
done" history lives — not in `PROJECT_STATUS`).

### Numbering and concurrency are project policy

There is **no universal `WIP=1`** and **no universal single plan stream**.

- A small single-owner project may reasonably keep one active plan at a time and
  a single sequential `NNNN-slug` series. Recommended, not required.
- A monorepo or multi-team project may use scoped IDs, team/component prefixes,
  multiple concurrent active plans, or another local convention.

The project documents whichever it uses.

---

## Owner acceptance

*(Module — the explicit sign-off gate. Configure it for high-risk work; a
solo project may treat "the maintainer merges it" as acceptance.)*

Where configured: a plan or high-risk change **closes only after the
owner/maintainer explicitly accepts the result** — an approving review is
necessary but not sufficient, and the author's belief that it is done never
closes it. Closure housekeeping: [prompts/close-work.md](../prompts/close-work.md).

---

## ADR modification policy

*(Module — applies only if the project uses ADRs.)*

An Architecture Decision Record captures a decision the owner has already made
(Context, Decision, Consequences). The governing rule: **once an ADR is
Accepted, its decision semantics are immutable — any semantic change is a new ADR
that supersedes the old one.** Only non-semantic edits (typo / format / link
fixes, factual metadata, dated clarifications) are allowed in place.

The exact, adoptable wording lives in one place: the adr module's index template,
[templates/adr-index.md](../templates/adr-index.md). A project copies it into its
own ADR index and that becomes the project's single home for the policy.

---

## Documentation rules (core)

- One document owns each topic; link instead of duplicating.
- A project-status document is a **current-state snapshot**, not a cumulative
  history — Git history, completed plans, and any changelog hold the history.
- Record only decisions already made by the owner. List open questions; do not
  resolve them on the owner's behalf.
- Never put secrets, credentials, tokens, or connection strings in the
  repository.
