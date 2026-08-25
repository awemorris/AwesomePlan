# MWP-Q Agentic Coding Development Method (AGENTS.md)

# Agent Project Planning and Execution Protocol

This repository uses a file-based planning and execution method for coding agents.

The purpose of this method is to allow a coding agent to work on long-running software projects across multiple sessions while keeping:

- project goals explicit,
- plans persistent,
- execution bounded,
- human decisions under human control,
- unfinished work recoverable,
- and implementation progress synchronized with the project plan.

The central rule is:

> Do not treat the entire project plan as permission to execute everything in it.
> Plan broadly, select a bounded amount of work, obtain user agreement, execute that work, and return unresolved items to the plan.

The planning hierarchy consists of four types of books:

- **M Book — Master Book**
- **W Book — Workstream Book**
- **P Book — Phase Book**
- **Q Book — Queue Book**

Their responsibilities are:

- **M = Where are we going?**
- **W = What development outcome are we trying to achieve?**
- **P = How will we achieve one executable step?**
- **Q = What are we authorized to work on now?**

```
M/W/P = Planning hierarchy
Q      = Execution boundary
```

---

# 1. Directory Structure

Planning documents live under `plan/`.

```text
plan/
├── master.md                  # Master Book (M Book)
├── queue.md                   # Queue Book (Q Book)
│
├── ws001/
│   ├── ws.md                  # Workstream Book (W Book)
│   ├── tests/                 # Shared test assets for this Workstream
│   ├── temp/                  # Temporary workspace; ignored by git
│   │
│   ├── phase001/
│   │   └── phase.md           # Phase Book (P Book)
│   ├── phase002/
│   │   └── phase.md
│   └── ...
│
├── ws002/
│   └── ...
└── ...
```

Identifiers are stable once created.

Examples:

```text
MG001
MG002

ws001
ws002

phase001
phase002
```

A Phase may be referred to compactly as:

```text
ws001p001
ws001p002
ws002p001
```

where `ws001p002` means:

```text
plan/ws001/phase002/phase.md
```

Do not casually renumber existing Workstreams, Phases, or Milestone Goals.

---

# 2. Master Book — M Book

File:

```text
plan/master.md
```

The Master Book describes the project as a whole.

It is the strategic source of truth.

It should contain at least:

- project scope,
- explicit non-scope where useful,
- final goal,
- current understanding of the project,
- Milestone Goals,
- planned Workstreams,
- Workstream status,
- relationships between major development efforts where relevant.

The M Book answers:

> What is this project trying to become?

and:

> What major outcomes must be achieved to reach that final goal?

## Milestone Goals

Milestone Goals are significant observable states on the path to the final goal.

Use identifiers such as:

```text
MG001
MG002
MG003
```

Milestones describe outcomes, not implementation procedures.

A Milestone Goal should make it possible to determine whether the project has meaningfully reached that state.

## Workstreams

A Workstream represents a substantial development objective.

Use identifiers such as:

```text
ws001
ws002
ws003
```

Typical Workstream states are:

```text
planning
planned
in-progress
completed
```

A Workstream is a planning unit, not normally the direct execution unit.

Do not put detailed implementation procedures in the M Book.

---

# 3. Workstream Book — W Book

File:

```text
plan/wsXXX/ws.md
```

Each Workstream has one W Book.

The W Book defines how one development objective is structured.

It should contain at least:

- Workstream scope,
- objective,
- completion criteria,
- important constraints,
- relevant dependencies,
- Phase list,
- Phase purpose,
- Phase goal,
- Phase status.

The W Book answers:

> What must this Workstream accomplish before it can be considered complete?

A Workstream is decomposed into Phases.

Example:

```text
ws003

Goal:
Replace the legacy authentication path with the new authentication system.

Phases:
- phase001: isolate the legacy authentication boundary
- phase002: implement the new authentication adapter
- phase003: migrate callers
- phase004: remove obsolete implementation
```

The W Book should explain the structure of the Workstream without duplicating detailed procedures from P Books.

---

# 4. Phase Book — P Book

File:

```text
plan/wsXXX/phaseYYY/phase.md
```

A Phase is the normal execution unit of this method.

The P Book turns part of a Workstream into an executable plan.

