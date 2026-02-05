---
title: Future work
has_children: false
nav_order: 13
---

# Future Work

## Features we'd like to add

### User-facing

**Color customization**
- Different color palettes (hot, cool, grayscale)
- User-defined color gradients
- Save favorite color schemes

**Bookmarking**
- Save interesting locations
- Quick navigation to bookmarks
- Export/import bookmark files

**Animation**
- Zoom in/out animations
- Parameter transitions
- GIF export

**More fractals**
- Newton fractal
- Phoenix fractal
- Tricorn
- More Julia set variations

**Better export**
- Higher resolution rendering
- Multiple file formats
- Batch export of zoom sequences

### Technical improvements

**Performance**
- Multiprocessing for faster rendering
- GPU acceleration with CUDA
- Progressive rendering (show rough → detailed)
- Caching for frequently viewed areas

**Precision**
- Arbitrary precision math for deeper zooms (20+ levels)
- Use libraries like mpmath
- Auto-switch to high precision at deep zoom

**UI improvements**
- Modern look with custom styling
- Minimap showing current position
- Zoom history with undo
- Keyboard shortcuts

## Architecture changes

**Web version**
- Convert to web app (JavaScript + WebGL)
- Share fractals via URL
- Online gallery of interesting spots

**Plugin system**
- Let users add custom fractals
- Plugin marketplace
- Easy fractal formula editor

**Advanced math**
- 3D fractals (Mandelbulb)
- Quaternion fractals
- Different iteration formulas

## Known limitations to fix

**Current issues:**
- Float precision limits at extreme zoom (>1e15)
- No undo/redo for navigation
- Iteration slider could be smarter (auto-adjust based on zoom)
- No way to export coordinates

**Technical debt:**
- Some code duplication in fractal classes
- UI code could be more modular
- Test coverage could be 100% (currently 95%)

## Nice-to-haves

- Fractal generation tutorial mode
- Side-by-side fractal comparison
- Parameter exploration mode (show how c affects Julia sets)
- Mathematical formula display
- Integration with Jupyter notebooks
- Mobile app version
- Final release on PyPI (currently only TestPyPI)

## What we won't do

Some things are out of scope:
- Social features (sharing, comments, etc.)
- Cloud rendering service
- Commercial features
- VR/AR visualization

## Priority order

If we continue development:

1. **Color customization** (most requested, easy to add)
2. **Bookmarking** (useful, medium effort)
3. **Performance improvements** (noticeable benefit)
4. **More fractals** (fun, good for learning)
5. **Web version** (big project, but valuable)

Everything else is lower priority.

## Conclusion

The core app is solid. Future work is about making it more powerful and user-friendly, not fixing fundamental issues. We built a good foundation that's easy to extend.
