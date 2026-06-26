# Runbook: Code Context Engine (CCE) on a large code repo

Use only when **all three** hold: the repo is **large**, **code-heavy**, and a session is **actually
bleeding context** on repeated file reads. Never on ai-os itself (small/markdown). Background:
[[code-context-engine]], [[large-codebase-context]].

- **Status:** Not yet validated on a real large repo (as of 2026-06-26).
- **Decision:** Documented-only; see verdict in [[claude-code-token-reduction-video]].

## 1. Install & index
```
uv tool install code-context-engine
cd /path/to/large/code/repo        # NOT ai-os
cce init                            # auto-detects the editor and writes MCP config
```
Confirm the MCP server registered, then prefer its `context_search` / `related_context` over bulk `Read`.

## 2. Use
- Search the index first; open the full file only on a confirmed hit.
- Treat every hit as a **hypothesis** — verify the code still exists/matches before acting (the index
  may be stale). This is the same rule as `large-codebase-context.md` §5.

## 3. Re-sync (the drift chore)
- Re-index after meaningful edits, branch switches, or pulls — a stale index gives confident-but-wrong
  hits. If unsure whether the index is current, re-run indexing or fall back to grep-and-read.

## 4. Vet before client work
- CCE is a **third-party MCP server with full read access** to the codebase. Confirm it's acceptable
  on the client's code (no cloud egress — it processes locally, but still get sign-off) before wiring in.

## 5. Tear down
- Remove the MCP entry when the heavy-lookup phase is over; don't leave it wired into small repos.

## One-time validation task (do this before recommending CCE in anger)
On a genuinely large code repo, measure tokens/query for the same task **with vs. without** CCE, and
note the re-sync overhead. Record the real numbers in [[code-context-engine]] — replace the author's
FastAPI benchmark with our own. Until then, treat the 94% figure as unverified-by-us.
