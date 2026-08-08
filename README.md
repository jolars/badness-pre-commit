# badness-pre-commit

[![CI](https://github.com/jolars/badness-pre-commit/actions/workflows/ci.yml/badge.svg)](https://github.com/jolars/badness-pre-commit/actions/workflows/ci.yml)

A [pre-commit](https://pre-commit.com) hook for
[badness](https://github.com/jolars/badness), a formatter, linter, and language
server for LaTeX.

Distributed as a thin Python package that depends on the [`badness` PyPI
package](https://pypi.org/project/badness/), so pre-commit installs a prebuilt
binary wheel—no Rust toolchain or LaTeX distribution required. Wheels are
available for Linux, macOS, and Windows on both x64 and ARM64.

## Usage

Add this to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/jolars/badness-pre-commit
    # badness version
    rev: v0.15.0
    hooks:
      # Lint .tex, .sty, .cls, .dtx, .ins, and .bib files
      - id: badness-lint
      # Format the same files in place
      - id: badness-format
```

To apply safe lint autofixes before formatting (badness's fix-then-format
pipeline), pass `--fix`:

```yaml
- id: badness-lint
  args: [--fix]
- id: badness-format
```

To check formatting without rewriting files:

```yaml
- id: badness-format
  args: [--check]
```

Both hooks pass `--force-exclude`, so files matched by `exclude` or
`extend-exclude` in your `badness.toml` are skipped even though pre-commit names
staged files explicitly.

## Versioning

Tags mirror badness releases: installing at tag `vX.Y.Z` gives you badness
X.Y.Z. New tags are created automatically when a new badness version is
published to PyPI.

## License

MIT
