---
title: Development
has_children: false
nav_order: 4
---

# Development

## Git Setup

We're using GitHub with two repositories:
- **artifact**: The actual code
- **report**: This documentation

We keep `main` branch for working code only. When adding features, we create a `feature/` or `fix/` branch, then merge via pull request after someone reviews it.

### Commit style

We're following Conventional Commits (mostly):
- `feat:` for new features
- `fix:` for bug fixes  
- `docs:` for documentation
- `refactor:` when cleaning up code

Example: `fix: Add option key support for zooming out on Macbook`

## How it's built

This is a standalone desktop app - no servers, no network calls, everything runs locally on your computer.

**Data:**
- NumPy arrays store the iteration counts and coordinates
- PIL creates the images from those arrays
- Everything lives in memory while the app runs

**No authentication needed** - it's just a single-user desktop app.

## Tech choices

### Python 3.11+
We went with Python because:
- NumPy is perfect for the heavy math
- tkinter comes built-in for the GUI
- Works on Windows, Mac, and Linux
- Quick to develop and iterate

### Key libraries

**NumPy (≥2.4.0)**
Does all the fractal calculations. Using NumPy's vectorized operations makes it 10-100x faster than regular Python loops.

**Pillow (≥12.0.0)**  
Creates the actual images and handles colors.

**tkinter (built-in)**
The GUI framework. It's already included with Python, so no extra dependencies needed.

### Dev tools
- **Poetry** for managing dependencies
- **pytest** for testing. Preferred instead of unittest for simplified writing and readability.
- **Git/GitHub** for version control

No external services - this runs completely offline.

## Getting started

Clone and run:
```bash
git clone https://github.com/unibo-dtm-se-2425-fractalzoomer/artifact.git
cd artifact
poetry install
poetry run fractalzoomer # Uses entry point defined in pyproject.toml
```

## Versions

We use Semantic Versioning (MAJOR.MINOR.PATCH):

- **4.1.0** (current): Fixed Option key zoom on Mac
- **4.0.0**: Added Ctrl+drag panning (changed how controls work)
- **3.0.0**: Fixed window closing issue on Windows
