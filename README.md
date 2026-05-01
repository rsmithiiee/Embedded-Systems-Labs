# CMPE 146 — Embedded Systems Lab Portfolio

Lab reports and firmware exercises for **CMPE 146 - Real-Time Embedded System Co-Design**.  
Each lab builds on the previous, progressing from bare-metal C on the MSP432 to a full RTOS-based multitasking application.

**Hardware:** Texas Instruments MSP432P401R LaunchPad  
**IDE / Toolchain:** Code Composer Studio (CCS) + MSP432 DriverLib SDK  
**Language:** C → TI-RTOS (later labs)

---

## Table of Contents

- [Lab Overview](#lab-overview)
- [Getting Started](#getting-started)
- [Lab Summaries](#lab-summaries)
  - [Lab 1 — CCS Setup & MCU Basics](#lab-1--ccs-setup--mcu-basics)
  - [Lab 2 — GPIO & Timing](#lab-2--gpio--timing)
  - [Lab 3 — CRC, Interrupts & DMA](#lab-3--crc-interrupts--dma)
  - [Lab 4 — Flash & SRAM Memory](#lab-4--flash--sram-memory)
  - [Lab 5 — Timers & Frequency Measurement](#lab-5--timers--frequency-measurement)
  - [Lab 6 — UART & EnergyTrace](#lab-6--uart--energytrace)
  - [Lab 7 — ADC & TI-RTOS Introduction](#lab-7--adc--ti-rtos-introduction)
  - [Lab 8 — RTOS Semaphores & Multitasking](#lab-8--rtos-semaphores--multitasking)
- [Demo Videos](#demo-videos)
- [Author](#author)

---

## Lab Overview

| Lab | Topic | Key Concepts |
|-----|-------|--------------|
| 1 | CCS & MCU Basics | SDK setup, Hello World, LED blink, TLV memory map |
| 2 | GPIO & Timing | Bit-banding, DriverLib GPIO, time & frequency measurement |
| 3 | CRC / Interrupts / DMA | CRC-32, checksum algorithms, ISR design, DMA transfers |
| 4 | Flash & SRAM Memory | Memory map, flash programming, non-volatile storage |
| 5 | Timers & Measurement | Timer32 delay, GPIO oscillator, frequency measurement, LED PWM |
| 6 | UART & Power | Serial communication, EnergyTrace power profiling |
| 7 | ADC & RTOS Intro | 14-bit ADC sampling, TI-RTOS task model |
| 8 | RTOS Multitasking | Semaphores, multi-task computation, shared resource protection |

---

## Getting Started

### Prerequisites

- **Code Composer Studio** 12.x or later
- **MSP432 SDK** (SimpleLink MSP432P4 SDK) — install via CCS Resource Explorer
- **TI-RTOS** (required for Labs 7–8) — available through CCS Resource Explorer
- **MSP432P401R LaunchPad** evaluation board

### Importing a Lab into CCS

1. Clone or download this repository.
2. Open CCS → **File → Import → CCS Projects**.
3. Browse to the desired `Lab N/` folder and select the project.
4. Click **Finish** — CCS will resolve SDK paths automatically if the SDK is installed.
5. Build with **Ctrl+B**, then flash to the board with **Run → Debug**.

### Folder Structure

```
├── Lab 1/
│   └── Lab 1.docx          # Report with code snippets, analysis, and screenshots
├── Lab 2/
│   ├── Lab 2.docx
│   └── Calculations.xlsx   # Timing/frequency calculation worksheet
├── Lab 3/
│   └── Lab 3.docx
├── Lab 4/
│   └── Lab 4.docx
├── Lab 5/
│   └── Lab 5.docx
├── Lab 6/
│   ├── Lab 6.docx
│   └── Measurements.xlsx   # UART / EnergyTrace measurement data
├── Lab 7/
│   └── Lab 7.docx
└── Lab 8/
    └── Lab 8.docx
```

---

## Lab Summaries

### Lab 1 — CCS Setup & MCU Basics

Sets up the development environment and introduces bare-metal programming on the MSP432.

| Exercise | Description |
|----------|-------------|
| 1 | Install and configure Code Composer Studio and the MSP432 SDK |
| 2 | Write and run a "Hello World" program over the debugger console |
| 3 | Blink an onboard LED using GPIO DriverLib calls |
| 4 | Walk the TLV (Tag-Length-Value) memory structure at `0x00201000` to read device info, die revision, and calibration data |

---

### Lab 2 — GPIO & Timing

Explores GPIO control via both bit-banding and DriverLib, then measures timing precision on the MSP432.

| Exercise | Description |
|----------|-------------|
| 1 | Bit-banding: toggle RGB LEDs and read button S1 via DriverLib; measure execution time at register vs. DriverLib level |
| 2 | Time measurement: benchmark the overhead of a DriverLib vs. direct-register GPIO write |
| 3 | Frequency measurement: use Timer_A to measure an external signal frequency |

---

### Lab 3 — CRC, Interrupts & DMA

Implements data integrity algorithms and hardware-accelerated data movement.

| Exercise | Description |
|----------|-------------|
| 1 | CRC-32: implement a simple byte-accumulation checksum, then compare it to the MSP432 hardware CRC-32 engine |
| 2 | Interrupt: configure a GPIO interrupt on button S1 and handle debouncing in the ISR |
| 3 | DMA: use the DMA controller to transfer a buffer without CPU involvement; measure throughput vs. CPU-copy |

---

### Lab 4 — Flash & SRAM Memory

Investigates the MSP432 memory map and programs non-volatile flash storage at runtime.

| Exercise | Description |
|----------|-------------|
| 1 | Flash memory: distinguish string literals (flash) from character arrays (SRAM); observe write-protection behavior |
| 2 | Non-volatile power-on-reset counter: write a counter to flash that survives reset/power cycle |
| 3 | SRAM function: dynamically copy and execute a function from SRAM |

---

### Lab 5 — Timers & Frequency Measurement

Uses Timer32 for precise software delays and builds a GPIO-based software oscillator.

| Exercise | Description |
|----------|-------------|
| 1 | Delay function: implement `delay_ms()` using Timer32 with wrap-around handling |
| 2 | GPIO oscillator: toggle a pin at a target frequency using the delay function; verify with an oscilloscope |
| 3 | Frequency measurement: measure a square wave on an input pin using Timer_A capture mode |
| 4 | LED control: use frequency measurement feedback to modulate LED brightness |

---

### Lab 6 — UART & EnergyTrace

Introduces serial communication and power profiling.

| Exercise | Description |
|----------|-------------|
| 1 | UART: configure eUSCI_A for 115200 baud; send and receive characters; loopback test |
| 2 | EnergyTrace: use CCS EnergyTrace to profile active vs. sleep current; compare LPM0, LPM3, LPM4 |

---

### Lab 7 — ADC & TI-RTOS Introduction

Samples analog signals with the onboard 14-bit ADC and transitions to an RTOS programming model.

| Exercise | Description |
|----------|-------------|
| 1 | ADC: configure ADC14 to sample the onboard temperature sensor and a potentiometer; print values over UART |
| 2 | TI-RTOS: create multiple tasks; observe preemptive scheduling with RTOS Analyzer |

---

### Lab 8 — RTOS Semaphores & Multitasking

Applies RTOS primitives to coordinate concurrent tasks safely.

| Exercise | Description |
|----------|-------------|
| 1 | Semaphore: protect a shared resource between two tasks using a binary semaphore; verify mutual exclusion |
| 2 | Multiple tasks to compute: split a computation (e.g., matrix multiply or sorting) across cooperating RTOS tasks and measure throughput improvement |

---

## Demo Videos

The table below maps each demo to the exercise it covers.

| Lab | Exercise | Description | Video |
|-----|----------|-------------|-------|
| 1 | Exercise 3 | Blink LED |  |
| 2 | Exercise 1 | Bit-banding — button toggles RGB LED |  |
| 3 | Exercise 2 | Button interrupt with debouncing |  |
| 4 | Exercise 2 | Non-volatile reset counter |  |
| 5 | Exercise 2 | GPIO oscillator verified on oscilloscope |  |

---

---

## Support & Resources

- [MSP430 Micontroller Device Documents]([https://www.ti.com/lit/ug/slau597f/slau597f.pdf](https://dev.ti.com/tirex/explore/node?isTheia=false&node=ACmHMTUKODOT9KJKrdqKyw))
- [Code Composer Studio IDE](https://www.ti.com/tool/CCSTUDIO)
