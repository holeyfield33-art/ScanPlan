# Product and user contract

## User and problem

For developers and reviewers who have tentative threat observations and want a rigorous **test plan** before touching a real system. A hypothesis is not a vulnerability. The user should be able to describe controlled fixture concerns without knowing every positive control, negative control or independent oracle needed to investigate them.

## Minimal CLI journey

Prepare JSON -> run `python -m scanplan plan <input.json> [--output <new.json>]` -> inspect deterministic plan -> human reviewer decides whether any test should ever be implemented and separately authorized. A screen-based UX is not relevant to this CLI.

## Input contract

The closed top-level object contains `version`, `project_id`, `subject`, `scope`, `threats`. The scope contains `review_owner`, `fixture_only: true`, `network_allowed: false`. Each threat has `id`, `kind`, `component`, `observation`. Exactly four threat kinds are currently supported. The identity of the reviewer is **declared text**, not verified authorization.

## Required outcomes

- Valid input produces deterministic UTF-8 JSON with one planned case per unique threat and a stable input hash.
- Each case specifies a hypothesis, positive control, negative control and independent oracle.
- Unsupported shape, duplicate keys/IDs, invalid text, malformed Unicode and unauthorized scope are rejected cleanly.
- Output files are created exclusively; existing content remains untouched.
- No plans claim that a test ran, a vulnerability exists, permission was obtained or a release was authorized.

## Non-goals

Live scanners, model orchestration, a web UI, source-code vulnerability finding, automatic exploit generation, network targeting, persistent account systems or a commercial multi-tenant service. Such additions require explicit new product scope, not opportunistic feature growth.
