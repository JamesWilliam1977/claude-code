```markdown
# claude-code Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you the core development patterns, coding conventions, and common workflows used in the `claude-code` repository. The project is a TypeScript codebase built with React, following strict conventions for file naming, imports/exports, commit messages, and workflow automation. You'll learn how to contribute features, fix bugs, update documentation, manage TypeScript types, and more, all in line with the project's established best practices.

---

## Coding Conventions

### File Naming

- Use **camelCase** for file names.
  - Example: `featureTool.ts`, `userProfile.tsx`

### Imports

- Use **relative imports** for modules.
  - Example:
    ```typescript
    import { FeatureTool } from './featureTool';
    ```

### Exports

- Use **named exports**.
  - Example:
    ```typescript
    export function runCommand() { ... }
    export const FEATURE_FLAG = true;
    ```

### Commit Messages

- Use **Conventional Commits** with prefixes:
  - `fix:`, `docs:`, `feat:`, `chore:`, `build:`
- Keep commit messages concise (average ~31 characters).
  - Example: `fix: correct type in userProfile`

---

## Workflows

### Update Contributors List

**Trigger:** When a new contributor is added or contributor information changes.  
**Command:** `/update-contributors`

1. Edit `contributors.svg` to add or update contributor entries.
2. Commit with the message: `docs: update contributors`.

---

### Documentation Sync and Correction

**Trigger:** When code changes or documentation is found to be out of sync with implementation.  
**Command:** `/sync-docs`

1. Identify discrepancies between documentation and code.
2. Edit relevant `.mdx` or `.md` files (e.g., `README.md`, `CLAUDE.md`) to correct or expand documentation.
3. Commit with a message referencing the documentation correction.

---

### Feature Addition with Tests and Docs

**Trigger:** When adding a significant new capability (e.g., new command, tool, or integration).  
**Command:** `/add-feature`

1. Add or modify implementation files (e.g., `src/commands/feature.tsx`, `src/tools/FeatureTool.ts`).
2. Add or update test files (e.g., `__tests__/feature.test.ts`).
3. Update or add documentation (e.g., `docs/features/feature-name.md`, `README.md`).
4. Update `package.json` or lock files (`bun.lock`) if dependencies are involved.

**Example:**
```typescript
// src/commands/newFeature.tsx
export function newFeature() {
  // Feature implementation
}
```
```typescript
// __tests__/newFeature.test.ts
import { newFeature } from '../src/commands/newFeature';

test('should execute new feature', () => {
  expect(newFeature()).toBeDefined();
});
```

---

### TypeScript Type Fix Sweep

**Trigger:** When type errors accumulate or after major refactors affecting types.  
**Command:** `/fix-types`

1. Identify files with type errors or unsafe casts (e.g., `as any`).
2. Edit files to correct types, add interfaces, or replace unsafe casts.
3. Commit with a message indicating type fixes.

**Example:**
```typescript
// Before
const user = data as any;

// After
interface User {
  id: string;
  name: string;
}
const user: User = data;
```

---

### Bugfix with Targeted Test or Doc

**Trigger:** When a bug is reported or discovered.  
**Command:** `/fix-bug`

1. Edit implementation files to fix the bug.
2. Optionally add or update a test to cover the bug scenario.
3. Optionally update documentation to clarify behavior.
4. Commit with `fix:` prefix and bug description.

**Example:**
```typescript
// src/utils/calculate.ts
export function add(a: number, b: number): number {
  return a + b; // Fixed off-by-one error
}
```
```typescript
// __tests__/calculate.test.ts
import { add } from '../src/utils/calculate';

test('add returns correct sum', () => {
  expect(add(2, 2)).toBe(4);
});
```

---

### Add or Update Command

**Trigger:** When a new user command is needed.  
**Command:** `/add-command`

1. Create or update `src/commands/command-name/index.ts` or `command-name.tsx`.
2. Register the command in `src/commands.ts`.
3. Add supporting files as needed (e.g., `src/commands/command-name/feature.tsx`).
4. Optionally add tests and documentation.

**Example:**
```typescript
// src/commands/greet/index.ts
export function greet(name: string) {
  return `Hello, ${name}!`;
}

// src/commands.ts
export { greet } from './commands/greet';
```

---

### Feature Flag or Config Addition

**Trigger:** When introducing a new experimental or optional feature.  
**Command:** `/add-feature-flag`

1. Edit `build.ts`, `scripts/dev.ts`, or `src/constants/product.ts` to add or update a feature flag.
2. Update code to check the new flag.
3. Optionally update documentation to describe the flag.

**Example:**
```typescript
// src/constants/product.ts
export const ENABLE_NEW_FEATURE = true;

// src/commands/feature.tsx
import { ENABLE_NEW_FEATURE } from '../constants/product';

if (ENABLE_NEW_FEATURE) {
  // Run experimental feature code
}
```

---

## Testing Patterns

- **Framework:** Jest
- **Test file pattern:** `*.test.ts`
- Place tests alongside or in a `__tests__` directory.
- Use named imports for tested modules.

**Example:**
```typescript
// __tests__/featureTool.test.ts
import { featureTool } from '../src/tools/featureTool';

test('featureTool returns expected result', () => {
  expect(featureTool()).toBe('expected');
});
```

---

## Commands

| Command               | Purpose                                                        |
|-----------------------|----------------------------------------------------------------|
| /update-contributors  | Update the contributors SVG list                               |
| /sync-docs            | Synchronize and correct documentation with code                |
| /add-feature          | Add a new feature with tests and documentation                 |
| /fix-types            | Sweep and fix TypeScript type errors                           |
| /fix-bug              | Fix a bug and optionally add a test or doc update              |
| /add-command          | Add or update a CLI or chat command                            |
| /add-feature-flag     | Add or update a feature flag or configuration setting          |
```
