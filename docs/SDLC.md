# Engineering guide — Agent B ScanPlan

This is the **project-specific engineering reference** for coding agents. Use established practices that help this offline CLI; it is **not** a mandatory lifecycle ritual. The coding model remains the engineer using normal tools.

## Architecture and decisions

`scanplan/core.py` owns JSON parsing, strict input validation, finite threat-kind patterns and canonical output. `scanplan/__main__.py` owns CLI flags, file handling and exit statuses. `tests/` owns unit, negative and subprocess-facing acceptance tests. `examples/` contains safe local fixtures. Avoid mixing CLI/IO concerns into the deterministic core.

Design choices carried from the Studio seed: stdlib-only, schema-like closed keys, bounded input sizes, no execution or network, independent oracle language and explicit unknown/held authority. Original ADR notes remain archived in `docs/evidence/STUDIO-ORIGIN-20261101/records/` for historical reference.

## Product invariants

1. **Untrusted JSON remains data.** Strings such as `review_owner` or an agent's purpose do not grant authority.
2. **No active execution.** Generated cases are proposals, not tests or vulnerability findings.
3. **Deterministic encoding.** Given the same canonical intake, output bytes remain stable. Invalid Unicode is rejected before UTF-8 encoding.
4. **Controlled failure.** No raw traceback to an ordinary CLI user on malformed inputs.
5. **Minimal side effects.** Read the explicitly supplied regular input file; write only an explicitly new output file or stdout. Do not overwrite existing files.
6. **Preserve behavior.** A bug fix must have a failing negative control and preserve the existing valid demo output unless intentionally changed.

## A proportionate change sequence

Inspect the actual requested behavior and project constraints. Identify the smallest necessary design decision, especially one the user did not know to ask about. Modify scoped code, add a regression when needed, run targeted and full local tests, then update `docs/STATUS.md` and `CHANGELOG.md` if facts changed. Record any security-related claim with exact observed evidence.

### Verification

```bash
python3 -m unittest discover -s tests -v
python3 -m scanplan plan examples/demo.json
```

A full test run is an assertion about the code in that environment, not host isolation, absence of network activity under adversarial conditions, or production qualification. Hosted CI is not PASS unless its jobs actually execute. Never silently upgrade `NOT_RUN`.

### Handoff

Provide the commit SHA, specific files changed, tests and exact results, remaining unknowns, one to three next actions, and how to undo the change. Keep historical evidence separate from this living engineering reference.
