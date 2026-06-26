---
name: system-design
description: Design a system end-to-end from requirements to components, data, and trade-offs — APIs, storage, scaling, failure modes. Use for greenfield design, "design X at scale", evaluating a new service, or capacity/architecture planning. Not for small in-module changes.
---

# System Design

## Purpose
Turn fuzzy requirements into a concrete, defensible architecture with explicit trade-offs and failure handling.

## Activation Criteria
Trigger on: "design a system/service for…", scaling a component, choosing between architectures, or capacity planning. Skip for localized code changes (use refactoring/debugging instead).

## Inputs
- Functional requirements and explicit non-functionals (scale, latency, availability, consistency, cost).
- Constraints: team, budget, existing stack, deadlines.
- `ai-os/standards/architecture.md`, `database.md`, `api.md`, `performance.md`.

## Outputs
- A design doc with component diagram, data model, API surface, and trade-off analysis.

## Workflow
1. Clarify requirements; quantify scale (QPS, data size, growth) and SLOs. State assumptions.
2. Sketch the high-level components and their boundaries (Hexagonal/DDD).
3. Define the data model and storage choice (consistency vs availability, read/write patterns).
4. Define the API/contract between components.
5. Address cross-cutting concerns: caching, scaling axis, failure modes, idempotency, observability.
6. Enumerate 2–3 viable approaches; compare on the stated non-functionals; recommend one.
7. Capture the decision as an ADR (`ai-os/templates/adr.md`).

## Checklist
- [ ] Scale and SLOs quantified, assumptions stated.
- [ ] Component boundaries map to capabilities.
- [ ] Data store justified by access pattern + consistency need.
- [ ] Failure modes and bottlenecks identified.
- [ ] Alternatives compared; choice recorded as ADR.

## Deliverables
- Design doc: `## Requirements`, `## Architecture`, `## Data`, `## APIs`, `## Trade-offs`, `## Risks`.
- ADR for the load-bearing decision.
