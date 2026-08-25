# WS001: identity and access

Last updated: 2026-08-25

WSID: `ws001`

Status: planned

Parent: [master plan](../master.md)

Resume point: execute `ws001p001` after Queue approval.

## Objective

Provide university-backed authentication and a minimal account lifecycle that
other Workstreams can trust for identity, eligibility, roles, and privacy-safe
ownership references.

## Scope

- OpenID Connect login, callback, logout, and session lifecycle;
- stable internal account IDs mapped to university subject identifiers;
- eligibility, suspension, terms acceptance, and minimal profiles;
- role claims needed for ordinary users and moderators;
- authorization middleware and audit-safe security events.

## Non-goals

- local passwords, social login, or public registration;
- choosing retention policy;
- assigning university disciplinary authority;
- profile discovery and social graphs.

## Dependencies

- University identity-team test issuer metadata and test accounts are required
  for `phase002`; `phase001` uses a local deterministic issuer fixture.
- University privacy approval is required before adding any profile fields not
  listed in the Master Book.

## Phase registry

| Phase | Status | Goal |
| --- | --- | --- |
| [`ws001p001`](phase001-account-model/phase.md) | ready | Establish the account model and authorization contracts without live SSO. |
| `ws001p002` | planned | Integrate the university OpenID Connect test tenant and session lifecycle. |
| `ws001p003` | proposed | Add terms acceptance, suspension synchronization, and admin recovery procedures. |

## Completion conditions

- Eligible identities authenticate through the approved issuer and map to one
  stable internal account each.
- Ineligible or suspended identities cannot create authenticated sessions.
- Authorization uses internal account/role state rather than client assertions.
- Sessions can be revoked, security events are auditable, and sensitive tokens
  or profile data do not enter logs.
- Identity and session threat-model acceptance cases pass.

## Reconsideration boundaries

Stop and return to planning if the university issuer lacks stable subject IDs,
eligibility cannot be expressed without storing additional sensitive data, or
role claims conflict with the approved moderation model.
