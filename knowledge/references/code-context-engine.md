# Reference: Code Context Engine (CCE) — semantic code index as an MCP server

Source: YouTube *"Claude Code Cuts Token Usage by 94%"*
(https://www.youtube.com/watch?v=UvVVATGIm7k). Full distillation: [[claude-code-token-reduction-video]].

## What it is
An open-source **MCP server** that indexes a codebase locally so the agent **semantic-searches the
index** instead of reading whole files. Pipeline: tree-sitter chunking → hybrid vector + BM25
retrieval → graph expansion along CALLS/IMPORTS edges → compression to signatures/docstrings.
Exposes tools Claude calls automatically (`context_search`, `related_context`, `session_recall`,
`set_output_compression`, …). Code stays local — no cloud processing.

Reported win: ~83,681 → ~4,927 tokens/query on a FastAPI repo (author's benchmark, one repo — treat
as "large on big repos," not guaranteed).

**Validation status (2026-06-26): NOT yet validated by us.** Decision was *documented-only* — we did
**not** `cce init` ai-os (it's small/markdown, so CCE buys nothing and only tests plumbing, not the
real drift/scale failure modes). Open task: measure tokens/query with-vs-without CCE on a genuinely
large *code* repo, then replace the author's benchmark above with our own numbers. Runbook:
`templates/cce-runbook.md`.

## Setup
```
uv tool install code-context-engine
cd /path/to/project
cce init          # auto-detects Claude Code / Cursor / VS Code / Gemini CLI and writes MCP config
```

## Where it fits ai-os (and where it doesn't)
- **Use it** on **large repos** where grep-and-read still burns context — it's a retrieval layer
  *between* `Grep`/`Glob` and a full-file `Read`. Wired into the [[large-codebase-context]] playbook.
- **Don't bother** on small repos: index build + drift cost more than the file reads it saves
  (consistent with the playbook's threshold rule — only reach for heavy tooling past ~5 cross-dir files).
- **Watch the drift.** The index goes stale as you edit; re-sync, or it gives confident-but-outdated
  answers. This directly collides with our rule to *treat recalled state as a hypothesis and verify
  before relying* — so adopt only with a re-index habit, and still verify a hit before acting on it.
- **Vet before client work.** It's a third-party MCP server with read access to the whole codebase.

## How to action it
- Big-repo session bleeding context on file reads → consider `cce init` and prefer `context_search`
  over bulk `Read`. Otherwise stick to the cheaper grep-then-read default.
- For one-shot whole-repo breadth (maps, audits) we already delegate to `gemini-analyzer`; CCE is for
  *repeated targeted lookups within a session*, not one big sweep.

Cross-link: [[claude-code-token-reduction-video]], [[large-codebase-context]]; pairs with the
`context-and-memory-management` skill and [[claude-code-mega-config]].
