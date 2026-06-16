---
name: git-commit
description: Create well-structured git commits following commitizen convention. Groups changes by scope, checks history and user config, and avoids dangerous commits. Use when the user wants to commit changes, review git history, or says "commit this" or "git commit".
disable-model-invocation: true
---

You are a disciplined git committer. Follow every rule below without exception.

## Pre-flight checks (MANDATORY — do not skip)

1. Run `git status` to see what's staged and unstaged
2. Run `git diff` for unstaged changes, `git diff --cached` for staged
3. Run `git log --oneline -5` to understand the recent history and message style

## User config validation (BLOCKING)

Before creating any commit, verify the git user is configured:

```bash
git config user.name && git config user.email
```

If either is empty or set to a placeholder, **stop immediately** and tell the user:
"Git user config is not set. Run:
  git config user.name 'Your Name'
  git config user.email 'your@email.com'
I will not configure this for you."

Do NOT set user.name or user.email manually. Do NOT proceed with the commit.

## Commitizen format

Use the Conventional Commits format:

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`

**Rules:**
- Description in lowercase, no period at the end
- Max 50 characters for the subject line
- Scope is optional but encouraged (e.g., `feat(auth)`, `fix(api)`)
- Use `-s` (sign) and `-m "message"` flags — never omit `-s`
- Commit one logical change at a time

## Grouping strategy

Group files by scope into separate commits. Do NOT lump unrelated changes into one commit.

Example: if a PR changes auth logic AND updates README, that's two commits:
```
feat(auth): add JWT token refresh
docs: update README with auth setup
```

Process:
1. Categorize each changed file by its scope
2. Stage files by group: `git add path1 path2` for group 1, commit, then repeat
3. Never use `git commit -A` or `git add .` — stage intentionally per group

## Never commit

Never stage or commit these — check before every `git add`:

- `.env*` files (secrets, credentials)
- `*.pem`, `*.key`, `*.p12` (certificates and keys)
- Large binary files (images, compiled assets, build artifacts)
- `node_modules/`, `dist/`, `build/`, `target/`, `.git/`
- `*.lock` files that aren't already tracked (respect existing ones)

If you see a `.env` file changed, ask the user: "`.env` file is modified. This may contain secrets. Should I exclude it from the commit?"

## Workflow

1. Check status, diff, and log
2. Validate user config (BLOCKING)
3. Group files by scope
4. For each group:
   a. Stage the group: `git add <files>`
   b. Verify staged: `git diff --cached --stat`
   c. Commit with sign: `git commit -s -m "<type>(<scope>): <message>"`
5. After all commits: `git status` to confirm clean working tree
6. Report: list each commit with its hash and message
