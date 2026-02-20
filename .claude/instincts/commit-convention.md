---
id: cncjs-commit-convention
trigger: when writing a commit message
confidence: 0.95
domain: git
source: local-repo-analysis
priority: high
analyzed_commits: 200
---

# Use Conventional Commits with Common Types

## Action

Follow the conventional commit format with these type prefixes:

```
<type>(<scope>): <description>
```

**Most common types (in order of usage):**

1. `chore` - Dependencies, releases, maintenance (39% of commits)
2. `feat` - New features (38% of commits)
3. `fix` - Bug fixes (13% of commits)
4. `build` - Build system changes (8%)
5. `docs` - Documentation (5%)
6. `refactor` - Code restructuring (4%)
7. `ci` - CI/CD changes (2%)
8. `test` - Testing (1%)

**Common scopes:**

- Controller-specific: `(grbl)`, `(Grbl)`, `(Marlin)`, `(TinyG)`, `(Smoothie)`, `(grbl-simulator)`
- UI: `(widgets/Axes)`, `(widgets/*)`, `(app)`
- i18n: `(l10n)`, `(i18n)`
- Dependencies: `(deps)`, `(deps-dev)`
- Release: `(release)`

## Evidence

- Analyzed 200 commits from cncjs repository
- 110+ commits use strict conventional commit format
- Type distribution:
  - chore: 39 commits
  - feat: 38 commits
  - fix: 13 commits
  - build: 8 commits
  - docs: 5 commits
  - refactor: 4 commits
  - ci: 2 commits
  - test: 1 commit

## Examples

**Good:**

```
feat(widgets/Axes): Replace GridSystem with flexbox layout in MDI component (#955)
fix: resolve ESLint Babel parsing errors
chore(deps): bump @babel/runtime from 7.20.13 to 7.27.6 (#923)
refactor: migrate from tap to jest testing framework
```

**Bad:**

```
Updated some files
Fixed bug
WIP
Merge branch 'master'
```

## When NOT to Apply

- Merge commits (these have their own format)
- Revert commits (use `revert:` prefix)
- Initial commits (use `chore: initial commit` or similar)
