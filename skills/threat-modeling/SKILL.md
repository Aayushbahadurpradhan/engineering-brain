---
name: threat-modeling
description: Produce a structured threat model for a system, feature, or change — enumerate assets, trust boundaries, and threats (STRIDE) with mitigations. Use when designing a new feature handling sensitive data, reviewing security posture, before a launch, or when asked "what could go wrong / how could this be attacked".
---

# Threat Modeling

## Purpose
Systematically find how a system can be attacked and decide what to do about each threat, before attackers do.

## Activation Criteria
Trigger when: designing/reviewing a feature that handles auth, money, PII, or external input; pre-launch security review; an explicit "threat model this" / "attack surface" request. Not for routine code style review.

## Inputs
- System/feature description or diagram; data flows and external entities.
- Trust boundaries, auth model, data classification.
- `ai-os/standards/security.md`.

## Outputs
- Threat model document: data-flow view, enumerated threats, mitigations, residual risk.

## Workflow
1. Define scope and assets (what's worth protecting: data, funds, availability, reputation).
2. Draw the data-flow: external entities, processes, data stores, and trust boundaries.
3. For each element/flow crossing a boundary, enumerate threats via STRIDE — Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege.
4. Rate each threat by likelihood × impact.
5. Assign a mitigation per threat (control, accept, transfer, or eliminate) mapped to security standard rules.
6. List residual risks and required follow-ups; flag anything needing a decision/ADR.

## Checklist
- [ ] All trust boundaries identified.
- [ ] Every boundary-crossing flow run through STRIDE.
- [ ] Auth, input validation, secrets, and logging considered.
- [ ] Each threat has an owner and a disposition.
- [ ] Residual risk stated explicitly.

## Deliverables
- Markdown doc: `## Scope & assets`, `## Data flow & trust boundaries`, `## Threats (STRIDE, rated)`, `## Mitigations`, `## Residual risk`.
