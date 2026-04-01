---
name: protocol-schema-and-type-update
description: Workflow command scaffold for protocol-schema-and-type-update in codex.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /protocol-schema-and-type-update

Use this workflow when working on **protocol-schema-and-type-update** in `codex`.

## Goal

Updates JSON schemas and corresponding TypeScript/Rust protocol types for API endpoints, events, or config. Often includes updating tests and sometimes README/docs.

## Common Files

- `codex-rs/app-server-protocol/schema/json/*.json`
- `codex-rs/app-server-protocol/schema/typescript/**/*.ts`
- `codex-rs/app-server-protocol/src/protocol/**/*.rs`
- `codex-rs/app-server/tests/suite/**/*.rs`
- `codex-rs/app-server/README.md`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit JSON schema files in codex-rs/app-server-protocol/schema/json/
- Regenerate or update TypeScript types in codex-rs/app-server-protocol/schema/typescript/
- Update Rust protocol code in codex-rs/app-server-protocol/src/protocol/
- Update or add tests in codex-rs/app-server/tests/suite/
- Optionally update README.md or docs

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.