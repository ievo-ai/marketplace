---
name: extract-best-practices
description: >-
  Analyze the current session to extract reusable patterns, workflows, and
  best practices. Proposes creating new skills or updating existing ones.
  Use after long sessions, when the user says "/extract-best-practices",
  or when a repeatable pattern emerges. This is /ievo for the skill library.
---

# Extract Best Practices

Analyze session history to identify reusable patterns and evolve the skill library.

## When to Use

- After a long or complex session with repeatable patterns
- When a multi-step workflow was performed that could be standardized
- When the user explicitly asks to extract or capture a best practice
- When you notice you're repeating the same sequence of actions across sessions

## Workflow

### 1. Analyze the Session

Review the conversation history and identify:

- **Repeated patterns**: sequences of actions performed multiple times
- **Multi-step workflows**: complex tasks that followed a consistent order
- **Domain knowledge**: specialized information that was researched and applied
- **Decision frameworks**: how choices were made (tradeoffs, criteria)
- **Error-recovery patterns**: how mistakes were caught and fixed

Produce a bullet list of candidate patterns (max 5).

### 2. Scan Existing Skills

List all existing skills:
```bash
ls .claude/skills/*/SKILL.md 2>/dev/null
ls src/ievo/marketplace/skills/*/SKILL.md 2>/dev/null
```

For each candidate pattern, check:
- Does an existing skill already cover this? → propose **update**
- Is it a new capability? → propose **new skill**
- Is it too narrow to be a skill? → propose **evolution rule** (use `/ievo` instead)

### 3. Present Findings

For each candidate:

```
### Pattern: [name]
**Type**: new skill | update [existing-skill] | evolution rule (/ievo)
**Trigger**: when should this activate
**Summary**: 2-3 sentences describing what it captures
**Value**: why this saves time or prevents errors
**Example**: concrete example from this session
```

Ask the user to select which patterns to act on (can be multiple).

### 4. Create or Update

For **new skills**:
- Use `/create-super-skill` to build the skill properly
- Deploy to `src/ievo/marketplace/skills/{name}/`
- Symlink: `.claude/skills/{name}` → marketplace source

For **skill updates**:
- Read the existing SKILL.md
- Propose specific additions/modifications
- Get approval before editing

For **evolution rules** (too narrow for a skill):
- Delegate to `/ievo` — writes to `.ievo/ievolution/KERNEL.md` or `agents/<name>.md`

### 5. Validate

- Confirm the skill description triggers correctly (would Claude invoke it?)
- Check for overlaps or conflicts with existing skills
- No duplicate logic between skills and evolution overlays

### 6. Summary

```
| Action | Target | Description |
|--------|--------|-------------|
| Created | skill-name | What it does |
| Updated | skill-name | What changed |
| Deferred | pattern-name | Why (too narrow, appeared only once) |
```

## Guidelines

- **Generalize**: extract the pattern, not the specific instance
- **Threshold**: a pattern should appear at least 2x or be clearly reusable
- **One skill = one concern**: don't create mega-skills
- **Defer when unsure**: note patterns that appeared only once, revisit later
- **Skills vs evolution**: repeated workflow = skill. One-time lesson = `/ievo`

## Anti-Patterns

- Creating skills for one-off tasks that won't recur
- Duplicating logic already in evolution overlays (use `/ievo` instead)
- Over-engineering: a 200-line skill for a 3-step process
- Creating skills without user approval
