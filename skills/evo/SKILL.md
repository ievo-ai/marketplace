---
name: evo
description: >-
  Trigger the Evolution agent to analyze a mistake and log a lesson.
  Use when you or another agent made an error worth learning from.
---

# /evo — Trigger Evolution

When `/evo` is invoked, immediately delegate to the `evolution` agent:

```
Use the evolution agent to analyze this error and create a curator issue.
```

Pass along any context about what went wrong. Do not analyze or log anything yourself — the evolution agent handles everything.
