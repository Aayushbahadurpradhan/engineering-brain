# Reference: Ponytail — AI-agent minimalism ruleset ("lazy senior dev")

Source: GitHub https://github.com/DietrichGebert/ponytail. Surfaced alongside the
*"Claude Code Cuts Token Usage by 94%"* video — see [[claude-code-token-reduction-video]] (which
tool the video actually demos is unconfirmed; we captured both candidates).

## What it is
A plugin/ruleset that injects a **decision ladder before code generation** to stop AI agents
over-engineering. The "lazy senior developer" philosophy: before writing anything, ask *should this
exist at all? → can existing code be reused? → is it in stdlib / the platform already?* — and only
then write custom code. It trims **features, dependencies, and abstractions**, not safety corners.

- Benchmarked: **~54% avg code reduction** (up to **94%** on over-built things like date pickers),
  ~20% cost savings, ~27% faster, across 12 real tasks measured by actual `git diff` (not isolated
  generation). Author's numbers — unverified by us.
- **lite / full / ultra / off** intensity modes; review/audit commands to flag over-engineering;
  lifecycle hooks; zero required config.
- Hosts: Claude Code, Codex, Copilot CLI, Cursor, Windsurf, Cline, OpenCode, Gemini/Antigravity, +more.
- Install (Claude Code): `/plugin install ponytail@ponytail`. Editors without plugins: copy the static ruleset.

## Where it fits ai-os
- It's a **tooling embodiment of rules ai-os already states in prose** — AGENTS.md "Design: SOLID,
  DRY, KISS, YAGNI… simplest design that satisfies today's requirement" and "Stub what you're told to
  stub. Don't gold-plate." Ponytail enforces that at generation time instead of relying on the model
  to remember it.
- Overlaps our `simplify` / `refactoring` skills, but acts **before** code exists (prevention) rather
  than cleaning up after (cure).
- Fewer lines generated → fewer output tokens, so it doubles as a token-cut — a different mechanism
  from [[code-context-engine]] (which cuts *input* tokens by not reading whole files).

## How to action it
- Building greenfield features with an agent and want to prevent bloat → install on the **work repo**
  and run in `full`; bump to `ultra` for throwaway/prototype code, `off` when scaffolding genuinely
  needs breadth. Not needed on ai-os itself (it's prose, not a code-gen target).
- Caveat: it's a **third-party ruleset that alters how the agent generates code** — vet its rules and
  pin a version before using on client work; `ultra` can under-build, so review diffs.

## Validation status (2026-06-26)
NOT yet trialed by us. Open task: run a real feature task with Ponytail `full` vs off, compare the
`git diff` size and whether anything was under-built, and record our own numbers here.

Cross-link: [[claude-code-token-reduction-video]], [[code-context-engine]]; pairs with the `simplify`
and `refactoring` skills and AGENTS.md's KISS/YAGNI principles.
