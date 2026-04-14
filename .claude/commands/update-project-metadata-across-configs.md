---
name: update-project-metadata-across-configs
description: Workflow command scaffold for update-project-metadata-across-configs in skill-manager.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /update-project-metadata-across-configs

Use this workflow when working on **update-project-metadata-across-configs** in `skill-manager`.

## Goal

Synchronize or update project metadata (such as name, version, product info) across multiple configuration files to ensure consistency during refactor, release, or rebranding.

## Common Files

- `package.json`
- `src-tauri/tauri.conf.json`
- `src-tauri/Cargo.toml`
- `.github/workflows/tauri.yml`
- `README.md`
- `README_CN.md`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update package.json with new name or version
- Update tauri.conf.json with new productName, identifier, or version
- Update Cargo.toml with new package name, lib name, or version
- Update workflow files (e.g., .github/workflows/tauri.yml) to match new metadata
- Update documentation files (e.g., README.md, README_CN.md) to reflect new name/version

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.