---
paths:
  - "specs/**/*"
  - "SPECS.md"
  - "TASKS.md"
  - "MEMORY.md"
---

# Specs-Driven Development

This project follows a specs-driven workflow. All planning and tracking lives in `specs/`.

## Directory structure

```
specs/
├── SPECS.md    # Product requirements, constraints, targets
└── TASKS.md    # Sprint-based implementation tasks
```

## SPECS.md format

Contains: PRD (product requirements document), constraints, targets, and any technical context needed before implementation.

## TASKS.md format

Tasks are organized into three sections:

### # Active
Current sprint being worked on:
```markdown
# Active
- Sprint {n} {name}
  - [ ] Task description
  - [ ] Another task
```

### # Pending
Future work not yet started:
```markdown
# Pending
- {name}
  Reason: {why this is pending}
  - Task detail
  - Another detail
```

### # Archive
Completed work — keep only the 5 most recent entries:
```markdown
# Archive
- {name} {short description} {date}
  - What was done
```

## Specs alignment (MANDATORY)

Before implementing any task, read `SPECS.md` and compare the current state of the code against it. This is non-negotiable.

- If code, plan, or task does not align with SPECS.md — **stop immediately**
- Ask the user: "SPECS.md says X, but the current code/task does Y. Why does this differ?"
- Do NOT proceed until the discrepancy is resolved
- If the user confirms intentional change, update SPECS.md first before continuing
- Common drift scenarios: client changed requirements mid-development, user updated code without specs, new constraints emerged

The spec is the source of truth.

## Session Start — Fresh Context

When starting in a new or cold context, establish context before any code changes:

1. **Check for specs** — read SPECS.md for requirements and active sprint
2. **Check MEMORY.md** — persistent project context, past decisions
3. **Check task list** — understand active sprint vs pending vs archived
4. **Explore codebase** — quick reconnaissance: language, framework, structure, key entry points

Only proceed once context is established.

## Per-Task Process

Every feature, fix, or change follows these steps in order.

### 1 — Understand
Explore relevant parts of the codebase. Read impacted files. Map dependencies and data flow. Do not jump to code.

### 2 — Discuss
Align with the user through conversation or explicit questions. If ambiguous, ask. If conflict with specs, flag it. Outline trade-offs, let user decide. Do not infer requirements silently.

### 3 — Plan
Break work into atomic tasks under the current Sprint. Each task = one atomic unit ("Add validation to login form", not "Build auth"). Order by dependency — foundations first.

### 4 — Review Tasks
**STOP HERE.** User reviews, adjusts, reorders, and adds missing items. Do not begin execution until confirmed.

### 5 — Execute
Work through each task in order. For each:
1. Read relevant files if not already loaded
2. Run the decision stack: MUST → EXIST → BREAK → TIGHT → SHIP, in order, no skipping
3. Run linters and type checks
4. Commit with conventional commits and signed messages

Do not move to the next task until current one passes all checks.

### 6 — Self Code Review
After all tasks complete, audit everything you wrote. Be critical. Check requirements, breaking changes, project conventions, TODO/FIXME artifacts. **No code changes during this phase.** Bugs found here are logged, not fixed.

### 7 — Report Findings
Report what you found: bugs or issues discovered, deviations from plan, suggestions for next sprint. Move completed tasks from Active to Archive. Create a new Sprint for any bugs found.

### 8 — Deliver
Comprehensive final summary: what was implemented, lints/tests passed, bugs found (assigned next sprint), what's coming next.
