# Standard: Architecture

## Purpose
Keep systems changeable: isolate business logic from delivery and infrastructure so either can be replaced without rewriting the core.

## Principles
- Dependencies point inward: domain ← application ← adapters ← infrastructure.
- The domain knows nothing about HTTP, DB, frameworks, or serialization.
- Ports (interfaces) are owned by the inside; adapters implement them on the outside.
- Composition over inheritance; explicit dependencies over globals.
- One reason to change per module (SRP); separate policy from mechanism.

## Rules
- No framework/ORM/cloud type may appear in domain or application layers.
- Cross-boundary data uses plain DTOs/value objects, not persistence entities.
- Application orchestrates use cases; it depends on ports, never on concrete adapters.
- Wire concrete implementations only at the composition root (main/bootstrap).
- A microservice owns its data; no shared database between services.
- Make illegal states unrepresentable — encode invariants in types/value objects.

## Checklist
- [ ] Domain compiles with zero infra dependencies.
- [ ] Each use case has a single entry point and clear inputs/outputs.
- [ ] All I/O (DB, network, clock, random) is behind an interface.
- [ ] No circular dependencies between modules.
- [ ] Boundaries match business capabilities, not technical layers only.

## Examples
- Port: `interface PaymentGateway { charge(Money, CardToken): Result<Receipt> }` in application; `StripeGateway` implements it in infrastructure.
- Use case `PlaceOrder` depends on `OrderRepository` + `PaymentGateway` ports; the controller and DB adapter are injected at startup.

## Anti-patterns
- Anemic domain: logic living in services while entities are bare data bags.
- Controllers calling the ORM directly; business rules in HTTP handlers.
- "Shared kernel" that turns into a god-module every service depends on.
- Leaking ORM entities to the API surface.
- Premature microservices before the domain boundaries are understood.
