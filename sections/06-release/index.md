---
title: Release
has_children: false
nav_order: 7
---

# Release

## What we release

Just one thing: a Python desktop app distributed through GitHub.

We don't publish to PyPI because this isn't a library - it's an application. Users just clone the repo and run it with Poetry.

GitHub works well for us because:
- It's a course project, not a commercial product
- Easy version tracking with tags
- Users can download specific versions
- No need for Docker or package registries

## License

**MIT License** for everything.

Why MIT?
- Simple and permissive
- Common for university projects
- Anyone can use, modify, and learn from the code
- No complicated restrictions

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
version = "4.0.2"  # or whatever the new version is
```

3. **Commit and tag**
```bash
git add pyproject.toml
git commit -m "chore: bump version to 4.0.2"
git push origin main

git tag -a v4.0.2 -m "Fix XYZ bug"
git push origin v4.0.2
```

4. **Create GitHub Release**
- Go to GitHub repo → Releases → "Draft a new release"
- Pick the tag we just created
- Write what changed
- Publish

That's it. No complicated CI/CD, no container builds. Just tag and release on GitHub.
