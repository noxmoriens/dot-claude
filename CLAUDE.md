# Workflow

This document describes how users work. It is the source of truth for the collaboration process between me and Claude.

## Session Start — Fresh Context

When starting in a new or cold context, always do the following before any code changes:

1. **Check for specs.** Look for a `specs/` directory or `SPECS.md` file. If they exist, read them to understand the project requirements, constraints, and current sprint.
2. **Check MEMORY.md.** Read `MEMORY.md` for persistent project context, references, and past decisions.
3. **Check the task list.** Look for active sprints — tasks are organized as **Sprints**, not arbitrary to-do lists. Understand what sprint is active and what's pending/archived.
4. **Explore the codebase.** Do a quick reconnaissance — understand the project structure, language, framework, key entry points. Don't dive into implementation yet. Just build a mental map.

Only proceed once context is established.

---

## Per-Task Process

Every feature, fix, or change follows this workflow:

### 1. Understand — Build Context
Explore the relevant parts of the codebase to understand the big picture. Read the files that will be impacted. If the scope is unclear, use `find`, `grep`, or the Explore agent to map dependencies and data flow. Do not jump to code.

### 2. Discuss — Align With the User
Use natural conversation or `AskUserQuestion` to clarify requirements until we share the same understanding.

- If the request is ambiguous, ask before assuming.
- If the request conflicts with existing specs or MEMORY.md context, flag it.
- If there are multiple valid approaches, outline trade-offs briefly and let the user decide.

Do not skip this step. Do not infer requirements silently.

### 3. Plan — Create the Sprint Tasks
Break the work into tracked tasks and organize them under the current **Sprint** in the project's task list (either `specs/TASKS.md` or the session's built-in task system).

- Each task should be one atomic unit of work (e.g. "Add validation to login form" not "Build auth").
- Order tasks logically — dependencies first.
- Present the task list to the user for review.

### 4. Review Tasks — Wait for User Sign-Off
Stop here. The user will review the assigned tasks, make adjustments, add missing items, or reorder. Do not begin execution until the user confirms the task list is approved.

### 5. Execute — Implement the Plan
Work through each task in order. For each task:

- Read relevant files if not already loaded.
- Write or edit code.
- Run linters and type checks (`bun run lint`, `bun run format`, `bun run check` for TypeScript; `cargo clippy` for Rust; etc.).
- Commit with conventional commits and signed messages.

Do not move to the next task until the current one is verified (lints pass, types check, tests pass).

### 6. Self Code Review — Audit Your Own Work
After all tasks are complete, review everything you just wrote. Be critical:

- Does the code meet the requirements from step 2?
- Are there any breaking changes, edge cases, or regressions?
- Does the code follow the project's conventions (error handling, naming, structure)?
- Are there any `TODO`, `FIXME`, or debug artifacts left behind?

**Critical rule: No code changes during this phase.** You are reviewing only — do not fix anything yet. If you find bugs, issues, or improvements, log them. Do not edit code.

### 7. Report Findings — Update Specs and Sprint
Report what you found during the code review to the user. This includes:

- Bugs or issues discovered during review.
- Deviations from the original plan.
- Suggestions for the next sprint.

Update `specs/TASKS.md`:
- Move completed tasks from Active to Archive.
- If bugs were found during code review, create a **new Sprint** for them in the Pending section. Do not fix them in the current sprint.
- If new work was discovered, add it to Pending.

### 8. Deliver — Comprehensive Summary
Give the user a final summary of:

- What was implemented.
- What lints/checks passed.
- Any bugs or issues found (and assigned to next sprint).
- What's coming next in the pipeline.

---

## Hard Rules

- **No mid-review fixes.** If a bug is found during code review, report it and assign it to the next sprint. Do not fix it in the current execution phase.
- **No silent assumptions.** If you don't know, ask.
- **No jumping to code.** Context first, plan second, code third.
- **Specs are the source of truth.** If code and specs disagree, stop and ask.