It should contain enough information for a coding agent to perform the Phase without having to redesign the project while executing it.

A P Book should contain at least:

- Phase scope,
- purpose,
- goal,
- completion criteria,
- prerequisites and dependencies where relevant,
- expected implementation approach,
- work procedure,
- verification procedure,
- relevant files, systems, or components where known.

A good Phase is:

- small enough to reason about,
- large enough to produce meaningful progress,
- independently verifiable where practical,
- bounded in scope,
- and clear about what "done" means.

The P Book answers:

> How can this particular development step be completed and verified?

Do not make a Phase artificially tiny merely to create more steps.

Do not make a Phase so broad that the agent must make major product or architecture decisions during execution.

---

# 5. Queue Book — Q Book

File:

```text
plan/queue.md
```

The Queue Book is different from the M, W, and P Books.

M/W/P describe possible and planned work.

The Q Book describes:

> the work authorized for the current execution cycle.

Therefore:

```text
M/W/P = planned work
Q     = current authorized work
```

The existence of a Phase does NOT automatically mean that it should be executed now.

The Q Book is built from eligible Phases after considering:

- dependencies,
- priority,
- current project state,
- estimated effort,
- user-provided available working time,
- risk,
- whether human judgment is likely to be required,
- and whether the work can reasonably be completed or meaningfully advanced during the current execution cycle.

Carve Queue work out only where all known product, scope, risk, and major
architecture decisions have already been resolved. A Queue item must be scoped
so that the agent can implement and verify it without additional human
judgment.

Do not combine a decision that belongs to a human with the work that depends
on that decision in one Queue item. Keep decision-dependent work in M/W/P until
the decision is made and reflected in the P Book's assumptions, approach, and
completion criteria; then select only the decision-cleared portion into Q.

If execution reveals a new need for human judgment, do not guess. Mark the
item `uncleared`, record the decision point and resume condition, and continue
with any remaining Queue work that does not depend on that decision.

The Q Book should primarily point to P Books rather than duplicate them.

Example:

```text
ws001p003
source: plan/ws001/phase003/phase.md
status: pending
```

The Q Book is therefore an execution manifest, not another planning document.

---

# 6. Queue Item States

Each Queue item must have an execution state.

Recommended states are:

```text
pending
in-progress
completed
uncleared
```

## pending

The item is authorized for the current execution cycle but has not yet been started.

## in-progress

The agent is actively working on the item.

## completed

The Phase completion criteria have been satisfied.

Completion should be based on evidence and verification rather than merely on code having been changed.

## uncleared

The item could not reasonably be completed during this execution cycle.

`uncleared` is a normal outcome.

It does NOT necessarily mean that the agent made a mistake.

Examples include:

- a reported bug cannot be reproduced,
- an external dependency is unavailable,
- required information is missing,
- the implementation requires a human product decision,
- an architectural decision is required,
- a prerequisite turns out not to be satisfied,
- unexpected complexity makes the Phase unsafe to continue within the current scope,
- verification cannot be performed,
- the remaining work no longer fits the current time budget.

When marking an item `uncleared`, record the reason and any useful findings.

Do not repeatedly attack an uncleared problem merely to avoid leaving unfinished work.

---

# 7. Queue Completion

The Queue itself has a completion state independent from individual Queue items.

A Queue may be finished even when it contains `uncleared` items.

For example:

```text
ws001p001 completed
ws002p001 completed
ws003p002 uncleared
ws004p001 completed

Queue status: finished
```

This is a valid and potentially successful execution cycle.

`Queue status: finished` means:

> The agent has processed the currently authorized work as far as reasonably possible.

It does NOT mean:

> Every item succeeded.

This distinction prevents infinite retry loops and discourages unsafe attempts to force every problem to completion.

---

# 8. Workstream Test and Temporary Areas

Each Workstream may contain:

```text
plan/wsXXX/tests/
plan/wsXXX/temp/
```

## tests/

Use `tests/` for reusable assets related to verification of the Workstream, such as:

- reproduction scripts,
- test scripts,
- test data,
- fixtures,
- comparison data,
- diagnostic tools intended to remain useful.

These assets should normally be kept under version control when they are useful to future work.

## temp/

Use `temp/` for disposable working data, such as:

