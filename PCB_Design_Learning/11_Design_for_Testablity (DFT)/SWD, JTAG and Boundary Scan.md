# SWD, JTAG and Boundary Scan

# Overview

Modern embedded systems contain highly integrated microcontrollers and processors packaged in fine-pitch packages such as QFN, BGA, and LQFP. Accessing internal signals directly using oscilloscope probes or multimeters is often impossible after assembly.

To overcome this challenge, standardized debug and test interfaces were developed that allow engineers to communicate directly with the processor after the PCB has been assembled.

Two of the most widely used interfaces are:

- JTAG (Joint Test Action Group)
- SWD (Serial Wire Debug)

These interfaces allow engineers to:

- Program Flash Memory
- Debug Firmware
- Access CPU Registers
- Halt CPU Execution
- Read Memory
- Write Memory
- Verify PCB Assembly
- Perform Boundary Scan Testing

Understanding these interfaces is essential for Embedded Hardware Engineers because PCB layout decisions directly affect debugging, production testing, and firmware development.

---

# Learning Objectives

After completing this chapter, I understood:

- Why JTAG was developed
- Why ARM introduced SWD
- Difference between SWD and JTAG
- TAP (Test Access Port)
- TAP Controller
- Boundary Scan
- Boundary Scan Register
- JTAG State Machine
- SWD Communication
- PCB Design Considerations
- Debug Header Placement
- Best Practices

---

# Why Do We Need Debug Interfaces?

Consider an STM32 microcontroller in an LQFP package.

```

      STM32

 ┌─────────────────┐

 │                 │

 │     CPU         │

 │                 │

 └─────────────────┘

```

Inside this package exist

- CPU
- Flash
- SRAM
- GPIO
- Timers
- ADC
- SPI
- UART

Without a debug interface,

there is no practical way to:

- Observe program execution
- Read internal registers
- Program Flash memory
- Debug firmware

A dedicated debug interface solves this problem.

---

# What is JTAG?

JTAG stands for

**Joint Test Action Group**

It is an IEEE standard

```
IEEE 1149.1
```

developed primarily for testing printed circuit boards and later adopted for debugging embedded processors.

Originally, JTAG was introduced because integrated circuits became too complex for traditional bed-of-nails testing.

Modern JTAG provides access to the internal logic of integrated circuits without physically probing every pin.

---

# Applications of JTAG

JTAG is commonly used for:

- Programming Flash memory
- Firmware debugging
- Boundary Scan testing
- FPGA configuration
- Manufacturing testing
- PCB validation
- Device verification

It is widely supported by:

- STM32
- NXP
- TI
- Microchip
- Xilinx
- Intel FPGA
- ARM Cortex Processors

---

# Standard JTAG Signals

A standard JTAG interface consists of:

| Signal | Function |
|----------|------------------------------|
| TCK | Test Clock |
| TMS | Test Mode Select |
| TDI | Test Data Input |
| TDO | Test Data Output |
| TRST | Optional Test Reset |
| GND | Ground |
| VTREF | Target Voltage Reference |

---

# JTAG Signal Description

## TCK

TCK is the clock signal.

Every JTAG operation is synchronized using TCK.

Without TCK,

no data movement occurs.

---

## TMS

TMS controls the internal JTAG state machine.

By changing TMS values,

the debugger moves between different TAP Controller states.

---

## TDI

TDI means

Test Data Input.

Instructions and data enter the processor through TDI.

---

## TDO

TDO means

Test Data Output.

The processor returns data through TDO.

---

## TRST

TRST resets the TAP controller.

Some microcontrollers omit this pin because reset can also be achieved through the JTAG state machine.

---

# What is SWD?

SWD stands for

**Serial Wire Debug**

SWD was developed by ARM as a simplified alternative to JTAG.

Instead of using four primary communication signals,

SWD uses only two.

| Signal | Function |
|----------|----------------|
| SWCLK | Serial Wire Clock |
| SWDIO | Serial Wire Data |

Additional pins normally include:

- NRST
- SWO (optional)
- VTREF
- GND

---

# Why ARM Developed SWD

As embedded systems became smaller,

PCB area became increasingly valuable.

JTAG requires:

- Four communication pins

SWD requires only:

- Two communication pins

Advantages include:

- Smaller connector
- Reduced PCB routing
- Lower pin count
- Lower manufacturing cost
- Simpler PCB layout

