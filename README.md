# Awesome Plan

Awesome Plan is a skill for AI coding agents working on large software projects
in which human experts direct the project and AI coding agents drive detailed
planning, implementation, verification, and record keeping.

## How to use

The complete skill is [awesome-plan.md](awesome-plan.md). An agent that can read
a web URL can acquire and apply the skill directly with a prompt like this:

```text
Read and acquire the Awesome Plan agent skill from:
https://raw.githubusercontent.com/awemorris/MWP-Q-Agentic-Coding-Method/main/awesome-plan.md

Inspect this repository before asking questions. Follow the adoption and
initial-deployment procedure in the skill. Ask whether I want GitHub mode or
local-only mode before making remote changes. Help me establish the project
scope, final goal, Milestone Goals, initial Workstreams, current focus, and
Guardrails. Ask only for material information that cannot be learned from the
repository. Ask about existing coding standards and additional guard
instructions. Present the initial project model for agreement, then deploy it
in the selected mode. Do not implement a Phase until I separately approve a
concrete Queue.
```

The `main` URL follows the latest published skill. For reproducible adoption,
replace `main` with a reviewed commit SHA.

For agents that cannot reliably load remote instructions, copy
`awesome-plan.md` into the target repository, for example as
`docs/agent/awesome-plan.md`, and add this short instruction to the repository's
`AGENTS.md` or equivalent entry file:

```text
Read and follow docs/agent/awesome-plan.md as the Awesome Plan agent skill for
project planning, execution boundaries, GitHub/local synchronization,
Guardrails, bug handling, and Queue operation.
Read plan/config.md to locate this project's current Awesome Plan records.
```

Then ask the agent to apply Awesome Plan. During adoption, the agent will:

1. inspect the codebase, documentation, existing plans, and development tools;
2. ask for missing scope, goal, milestone, focus, and constraint decisions;
3. confirm GitHub or local-only mode, reusing an existing explicit choice;
4. discover and confirm coding standards and Guardrails;
5. present the initial project model for expert review and agreement;
6. initialize the local `plan/` state; and
7. when GitHub mode is approved, create or reuse the Issues, relationships,
   milestones, Project fields, and Project views through `gh` and verify them.

Choosing GitHub mode authorizes only the described planning-resource setup. It
does not approve implementation. If GitHub setup is not approved, the agent
initializes the local version under `plan/`.

## Why Awesome Plan

It is intended for experts who understand the product or engineering domain and
can manage a complex project: they define the desired outcome, make professional
judgments, establish design policy, choose priorities, and review the plans and
results produced by agents. The agents turn that direction into detailed,
verifiable work and use their implementation speed to move the project forward.

The human expert is not reduced to an approval button. The expert continuously
directs the work, corrects assumptions, supplies design principles, and decides
questions of product intent, risk, architecture, and acceptable outcomes. AI
handles much of the investigation and detailed decomposition, presents its work
for expert review, and then executes rapidly inside the approved boundary.

This model is designed for development that spans many sessions, repositories,
or components and cannot safely fit inside one agent conversation. Goals,
decisions, priorities, execution permission, evidence, bugs, and unfinished work
are kept in durable project records instead of depending on chat history.

The central rule is:

> Plan broadly. Execute narrowly within a finite, agreed scope.

The complete project plan describes where the software is going. It is not
blanket permission to implement everything in the plan. Before implementation,
the agent proposes a finite Queue and the human expert approves its exact scope.
That approved Queue is the execution boundary for the current cycle.

## The collaboration model

Awesome Plan combines expert direction with agent speed through a repeated
review loop.

![Expert direction and the AI planning, implementation, and review cycle (Japanese)](img/1.png)

```text
Human expertise and management
  ├─ goals, constraints, priorities, design policy, professional judgment
  ↓
Agent investigation and detailed planning
  ├─ milestones, Workstreams, Phases, dependencies, verification plans
  ↓
Human review and Queue approval
  ↓
High-speed agent implementation and verification
  ↓
Human review of outcomes, risks, bugs, and next priorities
  ↺
```

| Human experts direct and review | Agents investigate, detail, and execute |
| --- | --- |
| Project scope and final goals | Repository and system investigation |
| Milestone acceptance | Drafting and maintaining planning records |
| Current focused goals and WS priority | Breaking outcomes into WSs and Phases |
| Product and engineering design policy | Elaborating the design within that policy |
| Professional decisions about architecture, risk, and tradeoffs | Identifying alternatives, dependencies, and uncertainties |
| Queue scope and material changes | Implementing only the approved Queue |
| Whether results meet the intended outcome | Testing, validation, evidence, and synchronization |
| Whether an unreproduced bug may stop blocking completion | Preserving bugs and residual work without stalling indefinitely |

An expert may delegate routine technical decisions to the agent. The agent then
proposes a reasonable detailed design within the established policy, explains
material tradeoffs, and presents it for review. Delegating detail does not give
the agent authority to change the product goal, risk posture, or project scope.

## Project structure

![Planning hierarchy, approved Queue, and execution boundary (Japanese)](img/3.png)

The outcome hierarchy is:

```text
Project Objectives
  └─ Milestone Goals
       └─ Workstreams (WS)
            └─ Phases
```

