# Bootstrap

First-run setup so this OS auto-loads in every tool on a new machine or repo. Run once per environment.

## Steps
1. **Clone/place this repo** at a stable path (default `/path/to/engineering-brain`). If elsewhere, update the path in `adapters/README.md` commands.
2. **Wire the adapters** — run the per-tool commands in [`../adapters/README.md`](../adapters/README.md):
   - `~/.claude/CLAUDE.md` → pointer (Claude Code, all sessions + VS Code).
   - `~/.gemini/GEMINI.md` → pointer (Gemini CLI).
   - `.github/copilot-instructions.md` → pointer (Copilot, per repo).
   - Codex / Cursor / Antigravity read `AGENTS.md` natively — no action.
3. **Add the gemini-analyzer permission whitelist** to `.claude/settings.json` (see adapters README): allow `Bash(gemini:*)`, deny `Read(.env)` and `Read(**/secrets/**)`.
4. **Verify** — see [`install.md`](install.md) for the verification checklist.
5. **Seed knowledge** — `knowledge/{decisions,patterns,lessons,playbooks}/` already exist; start adding real entries as you work.

## Verify it loaded
Open any tool in a fresh session and ask: "What are your operating principles?" — it should answer from `AGENTS.md` (Clean Architecture, behavior rules, skills-on-demand) without being told.
