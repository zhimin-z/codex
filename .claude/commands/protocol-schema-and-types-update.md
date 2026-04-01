---
name: protocol-schema-and-types-update
description: Workflow command scaffold for protocol-schema-and-types-update in codex.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /protocol-schema-and-types-update

Use this workflow when working on **protocol-schema-and-types-update** in `codex`.

## Goal

Update the protocol schema and regenerate associated TypeScript and Rust types, plus update protocol handlers and tests.

## Common Files

- `codex-rs/app-server-protocol/schema/json/*.json`
- `codex-rs/app-server-protocol/schema/typescript/**/*.ts`
- `codex-rs/app-server-protocol/src/protocol/**/*.rs`
- `codex-rs/app-server/src/**/*.rs`
- `codex-rs/app-server/tests/suite/**/*.rs`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit or add JSON schema files in codex-rs/app-server-protocol/schema/json/
- Regenerate TypeScript types in codex-rs/app-server-protocol/schema/typescript/ (matching the changed schema)
- Regenerate Rust protocol files in codex-rs/app-server-protocol/src/protocol/
- Update protocol consumers/handlers in codex-rs/app-server/src/ and/or codex-rs/core/src/
- Update or add tests in codex-rs/app-server/tests/suite/ or codex-rs/core/tests/suite/

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.