# ws003p001: report intake

Last updated: 2026-08-25

WSID: `ws003`

Phase ID: `p001`

Combined ID: `ws003p001`
Status: ready after `ws001p001`

Parent: [WS003](../ws.md)

## Objective

Implement authenticated report submission and acknowledgement using the
approved taxonomy, without introducing moderator judgment or disciplinary
behavior.

## Dependencies and fixed decisions

- `ws001p001` supplies account IDs and the active-member predicate.
- Supported target types are `account` and `post`; target existence is checked
  through a boundary interface so WS002 may be substituted by a fixture.
- Categories are `harassment`, `threat`, `hate`, `privacy`, `spam`, and `other`.
- Optional detail is limited to 1,000 Unicode scalar values.
- A reporter receives an opaque receipt ID, never another reporter's identity
  or report count.

## Scope

- report schema, target reference, category, optional detail, and timestamps;
- submit service/API with authorization, validation, rate limit, and receipt;
- target-lookup fixture for account and post targets;
- security-safe logs and focused privacy/abuse tests.

## Non-goals

- moderator UI, case assignment, sanctions, hide/restore actions, appeals;
- retention/deletion jobs, reporter disclosure, category changes, or automated
  prioritization.

## Work packages

- [ ] Add report migration with constraints and indexes.
- [ ] Implement target boundary and deterministic fixtures.
- [ ] Implement validation, rate limiting, atomic persistence, and receipt response.
- [ ] Add tests for invalid targets/categories, suspended reporters, duplicates,
  rate limits, concurrent submissions, and log redaction.
- [ ] Run focused formatting, type, migration, security, and test gates.

## Completion conditions

- Active members can submit a valid report and receive an opaque receipt.
- Unsupported or nonexistent targets and invalid categories create no record.
- Rate limiting has deterministic tests and does not reveal prior reports.
- API responses and logs do not disclose reporter identity, report counts, or detail text.
- Duplicate submissions remain independently auditable without changing policy.
- Focused migration, privacy, authorization, and abuse-resistance tests pass.

## Expected evidence

Record exact commands, passing tests, migration revision, changed files, and
any unrun security gate during execution.

## Interruption and resume record

Not started. If implementation requires a decision about retention, moderator
priority, sanctions, or reporter disclosure, mark the Phase `uncleared`, record
the exact decision, and leave it outside implementation until policy owners act.
