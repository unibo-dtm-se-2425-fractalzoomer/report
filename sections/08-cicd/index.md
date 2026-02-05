---
title: CI/CD
has_children: false
nav_order: 9
---

# CI/CD

## What we automate

We use GitHub Actions to automatically run tests whenever code is pushed:
- Catch bugs before merging
- Ensure cross-platform compatibility
- Consistent release process
- No manual version management errors
- Test results visible directly in GitHub

**What runs automatically:**
- All 85 tests via pytest
- Code coverage check
- Runs on every push to main
- Also runs on pull requests

## Why automate testing?

Simple reasons:
- Catch bugs before merging
- Make sure nothing breaks when adding features
- Don't have to remember to run tests manually
- See test results right in GitHub

## How it works

We have a workflow file at `.github/workflows/test.yml` that:

1. Triggers on push or PR
2. Sets up Python 3.11
3. Installs Poetry
4. Installs dependencies with `poetry install`
5. Runs `poetry run pytest --cov`
6. Shows results in the PR/commit

**Basic workflow:**
```yaml
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: ['3.11', '3.12', '3.13']
      - name: Install Poetry
        run: pip install poetry
      - name: Install dependencies
        run: poetry install
      - name: Run tests
        run: poetry run pytest --cov
```

We apply semantic release principles to versioning and releases, plus TestPyPI for distribution (see [Release](sections/06-release) for details).

## Deploy Workflow

Runs after successful tests on main branch:

1. Analyzes commits using Conventional Commits format
2. Determines version bump (major/minor/patch)
3. Updates pyproject.toml version
4. Builds and publishes to TestPyPI
5. Creates GitHub Release with changelog

deploy.yml snippet:
```yaml
- name: Release
  run: npx semantic-release
  env:
    PYPI_USERNAME: ${{ secrets.PYPI_USERNAME }}
    PYPI_PASSWORD: ${{ secrets.PYPI_PASSWORD }}
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Secrets configuration
The pipeline uses GitHub Secrets for secure storage of:
- `PYPI_USERNAME` - TestPyPI username
- `PYPI_PASSWORD` - TestPyPI password associated to a token provided by TestPyPI
- `GITHUB_TOKEN` - GitHub token for releases
