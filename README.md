# Custom Operating System Development

## Overview

This repository documents the development of a custom operating system built completely from scratch using low-level systems programming concepts.

The project focuses on understanding the internal architecture of operating systems by progressively implementing core components such as bootloading, memory management, interrupt handling, hardware communication, kernel functionality, and system-level abstractions.

The implementation is being developed by following the educational series:

- :contentReference[oaicite:0]{index=0}

This repository serves as:
- a learning journal
- an experimental systems programming workspace
- a low-level architecture study project
- a reference for future kernel and embedded development

---

# Objectives

The primary goals of this project are:

- Understand computer boot processes
- Develop a custom bootloader
- Learn x86 architecture fundamentals
- Build a minimal kernel
- Understand memory management
- Explore interrupt handling mechanisms
- Interface directly with hardware
- Study low-level systems programming
- Learn linker and compiler workflows
- Understand OS abstraction layers

---

# Topics Covered

The project will progressively explore concepts including:

- Bootloaders
- BIOS and hardware initialization
- Real Mode and Protected Mode
- x86 Assembly
- C-based kernel development
- Interrupt Descriptor Table (IDT)
- Global Descriptor Table (GDT)
- Paging and memory management
- Keyboard and screen drivers
- Timer interrupts
- System calls
- Basic shell implementation
- File systems
- Process management
- Multitasking fundamentals

---

# Technologies Used

| Component | Purpose |
|---|---|
| Assembly (NASM) | Low-level hardware interaction |
| C Programming | Kernel development |
| GNU Toolchain | Compilation and linking |
| QEMU | Virtual machine emulation |
| Make | Build automation |
| GCC | Cross compilation |
| GDB | Debugging |
| WSL/Linux Environment | Development environment |

---

# Development Environment

The operating system is being developed in a Linux-based workflow using:

- WSL2
- GNU development tools
- NASM assembler
- QEMU emulator
- GCC cross-compilation toolchain

---

# Learning Goals

This project is intended to strengthen understanding in:

- Computer Architecture
- Systems Programming
- Low-Level Memory Operations
- Hardware Abstraction
- Kernel Internals
- Assembly Language
- Embedded Concepts
- Debugging at Bare-Metal Level

---

# Current Status

The project is currently under active development.

Planned progress includes:
- boot sector development
- protected mode transition
- kernel initialization
- hardware driver implementation
- memory subsystem development
- basic operating system services

---

# References

## Main Learning Resource

- :contentReference[oaicite:1]{index=1}

## Additional References

- :contentReference[oaicite:2]{index=2}
- :contentReference[oaicite:3]{index=3}
- :contentReference[oaicite:4]{index=4}
- :contentReference[oaicite:5]{index=5}
- :contentReference[oaicite:6]{index=6}

---

# Educational Purpose

This repository is primarily intended for:
- learning
- experimentation
- systems programming practice
- architecture exploration

The implementation prioritizes educational understanding over production-level operating system design.

---

# Future Plans

Potential future enhancements include:

- custom shell
- filesystem support
- multitasking
- user mode support
- scheduler implementation
- memory allocator
- keyboard and display drivers
- ELF loading
- syscall interface
- simple GUI experimentation

---

# Author

Narendaran S G

---

# License

This project is intended for educational and research purposes.
