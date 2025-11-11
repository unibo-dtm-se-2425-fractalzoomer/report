***
title: Design
has_children: false
nav_order: 4
***

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

Component Responsibilities
Presentation Layer (FractalZoomerUI)

Capture user input events

Manage view state

Coordinate fractal computations

Render visual output

Business Logic Layer (Fractal Classes)

Implement mathematical algorithms

Calculate iteration counts

Provide consistent interface

Foundation Layer

NumPy: Numerical operations

Pillow: Image creation

tkinter: GUI framework

Modelling
Object-Oriented Design
Class Diagram
@startuml
class FractalZoomerUI {
  - root: Tk
  - canvas: Canvas
  - center_x: float
  - center_y: float
  - half_width: float
  - half_height: float
  - max_iter: int
  - fractal_type: str
  - mandelbrot: MandelbrotSet
  - julia: JuliaSet
  - burning_ship: BurningShipSet
  __
  + __init__(root: Tk)
  + setup_ui(): void
  + render_fractal(): void
  + zoom_in(event: Event): void
  + zoom_out(event: Event): void
  + update_iterations(value: int): void
  + change_fractal(): void
}

class MandelbrotSet {
  - max_iter: int
  __
  + __init__(max_iter: int)
  + iterations(re: float, im: float): int
  + {static} inside_fast(re: float, im: float): bool
}

class JuliaSet {
  - cr: float
  - ci: float
  - max_iter: int
  __
  + __init__(cr: float, ci: float, max_iter: int)
  + iterations(zr: float, zi: float): int
}

class BurningShipSet {
  - max_iter: int
  __
  + __init__(max_iter: int)
  + iterations(c_re: float, c_im: float): int
}

FractalZoomerUI *-- MandelbrotSet
FractalZoomerUI *-- JuliaSet
FractalZoomerUI *-- BurningShipSet
@enduml

Interaction
Sequence Diagram: Zoom Interaction
@startuml
actor User
participant "UI" as UI
participant "Fractal" as F

User -> UI: click canvas
activate UI
UI -> UI: calculate bounds
UI -> UI: render_fractal()

loop each pixel
  UI -> F: iterations(x, y)
  F --> UI: count
end

UI -> UI: create image
UI -> UI: display
User <-- UI: updated view
deactivate UI
@enduml

Sequence Diagram: Slider Update
@startuml
actor User
participant "UI" as UI
participant "MandelbrotSet" as MB
participant "JuliaSet" as JS
participant "BurningShipSet" as BS

User -> UI: move slider
activate UI
UI -> MB: max_iter = value
UI -> JS: max_iter = value
UI -> BS: max_iter = value
UI -> UI: render_fractal()
User <-- UI: updated fractal
deactivate UI
@enduml

Behaviour
State Diagram
@startuml
[*] --> Initializing
Initializing --> Ready : setup complete

state Ready {
  [*] --> AwaitingInput
}

Ready --> Processing : user action
Processing --> Rendering : parameters updated
Rendering --> Ready : render complete
Ready --> [*] : window closed
@enduml

Activity Diagram: Fractal Computation
@startuml
start
:Initialize z = 0, i = 0;

repeat
  if (|z| > 2?) then (yes)
    :return i;
    stop
  endif
  
  if (i >= max_iter?) then (yes)
    :return max_iter;
    stop
  endif
  
  :z = z² + c;
  :i++;
repeat while (continue)
@enduml
Performance
Optimizations
Quick Interior Tests (Mandelbrot): ~20% faster

Integer Arithmetic: Grayscale mapping

Simple Algorithms: Clear, adequate performance

Current Limitations
Single-threaded

~2-3 seconds for 600×400 at 256 iterations

Future Options
Multiprocessing

NumPy vectorization

GPU acceleration

Progressive rendering

Technology Justification
Python 3.8+

Rapid development, readable

Decision: Development speed prioritized

tkinter

Built-in, zero dependencies

Decision: Simplicity worth trade-off

NumPy

Industry standard, optimized

Decision: Performance justifies dependency

Pillow

Simple image creation

Decision: Simplifies rendering