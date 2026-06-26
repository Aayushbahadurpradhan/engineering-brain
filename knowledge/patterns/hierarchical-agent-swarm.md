# Pattern: Hierarchical Agent Swarm with Shared Memory

A multi-agent topology: a **boss/orchestrator** agent decomposes a goal and assigns roles to many
**worker** agents that build / research / test / review **in parallel**, all reading and writing a
**shared memory** so each run compounds. Captured from the "swarm of 60 agents, #1 on GitHub"
product category (Ruflo and similar — two source reels). The transferable ideas are the *topology*
and the *cost-aware model routing*, not the vendor.

Cross-links: [[large-codebase-context]].
Implement it here with the `agents/codebase-orchestrator.md` role plus parallel subagent dispatch —
an external autonomous-build loop (e.g. an orchestrator script) can drive the worker pool.

## The three parts
1. **Boss / orchestrator.** Owns the goal. Splits it into independent sub-tasks, assigns roles,
   sequences what must be serial, and merges results. Maps to `codebase-orchestrator`.
2. **Worker pool (parallel).** Specialized roles run concurrently on independent slices —
   build, research, test, review. Maps to the `agents/` roles + parallel dispatch.
3. **Shared memory.** A common store every agent reads before acting and writes after, so the swarm
   *learns across runs* instead of repeating mistakes. Maps to `knowledge/` + agent memory.

## Cost-aware model routing (the real lever)
The swarm's economics come from **not running every agent on the top model**. Route by task
difficulty: cheap/mechanical subtasks (lint fixes, boilerplate, simple tests, summarization) go to a
small/cheap model; only genuinely hard reasoning (architecture, tricky debugging, final review) hits
the frontier model (Claude Opus). Reported savings in this category (~75% cheaper) come almost
entirely from this routing, not from the parallelism.
- **Apply it here:** in `agents/`, the cheap roles can declare a smaller model in frontmatter and the
  hard roles `model: inherit`/Opus. The orchestrator decides which tier each sub-task needs *before*
  dispatch.
- **Guard:** routing too aggressively to a weak model produces work the strong model then has to
  redo — net more expensive. Route on *difficulty*, and keep the verify/review step on the strong
  model. (See `claude-api` skill for current model ids/pricing before hard-coding a tier.)

## When it pays off (and when it doesn't)
- **Pays off** when work splits into genuinely independent slices with no shared mutable state and
  the task exceeds one context window (large build, migration sweep, broad audit).
- **Doesn't** when tasks are sequentially dependent or small — spawn overhead and merge conflicts
  cost more than they save. Threshold rule from [[large-codebase-context]]: parallelize only past
  ~5 cross-directory files of independent work.
- "60 agents" is marketing. Parallelism is bounded by *independence and merge cost*, not a headcount.

## Failure modes to design against
- **Merge collisions** — workers editing overlapping files. Partition by directory/module; serialize
  the merge.
- **Context divergence** — workers drift without the shared memory. Make read-before-act mandatory.
- **Runaway cost/permissions** — many parallel agents with skip-permissions. Keep the
  detect → propose → run-on-confirm guardrail from `AGENTS.md`.
- **No verifiable done** — each worker still needs its own feedback loop (tests/build) before its
  output is trusted.

## How to run it here
- Orchestrate with `agents/codebase-orchestrator.md` plus parallel subagent dispatch.
- For autonomous parallel builds and multi-agent review/debate, drive the worker pool from an external
  orchestration loop; keep the verify/review step on the strong model.
- Shared memory = `knowledge/` (durable) + the per-project agent memory dir.
