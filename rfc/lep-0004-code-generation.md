# LEP-0004 : Code generation

| Field          | Value                 |
| -------------- | --------------------- |
| LEP            | 0004: Code generation |
| Author         | Alex Oleshkevich      |
| Type           | Standards Track       |
| Created        | 2025-10-07            |
| Target Version | 0.1.0                 |


## Summary

Define a code generation subcommand for `lune` (`lune gen`).

## Motivation

### Goals

- Deterministic, idempotent scaffolding and safe codemods.
- Extensible generators discoverable at runtime.
- Zero “reverse sync”: user owns code after generation.
- Uniform DX across core and extensions.

### Non-Goals

- No fuzzy path guessing, AST inference of user intent, or project autodetection.


## Specification

A key object of code generation is `Generator`. Generator orchestrates multiple actions to be executed.
Keeping a separation between generator and actions opens:
- dry-run/preview mode
- code reuse - packages can export their own generators and other packages can consume them

Example
```python

class Generator:
    name: str = 'db'

    def actions(self, context: GeneratorContext) -> list[Action]:
        return [
            RenderTemplateFile('{app}/database/manager.py'),
            InsertMiddleware('{package}.routing', Middleware(
                import_name: 'starlette.middleware.sessions.Sessions,
                kwargs: {}
            )),
        ]

    def execute(self, context: GeneratorContext) -> None:
        pass

```

## Generator

- questionnaire
- command queue
- dry run
- execute in tmp dir
- copy results

api
- is package installed
- install package
- apply codemod
- copy file
- copy and render file
- iter templates
- temmp chdir
- print message/error
- format code
- add dotenv var

generator context:
- package name
- package dir
- settings obj


## Standard Codemods
- insert middleware
- remove middleware
- add view
- remove view
- insert route
- remove route
- add config option
- delete config option
- append to module
- add import
- add class attr
- add command

## Standards Commands

`lune new --template --yes --force`
`lune add extension --force --yes`
`lune gen model app.feature.User --force --yes`
`lune gen view app.feature.User --name --path --force --yes --no-test --auth`
`lune gen feature users --force --yes`


## Extensions

Packages can contribute custom generators using entrypoint registrations:

```toml
[project.entry-points."lunette.generators"]
auth.model = "lunette_auth.codegen:UserModelGen"
```
