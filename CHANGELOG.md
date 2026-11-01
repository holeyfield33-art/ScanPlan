# Changelog

## v0.1.1 — 2026-11-01 (standalone seed)

- Separated Agent B ScanPlan into an independent project repository seed from the Studio greenfield experiment.
- Preserved the original fixed source and tests without adding runtime dependencies on Studio.
- Adopted project-focused README, AGENTS, current STATUS, PRODUCT, SDLC and historical evidence structure.
- Retained the one-line malformed-Unicode/surrogate guard and four extra regression checks (23 local tests passing).

## v0.1.0 — 2026-11-01 (Studio experiment, historical)

- Built a deterministic offline threat-to-test planner covering four threat kinds.
- Added negative controls and independent-oracle requirements, honest NOT_RUN results and HOLD decisions.
- Initial 19-test local suite passed; subsequent pilot found a malformed-Unicode error and fixed it in v0.1.1.
