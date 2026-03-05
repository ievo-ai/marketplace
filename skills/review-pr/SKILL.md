# /review-pr — Code Review a PR

Called by **Code-reviewer** after Acceptance direction check passes. Reviews code quality, style, security, test completeness.

## Steps

1. **Get PR diff**
   ```bash
   gh pr diff <number>
   gh pr view <number> --json files
   ```

2. **Read changed files** — understand what changed and why (cross-reference REQ + PLAN)

3. **Review checklist**
   - Code follows project conventions (CLAUDE.md, DECISIONS.md)
   - No security issues (injection, secrets in code, unsafe operations)
   - Tests are real (not mock-only for non-external boundaries)
   - No scope creep (code not in the spec)
   - No dead code or commented-out blocks
   - Error paths handled

4. **Verdict**

   **PASS** — no blocking issues:
   ```bash
   gh pr review <number> --approve --body "Code review ✓"
   ```
   If `gh pr review --approve` fails with "Can not approve your own pull request" →
   fall back to a comment: `gh pr comment <number> --body "Code review ✓ ..."` — this is expected when reviewer and author share the same GitHub account (dev environment).

   Return: `PASS`

   **FAIL** — blocking issues found:
   ```bash
   gh pr review <number> --request-changes --body "<issues>"
   ```
   Save report to `.ievo/reports/review/REVIEW-REQ-xxx.md`
   Set requirement status → `in-progress` in SPEC_INDEX.md.
   Return: `FAIL: <list of blocking issues>`
