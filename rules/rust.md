---
paths:
  - "**/*.rs"
---

# Rust Rules

- No `panic!`, `unwrap()`, or `expect()` — these are not acceptable in production code
- All errors must be handled explicitly
- Preferred error handling: `anyhow` for application-level errors, `thiserror` for library-level errors
- Note: these preferences depend on the project — adapt when the project already has established error handling conventions
