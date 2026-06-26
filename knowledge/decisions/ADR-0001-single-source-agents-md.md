# ADR-0001: One authoritative AGENTS.md with per-tool pointer files

- **Status:** Accepted
- **Date:** 2026-06-10
- **Deciders:** maintainers

## Context
Multiple AI coding tools are in daily use (Claude Code, Gemini CLI, Copilot, Cursor, Codex, Windsurf, Antigravity), each with its own instruction-file convention (`CLAUDE.md`, `GEMINI.md`, `.cursorrules`, `.windsurfrules`, `.github/copilot-instructions.md`). Duplicating standards, skills, and behavior rules per tool drifts immediately and multiplies maintenance. Instructions must also stay small per session — tools have finite context windows.

## Decision
We will keep one authoritative `AGENTS.md` at the repo root. Every tool-specific file is a single line: "Read and follow AGENTS.md as authoritative for all work in every session." AGENTS.md itself stays lean and references `skills/`, `standards/`, `agents/`, `templates/`, and `knowledge/` lazily — files are loaded only when the task matches.

## Options considered
1. **Per-tool full instruction files** — native to each tool; drifts, duplicates, unmaintainable.
2. **Symlinks to one file** — no drift, but symlinks are fragile on Windows and in some tools' file loaders.
3. **One-line pointer files → AGENTS.md (chosen)** — trivial to maintain, works everywhere, tools that read `AGENTS.md` natively need nothing.

## Consequences
- Positive: zero drift; new tools wire up with one line; OS content grows without growing session cost.
- Negative / trade-offs: relies on each tool actually following the pointer instruction; one extra indirection hop per session.
- Follow-ups: paths in AGENTS.md must stay relative to the repo root (fixed 2026-06-10 — they previously carried a spurious `ai-os/` prefix).

## References
- `adapters/README.md` — per-tool wiring commands.
- `bootstrap/README.md` — first-run setup and verification.
