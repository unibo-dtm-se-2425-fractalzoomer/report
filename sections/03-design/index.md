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

