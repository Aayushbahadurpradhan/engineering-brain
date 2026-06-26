# Standard: API Design

## Purpose
Design interfaces that are predictable, evolvable, and hard to misuse — contracts that outlive their implementations.

## Principles
- Contract-first: define and review the interface before coding it.
- Consistency over cleverness: same patterns for naming, errors, pagination everywhere.
- Backward compatibility is a promise; breaking it requires a new version.
- Be strict in what you emit, liberal in what you accept (within validation).

## Rules
- Publish a machine-readable contract (OpenAPI/proto/GraphQL schema); it is the source of truth.
- Version explicitly; never break an existing version. Additive changes only within a version.
- Mutating operations are idempotent where possible (idempotency keys for create/charge).
- Uniform error shape: stable code, human message, optional details — no stack traces.
- Paginate all list endpoints (cursor preferred); never return unbounded collections.
- Validate every input at the boundary; reject unknown/oversized payloads.
- Use correct status semantics (2xx/4xx/5xx); 4xx = client fault, 5xx = server fault.

## Checklist
- [ ] Contract published and reviewed before implementation.
- [ ] Versioning + compatibility policy explicit.
- [ ] Errors follow the uniform schema with stable codes.
- [ ] All lists paginated; inputs validated and bounded.
- [ ] Idempotency on unsafe operations.

## Examples
- Error: `{"code":"INSUFFICIENT_FUNDS","message":"Balance too low","details":{...}}`.
- `POST /charges` with `Idempotency-Key` header → safe to retry.

## Anti-patterns
- Returning 200 with an error in the body. Versioning by silently changing behavior.
- Leaking DB columns/ORM entities as the API shape.
- Unbounded list endpoints; inconsistent field naming across endpoints.
- Overloading one endpoint with a `type` flag that changes everything.
