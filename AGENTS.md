# Repository Guidelines

## Project Structure & Module Organization
DomainRanger keeps all runtime code under `src/`, grouped by bounded context (e.g. `src/analyzer/`, `src/api/`). Shared cross-cutting pieces go in `src/shared/`. Tooling and experimental spike code belongs in `tools/`. Tests mirror the production layout under `tests/`, with fixtures in `tests/fixtures/` and integration pipelines under `tests/integration/`. When a feature needs native helpers (C++ or Go), place sources in `native/` and surface them through the owning .NET project so they stay part of the solution file.

## Build, Test, and Development Commands
`dotnet restore` restores NuGet dependencies across the solution. `dotnet build` compiles every project with the default configuration. Use `dotnet test --collect:"XPlat Code Coverage"` to run the xUnit suites and produce coverage reports. Run `dotnet watch run --project src/api/DomainRanger.Api.csproj` for a hot-reload development loop, and `dotnet format` before committing to apply the repo’s analyzers.

## Coding Style & Naming Conventions
Stick to C# 12 features, four-space indentation, and file-scoped namespaces. Name classes, records, and public methods with PascalCase, locals and parameters in camelCase, and async methods with the Async suffix. Organize files so that one public type lives per file. Apply the built-in analyzers plus `dotnet format` to enforce MSBuild EditorConfig rules; do not bypass warnings without a documented justification.

## Testing Guidelines
Unit and component tests use xUnit; mirror the namespace of the system under test and suffix files with `Tests`. Prefer Arrange-Act-Assert structure and keep each test independent via fixture factories in `tests/shared/`. For coverage gates, aim for 80% line coverage and ensure critical domain flows have scenario tests in `tests/integration/`. Run `dotnet test` locally before opening a pull request, and include new regression cases alongside bug fixes.

## Commit & Pull Request Guidelines
The repository history currently consists of bootstrap commits; continue with Conventional Commits (`feat`, `fix`, `chore`, etc.) and imperative subjects. Limit the body to motivation plus notable decisions, and reference issue IDs when available. Pull requests should describe the change, outline validation steps, and attach screenshots or logs for UI or CLI-facing updates. Request reviews from a domain owner and ensure CI passes before merging.

## Security & Configuration Tips
Never commit secrets or API tokens; rely on local `.env.development` files ignored by Git. Document new configuration keys in `docs/configuration.md` (create the file if absent) and provide safe defaults. For third-party dependencies, prefer signed releases and track SBOM updates in `docs/security/`.
