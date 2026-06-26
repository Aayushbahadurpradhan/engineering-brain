---
name: api-design
description: Design REST or GraphQL API contracts, endpoints, payloads, and response codes.
---

# API Design

## Purpose
Create clear, consistent, and evolvable API contracts between systems or frontend/backend boundaries.

## Activation Criteria
Trigger when asked to design new endpoints, document an API, or establish a contract for a new feature.

## Outputs
- API specifications (OpenAPI/Swagger) or documented contracts.
- Defined request/response payloads and error formats.

## Workflow
1. Identify consumer needs and resource boundaries.
2. Map operations to standard HTTP methods (GET, POST, PUT, PATCH, DELETE).
3. Define URL structures using nouns (e.g., `/users/{id}/orders`).
4. Specify standard response codes (200, 201, 400, 401, 403, 404, 500).
5. Standardize error responses (e.g., standard JSON error format).

## Checklist
- [ ] Endpoints use correct HTTP verbs.
- [ ] Payloads are JSON.
- [ ] Pagination/filtering defined for collections.
- [ ] Error responses are consistent.
