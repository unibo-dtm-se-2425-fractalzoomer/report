---
title: Self-evaluation
has_children: false
nav_order: 12
---

# Self-evaluation

## What went well

**Code quality**
- 95% test coverage is solid
- Clean separation between fractal algorithms and UI
- NumPy vectorization makes it fast

**Project management**
- Git workflow worked smoothly
- Conventional commits kept history readable
- Incremental development with clear versions

**Technical choices**
- Python + NumPy was the right call for this
- tkinter is simple and works cross-platform
- Poetry makes dependency management easy

**Features**
- All three fractals work correctly
- Zoom and pan are responsive
- Platform-specific fixes (Mac Option key, Windows window closing)

## What could be better

**Testing**
- No automated GUI tests (manual only for tkinter)
- Could test more edge cases in coordinate transformations
- Some branches not covered (mostly error handling)

**Features we didn't implement**
- No color scheme customization
- No bookmarking of interesting locations
- No animation or recording
- Export feature exists but isn't in the UI

**Performance**
- Deep zooms (20+ levels) hit floating point precision limits
- Could try arbitrary precision libraries for deeper zooms
- No GPU acceleration (all CPU-based)

**Documentation**
- Could use more inline code comments
- Some design decisions not explained in code

## Lessons learned

**Technical:**
- NumPy is incredibly powerful for numerical work
- GUI testing is hard - manual testing sometimes makes more sense
- Cross-platform differences are real (Mac vs Windows behavior)

**Process:**
- Small, frequent commits are better than big batches
- Writing tests as you go prevents bugs later
- Semantic versioning helps track what changed

**Scope:**
- Better to do 3 fractals well than 10 poorly
- Simple UI > complex UI for a course project
- Desktop app is simpler than web app

## If we did this again

- **Start with tests first** (more TDD approach)
- **Add color customization** (users would like it)
- **Implement bookmarks** (to save interesting locations)
- **Try multiprocessing** for faster rendering
- **Better error messages** when things go wrong

## Grade self-assessment

Based on requirements:
- Multiple fractals working
- Interactive zoom and pan
- Cross-platform support
- Good test coverage
- Clean architecture
- Documentation complete

We met all the core requirements and added some extras (platform-specific fixes, export functionality). The code is maintainable and the architecture is extensible.

Overall, we're happy with what we built. It does what it's supposed to do, and the code quality is good. Could it be better? Sure but it's solid.


## Personal reflections

### Diana

From my side, I think we both managed the **project management** part quite well: we kept the repository structure clean, split the code and report into two repos, and communicated regularly about what each of us was doing. The overall structure of the project (core, UI, utils, tests) came out clear and easy to follow.

On the technical side, both of us struggled a bit with making the code efficient, especially around the zoom feature. The first versions of the rendering logic were quite heavy, and the app sometimes failed to load images properly or felt very slow when zooming. Iterating on the NumPy usage and the way we recomputed the viewport was not straightforward and took several rounds of trial and error.

Overall, I think we both did a good job, especially considering that we don’t come from a pure engineering background. We still managed to build something that works well, is reasonably fast, and is backed by a solid test suite.

### Luca

