---
name: debugging
description: Systematically isolate and fix a bug — reproduce, hypothesize, bisect, verify. Use when chasing incorrect behavior, a crash, a flaky test, or an unexplained failure. Pairs with rca for incidents.
---

# Debugging

## Purpose
Find the true cause of a defect by evidence and elimination, then fix it with a regression test — no shotgun edits.

## Activation Criteria
Trigger on: a reproducible-or-not bug, crash, wrong output, or flaky test. For production incidents needing systemic root cause, escalate to `rca`.

## Inputs
- Expected vs actual behavior; error/stack/logs; steps or inputs that trigger it.
- The relevant code path and recent changes (`git log`/diff).

## Outputs
- A reliable reproduction, the identified root cause, a minimal fix, and a regression test.

## Workflow
1. Reproduce deterministically; if flaky, find the source of nondeterminism (time/order/concurrency).
2. State a falsifiable hypothesis about the cause.
3. Narrow the search: bisect (code history or input), add targeted logging/assertions, inspect state at the boundary.
4. Confirm the cause by making the bug appear/disappear on demand.
5. Apply the smallest correct fix at the root, not the symptom.
6. Add a regression test that fails before and passes after; check for sibling occurrences.

## Checklist
- [ ] Reproduced reliably (or nondeterminism sourced).
- [ ] Cause confirmed, not guessed.
- [ ] Fix addresses root, not symptom.
- [ ] Regression test added (fails before, passes after).
- [ ] Looked for the same bug elsewhere.

## Deliverables
- Fix + regression test.
- Brief: `## Symptom`, `## Root cause`, `## Fix`, `## Prevention` (feed durable items to `knowledge/lessons/`).
