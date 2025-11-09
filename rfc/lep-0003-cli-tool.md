# LEP-0003 : CLI tool

| Field          | Value            |
| -------------- | ---------------- |
| LEP            | 0003: CLI tool   |
| Author         | Alex Oleshkevich |
| Type           | Standards Track  |
| Created        | 2025-10-07       |
| Target Version | 0.1.0            |


## Summary

This LEP describes `lune`, the unified command-line tool that ships with the Lunette framework. `lune` installs with the Lunette package, auto-detects the active project, and exposes both core and project-defined subcommands.

## Motivation

- One entry point for the entire lifecycle of the application
- Delegate jobs to real tools (alembic, uvicorn, esbuild) - but wrap with smart defaults
- Provide convenience wrappers where boilerplate/env/config can be inferred
- Allow extensions (auth, admin, payments, etc.) to register their own commands

## Design Goals

1. **Always available**: Installed alongside Lunette; no per-project bootstrap script.
2. **Project-aware**: Detect project name, location, and dependencies via `pyproject.toml`.
3. **Extensible**:  entry points allow packages to register commands; project-local plugins auto-discovered.
5. **Introspective**: Commands can read project metadata, dependencies, routing tables, and schema definitions without user wiring.

## Specification

Implemented with `click` and `rich` for prompts/output.

### Project & Dependency Detection

The tool detects current project name from `pyproject.toml` `project.name` key. Reads application instance configuration from `project_name/app.py`.

### Standard commands

Here is a list of built-in commands.

- `lune new`: initialize a new project from template. Provides interactive TUI to pick project features.
- `lune add`: add a project feature (database, cache, auth, ...)
- `lune run`: run application (production via gunicorn, development via uvicorn with reload)
- `lune gen`: run code generators
- `lune route list`: list all routes as a table
- `lune route match`: match URL path and show matched route info
- `lune route resolve`: resolve url by route name
- `lune config`: print configuration
- `lune reveal`: copy configuration file from the framework to the project (for example alembic.ini)
- `lune test`: run unit tests

Framework components add their own commands when configured for the project.

### Extensibility

Extension packages register commands under `lunette.commands`.

```toml
[project.entry-points."lunette.commands"]
payments = "myext_payments.cli:cli"
billing = "myext_billing.cli:cli"
```
