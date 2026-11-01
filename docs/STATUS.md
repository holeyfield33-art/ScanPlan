# Current project status

**Baseline:** Agent B ScanPlan v0.1.1 — independent standalone seed, November 1, 2026.
**State:** Experimental, offline planning utility. **Production/security qualification: HOLD**.

## Working, locally reproduced

- The packaged seed reports **23/23 passed** in its original isolated workspace (Python 3.11+; historical result, not reproduced in this Windows environment).
- Historical Windows verification with Python 3.14.6: **22 passed, 1 errored** because creation of the test symlink raised `WinError 1314`. This was a test-setup failure, not observed acceptance of a symlink by ScanPlan.
- Follow-up branch `fix/windows-symlink-test-portability`: local Linux/Python 3.13.5 regression run **24/24 PASS**, including a new directory-input negative control. The symlink test now skips **only** on Windows error 1314; all other errors still fail. **Updated Windows results are NOT_RUN** until tested on Windows.
- `python3 -m scanplan plan examples/demo.json`: deterministic output with four unexecuted proposals. Original demo output SHA-256 `e46237e1e3573ca04f260d1fb0d4b6cbe84ce8564a62561d2cba56c52d0ac373`.
- Unpaired Unicode surrogate input rejected with controlled `IntakeError` and clean CLI exit rather than a traceback.
- Original Studio sources and test hashes are preserved in [origin evidence](evidence/STUDIO-ORIGIN-20261101/README.md).

## Not established

- Live scanning, real target authorization and exploit detection: **not implemented** (intentional).
- Standalone GitHub Actions workflow restored on a follow-up branch (Windows/Linux, Python 3.11/3.14); **hosted results remain NOT_RUN/unverified** until runner steps actually execute.
- Studio canonical planner/independent host receipts for this seed: **NOT_RUN**; they are not required at runtime.
- Production readiness or independent external audit: **NOT_ESTABLISHED**.
- GitHub repository: `holeyfield33-art/ScanPlan` at baseline `a974ea0`; follow-up portability PR is not a production release.

## Next actions

1. On Windows, check out the follow-up branch and run `py -m unittest discover -s tests -v`. Expected without symlink creation privileges: **23 passed, 1 skipped** (24 tests total). With symlink privilege available: 24 passed. Record observed numbers rather than assuming them.
2. Verify hosted CI runner steps actually ran, then review and merge the small portability PR. A failing workflow with zero executed steps is NOT_RUN.
3. Preserve this repository as a standalone **Studio-born greenfield baseline**: use README, AGENTS, this living STATUS, SDLC and immutable origin evidence. Pause additional scanner features until a real user need is identified.
