---
name: add-or-update-tool-or-tool-feature
description: Workflow command scaffold for add-or-update-tool-or-tool-feature in codex.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /add-or-update-tool-or-tool-feature

Use this workflow when working on **add-or-update-tool-or-tool-feature** in `codex`.

## Goal

Adds a new tool, updates an existing tool, or extends tool features (such as code mode, exec, MCP tools). This includes implementation, updating tool specs, JS/runner/bridge files, and tests.

## Common Files

- `codex-rs/core/src/tools/*.rs`
- `codex-rs/core/src/tools/handlers/*.rs`
- `codex-rs/core/src/tools/spec.rs`
- `codex-rs/core/src/tools/code_mode_runner.cjs`
- `codex-rs/core/src/tools/code_mode_bridge.js`
- `codex-rs/core/tests/suite/code_mode.rs`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit or create files in codex-rs/core/src/tools/ (e.g., code_mode.rs, handlers/*.rs, spec.rs)
- Update or create runner/bridge files (e.g., code_mode_runner.cjs, code_mode_bridge.js)
- Update tool specs (spec.rs)
- Update or add tests in codex-rs/core/tests/suite/
- Optionally update protocol/models if tool output shape changes

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.