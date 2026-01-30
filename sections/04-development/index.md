---
title: Development
has_children: false
nav_order: 4
---

# Development

## DVCS Strategy

### Repository Structure
- **artifact**: Application source code
- **report**: Project documentation
- Hosted on GitHub: `unibo-dtm-se-2425-fractalzoomer/`

### Branching
- `main`: Production-ready code only
- Feature branches: `feature/<description>`
- Fix branches: `fix/<description>`
- Protected main branch requires PR reviews

### Commit Messages
Following Conventional Commits:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `refactor`: Code restructuring

**Example:** `fix: Add option key support for zooming out on Macbook`

### Pull Request Process
1. Create feature branch from main
2. Implement and test changes
3. Commit with conventional messages
4. Open PR with description
5. Code review by team member
6. Merge and delete branch

## Implementation Details

### Architecture
Standalone desktop application with no network communication. All computation happens locally.

### Data Representation
- **NumPy arrays**: Store iteration counts and coordinate grids
- **PIL Images**: RGB color mapping from iteration data
- **Python objects**: Application state in memory
- No persistent storage or databases

### Authentication
Not applicable - single-user desktop application with no network features.

## Technology Stack

### Core Language
**Python 3.10+**
- Excellent numerical libraries (NumPy)
- Built-in GUI (tkinter)
- Cross-platform compatibility
- Rapid development

### Dependencies

**NumPy (≥1.24.0)**
- Vectorized array operations (10-100x faster than loops)
- Complex number arithmetic
- Coordinate grid generation

**Pillow (≥10.0.0)**
- Image creation and color mapping
- tkinter integration
- RGB conversion from arrays

**tkinter (Built-in)**
- Zero external dependencies
- Cross-platform GUI
- Lightweight and fast

### Development Tools
- **Poetry**: Dependency management
- **pytest**: Unit testing
- **Git/GitHub**: Version control and collaboration

### External Services
None - fully offline application with no cloud dependencies.

### Development Setup

```bash
git clone https://github.com/unibo-dtm-se-2425-fractalzoomer/artifact.git
cd artifact
poetry install
poetry run python -m fractalzoomer.ui.app
```

### Versioning
Semantic Versioning (MAJOR.MINOR.PATCH):

- Current: **4.0.1**
- **4.0.1**: Option key zoom fix (Macbook)
- **4.0.0**: Ctrl+drag panning
- **3.0.0**: Windows context manager fix
