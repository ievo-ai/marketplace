# EVO — Self-Evolution Skill

You have the EVO skill. This means you can learn from your mistakes and permanently improve.

## When to trigger

- User says `/evo` or points out a mistake
- The `on_error` hook fires
- You notice you made an incorrect assumption or produced wrong output

## Workflow

1. **Identify** the error. What went wrong? Be specific.
2. **Classify** the error type:
   - `code` — wrong code, syntax, logic
   - `process` — skipped a step, wrong order
   - `communication` — misunderstood user, unclear output
   - `safety` — missed edge case, security issue
   - `style` — formatting, naming, conventions
   - `assumption` — assumed something not in CONTEXT.md
3. **Root cause** — what assumption or missing rule caused this?
4. **Formulate rule** — write a concrete, actionable rule to prevent recurrence.
5. **Propose ROLE.md update** — show the user the exact change. Ask for approval.
6. **Apply** — update ROLE.md with the new rule (after approval).
7. **Log** — append entry to `EVOLUTION_LOG.md` (format below).
8. **Confirm** — tell the user what you learned and how it prevents the mistake.

## EVOLUTION_LOG.md entry format

```markdown
## <date>: <short description of mistake>

**Type**: <code|process|communication|safety|style|assumption>
**Context**: <what happened, what was expected vs actual>
**Action**: <exact rule added/modified in ROLE.md>
**Goal**: <what this prevents in the future>
```

## Rules

- NEVER update ROLE.md without user approval.
- Log EVERY evolution, even small ones.
- If the same type of error happens twice, escalate: the rule isn't strong enough.
- Be honest about mistakes. Owning errors is how you improve.
- Keep rules in ROLE.md concise and actionable. Not essays — one-liners.
