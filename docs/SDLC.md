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


## Repository maintenance and security-testing coverage

This is ScanPlan's **risk-adjusted maintenance procedure** derived from the five-phase OWASP Web Security Testing Framework (requirements and design through maintenance). OWASP's approach is flexible; an offline CLI is not a deployed web app. Do not add HTTP scanning, web authentication, deployment monitoring, a background agent or a new status file to satisfy a generic checklist. See [Studio's reusable maintenance guidance](https://github.com/holeyfield33-art/software-research-studio/blob/main/docs/REPOSITORY_KNOWLEDGE_LAYOUT.md) as advisory engineering knowledge, not a runtime dependency.

### Phase-appropriate controls

| Concern | ScanPlan's selected check | Not applicable unless scope changes |
| --- | --- | --- |
| Before building | Pin Python support range, standard-library-only decision, allowed fixture-only inputs, expected behaviors and measurable checks (unit results, stable canonical output) | Organization-wide web security policy |
| Requirements/design | Review ambiguous threat claims, authorization language, user-facing CLI error contract and input/output boundaries; recheck that proposed tests are **not executed** | Account/session management, web UML diagrams |
| During development | Read `scanplan/core.py` and `scanplan/__main__.py` flow before reviewing a diff; add negative control for each new failure mode; preserve the four threat-kind behaviors and deterministic output | Unrelated application frameworks |
| Distribution/release | Test clean Python install/import and CLI on supported operating systems; verify exit codes, existing-output refusal, fixture output, packaging/license and GitHub CI on exact candidate | Live penetration testing and deployed infrastructure checks |
| Maintenance | Review Python version compatibility, GitHub workflow outcomes, repository access/branches, issue reports, documentation drift and any new software supply-chain advisories; verify relevant controls again after every change | Continuous uptime dashboards for an offline program |

### Triggers, cadence and evidence

- **Each PR:** verify `git status`, HEAD and scope; inspect diff; run `python -m unittest discover -s tests -v` and `python -m scanplan plan examples/demo.json`; check controlled malformed input, negative controls and output invariants when relevant. Preserve demo hash only when comparing exact canonical example bytes. A skipped symlink test is **SKIP**, not PASS.
- **Cross-platform or release candidate:** independently run the same suite and CLI fixture on Windows and Linux supported Python versions. Confirm the workflow jobs **executed test steps**; a zero-step GitHub Actions failure remains **NOT_RUN**. Check package/license/README commands and any platform-specific file behavior. No release/security-certification claim from local tests alone.
- **New security report, Python compatibility change or dependency addition:** evaluate impact, provenance, failure path, and compatibility. Standard-library-only is a deliberate constraint: external dependencies require explicit scope and justification.
- **Periodic health review:** suggest **quarterly** for this stable offline experiment, or sooner on a Python support change, vulnerability report, or user-visible failure. The operator must approve a cadence; no recurring review is currently scheduled or claimed completed. Check stale issues/PRs, broken docs/links, tests and CI, Python version support, and the integrity of the origin evidence.
- **If the product ever adds live execution, file-system mutations beyond new output files, sensitive data, network tools or hosted service functionality:** **STOP** and re-evaluate design, threat boundaries, user authorization, operations and testing before implementation. Existing offline claims do not apply to that expanded product.

### Reporting and ownership

This repository's [single living STATUS](STATUS.md) owns the latest verified environment, commit, pass/fail/skip/NOT_RUN results, unknowns, operator/reviewer ownership and next 1–3 actions. Update [CHANGELOG](../CHANGELOG.md) only for meaningful behavior or published maintenance-contract changes. Keep the original Studio seed and test evidence immutable; do not invent a new report on every ordinary edit. If a review only inspects source and docs, label test execution **NOT_RUN**.

**Current application:** policy guidance added; **no new post-change Windows run, hosted CI execution, production authorization or periodic health review has been performed by this documentation edit**. The existing 24-test local Linux evidence remains historical and the project's experimental/HOLD boundary is unchanged.
