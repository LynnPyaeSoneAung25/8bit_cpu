# 8bit_cpu
An 8-bit Von Neumann computer made with CD40 logic gates, with custom microcoded control unit and software assembler.

# Architecture

An 8-bit Von Neumann computer designed and built from discrete CD40-series logic gates on breadboards, eiyh a custom microcoded control unit and integrated software toolchain.

![CPU Overview](modules/01-clock/media/manual-pulse-demo.gif)

## Summary
This project is an end-to-end implementation of a functional 8-bit microprocessor built from basic logic components. Designed around a shared 8-bit parallel bus, the architecture features dedicated registers, an Arithmetic Logic Unit (ALU) capable of Two's Complement arithmetic, an EEPROM-based microcoded Control Unit, and custom software tooling for code assembly and hardware simulation.

## Specifications & Architecture

| Parameter         | Specification |
| :---              | :---                                                                         |
| Architecture Type | Von Neumann (Unified Instruction & Data Memory)                              |
| Data Bus Width    | 8-bit parallel, tri-state buffered (74HC245)                                 |
| Address Space     | 8-bit addressing (up to 256 memory locations)                                |
| Clock Modes       | Manual Single-Step (Debounced) / Free-Running (1 Hz – 1 kHz) / Hardware Halt |
| Logic Family      | High-Speed CMOS (74HC Series)                                                |
| Control Logic     | Microcoded via parallel EEPROMs (AT28C16 / AT28C64)                          |
| Instruction Set   | Custom RISC-like 8-bit ISA (Fetch-Decode-Execute pipeline)                   |

---

## Modular Subsystem Hierarchy

The hardware is partitioned into 9 distinct modules to isolate testing and ensure precise signal timing:

1. [`/modules/01-clock`](modules/01-clock) – **Clock Module:** 555-timer based variable frequency generator, debounced manual pulse logic, and halt gating.
2. [`/modules/02-bus`](modules/02-bus) – **Data Bus System:** 8-bit parallel distribution highway with active pull-down termination and LED monitoring.
3. [`/modules/03-registers`](modules/03-registers) – **Register Array:** Accumulator (A), B Register, Instruction Register (CIR), Program Counter (PC), and Memory Address Register (MAR).
4. [`/modules/04-alu`](modules/04-alu) – **Arithmetic Logic Unit:** XOR inversion array for Two's Complement subtraction, ripple-carry addition, and Zero/Carry flag generation.
5. [`/modules/05-ram`](modules/05-ram) – **Memory Module:** Static RAM array interfaced with Memory Address (MAR) and Memory Data (MDR) registers.
6. [`/modules/06-control-unit`](modules/06-control-unit) – **Control Unit:** Instruction decoding matrix driving microcode step generation and bus enable signals.

---

## Software Toolchain & Emulation

* **Assembler (`/software/assembler`):** A custom Python-based two-pass assembler that converts human-readable assembly code into binary machine code for EEPROM flashing.
* **Web Simulator (`/software/simulator`):** Browser-based hardware emulator allowing visual instruction execution and step-by-step register inspection.

---

## Repository Structure

```text
├── README.md                 <-- Main Project Documentation
├── LICENSE                   <-- CERN Open Hardware License / MIT
├── docs/                     <-- Timing diagrams, bus protocols, and ISA specs
├── software/                 <-- Assembler, compiler backends, and simulator code
└── modules/                  <-- Module schematics, BOMs, and hardware documentation
