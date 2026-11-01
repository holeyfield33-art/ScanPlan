# Immutable origin record: Studio greenfield experiment

This standalone project was **conceived from a broad idea, not a detailed implementation prompt**. The developer used Software Research Studio's accumulated engineering knowledge/SDLC guidance as context to select an appropriately narrow offline CLI and good engineering practices. This was a documented Studio-assisted model build, **not** proof that Studio's experimental canonical planner/selector/host executor generated the code.

## Provenance

- Source repository: `holeyfield33-art/software-research-studio`.
- Initial greenfield build in Studio PR #7, merged main `3795c1736b20ac3d6955e1587f4c7f7a8c778ec3`.
- Bounded Unicode fix and trials in Studio PR #8, merged main `d2c378c82a3afcd1b5723be85cd989b3394b10b3`.
- Studio documentation/knowledge layout PR #9, merged main `77eb08ca35a06f74152b698188e6ac28a9fd6960`.
- The initial generator core Git blob was `6b6851fd1d294fe7113bddfcd5e2ab2937704545`; corrected core blob `b4392ca21bed68de95ce83520729fe9232e57a91`.
- The original base tests blob was `629e04e9a4fb88c13622308bced434af2d84410b`, and additional Unicode tests blob `72ee69bf180f2a52b20382d5ab0b5dab333dcd37`.
- The local source files in this independent seed were compared against those blob hashes, then tested. This repo starts with a fresh independent Git history; it does **not** purport to import all Studio commit ancestry.

## Evidence and limitations

`records/` preserves original spec/decisions/evidence; `tests/` preserves red-phase and green-phase logs and generated demo output. Raw original archive files remain in Studio history. The red-phase tests are a *deliberate failing control*, not a current defect. Green phase: 23 tests pass, demo output SHA-256 `e46237e1e3573ca04f260d1fb0d4b6cbe84ce8564a62561d2cba56c52d0ac373`.

No independent signing host, authenticated execution grant, or CI for this new repo has been run. No licensing terms are inferred from the Studio repository; select a license before public distribution.
