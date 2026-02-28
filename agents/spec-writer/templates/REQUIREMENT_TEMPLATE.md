# REQ-XXX: <Title>

## Metadata
- **Status:** draft
- **Priority:** <1-10, where 1 is highest>
- **Dependencies:** <REQ-YYY, REQ-ZZZ | none>
- **Created:** <date>
- **Implemented:** <date or empty>

## Context

<!--
IMPORTANT: This section must be SELF-CONTAINED.
The agent reads ONLY this file when implementing.
Include everything it needs to know about the existing system state.
Do NOT write "see REQ-001" — copy the relevant facts here.
-->

Describe what already exists in the system that this requirement interacts with.
Mention specific models, endpoints, modules, and their behavior.

## Acceptance Criteria

<!--
Each criterion = one testable behavior.
Format: Given <precondition> → When <action> → Then <expected result>
Be SPECIFIC about inputs and outputs. No vague language.
-->

- [ ] `<action with specific input>` → `<specific expected output/behavior>`
- [ ] `<action with specific input>` → `<specific expected output/behavior>`
- [ ] `<edge case / error input>` → `<specific error response/behavior>`

## Negative Acceptance Criteria

<!--
What this requirement explicitly does NOT do.
Prevents the agent from over-building.
-->

- This does NOT include <feature X> (see REQ-ZZZ)
- This does NOT handle <edge case Y> — that is out of scope

## Technical Notes

<!--
Optional. Architecture hints, constraints, conventions.
Only include if there are hard technical requirements (e.g., "must use library X").
Leave empty if the agent should decide implementation details.
-->

## Examples

<!--
Optional but recommended. Concrete input/output examples help the agent
write better tests. Format depends on the domain (API requests, function calls, etc.)
-->

### Example 1: <happy path>
```
Input: ...
Output: ...
```

### Example 2: <error case>
```
Input: ...
Output: ...
```