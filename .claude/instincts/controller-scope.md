---
id: cncjs-controller-scope
trigger: when modifying CNC controller code
confidence: 0.90
domain: architecture
source: local-repo-analysis
priority: high
analyzed_commits: 200
---

# Use Controller-Specific Scopes for Controller Changes

## Action

When modifying code related to a specific CNC controller (Grbl, Marlin, TinyG, or Smoothie), use the controller name as the scope in your commit message.

**Scope naming:**

- `(Grbl)` or `(grbl)` - for Grbl controller changes
- `(grbl-simulator)` - for GRBL simulator changes
- `(Marlin)` - for Marlin controller changes
- `(TinyG)` - for TinyG controller changes
- `(Smoothie)` - for Smoothie controller changes
- `(g2core)` - for g2core controller changes

## Evidence

Most frequently modified files show controller-specific patterns:

- `src/server/controllers/Grbl/GrblController.js` - 16 changes
- `src/server/controllers/Marlin/MarlinController.js` - 13 changes
- `src/server/controllers/TinyG/TinyGController.js` - 12 changes
- `src/server/controllers/Smoothie/SmoothieController.js` - 12 changes

Controller-scoped commits found:

```
refactor(grbl-simulator): improve GRBL simulator functionality (#952)
fix(grbl): address a regression in PR #889 related to the `grbl-Mega` connection handling (#893)
feat(Grbl): support UART communication without resetting the connection upon opening (#880)
feat(Grbl): enhance Grbl parser to resolve issues with specific Grbl forks (#883)
feat(g2core): add `jogCancel` command to cancel jogging using feedhold and queue flush (#876)
feat(Marlin): add support for parsing temperature data for heated chamber, cooler, and other temperature states (#832)
```

## When to Apply

- Modifying files in `src/server/controllers/{Controller}/`
- Changing controller-specific widgets in `src/app/widgets/{Controller}/`
- Adding tests in `src/server/controllers/{Controller}/__tests__/`
- Updating controller-specific parsers or utilities

## Architecture Context

Each controller has:

```
src/
├── server/controllers/{Controller}/
│   ├── {Controller}Controller.js
│   ├── {Controller}LineParser.js
│   ├── {Controller}LineParserResult*.js
│   └── __tests__/
└── app/widgets/{Controller}/
    ├── index.js
    └── constants.js
```

Changes often span both server and app directories but keep the same scope.
