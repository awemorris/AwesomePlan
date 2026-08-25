# Campus Square master plan

Last updated: 2026-08-25

Status: active planning

## 1. Purpose

Campus Square is a private Web application where current students, faculty,
and staff can discover campus communities, publish posts, discuss university
life, and report harmful content. This Master Book is the strategic source of
truth; implementation detail belongs in W and P Books.

## 2. Scope

In scope:

- university SSO and eligibility enforcement;
- user profiles with privacy controls;
- campus communities, membership, posts, comments, reactions, and feeds;
- search and notifications;
- reporting, moderator review, appeals, and auditable actions;
- responsive Web access, accessibility, observability, backup, and recovery.

Out of scope for the initial product:

- public or cross-university federation;
- advertising, payments, and marketplace transactions;
- direct messaging and end-to-end encryption;
- native mobile applications;
- automated disciplinary decisions.

## 3. Final goal

The university can operate Campus Square for its eligible population with
documented privacy and moderation controls, accessible core workflows, and
reproducible security, performance, backup, and recovery evidence.

## 4. Constraints and fixed product decisions

- Sign-in uses the university OpenID Connect provider; local passwords are not
  stored.
- Access is limited to active university identities. Suspension and alumni
  policy are supplied by the identity system.
- The initial home and community feeds use reverse chronological ordering.
- Posts are campus-visible or community-visible; public Internet visibility is
  excluded.
- Moderators may hide content but permanent disciplinary decisions remain with
  authorized university staff.
- Accessibility target: WCAG 2.2 AA for supported core workflows.
- Security and privacy logs must avoid post bodies and unnecessary personal
  data.

## 5. Milestone Goals

| ID | Observable state |
| --- | --- |
| `MG001` | Eligible test users sign in through SSO, accept terms, and control a minimal profile. |
| `MG002` | Pilot users create communities and exchange posts, comments, and reactions through chronological feeds. |
| `MG003` | Reports move through an auditable moderator workflow with notification and appeal paths. |
| `MG004` | Search, notifications, accessibility, security, performance, backup, and recovery gates pass for a limited campus pilot. |
| `MG005` | Production rollout and operations meet the university's approved service and governance criteria. |

## 6. Workstream registry

| WSID | Workstream | Status | Milestones | Resume point | W Book |
| --- | --- | --- | --- | --- | --- |
| `ws001` | Identity and access | planned | MG001, MG004 | Implement the approved account domain model | [WS001](ws001-identity-access/ws.md) |
| `ws002` | Social core | planned | MG002, MG004 | Implement post creation and retrieval after the account model | [WS002](ws002-social-core/ws.md) |
| `ws003` | Trust and safety | planned | MG003, MG005 | Implement report intake against the fixed taxonomy | [WS003](ws003-trust-safety/ws.md) |
| `ws004` | Discovery and notifications | proposed | MG002, MG004 | Refine search and delivery semantics after the social model stabilizes | Not yet detailed |
| `ws005` | Web experience and accessibility | proposed | MG001–MG004 | Define shared UI foundations with the first vertical slice | Not yet detailed |
| `ws006` | Platform, security, and operations | proposed | MG004, MG005 | Refine deployment and SLO Phases before pilot infrastructure work | Not yet detailed |

## 7. Dependency map

```text
WS001 identity and account model
  +-- WS002 social ownership and visibility
  |     +-- WS004 search and notifications
  |     +-- WS005 accessible Web workflows
  +-- WS003 reporter/moderator identity and audit

WS006 security and operations supports every production-facing Workstream.
```

## 8. Known human decision points

These remain planning inputs and are not eligible for the current Queue:

- whether anonymous or pseudonymous posting is allowed;
- retention periods for deleted content, reports, appeals, and audit events;
- which university roles may create official communities;
- whether automated ranking or automated moderation will ever be introduced;
- production SLOs and the final pilot population.

The relevant W/P Books must be updated after each decision. A Queue must not
embed policy-making inside implementation work.
