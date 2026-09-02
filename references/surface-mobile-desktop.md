# Mobile And Desktop Surface Guide

Read this file when the repository targets mobile devices, desktop shells, or native packaging.

## What To Record In Repository Guidance

- target platforms, supported OS versions, simulators, emulators, or device requirements;
- packaging, signing, entitlements, and release prerequisites;
- native module boundaries, bridge layers, and host-shell lifecycle hooks;
- test commands for unit, integration, and UI automation;
- any local services or seeded data needed for smoke tests.

## Editing Priorities

- Preserve the established platform stack, such as Electron, Tauri, React Native, Flutter, Android, or iOS native tooling.
- Document which parts of the codebase are shared and which are platform-specific.
- Note fragile areas such as build signing, permissions, file-system access, native dependencies, or OS-specific behaviors.
- If UI code and service code live together, create separate repository-local type files for each concern.

## Testing Guidance

- Run fast unit checks during each edit cycle.
- Keep device or shell-level end-to-end automation separate and run it after a coherent work batch.
- If no UI automation exists, create a mock skeleton first.
- Ask the user before filling in device-specific end-to-end flows or before inventing dummy data that must look realistic.

## Typical Subtypes

Repository-local type files often need a separate note for:

- desktop shell;
- cross-platform mobile app;
- native iOS or Android project;
- plugin or extension loaded into a host desktop application.
