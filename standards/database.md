# Standard: Database

## Purpose
Model data for correctness first, then performance. Protect integrity and enable safe evolution of schema over time.

## Principles
- The schema is a contract; changes are versioned, reversible migrations.
- Normalize for integrity; denormalize deliberately for proven read performance.
- Let the database enforce invariants it can (constraints, FKs, uniqueness).
- Indexes serve access patterns — design them from real queries, not guesses.

## Rules
- All schema changes via migrations, checked in, forward + rollback tested.
- Migrations are backward-compatible during deploy (expand/contract; no destructive change in the same release as code relying on the old shape).
- Use transactions for multi-statement invariants; pick isolation deliberately.
- Index foreign keys and high-selectivity filter/sort columns; drop unused indexes.
- Enforce NOT NULL, UNIQUE, CHECK, and FK constraints rather than app-only checks.
- Use connection pooling; bound pool size; set statement timeouts.
- Each service owns its schema; no cross-service table sharing.

## Checklist
- [ ] Change shipped as a reversible, checked-in migration.
- [ ] Expand/contract used for zero-downtime deploys.
- [ ] Constraints enforce invariants in-DB.
- [ ] Indexes match actual query patterns; no missing FK index.
- [ ] Transactions + isolation chosen for multi-row invariants.

## Examples
- Expand/contract: add nullable column → backfill → switch reads → enforce NOT NULL → drop old.
- `CREATE UNIQUE INDEX ON users (lower(email))` to enforce case-insensitive uniqueness.

## Anti-patterns
- Editing schema by hand in prod. Destructive `DROP/ALTER` coupled to a code deploy.
- Validation only in app code while the DB allows bad rows.
- Indexing everything (write amplification) or nothing (full scans).
- Sharing one database across microservices.
