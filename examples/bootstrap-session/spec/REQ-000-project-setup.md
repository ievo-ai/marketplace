# REQ-000: Project Setup

## Metadata
- **Status:** ready
- **Priority:** 0
- **Dependencies:** none
- **Created:** <date>
- **Implemented:**

## Context

This is the very first requirement. No code exists yet.
This requirement establishes the project skeleton so that all subsequent
requirements have a working test runner, linter, and project structure.

## Acceptance Criteria

<!--
CUSTOMIZE THIS for your stack. Examples below — pick your stack and delete the rest.
-->

### Option A: Node.js / TypeScript
- [ ] `package.json` exists with project name and test script
- [ ] TypeScript compiles without errors (`npx tsc --noEmit` exits 0)
- [ ] Test runner is configured (Jest or Vitest) and `npm test` runs successfully
- [ ] A sample test file exists and passes: `expect(true).toBe(true)`
- [ ] Linter is configured (ESLint) and `npm run lint` passes
- [ ] `src/` and `tests/` directories exist
- [ ] `.gitignore` includes node_modules, dist, coverage

### Option B: Python
- [ ] `pyproject.toml` or `setup.py` exists with project metadata
- [ ] pytest is configured and `pytest` runs successfully
- [ ] A sample test file exists and passes: `assert True`
- [ ] Linter is configured (ruff or flake8) and passes
- [ ] `src/` and `tests/` directories exist
- [ ] `.gitignore` includes __pycache__, .venv, .pytest_cache

### Option C: Go
- [ ] `go.mod` exists with module name
- [ ] `go test ./...` runs successfully
- [ ] A sample test file exists and passes
- [ ] `golangci-lint run` passes (if installed)
- [ ] `.gitignore` includes binaries

### Option D: Other
- [ ] <Define your stack setup criteria here>

## Negative Acceptance Criteria

- This does NOT include any business logic
- This does NOT include CI/CD pipeline (add as separate REQ if needed)
- This does NOT include Docker configuration

## Technical Notes

<!--
Specify your stack choice here. The agent will use this to make setup decisions.
Example: "Use TypeScript 5.x, Vitest for testing, ESLint with flat config"
-->

Stack: <FILL IN YOUR STACK HERE>
