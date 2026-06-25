---
paths:
  - "*"
---

# Context Window Budget

Long sessions degrade. This protocol keeps decision quality consistent.

## Checkpoints

- After every 50 tool calls, call `checkpoint` + `rewind` — summarize resolved decisions into a concise report. Discard resolved conversation history.
- Before spawning a subagent, write context prerequisites to `local://<task>.md`. Do not carry state in memory.
- After every 3 completed tasks, if file contents are still loaded from a read, purge anything no longer referenced.

## File discipline

- Read only sections you need. Use `:50-100` ranges, not whole-file reads.
- When a read summary shows an elided region you do not need — do not read it. Do not open files "just to be safe."
- Archive old reads: do not keep file contents in context after the relevant edit is applied and verified.

## Subagent coordination

- When delegating, put shared contracts in `local://<contract>.md`. Subagents read it once instead of receiving the same context inline.
- Do not re-explain what a subagent's peer already communicated. Reference the artifact.

## When context feels crowded

Stop. Run `checkpoint` + `rewind`. If the session is too long to salvage, summarize the state into local files and flag the user:
- `local://session-state.md` — what was done, what's next, open decisions
- `local://blocked.md` — anything stuck
