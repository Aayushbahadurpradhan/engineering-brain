---
name: cloud
description: Design and review cloud architecture and infrastructure-as-code — compute/network/storage topology, reliability, security, and cost. Use for provisioning, cloud migration, IaC review, or well-architected assessments. Cloud-agnostic in principle; specialize to the target provider.
---

# Cloud Architecture

## Purpose
Design cloud infrastructure that is reliable, secure, and cost-aware, expressed as reviewable infrastructure-as-code.

## Activation Criteria
Trigger on: standing up cloud infra, cloud migration, IaC review, cost/reliability assessment. For pure app architecture use system-design.

## Inputs
- Workload profile, SLOs, traffic, data residency/compliance, budget.
- Target provider(s) and existing infra/IaC.
- `ai-os/standards/security.md`, `observability.md`, `performance.md`, `ci-cd.md`.

## Outputs
- An infra design (topology + IaC) with reliability, security, and cost trade-offs stated.

## Workflow
1. Capture requirements: availability target, RTO/RPO, scale, compliance, cost ceiling.
2. Design topology: network/segmentation, compute model (serverless/containers/VMs), storage, data flow.
3. Apply least privilege (identity, secrets, network) per the security standard.
4. Build in reliability: multi-AZ/region as warranted, autoscaling, health checks, backups/DR.
5. Estimate cost; right-size; flag the dominant cost drivers and cheaper equivalents.
6. Express as IaC; integrate with CI/CD; add observability.
7. Record the topology decision as an ADR.

## Checklist
- [ ] Availability/RTO/RPO and cost ceiling stated.
- [ ] Least-privilege identity, secrets, network segmentation.
- [ ] Reliability: scaling, health checks, backups/DR.
- [ ] Cost estimated and right-sized.
- [ ] Infra as code, observable, in CI/CD.

## Deliverables
- Infra design doc + IaC; cost estimate; ADR for the topology choice.
