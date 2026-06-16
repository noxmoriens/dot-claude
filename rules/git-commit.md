---
paths:
  - ".git/*"
  - ".gitignore"
---

# Git Commit Conventions

## Commit messages
- Follow [Conventional Commits](https://www.conventionalcommits.org/) format: `<type>(<scope>): <description>`
- Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`
- Description in lowercase, no trailing period, max 50 characters
- Always sign commits with `-s` flag: `git commit -s -m "..."`
- Group changes by scope into separate commits — never mix unrelated changes

## Dangerous patterns (NEVER do these)
- `git commit -A` or `git add .` — always stage intentionally per group
- Never manually set `user.name` or `user.email` — ask the user to configure them
- Never commit secrets: `.env*`, `*.pem`, `*.key`, `*.p12`
- Never commit large binaries or build artifacts: `node_modules/`, `dist/`, `build/`, `target/`
- If `.env` appears in changes, flag it to the user before committing

## Pre-commit discipline
- Always run `git status`, `git diff`, and `git log --oneline -5` before committing
- Verify `git config user.name` and `git config user.email` are set — if empty, stop and ask the user
- Review staged changes with `git diff --cached --stat` before each commit
