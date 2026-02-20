---
id: cncjs-yarn-package-manager
trigger: when managing dependencies
confidence: 0.98
domain: package-management
source: local-repo-analysis
priority: critical
analyzed_commits: 200
---

# Always Use Yarn for Package Management

## Action

**Use `yarn` exclusively** for package management in this project. Do not use `npm`.

**Correct commands:**

```bash
yarn install           # Install dependencies
yarn add <package>     # Add dependency
yarn add -D <package>  # Add dev dependency
yarn remove <package>  # Remove dependency
yarn upgrade <package> # Upgrade dependency
```

**Incorrect:**

```bash
npm install     # ❌ Never use npm
npm i <package> # ❌ Never use npm
```

## Evidence

1. **Lock file**: Project uses `yarn.lock` (19 commits modifying it), not `package-lock.json`
2. **Package manager field**: Not explicitly set, but all scripts use `yarn`
3. **Dependency update pattern**: All 39 `chore(deps)` commits show `yarn.lock` changes

Recent dependency updates show yarn usage:

```
chore(deps): bump http-proxy-middleware from 2.0.7 to 2.0.9 (#915)
chore(deps): bump @babel/runtime from 7.20.13 to 7.27.6 (#923)
chore(deps): bump @babel/runtime-corejs2 from 7.20.13 to 7.26.10 (#910)
```

## File Co-Change Pattern

`package.json` and `yarn.lock` **always change together**:

- `package.json` - 64 commits
- `yarn.lock` - 19 commits
- **100% correlation** when dependencies are updated

## Build Scripts

All build scripts in `package.json` assume yarn:

```json
{
  "scripts": {
    "dev": "yarn run build-dev && concurrently ...",
    "lint": "concurrently ... \"yarn i18nlint\" \"yarn eslint\" \"yarn stylint\""
  }
}
```

## Why This Matters

Using `npm` would:
- Generate `package-lock.json` (conflict with `yarn.lock`)
- Potentially install different versions of dependencies
- Break CI/CD pipelines expecting `yarn.lock`
- Violate project conventions

## Node Version

Minimum Node.js version: **18+**

```json
{
  "engines": {
    "node": ">=18"
  }
}
```
