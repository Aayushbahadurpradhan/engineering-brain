# Repository Pattern

## Context
Decoupling domain logic from data access code (databases, external APIs).

## Problem
When domain objects contain SQL queries or ORM specific code, the domain logic becomes hard to test, hard to change, and tightly coupled to a specific technology.

## Solution
Create an interface (the repository) in the domain layer that abstracts data access. Implement this interface in the infrastructure layer. 

## Structure
- `Domain Layer`: Defines `IUserRepository` (e.g., `Save(user)`, `FindById(id)`).
- `Infrastructure Layer`: Implements `SqlUserRepository` which uses SQL/ORM to talk to the DB.

## Benefits
- Domain is testable with in-memory mocks.
- DB technology can be swapped without touching domain logic.

## When to Use
- When following Clean Architecture or DDD.
- When business logic is complex and needs isolation.
