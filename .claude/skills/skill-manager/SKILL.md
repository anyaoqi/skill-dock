```markdown
# skill-manager Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches the core development patterns and workflows for the `skill-manager` repository, a Rust backend with a Vue frontend. It covers coding conventions, file organization, commit practices, and key maintenance workflows such as synchronizing project metadata and managing npm scripts and dependencies.

## Coding Conventions

### File Naming
- Use **camelCase** for all file names.
  - Example: `userProfile.vue`, `projectSettings.rs`

### Import Style
- Use **relative imports** throughout the codebase.
  - Example (Vue):
    ```js
    import { fetchData } from './apiClient'
    ```
  - Example (Rust):
    ```rust
    mod utils;
    use crate::utils::parse_config;
    ```

### Export Style
- Use **named exports** in JavaScript/TypeScript modules.
  - Example:
    ```js
    // src/utils/format.ts
    export function formatDate(date) { /* ... */ }
    export const DATE_FORMAT = 'YYYY-MM-DD'
    ```

### Commit Patterns
- Follow **conventional commit** style.
- Use prefixes like `fix` and `refactor`.
  - Example:
    ```
    fix: correct typo in userProfile component
    refactor: move validation logic to utils
    ```
- Average commit message length: ~44 characters.

## Workflows

### Update Project Metadata Across Configs
**Trigger:** When updating project name, version, or related metadata across all configs for a release, rebranding, or CI/CD process.  
**Command:** `/sync-metadata`

1. Update `package.json` with the new name or version.
2. Update `src-tauri/tauri.conf.json` with the new `productName`, `identifier`, or `version`.
3. Update `src-tauri/Cargo.toml` with the new package name, lib name, or version.
4. Update workflow files (e.g., `.github/workflows/tauri.yml`) to match the new metadata.
5. Update documentation files (`README.md`, `README_CN.md`) to reflect the new name/version.
6. Update other related config files (e.g., `src-tauri/targets/windows-manifest.xml`, comments in `src/types.ts`).
7. Commit all changes together.

**Example:**
```jsonc
// package.json
{
  "name": "skill-manager",
  "version": "2.0.0"
}
```
```toml
# src-tauri/Cargo.toml
[package]
name = "skill-manager"
version = "2.0.0"
```

---

### Add and Remove NPM Scripts and Dependencies
**Trigger:** When adding a new npm script (e.g., for dev mode) or removing an ineffective script/dependency after testing.  
**Command:** `/update-scripts`

1. Add or remove the script in `package.json`.
2. Add or remove the dependency in `package.json`.
3. Update lock files (`pnpm-lock.yaml`, `src-tauri/Cargo.lock`) accordingly.
4. Commit all related changes together.

**Example:**
```jsonc
// package.json
"scripts": {
  "dev": "vue-cli-service serve",
  "lint": "eslint ."
},
"dependencies": {
  "vue": "^3.2.0"
}
```
After removal:
```jsonc
// package.json
"scripts": {
  "dev": "vue-cli-service serve"
},
"dependencies": {
  "vue": "^3.2.0"
}
```

## Testing Patterns

- **Test file pattern:** Files are named with `*.test.*` (e.g., `userProfile.test.ts`).
- **Testing framework:** Not explicitly specified; check test files for framework usage.
- **Example:**
  ```js
  // userProfile.test.ts
  import { mount } from '@vue/test-utils'
  import UserProfile from './userProfile.vue'

  test('renders user name', () => {
    const wrapper = mount(UserProfile, { props: { name: 'Alice' } })
    expect(wrapper.text()).toContain('Alice')
  })
  ```

## Commands

| Command         | Purpose                                                         |
|-----------------|-----------------------------------------------------------------|
| /sync-metadata  | Synchronize project metadata across all config and doc files    |
| /update-scripts | Add or remove npm scripts and dependencies in the project       |
```
