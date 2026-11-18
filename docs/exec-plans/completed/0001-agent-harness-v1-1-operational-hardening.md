# 0001 — Agent Harness V1.1 Operational Hardening

Status: completed 2026-11-18

Delivery: `commit+push` to `agent-harness-v1-1` for closure.

Review gate: [repository policy](../../../AGENTS.md#governance-for-this-repo).
Final review verdict: ACCEPT. The owner explicitly accepted H1–H10 on
2026-11-18.

Base:
9e8bc6babc4680129ce792602a8115d71d47370e

## Goal

Refine the generic agent harness using lessons learned from sustained
multi-step agent-driven implementation work.

Keep the existing V1 architecture and principles intact.

The change should improve operational reliability around:

- delivery/commit expectations;
- immutable review targets;
- project-configurable review gates;
- narrow follow-up reviews;
- sizing of large implementation steps;
- stable requirement references for long plans;
- verification/reporting claim audits.

No runtime, automation framework, package dependency, or project-specific
policy is introduced.

## Context

V1 has now been exercised on a substantial agent-driven project through
multiple architecture, implementation, verification, independent-review,
fix-pass, and owner-acceptance cycles.

The core model has held up well:

repository as source of truth;
risk-based governance;
execution plans for substantial work;
honest verification;
independent review;
explicit owner acceptance.

Operational gaps observed during real use:

1. The V1 author prompt emphasized "do not commit unless asked". It left room
   for an agent to finish implementation and overlook a requested commit or
   push.

2. High-risk independent review is materially stronger when performed against
   an immutable Base SHA → Head SHA rather than a moving worktree.

3. Different projects legitimately use different severity gates.
   For example, one project may require Blockers=0, while another requires
   Blockers=0 AND Important=0. The generic harness should support this without
   imposing one universal gate.

4. A narrow fix after a comprehensive review should normally receive a narrow
   follow-up review rather than an expensive complete re-review, provided the
   fix scope is demonstrably narrow and the previous review established the
   rest of the change.

5. Very large execution steps can contain several independent correctness
   protocols even when they form one product feature. Step sizing guidance
   should consider independently reviewable correctness boundaries, not file
   count alone.

6. Very long implementation prompts tend to duplicate the canonical execution
   plan. Large plans need stable requirement identifiers/anchors so prompts can
   reference the plan precisely instead of restating it.

7. Long-running work accumulates stale status/test-count/"planned vs
   implemented" claims. A final claims audit should be an explicit verification
   activity.

8. A verification command may fail transiently and pass on retry. Honest
   reporting should preserve both events and distinguish product/test failure
   from infrastructure/transient failure.

## Scope

Modify only existing generic harness documentation/templates/prompts unless one
small new document is clearly necessary.

Expected files:

- docs/WORKFLOW.md
- docs/REVIEW.md
- docs/VERIFICATION.md
- docs/HARNESS_PRINCIPLES.md
- prompts/implement-change.md
- prompts/review-change.md
- prompts/close-work.md
- templates/AGENTS.md
- templates/EXEC_PLAN.md
- README.md if its overview needs a narrow sync

Avoid changing docs/MODULES.md unless the work actually introduces a new
optional module. The intended changes should remain core workflow refinements,
not a new module family.

## Non-goals

- no CLI;
- no scripts;
- no package manager;
- no dependencies;
- no GitHub Actions;
- no MCP/Claude/Codex-specific workflow;
- no names, stages, commands, severity policy, or repository structure from the
  project that motivated this work in binding rules;
- no universal requirement that every project commit/push before review;
- no universal Blockers/Important threshold;
- no universal one-plan-at-a-time rule;
- no mandatory requirement IDs for small plans;
- no automated semantic diffing or claims scanner.

## Constraints

The harness remains:

- generic;
- stack-neutral;
- self-contained after copying into a project;
- plain Markdown;
- progressively disclosed;
- small enough to read and adopt selectively.

One topic has one authoritative owner document.
Prompts point to policy instead of duplicating long policy text.

Do not weaken existing V1 rules.

## Requirements

### H1 — Delivery contract

Define a small generic delivery vocabulary:

- `worktree`
- `commit`
- `commit+push`

A project may define a default.
A task or execution plan may explicitly override that default.

If delivery is `commit` or `commit+push`, the implementation task is not
complete until the requested delivery happened successfully.

The final author handoff must report, when applicable:

- base revision;
- final commit SHA;
- whether it was pushed;
- final `git status`.

If push was requested and failed, report failure; do not describe the work as
fully delivered.

The generic default remains conservative:
do not commit/push unless project/task policy requests it.

### H2 — Immutable review target

For high-risk work, document immutable revision review as the recommended
default when the project's delivery model permits it:

Base SHA → Head SHA.

The reviewer must confirm that the reviewed HEAD is the intended immutable
target and state the exact reviewed revision.

Local/staged/unstaged review remains supported for projects that choose it.

Do not make remote Git hosting mandatory.

### H3 — Project-configurable review gate

Separate finding severity from readiness policy.

Keep the generic finding levels:

Blocker
Important
Minor

But require a project using independent review to state its readiness gate,
for example:

- Blockers = 0
or
- Blockers = 0 and Important = 0
or another explicit local policy.

The reviewer follows the project's gate.

Do not encode one universal threshold into the generic harness.

### H4 — Narrow follow-up review

Add a documented follow-up-review mode.

It is appropriate when:

- a previous comprehensive review exists;
- remaining findings are explicit;
- the fix commit/diff is narrow;
- unrelated code was not changed.

The follow-up reviewer checks:

- the original findings;
- the exact fix diff;
- regressions caused by that diff;
- required verification.

It does not mechanically repeat the entire original review.

If the fix scope expanded materially, return to a comprehensive review.

### H5 — Correctness-boundary task sizing

Add guidance for large implementation work:

Consider splitting a step when it contains multiple independently
committable/reviewable correctness protocols or failure domains.

Examples of signals:

- separate immutable commit protocols;
- independent state machines;
- distinct external side-effect boundaries;
- independently testable security/integrity contracts;
- separate rollback/resume semantics.

File count alone remains explicitly NOT a sizing criterion.

Do not require arbitrary numeric thresholds.

### H6 — Stable requirement references

Extend the execution-plan template:

For a large plan, requirements MAY receive stable IDs such as:

R1, R2, ...
or
S6-R1, S6-R2, ...

Prompts/reviews can then cite those IDs instead of copying large sections.

Rules:

- IDs are stable once implementation starts;
- changing requirement meaning updates the plan text, not the identifier;
- removed/superseded requirements are recorded, not silently renumbered;
- small plans do not need IDs.

Do not introduce a second requirements database.

The execution plan remains canonical.

### H7 — Claims audit

Before final implementation handoff and before closure of substantial work,
perform a documentation/claims consistency pass appropriate to the project.

Check statements such as:

- planned vs implemented;
- current/next stage;
- test counts;
- command names;
- file existence;
- workflow vs job terminology;
- dependency claims;
- "not started" / "complete";
- review status.

This is an inspection activity, not necessarily a new script.

Do not require exhaustive repo-wide rewriting.

### H8 — Verification retry reporting

Clarify honest verification:

If a verification command fails and later passes on retry, report both:

- initial failure;
- reason/evidence available;
- targeted investigation if performed;
- successful retry.

Do not rewrite history as simply "PASS".

Distinguish, when evidence supports it:

- implementation/test failure;
- deterministic test failure;
- transient external/infrastructure failure;
- timeout/resource failure.

Do not claim a failure was transient without evidence.

### H9 — Author handoff contract

For substantial work, the author report should identify:

- implemented scope;
- known deviations/open points;
- actual verification results;
- delivery state;
- exact revision when available;
- next lifecycle step.

Do not require long prose or a universal fixed template.

### H10 — Reviewer output

Update the generic review prompt so readiness uses the local project gate.

When reviewing an immutable target, include:

- reviewed HEAD;
- diff scope;
- verification state.

For narrow follow-up review, explicitly identify the original finding(s) being
rechecked.

## Implementation steps

1. Create this execution plan under:
   `docs/exec-plans/active/0001-agent-harness-v1-1-operational-hardening.md`.

2. Update `docs/WORKFLOW.md`:
   - delivery contract;
   - immutable-review recommendation;
   - project-defined review gate;
   - correctness-boundary sizing;
   - author handoff expectations.

3. Update `docs/REVIEW.md`:
   - immutable revision mode;
   - local readiness gate;
   - narrow follow-up-review protocol.

4. Update `docs/VERIFICATION.md`:
   - claims audit;
   - retry/failure reporting semantics.

5. Update `templates/EXEC_PLAN.md`:
   - optional Delivery field;
   - optional Review gate reference;
   - optional stable requirement IDs for large plans;
   - final claims-audit reminder.

6. Update `templates/AGENTS.md`:
   - project chooses delivery default;
   - project states its review gate when review module is adopted;
   - link/process wording remains concise.

7. Update prompts:
   - `implement-change.md` respects explicit task/project delivery mode;
   - `review-change.md` supports Base/Head and narrow follow-up;
   - `close-work.md` preserves delivery/acceptance semantics and exact final
     revision when applicable.

8. Update `docs/HARNESS_PRINCIPLES.md` only for genuinely principle-level
   concepts:
   - reviewable immutable handoff;
   - canonical-plan references over prompt duplication.
   Do not copy procedural detail there.

9. Update README only if necessary to keep its overview truthful.

10. Run full documentation verification.

11. Independent review.

12. Fix findings and run narrow follow-up review where appropriate.

13. Explicit owner acceptance.

14. Move plan to completed and perform closure commit/push only if owner
    requests that delivery mode.

## Acceptance criteria

- Existing V1 principles remain intact.
- No project/vendor/stack-specific binding rule is introduced.
- Delivery mode is explicit and cannot conflict with the generic
  "do not commit unless asked" rule.
- High-risk immutable Base→Head review is documented as recommended, not
  universally mandatory.
- Review readiness is explicitly project-configurable.
- Narrow follow-up review has finite eligibility rules.
- Step sizing is based on correctness boundaries, not number of files.
- Long plans can use stable requirement IDs without forcing them on small plans.
- Honest verification preserves failed-first/passed-on-retry history.
- Claims audit is defined without requiring new automation.
- Prompts remain short role briefs and do not duplicate long policies.
- No runtime/dependency is added.
- All relative Markdown links resolve.
- No secrets or project-specific assumptions.
- `git diff --check` is clean.
- Full diff manually reviewed.

## Verification

Run and record actual results:

- `git status --short`
- `git diff --check`
- full `git diff` review
- relative Markdown link validation for all Markdown files
- secret-pattern scan
- search for project-specific leakage, including names/vendors/commands from
  the project that motivated the lessons
- search for contradictory commit/push rules
- search for contradictory readiness-gate rules
- search for duplicated authoritative policy text across docs/prompts/templates
- confirm no runtime files/dependencies/package manifests were introduced
- verify every changed internal Markdown link resolves

For every failed check that is retried, record both the failure and the retry.

### Author verification

- At author handoff, `git status --short` showed 14 modified Markdown files
  and one new plan. Delivery was in the worktree, with HEAD at the plan base.
- `git diff --check` passed on the ordinary worktree diff and on the full
  diff including the new plan, using a temporary index. An initial
  `git diff --no-index --check` against the new plan returned 1 with no
  whitespace diagnostics because the files differed. The temporary-index
  check returned 0.
- Full diff reviewed, including the new plan. H1–H10 were checked against the
  policy text and the corresponding prompt and template guidance.
- Relative link validation passed for 78 local links across 22 Markdown
  files, including 19 heading fragments. This covered all 51 local links in
  changed files.
- The secret-pattern scan returned zero candidates across 22 files. The
  source-project name, vendor, workflow, and command search found no leaked
  binding rules. Vendor mentions are optional adapter examples or non-goals.
- Searches and comparison found consistent delivery and readiness rules.
  The workflow, review, and verification documents own their respective
  rules. Prompts and templates point to those policies.
- All 15 changed files are Markdown. The file inventory showed no scripts,
  workflow configuration, runtime, dependencies, or package manifests added.
- The handoff claims audit checked the active status, completed scope,
  command names, paths, dependency claims, and review and acceptance state.
  The next step at handoff was independent review.

### Closure verification

- The claims audit reconciled the completed status, both review outcomes,
  explicit owner acceptance, and the archived plan location.
- The link check passed for 86 relative links across 22 Markdown files,
  including 21 heading fragments, after the plan was moved.
- Inspection and a search for common credential patterns in the 15 staged
  documents found no potential secrets.
- `git diff --check` and `git diff --cached --check` passed. The staged scope
  contained only the 15 Markdown files for V1.1. Build and test checks did
  not apply to this documentation-only repository.

## Progress

- V1 baseline:
  `9e8bc6babc4680129ce792602a8115d71d47370e`.
- Plan drafted from post-V1 real-world usage.
- Implemented H1–H10 in a dedicated worktree. Policy locations:
  - H1, H5, H6, H9 — [workflow](../../WORKFLOW.md).
  - H2, H3, H4, H10 — [independent review](../../REVIEW.md).
  - H7, H8 — [verification](../../VERIFICATION.md).
- The comprehensive independent review found zero Blockers and three Important
  findings. The local gate passed, and the reviewer recommended FIX REQUIRED.
  The findings covered closure commit isolation (F1), closure secret checks
  (F2), and the link to execution plans after the last active plan is archived
  (F3).
- The fix pass addressed F1–F3 in `AGENTS.md`, `docs/WORKFLOW.md`,
  `docs/VERIFICATION.md`, and `prompts/close-work.md`.
- The narrow follow-up compared the exact fix-pass patch against the reviewed
  worktree. F1, F2, and F3 passed. The reviewer confirmed the four-file scope
  and verified 34 relative links before and after a simulated archive move.
  Final verdict: ACCEPT, with zero open Blockers and Important findings.
- On 2026-11-18, the owner explicitly accepted H1–H10 and requested a single
  implementation and closure commit pushed to `agent-harness-v1-1`.

## Result

V1.1 implemented H1–H10 and passed independent review after the three
follow-up fixes. The owner accepted the result on 2026-11-18.

- [Workflow](../../WORKFLOW.md) and [principles](../../HARNESS_PRINCIPLES.md)
- [Review](../../REVIEW.md) and [verification](../../VERIFICATION.md)
- [Role briefs](../../../prompts/README.md) and [project templates](../../../templates/README.md)
