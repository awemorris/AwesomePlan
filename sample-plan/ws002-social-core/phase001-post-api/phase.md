# ws002p001: authorized post API

Last updated: 2026-08-25

WSID: `ws002`

Phase ID: `p001`

Combined ID: `ws002p001`
Status: ready after `ws001p001`

Parent: [WS002](../ws.md)

## Objective

Implement the smallest complete post creation and retrieval API using the
approved account model and campus-only visibility.

## Dependencies and fixed decisions

- `ws001p001` is complete and its active-member predicate is available.
- Posts have opaque IDs, author account ID, UTF-8 text body, visibility,
  creation time, update time, and deletion marker.
- Allowed visibility values are `campus` and `community`; this Phase implements
  `campus` only and rejects other values.
- The first feed is reverse chronological with `(created_at, id)` cursor order.
- Body size is 1–2,000 Unicode scalar values after line-ending normalization.

## Scope

- schema and migration for posts;
- create, get-by-ID, and campus-feed service/API paths;
- server-side active-member checks and response DTOs;
- cursor validation, fixed page maximum, and content-safe structured logs;
- focused contract, authorization, pagination, and concurrency tests.

## Non-goals

- communities, comments, reactions, edits, media, hashtags, search, ranking,
  moderation actions, or anonymous authorship;
- choosing how deleted content is retained.

## Work packages

- [ ] Add post migration with author reference and feed indexes.
- [ ] Implement normalized validation and transactional creation.
- [ ] Implement authorized retrieval and deterministic campus-feed pagination.
- [ ] Add HTTP contract and error mapping without leaking hidden records.
- [ ] Test limits, invalid cursors, authorization, stable ties, and concurrent inserts.

## Completion conditions

- Active members can create and retrieve valid campus posts.
- Ineligible, suspended, and unauthenticated callers receive the specified denial.
- Invalid or oversized bodies create no row.
- Pagination has no duplicates within a stable snapshot test and breaks timestamp ties by ID.
- Response and logs never expose issuer/subject values or internal authorization data.
- Focused migration, contract, authorization, and concurrency tests pass.

## Expected evidence

Record exact commands, test results, migration revision, changed files, and
known performance observations during execution.

## Interruption and resume record

Not started. If product behavior for deletion, anonymity, or ranking becomes
necessary to satisfy this bounded API, mark the item `uncleared`; do not invent
that policy inside the Queue.