This is why most modern STM32 development boards expose SWD rather than full JTAG.

---

# JTAG vs SWD

| JTAG | SWD |
|------|------|
| 4 communication signals | 2 communication signals |
| IEEE Standard | ARM Proprietary Debug Protocol |
| Supports Boundary Scan | Debug focused |
| Larger connector | Smaller connector |
| More PCB routing | Simpler routing |
| Preferred for FPGA and production testing | Preferred for ARM Cortex-M debugging |

---

# What is the TAP (Test Access Port)?

The TAP (Test Access Port) is the hardware interface that controls JTAG communication.

Think of the TAP as the "manager" of the JTAG interface.

It receives:

- Clock
- Commands
- Test Data

and controls how data moves through the internal test logic.

---

# TAP Controller

At the heart of JTAG is the TAP Controller.

The TAP Controller is a finite state machine (FSM) that controls all JTAG operations.

Every JTAG command passes through this controller.

It determines:

- Whether instructions are shifted
- Whether data is shifted
- Whether registers are updated
- Whether boundary scan is performed

The TAP Controller changes state according to the TMS signal while being synchronized by TCK.

---

# JTAG State Machine

The TAP Controller follows a predefined state machine defined by IEEE 1149.1.

Major states include:

- Test Logic Reset
- Run-Test/Idle
- Select DR Scan
- Capture DR
- Shift DR
- Exit1 DR
- Pause DR
- Exit2 DR
- Update DR
- Select IR Scan
- Capture IR
- Shift IR
- Exit1 IR
- Pause IR
- Exit2 IR
- Update IR

The debugger moves through these states to execute different JTAG operations.

---

# What is Boundary Scan?

Boundary Scan is one of the most powerful features of JTAG.

Instead of probing physical PCB traces,

JTAG allows access to digital pins through internal scan cells.

Every I/O pin is connected to a small flip-flop called a **boundary scan cell**.

These cells form a chain known as the **Boundary Scan Register**.

This allows engineers to:

- Read pin states
- Drive output pins
- Test PCB interconnections
- Detect soldering defects

without using physical probes.

---

# Boundary Scan Register

A simplified boundary scan chain looks like:

```

TDI

↓

[Cell]

↓

[Cell]

↓

[Cell]

↓

TDO

```

Each boundary cell corresponds to one device pin.

During testing, data is shifted through these cells to observe or control external pins.

---

# Why Boundary Scan is Important

Boundary Scan enables detection of manufacturing defects such as:

- Open circuits
- Short circuits
- Missing components
- Incorrect solder joints
- Broken PCB traces

without requiring direct electrical access to every pin.

This is especially valuable for fine-pitch packages such as BGA devices.

---

# PCB Design Considerations for SWD/JTAG

When adding a debug interface to a PCB:

✔ Place the debug connector near the MCU.

✔ Keep SWD/JTAG traces short.

✔ Avoid routing through noisy switching power supplies.

✔ Clearly label the connector.

✔ Ensure easy physical access after assembly.

✔ Follow the recommended pinout from the MCU manufacturer.

✔ Provide a solid ground reference.

✔ Include the RESET signal where recommended.

---

# Typical STM32 SWD Header

```
SWDIO
SWCLK
NRST
SWO (Optional)
3.3V Reference
GND
```

This header allows firmware programming and debugging using tools such as ST-LINK.

---

# Common Beginner Mistakes

❌ Omitting the SWD/JTAG header from the PCB.

❌ Placing the connector beneath large components.

❌ Routing debug signals through noisy areas.

❌ Forgetting the ground reference.

❌ Using incorrect connector pinouts.

❌ Ignoring the manufacturer's hardware design guidelines.

---

# Practical Applications

SWD and JTAG are used in:

- STM32 Development
- ARM Cortex-M Systems
- FPGA Programming
- PCB Manufacturing
- Boundary Scan Testing
- Firmware Development
- Production Debugging
- Embedded Product Validation

---

# Key Takeaways

- JTAG is a standardized interface for testing and debugging digital devices.
- SWD is ARM's simplified two-wire debug interface.
- The TAP Controller manages all JTAG operations using a defined state machine.
- Boundary Scan enables testing of PCB interconnections without direct physical probing.
- Proper PCB layout of debug interfaces improves firmware development, manufacturing testing, and long-term maintainability.
