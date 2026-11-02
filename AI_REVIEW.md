# AI_REVIEW.md - Pull request and general code change review checklist

Use this checklist before proposing or accepting code changes.

## Scope

* confirm the change stays within the requested task
* confirm no unrelated refactors or file moves were introduced
* confirm protected projects were not modified unless explicitly requested
* distinguish identifying a rule needing revision from authority to silently violate it

## Architecture

* confirm logic is placed in the correct project
* confirm new abstractions are necessary and fit existing patterns
* confirm dependency direction remains appropriate

## Security and data handling

* confirm no secrets, tokens, passwords, certificates, private URLs, or real connection strings were added
* confirm sensitive data is not logged, exposed, or copied into examples or tests
* confirm configuration changes are safe for local, CI, and production use

## OpenClaw plugin rules

* confirm imports use published SDK subpaths, not core internals or repository-only test helpers
* confirm the entry helper fits the plugin capabilities
* confirm package metadata, manifest, configuration schemas, and runtime registrations agree
* confirm published entry points are compiled JavaScript and the packed artifact includes required files and runtime dependencies
* confirm claimed OpenClaw versions were tested and cancellation and lifecycle cleanup remain correct
* confirm accessibility remains intact for interactive UI, including keyboard support and ARIA expectations

## Testing

* confirm a focused test was added or updated when behavior changed
* confirm tests use Vitest and its built-in assertion patterns already used in the repo
* confirm tests use awaited async operations where applicable
* confirm tests do not use unnecessary delays or brittle timing
* confirm test names follow repo naming conventions

## Code quality

* confirm the diff is minimal and readable
* confirm JSDoc/TSDoc exists for new exported APIs
* confirm no warnings were suppressed to force success
* confirm no unnecessary dependencies were introduced
* confirm hard-coded colors were not added to interactive UI

## Verification

* confirm any suggested commands are targeted to the affected package, not the whole workspace, unless explicitly requested
* confirm formatting guidance is scoped to changed files when possible
* confirm the consumer is told about any critical problems that were found

## Output expectations

* keep feedback brief and actionable
* separate required fixes from optional suggestions
* call out critical problems explicitly
* do not request unnecessary cleanup outside the task scope
