# Playbook: Working in a Large Codebase Without Blowing Context

How to stay effective when the repo is far bigger than the context window. Default to the cheapest layer that answers the question.

## 1. Sparse, on-demand loading (don't preload)
- `AGENTS.md` is a lean index, not a manual — keep it that way; it loads every session.
- Load a `SKILL.md` or `standards/<topic>.md` ONLY when the task matches. Never bulk-read the OS.
- Read the slice of a file you need (offset/limit), not the whole file.

## 2. Three-layer retrieval
1. **Intent** — classify the task (debug / design / review / migrate). Zero file reads.
2. **Top-1–2 load** — pull only the 1–2 directly relevant standards/skills/knowledge files.
3. **Deep read on trigger** — open more only when a specific problem surfaces (e.g. deploy failure → `lessons/`), not speculatively.

### Locating code: cheapest layer first
**Baseline (default, always):** `Grep`/`Glob` → read the slice → (only if the slice isn't enough)
full read; delegate whole-repo breadth to `gemini-analyzer`. This is the default and stays the default.

**Conditional escalation — a semantic index.** *Only* when **all three** hold — the repo is **large
AND code-heavy AND a session is actually bleeding context on repeated lookups** — add a semantic-index
layer between grep and full read: index once, then search the index so each query returns ~hundreds of
relevant tokens instead of a whole file. The [[code-context-engine]] tool (an MCP server) does this;
reported ~94% fewer tokens/query on big *code* repos. **Never the default**, and never on ai-os itself
(it's small/markdown — pure overhead). Caveats: the index **drifts** as you edit (re-sync, and still
verify a hit before acting — per §5), and it's a third-party server with full read access (vet before
client work). Runbook: `templates/cce-runbook.md`. Skip on small or prose-heavy repos (see §4).

## 3. Delegate breadth, keep depth
- Whole-repo sweeps, dependency maps, migration audits → hand to the `gemini-analyzer` subagent (`gemini --all-files --yolo -p "<focused question>"`). Don't load thousands of files into your own context.
- For parallel exploration of a huge monorepo, spawn focused `Explore`/mapper subagents per area; have each write a short markdown findings file and read the summaries (~hundreds of tokens), not the raw source.
- Use `Grep`/`Glob` to locate before you read. Search, then open the hit.

## 4. Threshold rule
Use subagents/parallel mappers only when a task touches more files than fit comfortably in context (roughly >5 cross-directory files). For small tasks the spawn overhead costs more than it saves.

## 5. Memory hygiene
- Treat recalled memory/knowledge as a hypothesis. **Verify a file/function/flag still exists before relying on it.**
- Date-stamp durable learnings; prune or supersede stale ones — stale memory cited as fact is the top failure mode.
- When `AGENTS.md` or a knowledge file drifts past usefulness, compact it; move detail into a topic file and leave a pointer.
