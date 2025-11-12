---
title: Design
has_children: false
nav_order: 4
---

# Design

This chapter explains the design strategies used to meet the requirements identified in the analysis phase.

## Architecture

### Architectural Style: Layered Architecture

**Chosen Style:** Layered (N-tier) Architecture

**Why Layered?**
- Clear **separation of concerns** between UI and computation logic
- **Modular design** allows independent development and testing
- **Reusability** of fractal computation modules in other contexts
- **Maintainability** through isolated responsibilities

**Why Not Other Styles?**
- **Event-based**: Overkill for simple request-response interactions
- **Shared dataspace**: No need for persistent shared state
- **Service-oriented**: No distributed services needed
- **Microservices**: Single-machine application

### Component Diagram

```plantuml
@startuml
package "Presentation Layer" {
  component [FractalZoomerUI] as UI
}

package "Business Logic Layer" {
  component [MandelbrotSet] as MB
  component [JuliaSet] as JS
  component [BurningShipSet] as BS
}

package "Foundation Layer" {
  component [NumPy]
  component [Pillow]
  component [tkinter]
}

UI --> MB : uses
UI --> JS : uses
UI --> BS : uses
UI --> [tkinter]
UI --> [Pillow]
UI --> [NumPy]
@enduml
```

### Component Responsibilities
**Presentation Layer (FractalZoomerUI)**
-Capture user input events
-Manage view state
-Coordinate fractal computations
-Render visual output

**Business Logic Layer (Fractal Classes)**
-Implement mathematical algorithms
-Calculate iteration counts
-Provide consistent interface

**Foundation Layer**
-NumPy: Numerical operations
-Pillow: Image creation
-tkinter: GUI framework

## Modelling
### Object-Oriented Design
#### Class Diagram

```plantuml
@startuml
class FractalZoomerUI {
  - root: Tk
  - canvas: Canvas
  - center_x: float
  - center_y: float
  - half_width: float
  - max_iter: int
  - fractal_type: str
  __
  + __init__(root: Tk)
  + render_fractal(): void
  + zoom_in(event: Event): void
}

class MandelbrotSet {
  - max_iter: int
  __
  + iterations(re: float, im: float): int
}

class JuliaSet {
  - cr: float
  - ci: float
  - max_iter: int
  __
  + iterations(zr: float, zi: float): int
}

class BurningShipSet {
  - max_iter: int
  __
  + iterations(c_re: float, c_im: float): int
}

FractalZoomerUI *-- MandelbrotSet
FractalZoomerUI *-- JuliaSet
FractalZoomerUI *-- BurningShipSet
@enduml
```

## Interaction
### Sequence Diagram: Zoom Interaction

```plantuml
@startuml
actor User
participant "UI" as UI
participant "Fractal" as F

User -> UI: click canvas
UI -> UI: render_fractal()
loop each pixel
  UI -> F: iterations(x, y)
  F --> UI: count
end
UI -> UI: display
@enduml
```

## Behaviour
### State Diagram
```plantuml
@startuml
[*] --> Ready
Ready --> Rendering : user action
Rendering --> Ready : complete
@enduml
```

## Performance
### Optimizations
-Quick Interior Tests (Mandelbrot): ~20% faster
-Integer Arithmetic: Grayscale mapping
-Simple Algorithms: Clear, adequate performance

### Current Limitations
Single-threaded

~2-3 seconds for 600×400 at 256 iterations
### Future Options
-Multiprocessing
-NumPy vectorization
-GPU acceleration

## Technology Justification
Python 3.8+: Rapid development, readable

-tkinter: Built-in, zero dependencies
-NumPy: Industry standard, optimized
-Pillow: Simple image creation
