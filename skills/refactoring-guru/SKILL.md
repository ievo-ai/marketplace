---
name: refactoring-guru
description: >-
  Deep refactoring workflow with expert panel review. Analyzes code
  architecture, proposes improvements using design patterns, and ensures
  test coverage before and after changes. Use when refactoring a file
  or module, or when the user says /refactoring-guru.
argument-hint: "<file_path>"
disable-model-invocation: true
---

# Refactoring Guru

Comprehensive refactoring workflow with multi-expert review panel.

## Usage

```
/refactoring-guru <file_path>
```

## Supporting Files

| File | Purpose |
|------|---------|
| [patterns.md](patterns.md) | Design patterns catalog from refactoring.guru |
| [proposal-template.md](proposal-template.md) | Structured proposal output format |

## Related Skills

- **fact-check** — use when recommending a new library or referencing an external package during analysis

## Expert Panel

Auto-detected from file content. Python Guru is always active.

| Condition | Expert |
|-----------|--------|
| complex class hierarchies, SRP violations | Architect |
| always | Python Guru |

## Workflow

### Phase 0: Scope

1. Read target file completely
2. Identify dependencies (files that import or are imported by target)
3. Assess complexity:
   - **High**: >300 lines, multiple classes, complex inheritance
   - **Medium**: 100-300 lines, 1-2 classes, moderate dependencies
   - **Low**: <100 lines, single class/module, few dependencies
4. Present scope to user and get confirmation before proceeding

### Phase 1: Expert Analysis

**Python Guru** (always):
- Type annotations, Pythonic idioms, error handling
- Naming conventions, keyword-only arguments where appropriate
- Docstring quality (Google style)

**Architect** (when complex class hierarchies detected):
- SRP violations, class cohesion, God objects
- Missing abstractions, circular imports
- Reference: https://refactoring.guru/refactoring/smells

Document findings per expert as:
```
### {Expert} Findings
**Issues:** numbered list with severity (High/Medium/Low)
**Recommendations:** numbered list
```

### Phase 2: Pattern Analysis

Read [patterns.md](patterns.md). Apply relevant design patterns to identified code smells. For each pattern, show before/after code snippets.

### Phase 3: Test Coverage

**Before any code changes**, ensure refactored code has full test coverage:

1. Run `uv run pytest --cov=<module> --cov-report=term-missing` on the target module
2. Identify uncovered lines that will be moved, renamed, or restructured
3. Write tests to cover those lines — focus on behavior, not implementation
4. Run the full suite — all green before proceeding

Key tests:
- **Characterization tests**: deterministic inputs → expected outputs. Guarantee refactoring doesn't change behavior.
- **Guard/edge-case tests**: empty input, missing data — cover early-return paths that move during refactoring.

### Phase 4: Synthesis & Proposal

Read [proposal-template.md](proposal-template.md). Compile all findings into a structured proposal with options.

### Phase 5: User Approval

Present proposal. Options:
1. **Approve** — proceed with implementation
2. **Discuss** — clarify specific points
3. **Modify** — adjust scope or approach
4. **Cancel** — abort refactoring

**Do NOT proceed without explicit approval.**

### Phase 6: Implementation

**Critical rules:**
- **Never mix refactoring with behavior changes.** API signature changes, new features, and bug fixes go in separate commits before or after the structural refactoring.
- **Each step = one commit with green tests.** If something breaks, `git revert` of a single commit is trivial.
- **Run tests after every commit**, not just at the end.

Steps:
1. Create feature branch if not already on one
2. Commit behavior/API changes first — separate from structural refactoring
3. Execute structural refactoring iteratively with `uv run pre-commit run --files <changed>` validation
4. One commit per logical chunk

### Phase 7: Finalization

1. Run full verification:
   ```bash
   uv run pre-commit run --all-files
   uv run pytest -x
   ```
2. Ask user whether to keep `.refactoring/{module}.md` plan file

## Communication

- Speak to user in their language
- Write code and comments in English
