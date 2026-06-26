# Standard: CI/CD

## Purpose
Make releasing small, frequent, and boring. The pipeline is the quality gate and the only path to production.

## Principles
- Automate the path from commit to production; manual steps are bugs.
- Fail fast and cheap: cheapest checks first, expensive ones later.
- Build once, promote the same artifact through environments.
- Every change is releasable and reversible.

## Rules
- CI runs on every push/PR: lint → unit → integration → build → security scan. Block merge on failure.
- Build a single immutable, versioned artifact; promote it dev→staging→prod (no rebuilds per env).
- Configuration via environment, not baked into the artifact; secrets from a manager.
- Keep environments at parity; deploy with a tested rollback (or auto-rollback on health failure).
- Progressive delivery for risk (canary/blue-green/feature flags) on user-facing changes.
- Pipeline as code, versioned with the repo. No manual prod hotfixes outside it.

## Checklist
- [ ] CI gates merges on lint/test/build/scan.
- [ ] One artifact built and promoted across envs.
- [ ] Config/secrets injected per env, not baked in.
- [ ] Rollback path tested; health checks gate the rollout.
- [ ] Risky changes behind canary/flag.

## Examples
- Tag-built image `app:1.4.2` deployed unchanged to staging then prod.
- Canary 5% → watch SLO burn → 100%, auto-rollback on error spike.

## Anti-patterns
- Rebuilding per environment (staging ≠ prod artifact).
- Manual "click to deploy" tribal knowledge; SSH hotfixes.
- Secrets baked into images. Big-bang deploys with no rollback.
- Green pipeline that doesn't actually run the tests.
