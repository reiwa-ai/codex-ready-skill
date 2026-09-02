# Python Ecosystem Guide

Read this file when the repository contains Python application code, tooling, notebooks, or services.

## Detection

Common signals include:

- `pyproject.toml`, `requirements.txt`, `requirements-dev.txt`, `setup.py`, `setup.cfg`, `tox.ini`, or `Pipfile`;
- package directories with `__init__.py`;
- dependencies such as `pytest`, `ruff`, `black`, `mypy`, `fastapi`, `flask`, `django`, `celery`, `sqlalchemy`, `pandas`, or `jupyter`.

## What To Record In Repository Guidance

- the environment manager in use, such as `venv`, `uv`, `poetry`, `pip-tools`, or `conda`;
- test, lint, type-check, and format commands already used by the project;
- runtime entrypoints, background workers, management commands, migrations, and fixture loading paths;
- framework-specific conventions such as Django settings modules, Flask app factories, FastAPI dependency injection, or Celery task discovery.

## Editing And Documentation Priorities

- Reuse the existing package manager and test runner instead of introducing a new one.
- Respect the repository's formatter and linter choices. Do not force `black`, `ruff`, or `mypy` if the project uses something else.
- Document import path expectations, environment variables, migrations, and local data files in `README.md` or `KNOWLEDGE.md`.
- If notebooks exist, document which notebooks are exploratory and which produce artifacts used elsewhere.

## Testing Guidance

- Prefer the repository's current framework, usually `pytest` or `unittest`.
- Keep fast function-level tests close to important logic.
- When a lightweight manual harness is missing, add a local entrypoint using `if __name__ == "__main__":`.
- That harness should allow selecting a major function by CLI argument, generate safe dummy data, and carry detailed comments that future agents can maintain alongside the code.
- Keep side effects isolated with temp directories, test databases, or explicit dry-run flags where possible.

## Common Python Subtypes

Adapt repository-local type files for the actual mix:

- API service: note framework, routing layout, schemas, auth, and startup commands.
- Web server: note templates, static assets, session or auth behavior, and form handling.
- Worker or scheduler: note queue backend, retry semantics, cron schedule, and idempotency assumptions.
- Data or notebook workflow: note datasets, cache locations, artifact outputs, and reproducibility risks.
- CLI package: note argument parser, install mode, and sample commands for smoke tests.
