---
paths:
  - "**/*.ts"
  - "**/*.tsx"
  - "**/package.json"
  - "**/tsconfig.json"
  - "**/biome.json"
---

# TypeScript Project Rules

## Package manager (mandatory)
- Only **bun** is allowed. Never use npm, pnpm, yarn, or npx.
- All package operations must go through bun: `bun add`, `bun remove`, `bun install`, `bun run`.

## package.json
- Never edit `package.json` directly. No manual writes, no sed/awk/echo patching.
- All dependency changes must be done through `bun add <pkg>` or `bun remove <pkg>`.
- Exception: `bun add` doesn't support some fields (e.g. `trustedDependencies`, `overrides`, `workspaces`) — for those, ask the user before editing directly.

## Required package.json scripts
Every TypeScript project must configure these scripts in `package.json`:

| Command | Runs |
|---------|------|
| `bun run lint` | `biome lint` |
| `bun run format` | `biome format --write` |
| `bun run check` | `tsc --noEmit` |

Configure via `bun x biome init` first (do not manually edit `package.json`).

## Version pinning
- Do not pin specific package versions. Let `bun add` resolve the latest compatible version.
- Exception: if the user explicitly requests a specific version, or if a known breaking change requires pinning, add a `// pinned because: <reason>` comment above the dependency.

## Linting & formatting (mandatory)
- Use **biome** only. No eslint, prettier, or any other linting/formatting tool.
- Validate with `bun run lint`.
- Format with `bun run format`.
- Auto-fix both with `bunx biome check --write`.

## Type checking
- Use `bun run check` (`tsc --noEmit`) as your primary type-checking command — run it frequently during development.
- For **Next.js projects**: do NOT run `next build` repeatedly. Use `tsc --noEmit` for all intermediate checks. Only run `next build` once at the very end, before delivering the comprehensive report, as a final verification.

## Code style
- Strings: use double quotes `"` — never single quotes.
- Indentation: 4 spaces per level. No tabs.
- Semicolons required at end of every statement.
- Trailing commas where syntax allows.

## React components
- Use function components only. No class components.
- Every component gets a named props interface and a default export:

```typescript
export interface ComponentNameProps {
    // typed props here
}

export default function ComponentName(props: ComponentNameProps) {
    return (<></>);
}
```

- Props interface name must match `{ComponentName}Props`.
- Export the interface (for external usage) and default-export the function.
