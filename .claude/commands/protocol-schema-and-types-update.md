---
name: protocol-schema-and-types-update
description: Workflow command scaffold for protocol-schema-and-types-update in codex.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /protocol-schema-and-types-update

Use this workflow when working on **protocol-schema-and-types-update** in `codex`.

## Goal

Update or add new fields to the protocol schema and propagate changes through TypeScript types, Rust protocol code, and tests.

## Common Files

- `codex-rs/app-server-protocol/schema/json/*.json`
- `codex-rs/app-server-protocol/schema/typescript/**/*.ts`
- `codex-rs/app-server-protocol/src/protocol/**/*.rs`
- `codex-rs/app-server/tests/suite/v2/**/*.rs`
- `codex-rs/protocol/src/models.rs`
- `codex-rs/protocol/src/protocol.rs`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit or add JSON schema files in codex-rs/app-server-protocol/schema/json/
- Regenerate or update corresponding TypeScript types in codex-rs/app-server-protocol/schema/typescript/
- Update Rust protocol code in codex-rs/app-server-protocol/src/protocol/
- Update or add related tests in codex-rs/app-server/tests/suite/v2/
- Update core/protocol models if needed (codex-rs/protocol/src/models.rs, codex-rs/protocol/src/protocol.rs)

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.