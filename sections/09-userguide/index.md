---
title: User Guide
has_children: false
nav_order: 10
---

# User Guide

## Getting started

After installing (see Deployment section), run:
```bash
poetry run python -m fractalzoomer.ui.app
```

A window will open showing the Mandelbrot set.

## Basic controls

### Zooming
- **Left-click** on any point to zoom in (10% closer)
- **Right-click** (or **Option+click** on Mac) to zoom out
- The zoom centers on where you clicked

### Panning
- **Hold Ctrl + left-click and drag** to pan around
- Release to re-render at the new position

### Iteration control
- Use the **slider** at the bottom to change iteration count (50-500)
- More iterations = more detail, but slower rendering
- Default is 256 (good balance)

### Switching fractals
- Use **radio buttons** to switch between:
  - Mandelbrot set
  - Julia set
  - Burning Ship

Each fractal starts at its default view.

## What you'll see

**Mandelbrot set**
The classic fractal. Black areas are "in the set", colored areas show how quickly points escape to infinity.

**Julia set**
Similar to Mandelbrot but with a fixed constant. Creates different patterns.

**Burning Ship**
Like Mandelbrot but with a twist - creates ship-like shapes.

## Tips

- **Start with low iterations** (100-200) when exploring, then increase for final view
- **Interesting spots in Mandelbrot**: Try zooming into the edges of the black areas
- **Deep zooms**: You can go 15+ levels deep before numerical precision limits kick in
- **Performance**: If rendering is slow, lower the iteration count

## Coordinates display

The top of the window shows:
- Current center coordinates (complex plane)
- Zoom level
- Iteration count

Use these to revisit interesting locations (though we don't have bookmarks implemented yet).

## Example workflow

1. Start the app (shows Mandelbrot)
2. Click around to explore
3. Find an interesting edge or spiral
4. Zoom in several times
5. Increase iterations to 400-500 for detail
6. Switch to Julia set to see different patterns
7. Try Burning Ship for something completely different

That's basically it! The app is pretty straightforward - just click and explore.
