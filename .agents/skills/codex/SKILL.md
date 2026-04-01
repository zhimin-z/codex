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
- **Architecture**: hybrid module organization
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

- `feat`
- `fix`
- `chore`

### Message Guidelines

- Average message length: ~55 characters
- Keep first line concise and descriptive
- Use imperative mood ("Add feature" not "Added feature")


*Commit message example*

```text
feat: add codex ECC bundle (.claude/commands/protocol-schema-and-type-update.md)
```

*Commit message example*

```text
chore: wire through plugin policies + category from marketplace.json (#14305)
```

*Commit message example*

```text
fix(otel): make HTTP trace export survive app-server runtimes (#14300)
```

*Commit message example*

```text
Responses: set x-client-request-id as convesration_id when talking to responses (#14312)
```

*Commit message example*

```text
add(core): arc_monitor (#13936)
```

*Commit message example*

```text
feat: add codex ECC bundle (.claude/commands/add-or-update-tool-or-tool-feature.md)
```

*Commit message example*

```text
feat: add codex ECC bundle (.claude/commands/feature-development.md)
```

*Commit message example*

```text
feat: add codex ECC bundle (.claude/homunculus/instincts/inherited/codex-instincts.yaml)
```

## Architecture

### Project Structure: Monorepo

This project uses **hybrid** module organization.

### Configuration Files

- `.devcontainer/Dockerfile`
- `.github/workflows/bazel.yml`
- `.github/workflows/cargo-deny.yml`
- `.github/workflows/ci.yml`
- `.github/workflows/cla.yml`
- `.github/workflows/close-stale-contributor-prs.yml`
- `.github/workflows/codespell.yml`
- `.github/workflows/issue-deduplicator.yml`
- `.github/workflows/issue-labeler.yml`
- `.github/workflows/rust-ci.yml`
- `.github/workflows/rust-release-prepare.yml`
- `.github/workflows/rust-release-windows.yml`
- `.github/workflows/rust-release.yml`
- `.github/workflows/sdk.yml`
- `.github/workflows/shell-tool-mcp-ci.yml`
- `.github/workflows/shell-tool-mcp.yml`
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
- `shell-tool-mcp/package.json`
- `shell-tool-mcp/tsconfig.json`

### Guidelines

- This project uses a hybrid organization
- Follow existing patterns when adding new code

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

### Database Migration

Database schema changes with migration files

**Frequency**: ~2 times per month

**Steps**:
1. Create migration file
2. Update schema definitions
3. Generate/update types

**Files typically involved**:
- `**/schema.*`

**Example commit sequence**:
```
chore: add a separate reject-policy flag for skill approvals (#14271)
Stabilize pipe process stdin round-trip test (#14013)
prompt changes to guardian (#14263)
```

### Feature Development

Standard feature implementation workflow

**Frequency**: ~18 times per month

**Steps**:
1. Add feature implementation
2. Add tests for feature
3. Update documentation

**Files typically involved**:
- `codex-rs/app-server-protocol/schema/typescript/v2/*`
- `codex-rs/app-server-protocol/schema/typescript/*`
- `**/*.test.*`
- `**/api/**`

**Example commit sequence**:
```
feat: Allow sync with remote plugin status. (#14176)
Add granular metrics for cloud requirements load (#14108)
fix(python-sdk): stop checking in codex binaries; stage pinned runtim… (#14232)
```

### Protocol Schema And Types Update

Update or add new fields to the protocol schema and propagate changes through TypeScript types, Rust protocol code, and tests.

**Frequency**: ~4 times per month

**Steps**:
1. Edit or add JSON schema files in codex-rs/app-server-protocol/schema/json/
2. Regenerate or update corresponding TypeScript types in codex-rs/app-server-protocol/schema/typescript/
3. Update Rust protocol code in codex-rs/app-server-protocol/src/protocol/
4. Update or add related tests in codex-rs/app-server/tests/suite/v2/
5. Update core/protocol models if needed (codex-rs/protocol/src/models.rs, codex-rs/protocol/src/protocol.rs)
6. Update documentation (optional, e.g., codex-rs/app-server/README.md)

**Files typically involved**:
- `codex-rs/app-server-protocol/schema/json/*.json`
- `codex-rs/app-server-protocol/schema/typescript/**/*.ts`
- `codex-rs/app-server-protocol/src/protocol/**/*.rs`
- `codex-rs/app-server/tests/suite/v2/**/*.rs`
- `codex-rs/protocol/src/models.rs`
- `codex-rs/protocol/src/protocol.rs`

**Example commit sequence**:
```
Edit or add JSON schema files in codex-rs/app-server-protocol/schema/json/
Regenerate or update corresponding TypeScript types in codex-rs/app-server-protocol/schema/typescript/
Update Rust protocol code in codex-rs/app-server-protocol/src/protocol/
Update or add related tests in codex-rs/app-server/tests/suite/v2/
Update core/protocol models if needed (codex-rs/protocol/src/models.rs, codex-rs/protocol/src/protocol.rs)
Update documentation (optional, e.g., codex-rs/app-server/README.md)
```

### Tool Spec And Handler Update

Add or update a tool's implementation, spec, and tests, often for new features or bug fixes.

