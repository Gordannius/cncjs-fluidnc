---
id: cncjs-test-organization
trigger: when creating or modifying tests
confidence: 0.92
domain: testing
source: local-repo-analysis
priority: high
analyzed_commits: 200
---

# Organize Tests in __tests__ Directories with .test.js Extension

## Action

Place test files in `__tests__/` directories adjacent to the code being tested, with `.test.js` extension.

**Pattern:**

```
src/server/
├── lib/
│   ├── Sender.js
│   └── __tests__/
│       └── Sender.test.js
├── controllers/
│   ├── Grbl/
│   │   ├── GrblController.js
│   │   ├── GrblRunner.js
│   │   └── __tests__/
│   │       └── GrblRunner.test.js
│   └── Marlin/
│       ├── MarlinController.js
│       ├── MarlinRunner.js
│       └── __tests__/
│           └── MarlinRunner.test.js
```

## Evidence

Test files found in the repository follow this pattern:

```
src/server/lib/__tests__/Sender.test.js
src/server/lib/__tests__/evaluate-assignment-expression.test.js
src/server/lib/__tests__/evaluate-expression.test.js
src/server/lib/__tests__/translate-expression.test.js
src/server/controllers/Grbl/__tests__/GrblRunner.test.js
src/server/controllers/Marlin/__tests__/MarlinRunner.test.js
src/server/controllers/Smoothie/__tests__/SmoothieRunner.test.js
src/server/controllers/TinyG/__tests__/TinyGRunner.test.js
src/server/controllers/utils/__tests__/gcode.test.js
grbl-simulator/__tests__/grbl-simulator.test.js
```

Jest configuration confirms this pattern:

```json
{
  "testMatch": [
    "<rootDir>/src/server/**/__tests__/**/*.test.js",
    "<rootDir>/grbl-simulator/__tests__/**/*.test.js"
  ]
}
```

## Migration Note

The project **migrated from tap to Jest** in January 2026:

```
refactor: migrate from tap to jest testing framework
```

Use Jest syntax, not tap syntax, for all new tests.

## Running Tests

```bash
yarn test              # Run all tests with coverage
```

## Coverage Configuration

Tests cover server-side code only:

```json
{
  "collectCoverageFrom": [
    "<rootDir>/src/server/**/*.js",
    "!<rootDir>/src/server/**/*.test.js",
    "!<rootDir>/src/server/**/__tests__/**"
  ]
}
```

## Test Environment

- **Framework**: Jest 29
- **Environment**: Node.js (`testEnvironment: "node"`)
- **Timeout**: 10 seconds per test
- **Coverage**: Enabled by default
