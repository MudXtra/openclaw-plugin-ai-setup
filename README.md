# openclaw-plugin-ai-setup

An opinionated starting template for **AI-assisted OpenClaw plugin development**, using **TypeScript, Node.js, and ESM**.

Start a repository with a consistent set of instructions for how AI should work in your project: where code belongs, which conventions to follow, how to test changes, and what to check before calling the work complete.

This is not a complete plugin or a plugin scaffolder. It provides the repository guidance and configuration that surround your plugin. You supply the implementation, its requirements, and its boundaries. Adapted from [MudXtra/dotnet-ai-setup](https://github.com/MudXtra/dotnet-ai-setup).

## Why use it?

AI works better when it does not have to rediscover your project or guess your expectations on every task.

This template gives you a starting point for:

- Keeping changes and additions minimal, without expanding architecture any more than is absolutely necessary.
- Giving AI the project paths and commands it needs to work with less supervision.
- Following test-driven development for behavior changes.
- Reviewing code for correctness, accessibility, security, and maintainability.
- Keeping sensitive data and external databases outside ordinary AI development work.

The defaults reflect the technologies and practices used by the author. They are intentionally opinionated—not an attempt to prescribe the right setup for every OpenClaw plugin.

## Getting started

1. **Create your repository** and copy the starter files from this repository into it.
2. **Create or add your plugin and tests.** Use the smallest shape matching its capabilities. For a tools-only plugin, OpenClaw provides `openclaw plugins init <plugin-id>`; see the [tool-plugin guide](https://docs.openclaw.ai/plugins/tool-plugins). This starter adds no application layers or runtime dependencies.
3. **Configure `PROJECTS.md`** with your actual project paths, responsibilities, protected areas, and verification commands.
4. **Review the defaults** in `AGENTS.md`, the test instructions, `.editorconfig`, and `tsconfig.json`. Adapt them to your project before relying on them. This starter does not prescribe a file header; if your project requires one, configure `file_header_template` in the applicable EditorConfig after checking ownership and licensing.
5. **Check configuration placement.** The root `.editorconfig` covers source, tests, and configuration. Merge `tsconfig.json` settings into the plugin's existing or generated configuration; preserve its entry paths, output layout, and package metadata. Nested packages must extend or merge TypeScript settings deliberately; they are not inherited automatically.
6. **Keep strict type checking and failing lint checks enabled; document intentional exceptions in `PROJECTS.md`.** Use a supported Node.js version and pin the development OpenClaw host version. Plugin APIs are experimental; test each version claimed compatible. Record the actual versions rather than copying version numbers from examples. See [OpenClaw's authoring requirements](https://docs.openclaw.ai/plugins/building-plugins).
7. **Run your documented build and test commands**, then commit the configured starting point.

You can ask AI to inspect your package and draft `PROJECTS.md`. Review the result—especially project responsibilities, protected paths, and commands—before using it as the project map.

## What is included?

| File | Purpose |
| --- | --- |
| `AGENTS.md` | Working rules, development conventions, boundaries, and completion expectations. |
| `PROJECTS.md` | Your repository's project map and targeted verification commands. |
| `AI_REVIEW.md` | A checklist for reviewing changes before submission. |
| `CLAUDE.md` | Loads the shared repository instructions, project map, and review checklist for Claude Code. |
| `.github/copilot-instructions.md` | Directs GitHub Copilot to the shared repository guidance. |
| `.github/instructions/tests.instructions.md` | Testing conventions and regression-test guidance. |
| `.github/pull_request_template.md` | A consistent structure for describing and checking changes. |
| `.editorconfig` | Formatting preferences for source, tests, and configuration. |
| `tsconfig.json` | TypeScript ESM and strict-checking defaults to merge into the plugin configuration. |
| `.gitignore` and `.gitattributes` | Source-control defaults for Node.js plugin development. |

### Testing and tooling

The testing guidance favors **Vitest and its built-in assertions**. Adapt it to the frameworks your plugin actually uses. Do not import OpenClaw's repository-local test helpers into standalone plugins; they are not published package exports. See [plugin testing](https://docs.openclaw.ai/plugins/sdk-testing).

Standalone plugins may use npm or pnpm. Preserve one package manager and its committed lockfile. Work inside the OpenClaw source repository uses pnpm and that repository's commands. ESLint and Prettier are suggested equivalents for linting and formatting; preserve existing tooling and add only what the plugin needs.

Native plugins need `openclaw.plugin.json` with a configuration schema, even with no configuration. Published runtime entries must point to built JavaScript. Keep metadata aligned with runtime registrations and test the packed artifact in an isolated local profile. Tools-only plugins using `defineToolPlugin` generate their metadata; other capability combinations use the appropriate entry helper. See [plugin entry points](https://docs.openclaw.ai/plugins/sdk-entrypoints) and [manifest requirements](https://docs.openclaw.ai/plugins/manifest).

## Make `PROJECTS.md` yours

`PROJECTS.md` connects the general instructions to your actual plugin. It is not a list of tasks—it tells AI where and how to work.

Replace every placeholder with useful project information:

- The package, manifest, source, runtime entry, and test paths.
- The plugin ID, capabilities, toolchain versions, and tested OpenClaw compatibility.
- What belongs in each project.
- Areas that require explicit permission to change.
- Which test projects cover the affected code.
- The commands needed to build, test, and verify changes.

Keep it concise and update it when the project structure or commands change. Do not put credentials, real connection strings, or sensitive plugin data in it.

A well-maintained project map lets you describe the outcome you want without explaining the repository from scratch each time.

## Working with AI

Once the template is configured, give your AI tool a concrete task and the expected outcome. Ask it to follow `AGENTS.md`, use `PROJECTS.md` to find the right projects and commands, and check its changes against `AI_REVIEW.md`.

For an approved task, end-to-end execution is the default: the agent continues implementation and proportional verification without routine stage pauses. It pauses only at a material boundary or explicit request; scope changes and decisions requiring approval still need your direction.

Repository instructions are guidance, not a security sandbox. Tool support for discovering instruction files varies, so confirm your AI tool is loading the relevant guidance. Review the resulting changes and verification evidence before accepting them.

The external-database boundary is defined in [AGENTS.md](AGENTS.md#external-database-boundary). Development and tests should use permitted local, synthetic data—not external databases or copies of real customer or production data.

## Using the files in an existing repository

Starting a new project is the primary use, but you can also adapt these files to an existing repository. Review and merge its existing instructions and configuration rather than assuming the template should replace them.

Copy the files you need manually, preserve your repository-specific settings, and configure `PROJECTS.md` with the existing project structure and commands.

## License

This template is provided under the [MIT License](LICENSE).
