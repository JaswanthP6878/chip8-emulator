## CHIP-8 Emulator

This project implements a **CHIP-8 emulator**, a simple virtual machine designed to run classic CHIP-8 programs and games. The emulator is structured with a **shared backend core** and multiple **frontend targets**, enabling execution on both desktop and web platforms.

The goal of this project is to provide a clean, well-structured implementation of the CHIP-8 architecture while keeping the core logic independent of rendering, input, and platform-specific concerns.

---

## Architecture Overview

The project is divided into two major components:

### `chip8_core` (Backend)
- Implements the complete CHIP-8 virtual machine:
  - CPU (instruction fetch–decode–execute cycle)
  - Memory (4 KB address space)
  - Registers (V0–VF, I, PC, SP)
  - Stack and timers (delay and sound)
- Fully platform-agnostic
- Exposes a minimal interface for:
  - Instruction stepping
  - Display buffer updates
  - Keyboard input
  - Timer ticks

This separation allows the same core emulator logic to be reused across multiple execution environments.

---

### Frontends

#### Desktop Frontend (SDL2)
- Uses the **SDL2** library for:
  - Graphics rendering
  - Keyboard input handling
  - Audio output (sound timer)
- Runs the emulator loop on the host machine
- Handles timing to approximate original CHIP-8 clock behavior

#### Web Frontend (WASM)
- Compiles the `chip8_core` to **WebAssembly (WASM)**
- Runs directly in modern web browsers
- JavaScript is used for:
  - Canvas-based rendering
  - Keyboard input mapping
  - Timer and event loop integration
- Enables CHIP-8 programs to be executed without native installation

---

## Execution Model

- The frontend drives the emulation loop:
  - Fetch → Decode → Execute instructions
  - Update timers at a fixed rate
  - Render the display buffer
- The backend remains deterministic and stateless with respect to platform concerns
- Input and display updates are passed through clearly defined interfaces

This design keeps the emulator accurate, testable, and easy to extend.

---

## Supported Features

- Full CHIP-8 instruction set
- 64×32 monochrome display
- Hex-based keypad input
- Delay and sound timers
- ROM loading and execution

---

## References

- **Cowgod’s CHIP-8 Technical Reference**  
  http://devernay.free.fr/hacks/chip8/C8TECH10.HTM

