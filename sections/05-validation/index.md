---
title: Validation
has_children: false
nav_order: 6
---

# Validation

## Testing approach

We used **pytest** for testing because it's simpler than unittest and has better error messages. We didn't follow strict TDD (test-driven development), but we wrote tests as we built features.

The focus was on testing the fractal math and coordinate calculations. We skipped automated testing for the tkinter GUI since it's really difficult to test GUI components automatically - manual testing works better for that.

## Automated tests

### Unit tests

We have **85 tests** across 4 files, all passing with **95% coverage**.

**What we tested:**

`test_coordinate_mapping.py` (20 tests) - Coordinate conversions
- Converting screen pixels to complex plane coordinates
- Going back from complex to screen coordinates
- Making sure roundtrip conversions work correctly

`test_core.py` (32 tests) - The fractal algorithms
- All three fractals (Mandelbrot, Julia, Burning Ship)
- Parameter validation
- Making sure each fractal computes correctly

`test_exporter.py` (22 tests) - Image export
- Saving as PNG, JPEG, BMP
- Adding metadata to images
- Color mapping from iteration data

`test_parameter_julia.py` (11 tests) - Julia set parameters
- Testing different c values
- Preset configurations
- Edge cases

### Coverage

| File | Coverage | Notes |
|------|----------|-------|
| coordinates.py | 100% | All coordinate math covered |
| mandelbrot.py | 97% | One edge case branch not hit |
| julia.py | 96% | Almost complete |
| exporter.py | 93% | Main functionality covered |
| burning_ship.py | 92% | Core algorithm tested |

Overall: **95% coverage**

The UI file (`app.py`) isn't included because testing tkinter is more trouble than it's worth - we test that manually.

### Running tests

```bash
poetry run pytest --cov=fractalzoomer --cov-report=term-missing -v
```

## Manual testing

For the GUI, we manually tested:

**Zoom and pan**
- Click to zoom in, right-click (or Option on Mac) to zoom out
- Ctrl+drag to pan around
- Tested going 15+ zoom levels deep

**Fractal switching**
- Switch between all three fractals with radio buttons
- Make sure it switches within 3 seconds

**Iteration slider**
- Adjust from 50 to 500 iterations
- Check that more iterations = more detail

**Cross-platform**
- Tested on Mac (Option key zoom fix in v4.0.1)
- Tested on Windows (window closing fix in v3.0.0)
- Tested on Linux (works fine)

All manual tests passed. The app is responsive and doesn't freeze during calculations.
