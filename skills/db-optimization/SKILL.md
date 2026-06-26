---
name: db-optimization
description: Diagnose and fix database performance — slow queries, missing/wrong indexes, N+1 access, lock contention, and schema/access-pattern mismatches. Use when queries are slow, DB CPU is high, or load tests reveal data-layer bottlenecks.
---

# Database Optimization

## Purpose
Find and remove the real data-layer bottleneck using evidence (plans, metrics), not guesswork.

## Activation Criteria
Trigger on: slow endpoints traced to the DB, high DB CPU/IO, timeouts under load, or "this query is slow". Not for schema design from scratch (use system-design).

## Inputs
- The slow query/endpoint, its `EXPLAIN ANALYZE` plan, and table sizes/cardinality.
- Access patterns and current indexes; DB metrics (cache hit ratio, locks, slow log).
- `ai-os/standards/database.md`, `performance.md`.

## Outputs
- Root-cause finding + a verified fix (index, query rewrite, schema/access change) with before/after numbers.

## Workflow
1. Confirm the bottleneck with metrics/slow log — optimize the proven one.
2. Read the query plan; look for seq scans, bad join order, sorts, and row-estimate errors.
3. Check for N+1 / chatty access from the app layer; batch if present.
4. Add/adjust indexes to match the filter+sort; verify the plan changes.
5. If schema/access pattern is the cause, propose denormalization/caching deliberately.
6. Re-measure under representative load; record before/after.

## Checklist
- [ ] Bottleneck proven by data, not assumed.
- [ ] Query plan inspected; scan/sort/join issues addressed.
- [ ] N+1 eliminated; results bounded/paginated.
- [ ] Index matches access pattern; no redundant indexes added.
- [ ] Before/after numbers captured.

## Deliverables
- Report: `## Symptom`, `## Diagnosis (plan)`, `## Fix`, `## Before/After`, `## Follow-ups`.
- Migration for any index/schema change (per database standard).
