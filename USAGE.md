# Usage

Day-to-day guide: what to say so a tool reaches for the right part of the brain. You rarely name files — you describe the task, and the tool loads the matching skill/standard/agent on demand (per `AGENTS.md`).

## Skills — say the task, the skill loads
Skills live in `skills/<name>/SKILL.md` and declare *when* they apply. Examples:

| You say… | Skill that applies |
|----------|--------------------|
| "design the API for X" / "review this endpoint contract" | `api-design` |
| "this is broken, help me debug" | `debugging` |
| "do a root-cause analysis of the incident" | `rca` |
| "threat-model this feature" | `threat-modeling` |
| "write a PRD for …" / "spec out this feature" | `prd` |
| "review the architecture" | `architecture-review` |
| "optimize this query / schema" | `db-optimization` |
| "clean this up / refactor" | `refactoring` |
| "write tests for …" | `tdd-and-testing-patterns` |
| "capture this article/video into our knowledge" | `knowledge-capture` |
| "we're running low on context / summarize state" | `context-and-memory-management` |

Full list is in [`AGENTS.md`](AGENTS.md).

## Standards — the rules a task is held to
Read on demand when a task touches the topic: `architecture`, `security`, `testing`, `performance`, `observability`, `api`, `database`, `git`, `ci-cd`, `frontend`. e.g. *"follow our security standard"* → loads `standards/security.md`.

## Agents — delegate a role
Hand a fitting task to a role in `agents/`: `backend-engineer`, `frontend-engineer`, `qa-engineer`, `code-reviewer`, `security-architect`, `software-architect`, `gemini-analyzer` (whole-repo sweeps / heavy analysis), and more.

## Templates — produce an artifact
*"write an ADR for this decision"* → `templates/adr.md`; likewise `rfc`, `postmortem`, `incident`, `spec`, `feature-spec`, `migration`.

## Knowledge — learn in place
When something durable is learned, it lands in `knowledge/{decisions,patterns,lessons,playbooks,references}/` — one learning per file, cross-linked with `[[name]]`. Consult it before re-deriving.
