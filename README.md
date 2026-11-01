# Agent B ScanPlan

**Experimental offline threat-to-test planner. Not a vulnerability scanner.**

ScanPlan turns a small, structured list of security hypotheses into deterministic, reviewable proposed fixture tests. Each case includes a positive control, negative control, independent-oracle requirement, and explicit **NOT_RUN** result. It performs **no network calls, code execution, target inspection, or vulnerability detection**.

The app is an independent greenfield project originally developed as an experiment using the Software Research Studio engineering-knowledge baseline. Studio is **not** a runtime dependency or controlling lifecycle service. Read [the origin record](docs/evidence/STUDIO-ORIGIN-20261101/README.md) for exact provenance.

## What it supports

- Four hypothesis types: `path_traversal`, `prompt_injection`, `tool_authority`, `secret_exposure`.
- Validated JSON input with a closed schema, a maximum of 40 threats and 1 MiB input size.
- UTF-8-safe free-text fields, duplicate-key/ID rejection, deterministic JSON output.
- CLI stdout or exclusive creation of a new output file; refuses overwriting an existing file.
- All plans retain `execution_authority: UNVERIFIED`, `release_disposition: HOLD` and `execution: NOT_RUN`.

## Run

Python 3.11+; standard library only for the application and tests.

```bash
python3 -m scanplan plan examples/demo.json
python3 -m scanplan plan examples/demo.json --output /tmp/scanplan-test-plan.json
python3 -m unittest discover -s tests -v  # Windows: py -m unittest discover -s tests -v
```

`--output` must name a new file in an existing directory. **Exit 0 means the plan was written, not that any security tests ran.** Input/output errors return 1; CLI syntax errors return 2.

## How to maintain it

Read [AGENTS.md](AGENTS.md) for agent entry, [docs/STATUS.md](docs/STATUS.md) for current truth, [docs/PRODUCT.md](docs/PRODUCT.md) for use cases and acceptance, and [docs/SDLC.md](docs/SDLC.md) for project-specific engineering practices. [CHANGELOG.md](CHANGELOG.md) records changes, while `docs/evidence/` preserves past observations separately from current status.

## Current boundary

Experimental local utility; **no production security certification** or permission to probe systems. The original Studio pilot reported 19 passing tests, followed by 23 passing after fixing malformed Unicode handling. Tests were independently rerun in the extracted standalone workspace before this seed was created. The standalone Windows/Linux CI workflow is included in the follow-up portability branch; **hosted execution is not yet verified**. The latest Linux run of the updated tests passed 24/24. Windows rerun is pending.
