# Install & Verify

Idempotent checklist to wire the OS into every tool. Re-running overwrites pointers safely. Adjust `/path/to/engineering-brain` if your clone differs.

## 1. Claude Code (global)
```powershell
$p = "$HOME\.claude"; New-Item -ItemType Directory -Force $p | Out-Null
Set-Content "$p\CLAUDE.md" "Read and follow /path/to/engineering-brain/AGENTS.md as authoritative for all work in every session."
```

## 2. Gemini CLI (global)
```powershell
$p = "$HOME\.gemini"; New-Item -ItemType Directory -Force $p | Out-Null
Set-Content "$p\GEMINI.md" "Read and follow /path/to/engineering-brain/AGENTS.md as authoritative for all work in every session."
```

## 3. Copilot (per repo)
```powershell
New-Item -ItemType Directory -Force ".github" | Out-Null
Set-Content ".github\copilot-instructions.md" "Read and follow /path/to/engineering-brain/AGENTS.md as authoritative for all work in every session."
```

## 4. gemini-analyzer permissions (`.claude/settings.json`)
Merge into the `permissions` block:
```json
{ "permissions": { "allow": ["Bash(gemini:*)"], "deny": ["Read(.env)", "Read(**/secrets/**)"] } }
```

## 5. Verify
- [ ] `Test-Path $HOME\.claude\CLAUDE.md` → True
- [ ] `Test-Path $HOME\.gemini\GEMINI.md` → True
- [ ] `Test-Path .github\copilot-instructions.md` → True (in repos using Copilot)
- [ ] `gemini --list-models` returns model names (Gemini CLI installed & authed)
- [ ] Fresh Claude Code session answers "operating principles?" from AGENTS.md
- [ ] Codex/Cursor/Antigravity: open repo, confirm AGENTS.md is picked up natively
