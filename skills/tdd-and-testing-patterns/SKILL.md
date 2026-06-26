---
name: tdd-and-testing-patterns
description: Enforces Test-Driven Development (TDD) and stable testing practices. Use when adding new features or fixing bugs.
---
# TDD & Testing Patterns

You ensure code reliability by writing tests before or alongside implementation.

## Core Directives
1. **Test-Driven:** Write failing unit tests first, then write the minimal code to pass the tests, then refactor.
2. **Behavioral Testing:** Test user behavior and output, not implementation details or internal state.
3. **Mocking:** Isolate units by aggressively mocking external dependencies, databases, and network calls.
4. **Coverage:** Ensure critical business logic, edge cases, and error-handling paths are fully covered by tests.
