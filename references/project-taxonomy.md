# Project Taxonomy

Read this file after the initial repository scan. The repository may belong to several categories at once. Capture all of them and create one repository-local markdown file per detected type under `.codex-ready/project-types/`.

## Classify Across Multiple Axes

Classify the repository across these axes instead of forcing a single label:

- repository shape: single package, application, library or SDK, monorepo, template or starter, plugin or extension, documentation-heavy project;
- primary ecosystems: Python, JavaScript or TypeScript, Go, Rust, Java or Kotlin, C#, C or C++, Ruby, PHP, shell or PowerShell, SQL-heavy, infrastructure configuration;
- operating surfaces: API service, server-rendered web app, SPA frontend, component library, CLI or TUI, worker or scheduler, data pipeline, notebook workflow, ML training or inference, desktop app, mobile app, infrastructure or deployment repo;
- cross-cutting concerns: database migrations, queues, caches, auth, payments, third-party API clients, file storage, containers, CI pipelines, generated code, localization, or plugins.

## Useful Detection Signals

Inspect these signals before deciding which reference guides to load:

- manifests and lockfiles such as `pyproject.toml`, `requirements.txt`, `package.json`, `Cargo.toml`, `go.mod`, `pom.xml`, `build.gradle`, `*.csproj`, `Gemfile`, `composer.json`, `CMakeLists.txt`, `Dockerfile`, and `terraform` files;
- framework-specific directories such as `app/`, `src/`, `pages/`, `components/`, `api/`, `migrations/`, `infra/`, `charts/`, `notebooks/`, `cmd/`, `bin/`, `packages/`, and `services/`;
- CI files and scripts that reveal build, lint, packaging, deployment, and test commands;
- imports and dependencies that reveal the actual stack even when top-level docs are outdated.

## Reference Mapping

Load the ecosystem guide that best matches each primary language:

- Python: [ecosystem-python.md](ecosystem-python.md)
- JavaScript or TypeScript: [ecosystem-js-ts.md](ecosystem-js-ts.md)
- Go, Rust, Java, Kotlin, or .NET: [ecosystem-go-rust-java-dotnet.md](ecosystem-go-rust-java-dotnet.md)
- C, C++, Ruby, or PHP: [ecosystem-c-cpp-ruby-php.md](ecosystem-c-cpp-ruby-php.md)

Load the surface guide that matches the user-facing or operational shape:

- Web UI, SSR, or component library: [surface-web-ui.md](surface-web-ui.md)
- Mobile or desktop app: [surface-mobile-desktop.md](surface-mobile-desktop.md)
- Data, ML, infra, notebooks, shell-heavy automation, or CI-focused repo: [surface-data-ml-infra.md](surface-data-ml-infra.md)

## Common Open-Source Patterns To Consider

These mixes show up often and should be captured explicitly when present:

- Python API service with FastAPI, Flask, or Django plus migrations and background jobs;
- Node.js or TypeScript service with Express, NestJS, Hono, or serverless handlers;
- React, Vue, Svelte, Next.js, Nuxt, Astro, or static-site frontend;
- shared component library or SDK consumed by other applications;
- CLI or TUI tool distributed as a package or binary;
- monorepo with multiple packages, apps, or services and per-package scripts;
- Go or Rust service with CLI utilities and deployment manifests;
- Java or Kotlin service with Spring Boot, Maven, or Gradle;
- .NET solution with web app, worker, and test projects;
- C or C++ library or app using CMake, Make, or custom build scripts;
- Ruby or Rails app with Rake tasks, jobs, and migrations;
- PHP or Laravel application with Composer and web routing;
- data-science, notebook, ETL, or ML workflow with fixtures, models, and long-running jobs;
- infrastructure repository with Terraform, Kubernetes, Helm, Docker, or GitHub Actions;
- Electron, Tauri, Flutter, React Native, Android, or iOS application;
- plugin, extension, or integration repo that depends on a host platform's lifecycle and packaging rules.

## Repository-Local Type Files

Translate the relevant guidance into short repository-local markdown files. Keep each file specific to one detected type, for example:

- `.codex-ready/project-types/python.md`
- `.codex-ready/project-types/frontend-web.md`
- `.codex-ready/project-types/monorepo.md`
- `.codex-ready/project-types/data-pipeline.md`

Those local files should mention the repository's actual frameworks, commands, and known sharp edges instead of repeating the generic guidance verbatim.
