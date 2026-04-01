```markdown
# codex Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you how to contribute effectively to the `codex` Rust codebase. You'll learn the project's coding conventions, how to update protocol schemas, tool specs, and config schemas, as well as how to develop features with proper tests and documentation. The guide covers common workflows, step-by-step instructions, and recommended commands to streamline your development process.

## Coding Conventions

- **File Naming:**  
  Use `snake_case` for all file and module names.
  ```
  // Good
  mod my_feature;
  pub mod protocol_handler;
  // Bad
  mod MyFeature;
  pub mod ProtocolHandler;
  ```

- **Import Style:**  
  Use relative imports within modules.
  ```rust
  // In codex-rs/core/src/tools/processor.rs
  use super::helper;
  use crate::config::Config;
  ```

- **Export Style:**  
  Use named exports for modules and functions.
  ```rust
  pub mod tools;
  pub fn process_data() { ... }
  ```

- **Commit Messages:**  
  - Use prefixes: `feat`, `fix`, `chore`
  - Keep commit messages concise (~56 characters on average)
  ```
  feat: add new protocol message for user sync
  fix: correct tool runner error handling
  chore: update dependencies
  ```

## Workflows

### Protocol Schema and Types Update
**Trigger:** When you need to add or change an API contract, protocol message, or endpoint.  
**Command:** `/update-protocol-schema`

1. Edit or add JSON schema files in `codex-rs/app-server-protocol/schema/json/`.
2. Regenerate TypeScript types in `codex-rs/app-server-protocol/schema/typescript/` to match the updated schema.
3. Regenerate Rust protocol files in `codex-rs/app-server-protocol/src/protocol/`.
4. Update protocol consumers/handlers in `codex-rs/app-server/src/` and/or `codex-rs/core/src/`.
5. Update or add tests in `codex-rs/app-server/tests/suite/` or `codex-rs/core/tests/suite/`.

**Example:**
```sh
# After editing schema
/update-protocol-schema
```

---

### Tool Spec and Implementation Update
**Trigger:** When adding a new tool, updating an existing tool's logic, or changing its interface.  
**Command:** `/update-tool`

1. Edit or add tool implementation in `codex-rs/core/src/tools/` (Rust and/or JS/CJS/Bridge files).
2. Update the tool spec in `codex-rs/core/src/tools/spec.rs`.
3. Update or add tests in `codex-rs/core/tests/suite/`.
4. Update documentation or helper files if needed.

**Example:**
```rust
// codex-rs/core/src/tools/my_tool.rs
pub fn run_my_tool() { ... }
```
```sh
/update-tool
```

---

### Config Schema and Behavior Update
**Trigger:** When adding or changing a config option, or altering config validation/behavior.  
**Command:** `/update-config-schema`

1. Edit `codex-rs/core/config.schema.json`.
2. Update Rust config handling in `codex-rs/core/src/config/`.
3. Update or add config-related tests in `codex-rs/core/src/config/config_tests.rs` or `codex-rs/core/tests/suite/`.
4. Update documentation in `docs/config.md` if needed.

**Example:**
```json
// codex-rs/core/config.schema.json
{
  "new_option": {
    "type": "boolean",
    "default": false
  }
}
```
```sh
/update-config-schema
```

---

### Feature Development with Tests and Docs
**Trigger:** When adding a new capability, improving an existing feature, or fixing a bug with tests.  
**Command:** `/feature`

1. Edit or add implementation files (Rust, JS, etc.).
2. Update or add tests in `codex-rs/core/tests/suite/` or other relevant test directories.
3. Update documentation or spec files if needed.

**Example:**
```rust
// codex-rs/core/src/new_feature.rs
pub fn new_feature() { ... }
```
```sh
/feature
```

## Testing Patterns

- **Framework:** Jest (for TypeScript/JS), Rust built-in test framework for Rust code.
- **Test File Pattern:**  
  - TypeScript/JS: `*.test.ts`
  - Rust: Place tests in `tests/suite/` or alongside modules in `mod tests { ... }`
- **Example (Rust):**
  ```rust
  #[cfg(test)]
  mod tests {
      use super::*;
      #[test]
      fn test_my_feature() {
          assert_eq!(my_feature(), expected_value);
      }
  }
  ```

## Commands

| Command                  | Purpose                                                         |
|--------------------------|-----------------------------------------------------------------|
| /update-protocol-schema  | Regenerate protocol types and update handlers/tests             |
| /update-tool             | Add or update a tool's implementation, spec, and tests         |
| /update-config-schema    | Update config schema, Rust config logic, and related docs/tests |
| /feature                 | Implement a new feature or enhancement with tests and docs      |
```
