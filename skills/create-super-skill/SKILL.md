---
name: create-super-skill
description: Creates high-quality Claude Code skills following official best practices. Use when creating a new skill, improving an existing skill, or when the user asks to build a skill/slash-command. Loads fresh documentation on skill authoring.
argument-hint: "[skill-name] [brief description]"
---

# Create Super Skill

Create well-structured, effective Claude Code skills following official Anthropic best practices.

## Workflow

### 1. Gather Requirements

Do NOT jump into writing code immediately. Ask the user clarifying questions first.
If any of the following is unclear — ask before proceeding:

- **Purpose**: What should the skill do? What problem does it solve?
- **Trigger**: When should it activate? (user-only `/slash`, auto-invocation, or both)
- **Side effects**: Does it modify files, make API calls, commit code? (→ `disable-model-invocation: true`)
- **Tools needed**: Which tools does the skill require? (Read, Write, Bash, Grep, MCP tools)
- **Scope**: Project skill (`.claude/skills/`) or personal (`~/.claude/skills/`)?
- **Auto-discovery**: Should the model invoke this skill automatically when it detects a matching context? Or should it be user-only (`/slash`)? Skills with destructive side effects (deploy, commit, send) MUST be `disable-model-invocation: true`.

#### Check for duplicates

Before creating a new skill, scan existing skills:
```bash
ls .claude/skills/*/SKILL.md ~/.claude/skills/*/SKILL.md 2>/dev/null
```

Read the `description` of each existing skill. If a skill with **similar purpose** already exists:
- **Tell the user** which skill overlaps and what it does
- **Propose alternatives**: extend the existing skill, rename for specificity, or confirm the user wants a separate one
- Do NOT silently create a duplicate

#### Look at existing patterns

Check the project's existing skills for style and structure conventions to follow.

Only proceed to step 2 when you have a clear understanding of what the user wants.

### 2. Load Reference Documentation

Before writing any skill content, fetch the **latest official documentation** from the web.
This is mandatory — do NOT rely on training data, always read fresh docs.

Read these pages (in order of priority):

1. **Best practices**: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices
2. **Claude Code skills**: https://code.claude.com/docs/en/skills
3. **Skills overview**: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview

Focus on the best practices and frontmatter reference sections — they contain the rules for writing effective skills.
There are no local fallback files — Claude Code requires internet, so web fetch always works.

### 3. Design the Skill

Based on requirements and best practices:

1. **Choose the name**: lowercase, hyphens, gerund or action form (`processing-pdfs`, `fix-issue`)
2. **Write the description**: 3rd person, specific, includes both WHAT and WHEN. Max 1024 chars.
3. **Decide on freedom level**:
   - **High** (text instructions): multiple valid approaches, context-dependent
   - **Medium** (pseudocode/templates): preferred pattern exists
   - **Low** (exact scripts): fragile operations, consistency critical
4. **Plan file structure**:
   - Simple skill → just `SKILL.md`
   - Complex skill → `SKILL.md` + reference files (one level deep, no nesting)
   - With scripts → add `scripts/` directory

### 4. Write SKILL.md

Follow these rules:
- **Be concise**: Claude is smart. Only add context Claude doesn't already have.
- **Under 500 lines**: Split into separate files if approaching this limit.
- **Progressive disclosure**: Keep SKILL.md as overview, link to details.
- **No time-sensitive info**: Use "Current method" / "Old patterns" sections.
- **Consistent terminology**: Pick one term and use it throughout.

Required YAML frontmatter:
```yaml
---
name: my-skill-name          # ≤64 chars, lowercase+hyphens only
description: >-              # ≤1024 chars, 3rd person, no XML tags
  Does X and Y. Use when Z happens
  or the user asks for W.
---
```

Optional frontmatter fields (Claude Code):
```yaml
argument-hint: "[arg1] [--flag]"
disable-model-invocation: true    # user-only invocation
user-invocable: false             # model-only (background knowledge)
allowed-tools: Read, Grep, Bash   # restrict tool access
context: fork                     # run in subagent
agent: Explore                    # subagent type (Explore/Plan/custom)
```

### 5. Add Supporting Files (if needed)

For reference files:
- Link directly from SKILL.md (one level deep — no chain references)
- Add table of contents for files >100 lines
- Name descriptively: `form-validation-rules.md`, not `doc2.md`

For scripts:
- Handle errors explicitly (don't punt to Claude)
- No magic numbers — document all constants
- Make execution intent clear in SKILL.md: "Run X" vs "See X for reference"

### 6. Validate the Skill

Checklist (copy and check off):
```
Skill Quality:
- [ ] description is specific, includes WHAT + WHEN
- [ ] description is 3rd person
- [ ] SKILL.md body < 500 lines
- [ ] No time-sensitive information
- [ ] Consistent terminology
- [ ] Concrete examples (not abstract)
- [ ] File references one level deep
- [ ] Workflows have clear steps
- [ ] Scripts handle errors explicitly
- [ ] No voodoo constants
- [ ] Forward slashes in all paths
```

### 7. Test the Skill

1. Verify discovery: ask Claude "What skills are available?"
2. Test with a real request matching the description
3. If skill has `/slash` command, invoke directly
4. Check that Claude loads only relevant files (progressive disclosure working)

## Communication

- Speak to user in **Russian**
- Write skill content (SKILL.md, code, comments) in **English**
- Present the complete skill structure before creating files
- Get user approval before writing

## Anti-Patterns

- **Verbose explanations** of things Claude already knows
- **Deeply nested references** (file A → file B → file C)
- **Vague descriptions** ("Helps with stuff")
- **Too many options** without a clear default
- **Windows-style paths** (`\` instead of `/`)
- **Inconsistent point-of-view** in description (use 3rd person)
- **Missing error handling** in scripts
