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
- **Shared dataspace**: No need for persistent shared state between components
- **Service-oriented**: No need for distributed services in desktop application
- **Microservices**: Single-machine application doesn't require distribution

### Architecture Overview

The application adopts a **3-layer architecture**:

@startuml
package "Presentation Layer" {
component [FractalZoomerUI] as
I note right o
UI - Event
andling - Canv
s rendering
User controls - V
ew state
package "Business Logic Layer" {
component [MandelbrotSet] as
B component [JuliaSet] a
JS component [BurningShipSet]
as BS note rig
t of MB - Iteratio
algorithms - Mathemati
al computations -
No UI d
package "Foundation Layer" {
component [NumP
] component [Pil
ow] component [tk
UI --> MB : uses
UI --> JS : uses
UI --> BS : uses
UI --> [tkinter] : GUI framework
UI --> [Pillow] : image rendering
UI --> [NumPy] : array operations


### Component Responsibilities

**Presentation Layer (FractalZoomerUI)**
- Capture and process user input events
- Manage view state (center coordinates, zoom level)
- Coordinate fractal computation requests
- Convert computation results to visual representation
- Handle UI updates and rendering

**Business Logic Layer (Fractal Classes)**
- Implement mathematical algorithms for each fractal type
- Calculate iteration counts for given complex coordinates
- Provide consistent interface (`iterations(x, y)` method)
- No dependencies on UI or external libraries

**Foundation Layer (External Libraries)**
- NumPy: Efficient numerical array operations
- Pillow: Image creation from numerical data
- tkinter: GUI framework and event system

## Infrastructure

**Not Applicable:** This is a standalone desktop application with no network components, servers, or distributed infrastructure.

All components run in a **single Python process** on the **user's local machine**.

## Modelling

### Object-Oriented Design

#### UML Class Diagram

@startuml
class FractalZoomerUI {

root: Tk

canvas: Canvas

center_x: float

center_y: float

half_width: float

half_height: float

max_iter: int

fractal_type: str

mandelbrot: MandelbrotSet

julia: JuliaSet

burning_ship: BurningShipSet

iter_slider: Scale

fractal_var: StringVar

info_label: Label
__

init(root: Tk)

setup_ui(): void

render_fractal(): void

zoom_in(event: Event): void

zoom_out(event: Event): void

update_iterations(value: int): void

change_fractal(): void
}

class MandelbrotSet {

max_iter: int
__

init(max_iter: int)

iterations(re: float, im: float): int

{static} inside_fast(re: float, im: float): bool
}

class JuliaSet {

cr: float

ci: float

max_iter: int
__

init(cr: float, ci: float, max_iter: int)

iterations(zr: float, zi: float): int
}

class BurningShipSet {

max_iter: int
__

init(max_iter: int)

iterations(c_re: float, c_im: float): int
}

FractalZoomerUI *-- "1" MandelbrotSet : contains
FractalZoomerUI *-- "1" JuliaSet : contains
FractalZoomerUI *-- "1" BurningShipSet : contains

note right of FractalZoomerUI
Main UI controller that
orchestrates all interactions
end note

note bottom of MandelbrotSet
z = z² + c
starting from z₀ = 0
end note

note bottom of JuliaSet
z = z² + c
c is fixed, z₀ varies
end note

note bottom of BurningShipSet
z = (|Re(z)| + i|Im(z)|)² + c
end note
@enduml


#### Main Data Types

**1. FractalZoomerUI**
- **Purpose**: Manage entire user interface and coordinate interactions
- **Key Attributes**:
  - `center_x, center_y`: Current view center in complex plane
  - `half_width, half_height`: Current view dimensions
  - `max_iter`: Maximum iteration count
  - `fractal_type`: Currently selected fractal ("mandelbrot", "julia", "burning_ship")
  - Fractal instances: `mandelbrot`, `julia`, `burning_ship`

- **Key Methods**:
  - `render_fractal()`: Main rendering pipeline
  - `zoom_in(event)`, `zoom_out(event)`: Handle zoom interactions
  - `update_iterations(value)`: Adjust detail level
  - `change_fractal()`: Switch between fractal types

**2. MandelbrotSet**
- **Purpose**: Compute Mandelbrot set iterations
- **Key Attributes**:
  - `max_iter`: Maximum iteration threshold
- **Key Methods**:
  - `iterations(re, im)`: Calculate escape iterations for point c = re + i·im
  - `inside_fast(re, im)`: Quick check for main cardioid and bulb (optimization)

**3. JuliaSet**
- **Purpose**: Compute Julia set iterations with fixed parameter
- **Key Attributes**:
  - `cr, ci`: Fixed complex parameter c = cr + i·ci
  - `max_iter`: Maximum iteration threshold
- **Key Methods**:
  - `iterations(zr, zi)`: Calculate escape iterations starting from z₀ = zr + i·zi

**4. BurningShipSet**
- **Purpose**: Compute Burning Ship fractal iterations
- **Key Attributes**:
  - `max_iter`: Maximum iteration threshold
- **Key Methods**:
  - `iterations(c_re, c_im)`: Calculate iterations with absolute value transformation

#### Relationships

- **Composition**: `FractalZoomerUI` contains instances of all three fractal classes
- **No Inheritance**: Fractal classes are independent (no base class)
- **Polymorphism**: All fractals implement `iterations(x, y)` method with same signature
- **Dependency**: UI layer depends on fractal layer; fractals have zero dependencies

### Design Patterns

**Strategy Pattern (Implicit)**
- **Context**: `FractalZoomerUI` selects which fractal algorithm to use
- **Strategies**: `MandelbrotSet`, `JuliaSet`, `BurningShipSet`
- **Benefit**: Easy to switch fractals at runtime without changing UI code

**Composition over Inheritance**
- No class hierarchy among fractals
- Each fractal is independent and self-contained
- New fractals can be added without modifying existing ones

## Interaction

### Component Communication

**Interaction Pattern: Request-Response (Synchronous)**

All interactions are **synchronous** and **local** (no network, no async operations):

1. **User → UI**: User performs action (click, move slider, select radio button)
2. **UI → Fractal**: UI calls `fractal.iterations(x, y)` for each pixel
3. **Fractal → UI**: Fractal returns iteration count (integer)
4. **UI → User**: UI renders image and displays to user

### UML Sequence Diagram: Zoom Interaction

@startuml
actor User
participant "FractalZoomerUI" as UI
participant "Canvas" as Canvas
participant "MandelbrotSet" as Fractal

User -> UI: left-click on canvas
activate UI

UI -> UI: zoom_in(event)
note right: Calculate click position\nin complex plane

UI -> UI: Calculate new bounds
note right: Scale by zoom factor 0.9\nCenter on click point

UI -> UI: render_fractal()

loop for each pixel (i, j) in 600×400
UI -> Fractal: iterations(x[j], y[i])
activate Fractal
Fractal -> Fractal: Compute escape time
Fractal --> UI: return iteration_count
deactivate Fractal
UI -> UI: Map to grayscale
end

UI -> UI: Create Image from array
note right: PIL.Image.fromarray()

UI -> Canvas: create_image(PhotoImage)
activate Canvas
Canvas --> UI: Display on canvas
deactivate Canvas

UI -> UI: Update info label
note right: Show coordinates,\nzoom level, iterations

User <-- UI: See updated fractal view
deactivate UI
@enduml


### UML Sequence Diagram: Iteration Slider Update
@startuml
actor User
participant "FractalZoomerUI" as UI
participant "Slider" as Slider
participant "MandelbrotSet" as MB
participant "JuliaSet" as JS
participant "BurningShipSet" as BS

User -> Slider: Move slider
activate Slider
Slider -> UI: trigger callback with value
deactivate Slider

activate UI
UI -> UI: update_iterations(value)

UI -> MB: max_iter = value
activate MB
deactivate MB

UI -> JS: max_iter = value
activate JS
deactivate JS

UI -> BS: max_iter = value
activate BS
deactivate BS

UI -> UI: render_fractal()
note right: Re-render with new\niteration limit

User <-- UI: See updated fractal\nwith new detail level
deactivate UI
@enduml


### UML Sequence Diagram: Fractal Type Switch
@startuml
actor User
participant "FractalZoomerUI" as UI
participant "RadioButton" as Radio

User -> Radio: Select "Julia"
activate Radio
Radio -> UI: trigger change_fractal()
deactivate Radio

activate UI
UI -> UI: fractal_type = fractal_var.get()
note right: Get selected value\n("mandelbrot", "julia", or "burning_ship")

alt fractal_type == "mandelbrot"
UI -> UI: Reset to (-0.5, 0.0)
else fractal_type == "julia"
UI -> UI: Reset to (0.0, 0.0)
else fractal_type == "burning_ship"
UI -> UI: Reset to (-1.75, -0.03)
end

UI -> UI: half_width = 1.75
UI -> UI: half_height = 1.0

UI -> UI: render_fractal()
note right: Render new fractal type\nwith default view

User <-- UI: See selected fractal
deactivate UI
@enduml


## Behaviour

### UI Component State Machine

The `FractalZoomerUI` is **stateful** and maintains:
- Current view position (`center_x`, `center_y`)
- Current zoom level (`half_width`, `half_height`)
- Current iteration limit (`max_iter`)
- Active fractal type (`fractal_type`)

#### UML State Diagram: FractalZoomerUI States
@startuml
[*] --> Initializing

state Initializing {
[] --> CreatingFractals
CreatingFractals --> SettingUpUI
SettingUpUI --> []
}
note right of Initializing : Create fractal instances\nSetup UI components\nSet default parameters

Initializing --> Ready : Initial render complete

state Ready {
[*] --> AwaitingInput
}
note right of Ready : Display current view\nAll controls active\nReady for user interaction

Ready --> ProcessingZoom : User clicks canvas
Ready --> ProcessingSlider : User moves slider
Ready --> ProcessingSwitch : User selects fractal

state ProcessingZoom {
[] --> CalculatingBounds
CalculatingBounds --> []
}

state ProcessingSlider {
[] --> UpdatingIterations
UpdatingIterations --> []
}

state ProcessingSwitch {
[] --> ChangingFractal
ChangingFractal --> ResettingView
ResettingView --> []
}

ProcessingZoom --> Rendering : Trigger render
ProcessingSlider --> Rendering : Trigger render
ProcessingSwitch --> Rendering : Trigger render

state Rendering {
[] --> GeneratingGrid
GeneratingGrid --> ComputingIterations
ComputingIterations --> CreatingImage
CreatingImage --> DisplayingImage
DisplayingImage --> []
}
note right of Rendering : Compute fractal\nfor all pixels\nDisplay result

Rendering --> Ready : Render complete

Ready --> [*] : Window closed
@enduml


### Fractal Component Behaviour

All fractal classes are **stateless** at the computation level:
- Each call to `iterations(x, y)` is independent
- No internal state changes during computation
- `max_iter` is configuration, not mutable state

#### UML Activity Diagram: Fractal Iteration Computation
@startuml
start
:Receive complex coordinate (c_re, c_im);
:Initialize z = 0 + 0i;
:iteration = 0;

repeat
:Calculate |z| = sqrt(re² + im²);

if (|z| > 2.0?) then (yes)
:return iteration;
stop
endif

if (iteration >= max_iter?) then (yes)
:return max_iter;
stop
endif

:z_new = z² + c;
note right: For Mandelbrot/Julia\nBurning Ship uses |z|² + c

:z = z_new;
:iteration = iteration + 1;

repeat while (continue)

@enduml


#### UML Activity Diagram: Rendering Pipeline
@startuml
start
:User triggers render;

:Calculate view bounds;
note right: x_min, x_max, y_min, y_max\nfrom center and half_width/height

:Generate coordinate grids;
note right: NumPy linspace\nx, y

:Create empty image array;
note right: numpy.zeros((H, W), uint8)

partition "For each pixel" {
:Get pixel (i, j);
:Map to complex (x[j], y[i]);
:Call fractal.iterations(x, y);
:Get iteration count;
:Map to grayscale [0-255];
:Store in array[i, j];
}

:Create PIL Image from array;
:Convert to PhotoImage;
:Display on canvas;
:Update info label;

stop
@enduml


## Data-Related Aspects

### Persistent Storage

**Not Required:** The application does not persist any data between sessions.

**Rationale:**
- Fractal views are generated on-demand from parameters
- No user-generated content to save
- Exploration is ephemeral (like a calculator)
- Future enhancement: Could add bookmark/favorite views

### Transient Data

**Runtime Data Only:**
- View state (coordinates, zoom) - stored in UI instance variables
- Rendered image - stored as `PhotoImage` in memory
- Iteration results - computed per-frame, discarded after rendering

**No File I/O:**
- No configuration files
- No export/import functionality (could be future enhancement)
- No logging (development uses console output)

### Data Sharing

**No Inter-Component Data Sharing:**
- UI and fractals communicate only through method calls
- No shared memory or global state
- Each render is independent computation

**Data Flow is Unidirectional:**
UI parameters → Fractal computation → Iteration counts → Image data → Display


## Performance Considerations

### Optimization Strategies

**1. Quick Interior Tests (Mandelbrot only)**
- Skip expensive iterations for known interior points
- Cardioid and period-2 bulb detection
- ~20% performance improvement for typical views

**2. Integer Arithmetic Where Possible**
- Grayscale mapping uses integer division
- Avoids floating-point conversion overhead

**3. Simplicity Over Premature Optimization**
- Clear, straightforward algorithms
- Python loops (not vectorized)
- Adequate performance for intended use

### Scalability Analysis

**Current Limitations:**
- Single-threaded computation
- O(width × height × avg_iterations) complexity
- ~2-3 seconds for 600×400 at 256 iterations

**Future Scalability Options:**
- Multiprocessing: Parallelize pixel computations
- NumPy vectorization: Compute entire arrays at once
- GPU acceleration: CUDA/OpenCL for massive parallelism
- Progressive rendering: Show low-res preview first

## Technology Justification

### Python 3.8+
- **Pro**: Rapid development, readable, excellent libraries
- **Con**: Slower than C/C++/Rust
- **Decision**: Development speed and maintainability prioritized over raw performance

### tkinter
- **Pro**: Built-in (no pip install), cross-platform, simple
- **Con**: Dated appearance, limited widgets
- **Decision**: Zero-dependency GUI worth the aesthetic trade-off

### NumPy
- **Pro**: Industry standard, optimized, well-tested
- **Con**: External dependency
- **Decision**: Performance and utility justify dependency

### Pillow (PIL)
- **Pro**: Simple image creation, tkinter integration
- **Con**: External dependency
- **Decision**: Simplifies rendering pipeline significantly

## Alternative Designs Considered

### Web-Based Application (JavaScript + Canvas)
- **Pro**: No installation, runs anywhere, easy sharing
- **Con**: More complex stack, network dependency, browser compatibility
- **Rejected**: Overkill for local exploration tool

### Base Class for Fractals (Inheritance Hierarchy)
- **Pro**: Code reuse through inheritance
- **Con**: Tight coupling, rigidity, harder to extend
- **Rejected**: Composition provides more flexibility

### GPU Acceleration from Start
- **Pro**: 100-1000x performance improvement possible
- **Con**: Complex, platform-specific, CUDA/OpenCL learning curve
- **Rejected**: Premature optimization for project scope




