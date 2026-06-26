---
name: rca
description: Root-cause analysis for incidents — reconstruct the timeline, find systemic causes (5 whys / fault tree), and produce prevention actions. Use after an outage/regression or when asked "why did this happen and how do we stop it recurring". Blameless.
---

# Root Cause Analysis

## Purpose
Move past the trigger to the systemic causes of an incident and produce concrete prevention, blamelessly.

## Activation Criteria
Trigger on: post-incident review, recurring failures, "why did this break", or a postmortem write-up. For isolated code defects use `debugging`.

## Inputs
- Incident facts: timeline, alerts, logs, metrics, what changed.
- Impact and detection details; the immediate fix applied.
- `ai-os/templates/postmortem.md`, `ai-os/standards/observability.md`.

## Outputs
- A blameless RCA feeding a postmortem with owned, dated action items.

## Workflow
1. Reconstruct the timeline (UTC): change → trigger → detection → mitigation → resolution.
2. Identify the trigger, then ask "why" iteratively (5 whys) to reach systemic causes.
3. Separate root causes from contributing factors; consider a fault tree if multiple paths.
4. Assess detection: could monitoring have caught it sooner?
5. Derive prevention/detection/mitigation actions; assign owners and due dates.
6. Capture durable lessons in `knowledge/lessons/`; fill the postmortem.

## Checklist
- [ ] Timeline reconstructed from evidence.
- [ ] Systemic cause reached (not just the trigger).
- [ ] Contributing factors listed.
- [ ] Detection gap evaluated.
- [ ] Actions owned, dated, and typed (prevent/detect/mitigate).

## Deliverables
- Completed postmortem (`templates/postmortem.md`).
- Lessons recorded under `knowledge/lessons/`; action items tracked.
