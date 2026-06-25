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

## Optimization
- Avoid premature optimization
- Build a quick prototype in a `test/` or `eval/` folder first to verify performance before committing to an approach
- Once the system is running, focus optimization effort only on measured bottlenecks: I/O, memory allocation, and actual hot paths

## Error Handling
- Validate at system boundaries. Trust internal code and framework guarantees.
- For recoverable errors at boundaries, handle explicitly. No panics, no crashes.
- Do not add validation, error handling, or fallbacks for scenarios that cannot happen.

## Code Review Timing
- Code review sessions happen after all tasks are complete — not mid-stream
- Reviews should be thorough and critical — roast the code
- Check for breaking changes, non-standard patterns, violations of project guidelines, and linting errors
- **If bugs or issues are found during review, log them and assign to the next sprint. Do not fix them in the current execution phase.**

## Verification Depth

| Change type | Minimum verification |
|---|---|
| Single function, pure logic | Unit test for new path, existing tests pass |
| New API endpoint | Integration test (request → response), schema validation |
| Dependency bump | `bun run check` + existing tests, flag breaking changes in changelog |
| Refactor, no behavior change | Existing tests pass, diff shows only structural change |
| Schema / migration | Dry-run both directions, test with representative data |
| Config / env change | Print effective config, verify no syntax error |

Strike the balance: do not test defaults or trivial plumbing. Test conditional branches, edge values, invariants across fields, and error paths.
