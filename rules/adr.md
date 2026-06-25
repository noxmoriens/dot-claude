---
paths:
  - "specs/**/*"
  - "DECISIONS.md"
  - "docs/decisions/**/*"
  - "**/DECISIONS.md"
---

# Decision Records

Preserve why non-obvious choices were made. Prevents re-litigating closed questions across sessions.

## When to record

Append a decision when you choose between alternatives with real trade-offs:
- Architecture fork (client-side vs server-side rendering, monolith vs microservices)
- Library selection rejected alternatives
- Performance workaround justified by measurement
- Constraint discovery that shaped the design

Do not record:
- Trivial choices ("used HashMap", "named variable X")
- Implementation details that code already expresses
- Spec requirements that are already documented

## Format

Append to `specs/DECISIONS.md`:

```markdown
YYYY-MM-DD: Chose X over Y because Z
- Context: one sentence describing the situation
- Considered: A, B, C (briefly, one line each)
- Rationale: why X won — concrete trade-off, not opinion
- Consequences: what this enables or forecloses
```

## Session start

Check if `specs/DECISIONS.md` exists. If so, read it first. Past decisions are binding unless new evidence invalidates them.

## Revising a decision

If new information contradicts a past decision:
1. Document why the old decision no longer holds
2. Append a new entry — do not edit the old one
3. Reference the old entry by date
