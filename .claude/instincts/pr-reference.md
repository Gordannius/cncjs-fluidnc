---
id: cncjs-pr-reference
trigger: when creating a commit for a merged PR
confidence: 0.85
domain: git
source: local-repo-analysis
priority: medium
analyzed_commits: 200
---

# Include PR Number in Commit Messages

## Action

When committing work that's associated with a pull request, include the PR number at the end of the commit message in the format `(#NUMBER)`.

**Format:**

```
<type>(<scope>): <description> (#PR-number)
```

## Evidence

- 56% of commits (112 out of 200) include PR references
- This is a strong project convention
- PR numbers appear at the end of the subject line in parentheses

## Examples

**Good:**

```
feat: add Grbl v1.1 simulator (#950)
fix: upgrade to @electron/rebuild for Python 3.12 compatibility (#949)
chore(deps): bump http-proxy-middleware from 2.0.7 to 2.0.9 (#915)
refactor(grbl-simulator): improve GRBL simulator functionality (#952)
```

**When to skip:**

- Direct commits to master without PR (rare, usually releases)
- Hot fixes that don't go through PR process
- Release commits: `chore(release): publish 1.10.7`

## Automation Tip

If using `gh` CLI to create commits after merging a PR, you can automatically include the PR number:

```bash
# Get the PR number from gh
PR_NUM=$(gh pr view --json number -q .number)
git commit -m "feat: add feature (#${PR_NUM})"
```
