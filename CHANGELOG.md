# Changelog

## Unreleased — Windows test portability (test/CI only)

- Preserve the symlink-input negative test; skip it only when Windows refuses to create a symlink with WinError 1314.
- Add an ordinary-directory input rejection test that runs without symlink privileges.
- Restore the standalone CI workflow (Ubuntu/Windows; Python 3.11/3.14) missing from the first remote push.
- Linux/Python 3.13.5 local verification: 24/24 PASS. Windows post-change and hosted CI remain NOT_RUN.
- No runtime scanning feature, input contract or release-status change.

## v0.1.1 — 2026-11-01 (standalone seed)

- Separated Agent B ScanPlan into an independent project repository seed from the Studio greenfield experiment.
- Preserved the original fixed source and tests without adding runtime dependencies on Studio.
- Adopted project-focused README, AGENTS, current STATUS, PRODUCT, SDLC and historical evidence structure.
- Retained the one-line malformed-Unicode/surrogate guard and four extra regression checks (23 local tests passing).

## v0.1.0 — 2026-11-01 (Studio experiment, historical)

- Built a deterministic offline threat-to-test planner covering four threat kinds.
- Added negative controls and independent-oracle requirements, honest NOT_RUN results and HOLD decisions.
- Initial 19-test local suite passed; subsequent pilot found a malformed-Unicode error and fixed it in v0.1.1.
