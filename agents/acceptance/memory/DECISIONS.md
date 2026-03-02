# Decisions

## D-001: Read-only agent
Acceptance never modifies code. It verifies and reports. Fixes go back to Coder.

## D-002: Mock-only = gap
Tests that only assert `.assert_called_once()` without verifying real outcomes count as gaps unless the mocked boundary is truly external (Docker, network, subprocess).

## D-003: Coverage is necessary but not sufficient
100% line coverage with bad tests is worse than 80% with good tests. Check WHAT tests verify, not just that they exist.
