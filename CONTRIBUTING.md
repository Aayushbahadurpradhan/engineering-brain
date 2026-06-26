# Contributing to engineering-brain

Thanks for helping build a shared, vendor-neutral operating brain for AI coding tools. This guide is the "committing guide" — how to propose changes, the conventions, and the rules that keep the repo safe to be public.

## Ground rules (read first)

1. **Never commit secrets.** No API keys, tokens, `.env` files, or `secrets/` contents — ever. Keys belong in your environment. See [SECURITY.md](SECURITY.md). PRs that add secrets will be closed and the credential treated as compromised.
2. **No personal or machine-specific content.** No real names, employer/client names, absolute home paths (`C:\Users\you`, `/home/you`), account profiles, or private project references. Keep everything generic and reusable.
3. **Stay vendor-neutral and model-agnostic.** Prefer "a strong model" / "a long-context model" over hard-coding one vendor, except where a concrete example genuinely helps (then mark it as an example).
4. **Be kind.** See the [Code of Conduct](CODE_OF_CONDUCT.md).

## How to contribute

1. **Fork** the repo and create a branch: `git checkout -b feat/<short-name>`.
2. Make your change following the conventions below.
3. Run the local checks (below) so CI passes.
4. **Open a pull request** against `main` with a clear description of *what* and *why*. Link any related issue.
5. A maintainer reviews. Direct pushes to `main` are not accepted — everything lands via reviewed PR.

## What to contribute

| Type | Where | Format |
|------|-------|--------|
| A new task playbook | `skills/<name>/SKILL.md` | YAML frontmatter (`name`, `description` = *when to use it*) + `## Workflow` + `## Deliverables` |
| A reference rule set | `standards/<topic>.md` | Timeless rules for a topic; keep it concise and skimmable |
| A subagent role | `agents/<role>.md` | Role definition; state whether it edits code or only advises |
| An artifact scaffold | `templates/<name>.md` | A fill-in-the-blanks template |
| A durable learning | `knowledge/{decisions,patterns,lessons,playbooks,references}/` | One learning per file; dated; cross-link with `[[name]]` |

- **Skills** must declare *when they apply* in the `description` — that's how a tool decides to load them. Keep `AGENTS.md`'s skill list in sync when you add one.
- **Knowledge** entries are specific and dated. `references/` points to external tools (what it is, why it matters, how to use it). Don't duplicate what a standard already says.
- Keep `AGENTS.md` **lean** — it loads every session. Add detail to a topic file and reference it, don't inline it.

## Commit conventions

- **One logical change per commit.** Atomic and reversible.
- **[Conventional Commits](https://www.conventionalcommits.org/)** style:
  `type(scope): summary` — types: `feat`, `fix`, `docs`, `refactor`, `chore`, `test`.
  - e.g. `feat(skills): add load-testing skill`, `docs(standards): clarify api pagination rules`.
- Subject in the imperative mood, ≤ 72 chars, no trailing period.
- Body (optional): *why*, not *what* the diff already shows.

## Local checks before you push

```bash
# 1. No secrets / personal data staged (CI enforces this too)
git diff --cached | grep -nEi 'nvapi-|sk-[a-z0-9]|AKIA[0-9A-Z]{16}|-----BEGIN .*PRIVATE KEY-----' && echo "BLOCKED: secret-like content" || echo "clean"

# 2. Pointer files still delegate to AGENTS.md
grep -L 'AGENTS.md' CLAUDE.md GEMINI.md .cursorrules .windsurfrules .github/copilot-instructions.md

# 3. A new skill has the required shape
test -f skills/<name>/SKILL.md && head -5 skills/<name>/SKILL.md
```

## PR checklist

- [ ] No secrets, keys, or `.env`/`secrets/` content.
- [ ] No personal/employer/client names or absolute home paths.
- [ ] New skills added to the `AGENTS.md` skill list.
- [ ] Conventional-commit messages; one logical change per commit.
- [ ] CI is green.

By contributing you agree your work is licensed under the repo's [MIT License](LICENSE).
