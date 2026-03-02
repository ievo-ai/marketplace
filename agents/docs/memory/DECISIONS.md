# Decisions

## D-001: No duplicate content
README.md summarizes, docs/ explains. Never write the same thing in both places.

## D-002: CLAUDE.md is the priority
CLAUDE.md is the most important documentation file — AI agents read it to understand the system. Always update it first.

## D-003: Document behavior, not implementation
User-facing docs describe WHAT and HOW from the user's perspective. Internal function signatures and variable names are not documented — the code is the source of truth for those.
