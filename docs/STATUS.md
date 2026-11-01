# Current project status

**Baseline:** Agent B ScanPlan v0.1.1 — independent standalone seed, November 1, 2026.
**State:** Experimental, offline planning utility. **Production/security qualification: HOLD**.

## Working, locally reproduced

- The packaged seed reports **23/23 passed** in its original isolated workspace (Python 3.11+; historical result, not reproduced in this Windows environment).
- Current Windows verification with Python 3.14.6: **22 passed, 1 errored** because the symlink-input test cannot create a symlink without the required Windows privilege (`WinError 1314`). The symlink rejection check remains unverified here.
- `python3 -m scanplan plan examples/demo.json`: deterministic output with four unexecuted proposals. Original demo output SHA-256 `e46237e1e3573ca04f260d1fb0d4b6cbe84ce8564a62561d2cba56c52d0ac373`.
- Unpaired Unicode surrogate input rejected with controlled `IntakeError` and clean CLI exit rather than a traceback.
- Original Studio sources and test hashes are preserved in [origin evidence](evidence/STUDIO-ORIGIN-20261101/README.md).

## Not established

- Live scanning, real target authorization and exploit detection: **not implemented** (intentional).
- Hosted CI: **NOT_RUN** for this standalone repository.
- Studio canonical planner/independent host receipts for this seed: **NOT_RUN**; they are not required at runtime.
- Production readiness or independent external audit: **NOT_ESTABLISHED**.
- GitHub repository: `holeyfield33-art/ScanPlan`. Hosted CI is **NOT_RUN**.

## Next actions

1. Verify a clean checkout on an independent host, run `python3 -m unittest discover -s tests -v`, record environment and actual result.
2. Choose the next **small user-facing** improvement or maintenance fix only after confirming it is useful; avoid expanding to network scanning without a separate specification and authorization.
