
# Project Requirements

## Purpose

Develop an embedded communication gateway capable of bridging Bluetooth Low Energy devices, industrial RS485 networks, and Linux-based edge processing systems.

The system should support wireless communication, local processing, industrial connectivity, and future IoT expansion.

---

# Functional Requirements

## FR-01: BLE Communication

The system shall support Bluetooth Low Energy communication using the BM15M module.

### Objective

Allow wireless communication with nearby BLE-enabled devices.

---

## FR-02: Embedded Controller

The system shall include an ESP32 microcontroller.

### Objective

- Process communication data.
- Manage peripheral interfaces.
- Handle UART communication between modules.

---

## FR-03: Linux Edge Processing

The system shall include Raspberry Pi Zero 2W support.

### Objective

- Execute Linux-based applications.
- Enable edge computing.
- Support future cloud integration.
- Provide local data processing capability.

---

## FR-04: Industrial Communication

The system shall support RS485 communication.

### Objective

- Long-distance communication.
- Industrial device connectivity.
- Improved noise immunity.

---

## FR-05: Local Storage

The system shall support external SD Card storage.

### Objective

- Data logging.
- Event recording.
- Future firmware storage capability.

---

## FR-06: Status Indication

The system shall provide RGB LED indication.

### Objective

Display:

- Power status
- Communication status
- Fault status
- System activity

---

## FR-07: Power Input

The system shall operate from a USB Type-C power source.

### Objective

Provide standardized power delivery and easy deployment.

---

## FR-08: Internal Communication

The system shall use UART communication between major subsystems.

### Interfaces

| Interface | Protocol |
|------------|-----------|
| BM15M ↔ ESP32 | UART |
| BM15M ↔ Raspberry Pi | UART |
| ESP32 ↔ Raspberry Pi | UART |

---

# Power Requirements

## Input Voltage

5V USB Type-C Supply

## Regulated Output

3.3V Rail

### Powered Devices

- BM15M
- ESP32
- Logic Interfaces

---

# Design Constraints

## Cost

The design should prioritize commercially available and cost-effective components.

## Manufacturability

The PCB should be suitable for standard PCB fabrication processes.

## Reliability

The design should maintain stable communication under normal operating conditions.

## Scalability

The architecture should allow future software and hardware expansion.

---

# Expected Deliverables

- System Architecture
- Component Selection Report
- Schematic Design
- PCB Layout
- Design Verification Report
- Hardware Bring-Up Documentation
