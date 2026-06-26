# Migration: <what is changing>

- **Status:** Planned | In progress | Completed | Rolled back
- **Owner:** <name>
- **Date:** YYYY-MM-DD
- **Type:** schema | data | infra | API | dependency

## Goal
What state we're moving from → to, and why. Expected duration and risk level.

## Scope & impact
What's affected (tables, services, consumers), expected downtime (target: zero), and blast radius.

## Strategy
Expand/contract or equivalent zero-downtime approach:
1. **Expand** — add the new shape, backward-compatible; deploy.
2. **Migrate/backfill** — populate new shape; dual-write if needed; verify.
3. **Switch** — move reads/writes to the new shape behind a flag.
4. **Contract** — remove the old shape once nothing depends on it.

## Steps
- [ ] <ordered, reversible step>
- [ ] …

## Validation
How correctness/completeness is verified at each stage (counts, checksums, shadow reads, canary).

## Rollback
Exact steps to revert at each stage, and the point of no return (if any).

## Cutover plan
Timing, who runs it, monitoring during, and go/no-go criteria.
