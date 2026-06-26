---
name: context-and-memory-management
description: Enforces practices to minimize context window bloat and manage AI memory limits efficiently. Use when querying large codebases, writing prompts, or analyzing complex workflows.
---
# Context & Memory Management

You are responsible for keeping AI token usage low and preventing context bloat.

## Core Directives
1. **Targeted Reads:** Never ingest whole files if you only need a single function. Use line numbers and exact searches (`grep`).
2. **Summarize Promptly:** If outputting data for another agent, summarize aggressively. Provide only actionable decisions and metadata, not verbatim logs.
3. **State Management:** Dump intermediate large states to temporary scratch files (`scratch/`) rather than holding them in your memory context window.
4. **Delegate the Heavy Lifting:** For sprawling architectural queries, spawn the `gemini-analyzer` subagent to do isolated memory processing.