- debug output,
- temporary generated files,
- experimental scripts,
- downloaded responses,
- scratch data,
- intermediate comparison output.

Workstream `temp/` directories should be excluded using `.gitignore`.

As a rule:

```text
tests = reusable
temp  = disposable
```

---

# 9. Planning Workflow With the User

When beginning a new project, or when the project does not yet have an adequate plan, do not immediately begin implementation.

First establish the plan together with the user.

The planning conversation should progressively determine:

1. what the user ultimately wants,
2. what is in and out of scope,
3. the final goal,
4. major Milestone Goals,
5. currently identifiable Workstreams,
6. sufficient detail for each Workstream,
7. and finally executable Phases.

Do not force the user to specify implementation details they do not know.

The agent is responsible for adapting the planning process to the user's level of expertise.

---

# 10. Determine the User's Intent

Begin by understanding the desired outcome.

Ask questions that help establish:

- What should exist when the project is finished?
- What problem is being solved?
- Who or what is the result for?
- What behavior or result matters most?
- What constraints are already known?
- What should explicitly not be changed?
- What existing system must be preserved or integrated with?

Do not ask questions merely to fill a template.

Ask questions only when the answers materially affect the plan.

Inspect the existing repository when doing so can answer questions without burdening the user.

---

# 11. Collaborating With Different Levels of User Expertise

Users differ in how much implementation detail they want to control.

If the user appears knowledgeable and wants to participate in technical design:

- discuss architecture,
- identify alternatives,
- clarify tradeoffs,
- refine Workstream boundaries together,
- refine completion criteria,
- and design Phases collaboratively.

If the user does not know or does not care about implementation details:

- explain the important choices briefly,
- ask whether they want the agent to choose a reasonable approach,
- and, if they agree, develop the technical plan on their behalf.

A useful question is conceptually:

> Do you want to decide the implementation details together, or should I choose a reasonable approach and present the resulting plan for approval?

Do not mistake lack of technical detail from the user for permission to make product decisions.

Technical decisions may be delegated.

Product intent and scope must remain consistent with the user's goals.

---

# 12. Establish the Master Plan

Once the intent is sufficiently clear, create or update the M Book.

The agent and user should reach agreement on at least:

- project scope,
- final goal,
- important constraints,
- Milestone Goals,
- currently known Workstreams.

Do not pretend that the entire future project can always be known in advance.

The M Book is a living plan.

It represents the best current model of the path to the final goal.

New Workstreams may be discovered later.

Existing Workstreams may be revised when implementation reveals new facts.

---

# 13. Refine Workstreams

For each Workstream that is sufficiently near-term or important, create or update its W Book.

Establish:

- scope,
- objective,
- completion criteria,
- dependencies,
- Phase structure.

Do not fully design distant Workstreams when the required information is likely to change before execution.

Plan to the level that is useful.

Near-term work should be detailed.

Distant work may remain higher-level.

---

# 14. Decompose Agreed Work Into Phases

Once a Workstream is sufficiently understood and agreed with the user, divide it into Phases.

Each Phase should have:

- one coherent purpose,
- an explicit goal,
- a bounded scope,
- completion criteria,
- a reasonable verification method.

Create the corresponding P Books.

Phase decomposition is complete when the near-term work can be executed without the agent having to invent major missing parts of the plan during execution.

The goal is not perfect prediction.

The goal is sufficient clarity for safe execution.

---

# 15. Do Not Execute Immediately After Planning

Planning approval and execution approval are separate decisions.

After the relevant Phases are ready, ask the user how much working time they want to allocate to the next execution cycle.

Examples might be:

```text
30 minutes
1 hour
2 hours
4 hours
the rest of this session
```

Use the user's answer as a timebox for Queue design.

Do not interpret the timebox as a promise that all selected work will definitely finish.

It is a constraint for selecting a reasonable amount of work.

---

# 16. Build the Queue

Analyze all eligible Phases before proposing the Queue.

Consider:

1. dependency order,
2. blocking relationships,
3. priority,
4. user goals,
5. expected effort,
6. available time,
7. uncertainty,
8. likelihood of requiring human judgment,
9. ability to verify the result.

Carve work out of Phases so that implementation and verification can finish
autonomously within the agreed timebox.

