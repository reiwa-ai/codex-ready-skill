# JavaScript And TypeScript Ecosystem Guide

Read this file when the repository contains Node.js, browser, or TypeScript code.

## Detection

Common signals include:

- `package.json`, `package-lock.json`, `pnpm-lock.yaml`, `yarn.lock`, `turbo.json`, `nx.json`, or `tsconfig.json`;
- dependencies such as `react`, `next`, `vue`, `nuxt`, `svelte`, `vite`, `webpack`, `express`, `nestjs`, `vitest`, `jest`, `playwright`, or `cypress`.

## What To Record In Repository Guidance

- the package manager in use and the commands already used for install, dev, build, lint, type-check, and test;
- whether the repo is a single app, package library, or monorepo with per-package scripts;
- runtime boundaries between frontend, backend, serverless, shared packages, and generated code;
- env-file expectations, build outputs, code generation steps, and browser or Node version constraints.

## Editing And Documentation Priorities

- Reuse the existing package manager, workspace layout, and test runner.
- Respect `eslint`, `prettier`, `biome`, `tsc`, or other existing checks rather than adding new tooling by default.
- Document script entrypoints, dev servers, preview commands, and cross-package dependencies.
- If code generation is present, record the generator command and the source-of-truth files.

## Testing Guidance

- Use the existing unit and integration tools, typically `vitest`, `jest`, or framework-native runners.
- Separate fast local checks from browser-level end-to-end tests.
- When the repository lacks a small manual runner for core logic, add an idiomatic equivalent such as `require.main === module`, `import.meta.main`, or a narrow smoke-test script.
- Keep dummy data explicit and easy to update, and ask the user before turning a mock end-to-end skeleton into a fully implemented suite.

## Common JS Or TS Subtypes

Adapt repository-local type files for the actual mix:

- Node service: note server entrypoint, route layout, async boundaries, workers, and deployment mode.
- SSR app: note routing conventions, server components or loaders, asset pipeline, and data-fetch boundaries.
- SPA frontend: note state management, API client layer, build tool, and component test strategy.
- Package library: note public API surface, build targets, generated types, and compatibility promises.
- Monorepo: note package graph, shared config packages, and affected test commands.
