```markdown
# codex Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you how to contribute effectively to the `codex` Rust codebase. It covers the project's coding conventions, file organization, and the main development workflows for adding tools, updating schemas, changing configuration, implementing features or bugfixes, and working with the TUI (Text User Interface). You'll learn how to structure your code and tests, follow commit patterns, and use suggested commands to streamline your work.

---

## Coding Conventions

- **File Naming:**  
  Use `snake_case` for all Rust source files and modules.
  ```
  // Good
  mod agent_roles;
  mod code_mode_runner;

  // Bad
  mod AgentRoles;
  mod CodeModeRunner;
  ```

- **Import Style:**  
  Use relative imports within modules.
  ```rust
  // In src/tools/handlers/code_mode.rs
  use super::spec;
  use crate::tools::handlers::common;
  ```

- **Export Style:**  
  Use named exports for modules and functions.
  ```rust
  pub mod agent_roles;
  pub fn run_tool() { ... }
  ```

- **Commit Messages:**  
  Use prefixes: `feat`, `fix`, `chore`.  
  Keep messages concise (average ~56 characters).
  ```
  feat: add code mode runner for new tool
  fix: correct agent role validation logic
  chore: update config schema for new flag
  ```

---

## Workflows

### Add or Update Tool or Tool Feature
**Trigger:** When adding, renaming, or enhancing a tool (e.g., code mode, exec, MCP tools).  
**Command:** `/add-tool`

1. Edit or create files in `codex-rs/core/src/tools/` (e.g., `code_mode.rs`, `handlers/*.rs`, `spec.rs`).
2. Update or create runner/bridge files (e.g., `code_mode_runner.cjs`, `code_mode_bridge.js`).
3. Update tool specs (`spec.rs`).
4. Update or add tests in `codex-rs/core/tests/suite/`.
5. Optionally, update protocol/models if the tool output shape changes.

**Example:**
```rust
// codex-rs/core/src/tools/code_mode.rs
pub fn run_code_mode() {
    // implementation
}
```
```js
// codex-rs/core/src/tools/code_mode_runner.cjs
module.exports = function run() { /* ... */ }
```

---

### Protocol Schema and Type Update
**Trigger:** When adding or modifying API fields, event payloads, or protocol types.  
**Command:** `/update-protocol-schema`

1. Edit JSON schema files in `codex-rs/app-server-protocol/schema/json/`.
2. Regenerate or update TypeScript types in `codex-rs/app-server-protocol/schema/typescript/`.
3. Update Rust protocol code in `codex-rs/app-server-protocol/src/protocol/`.
4. Update or add tests in `codex-rs/app-server/tests/suite/`.
5. Optionally, update `README.md` or docs.

**Example:**
```json
// codex-rs/app-server-protocol/schema/json/tool_event.json
{
  "type": "object",
  "properties": {
    "tool_id": { "type": "string" },
    "status": { "type": "string" }
  }
}
```
```rust
// codex-rs/app-server-protocol/src/protocol/tool_event.rs
pub struct ToolEvent {
    pub tool_id: String,
    pub status: String,
}
```

---

### Config Schema and Loader Update
**Trigger:** When adding or changing configuration options (e.g., agent roles, tool config, flags).  
**Command:** `/update-config-schema`

1. Edit `codex-rs/core/config.schema.json`.
2. Update loader/validation code in `codex-rs/core/src/config/`.
3. Update or add tests in `codex-rs/core/src/config/config_tests.rs`.
4. Update or add related Rust modules (e.g., `agent_roles.rs`, `mod.rs`).
5. Optionally, update `docs/config.md`.

**Example:**
```json
// codex-rs/core/config.schema.json
{
  "properties": {
    "enable_feature_x": { "type": "boolean" }
  }
}
```
```rust
// codex-rs/core/src/config/loader.rs
pub fn load_config() -> Result<Config, Error> {
    // validation logic
}
```

---

### Feature or Bugfix with Test
**Trigger:** When adding a new feature or fixing a bug and ensuring it's covered by tests.  
**Command:** `/feature`

1. Edit implementation files in the relevant module (e.g., `src/...`).
2. Update or add tests in `tests/suite/` or `tests/common/`.
3. Optionally, update related docs or README.

**Example:**
```rust
// codex-rs/core/src/agent.rs
pub fn assign_role(agent: &mut Agent, role: Role) {
    agent.role = role;
}
```
```rust
// codex-rs/core/tests/suite/agent_jobs.rs
#[test]
fn test_assign_role() {
    // test logic
}
```

---

### TUI Feature Update with Snapshots
**Trigger:** When adding or changing a TUI feature and ensuring UI output is correct.  
**Command:** `/tui-feature`

1. Edit implementation files in `codex-rs/tui/src/`.
2. Update or add snapshot files in `codex-rs/tui/src/snapshots/`.
3. Update or add tests in `codex-rs/tui/src/*/tests.rs`.

**Example:**
```rust
// codex-rs/tui/src/status.rs
pub fn render_status() -> String {
    // render logic
}
```
```
// codex-rs/tui/src/snapshots/status.snap
"Status: OK"
```

---

## Testing Patterns

- **Framework:**  
  Uses `jest` for JavaScript/TypeScript tests (`*.test.ts`).
- **Rust Tests:**  
  Place Rust tests in `tests/suite/` or `tests/common/` directories, or alongside modules as `mod tests`.

**Example:**
```rust
// codex-rs/core/tests/suite/code_mode.rs
#[test]
fn test_code_mode_execution() {
    // assert logic
}
```
```typescript
// codex-rs/app-server-protocol/schema/typescript/tool_event.test.ts
test('should parse ToolEvent', () => {
  // test logic
});
```

---

## Commands

| Command                | Purpose                                                          |
|------------------------|------------------------------------------------------------------|
| /add-tool              | Add or update a tool or tool feature                             |
| /update-protocol-schema| Update protocol JSON schemas and types                           |
| /update-config-schema  | Update config schema and loader/validation code                  |
| /feature               | Implement a new feature or bugfix with corresponding tests       |
| /tui-feature           | Add or update a TUI feature and update UI snapshots              |
```
