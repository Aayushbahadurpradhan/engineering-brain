---
name: refactoring
description: Improve internal structure without changing external behavior — reduce coupling, clarify names, extract units, kill duplication and code smells, guided by tests. Use for cleanup, "make this maintainable", taming a god-class, or prepping code before a feature.
---

# Refactoring

## Purpose
Make code easier to change while provably preserving behavior.

## Activation Criteria
Trigger on: "clean up / restructure / refactor", code smells (duplication, long methods, god-class, tangled deps), or preparing a messy area before adding a feature. Not for behavior changes or bug fixes.

## Inputs
- The target code and its current tests.
- The smell(s) to address and any structural goal.
- `ai-os/standards/architecture.md`, `testing.md`.

## Outputs
- Behavior-preserving change with green tests, smaller/clearer units, reduced coupling.

## Workflow
1. Ensure a passing test net around the target; add characterization tests if missing.
2. Identify the dominant smell and the smallest improving move.
3. Refactor in small steps — extract, rename, introduce interface, remove duplication — running tests after each.
4. Push I/O behind ports; align with dependency-inward rule if relevant.
5. Stop when readability/coupling is acceptably better — avoid speculative generality (YAGNI).
6. Confirm no behavior change: same tests, same outputs.

## Checklist
- [ ] Tests green before and after every step.
- [ ] External behavior unchanged.
- [ ] Duplication removed; units have one responsibility.
- [ ] Names reveal intent; dependencies point inward.
- [ ] No new abstraction without a present need.

## Deliverables
- The refactored code + any added characterization tests.
- Short note: smell addressed, moves made, what's intentionally left.
