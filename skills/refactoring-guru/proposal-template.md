# Proposal Template

Use this template for Phase 4 synthesis.

---

```markdown
## Refactoring Proposal: `{file_name}`

### Executive Summary
{1-2 sentence overview of goals and expected outcomes}

### Code Smells

| # | Smell | Severity | Location |
|---|-------|----------|----------|
| 1 | {description} | High/Medium/Low | L{line} |

### Proposed Architecture

#### Option A: {approach_name}
{description with before/after comparison}

#### Option B: {alternative} (if applicable)
{alternative description}

### Design Patterns

| Pattern | Purpose | Reference |
|---------|---------|-----------|
| {Pattern} | {why} | [Link](https://refactoring.guru/design-patterns/{pattern}) |

### Breaking Changes
- {API changes, or "None"}

### Implementation Plan

| Step | Description | Files Affected |
|------|-------------|----------------|
| 1 | {step} | `{file}` |

### Rollback Strategy
{how to revert if something goes wrong}
```

---

Present to user with options:
1. **Approve** — proceed
2. **Discuss** — clarify points
3. **Modify** — adjust scope
4. **Cancel** — abort