**Frequency**: ~6 times per month

**Steps**:
1. Edit or add tool handler code in codex-rs/core/src/tools/handlers/
2. Update tool spec in codex-rs/core/src/tools/spec.rs
3. Update or add related code in codex-rs/core/src/tools/*.rs (e.g., code_mode.rs, context.rs, parallel.rs)
4. Update or add JS/bridge files if needed (e.g., code_mode_bridge.js, code_mode_runner.cjs)
5. Update or add tests in codex-rs/core/tests/suite/
6. Update protocol models if tool output changes (codex-rs/protocol/src/models.rs)

**Files typically involved**:
- `codex-rs/core/src/tools/handlers/*.rs`
- `codex-rs/core/src/tools/spec.rs`
- `codex-rs/core/src/tools/*.rs`
- `codex-rs/core/src/tools/*.js`
- `codex-rs/core/src/tools/*.cjs`
- `codex-rs/core/tests/suite/*.rs`
- `codex-rs/protocol/src/models.rs`

**Example commit sequence**:
```
Edit or add tool handler code in codex-rs/core/src/tools/handlers/
Update tool spec in codex-rs/core/src/tools/spec.rs
Update or add related code in codex-rs/core/src/tools/*.rs (e.g., code_mode.rs, context.rs, parallel.rs)
Update or add JS/bridge files if needed (e.g., code_mode_bridge.js, code_mode_runner.cjs)
Update or add tests in codex-rs/core/tests/suite/
Update protocol models if tool output changes (codex-rs/protocol/src/models.rs)
```

### Feature Development With Tests

Develop a new feature or significant enhancement, including implementation, tests, and often documentation.

**Frequency**: ~5 times per month

**Steps**:
1. Implement feature in relevant Rust/JS files (e.g., codex-rs/core/src/, codex-rs/tui/src/)
2. Update or add tests in codex-rs/core/tests/suite/ or codex-rs/tui/src/snapshots/
3. Update documentation if applicable (e.g., README.md, docs/*.md)

**Files typically involved**:
- `codex-rs/core/src/**/*.rs`
- `codex-rs/core/tests/suite/*.rs`
- `codex-rs/tui/src/**/*.rs`
- `codex-rs/tui/src/snapshots/*.snap`
- `docs/*.md`
- `README.md`

**Example commit sequence**:
```
Implement feature in relevant Rust/JS files (e.g., codex-rs/core/src/, codex-rs/tui/src/)
Update or add tests in codex-rs/core/tests/suite/ or codex-rs/tui/src/snapshots/
Update documentation if applicable (e.g., README.md, docs/*.md)
```

### Config Schema And Implementation Update

Update or extend configuration schema and propagate changes through config handling code and tests.

**Frequency**: ~3 times per month

**Steps**:
1. Edit codex-rs/core/config.schema.json
2. Update config handling code in codex-rs/core/src/config/
3. Update or add related tests in codex-rs/core/src/config/config_tests.rs or codex-rs/core/tests/suite/
4. Update documentation if needed (e.g., docs/config.md)

**Files typically involved**:
- `codex-rs/core/config.schema.json`
- `codex-rs/core/src/config/*.rs`
- `codex-rs/core/src/config/config_tests.rs`
- `codex-rs/core/tests/suite/*.rs`
- `docs/config.md`

**Example commit sequence**:
```
Edit codex-rs/core/config.schema.json
Update config handling code in codex-rs/core/src/config/
Update or add related tests in codex-rs/core/src/config/config_tests.rs or codex-rs/core/tests/suite/
Update documentation if needed (e.g., docs/config.md)
```

### Agent Schema And Behavior Update

Update agent-related schemas, role files, handler code, and tests to support new agent features or metadata.

**Frequency**: ~2 times per month

**Steps**:
1. Edit agent schema or role files (e.g., codex-rs/core/config.schema.json, codex-rs/core/src/agent/role.rs)
2. Update agent config/behavior code (e.g., codex-rs/core/src/config/agent_roles.rs, codex-rs/core/src/tools/handlers/multi_agents.rs)
3. Update or add tests (e.g., codex-rs/core/tests/suite/agent_jobs.rs, codex-rs/core/tests/suite/subagent_notifications.rs)
4. Update documentation if applicable

**Files typically involved**:
- `codex-rs/core/config.schema.json`
- `codex-rs/core/src/agent/role.rs`
- `codex-rs/core/src/config/agent_roles.rs`
- `codex-rs/core/src/tools/handlers/multi_agents.rs`
- `codex-rs/core/tests/suite/agent_jobs.rs`
- `codex-rs/core/tests/suite/subagent_notifications.rs`

**Example commit sequence**:
```
Edit agent schema or role files (e.g., codex-rs/core/config.schema.json, codex-rs/core/src/agent/role.rs)
Update agent config/behavior code (e.g., codex-rs/core/src/config/agent_roles.rs, codex-rs/core/src/tools/handlers/multi_agents.rs)
Update or add tests (e.g., codex-rs/core/tests/suite/agent_jobs.rs, codex-rs/core/tests/suite/subagent_notifications.rs)
Update documentation if applicable
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
