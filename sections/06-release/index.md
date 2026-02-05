---
title: Release
has_children: false
nav_order: 7
---

# Release

## What we release

Fractalzoomer is a lightweight application intended to run on desktop and laptop computers without requiring powerful hardware. The distribution strategy combines GitHub Releases for source code access with TestPyPI for streamlined package installation, providing flexibility for both developers who want to examine the codebase and users who simply want to run the application.

### PyPi installation:
```bash
pip install -i https://test.pypi.org/simple/ fractalzoomer
```

### GitHub installation (Source Code):
1. Clone the repository:
```bash
git clone https://github.com/your-username/fractalzoomer.git
```
2. Navigate to the project directory:
```bash
cd fractalzoomer
```
3. Install dependencies:
```bash
poetry install
```
4. Run the application:
```bash
poetry run fractalzoomer
```

### Distribution Strategy:
- **GitHub**: Provides access to the source code, allowing developers to contribute, report issues, and understand how the application works. Releases on GitHub include source code archives and changelogs.
- **TestPyPI**: As an educational project, we use TestPyPi to provide us the ability to experience package distribution without polluting the official PyPI repository. This allows users to easily install the application using pip while we test our release process.

## License

**Apache License 2.0**: This license allows users to freely use, modify, and distribute the software, with minimal restrictions. It provides a permissive framework that encourages collaboration and sharing while protecting the original authors' rights.

## Versioning

We use **Semantic Versioning** (MAJOR.MINOR.PATCH):

- **PATCH** (like 4.0.1): Bug fixes, no new features
- **MINOR** (like 4.1.0): New features, backward compatible
- **MAJOR** (like 5.0.0): Breaking changes

Our versions so far:
- **4.0.1**: Fixed Option key zoom on Mac (bug fix → PATCH)
- **4.0.0**: Added Ctrl+drag panning (changed controls → MAJOR)
- **3.0.0**: Fixed window closing on Windows (platform fix → MAJOR)

## How to release

When we want to release a new version:

1. **Make sure tests pass**
```bash
poetry run pytest -v
```

2. **Update version in pyproject.toml**
```toml
version = "4.1.0"  # or whatever the new version is
```

3. **Commit and tag**
```bash
git add pyproject.toml
git commit -m "chore: bump version to 4.1.0"
git push origin main

git tag -a v4.1.0 -m "Fix XYZ bug"
git push origin v4.1.0
```

4. **Create GitHub Release**
- Go to GitHub repo → Releases → "Draft a new release"
- Pick the tag we just created
- Write what changed
- Publish

