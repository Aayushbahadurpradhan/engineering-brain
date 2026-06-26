# Standard: Observability

## Purpose
Be able to answer "what is the system doing and why" from the outside, in production, without a debugger.

## Principles
- Three pillars: logs (events), metrics (aggregates), traces (causal paths). Use each for its job.
- Instrument for the questions you'll ask at 3am, not for vanity dashboards.
- Every request is traceable end-to-end via a propagated correlation/trace ID.
- Alert on symptoms users feel (SLO burn), not on causes.

## Rules
- Structured logs (key-value/JSON), leveled, with correlation IDs; never log secrets/PII.
- Emit RED (Rate, Errors, Duration) for services and USE (Utilization, Saturation, Errors) for resources.
- Propagate trace context across every service and async boundary.
- Define SLIs and SLOs for user-facing paths; alert on error-budget burn.
- Every alert is actionable and links to a runbook; delete alerts no one acts on.
- Health/readiness endpoints expose real dependency status.

## Checklist
- [ ] Logs structured, leveled, correlation-tagged, secret-free.
- [ ] RED/USE metrics emitted and dashboarded.
- [ ] Distributed tracing spans the full request path.
- [ ] SLIs/SLOs defined; alerts fire on burn, link to runbooks.
- [ ] No noisy/unactionable alerts.

## Examples
- Log: `{"level":"error","trace_id":"abc","event":"charge_failed","order_id":42}`.
- Alert: "checkout p99 > 2s for 5m (SLO burn)" → runbook link.

## Anti-patterns
- `print`/unstructured logs grep-archaeology. Logging tokens or full PII payloads.
- Dashboards full of CPU graphs but no user-facing latency/error SLI.
- Alerting on every CPU spike; pager fatigue; "is it down?" with no health signal.
- Trace IDs that stop at the first service boundary.
