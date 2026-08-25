# WS003: trust and safety

Last updated: 2026-08-25

WSID: `ws003`

Status: planned

Parent: [master plan](../master.md)

Resume point: execute `ws003p001` after `ws001p001` completes and Queue approval is active.

## Objective

Provide bounded, auditable reporting and review workflows without allowing the
application to make automatic disciplinary decisions.

## Scope

- reports against supported content and accounts;
- fixed report categories, reporter acknowledgements, and duplicate handling;
- moderator queues, case notes, hide/restore actions, and audit events;
- user notification and appeal handoff;
- least-privilege access and operational metrics without sensitive content.

## Non-goals

- defining university disciplinary policy;
- automated sanctions, content scoring, or predictive risk classification;
- law-enforcement disclosure workflow;
- deciding retention periods.

## Dependencies

- WS001 supplies stable reporter and moderator identities.
- WS002 supplies stable content IDs before content-target review is completed.
- University policy owners approve action categories, retention, appeal rules,
  and moderator roles before their dependent Phases become Queue-eligible.

## Phase registry

| Phase | Status | Goal |
| --- | --- | --- |
| [`ws003p001`](phase001-report-intake/phase.md) | ready after WS001 P001 | Implement report intake and acknowledgement without moderator decisions. |
| `ws003p002` | proposed | Add moderator case queue and audited hide/restore actions after policy approval. |
| `ws003p003` | proposed | Add notifications and appeal handoff after appeal policy approval. |
| `ws003p004` | proposed | Validate abuse resistance, operational playbooks, and access reviews. |

## Completion conditions

- Authorized users can report supported targets without exposing reporter identity.
- Moderators process cases through approved states with immutable audit evidence.
- Actions are least-privilege, reviewable, and reversible where policy requires.
- Notifications and appeals follow approved rules.
- Abuse, security, privacy, and operational acceptance suites pass.

## Reconsideration boundaries

Stop before implementing any sanction, retention behavior, report disclosure,
or automated classification that lacks an explicit university policy decision.
