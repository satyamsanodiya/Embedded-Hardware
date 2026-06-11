# Component Selection

## Design Philosophy

Component selection was performed based on the following criteria:

* Functional requirements
* Availability
* Cost effectiveness
* Ease of development
* Community support
* Future scalability
* Industrial applicability

The goal was to create a flexible communication gateway capable of wireless communication, Linux-based edge processing, industrial networking, and local data storage.

---

# USB Type-C (5V Supply)

## Purpose

Provides the primary power source for the entire system.

## Selection Criteria

* Industry standard connector
* Reversible connection
* Wide adapter availability
* Reliable current delivery
* Easy deployment during development and testing

## Benefits

* Simplified power distribution
* Improved user experience
* Future compatibility

---

# Voltage Regulator (5V → 3.3V)

## Purpose

Generates the regulated 3.3V rail required by low-voltage digital devices.

## Powered Devices

* BM15M BLE Module
* ESP32 With Bluetooth Module
* Supporting logic circuitry

## Selection Criteria

* Stable output voltage
* Low output ripple
* Good efficiency
* Availability

## Benefits

* Reliable operation of digital devices
* Improved system stability
* Reduced noise sensitivity

---

# BM15M (BLE)

## Purpose

Provides Bluetooth Low Energy communication capability.

## Selection Criteria

* BLE support
* UART communication interface
* Low power operation
* Simple integration
* Compact module design

## Responsibilities

* BLE device pairing
* Wireless communication
* Data transmission
* Data reception

## Architectural Role

The BM15M acts as the wireless communication front-end of the system.

It can communicate with both:

* ESP32 With Bluetooth Module
* Raspberry Pi Zero 2W

This provides flexibility for embedded and Linux-based applications.

---

# ESP32 With Bluetooth Module

## Purpose

Acts as the primary embedded controller and communication manager.

## Selection Criteria

* Low cost
* High performance
* Large community support
* Multiple UART interfaces
* SPI support
* Integrated wireless capability

## Responsibilities

* Communication management
* Data routing
* SD Card handling
* RS485 communication
* Peripheral control

## Architectural Role

The ESP32 is responsible for real-time communication tasks and can operate independently without requiring Linux-based processing.

This allows the system to function as a standalone embedded controller when necessary.

---

# Raspberry Pi Zero 2W

## Purpose

Provides Linux-based processing capability.

## Selection Criteria

* Linux operating system support
* Python development environment
* Large developer ecosystem
* Edge computing capability
* Networking support

## Responsibilities

* Data processing
* Application execution
* Data logging
* Future cloud integration
* Gateway functionality

## Architectural Role

The Raspberry Pi enables development of high-level software applications without increasing firmware complexity on the ESP32.

---

# RS485

## Purpose

Provides industrial communication capability.

## Selection Criteria

* Industry-standard communication protocol
* Long-distance communication support
* Noise immunity
* Differential signalling

## Responsibilities

* Communication with external industrial devices
* Field device integration
* Industrial network connectivity

## Architectural Role

The RS485 interface allows the platform to interact with industrial equipment while maintaining communication reliability in electrically noisy environments.

The interface can be accessed through:

* ESP32 With Bluetooth Module
* Raspberry Pi Zero 2W

depending on application requirements.

---

# Component Selection Summary

| Component                   | Primary Function                   |
| --------------------------- | ---------------------------------- |
| USB Type-C (5V Supply)      | System Power Input                 |
| Voltage Regulator (5V→3.3V) | Low Voltage Power Generation       |
| BM15M (BLE)                 | Bluetooth Low Energy Communication |
| ESP32 With Bluetooth Module | Embedded Control and Communication |
| Raspberry Pi Zero 2W        | Linux-Based Processing             |
| RS485                       | Industrial Communication           |
| SD Card                     | Local Data Storage                 |

---

# Design Outcome

The selected components provide a balance between:

* Performance
* Cost
* Flexibility
* Expandability
* Ease of development

while supporting both embedded firmware development and Linux-based application development within a single hardware platform.
