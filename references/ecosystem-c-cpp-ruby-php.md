# C, C++, Ruby, And PHP Guide

Read this file when the repository primarily uses C, C++, Ruby, or PHP.

## Detection

Common signals include:

- `CMakeLists.txt`, `Makefile`, `meson.build`, `Gemfile`, `Rakefile`, `composer.json`, or `artisan`;
- dependencies such as RSpec, Minitest, Rails, PHPUnit, Pest, Laravel, Symfony, or Boost.

## What To Record In Repository Guidance

- the build or package manager actually used by the repository;
- compiler or runtime version requirements;
- native library dependencies, extension build steps, or platform-specific prerequisites;
- test, lint, and packaging commands;
- code-generation or migration commands when frameworks provide them.

## Editing And Documentation Priorities

- For C or C++, document the expected compiler toolchain, build generator, sanitizer usage, and supported platforms.
- For Ruby, document Bundler commands, Rails task entrypoints, job runners, and migration workflows.
- For PHP, document Composer commands, framework entrypoints, local server expectations, and migration or seed commands.
- Preserve the repository's existing style and test framework instead of adding a new one by default.

## Testing Guidance

- C or C++: use the existing unit harness, compiler warnings, and sanitizers where available.
- Ruby: use the existing `rspec` or `minitest` setup and note any database or fixture helpers.
- PHP: use the existing PHPUnit or Pest setup and note framework-specific bootstrapping.
- Add mock end-to-end suites before full implementation when none exist, and ask the user before expanding them into full flows.

## Common Subtypes

Adapt repository-local type files for the actual mix:

- native library or SDK;
- web application;
- CLI tool;
- plugin or extension loaded by another host application.
