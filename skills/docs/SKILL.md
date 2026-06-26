---
name: docs
description: Produce clear, durable technical documentation — READMEs, runbooks, API docs, architecture overviews, and diagrams. Use when asked to document a system, write a runbook/guide, or make existing docs understandable. Optimize for the reader's task, not completeness.
---

# Technical Documentation

## Purpose
Write documentation that gets the reader to their goal fast and stays true as the system evolves.

## Activation Criteria
Trigger on: "document this", README/runbook/API-doc/guide requests, or onboarding material. Not for code comments inline (write those as you code).

## Inputs
- The subject (system/feature/process) and its source of truth (code, configs).
- The audience and the task they're trying to accomplish.
- Relevant standards and `ai-os/templates/` (adr, spec, migration, postmortem).

## Outputs
- Task-oriented docs: concise, accurate, example-driven, with a clear next action.

## Workflow
1. Identify the reader and the one job the doc must enable.
2. Lead with the outcome and the fastest path (quickstart/TL;DR), then detail.
3. Verify every command/claim against the real system; prefer copy-pasteable examples.
4. Use diagrams for structure/flow; keep them simple and labeled.
5. Cut anything that doesn't serve the reader's task; link rather than duplicate.
6. State how the doc stays current (owner, where the source of truth lives).

## Checklist
- [ ] Audience and purpose explicit.
- [ ] Quickstart/outcome first; details after.
- [ ] Commands/claims verified against reality.
- [ ] Examples are runnable; diagrams labeled.
- [ ] No duplication; links to source of truth; ownership noted.

## Deliverables
- The document (README/runbook/API/overview) using the right template where one exists.
- Durable conventions worth reuse → `knowledge/patterns/` or `playbooks/`.
