# ESP32 Based Graphical LCD Controller

## Project Overview

This project was developed to design a compact graphical display controller using the ESP32-S3 microcontroller.

The system interfaces a 128×64 graphical LCD through an I²C I/O expander and provides additional keypad input capability. The design focuses on reducing GPIO utilization, simplifying PCB routing, and maintaining a compact board form factor suitable for embedded HMI (Human Machine Interface) applications.

The complete design includes:

- ESP32-S3 based control unit
- 128×64 graphical LCD interface
- MCP23017 I²C GPIO expander
- Matrix keypad interface
- On-board DC-DC power supply
- Programming and debugging interface
- Compact two-layer PCB implementation

---

## Design Objectives

- Implement a graphical LCD interface using ESP32-S3.
- Reduce LCD GPIO requirements through I²C expansion.
- Provide keypad input support.
- Design a manufacturable two-layer PCB.
- Maintain all major components on the bottom side of the PCB.
- Place the LCD connector on the top side for enclosure compatibility.
- Ensure reliable power distribution from a 15V external supply.

---

## Hardware Features

### ESP32-S3

The ESP32-S3 serves as the primary processing unit responsible for:

- LCD control
- Keypad scanning
- User interface logic
- Communication handling

### Graphical LCD Interface

A 128×64 graphical LCD is connected through an MCP23017 I²C GPIO expander, significantly reducing the number of ESP32 GPIOs required for display control.

### Keypad Interface

The keypad connector allows external button matrix integration for user interaction.

### Power Management

The board accepts a 15V external supply and generates regulated 5V and 3.3V rails for system operation.

---

## Repository Structure

- Project Requirements
- System Architecture
- Schematic Design
- Component Selection
- PCB Layout
- Manufacturing Files
- Lessons Learned

---

## Key Design Challenges

- Reducing LCD GPIO consumption
- Routing a dense LCD interface on a compact PCB
- Separating power and signal paths
- Maintaining manufacturability
- Supporting future display upgrades

---

## Design Status

✔ Requirements Definition

✔ Architecture Design

✔ Schematic Capture

✔ Component Selection

✔ PCB Layout

✔ Routing Completion

✔ Design Verification

✔ Manufacturing Output Generation
