# Repository Guidelines

## Project Structure & Module Organization
OpenCode is a Bun + TypeScript monorepo. Key locations:
- `packages/opencode`: core server/runtime, CLI, tools, and tests.
- `packages/console`: TUI front end.
- `packages/web`: marketing site and assets.
- `packages/desktop`: Tauri desktop wrapper.
- `packages/sdk`: SDKs (JS lives under `packages/sdk/js`).
- Shared utilities live in `packages/ui`, `packages/util`, and `packages/plugin`.

## Build, Test, and Development Commands
From repo root:
- `bun install`: install dependencies.
- `bun dev`: run OpenCode in `packages/opencode` (default dev entry).
- `bun run --cwd packages/opencode --conditions=browser src/index.ts`: run core directly.
- `bun run typecheck`: typecheck via Turborepo.
- `./packages/sdk/js/script/build.ts`: regenerate the JavaScript SDK.
Avoid `bun test` at the root; run tests from the package that owns them.

## Coding Style & Naming Conventions
- Runtime: Bun, TypeScript ESM modules.
- Formatting: Prettier (see root `package.json` config).
- Style guide: keep logic in a single function when possible; avoid `else`, `try/catch` when a promise chain works, `any`, and `let`; prefer concise names and Bun APIs like `Bun.file()`.
- Naming: `camelCase` for functions/vars, `PascalCase` for types/classes, and `kebab-case` for package directories.

## Testing Guidelines
- Tests live in package-local `test/` directories (for example `packages/opencode/test`).
- Run all tests: `bun test` inside the package.
- Run a single file: `bun test test/tool/tool.test.ts` (from `packages/opencode`).

## Commit & Pull Request Guidelines
- Commit messages in this repo follow a conventional style such as `fix(app): ...` or `feat: ...`; include scopes and issue numbers when relevant.
- PRs should be small, linked to issues, and clearly explain the problem and fix; avoid verbose AI-generated descriptions.
- UI/core feature work requires a design review with the core team before implementation.

## Architecture & API Notes
- The TUI communicates with the server via `@opencode-ai/sdk`.
- If you change server endpoints in `packages/opencode/src/server/server.ts`, regenerate SDK artifacts (`./script/generate.ts`) and update the JS SDK (`./packages/sdk/js/script/build.ts`) as needed.
