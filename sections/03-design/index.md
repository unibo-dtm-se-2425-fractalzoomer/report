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
![Component diagram showing layered architecture with three tiers: Presentation Layer containing FractalZoomerUI at the top, Business Logic Layer in the middle with MandelbrotSet, JuliaSet, and BurningShipSet components, and Foundation Layer at the bottom with NumPy, Pillow, and tkinter components. Arrows labeled uses connect FractalZoomerUI to each component in the other layers, illustrating the dependencies between layers in a clean, hierarchical software architecture design](images/Componentdiagram.png)

## Component Responsibilities

### Presentation Layer (FractalZoomerUI)

-Capture user input events
-Manage view state
-Coordinate fractal computations
-Render visual output

### Business Logic Layer (Fractal Classes)

-Implement mathematical algorithms
-Calculate iteration counts
-Provide consistent interface

### Foundation Layer

-NumPy: Numerical operations
-Pillow: Image creation
-tkinter: GUI framework

## Modelling

### Object-Oriented Design

#### Class Diagram

![Class diagram displaying object-orieROdeoRodeonted design for fractal zoomer application with four main classes. FractalZoomerUI class at top contains attributes like root Tk, canvas Canvas, center coordinates, dimensions, max_iter int, fractal_type str, and three fractal objects. Methods include init, setup_ui, render_fractal, zoom_in, zoom_out, update_iterations, and change_fractal. MandelbrotSet class on bottom left has max_iter int attribute and methods init, iterations, and static inside_fast. JuliaSet class in bottom center contains cr float, ci float, max_iter int attributes with init and iterations methods. BurningShipSet class on bottom right has max_iter int attribute and init plus iterations methods. Composition relationships connect FractalZoomerUI to all three fractal classes with filled diamond arrows indicating ownership. Clean technical diagram with standard UML notation showing hierarchical software architecture](images/OODclassdiagram.png)

## Interaction
### Sequence Diagram: Zoom Interaction

![Sequence diagram illustrating zoom interaction workflow between User, UI, and Fractal components. User clicks canvas triggering UI activation. UI calculates bounds and calls render_fractal function. A loop processes each pixel by calling iterations method on Fractal component which returns count value to UI. UI then creates image, displays result, and returns updated view to User before deactivating. Vertical lifelines show object existence with rectangular activation boxes indicating processing periods. Horizontal arrows represent method calls and responses in chronological order from top to bottom. Clean technical diagram using standard UML sequence diagram notation with clear labels and systematic flow depicting interactive fractal rendering process](images/SequenceDiagram.png)

### Sequence Diagram: Slider Update

![Sequence diagram showing slider update interaction between User, UI, MandelbrotSet, JuliaSet, and BurningShipSet components. User moves slider triggering UI activation. UI sets max_iter value on all three fractal components MandelbrotSet, JuliaSet, and BurningShipSet, then calls render_fractal function internally. UI returns updated fractal to User and deactivates. Vertical lifelines represent object existence with rectangular activation boxes showing processing periods. Horizontal arrows indicate method calls flowing left to right in chronological sequence from top to bottom. Clean technical diagram using standard UML sequence notation depicting systematic parameter update workflow across multiple fractal computation classes](images/Sliderupdate.png)

## Behaviour

### State Diagram

![State diagram showing application behavior with five states connected by labeled transitions. Starting from a black dot at top, an arrow leads to Initializing state represented as rounded rectangle. Arrow labeled setup complete connects to Ready state which contains nested AwaitingInput state with its own initial state marker. From Ready, arrow labeled user action leads to Processing state, then parameters updated arrow connects to Rendering state, and render complete arrow returns to Ready state creating a cycle. Final arrow labeled window closed leads from Ready to end state represented by black dot with circle. Clean technical diagram using standard UML state diagram notation depicting systematic application workflow from initialization through user interaction cycle to termination](images/behaviourStateDiagram.png)

### Fractal Iteration Algorithm Flow

![Flowchart diagram depicting fractal iteration algorithm with decision points and loops. Flow begins at black circle labeled start, proceeds to Initialize z equals 0 comma i equals 0 in rounded rectangle. Arrow points down to diamond-shaped decision node asking is absolute value of z greater than 2 question mark. If yes branch leads right to return i in rounded rectangle, then down to black circle with inner circle indicating end state. If no branch continues down to another diamond asking is i greater than or equal to max underscore iter question mark. Yes branch connects right to return max underscore iter rounded rectangle, then down to end state. No branch flows down to rectangular process box stating z equals z squared plus c, followed by i plus plus increment operation, then continue label with arrow looping back up to first decision point. Clean technical flowchart using standard symbols with black text on white background depicting systematic mathematical computation process for fractal generation algorithms](images/Algorithmflow.png)

## Performance
### Optimizations

-Quick Interior Tests (Mandelbrot): ~20% faster
-Integer Arithmetic: Grayscale mapping
-Simple Algorithms: Clear, adequate performance

### Current Limitations
-Single-threaded
-~2-3 seconds for 600×400 at 256 iterations

### Future Options
-Multiprocessing
-NumPy vectorization
-GPU acceleration

## Technology Justification
-Python 3.8+: Rapid development, readable
-tkinter: Built-in, zero dependencies
-NumPy: Industry standard, optimized
-Pillow: Simple image creation

**Pillow**
- Simple image creation
- Decision: Simplifies rendering