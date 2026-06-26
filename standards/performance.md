# Standard: Performance

## Purpose
Meet explicit latency/throughput/cost targets without premature optimization. Make speed a measured property, not a guess.

## Principles
- Measure before optimizing; optimize the proven bottleneck only.
- Set budgets (p99 latency, throughput, memory, $/request) before building.
- Algorithmic complexity beats micro-tuning; fix the O(n²) before the constant.
- Do less work: cache, batch, paginate, stream. The fastest call is the one not made.
- Performance is a feature with a cost — trade it deliberately against simplicity.

## Rules
- Define and record a budget per critical path; fail CI/review if regressed.
- Profile with realistic data and load; never optimize from intuition.
- Eliminate N+1 access patterns; batch or join. Page all unbounded result sets.
- Cache with explicit invalidation and TTL; never cache without an eviction story.
- Bound concurrency; apply backpressure and timeouts to every external call.
- Stream large payloads; avoid loading whole datasets into memory.
- Load-test before launch for anything user-facing at scale.

## Checklist
- [ ] Latency/throughput budget stated for the hot path.
- [ ] Profiled under representative load; bottleneck identified by data.
- [ ] No N+1; queries indexed; results paginated.
- [ ] Caches have TTL + invalidation; hit ratio observable.
- [ ] Timeouts + concurrency limits on all I/O.

## Examples
- Replace per-item DB lookups in a loop with a single batched `WHERE id IN (...)`.
- Cache an expensive computed view keyed by inputs, invalidated on write.

## Anti-patterns
- "Optimizing" code that runs once at startup. Caching with no invalidation.
- Micro-benchmarks driving design while the real cost is a chatty network loop.
- Unbounded queries / loading entire tables into memory.
- Adding threads to a lock-bound system and calling it scaling.
