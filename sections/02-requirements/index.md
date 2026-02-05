---
title: Requirements
has_children: false
nav_order: 2
---

# Requirements

## What the app needs to do

### FR1: Show fractals
- Render Mandelbrot, Julia, and Burning Ship fractals in real-time
- Let users zoom in smoothly
- Use colors to visualize the patterns

### FR2: User interactions
- Click to zoom in, right-click to zoom out
- Ctrl+drag to pan around
- Reset button to go back to the default view
- Slider to adjust iteration count (more iterations = more detail)

### FR3: Controls
- Iteration slider from 50 to 500
- Switch between fractal types with radio buttons
- Display current coordinates and zoom level

### FR4: Performance targets
- Render within 1-2 seconds for normal views
- Keep the app responsive while calculating
- Don't freeze the UI

### FR5: Export (nice to have)
- Save current view as PNG or JPEG
- Export at higher resolution than screen size

## Non-functional stuff

### NFR1: Usability
- Simple enough to use without reading instructions
- Show what's happening (like when it's computing)
- Controls should feel natural

### NFR2: Performance
- Keep memory usage under 500MB
- Fast enough for interactive exploration
- Use NumPy for speed

### NFR3: Cross-platform
- Works on Windows, Mac, and Linux
- Python 3.11+ required
- Supports normal screen resolutions (Canvas is fixed at 600×400)

### NFR4: Code quality
- Clean code that's easy to understand
- Separate UI from calculation logic
- Follow PEP 8 Python style guide
- Add docstrings for main functions

### NFR5: Stability
- Don't crash on weird input
- Handle extreme zoom levels gracefully
- Show helpful error messages if something goes wrong

## Tech stack

**Python 3.11+** - Main language

**tkinter** - Built-in GUI framework (no extra installation needed)

**NumPy** - Fast array operations for fractal math

**Pillow** - Creating and coloring images

## What success looks like

- All three fractals render correctly
- Zoom and pan work smoothly
- At least 15 zoom levels supported
- Memory stays under 500MB
- Tests pass
- Works on all three major operating systems

## Terminology

**Fractal** - Self-similar pattern that looks similar when you zoom in

**Mandelbrot Set** - Formula: z = z² + c, starting from z = 0

**Julia Set** - Same formula as Mandelbrot, but with a fixed c value

**Iterations** - How many times to repeat the formula. Default at 128 (more = more detail but slower)

**Escape radius** - When |z| > 2, we know the point escapes to infinity
