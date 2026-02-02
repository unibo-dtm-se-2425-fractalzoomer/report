---
title: Developer Guide
has_children: false
nav_order: 11
---

# Developer Guide

## Setting up for development

```bash
# Clone the repo
git clone https://github.com/unibo-dtm-se-2425-fractalzoomer/artifact.git
cd artifact

# Install with dev dependencies
poetry install

# Run tests
poetry run pytest -v

# Check coverage
poetry run pytest --cov=fractalzoomer --cov-report=term-missing
```

## Project structure

```
artifact/
├── src/fractalzoomer/
│   ├── core/              # Fractal algorithms
│   │   ├── base.py        # Abstract base class
│   │   ├── mandelbrot.py  # Mandelbrot implementation
│   │   ├── julia.py       # Julia set implementation
│   │   └── burning_ship.py # Burning Ship implementation
│   ├── ui/                # GUI code
│   │   ├── app.py         # Main application window
│   │   └── coordinates.py # Coordinate transformations
│   └── utils/             # Utilities
│       └── exporter.py    # Image export
├── tests/                 # All tests
└── pyproject.toml         # Dependencies
```

## Adding a new fractal

1. Create a new file in `src/fractalzoomer/core/`
2. Inherit from `FractalSet`
3. Implement the `compute()` method
4. Add to the fractal switcher in `app.py`

**Example:**
```python
from fractalzoomer.core.base import FractalSet
import numpy as np

class MyFractal(FractalSet):
    def compute(self, xmin, xmax, ymin, ymax):
        # Your fractal algorithm here
        # Return a 2D NumPy array of iteration counts
        pass
```

## Running tests

```bash
# All tests
poetry run pytest

# Specific test file
poetry run pytest tests/test_core.py

# With coverage
poetry run pytest --cov

# Verbose mode
poetry run pytest -v
```

## Code style

We follow PEP 8. Main points:
- 4 spaces for indentation
- Max line length: 100 characters (ish)
- Snake_case for functions and variables
- PascalCase for classes
- Add docstrings for public methods

## Making changes

1. Create a branch: `git checkout -b feature/my-feature`
2. Make your changes
3. Write/update tests
4. Make sure tests pass: `poetry run pytest`
5. Commit: `git commit -m "feat: add my feature"`
6. Push and open a PR

## Common tasks

**Run the app during development:**
```bash
poetry run python -m fractalzoomer.ui.app
```

**Add a dependency:**
```bash
poetry add numpy  # runtime
poetry add --group dev pytest  # dev only
```

**Update dependencies:**
```bash
poetry update
```

## Debugging tips

**Print debug info:**
```python
# In any file
print(f"Debug: {variable}")
```

**Check computation output:**
```python
# In core/*.py files
result = self.compute(...)
print(f"Min: {result.min()}, Max: {result.max()}")
```

**Test a single fractal:**
```python
from fractalzoomer.core.mandelbrot import MandelbrotSet
m = MandelbrotSet()
arr = m.compute(-2, 2, -2, 2)
print(arr.shape)  # Should match image dimensions
```

## Performance

- Use NumPy vectorized operations (no Python loops)
- Profile with `cProfile` if things are slow
- Default 256 iterations is a good balance

## Need help?

Check the test files - they show how everything is supposed to work.
