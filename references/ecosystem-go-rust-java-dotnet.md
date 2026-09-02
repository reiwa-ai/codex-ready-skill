# Go, Rust, Java, Kotlin, And .NET Guide

Read this file when the repository is built around Go, Rust, JVM languages, or .NET.

## Detection

Common signals include:

- `go.mod`, `Cargo.toml`, `pom.xml`, `build.gradle`, `build.gradle.kts`, `settings.gradle`, `*.sln`, or `*.csproj`;
- directories such as `cmd/`, `internal/`, `pkg/`, `src/main`, `src/test`, `bin/`, or `Properties/`;
- dependencies such as Spring Boot, Micronaut, Quarkus, Tokio, Axum, Actix, Serde, ASP.NET, xUnit, or JUnit.

## What To Record In Repository Guidance

- canonical build, test, lint, and run commands;
- workspace or module boundaries and how binaries, libraries, and test projects relate;
- framework conventions for configuration, dependency injection, migrations, background jobs, and generated code;
- any version pinning requirements for JDK, .NET SDK, Go, or Rust toolchains.

## Editing And Documentation Priorities

- Follow the existing build system instead of mixing tools.
- Record how local development starts the service or application and how fixtures or test databases are provisioned.
- Note generated code sources such as protobuf, OpenAPI, Entity Framework migrations, or build-time asset generation.
- Keep repository-local type files explicit about where business logic lives versus framework glue.

## Testing Guidance By Ecosystem

- Go: favor package tests, table-driven cases, and `go test` targets that map to the edited package.
- Rust: favor `cargo test`, module tests, integration tests, and examples when they match the crate layout.
- Java or Kotlin: use the existing JUnit and Gradle or Maven targets, and note any Spring test slices or containerized dependencies.
- .NET: use the existing test project structure and document solution-level versus project-level commands.
- Add a manual smoke harness only when it fits the ecosystem cleanly; otherwise prefer the native test framework.

## Common Subtypes

Adapt repository-local type files for the actual mix:

- service or API server;
- CLI binary plus supporting library packages;
- multi-module monorepo;
- desktop or GUI app;
- background worker or stream processor.
