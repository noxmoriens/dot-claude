---
paths:
  - "specs/**/*"
  - "SPECS.md"
  - "TASKS.md"
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

Before implementing any task, Claude must read `SPECS.md` and compare the current state of the code against it. This is non-negotiable.

- If the code, plan, or task does not align with what's documented in `SPECS.md` — **stop immediately**
- Ask the user: "SPECS.md says X, but the current code/task does Y. Why does this differ?"
- Do NOT proceed with implementation until the discrepancy is resolved
- If the user confirms a change was intentional (client requirement change, new constraint, etc.), update `SPECS.md` first before continuing
- Common drift scenarios: client changed requirements mid-development, user updated code without updating specs, new constraints emerged

This rule prevents silent drift between what the specs say and what the code does. The spec is the source of truth.

## Workflow

1. **Discuss** — align on requirements and approach
2. **Context sync** — ensure shared understanding
3. **Read specs** — load SPECS.md and TASKS.md, verify current code aligns with specs
4. **Plan** — update SPECS.md if requirements changed; otherwise proceed
5. **Assign tasks** — break into checkboxes in TASKS.md Active section
6. **Execute** — work through tasks in order
7. **Code review** — roast the code after all tasks complete
8. **QA / Unit test** — verify correctness
9. **Report** — comprehensive summary of what was done

Move completed tasks from Active to Archive. Move future work from Pending to Active when a new sprint starts.
