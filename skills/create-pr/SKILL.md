# /create-pr — Push Branch and Open PR

Called by **Coder** after implementation is verified. Pushes the feature branch, creates a PR with structured description, and notifies the user.

## Steps

1. **Check git state**
   ```bash
   git status --short
   ```
   If uncommitted changes exist → commit them first or ask via `AskUserQuestion`.

2. **Push branch**
   ```bash
   git push origin <current-branch>
   ```

3. **Build PR description** from:
   - REQ-xxx.md — title and acceptance criteria (what was built)
   - PLAN-REQ-xxx.md — Scope Guard (what was NOT built)
   - Test run output — test count and coverage
   - `.ievo/spec/SPEC_INDEX.md` — REQ link

   Format:
   ```
   ## What was implemented
   - <acceptance criterion 1> ✓
   - <acceptance criterion 2> ✓

   ## What was NOT implemented (Scope Guard)
   - <deferred item> → IDEA-NNN

   ## Tests
   - Added: N tests
   - Total: N passing
   - Coverage: 100%

   ## Spec
   REQ-xxx: .ievo/spec/requirements/REQ-xxx.md
   ```

4. **Create PR**
   ```bash
   gh pr create --title "REQ-xxx: <title>" --body "<description>"
   ```

5. **Check for merge conflicts**
   ```bash
   gh pr view <number> --json mergeable,mergeStateStatus
   ```
   - `mergeable: MERGEABLE` → ok
   - `mergeable: CONFLICTING` → STOP. Resolve conflicts locally, push, then re-check.
   - `mergeable: UNKNOWN` → wait 5s and retry once (GitHub is still computing).

6. **Notify user**
   Use `AskUserQuestion`: "PR #N created: <url>. No conflicts. Trigger Acceptance direction check?"
