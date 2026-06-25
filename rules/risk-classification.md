---
paths:
  - "**/*.py"
  - "**/*.go"
  - "**/*.rs"
  - "**/*.ts"
  - "**/*.tsx"
  - "**/*.js"
  - "**/Cargo.toml"
  - "**/package.json"
---

# Risk Classification Gate

Before any change, classify its risk level and apply the corresponding procedure.

## Classification

### LOW
Config tweak, comment fix, single-file refactor with full test coverage, dependency patch bump, trivial style change.
- **Procedure:** Proceed directly. Write tests if new logic was added.

### MEDIUM
Multi-file change, API contract shift, dependency minor bump, new feature branch, database column add (nullable).
- **Procedure:** Write a plan first. Run existing tests before and after. Get user sign-off before implementation.

### HIGH
Schema migration, auth flow change, payment/security logic, public API break, state migration, dependency major bump, anything touching production data.
- **Procedure:** Write the plan. Prototype in /tmp or test/ first. Get explicit user approval before touching main codebase.

## If uncertain

Default to the higher classification. Over-classifying wastes a minute. Under-classifying can lose data or ship a security hole.

## At session start

If the project has no SPECS.md or TASKS.md, classify the session itself:
- **Exploration / research** — LOW. Read, investigate, report.
- **Scaffold / init** — MEDIUM. Plan structure, get approval, then build.
- **Production work on active project** — HIGH by default.
