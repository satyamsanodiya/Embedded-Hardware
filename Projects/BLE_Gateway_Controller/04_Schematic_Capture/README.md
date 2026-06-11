# Schematic Capture

## Overview

The schematic was developed using a modular block-based design approach to simplify verification, debugging, PCB layout, and future maintenance.

Each functional block performs a dedicated task while communicating through clearly defined interfaces.

The final design integrates power management, wireless communication, industrial communication, Linux-based processing, and local data storage into a single hardware platform.

---

# System Signal Flow

# USB Type-C (5V Supply)

## Function

Acts as the primary power input of the system.

The USB Type-C interface provides:

* External power connection
* Standardized power source
* Easy deployment and testing

## Output

* 5V Power Rail

This rail is distributed to the remaining system blocks.

---

# Voltage Regulator (5V → 3.3V)

## Function

Generates the regulated 3.3V supply required by low-voltage digital devices.

## Powered Blocks

* BM15M (BLE)
* ESP32 With Bluetooth Module
* Logic Interfaces

## Design Objective

Provide stable and low-noise power to communication and processing circuits.

---

# BM15M (BLE)

## Function

Provides Bluetooth Low Energy communication capability.

## Interfaces

### UART to ESP32

Used for:

* BLE data transfer
* Command exchange
* Real-time communication

### UART to Raspberry Pi Zero 2W

Used for:

* Linux-based BLE applications
* Direct access to BLE data
* Software development and testing

### RGB LED Interface

Provides:

* Connection indication
* Communication status
* Fault indication

---

# ESP32 With Bluetooth Module

## Function

Acts as the embedded communication controller.

## Interfaces

### UART to BM15M

Used for BLE communication handling.

### UART to Raspberry Pi Zero 2W

Used for:

* Data exchange
* Logging support
* Application integration

### SPI to SD Card

Used for:

* Data storage
* Event logging
* Debug data recording

### UART to RS485

Used for industrial communication.

## Responsibilities

* Communication management
* Data routing
* Peripheral handling
* Local processing

---

# Raspberry Pi Zero 2W

## Function

Provides Linux-based edge computing capability.

## Interfaces

### UART to BM15M

Provides direct access to BLE communication.

### UART to ESP32

Provides communication with the embedded subsystem.

### UART to RS485

Provides access to industrial communication from Linux applications.

## Responsibilities

* Data logging
* Application execution
* Protocol conversion
* Future cloud integration

---

# SD Card

## Function

Provides local non-volatile storage.

## Interface

SPI

## Applications

* Data logging
* Event recording
* System diagnostics
* Future configuration storage

---

# RS485

## Function

Provides industrial communication capability.

## Connected Controllers

* ESP32 With Bluetooth Module
* Raspberry Pi Zero 2W

## Communication Benefits

* Long-distance communication
* Noise immunity
* Differential signalling
* Industrial compatibility

The dual-controller access allows the interface to be managed by either the embedded firmware layer or Linux-based applications.

---

# RGB LED

## Function

Provides visual feedback of system status.

## Indications

* Power status
* BLE connection status
* Communication activity
* Fault conditions

This simplifies debugging and field diagnostics.

---

# Design Verification

The following checks were performed during schematic development:

* Power rail connectivity review
* UART signal verification
* SPI interface verification
* RS485 communication path review
* Component footprint verification
* Electrical Rules Check (ERC)

---

# Design Outcome

The schematic successfully integrates wireless communication, industrial networking, local storage, and Linux-based edge processing into a single platform.

The modular architecture provides flexibility for multiple deployment scenarios including standalone embedded operation, Linux gateway operation, and hybrid processing applications.
