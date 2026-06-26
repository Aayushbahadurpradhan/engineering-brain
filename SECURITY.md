# Security Policy

## No secrets in this repository

This repo is a public operating brain. It contains **no** credentials and never should.

- API keys, tokens, and passwords belong in your environment or a **gitignored** `secrets/` directory — never in a tracked file.
- `.gitignore` already excludes `.env`, `.env.*`, and `secrets/` (except a tracked `*.example` template). Keep it that way.
- If you ever paste a key somewhere it could be logged or shared, treat it as **compromised** and rotate it immediately.

## Reporting a vulnerability or an exposed secret

If you find a leaked credential in the history, a security issue in a script/template, or any unsafe guidance:

1. **Do not open a public issue** for an active credential leak.
2. Email the maintainer or use GitHub's **private vulnerability reporting** (Security tab → "Report a vulnerability").
3. Include what you found and where (file/commit). We'll confirm, rotate/scrub if needed, and credit you if you'd like.

## Scope

This project ships **instructions and templates that AI tools execute**. Treat changes to `AGENTS.md`, `skills/`, and `agents/` as you would executable code in a review — a malicious instruction is a supply-chain risk for anyone who loads the brain. That's why all changes land via reviewed pull request, never direct push.
