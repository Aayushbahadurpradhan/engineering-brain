---
name: architecture-review
description: Review a system or change for architectural soundness — layering, dependency direction, boundaries, coupling, and SOLID/Clean/Hexagonal adherence. Use when asked to assess design, review an architecture or large refactor, evaluate module boundaries, or before merging structural changes.
---

# Architecture Review

## Purpose
Evaluate whether a design or change keeps the system changeable: correct dependency direction, clean boundaries, and isolation of domain logic from infrastructure.

## Activation Criteria
Trigger when the task is: "review the architecture", assessing a design doc/ADR, a large structural refactor, introducing a new module/service boundary, or diagnosing tangled coupling. Do not trigger for small localized bug fixes.

## Inputs
- The code, diff, or design under review (paths or description).
- Relevant `ai-os/standards/architecture.md` rules.
- Stated constraints: scale, team, deadlines, existing tech.

## Outputs
- A findings report: strengths, violations (ranked by risk), and concrete remediations.
- Optional ADR draft for any decision the review forces.

## Workflow
1. Map the layers and modules; identify the domain core and the I/O edges.
2. Trace dependency direction — flag anything pointing outward-in (domain depending on infra/framework).
3. Check boundaries against business capabilities; look for god-modules and shared mutable state.
4. Assess each module against SRP and the open/closed boundary; note leaked persistence/framework types.
5. Evaluate coupling/cohesion; identify cycles.
6. Rank findings by blast radius and cost-to-change; propose the smallest fix per finding.
7. If a structural decision is implied, draft an ADR (`ai-os/templates/adr.md`).

## Checklist
- [ ] Domain layer free of framework/infra dependencies.
- [ ] Dependencies point inward; no cycles.
- [ ] Boundaries align with capabilities; data ownership clear.
- [ ] Ports abstract all I/O; adapters wired at composition root.
- [ ] No anemic domain / logic-in-controllers.

## Deliverables
- Markdown report: `## Strengths`, `## Violations (ranked)`, `## Remediations`, `## Open questions`.
- ADR draft when a decision is required.
