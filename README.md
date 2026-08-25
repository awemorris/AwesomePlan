# MWP-Q Agentic Coding Method

MWP-Q is a file-based planning and execution method for long-running software
development with coding agents. It keeps the project direction persistent
across sessions while separating planned work from work that is authorized for
the current execution cycle.

## The four Books

| Book | Role | Question it answers |
| --- | --- | --- |
| M — Master | Project strategy, scope, milestones, and Workstreams | Where are we going? |
| W — Workstream | One substantial development outcome and its Phases | What must this Workstream achieve? |
| P — Phase | A bounded, executable, verifiable plan | How will this step be completed? |
| Q — Queue | The current execution manifest | What may the agent work on now? |

```text
M/W/P = planning hierarchy
Q     = execution and authorization boundary
```

The central rule is: plan broadly and execute narrowly. A Phase appearing in
M/W/P is not permission to implement it. Before execution, eligible Phases are
selected into a finite Queue, the Queue is approved by the user, and only then
is implementation started.

Queue items should be carved out so that all known product, scope, risk, and
major architecture decisions have already been resolved. The agent should be
able to execute and verify them without further human judgment. Work that is
already known to require a human decision stays in M/W/P until that decision is
made; an unexpected decision discovered during execution makes the item
`uncleared` and returns the residual work to planning.

## Typical layout

```text
plan/
├── master.md
├── queue.md
├── ws001-name/
│   ├── ws.md
│   ├── phase001-name/
│   │   └── phase.md
│   ├── tests/
│   └── temp/
└── ws002-name/
    └── ...
```

Stable IDs keep references valid across sessions. Completion is determined by
the acceptance criteria and recorded evidence, not merely by code changes. A
Queue can finish with `uncleared` items when their findings, reason, and resume
condition are preserved.

## How to use this repository

- Copy [AGENTS-en.md](AGENTS-en.md) or [AGENTS-ja.md](AGENTS-ja.md) to a
  project's `AGENTS.md` and adapt project-specific commands and constraints.
- Create the M/W/P planning hierarchy with the user.
- Agree on a timebox and propose a Q Book containing only bounded,
  decision-cleared work.
- Obtain explicit Queue approval, execute it, verify each item, and synchronize
  the result back into M/W/P.

See [sample-plan/README.md](sample-plan/README.md) for a worked example of a
fictional university community social-networking Web application. It includes
an M Book, three W Books, near-term P Books, and a Q Book that deliberately
excludes unresolved human decisions.

## License

This repository is available under the [MIT License](LICENSE).
