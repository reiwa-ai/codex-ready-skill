# Web UI And Frontend Surface Guide

Read this file when the repository contains a browser UI, component library, SSR app, static site, or design-system package.

## What To Record In Repository Guidance

- route structure, page ownership, shared layouts, and how data reaches the UI;
- styling system, design tokens, asset pipeline, localization, and accessibility requirements;
- state-management approach, API client boundaries, and feature-flag behavior;
- visual test, component test, and browser test commands;
- any mock servers, seeded accounts, screenshots, or fixtures needed to reproduce flows.

## Editing Priorities

- Preserve the existing framework and styling system.
- Document how to start the UI locally, how it depends on backend services, and where reusable components live.
- Call out fragile areas such as hydration boundaries, server/client splits, generated routes, or build-time content pipelines.
- If the repo also contains backend code, create separate repository-local type files for frontend and backend responsibilities.

## Testing Guidance

- Run component or unit tests during each edit cycle when they exist.
- Keep browser-level end-to-end tests separate and run them after a coherent work batch.
- If the repository lacks end-to-end tests, create a mock suite first and ask the user before implementing the full flows.
- When dummy users, seeded records, or fake API responses are needed, ask the user to validate that data before treating it as canonical.

## Typical Subtypes

Repository-local type files often need a separate note for:

- SPA frontend;
- SSR or hybrid frontend;
- shared component library or design system;
- docs site or static content app.
