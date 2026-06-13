# Schematic Design

## Overview

The schematic was developed to implement a compact graphical display controller using the ESP32-S3 microcontroller. The design focuses on minimizing GPIO usage, simplifying PCB routing, and providing a scalable architecture for future firmware development.

The system consists of the following major functional blocks:

* ESP32-S3 Controller
* MCP23017 I²C GPIO Expander
* 128×64 Graphical LCD Interface
* LCD Brightness Control Circuit
* Power Supply Section
* Programming Interface
* Keypad Interface
* Decoupling and Signal Integrity Network

---

## ESP32-S3 Controller

The ESP32-S3 serves as the primary processing unit of the system.

Its responsibilities include:

* Graphical LCD control
* Keypad scanning
* User interface management
* I²C communication
* Future communication and application expansion

The ESP32-S3 was selected due to:

* High processing capability
* Large memory resources
* Extensive GPIO support
* Strong software ecosystem
* Cost-effective development platform

A dedicated programming header is provided to support firmware development, debugging, and future software updates.

---

## MCP23017 I²C GPIO Expander

The graphical LCD requires a large number of digital control and data signals.

Directly connecting the LCD to the ESP32 would consume a significant number of GPIO pins and increase routing complexity.

To solve this problem, an MCP23017 I²C GPIO expander was implemented.

The MCP23017 communicates with the ESP32 through the I²C bus and provides sixteen additional programmable GPIO pins.

Benefits of using MCP23017:

* Significant reduction in GPIO utilization
* Simpler PCB routing
* Improved firmware scalability
* Easier future hardware expansion
* Reduced controller pin dependency

Only two ESP32 pins are required for communication:

* SDA
* SCL

This architecture preserves valuable GPIO resources for future features.

---

## Graphical LCD Interface

A 128×64 graphical LCD is used as the primary user interface.

Compared to standard character LCDs, the graphical display provides:

* Bitmap graphics support
* Custom symbols and icons
* Enhanced user experience
* Flexible menu implementation

The display is controlled through the MCP23017 GPIO expander.

The interface includes:

| Signal | Function                           |
| ------ | ---------------------------------- |
| VCC    | LCD Power Supply                   |
| GND    | Ground Reference                   |
| RS     | Command/Data Selection             |
| R/W    | Read/Write Control                 |
| E      | Data Latch Enable                  |
| D0-D7  | Parallel Data Bus                  |
| CS1    | Left Display Controller Selection  |
| CS2    | Right Display Controller Selection |
| RST    | Display Reset                      |
| LED+   | Backlight Supply                   |
| LED-   | Backlight Return                   |

The MCP23017 generates these signals while the ESP32 communicates only through I²C.

This significantly reduces wiring complexity while maintaining full graphical functionality.

---

## Display Firmware Architecture

The hardware architecture was developed to support common graphical display libraries.

The design was evaluated using:

* openGLCD Library
* U8g2 Library

These libraries provide:

* Character rendering
* Bitmap rendering
* Font management
* Menu systems
* Display abstraction layers

Using these libraries reduces firmware development effort and improves maintainability.

---
### Input Power Protection

The board accepts an external 15V DC supply through a dedicated power terminal connector.

A TVS (Transient Voltage Suppressor) diode is placed across the input power rail to protect the system against:

- Electrostatic discharge (ESD)
- Cable-induced transients
- Hot-plugging voltage spikes
- Power supply surge events

Under normal operating conditions the TVS diode remains inactive.

When the input voltage exceeds the device clamping threshold, the TVS rapidly conducts and redirects excess energy to ground, protecting downstream circuitry including the voltage regulators, ESP32-S3, and peripheral devices.

This protection strategy improves overall system robustness and reliability in real-world operating environments.

## LCD Brightness Control Circuit

A dedicated resistor divider network is implemented for graphical LCD brightness control.

Purpose of the circuit:

* Adjust display visibility
* Reduce power consumption
* Prevent excessive backlight current
* Improve display lifetime

The resistor divider generates a controlled voltage level for the display brightness adjustment input.

This approach provides a simple and low-cost brightness control solution without requiring active control circuitry.

---

## Keypad Interface

A dedicated keypad connector is provided for user interaction.

The keypad interface supports:

* Menu navigation
* User selections
* System configuration
* Human-machine interaction

Separating the keypad interface from the display architecture improves firmware modularity and future scalability.

---

## Power Supply Architecture

The system receives power from an external DC source.

The power distribution network supplies:

* ESP32-S3
* MCP23017
* Graphical LCD
* Keypad circuitry

The power stage was designed to provide:

* Stable voltage rails
* Reliable operation
* Low-noise supply distribution

Special attention was given to power routing and decoupling to ensure stable operation during display updates and processor activity.

---

## Decoupling Network

Each integrated circuit includes local decoupling capacitors positioned close to its power pins.

Purpose of decoupling capacitors:

* Suppress high-frequency noise
* Improve power integrity
* Stabilize supply voltage
* Reduce transient voltage drops

Placing capacitors close to the device power pins minimizes parasitic inductance and maximizes filtering effectiveness.

This is a critical practice in professional embedded hardware design.

---

## Programming Interface

A dedicated programming connector is included to support:

* Firmware upload
* Bootloader access
* Debugging
* Manufacturing testing

The programming interface simplifies software development and future maintenance activities.

---

## Connector Placement Strategy

The graphical LCD connector was intentionally placed on the top side of the PCB.

Reasons:

* Improved mechanical integration
* Easier front-panel mounting
* Reduced cable stress
* Simplified enclosure assembly

All remaining components were placed on the bottom layer whenever possible.

This placement strategy:

* Maximizes available display area
* Improves assembly accessibility
* Supports compact product packaging

---

## Design Philosophy

The schematic was developed following the following engineering objectives:

* Minimize GPIO utilization
* Reduce routing complexity
* Improve manufacturability
* Maintain modular architecture
* Support future firmware scalability
* Improve system reliability

The resulting design provides a compact and reusable embedded graphical display platform suitable for future Human-Machine Interface (HMI) applications.
