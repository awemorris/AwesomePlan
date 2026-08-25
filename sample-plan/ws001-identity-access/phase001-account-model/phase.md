# ws001p001: account domain model

Last updated: 2026-08-25

WSID: `ws001`

Phase ID: `p001`

Combined ID: `ws001p001`
Status: ready

Parent: [WS001](../ws.md)

## Objective

Implement the persistence model and service contracts for campus accounts
before connecting the live university identity provider.

## Baseline and fixed decisions

- The application skeleton, database migration runner, and automated test
  command already exist.
- The internal account ID is an opaque UUID and never the university subject.
- Store issuer, subject, eligibility state, display name, affiliation, terms
  timestamp, creation time, and update time.
- Display name and affiliation are the only profile fields in this Phase.
- The `(issuer, subject)` pair is unique and never exposed in public APIs.
- Logs may contain the internal account ID but not tokens or the subject value.

## Scope

- account schema and migration;
- domain types for eligibility and application role;
- repository create/find/update operations;
- authorization predicates for active member and moderator;
- deterministic issuer fixture and unit/integration tests.

## Non-goals

- HTTP login/callback routes and real OpenID Connect traffic;
- UI, terms pages, profile search, alumni policy, and data retention;
- changing the approved profile fields or role taxonomy.

## Work packages

- [ ] Add forward and rollback migrations with declared constraints and indexes.
- [ ] Implement bounded domain types and repository operations.
- [ ] Implement authorization predicates that reject ineligible or suspended accounts.
- [ ] Add fixture-based happy-path, duplicate-identity, invalid-state, and log-redaction tests.
- [ ] Run the repository's focused formatting, type, migration, and test gates.

## Completion conditions

- Migration up/down/up succeeds against a clean test database.
- Concurrent creation cannot produce two accounts for one `(issuer, subject)`.
- Invalid eligibility/role states fail before persistence.
- Active-member and moderator predicates match the fixed role table.
- Tests demonstrate that subject identifiers and tokens are absent from logs.
- No production route or live identity-provider configuration changes.

## Expected evidence

Record exact commands, passing test names, migration revision, changed files,
and any skipped gate here during execution.

## Interruption and resume record

Not started. If the existing database cannot enforce the required uniqueness or
rollback safely, mark the Phase `uncleared`, record the database constraint,
and request an architecture decision before changing storage technology.
