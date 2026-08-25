# Campus Square Queue Book: q001 foundation slice

Last updated: 2026-08-25

Queue ID: `q001`

Queue status: proposed

Timebox: one implementation cycle

Parent: [master plan](master.md)

## 1. Purpose

This Queue selects a small foundation slice whose product and architecture
decisions are already recorded in M/W/P. The user must approve this Queue before
implementation begins.

## 2. Authorization boundary

The Queue authorizes only the three referenced Phases and only within their
declared scopes. Each item can be implemented and verified without a new human
product, policy, risk, or major architecture decision.

Not authorized: anonymous posting, retention policy, official-community roles,
ranking, automated moderation, production deployment, and any later Phase.

If a selected item unexpectedly requires one of those decisions, mark it
`uncleared`, record the decision and resume condition in its P Book, and proceed
to an independent item where possible.

## 3. Execution registry

| Order | Queue item | Source | Status | Why it is decision-cleared |
| --- | --- | --- | --- | --- |
| 1 | `ws001p001` account domain model | [P Book](ws001-identity-access/phase001-account-model/phase.md) | pending | Identity source, eligibility boundary, fields, and lifecycle semantics are fixed. |
| 2 | `ws002p001` post API | [P Book](ws002-social-core/phase001-post-api/phase.md) | pending | Visibility, initial feed order, limits, and authorization rules are fixed; it depends on item 1. |
| 3 | `ws003p001` report intake | [P Book](ws003-trust-safety/phase001-report-intake/phase.md) | pending | Report taxonomy and intake behavior are fixed; it depends on item 1 but not item 2. |

## 4. Execution rules

1. Mark the Queue `active`, then mark one eligible item `in-progress`.
2. Follow the referenced P Book rather than expanding this manifest.
3. Run each Phase's acceptance checks and record evidence in that P Book.
4. Mark the item `completed` only when its completion conditions pass.
5. Mark it `uncleared` when safe progress requires an unresolved human decision
   or unavailable prerequisite; record findings and a concrete resume condition.
6. Synchronize the relevant W Book and Master Book after each terminal result.

Items 2 and 3 may proceed in either order after item 1 is complete. Failure of
item 2 does not block item 3 unless the recorded cause also invalidates the
shared account model.

## 5. Update record

| Queue item | Status | Last verified result | Blocker / decision needed | Next action |
| --- | --- | --- | --- | --- |
| `ws001p001` | pending | Plan reviewed | None known | Implement account model and tests |
| `ws002p001` | pending | Plan reviewed | Waits for `ws001p001` | Start after account model passes |
| `ws003p001` | pending | Plan reviewed | Waits for `ws001p001` | Start after account model passes |

## 6. Closure checklist

- [ ] Every Queue item is `completed` or `uncleared`.
- [ ] Each terminal item has acceptance evidence or a documented resume condition.
- [ ] Affected P, W, and M Books agree with actual results.
- [ ] No unapproved policy or scope decision was made during execution.
- [ ] Queue status is `finished`.

A finished Queue may contain `uncleared` items.
