---
title: CI/CD
has_children: false
nav_order: 9
---

# CI/CD

## What we automate

We use GitHub Actions to automatically run tests whenever code is pushed.

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
          python-version: '3.10'
      - name: Install Poetry
        run: pip install poetry
      - name: Install dependencies
        run: poetry install
      - name: Run tests
        run: poetry run pytest --cov
```

No secrets needed since everything runs locally. No deployment automation - this is just a desktop app that users run on their machines.

## What we don't automate

- Releases (we do those manually with git tags)
- Deployment (there's nothing to deploy - it's a desktop app)
- Building packages (users just clone and run)
- Publishing to PyPI (not a library)

For a course project, automated testing is enough. Keeping it simple.
