# Standard: Git & Version Control

## Purpose
Keep history a readable, bisectable record of intent — so any change can be understood, reviewed, and reverted cleanly.

## Principles
- A commit is one logical change with a clear reason; history tells a story.
- main is always releasable; risky work happens on branches.
- Review is a gate, not a formality.

## Rules
- Atomic commits: one concern each; build/tests pass at every commit.
- Conventional commit subject: `type(scope): summary` (feat/fix/docs/refactor/test/chore), imperative, ≤72 chars; body explains why.
- Short-lived feature branches off main; rebase to keep linear history before merge (don't rebase shared/pushed branches others use).
- Never commit secrets, credentials, or large binaries; enforce via `.gitignore` + secret scanning.
- All changes to protected branches via reviewed PR; CI green before merge.
- Reference issues/ADRs in the body; squash noise, preserve meaningful steps.

## Checklist
- [ ] Each commit is atomic and green.
- [ ] Messages follow the convention; body says why.
- [ ] No secrets/binaries committed.
- [ ] Branch short-lived; history clean before merge.
- [ ] PR reviewed, CI passing.

## Examples
- `fix(auth): reject expired refresh tokens` + body describing the exploit it closes.
- Rebase a 6-WIP-commit branch into 2 meaningful commits before opening the PR.

## Anti-patterns
- `git commit -m "stuff"` / "wip" / "fix" with no context.
- Giant mixed commits touching ten unrelated things.
- Force-pushing a shared branch others are based on.
- Committing `.env`, keys, or 50MB assets.
