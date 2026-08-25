# Sample plan: Campus Square

This directory is a worked MWP-Q example for **Campus Square**, a fictional
university-only social-networking Web application. The example is intentionally
larger than a tutorial application: it includes institutional identity,
community posting, moderation, privacy, operations, and staged delivery.

The sample demonstrates the abstraction boundary between the Books:

- [master.md](master.md) defines the product direction, milestones, and full
  Workstream registry.
- Each `ws.md` defines one outcome and decomposes it into Phases.
- Each `phase.md` makes near-term work executable and verifiable.
- [queue.md](queue.md) selects only the current decision-cleared work. It is not
  a backlog and does not authorize every planned Phase.

```text
sample-plan/
├── master.md
├── queue.md
├── ws001-identity-access/
│   ├── ws.md
│   └── phase001-account-model/phase.md
├── ws002-social-core/
│   ├── ws.md
│   └── phase001-post-api/phase.md
└── ws003-trust-safety/
    ├── ws.md
    └── phase001-report-intake/phase.md
```

Assume the product choices in the sample—university SSO, campus-only access,
chronological feeds for the first release, and the report categories—have
already been approved by the fictional university. Open questions such as
anonymous posting and automated moderation remain outside the Queue because
they still require human policy decisions.

The documents illustrate structure and traceability, not a mandatory Web stack
or a complete production specification.
