# System Architecture

## Overview

The BLE Gateway Controller is designed as a multi-processor communication platform that combines Bluetooth Low Energy (BLE), Wi-Fi capable embedded processing, industrial RS485 communication, local storage, and Linux-based edge computing.

The architecture uses dedicated processing devices for specific tasks to improve modularity, maintainability, and future scalability.

The system consists of three primary processing units:

* BM15M BLE Module
* ESP32 Microcontroller
* Raspberry Pi Zero 2W

All communication between processing units is performed through UART interfaces.

---
# Design Flexibility and Communication Redundancy

The system was intentionally designed with multiple communication paths between processing units and communication interfaces.

Instead of creating a single-point communication architecture, both the BM15M BLE module and RS485 interface can be accessed by either the ESP32 or Raspberry Pi Zero 2W depending on application requirements.

## BM15M Connection Strategy

The BM15M BLE module is connected to both the ESP32 and Raspberry Pi.

### ESP32 Access

The ESP32 can directly communicate with the BM15M for:

* Real-time BLE communication
* Low-latency data acquisition
* Embedded control applications
* Power-efficient operation

This allows the system to operate without requiring the Raspberry Pi to be powered continuously.

### Raspberry Pi Access

The Raspberry Pi can also communicate directly with the BM15M for:

* Linux-based BLE applications
* Python development
* Advanced BLE data processing
* Future cloud integration
* Rapid software prototyping

This approach eliminates the need for BLE data to always pass through the ESP32 before reaching Linux applications.

---

## RS485 Connection Strategy

The RS485 interface is accessible from both the ESP32 and Raspberry Pi.

### ESP32 Access

The ESP32 can control RS485 communication for:

* Real-time industrial communication
* Deterministic timing requirements
* Protocol implementation at firmware level
* Low-power standalone operation

This mode is suitable for field deployments where Linux processing is unnecessary.

### Raspberry Pi Access

The Raspberry Pi can access RS485 communication for:

* Industrial data logging
* Protocol analysis
* Gateway applications
* SCADA integration
* Modbus software development
* Cloud-connected industrial monitoring

This enables development of high-level applications without modifying firmware.

---

## System Operation Modes

### Mode 1 – Embedded Controller Mode

BM15M → ESP32 → RS485

In this mode, the ESP32 handles all communication and the Raspberry Pi is not required.

Advantages:

* Lower power consumption
* Faster boot time
* Real-time operation

---

### Mode 2 – Linux Gateway Mode

BM15M → Raspberry Pi

RS485 → Raspberry Pi

In this mode, the Raspberry Pi performs data processing, logging, protocol conversion, and network communication.

Advantages:

* Advanced software capabilities
* Easier application development
* Cloud connectivity

---

### Mode 3 – Hybrid Mode

BM15M ↔ ESP32 ↔ Raspberry Pi ↔ RS485

In this mode, each subsystem performs its dedicated task.

* ESP32 handles real-time communication.
* Raspberry Pi handles application-level processing.
* BM15M provides wireless connectivity.
* RS485 provides industrial communication.

This mode offers maximum system flexibility and scalability.

---

## Engineering Rationale

The architecture was designed to avoid dependency on a single processing unit.

By providing communication access to both ESP32 and Raspberry Pi, the platform can support:

* Standalone embedded operation
* Linux-based gateway operation
* Future software expansion
* Faster development and debugging
* Multiple deployment scenarios

without requiring hardware redesign.


# Power Architecture

The system is powered through a USB Type-C connector.

A USB Power Delivery controller generates a regulated 5V rail which acts as the primary system power source.

The 5V rail is distributed to:

* Raspberry Pi Zero 2W
* 3.3V DC-DC Converter

The DC-DC converter generates the 3.3V rail required by the BM15M BLE module and ESP32 controller.

This architecture separates high-current and low-voltage domains while maintaining a simple power distribution network.

---

# BM15M BLE Module

The BM15M module acts as the wireless communication front-end of the system.

### Responsibilities

* Bluetooth Low Energy communication
* Wireless device pairing
* Data reception from BLE devices
* Data transmission to BLE devices

### Interfaces

| Interface | Connection           |
| --------- | -------------------- |
| UART      | ESP32                |
| UART      | Raspberry Pi Zero 2W |
| GPIO      | RGB Status LEDs      |

The BM15M provides wireless connectivity while offloading BLE protocol handling from the remaining system.

---

# ESP32 Controller

The ESP32 acts as the communication management controller.

### Responsibilities

* BLE data processing
* UART communication management
* RS485 communication handling
* SD Card management
* Data routing between subsystems

### Interfaces

| Interface | Connection           |
| --------- | -------------------- |
| UART      | BM15M                |
| UART      | Raspberry Pi Zero 2W |
| SPI       | SD Card              |
| UART      | RS485 Interface      |

The ESP32 serves as the bridge between wireless communication, industrial communication, and local storage.

---

# Raspberry Pi Zero 2W

The Raspberry Pi Zero 2W provides Linux-based processing capability.

### Responsibilities

* Application layer execution
* Data logging
* Local processing
* Future cloud connectivity
* Edge computing applications

### Interfaces

| Interface | Connection |
| --------- | ---------- |
| UART      | BM15M      |
| UART      | ESP32      |

The Raspberry Pi allows complex software applications to be executed without increasing the firmware complexity of the ESP32.

---

# SD Card Storage

The SD Card is connected to the ESP32 through an SPI interface.

### Functions

* Data logging
* Event recording
* Debug information storage
* Future configuration storage

The storage subsystem allows persistent data retention independent of the Raspberry Pi.

---

# RS485 Interface

The RS485 block provides industrial communication capability.

### Functions

* Long-distance communication
* Noise-resistant communication
* Industrial equipment interfacing

The RS485 interface enables integration with industrial controllers and field devices.

---

# RGB Status Indication

RGB LEDs are connected to the BM15M module.

### Status Indications

* Power Status
* BLE Connection Status
* Communication Activity
* Fault Conditions

Visual indication simplifies debugging and field diagnostics.

---

# Communication Flow

### BLE Device → BM15M → ESP32

Wireless sensor data is received through BLE and forwarded to the ESP32 for processing.

### ESP32 → SD Card

Processed data can be stored locally for logging purposes.

### ESP32 → RS485

Data can be transmitted to industrial equipment through the RS485 network.

### ESP32 ↔ Raspberry Pi

The Raspberry Pi can exchange information with the ESP32 for advanced processing, visualization, and future cloud integration.

### BM15M ↔ Raspberry Pi

Direct UART communication is available for Linux applications that require direct access to BLE data.

---

# Design Philosophy

The architecture separates communication, processing, storage, and Linux application layers into dedicated functional blocks.

This modular design provides:

* Easier debugging
* Simplified firmware development
* Better scalability
* Improved maintainability
* Future expansion capability

while keeping the hardware architecture simple and cost-effective.