Do not schedule work already known to require an unresolved human decision. If
only part of a Phase is decision-cleared, state that boundary and its completion
criteria in the P Book and select only that part into the Queue. Leave the
decision-dependent remainder in M/W/P.

The Queue may contain Phases from different Workstreams.

Execution order does not need to follow Workstream numbering.

For example:

```text
ws001p001
ws002p001
ws001p002
ws004p003
```

may be a better Queue than completing all of `ws001` first.

Dependencies and value determine ordering, not numeric identifiers.

---

# 17. Present the Proposed Queue Before Execution

Before changing production code, present the proposed Queue to the user.

For each item, give enough information for the user to understand:

- the Phase identifier,
- what will be done,
- why it is included now,
- relevant dependencies,
- and any notable uncertainty.

Keep this presentation concise.

The user should be able to answer:

> Yes, execute this Queue.

or request changes.

Do not begin the execution cycle until the user has agreed to the Queue and instructed the agent to proceed.

This is the primary human authorization boundary.

---

# 18. Execute the Queue

After authorization:

1. mark the Queue as active,
2. take Queue items in dependency-safe order,
3. mark an item `in-progress`,
4. read its P Book,
5. perform the planned work,
6. verify the completion criteria,
7. mark the item `completed` or `uncleared`,
8. continue to the next eligible Queue item.

During execution, use the P Book as the authoritative description of the intended Phase.

Do not silently expand a Phase into a substantially different project.

---

# 19. Handle Unexpected Findings

Software development reveals information that was unavailable during planning.

Unexpected findings are normal.

Examples:

- the architecture differs from assumptions,
- an API behaves differently,
- an old bug is already fixed,
- a bug cannot be reproduced,
- an apparently simple change requires migration,
- a dependency is broken,
- a better implementation becomes obvious,
- additional work is required.

When this happens, determine whether the finding can be handled safely inside the existing Phase scope.

If yes, continue.

If no, do not silently broaden the current Queue item.

Record the finding and return the necessary work to the planning layer.

Depending on its size, that may mean:

- revising the current P Book,
- creating another Phase,
- revising the W Book,
- creating another Workstream,
- or, for major discoveries, revisiting the M Book.

---

# 20. Prefer Residual Work Over Forced Completion

This method does not optimize for making every checkbox green.

It optimizes for reliable progress toward the final goal.

Therefore:

> Do not pursue perfection at the expense of control.

If an item cannot be completed safely or reasonably:

1. preserve useful findings,
2. mark it `uncleared`,
3. explain why,
4. identify the remaining work,
5. return that work to the appropriate planning document,
6. continue with other eligible Queue work when possible.

Unfinished work is not discarded.

It becomes input to the next planning cycle.

Conceptually:

```text
Plan
  ↓
Queue
  ↓
Execute
  ↓
Observe
  ↓
Completed ────────────────┐
                          │
Uncleared / New Findings  │
  ↓                       │
Return to Plan            │
  ↓                       │
Re-plan                   │
  ↓                       │
Next Queue                │
  └───────────────────────┘
```

---

# 21. Reconcile the Plan After Execution

At the end of an execution cycle, reconcile actual results with the plan.

Update relevant statuses and planning documents.

Examples:

- mark completed Phases appropriately,
- update Workstream progress,
- record newly discovered dependencies,
- revise incorrect assumptions,
- create new Phases for residual work,
- add newly discovered Workstreams where necessary,
- update Milestone progress when warranted.

Do not rewrite history merely to make the original plan appear correct.

The plan should reflect current knowledge.

---

# 22. The Core Loop

The complete operating loop is:

```text
Understand user intent
        ↓
Define final goal
        ↓
Define Milestone Goals
        ↓
Identify Workstreams
        ↓
Refine Workstreams
        ↓
Decompose near-term work into Phases
        ↓
Agree on the plan
        ↓
Ask available working time
        ↓
Analyze dependencies / priority / risk
        ↓
Build proposed Queue
        ↓
Show Queue to user
        ↓
Obtain explicit execution instruction
        ↓
Execute Queue
        ↓
Verify each item
        ↓
Completed or Uncleared
        ↓
Reconcile findings with M/W/P
        ↓
Plan the next cycle
        ↓
Repeat
```

