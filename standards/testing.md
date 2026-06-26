# Standard: Testing

## Purpose
Tests exist to let you change code with confidence. Test behavior and contracts, not implementation detail.

## Principles
- Test pyramid: many fast unit tests, fewer integration, few end-to-end.
- A test asserts observable behavior through a public interface.
- Deterministic and isolated: no shared mutable state, no real clock/network unless that's the subject.
- Tests are first-class code: readable, DRY via fixtures, refactored like production.

## Rules
- Domain/application logic covered by fast unit tests with no I/O.
- Mock only at architectural boundaries (ports); never mock what you don't own without a wrapper.
- Each test has one reason to fail; name = behavior under condition → expectation.
- Integration tests exercise real adapters against real-ish dependencies (containers/in-memory), not mocks-of-mocks.
- No assertions on private state; no sleeps — use deterministic clocks/awaits.
- A bug fix ships with a regression test that fails before the fix.

## Checklist
- [ ] New behavior has a unit test; new bug fix has a regression test.
- [ ] Tests pass in isolation and in any order.
- [ ] No real network/disk/clock in unit tests.
- [ ] Failure messages point to the cause.
- [ ] Edge cases and error paths covered, not just the happy path.

## Examples
- Arrange–Act–Assert: build a use case with fake ports, invoke it, assert the returned result and emitted events.
- Contract test: the `PaymentGateway` fake and the real adapter run the same suite.

## Anti-patterns
- Asserting on internal calls/mocks instead of outcomes (over-mocking).
- Snapshot tests that ossify implementation detail.
- One giant test covering many behaviors; flaky time/order-dependent tests.
- Chasing coverage % by testing getters; tests that never fail.
