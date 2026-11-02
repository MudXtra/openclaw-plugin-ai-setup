# Project boundaries

## First-use project map workflow
PROJECTS.md is a maintained map of verified facts, not a task list or source of new permission. Inspect the existing package first and record its OpenClaw host and compatibility versions, Node.js version, package manager, roles, test mapping, protected areas, and verified commands. For an empty repository, use the smallest OpenClaw plugin shape matching the requested capabilities and obtain approval for material structure decisions. UI, data, and separate test roles may be `N/A`; never create a package merely to satisfy a placeholder. Never record secrets, real connection strings, or sensitive data.

This starter has no plugin implementation, package manifest, installed tools, or runnable build/test target. The entries and commands below are templates to configure and verify in the consuming plugin repository.

## Files and paths
- {{PACKAGE_PATH}} is the plugin package root containing `package.json` and `openclaw.plugin.json`
- {{PLUGIN_ID_AND_TYPE}} identifies the plugin and its capabilities (tools, hooks, channel, provider, or other)
- {{ENTRY_PATH}} is the runtime entry; published packages point to compiled JavaScript
- {{SOURCE_PATH}} owns plugin implementation
- {{TEST_PATHS}} owns Vitest tests; colocated tests are allowed
- {{UI_PATH}} owns interactive UI, if any; N/A is allowed
- {{DATA_PATH}} owns persistence, if any; N/A is allowed
- {{PROTECTED_PATHS}} allows N/A; do not edit unless explicitly instructed
- {{TOOLCHAIN}} records the Node.js version, package-manager version, exact development OpenClaw version, and tested compatibility range

## Verification prerequisites and evidence
Run commands from the package root unless a documented command names another working directory. Before running a command, verify the package's scripts, tool versions, test runner, and paths. Run a focused test before the full package tests when it applies. Use broader workspace validation only when the change, dependency, shared setting, or package wiring justifies it.

In the final report, name every command actually run and its outcome. Name relevant checks not run, explain why they were not run or not applicable, and never imply a build or test ran when this project map has no runnable target.

## Targeted commands

These examples assume npm, Vitest, TypeScript, ESLint, and Prettier. Define and verify the corresponding scripts in the consuming package; preserve existing tooling. Use one package manager and commit its lockfile. Standalone plugins may use npm or pnpm; OpenClaw source-checkout development requires pnpm and its repository commands.

| Check | Example command |
| --- | --- |
| Focused test | `npm test -- --run src/example.test.ts -t "behavior name"` |
| Package tests | `npm test -- --run` |
| Type checking | `npm run typecheck` |
| Lint | `npm run lint -- --max-warnings 0` |
| Build | `npm run build` |
| Format changed files | `npm exec -- prettier --write <changed-files>` |
| Inspect package contents | `npm pack --dry-run` |
| Create package for isolated installation test | `npm pack` |

For a tools-only plugin using `defineToolPlugin`, generate metadata after building with `openclaw plugins build --entry ./dist/index.js`. Then check it with `openclaw plugins build --entry ./dist/index.js --check` and `openclaw plugins validate --entry ./dist/index.js`. Replace the entry path with the package's actual built entry. These commands are specific to that helper; use the documented validation for other plugin shapes.

Install the packed artifact only in an isolated local OpenClaw test profile and inspect its runtime registration. Record the verified install and inspection commands here. Do not use a personal Gateway or claim an installation test passed from a package-content listing alone.
