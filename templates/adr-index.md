# Architecture Decision Records

> Module: adr. This is the project's **one authoritative statement** of the ADR
> modification policy, plus the index. Link here from elsewhere in the project;
> do not restate the policy.
>
> Delete guidance lines before use.

Each ADR records one decision already made by the owner: Context, Decision,
Consequences. Template: `<path to your ADR template>`.

## Modification policy

Once an ADR is **Accepted**, its **decision semantics are immutable**.

- **Allowed in place:** typo / formatting / link fixes; factual metadata
  corrections; wording clarification that does **not** change the meaning; a
  dated `Clarification YYYY-MM-DD` note.
- **Not allowed in place:** changing the choice; materially widening or narrowing
  it; swapping a technology or pattern; changing a contract's semantics.
- **Any semantic change requires a new ADR that supersedes the old one** — add
  the new ADR and mark the old one `Superseded by NNNN`.

## Index

| ADR | Title | Status |
| --- | --- | --- |
| <NNNN> | <title> | <Proposed / Accepted / Superseded by NNNN> |
