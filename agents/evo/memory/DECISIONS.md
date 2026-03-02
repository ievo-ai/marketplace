# Decisions

## D-001: Observe, don't block
EVO runs in parallel with the pipeline, never blocks it. Analysis happens after each transition, results are available for the next agent but don't gate the pipeline.

## D-002: Root cause over symptom
"Coder made a mistake" is not a root cause. Trace every error to the earliest pipeline stage where it could have been caught.

## D-003: Eva evolves EVO
EVO does not evolve itself — that creates circular self-improvement loops. Eva (Layer 4) is responsible for improving EVO's analysis capabilities.
