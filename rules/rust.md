---
paths:
  - "**/*.rs"
  - "**/Cargo.toml"
  - "**/Cargo.lock"
---

# Rust Project Rules

## Clippy as the linter (mandatory)
- Use **cargo clippy** over `cargo check`. `cargo check` does not catch lint issues.
- Run `cargo clippy -- -D warnings` before committing.
- Do NOT run `cargo check` as a standalone command — if you need type-checking, `cargo clippy` already does that.

## Enforced clippy lint configuration
Every Cargo workspace must configure lints in root `Cargo.toml` like this:

```toml
[workspace.lints.clippy]
all = { level = "allow" }
expect_used = { level = "deny" }
nursery = { level = "allow" }
panic = { level = "deny" }
pedantic = { level = "warn" }
unwrap_used = { level = "deny" }
```

Each crate in the workspace then enables clippy via:

```toml
[lints]
workspace = true
```

## Adding dependencies (mandatory)
- Never add crate versions manually or guess version numbers.
- Always check the latest version first using `cargo info <crate>`.
- Dependencies must use the expanded TOML format:
  ```toml
  <package> = { version = "<version>" }
  ```
- Inline format is forbidden:
  ```toml
  # BAD — DO NOT USE
  <package> = "<version>"
  ```
- For crates with features, add them explicitly:
  ```toml
  <package> = { version = "<version>", features = ["<feature1>", "<feature2>"] }
  ```

## Creating new crates (mandatory)
- Never create `Cargo.toml` or crate files manually. Always use `cargo init`:
  ```bash
  cargo init --name <crate_name> {--lib (if library)} {./path/to/crate}
  ```
- For workspace crates, run `cargo init` inside the workspace directory, then register it in root `Cargo.toml` workspace members.

## Error handling (mandatory)
- **anyhow** for application-level error handling; **thiserror** for library/domain error types. The combination covers all cases.
- Since `unwrap_used`, `expect_used`, and `panic` are denied by clippy, every `Result` and `Option` **must** be handled explicitly:
  - Use `match` or `if let` branches for control flow.
  - Use `anyhow::Context` (`context()` / `with_context()`) to attach meaningful error context instead of `unwrap()` / `expect()`:
    ```rust
    // GOOD
    let data = file.read_to_end().context("failed to read config file")?;
    
    // BAD — will not compile
    let data = file.read_to_end().unwrap();
    ```
  - For `Option` values that must exist, use `context("...")?` or `ok_or_else(|| anyhow!("..."))?` — never `.unwrap()`.
- `if`/`match` branching on errors is not optional — it is required. Every fallible operation must have explicit error handling visible in the code.
- `?` operator is the preferred propagation method for fallible functions.

## Workspace organization (mandatory)
- All crates must be declared in the root `Cargo.toml` workspace members list.
- Local workspace crates must use path imports from root:
  ```toml
  <crate> = { path = "<relative-path>" }
  ```
- No crate is allowed to have its own independent `Cargo.toml` dependencies outside the workspace — all dependencies must be centralized at the workspace level.
- If you find a crate outside the workspace setup, move it into the workspace and register it in root.
