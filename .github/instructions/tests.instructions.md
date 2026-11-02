---
applyTo: "**/*.test.ts,**/*.spec.ts,**/tests/**/*.ts,**/test/**/*.ts"
---
# Test instructions

Use these rules for test work. Keep tests small, deterministic, and behavior-focused.

Defaults below are for TypeScript OpenClaw plugins. If a repository uses a different stack, use the repo's existing framework and conventions unless they conflict with these instructions.

## Do / Don't (Read First)

### Do
- default to Vitest for test execution and its built-in assertions; do not add another assertion library without approval
- keep tests in the paths defined in `PROJECTS.md`; colocated `*.test.ts` files are supported
- use plain unit tests for logic and focused registration or integration tests for plugin behavior
- prefer the simplest test type that verifies the behavior
- test observable registration, tool results, configuration validation, errors, cancellation, and lifecycle cleanup where applicable, not implementation internals
- register only the minimal required test doubles
- mock or fake network clients, time, and external services as needed
- use TDD for behavior changes: start with a failing test
- keep tests isolated and deterministic
- use Vitest fake timers or event-driven gates instead of fixed sleeps
- await async operations and cleanup; restore mocks, timers, and environment changes after each test
- ensure test names clearly describe the behavior being verified

### Don't
- do not create a separate test package unless repository structure or maintainability requires it
- do not use broad snapshot assertions when targeted assertions are enough
- do not test third-party library internals directly
- do not use live network calls, real external services, or unnecessary filesystem access
- do not put secrets or sensitive data in fixtures or sample inputs
- do not import OpenClaw repository-only test helpers into standalone plugins; use local test doubles for the published SDK interfaces
- do not end test names with `Test` or `Async`
- do not include `Test_` in test names
- do not end test names with `_`

## Test project structure

Use colocated tests or the existing test directory recorded in `PROJECTS.md`. Do not introduce additional layers just to organize tests.

## Regression testing

- For each behavior bug fix, write a failing test first that captures the defect scenario and expected behavior.
- Keep at least one targeted assertion tied to the historical bug symptom.
- Preserve nearby existing behavior checks to reduce regression risk.
- Avoid broad refactors; prefer minimal, behavior-preserving test additions and fixes.
- When the consuming project uses an issue tracker, record its identifier in that project's convention; otherwise retain a targeted assertion tied to the historical symptom.

## Verification

Use `PROJECTS.md` for project-specific verification paths and commands.
