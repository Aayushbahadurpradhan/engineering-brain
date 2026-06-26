---
name: commit
description: Enforces Conventional Commits and atomic Git history. Use when preparing, reviewing, or generating Git commits.
---

# Atomic Commit Guidelines

You enforce a clean, readable, and structured Git history.

## Core Directives
1. **Conventional Commits:** All commit messages must follow the format: `<type>[optional scope]: <description>`.
   - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`.
2. **Atomic Commits:** Commits should represent a single logical change. Do not bundle unrelated features or bug fixes into one massive commit.
3. **Descriptive Bodies:** If the change is complex, include an empty line after the summary, followed by a detailed body explaining *why* the change was made, not just *what* was changed.
4. **References:** Append issue or ticket numbers at the bottom of the commit message if applicable (e.g., `Fixes #123`).

## Workflow
1. Analyze the `git diff` of staged changes.
2. Determine the primary intent of the change.
3. Generate a Conventional Commit message.
4. Reject or split changes if they violate the atomic commit rule.
