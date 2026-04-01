---
name: extract-shared-tool-specs-from-codex-core-to-codex-tools
description: Workflow command scaffold for extract-shared-tool-specs-from-codex-core-to-codex-tools in codex.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /extract-shared-tool-specs-from-codex-core-to-codex-tools

Use this workflow when working on **extract-shared-tool-specs-from-codex-core-to-codex-tools** in `codex`.

## Goal

Migrates passive tool specification logic, models, and builders from codex-core to codex-tools, splitting code along crate boundaries for improved modularity.

## Common Files

- `codex-rs/core/src/tools/spec.rs`
- `codex-rs/core/src/tools/spec_tests.rs`
- `codex-rs/core/src/tools/discoverable.rs`
- `codex-rs/core/src/tools/handlers/tool_suggest.rs`
- `codex-rs/core/src/tools/handlers/tool_suggest_tests.rs`
- `codex-rs/core/src/tools/code_mode_description.rs`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Identify passive tool spec/model code in codex-rs/core/src/tools (e.g., spec.rs, discoverable.rs, code_mode_description.rs).
- Move relevant structs, enums, and builder functions to new or existing modules in codex-rs/tools/src/ (e.g., tool_spec.rs, code_mode.rs, agent_tool.rs, local_tool.rs, etc.).
- Add or update unit tests in sibling *_tests.rs files in codex-rs/tools/src/.
- Update codex-rs/tools/README.md to document the expanded crate boundary.
- Update codex-rs/core/src/tools/*.rs and other call sites to import and use the extracted code from codex-tools.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.