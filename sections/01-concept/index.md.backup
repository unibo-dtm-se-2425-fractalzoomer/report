---
title: Requirements
has_children: false
nav_order: 3
---

# Requirements

## User Stories

### Primary User: Explorer
**As an** explorer interested in fractals,  
**I want to** zoom into different fractal types interactively,  
**So that** I can discover intricate mathematical patterns at various scales.

**As an** explorer,  
**I want to** adjust the detail level of the rendering,  
**So that** I can balance visual quality with rendering speed.

### Secondary User: Student
**As a** mathematics student,  
**I want to** view coordinate information while exploring,  
**So that** I can understand the mathematical relationship between position and fractal features.

**As a** student,  
**I want to** compare different fractal types side-by-side,  
**So that** I can understand their unique characteristics.

### Tertiary User: Educator
**As an** educator,  
**I want to** demonstrate fractal concepts in real-time,  
**So that** I can make abstract mathematical concepts tangible for students.

## Requirements Analysis

### Functional Requirements

**FR1: Multiple Fractal Types**  
The system shall support rendering of three fractal types: Mandelbrot set, Julia set, and Burning Ship fractal.

*Acceptance Criteria:*
- User can select between Mandelbrot, Julia, and Burning Ship via radio buttons
- Each fractal renders with accurate mathematical algorithms
- Switching between fractals resets the view to appropriate default coordinates

**FR2: Interactive Zoom**  
The system shall allow users to zoom in and out by clicking on the rendered fractal.

*Acceptance Criteria:*
- Left-click zooms in by 10% centered on cursor position
- Right-click zooms out by 10%
- Zoom operations complete within 3 seconds for standard parameters
- Minimum 15 levels of zoom depth supported

**FR3: Dynamic Iteration Control**  
The system shall provide a slider to adjust maximum iterations between 50 and 500.

*Acceptance Criteria:*
- Slider updates iteration count in real-time
- Changes to iteration count trigger immediate re-rendering
- Current iteration value is displayed to user
- Higher iterations produce more detailed boundary rendering

**FR4: Coordinate Display**  
The system shall display current view center coordinates and zoom level.

*Acceptance Criteria:*
- Coordinates update after each zoom/pan operation
- Display uses scientific notation for precision
- Zoom level shown as multiplier (e.g., "2.5x")

**FR5: Responsive Rendering**  
The system shall provide visual feedback during computation.

*Acceptance Criteria:*
- Canvas updates within 2 seconds for default parameters
- Application remains responsive during rendering
- No system freezing during calculations

### Non-Functional Requirements

**NFR1: Performance**  
The system shall render fractals efficiently using optimized algorithms.

*Acceptance Criteria:*
- 90% of renders complete under 3 seconds (600x400px, 256 iterations)
- Memory usage remains under 500MB during operation
- CPU usage is reasonable for interactive exploration

**NFR2: Usability**  
The system shall have an intuitive interface requiring minimal learning.

*Acceptance Criteria:*
- First-time users can zoom and switch fractals without documentation
- All controls clearly labeled and visible
- Instructions displayed in UI

**NFR3: Portability**  
The system shall run on major desktop operating systems.

*Acceptance Criteria:*
- Compatible with macOS, Windows, and Linux
- Consistent behavior across platforms
- No platform-specific bugs in core functionality

**NFR4: Maintainability**  
The system code shall follow clean architecture principles.

*Acceptance Criteria:*
- Fractal algorithms separated from UI code
- Each fractal class independent and reusable
- Code follows PEP 8 Python style guidelines
- Functions documented with docstrings

**NFR5: Extensibility**  
The system architecture shall allow easy addition of new fractal types.

*Acceptance Criteria:*
- New fractals can be added without modifying existing fractal classes
- UI can accommodate additional fractal types with minimal changes
- Common interface pattern followed by all fractal implementations

### Implementation Requirements

**IR1: Programming Language**  
The system shall be implemented in Python 3.8 or higher.

*Justification:* Python provides excellent mathematical libraries (NumPy) and GUI frameworks (tkinter) while maintaining readability and rapid development.

**IR2: GUI Framework**  
The system shall use tkinter for the graphical interface.

*Justification:* tkinter is included with Python installations, ensuring zero external dependencies for the GUI and maximum portability.

**IR3: Numerical Computing**  
The system shall use NumPy for array operations and fractal calculations.

*Justification:* NumPy's vectorized operations provide significant performance improvements over pure Python loops for mathematical computations.

**IR4: Image Rendering**  
The system shall use Pillow (PIL) for image creation and display.

*Justification:* Pillow integrates seamlessly with tkinter and provides efficient image manipulation for fractal visualization.

## Glossary

**Fractal**: A self-similar mathematical structure exhibiting similar patterns at different scales.

**Mandelbrot Set**: The set of complex numbers c for which the iteration z_{n+1} = z_n² + c (starting from z_0 = 0) remains bounded.

**Julia Set**: A family of fractals where z_{n+1} = z_n² + c, but c is fixed and the starting point z_0 varies (inverse of Mandelbrot).

**Burning Ship Fractal**: Similar to Mandelbrot but uses absolute values: z_{n+1} = (|Re(z_n)| + i|Im(z_n)|)² + c.

**Iteration Count**: Maximum number of times the fractal formula is applied before determining if a point is in the set.

**Escape Radius**: The threshold (typically |z| = 2) beyond which a point is considered to have escaped to infinity.

**Complex Plane**: Two-dimensional space where points represent complex numbers (x + yi).

**Zoom Level**: Multiplicative factor indicating magnification relative to initial view.
