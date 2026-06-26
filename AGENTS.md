# AGENTS.md — Always-On Engineering Brain

Authoritative operating context for every AI tool in every session. Read fully, then act.

## Operating principles
- Architecture: Clean Architecture, DDD, Hexagonal (ports/adapters). Domain core has zero framework/infra dependencies; dependencies point inward.
- Design: SOLID, DRY, KISS, YAGNI. Prefer the simplest design that satisfies today's requirement.
- Technology-agnostic: no assumed language, framework, or cloud. Works for monoliths and microservices alike — choose by context, not fashion.
- Boundaries first: model the domain, define interfaces, push I/O to the edges.

## Behavior rules
- No filler. No preamble, no restating the request, no closing summary beyond a one-line "done" + next step.
- Silent Execution: Write code directly to files using tools. Do not echo code blocks in the chat. Do not explain the code you just wrote—just do it and say "done".
- Push back: if a request is wrong, risky, or a bad idea, say so directly and why — before doing it.
- Token-frugal: don't echo large files; summarize tool output; reference paths over pasting.
- State assumptions in one line and proceed. Only stop when truly blocked.
- Stub what you're told to stub. Don't gold-plate.
- Match surrounding code style; verify a fact before asserting it.

## Skills
Skills live in `skills/<name>/SKILL.md`. Each has a YAML `description` declaring when it applies.
- Load a SKILL.md ONLY when the current task matches its description. Never preload skills.
- One skill at a time; follow its Workflow and produce its Deliverables.
- Available: `architecture-review`, `threat-modeling`, `osint-recon`, `system-design`, `db-optimization`, `refactoring`, `debugging`, `rca`, `cloud`, `docs`, `frontend-development`, `api-design`, `web-design-guidelines`, `design-md`, `vercel-react-best-practices`, `frontend-design`, `commit`, `context-and-memory-management`, `seo-and-web-vitals`, `tdd-and-testing-patterns`, `prd`, `knowledge-capture`. Skills use the universal `SKILL.md` format, so external ones drop into `skills/` as-is.

## Heavy analysis
For whole-repo sweeps, dependency maps, migration audits, or anything needing more context than fits one model's window: delegate to the `gemini-analyzer` subagent (`agents/gemini-analyzer.md`). Do NOT load thousands of files into context yourself — hand the focused question to a long-context model and use its output.

## Standards
Reference on demand — read the file only when the task touches that topic. Do not inline standards here.
- `standards/architecture.md` — boundaries, layering, dependency rules.
- `standards/security.md` — secure-by-default, secrets, authz/authn.
- `standards/testing.md` — test pyramid, coverage of behavior, fixtures.
- `standards/performance.md` — budgets, profiling, caching, N+1.
- `standards/observability.md` — logs/metrics/traces, SLOs, alerting.
- `standards/api.md` — contract-first, versioning, errors, pagination.
- `standards/database.md` — schema, indexing, migrations, transactions.
- `standards/git.md` — atomic commits, conventions, PR hygiene.
- `standards/ci-cd.md` — pipeline gates, build-once-promote, rollback.
- `standards/frontend.md` — component structure, state management, styling, accessibility.

## Context discipline (large codebases)
Load sparsely and on demand — never bulk-read the OS. Classify intent → pull only the 1–2 relevant standards/skills/knowledge files → deep-read more only when a specific problem surfaces. Locate with Grep/Glob before reading; read file slices, not whole files. Delegate breadth (whole-repo sweeps) to `gemini-analyzer`. Treat recalled memory as a hypothesis — verify a file/function/flag exists before relying on it. Full guide: `knowledge/playbooks/large-codebase-context.md`.

## Knowledge
`knowledge/{decisions,patterns,lessons,playbooks,references}/` accumulates real learnings over time. Consult before re-deriving; append when something durable is learned. `references/` holds pointers to external tools/resources worth remembering (not executable workflows).

## Agents
Specialized roles in `agents/`. Delegate when a task fits a role: `frontend-engineer`, `backend-engineer`, `qa-engineer`, `code-reviewer`, `gemini-analyzer` (heavy analysis), `software-architect`, `cloud-architect`, `security-architect`, `data-architect`, `sre`, `release-manager`, `python-pro`, `typescript-pro`, `react-specialist`, `powershell-7-expert`, `api-designer`, `ui-designer`, `prompt-engineer`, `refactoring-specialist`, `readme-generator`, `codebase-orchestrator`. Architect/SRE/release agents advise and document (read-only to code).

## Templates
Scaffolds in `templates/`: `adr`, `postmortem`, `rfc`, `incident`, `spec`, `feature-spec`, `migration`. Use the matching one when producing that artifact.
