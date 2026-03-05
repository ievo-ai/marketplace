# /review-acceptance-pr — PR Direction Check

Called by **Acceptance** when Coder opens a PR. Fast check: did Coder build the right thing?

This is intentionally **shallow** — reads PR description and REQ, does NOT read code. Speed matters.

## Steps

1. **Read PR description**
   ```bash
   gh pr view <number> --json title,body,url
   ```

2. **Read REQ** — extract all acceptance criteria

3. **Check each criterion**
   For each criterion in REQ:
   - Is it addressed in the PR description? YES / NO / PARTIAL

4. **Verdict**

   **PASS** — all criteria addressed:
   - Comment on PR: "Direction check ✓ — proceeding to code review"
   - Return: `PASS`

   **FAIL** — any criterion missing or wrong:
   - Comment on PR listing exactly which criteria are missing/wrong
   - Set REQ status → `in-progress` in SPEC_INDEX.md
   - Return: `FAIL: <list of missing criteria>`
