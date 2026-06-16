---
paths:
  - "**/*.ts"
  - "**/*.tsx"
  - "**/*.js"
  - "**/*.jsx"
  - "**/*.rs"
  - "**/*.toml"
  - "**/package.json"
  - "**/biome.json"
---

# Tooling Preferences

## Package manager
- Use **bun** over npm, pnpm, or yarn for all JS/TS projects.
- Prefer `bun run <script>`, `bun add <pkg>`, `bun install`.

## Linting / formatting
- Use **biome** over eslint and prettier — it handles both linting and formatting in a single tool.
- Run `bun run lint` or `bunx biome check` rather than `npx eslint`.

## Rust
- Use **cargo clippy** over `cargo check` — it catches more issues.
