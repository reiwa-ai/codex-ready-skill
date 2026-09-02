# Baseline Workflow

Read this file for every repository prepared with `codex-ready`.

## Outcome

The repository should become easier for future agents to edit safely, not merely easier to describe. Favor documentation, guidance, test scaffolding, and reproducible entrypoints before broad source-code edits.

## Preflight Checklist

Inspect and record:

- repository shape, top-level directories, and whether it is a monorepo, app, library, template, or mixed workspace;
- git status and whether version control is already initialized;
- languages, frameworks, lockfiles, build tools, formatters, linters, and test runners;
- executable entrypoints, scripts, background jobs, deployment files, containers, and CI workflows;
- environment variables, secrets placeholders, configuration files, data fixtures, and migrations;
- existing docs and agent instructions that should be merged instead of replaced.

## Required Repository Artifacts

Create or update these files as part of the preparation pass:

- `README.md`: human-facing overview, architecture, setup, run commands, test commands, deployment outline, and major workflows.
- `KNOWLEDGE.md`: agent-facing sharp edges, naming traps, non-obvious conventions, local debugging notes, fixture locations, and other details that are easy to forget.
- `KNOWN_BUGS.md`: issue log with at least a title, affected area, repro summary, and current status.
- `AGENT.md`: repository-specific rules for future coding agents.
- `.codex-ready/project-types/*.md`: one markdown file per detected project type, referenced from `AGENT.md`.

If equivalent files already exist, merge with them. Do not duplicate the same guidance across multiple files.

## Documentation Rules

- Put the big picture in `README.md`.
- Put details that are mostly useful during editing in `KNOWLEDGE.md`.
- When code intent is uncertain, ask the user instead of inventing an explanation.
- When a bug or suspicious behavior is discovered during inspection, document it in `KNOWN_BUGS.md` and continue the preparation pass without fixing it unless the user explicitly asks for a fix.
- Update `KNOWLEDGE.md` as new discoveries are made so later edits do not repeat the same investigation.

## AGENT.md Minimum Content

The generated `AGENT.md` must tell future agents to:

- inspect the repository before editing;
- classify the repository into all applicable project types instead of choosing only one;
- read the relevant `.codex-ready/project-types/*.md` files before making changes;
- keep edits small and stepwise;
- preserve existing code as much as possible;
- request clarification when code intent is unclear;
- request permission before editing existing source code when the task can begin with docs, tests, or scaffolding;
- consult `KNOWLEDGE.md` before repeated work;
- update `KNOWN_BUGS.md` from inspection findings and from end-to-end test results.

An `AGENT.md` import block can be as simple as:

```md
Before editing, read:

- `.codex-ready/project-types/python.md`
- `.codex-ready/project-types/frontend-web.md`
- `.codex-ready/project-types/api-service.md`
```

## Testing Rules

- Run or update unit tests for important functions during each edit cycle.
- Treat unit tests and end-to-end tests as separate responsibilities.
- Use unit tests to catch local mistakes quickly.
- Run end-to-end tests after a coherent batch of work, not after every small edit.
- If the repository has no end-to-end tests, create a mock or skeleton suite first.
- After the mock suite exists, ask the user before filling in the full end-to-end implementation.
- Whenever end-to-end tests need dummy data, ask the user to validate that the data is acceptable.
- Use end-to-end results to update `KNOWN_BUGS.md`.

## Runnable Unit-Test Entry Points

Prefer the repository's existing test framework. When the repository lacks a lightweight function-level harness, add a small runnable entrypoint that matches the stack's conventions.

For Python repositories, the default pattern is:

- use `if __name__ == "__main__":` in the module or in a close companion runner;
- allow selecting a major function by CLI argument;
- generate safe dummy data for local function checks;
- keep detailed comments around the test harness so future agents can update it along with the code.

For other stacks, use the nearest idiomatic equivalent only if it fits the project. Examples include `require.main === module`, `import.meta.main`, `examples/`, dedicated smoke-test commands, or existing test targets.

## Review Checklist

Before finishing, confirm that:

1. the generated instructions are broad enough to guide future work without becoming vague;
2. the project-type files reflect the actual repository instead of a generic template;
3. the doc split between `README.md` and `KNOWLEDGE.md` is clear;
4. the testing workflow separates per-edit unit checks from batch end-to-end checks;
5. the permission and clarification rules are visible in `AGENT.md`;
6. the repository-local project-type markdown files are explicitly referenced from `AGENT.md`.
