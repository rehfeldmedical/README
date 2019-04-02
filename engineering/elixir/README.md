# Introduction

We standardize a number of processes & tooling across all of our Elixir applications, so that they don't drift too far apart when it comes to cross-cutting concerns. This document summarizes those elements for easy overview.

## Release management
TODO: Distillery.

## Configuration
TODO: Note where global, app-specific non-runtime, and runtime configuration should occur.

## Documentation
API documentation is part manually defined, part automated generation.

- [Bureaucrat](https://github.com/api-hogs/bureaucrat) generates Swagger JSON content for API documentation automatically based on the result of test(s)
- [Phoenix Swagger](https://github.com/xerions/phoenix_swagger) generates Swagger schemas and operations using Elixir macros written for each controller

Non-API code is documented via [ExDoc](https://github.com/elixir-lang/ex_doc)

We do not have a hard requirement to always document, but lack of documentation is a perfectly valid reason to reject a pull request. Integral or complex code should be well-documented, while peripheral or simple code can usually get away with less. Public interfaces between either modules or internal/external should almost _always_ be documented.

## Testing
We currently write both API tests and unit tests using Elixir's built-in ExUnit. There is currently no hard rule about when and where tests are appropriate, as we are still assessing those kinds of needs within Elixir project(s). In lieu of better, follow the rule from above: Extensively test things that are complex and/or core to the project, while other things can probably do with less.
