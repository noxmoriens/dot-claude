---
paths:
  - "**/*.py"
  - "**/*.go"
  - "**/*.rs"
  - "**/*.ts"
  - "**/*.tsx"
  - "**/*.js"
  - "**/*.c"
  - "**/*.cpp"
  - "**/*.java"
---

# Debug Protocol

Structured approach when something does not work. No shotgun debugging.

## When an approach fails

1. **State the gap** — one sentence: "Expected X, got Y."
2. **Generate hypotheses** — list 2-3 possible causes. For each, note supporting and contradicting evidence already visible.
3. **Design one experiment** — pick the most probable cause. What single tool call, read, or test run would confirm or eliminate it?
4. **Execute the experiment** — only then touch code. No speculative edits.
5. **Interpret the result** — did it confirm or reject the hypothesis? Update belief. If rejected, return to step 2.

## When stuck >5 minutes

Write the problem to `local://blocked.md`:
- What you expected
- What happened
- Hypotheses tried and results
- What input from the user would unblock

Then switch to another task. Flag the user.

## Quick checks before reporting a bug

- Is the code actually being run? (Correct file? Correct branch? Restarted the server?)
- Is the test testing what you think it tests? (Read the assertion, not the name.)
- Is the error from your code or from a dependency / environment?
- Does it reproduce with minimal input? (Strip everything non-essential.)

## Dangerous debugging patterns (never)

- Adding debug prints/logs to "see what happens" without a hypothesis
- Changing a value because "maybe this fixes it" without understanding why
- Restarting services as a first resort
- Re-running without changes to "see if it was transient"
