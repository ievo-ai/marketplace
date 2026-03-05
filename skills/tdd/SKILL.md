---
name: tdd
description: >-
  6-phase TDD discipline enforcer. Use when implementing any non-trivial feature.
  Guides through Red → Green → Refactor with strict anti-pattern detection.
  Enforces 100% coverage on changed files.
argument-hint: "<feature or REQ-xxx to implement>"
---

# /tdd — Test-Driven Development Cycle

Enforces strict red-green-refactor discipline across 6 phases and 12 steps. Stops at 4 user checkpoints. Never skips a step.

## When to Use

- Implementing a new REQ spec
- Adding any non-trivial function or class
- Refactoring with safety net
- When Coder is tempted to write implementation first

## Phase Overview

```
Phase 1 — Spec & Design      Steps 1–2   → test architecture, no code
Phase 2 — RED                Steps 3–4   → failing tests only, verify failures
Phase 3 — GREEN              Steps 5–6   → minimal implementation, all pass
Phase 4 — REFACTOR           Steps 7–8   → cleanup, tests still green
Phase 5 — Extended Testing   Steps 9–11  → integration, edge cases, performance
Phase 6 — Final Review       Step 12     → coverage gate, 100% on changed files
```

## The 12 Steps

### Phase 1: Specification & Design

**Step 1 — Requirements analysis**
- Read the REQ spec (acceptance criteria are your test spec)
- Map each criterion to one or more test cases
- Output: test list (what to test, not how)

**Step 2 — Test architecture**
- Choose test types: unit, integration, edge cases
- Identify fixtures, mocks needed (only true external boundaries)
- Identify file structure
- **CHECKPOINT 1** → show plan, wait for approval before writing any code

### Phase 2: RED

**Step 3 — Write failing tests**
- Write ALL tests first. Zero production code.
- Arrange-Act-Assert pattern, one behavior per test
- Descriptive names: `test_<behavior>_when_<condition>`
- Edge cases: null, empty, boundary values, error paths

**Step 4 — Verify failures**
- Run tests: ALL must fail
- Each failure must have a meaningful error message
- If a test passes at RED → it's wrong. Fix it or delete it.
- **CHECKPOINT 2** → confirm all tests fail before proceeding

### Phase 3: GREEN

**Step 5 — Minimal implementation**
- Implement ONLY what the failing tests require
- "Fake it": hard-code values if a single test demands it
- "Triangulate": generalize only when multiple tests demand it
- NO features beyond what tests test

**Step 6 — Verify green**
- Run tests: ALL must pass
- No existing tests broken
- **CHECKPOINT 3** → confirm all tests pass, show coverage numbers

### Phase 4: REFACTOR

**Step 7 — Code quality**
Trigger refactoring if any of:
- Function > 20 lines
- Class > 200 lines
- Cyclomatic complexity > 10
- Duplication (3+ similar blocks)
- SOLID violation visible

Apply: extract method/class, rename for clarity, remove duplication.
Run tests after EVERY change. If tests break → revert immediately.

**Step 8 — Test quality**
- Remove test duplication
- Improve test names for clarity
- Ensure each test tests exactly one thing
- **CHECKPOINT 4** → review refactoring diff, confirm green

### Phase 5: Extended Testing

**Step 9 — Integration tests**
- Wire the new code into real system paths
- Test with real files (`tmp_path`), real objects — no mock substitutes

**Step 10 — Edge cases sweep**
- Unicode, whitespace, special characters
- Concurrent access (if applicable)
- Permission errors, missing files
- Min/max boundary values

**Step 11 — Performance (if applicable)**
- Add benchmark if function is on a hot path
- Document any known complexity

### Phase 6: Final Review

**Step 12 — Coverage gate**
- Run: `uv run pytest --cov --cov-report=term-missing <changed files>`
- 100% line coverage on ALL changed files — no exceptions
- If below 100%: identify uncovered lines → write tests → re-run
- Output summary: files changed, tests added, coverage achieved

## Anti-Pattern Detection

Stop and warn if:
- Implementation code written before tests (test-after)
- Any test passes during RED phase
- REFACTOR phase skipped ("I'll clean up later")
- Mocks used for non-external code (internal functions, utils)
- Test asserts only `.assert_called_once()` without checking real output
- Coverage below 100% marked as "good enough"

## State File

Save progress to `.tdd-cycle/state.json` after each step:

```json
{
  "feature": "REQ-042-user-login",
  "current_step": 6,
  "phase": "GREEN",
  "tests_written": 12,
  "tests_passing": 12,
  "coverage": 87,
  "files_changed": ["src/ievo/auth.py", "tests/test_auth.py"]
}
```

Resume with `/tdd --resume` after context loss.

## Modes

- **Default (suite)**: write all tests for the feature, then implement
- **Incremental** (`/tdd <feature> --incremental`): one failing test → implement → refactor → repeat

## iEvo Specifics

- Coverage threshold: **100%** (not 80% — see CLAUDE.md)
- Mock policy: real objects + real `tmp_path` filesystem. Mocks only for Docker daemon, network APIs, subprocess
- Guard conditions: satisfy with real config/env state, never mock internal app logic
- TUI tests: must cover focus on launch + keyboard navigation + primary actions

## Source

Adapted from [wshobson/agents](https://github.com/wshobson/agents) `plugins/tdd-workflows` — verified 2026-03-04.
