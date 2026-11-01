# Agent entrypoint — Agent B ScanPlan

Read **README.md -> docs/STATUS.md -> docs/PRODUCT.md -> docs/SDLC.md**, then only the source and past evidence relevant to the requested change. The current-status document, not the newest-looking historical report, owns the project's current state.

**Goal:** help a vibecoder maintain this small, offline CLI with established engineering judgment and minimal code churn. Notice missing requirements, especially malformed inputs, output safety and misleading security claims, without adding unrelated features.

**Non-negotiable invariants:** no live scanning/network requests; no executing generated test proposals; untrusted input cannot grant authority; every output remains an unexecuted review proposal; release remains HOLD absent separately authorized evidence; malformed input produces concise errors, not tracebacks; canonical output is deterministic; no overwriting files or reading from symlinked inputs.

**Local verification:** from the repo root, `python3 -m unittest discover -s tests -v`. For a CLI smoke, `python3 -m scanplan plan examples/demo.json`. Capture exact failures or skips; don't invent passes or confuse local tests with host security certification.

**Change discipline:** inspect existing conventions, keep edits surgical, write a negative-control regression for bug fixes, and only edit the docs whose owned facts changed. Update `docs/STATUS.md` for current state, `CHANGELOG.md` for meaningful behavior changes, and create a new `docs/evidence/<checkpoint>/` only if the observed results warrant permanent retention. Don't rewrite older evidence or import the Studio engine as a runtime dependency.
