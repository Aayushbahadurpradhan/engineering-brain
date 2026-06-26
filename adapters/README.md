# Adapters — wire every tool to this repo's AGENTS.md

`AGENTS.md` at the repo root is the single source of truth. Codex, Cursor, and Antigravity read `AGENTS.md` natively — no wiring needed; just open the repo. The tools below need a one-line global pointer so they auto-load it in every session.

Replace `/path/to/engineering-brain` below if your clone lives elsewhere. Pointers are intentionally one line: they delegate, they don't duplicate.

## Claude Code (global — all sessions + VS Code)
`~/.claude/CLAUDE.md`:
```powershell
$p = "$HOME\.claude"; New-Item -ItemType Directory -Force $p | Out-Null
Set-Content "$p\CLAUDE.md" "Read and follow /path/to/engineering-brain/AGENTS.md as authoritative for all work in every session."
```

## Gemini CLI (global)
`~/.gemini/GEMINI.md`:
```powershell
$p = "$HOME\.gemini"; New-Item -ItemType Directory -Force $p | Out-Null
Set-Content "$p\GEMINI.md" "Read and follow /path/to/engineering-brain/AGENTS.md as authoritative for all work in every session."
```

## GitHub Copilot (per-repo)
`.github/copilot-instructions.md`:
```powershell
New-Item -ItemType Directory -Force ".github" | Out-Null
Set-Content ".github\copilot-instructions.md" "Read and follow /path/to/engineering-brain/AGENTS.md as authoritative for all work in every session."
```

## Codex / Cursor / Antigravity
Native `AGENTS.md` support — open the repo, no config required.

## Windsurf (per-repo)
`.windsurfrules` at the repo root (already present here):
```powershell
Set-Content ".windsurfrules" "Read and follow AGENTS.md as authoritative for all work in every session."
```

## Permission whitelist for gemini-analyzer
Add to `.claude/settings.json` so the subagent can run Gemini but never read secrets:
```json
{
  "permissions": {
    "allow": ["Bash(gemini:*)"],
    "deny": ["Read(.env)", "Read(**/secrets/**)"]
  }
}
```
