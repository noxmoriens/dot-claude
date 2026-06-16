---
paths:
  - "**/*.py"
  - "**/*.go"
  - "**/*.rs"
  - "**/*.ts"
  - "**/*.tsx"
  - "**/*.js"
  - "**/*.php"
  - "**/*.dart"
  - "**/*.java"
  - "**/*.kt"
  - "**/*.c"
  - "**/*.h"
  - "**/*.cpp"
  - "**/*.hpp"
  - "**/*.cc"
---

# Code Guidelines

## Naming
- All function and variable names must be self-documenting — the name alone should convey purpose without needing extra context

## Comments
- No block comments except for: `// TODO`, `// FIXME`, and similar markers; public function documentation; and file header licensing in SPDX format
- Write code that explains itself — comments should be the exception, not the default

## Before Coding
- Study all impacted files before writing any code
- Ask: does this introduce new bugs? Is the algorithm unnecessarily complex? Can the target machine/server handle it? Consider CPU efficiency, cache behavior, and network latency

## Algorithm Complexity
- Don't write code that looks clever but burns memory and introduces latency
- Target O(1) or O(log n) at minimum — if higher complexity is unavoidable, stop and discuss the trade-off with the user before proceeding

## Code Reviews
- Code review sessions happen after all tasks are complete — not mid-stream
- Reviews should be thorough and critical — roast the code
- Check for breaking changes, non-standard patterns, violations of project guidelines, and linting errors

## Optimization
- Avoid premature optimization
- Build a quick prototype in a `test/` or `eval/` folder first to verify performance before committing to an approach
- Once the system is running, focus optimization effort only on measured bottlenecks: I/O, memory allocation, and actual hot paths

## Defensive Programming
- Code must be fault-tolerant — every error must be handled correctly
- No segfaults, panics, or crashes from unhandled errors
- Assume failure is the default state and code accordingly
