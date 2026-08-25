# WS002: social core

Last updated: 2026-08-25

WSID: `ws002`

Status: planned

Parent: [master plan](../master.md)

Resume point: execute `ws002p001` after `ws001p001` completes and Queue approval is active.

## Objective

Deliver the campus community, posting, conversation, reaction, and
reverse-chronological feed capabilities required for the pilot.

## Scope

- communities and membership;
- posts, comments, reactions, and deletion markers;
- campus and community visibility authorization;
- reverse-chronological home and community feeds;
- stable pagination, abuse-resistant limits, and core social API contracts.

## Non-goals

- anonymous posting, direct messages, advertising, and public sharing;
- ranking or recommendation algorithms;
- search and notification delivery, which belong to WS004;
- moderator case handling, which belongs to WS003.

## Dependencies

- WS001 supplies stable account IDs and active-member authorization.
- WS003 consumes stable content IDs and deletion state.
- WS005 consumes the API contracts for the accessible Web interface.

## Phase registry

| Phase | Status | Goal |
| --- | --- | --- |
| [`ws002p001`](phase001-post-api/phase.md) | ready after WS001 P001 | Implement authorized post creation and retrieval contracts. |
| `ws002p002` | planned | Implement communities, membership, and community feeds. |
| `ws002p003` | planned | Add comments, reactions, deletion markers, and pagination consistency. |
| `ws002p004` | proposed | Prove pilot-scale performance and concurrency behavior. |

## Completion conditions

- Eligible members can use communities and content according to visibility and
  membership rules.
- Feeds are deterministic under documented pagination semantics.
- Authorization is enforced server-side on every read and mutation path.
- Deletes, moderation hides, and author state changes have defined behavior.
- API, concurrency, accessibility-supporting metadata, and load gates pass.

## Reconsideration boundaries

Return to planning before adding anonymous identity, ranked feeds, cross-campus
visibility, new content types, or a consistency model that changes user-visible
ordering guarantees.