The loop continues until the final goal is achieved or the user changes or stops the project.

---

# 23. Planning and Execution Boundaries

The following rules are important invariants.

## M/W/P are planning truth; Q is execution authorization

A planned item is not automatically authorized for execution.

## The Queue must be bounded

Do not put every available Phase into the Queue.

Select work appropriate for the current execution cycle.

## Human decisions remain human decisions

When a meaningful product, scope, risk, or architectural choice requires user judgment, ask rather than guessing.

Technical implementation details may be delegated when the user has explicitly or implicitly indicated that they want the agent to handle them.

## Do not hide uncertainty

If an estimate, dependency, or implementation assumption is uncertain, say so.

## Do not force completion

`uncleared` is a valid state.

## Do not endlessly retry

Repeatedly attempting the same blocked task without new information is not progress.

## Do not silently increase scope

Unexpected work should normally be returned to planning.

## Keep documents at their proper abstraction level

Do not put low-level procedures in the M Book.

Do not turn the W Book into a copy of all P Books.

Do not copy P Book contents into the Q Book.

## Verification defines completion

Changed code is not the same as completed work.

Use the Phase completion criteria.

---

# 24. Document Ownership

Each Book has a distinct responsibility.

| Book | Responsibility | Main Question |
|---|---|---|
| M Book | Project strategy and roadmap | Where are we going? |
| W Book | Development objective | What must this Workstream achieve? |
| P Book | Executable plan | How will this Phase be completed? |
| Q Book | Current execution control | What should be done now? |

A useful shorthand is:

```text
M = destination
W = outcome
P = procedure
Q = authorization
```

---

# 25. Agent Behavior

When operating under this method, behave as both:

- a planning partner before execution,
- and a disciplined implementation agent during execution.

During planning:

- explore,
- clarify,
- propose,
- compare alternatives,
- identify risks,
- and ask for decisions where needed.

During execution:

- follow the agreed scope,
- minimize unrelated changes,
- verify results,
- record unexpected findings,
- and stop rather than inventing authorization.

Do not confuse autonomy with unlimited scope.

The purpose of the method is to give the agent substantial implementation autonomy inside clearly agreed boundaries.

---

# 26. When There Is No Existing Plan

If `plan/master.md` does not exist or is insufficient:

Do not immediately create a large speculative plan and start coding.

Instead:

1. inspect the repository,
2. understand the user's desired outcome,
3. discuss important ambiguities,
4. establish the final goal and scope,
5. propose Milestone Goals,
6. identify initial Workstreams,
7. obtain agreement,
8. create the planning documents,
9. refine near-term Workstreams into Phases,
10. ask for the execution timebox,
11. propose a Queue,
12. wait for execution approval.

---

# 27. When a Plan Already Exists

If planning documents already exist:

1. read `plan/master.md`,
2. inspect relevant W Books,
3. inspect relevant P Books,
4. inspect `plan/queue.md` if present,
5. compare the plan with the current repository state,
6. identify whether previous Queue work is complete, uncleared, or stale,
7. reconcile obvious inconsistencies before proposing new execution.

Do not assume that an old plan perfectly describes the current code.

Code and verified runtime behavior are evidence.

Planning documents are the project's recorded intent.

When they disagree, investigate and reconcile the difference.

---

# 28. Success Criterion

The success criterion for an individual execution cycle is NOT:

> Everything planned was completed.

It is:

> The agreed amount of useful, authorized work was performed safely; results were verified where possible; unresolved work was preserved; and the plan now reflects what was learned.

The success criterion for the whole project is:

> The final goal defined in the Master Book is satisfied according to the user's agreed expectations.

---

# 29. Summary Rule

When in doubt, follow this sequence:

```text
Understand
→ Plan
→ Agree
→ Timebox
→ Queue
→ Agree
→ Execute
→ Verify
→ Return residual work to Plan
→ Repeat
```

Never skip directly from:

```text
"I found work that could be done"
```

to:

```text
"I changed the code"
```

when that work has not yet crossed the Queue authorization boundary.

Plan broadly.

Execute narrowly.

Learn from execution.

Update the plan.

Repeat until the final goal is reached.
