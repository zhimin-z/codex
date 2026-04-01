---
name: codex-conventions
description: Development conventions and patterns for codex. Rust project with mixed commits.
---

# Codex Conventions

> Generated from [zhimin-z/codex](https://github.com/zhimin-z/codex) on 2026-04-01

## Overview

This skill teaches Claude the development patterns and conventions used in codex.

## Tech Stack

- **Primary Language**: Rust
- **Architecture**: type-based module organization
- **Test Location**: mixed
- **Test Framework**: jest

## When to Use This Skill

Activate this skill when:
- Making changes to this repository
- Adding new features following established patterns
- Writing tests that match project conventions
- Creating commits with proper message format

## Commit Conventions

Follow these commit message conventions based on 200 analyzed commits.

### Commit Style: Mixed Style

### Prefixes Used

- `fix`
- `feat`
- `chore`
- `ci`
- `[plugins]`
- `[codex]`

### Message Guidelines

- Average message length: ~55 characters
- Keep first line concise and descriptive
- Use imperative mood ("Add feature" not "Added feature")


*Commit message example*

```text
auth: generalize external auth tokens for bearer-only sources (#16286)
```

*Commit message example*

```text
ci: run Windows argument-comment-lint via native Bazel (#16120)
```

*Commit message example*

```text
fix: close Bazel argument-comment-lint CI gaps (#16253)
```

*Commit message example*

```text
feat: add mailbox concept for wait (#16010)
```

*Commit message example*

```text
exec: make review-policy tests hermetic (#16137)
```

*Commit message example*

```text
Update code mode exec() instructions (#16279)
```

*Commit message example*

```text
[codex-analytics] refactor analytics to use reducer architecture (#16225)
```

*Commit message example*

```text
codex-tools: extract discoverable tool models (#16254)
```

## Architecture

### Project Structure: Monorepo

This project uses **type-based** module organization.

### Configuration Files

- `.devcontainer/Dockerfile`
- `.github/workflows/bazel.yml`
- `.github/workflows/blob-size-policy.yml`
- `.github/workflows/cargo-deny.yml`
- `.github/workflows/ci.yml`
- `.github/workflows/cla.yml`
- `.github/workflows/close-stale-contributor-prs.yml`
- `.github/workflows/codespell.yml`
- `.github/workflows/issue-deduplicator.yml`
- `.github/workflows/issue-labeler.yml`
- `.github/workflows/rust-ci-full.yml`
- `.github/workflows/rust-ci.yml`
- `.github/workflows/rust-release-argument-comment-lint.yml`
- `.github/workflows/rust-release-prepare.yml`
- `.github/workflows/rust-release-windows.yml`
- `.github/workflows/rust-release-zsh.yml`
- `.github/workflows/rust-release.yml`
- `.github/workflows/rusty-v8-release.yml`
- `.github/workflows/sdk.yml`
- `.github/workflows/v8-canary.yml`
- `codex-cli/Dockerfile`
- `codex-cli/package.json`
- `codex-rs/.github/workflows/cargo-audit.yml`
- `codex-rs/responses-api-proxy/npm/package.json`
- `codex-rs/vendor/bubblewrap/.github/workflows/check.yml`
- `package.json`
- `sdk/typescript/.prettierrc`
- `sdk/typescript/eslint.config.js`
- `sdk/typescript/package.json`
- `sdk/typescript/tsconfig.json`

### Guidelines

- Group code by type (components, services, utils)
- Keep related functionality in the same type folder
- Avoid circular dependencies between type folders

## Code Style

### Language: Rust

### Naming Conventions

| Element | Convention |
|---------|------------|
| Files | snake_case |
| Functions | camelCase |
| Classes | PascalCase |
| Constants | SCREAMING_SNAKE_CASE |

### Import Style: Relative Imports

### Export Style: Named Exports


*Preferred import style*

```typescript
// Use relative imports
import { Button } from '../components/Button'
import { useAuth } from './hooks/useAuth'
```

*Preferred export style*

```typescript
// Use named exports
export function calculateTotal() { ... }
export const TAX_RATE = 0.1
export interface Order { ... }
```

## Testing

### Test Framework: jest

### File Pattern: `*.test.ts`

### Test Types

- **Unit tests**: Test individual functions and components in isolation
- **Integration tests**: Test interactions between multiple components/services
- **E2e tests**: Test complete user flows through the application

### Mocking: jest.mock


*Test file structure*

```typescript
import { describe, it, expect } from 'jest'

describe('MyFunction', () => {
  it('should return expected result', () => {
    const result = myFunction(input)
    expect(result).toBe(expected)
  })
})
```

## Error Handling

### Error Handling Style: Try-Catch Blocks


*Standard error handling pattern*

```typescript
try {
  const result = await riskyOperation()
  return result
} catch (error) {
  console.error('Operation failed:', error)
  throw new Error('User-friendly message')
}
```

## Common Workflows

These workflows were detected from analyzing commit patterns.

### Feature Development

Standard feature implementation workflow

**Frequency**: ~5 times per month

**Steps**:
1. Add feature implementation
2. Add tests for feature
3. Update documentation

**Files typically involved**:
- `**/*.test.*`

**Example commit sequence**:
```
Fix tui_app_server resume-by-name lookup regression (#16050)
Fix tui_app_server agent picker closed-state regression (#16014)
chore: clean up argument-comment lint and roll out all-target CI on macOS (#16054)
```

### Refactoring

Code refactoring and cleanup workflow

**Frequency**: ~2 times per month

**Steps**:
1. Ensure tests pass before refactor
2. Refactor code structure
3. Verify tests still pass

**Files typically involved**:
- `src/**/*`

**Example commit sequence**:
```
chore: clean up argument-comment lint and roll out all-target CI on macOS (#16054)
Support Codex CLI stdin piping for `codex exec` (#15917)
shell-command: reuse a PowerShell parser process on Windows (#16057)
```

### Extract Shared Tool Specs From Codex Core To Codex Tools

Migrates passive tool specification logic, models, and builders from codex-core to codex-tools, splitting code along crate boundaries for improved modularity.

**Frequency**: ~6 times per month

**Steps**:
1. Identify passive tool spec/model code in codex-rs/core/src/tools (e.g., spec.rs, discoverable.rs, code_mode_description.rs).
2. Move relevant structs, enums, and builder functions to new or existing modules in codex-rs/tools/src/ (e.g., tool_spec.rs, code_mode.rs, agent_tool.rs, local_tool.rs, etc.).
3. Add or update unit tests in sibling *_tests.rs files in codex-rs/tools/src/.
4. Update codex-rs/tools/README.md to document the expanded crate boundary.
5. Update codex-rs/core/src/tools/*.rs and other call sites to import and use the extracted code from codex-tools.
6. Remove or simplify compatibility shims in codex-core.
7. Update Cargo.toml dependencies and Cargo.lock as needed.
8. Run and update tests to validate the migration.

**Files typically involved**:
- `codex-rs/core/src/tools/spec.rs`
- `codex-rs/core/src/tools/spec_tests.rs`
- `codex-rs/core/src/tools/discoverable.rs`
- `codex-rs/core/src/tools/handlers/tool_suggest.rs`
- `codex-rs/core/src/tools/handlers/tool_suggest_tests.rs`
- `codex-rs/core/src/tools/code_mode_description.rs`
- `codex-rs/core/src/tools/code_mode/mod.rs`
- `codex-rs/core/src/tools/registry.rs`
- `codex-rs/core/src/client_common.rs`
- `codex-rs/core/src/client.rs`
- `codex-rs/tools/src/tool_spec.rs`
- `codex-rs/tools/src/tool_spec_tests.rs`
- `codex-rs/tools/src/code_mode.rs`
- `codex-rs/tools/src/code_mode_tests.rs`
- `codex-rs/tools/src/agent_tool.rs`
- `codex-rs/tools/src/agent_tool_tests.rs`
- `codex-rs/tools/src/local_tool.rs`
- `codex-rs/tools/src/local_tool_tests.rs`
- `codex-rs/tools/src/view_image.rs`
- `codex-rs/tools/src/view_image_tests.rs`
- `codex-rs/tools/src/utility_tool.rs`
- `codex-rs/tools/src/utility_tool_tests.rs`
- `codex-rs/tools/src/mcp_resource_tool.rs`
- `codex-rs/tools/src/mcp_resource_tool_tests.rs`
- `codex-rs/tools/src/request_user_input_tool.rs`
- `codex-rs/tools/src/request_user_input_tool_tests.rs`
- `codex-rs/tools/src/agent_job_tool.rs`
- `codex-rs/tools/src/agent_job_tool_tests.rs`
- `codex-rs/tools/src/tool_discovery.rs`
- `codex-rs/tools/src/tool_discovery_tests.rs`
- `codex-rs/tools/README.md`

**Example commit sequence**:
```
Identify passive tool spec/model code in codex-rs/core/src/tools (e.g., spec.rs, discoverable.rs, code_mode_description.rs).
Move relevant structs, enums, and builder functions to new or existing modules in codex-rs/tools/src/ (e.g., tool_spec.rs, code_mode.rs, agent_tool.rs, local_tool.rs, etc.).
Add or update unit tests in sibling *_tests.rs files in codex-rs/tools/src/.
Update codex-rs/tools/README.md to document the expanded crate boundary.
Update codex-rs/core/src/tools/*.rs and other call sites to import and use the extracted code from codex-tools.
Remove or simplify compatibility shims in codex-core.
Update Cargo.toml dependencies and Cargo.lock as needed.
Run and update tests to validate the migration.
```

### Argument Comment Lint Ci Integration And Enforcement

Rolls out, migrates, or tightens enforcement of the argument-comment-lint tool in CI, including Bazel/Cargo integration, wrapper refactors, and cross-platform coverage.

**Frequency**: ~5 times per month

**Steps**:
1. Update or migrate argument-comment-lint wrappers (e.g., from shell to Python).
2. Modify CI workflows (.github/workflows/rust-ci.yml, rust-ci-full.yml, bazel.yml) to change how/where the lint runs (e.g., Bazel aspect, Cargo wrapper, platform-specific logic).
3. Patch or update scripts (e.g., run-bazel-ci.sh, run-prebuilt-linter.py, run.py) to support new invocation patterns.
4. Fix or update codebase to resolve new lint violations surfaced by stricter enforcement.
5. Add or update documentation in tools/argument-comment-lint/README.md.
6. Add or update tests for the linter and its wrappers.
7. Validate in CI across Linux, macOS, and Windows runners.

**Files typically involved**:
- `.github/workflows/rust-ci.yml`
- `.github/workflows/rust-ci-full.yml`
- `.github/workflows/bazel.yml`
- `tools/argument-comment-lint/run-prebuilt-linter.py`
- `tools/argument-comment-lint/run-prebuilt-linter.sh`
- `tools/argument-comment-lint/run.py`
- `tools/argument-comment-lint/run.sh`
- `tools/argument-comment-lint/wrapper_common.py`
- `tools/argument-comment-lint/README.md`
- `tools/argument-comment-lint/lint_aspect.bzl`
- `tools/argument-comment-lint/test_wrapper_common.py`
- `justfile`

**Example commit sequence**:
```
Update or migrate argument-comment-lint wrappers (e.g., from shell to Python).
Modify CI workflows (.github/workflows/rust-ci.yml, rust-ci-full.yml, bazel.yml) to change how/where the lint runs (e.g., Bazel aspect, Cargo wrapper, platform-specific logic).
Patch or update scripts (e.g., run-bazel-ci.sh, run-prebuilt-linter.py, run.py) to support new invocation patterns.
Fix or update codebase to resolve new lint violations surfaced by stricter enforcement.
Add or update documentation in tools/argument-comment-lint/README.md.
Add or update tests for the linter and its wrappers.
Validate in CI across Linux, macOS, and Windows runners.
```

### Bazel Windows Gnullvm Support And Cross Platform Ci

Expands and maintains Bazel CI/test/build support for Windows (gnullvm), including toolchain patches, workflow matrix updates, and platform-specific fixes.

**Frequency**: ~3 times per month

**Steps**:
1. Patch Bazel toolchain, rules_rust, rules_rs, LLVM, or V8 modules as needed for Windows gnullvm compatibility.
2. Update .github/workflows/bazel.yml to add or adjust Windows matrix entries for build/test/clippy.
3. Update .github/actions/setup-bazel-ci/action.yml and related scripts to support Windows-specific setup (output root, longpaths, env vars).
4. Adjust defs.bzl and related Bazel macros to ensure correct flags and stack sizes for Windows unit test binaries.
5. Update MODULE.bazel and MODULE.bazel.lock for new pins, patches, or SDKs.
6. Validate by running Bazel build/test/clippy on Windows runners in CI.

**Files typically involved**:
- `.github/workflows/bazel.yml`
- `.github/actions/setup-bazel-ci/action.yml`
- `MODULE.bazel`
- `MODULE.bazel.lock`
- `defs.bzl`
- `patches/BUILD.bazel`
- `patches/abseil_windows_gnullvm_thread_identity.patch`
- `patches/llvm_windows_symlink_extract.patch`
- `patches/rules_rs_windows_gnullvm_exec.patch`
- `patches/rules_rust_windows_gnullvm_build_script.patch`
- `patches/rusty_v8_prebuilt_out_dir.patch`
- `patches/v8_bazel_rules.patch`
- `patches/v8_module_deps.patch`
- `patches/v8_source_portability.patch`
- `third_party/v8/BUILD.bazel`
- `workspace_root_test_launcher.bat.tpl`

**Example commit sequence**:
```
Patch Bazel toolchain, rules_rust, rules_rs, LLVM, or V8 modules as needed for Windows gnullvm compatibility.
Update .github/workflows/bazel.yml to add or adjust Windows matrix entries for build/test/clippy.
Update .github/actions/setup-bazel-ci/action.yml and related scripts to support Windows-specific setup (output root, longpaths, env vars).
Adjust defs.bzl and related Bazel macros to ensure correct flags and stack sizes for Windows unit test binaries.
Update MODULE.bazel and MODULE.bazel.lock for new pins, patches, or SDKs.
Validate by running Bazel build/test/clippy on Windows runners in CI.
```

### Remove Legacy Or Obsolete Features

Deletes legacy code, features, or split implementations (e.g., legacy TUI, custom prompts, voice transcription), including code, tests, docs, and feature flags.

**Frequency**: ~2 times per month

**Steps**:
1. Identify all code, tests, and documentation related to the obsolete feature.
2. Delete feature-specific modules, files, and references from the codebase.
3. Remove feature flags and related config/schema entries.
4. Update documentation to remove references to the deleted feature.
5. Update or clean up downstream event handling and UI logic.
6. Validate that the codebase builds and tests pass without the feature.

**Files typically involved**:
- `codex-rs/features/src/lib.rs`
- `codex-rs/tui/Cargo.toml`
- `codex-rs/tui/src/app.rs`
- `codex-rs/tui/src/app_event.rs`
- `codex-rs/tui/src/bottom_pane/chat_composer.rs`
- `codex-rs/tui/src/bottom_pane/mod.rs`
- `codex-rs/tui/src/bottom_pane/textarea.rs`
- `codex-rs/tui/src/chatwidget.rs`
- `codex-rs/tui/src/chatwidget/realtime.rs`
- `codex-rs/tui/src/chatwidget/tests.rs`
- `codex-rs/tui/src/lib.rs`
- `codex-rs/tui/src/voice.rs`
- `codex-rs/core/src/custom_prompts.rs`
- `codex-rs/core/src/custom_prompts_tests.rs`
- `codex-rs/protocol/src/custom_prompts.rs`
- `codex-rs/protocol/src/lib.rs`
- `codex-rs/protocol/src/protocol.rs`
- `codex-rs/rollout/src/policy.rs`
- `codex-rs/tui/src/bottom_pane/command_popup.rs`
- `codex-rs/tui/src/bottom_pane/prompt_args.rs`
- `docs/prompts.md`
- `docs/tui-chat-composer.md`

**Example commit sequence**:
```
Identify all code, tests, and documentation related to the obsolete feature.
Delete feature-specific modules, files, and references from the codebase.
Remove feature flags and related config/schema entries.
Update documentation to remove references to the deleted feature.
Update or clean up downstream event handling and UI logic.
Validate that the codebase builds and tests pass without the feature.
```


## Best Practices

Based on analysis of the codebase, follow these practices:

### Do

- Write tests using jest
- Follow *.test.ts naming pattern
- Use snake_case for file names
- Prefer named exports

### Don't

- Don't skip tests for new features
- Don't deviate from established patterns without discussion

---

*This skill was auto-generated by [ECC Tools](https://ecc.tools). Review and customize as needed for your team.*
