---
name: evo
description: >-
  Self-evolution skill for pipeline agents. Analyze your own mistakes,
  extract lessons, and log them for the Evolution agent to pick up.
  Use when you detect an error pattern in your work.
---

# /evo — Agent Self-Evolution

Analyze your own mistakes and log evolution entries for the Evolution agent.

## Usage

```
/evo <describe what went wrong>
```

## Workflow

### 1. Identify the Error

Classify what went wrong:

| Type | Description | Example |
|------|-------------|---------|
| **Spec error** | Ambiguous or incomplete requirement | Criterion says "fast" without threshold |
| **Plan error** | Architecture doesn't account for reality | Missing edge case in plan |
| **Code error** | Implementation diverges from plan | Added feature not in spec |
| **Test error** | Tests don't catch the actual issue | Mocks where integration needed |
| **Process error** | Skipped a step, wrong workflow | Coded before plan was approved |

### 2. Root Cause

Answer:
- What assumption was wrong?
- Where in the pipeline could this have been caught earlier?
- Is this a one-off or a pattern?

### 3. Log the Evolution

Append to `.ievo/evolution/<your-agent-name>.md`:

```markdown
## YYYY-MM-DD: <brief title>

**Type:** <error type from table above>
**What happened:** <1-2 sentences>
**Root cause:** <why it happened>
**Lesson:** <actionable rule to prevent recurrence>
```

### 4. Continue Working

Don't stop for lengthy analysis. Log the entry and move on. The Evolution agent will pick it up at the next pipeline gate and decide whether to create a curator issue.

## Rules

- **Speed over ceremony.** Log the lesson in 30 seconds, don't write an essay.
- **Honest self-assessment.** Don't blame other agents. What could YOU have done differently?
- **No sensitive data.** Evolution logs are public. No tokens, paths, or PII.
- **One lesson per entry.** Don't bundle multiple issues into one log.
