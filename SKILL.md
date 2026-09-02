---
name: codex-ready
description: Prepare an existing software repository for AI-assisted editing by generating agent guidance, documentation, project-type instructions, and test entrypoints before broader code changes begin.
metadata:
  short-description: Prepare a repo for safe AI editing
---

# Codex Ready

Use this skill when the user wants an existing repository prepared for repeated work by coding agents. The outcome is a repository that is easier to inspect, safer to edit, and clearer to test before larger implementation changes start.

## Expected Deliverables

Create or update the repository artifacts that make agent work repeatable:

- `README.md` for the human-oriented overview, architecture, setup, and workflows.
- `KNOWLEDGE.md` for agent-oriented gotchas, invariants, and local rules that are easy to miss.
- `KNOWN_BUGS.md` for bugs or suspicious behavior discovered during inspection or testing. Record them before fixing unless the user separately asks for fixes.
- `AGENT.md` for repository-specific editing instructions.
- A repository-local project-type folder such as `.codex-ready/project-types/` with one markdown file per detected project type, referenced from `AGENT.md`.
- Runnable unit-test entrypoints for important functions and an end-to-end test plan or suite appropriate to the stack.

## First Pass

Before editing, inspect the repository structure, git state, languages, frameworks, package managers, build tools, test tools, entrypoints, deployment files, and existing documentation.

- If the repository is not under git, initialize git before wider edits so future diffs are traceable.
- If the repository already has agent instructions or documentation, extend and reconcile them instead of replacing them wholesale.
- Read [references/baseline-workflow.md](references/baseline-workflow.md) and [references/project-taxonomy.md](references/project-taxonomy.md).
- After classification, read only the relevant ecosystem and surface guides from `references/`.

## Non-Negotiable Behaviors

- Work step by step and prefer the smallest change that satisfies the user.
- Respect existing code and structure. Do not delete working code except for user-approved bug fixes or unavoidable refactors.
- Ask the user when code intent is unclear.
- Ask the user before editing existing source code when documentation, scaffolding, or tests can be prepared first.
- When bugs are found during inspection or testing, write them to `KNOWN_BUGS.md` before attempting fixes.
- Keep `KNOWLEDGE.md` updated with discoveries made during the work, and consult it before repeated edits so the same issue is not rediscovered.

## How To Build The Repository's AGENT.md

The generated `AGENT.md` must instruct future agents to:

- scan the repository first and classify it across multiple project types;
- load the relevant repository-local project-type markdown files before editing;
- separate human documentation in `README.md` from agent documentation in `KNOWLEDGE.md`;
- log inspection and test findings in `KNOWN_BUGS.md`;
- run unit tests for important functions during each edit cycle;
- run end-to-end tests separately after a coherent batch of work;
- preserve user intent, minimize edits, request clarification when intent is unclear, and request permission before editing existing source code.

Use the baseline checklist in [references/baseline-workflow.md](references/baseline-workflow.md), then translate the relevant stack guidance from the other reference files into the repository's own `.codex-ready/project-types/` files.

## Reference Routing

Always read:

- [references/baseline-workflow.md](references/baseline-workflow.md)
- [references/project-taxonomy.md](references/project-taxonomy.md)

Read the matching ecosystem guides:

- [references/ecosystem-python.md](references/ecosystem-python.md)
- [references/ecosystem-js-ts.md](references/ecosystem-js-ts.md)
- [references/ecosystem-go-rust-java-dotnet.md](references/ecosystem-go-rust-java-dotnet.md)
- [references/ecosystem-c-cpp-ruby-php.md](references/ecosystem-c-cpp-ruby-php.md)

Read the matching surface guides:

- [references/surface-web-ui.md](references/surface-web-ui.md)
- [references/surface-mobile-desktop.md](references/surface-mobile-desktop.md)
- [references/surface-data-ml-infra.md](references/surface-data-ml-infra.md)

If a repository spans multiple categories, combine the relevant guides and produce one repository-local markdown file per detected type instead of forcing everything into a single generic instruction file.

## Self-Review Before Finishing

Check the resulting skill output against these questions:

1. Is the generated repository guidance complete without becoming bloated?
2. Does the project taxonomy cover the repository's actual mix of languages, frameworks, and operating surfaces?
3. Are the type-specific instructions tailored to the detected stack rather than copied blindly?
4. Does the generated `AGENT.md` give future agents a workflow that will still work on the repository after handoff?
5. Do the generated instructions clearly require the documentation, testing, and bug-tracking behaviors listed above?
6. Does the generated `AGENT.md` explicitly tell future agents to load the repository-local project-type markdown files?
