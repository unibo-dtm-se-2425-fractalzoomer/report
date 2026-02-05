---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

This is a desktop app - no servers, no cloud, nothing fancy. Just runs on your computer.

## Installation

### What you need

**Python 3.11+**
Check: `python3 --version`

If you don't have it:
- Mac: `brew install python@3.11` or download from python.org
- Windows: Download from python.org
- Linux: `sudo apt install python3.11` (Ubuntu) or `sudo dnf install python3.11` (Fedora)

**Poetry**
Install: `curl -sSL https://install.python-poetry.org | python3 -`

**Git**
Most systems have this. If not: `brew install git` (Mac) or download from git-scm.com

### Steps

1. **Clone the repo**
```bash
git clone https://github.com/unibo-dtm-se-2425-fractalzoomer/artifact.git
cd artifact
```

2. **Install dependencies**
```bash
poetry install
```

This installs NumPy, Pillow, and sets up a virtual environment automatically.

3. **Run it**
```bash
poetry run python -m fractalzoomer.ui.app
```

That's it! The app window should open.

### Optional: Test it works
```bash
poetry run pytest -v
```

Should see "85 passed".

### Configuration

No configuration needed. It just works with sensible defaults:
- 600×400 window
- Mandelbrot fractal shown first
- 256 iterations

If you want to change defaults, edit `src/fractalzoomer/ui/app.py` (lines around 15-20).

### Uninstalling

```bash
rm -rf artifact  # Delete the folder
```

## Server stuff

**There is no server.** Everything runs locally on your machine.

No database, no API, no network calls, no cloud services. Just pure desktop application.

## Platform notes

**Mac:**
- tkinter included with Python
- Option key for zoom out works (fixed in v4.0.1)

**Windows:**
- tkinter included with Python
- Window closing works correctly (fixed in v3.0.0)

**Linux:**
- May need to install tkinter separately: `sudo apt install python3-tk`
- Otherwise works the same

## System requirements

**Minimum:**
- Dual-core CPU
- 2GB RAM
- 100MB disk space

**Better experience:**
- Quad-core CPU or better
- 4GB+ RAM

Faster computer = faster fractal rendering at high iteration counts.
