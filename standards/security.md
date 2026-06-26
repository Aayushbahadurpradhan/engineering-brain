# Standard: Security

## Purpose
Make the secure path the default path. Reduce attack surface and blast radius before adding features.

## Principles
- Defense in depth; least privilege; fail closed.
- Never trust input — validate at the boundary, encode at the sink.
- Secrets are configuration, never code. Identity over network location.
- Auditable by design: security-relevant events are logged (without secrets).

## Rules
- No credentials, tokens, or keys in source, logs, or error messages. Load from a secrets manager/env.
- Validate and normalize all external input; allowlist over denylist.
- Parameterized queries only; no string-built SQL/shell. Escape per output context.
- AuthN and AuthZ are explicit and server-side; check authorization on every request, per resource.
- Hash passwords with a memory-hard KDF (argon2/bcrypt). Encrypt sensitive data at rest and in transit (TLS).
- Default-deny on new endpoints; rate-limit and time out external calls.
- Pin/scan dependencies; patch known CVEs promptly.

## Checklist
- [ ] No secret is committed or logged (scanned).
- [ ] Every endpoint enforces authn + per-resource authz.
- [ ] All inputs validated; outputs encoded for their context.
- [ ] Queries parameterized; no dynamic shell/SQL from user data.
- [ ] Errors don't leak stack traces, secrets, or internal topology.
- [ ] Dependencies scanned; high/critical CVEs resolved.

## Examples
- `db.query("SELECT * FROM users WHERE id = ?", [id])` — never string concatenation.
- Authorization: `assert actor.can(READ, resource)` inside the use case, not just route middleware.

## Anti-patterns
- "We'll add auth later." Client-side-only validation.
- Logging full request bodies including tokens/PII.
- Rolling custom crypto. Long-lived static credentials shared across services.
- Trusting JWT claims without verifying signature and audience.
