# engineering-brain — a portable engineering brain for AI coding tools

One repo that every AI coding assistant (Claude Code, Gemini CLI, GitHub Copilot, Cursor, Codex, Windsurf, Antigravity) loads as its operating context in every session. Write your standards, skills, and learnings once; every tool follows them.

> Vendor-neutral and model-agnostic. No secrets, no accounts, no machine-specific config — just the reusable operating system. Bring your own keys and wiring.

## How it works

[`AGENTS.md`](AGENTS.md) is the single source of truth. Every tool-specific rule file is a one-line pointer to it:

```
CLAUDE.md · GEMINI.md · .cursorrules · .windsurfrules · .github/copilot-instructions.md
        └──────────────→ AGENTS.md (authoritative)
                              └──→ skills/ · standards/ · agents/ · templates/ · knowledge/
```

AGENTS.md stays small and references everything else lazily — a tool loads a skill, standard, or agent file only when the task at hand needs it. This keeps every session token-frugal regardless of how much the brain grows. The rationale is recorded in [ADR-0001](knowledge/decisions/ADR-0001-single-source-agents-md.md).

New here? [`USAGE.md`](USAGE.md) is the day-to-day guide — what to say to trigger each skill, agent, standard, and template.

## Layout

| Directory | What it holds |
|-----------|---------------|
| [`skills/`](skills/) | Task playbooks (`debugging`, `rca`, `threat-modeling`, `api-design`, `prd`, …) in universal `SKILL.md` format — external skills drop in as-is |
| [`standards/`](standards/) | Reference rules: security, testing, api, database, ci-cd, frontend, … |
| [`agents/`](agents/) | Specialized subagent roles (`backend-engineer`, `security-architect`, `gemini-analyzer`, …) |
| [`templates/`](templates/) | Artifact scaffolds: ADR, RFC, postmortem, incident, spec, migration |
| [`knowledge/`](knowledge/) | Accumulated real learnings: decisions, patterns, lessons, playbooks, references |
| [`adapters/`](adapters/) | One-line wiring per tool so it auto-loads AGENTS.md |
| [`bootstrap/`](bootstrap/) | First-run setup for a new machine |

## Quick start

1. Clone to a stable path.
   ```bash
   git clone https://github.com/Aayushbahadurpradhan/engineering-brain.git
   ```
2. Wire your tools — follow [`bootstrap/README.md`](bootstrap/README.md) and [`adapters/README.md`](adapters/README.md). For most tools it's a single one-line pointer file; Codex / Cursor / Antigravity read `AGENTS.md` natively.
3. Verify: open any tool in a fresh session and ask *"What are your operating principles?"* — it should answer from AGENTS.md unprompted.

## Philosophy

- **One brain, many hands** — tools change, the brain persists.
- **Lazy loading** — context on demand, never bulk-read.
- **Learn in place** — durable lessons land in `knowledge/`, not in chat history.
- **Delegate breadth** — whole-repo sweeps go to the `gemini-analyzer` subagent, not your context window.
- **No secrets in the repo** — keys live in your environment or a gitignored `secrets/`; never commit them. See [SECURITY.md](SECURITY.md).

## Contributing

Contributions are welcome via pull request — new skills, agents, standards, templates, and battle-tested knowledge entries. Read [CONTRIBUTING.md](CONTRIBUTING.md) for the workflow, conventions, and the secrets policy, and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) before opening a PR.

## License

[MIT](LICENSE) — use it, fork it, adapt it for your own team.