Each WS has one Primary Milestone and may link to other milestones it supports.
A Phase is a bounded, verifiable unit of execution. Current Focused Goals explain
what matters now; WS priority expresses how the project should respond to that
focus.

The method uses the following records:

| Record | Purpose |
| --- | --- |
| Master Board | Objectives, scope, milestones, current focus, and WS priority |
| Workstream Board | One substantial outcome, its constraints, dependencies, and Phases |
| Phase | Executable scope, procedure, completion criteria, and evidence |
| Queue Board | The currently authorized work and dependency graph |
| Upcoming Work Outlook | A non-authorizing forecast of likely next work |
| Guardrail Board | Project-specific source contribution rules and coding-standard links |
| Future Work Board | Ideas and deferred work that are not current commitments |
| Bug Board and Bug Tickets | A compact bug index with detailed investigation records |
| Past Log Board | The latest Queue summary and durable execution history |

Phase execution ends as `cleared` or `uncleared`. An `uncleared` result is a
controlled outcome: evidence and a concrete resume condition are retained. A
Queue can finish with uncleared items after all authorized work has been
processed as far as reasonably possible.

An unreproduced bug does not need to block a WS forever. After bounded
investigation, the agent records the test scope and asks the expert whether the
bug should move to the Bug Board and stop blocking the Phase. The transfer does
not claim that the bug was fixed or disproved.

## Guardrails and code quality

![Coding standards, verification, and continued bug tracking (Japanese)](img/4.png)

Before designing a WS or Phase, the agent reads the Guardrail Board and follows
the applicable architecture, source-layout, testing, security, and coding
standards supplied or approved by the expert.

Where practical, the project keeps both:

- a full coding standard used for authoritative validation; and
- a concise, context-efficient version passed directly to smaller models during
  code generation.

Machine-enforceable rules should use checked-in tools such as `clang-format`,
language formatters, linters, and static analysis. Tool coverage is recorded so
that prose-only rules are not mistaken for automated checks. Each code-producing
WS includes a near-final Phase that validates all WS changes against the full
standard before the WS can become `completed`.

New coding or guard instructions from the expert are recorded in the Guardrail
Board and the applicable full standard. The concise version and automation map
are regenerated, and affected WSs and Phases are reassessed.

## GitHub and local operation

![GitHub Issues and Projects, local records, and write-back synchronization (Japanese)](img/2.png)

Awesome Plan supports two modes with the same semantics.

In GitHub mode, the agent maps Boards, WSs, Phases, Queue history, and Bug
Tickets to GitHub Issues. Native milestones, sub-issues, and issue dependencies
support navigation. A GitHub Project provides views for milestones and WSs,
current focus, the current Queue, Upcoming Work Outlook, and bugs.

GitHub Projects is a view over the project records. Exact Queue approval,
completion evidence, decisions, Guardrails, and history remain in Issue bodies
and the local cache.

The local cache supports disconnected work. Changes are written to a durable
outbox and reconciled with GitHub when connectivity returns. If GitHub is not
used, the same records operate entirely under `plan/` as the authoritative
local project state.

The agent performs synchronization at work checkpoints and on later sessions
unless a separate sync service has been configured; the skill itself does not
install a background service.

Phase Issues receive comments when work becomes `uncleared`, human judgment is
needed, or an approved bug transfer permits clearance. Cleared Phases and
completed WSs are closed and may be reopened with a recorded reason. WS comments
summarize Phase additions, structural changes, completion, cancellation, and
closure. These are minimum requirements: additional comments are welcome when
they convey useful findings, decisions, changed impact, or requested summaries.
Combine related events and normally omit standalone comments for minor edits
or unchanged status; keep the history informative without repetitive posts.
Offline, these events are retained for write-back; local-only operation keeps
the same history locally. Cancellation is recorded separately from completion.

After an `uncleared` outcome, a design revision confined to that Phase is
explained in a Phase comment. If recovery adds, changes, or removes Phases or
affects their shared interfaces or dependencies, also comment on every other
Phase whose plan changes and on each affected WS. Each Phase comment explains
its own change and reason; the WS comment summarizes the revised structure and
impact, with links connecting the originating and changed Phases.

## Working cycle

1. The expert states a focused goal or identifies a WS to prioritize.
2. The agent updates Current Focused Goals, WS priorities, dependencies, and
   near-term Phase plans.
3. The expert reviews and corrects the proposed design and planning detail.
4. The expert provides a timebox or desired execution cycle.
5. The agent proposes a finite Queue and an Upcoming Work Outlook.
6. The expert approves the Queue's exact execution scope.
7. The agent implements and verifies only that Queue.
8. Results become `cleared` or `uncleared`; bugs and future work are preserved.
9. The agent updates the Past Log, planning records, and GitHub/local state.
10. The expert reviews the outcome and directs the next cycle.

## Skill specification

[awesome-plan.md](awesome-plan.md) is the authoritative current skill
specification, written compactly to reduce context use. It is self-contained.

The [archived detailed edition](original/awesome-plan-original.md) preserves
the fuller explanations and review scenarios. It is reference material and
does not need to be loaded alongside the current skill. The
[review and compression comparison](awesome-plan-review.md) records the
changes and comparison before adoption.

## License

This repository is available under the [MIT License](LICENSE).
