# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.3.1] - 2026-11-18

### Changed
- The repository moved to the GitHub organisation `ifdd-de` as
  `tools-sbom`; links point there. The package name stays
  `sphinx-sbom-generator`.
- Package metadata: maintainers `ifdd.de contributors <maintainers@ifdd.de>`,
  homepage https://ifdd.de/packages/ and repository URL. PyPI shows them with
  the next release.
- `SECURITY.md`: contact `maintainers@ifdd.de`; the latest release is the
  supported one.

- Release workflow: the GitHub release is created with the GitHub CLI of the
  runner instead of `softprops/action-gh-release`, which the organisation
  does not allow; the tag of the first attempt at 0.3.1 failed at startup
  and published nothing.

### Removed
- The CodeQL workflow `.github/workflows/codeql.yml`. The organisation
  enables CodeQL's default setup, and GitHub refuses the results of an
  own workflow while it is on ("advanced configurations cannot be processed
  when the default setup is enabled"); every CodeQL run failed since the move.

## [0.3.0] - 2026-05-10

### Added
- Initial public release as `sphinx-sbom-generator`.
- Parsers for:
  - `requirements.txt` (pip).
  - `package.json` (npm) — `dependencies`, `devDependencies`, and
    `optionalDependencies`. Non-registry entries (git, file, link, http,
    workspace) are skipped.
  - `pyproject.toml`, supporting **PEP 621** `[project]` dependencies and
    `[project.optional-dependencies]`, **PEP 735** `[dependency-groups]`,
    and **Poetry** `[tool.poetry.dependencies]`,
    `[tool.poetry.dev-dependencies]`, and
    `[tool.poetry.group.<name>.dependencies]`.
- Metadata enrichment from PyPI and the npm registry.
- Vulnerability lookup via the OSV.dev batch API.
- **Optional transitive dependency resolution** (`--transitive` flag) for
  both PyPI and npm. Walks `requires_dist` (filtering extras and markers
  for the current environment) and `versions[v].dependencies`. BFS-based
  with cycle detection, configurable `--max-depth` (default 5) and
  `--max-packages` ceiling (default 2000).
- JSON file cache with TTL and atomic writes.
- Sphinx-ready Markdown renderer with an overview, per-ecosystem tables
  separating direct from transitive dependencies, a "Via" column for
  transitive provenance, and a per-package vulnerability detail section.
- Command-line interface (`sphinx-sbom-generator`) and module entry point
  (`python -m sbom_generator`), including `--version` / `-V`.

[0.3.1]: https://github.com/ifdd-de/tools-sbom/compare/v0.3.0...v0.3.1
[0.3.0]: https://github.com/ifdd-de/tools-sbom/releases/tag/v0.3.0
