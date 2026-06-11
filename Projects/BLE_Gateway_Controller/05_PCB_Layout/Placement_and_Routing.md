# PCB Placement and Routing

## Overview

After schematic completion, component placement and routing were performed with the objective of minimizing routing complexity, improving communication reliability, and simplifying future debugging.

The PCB integrates wireless communication, industrial communication, Linux processing, and local storage into a compact hardware platform.

---

# Functional Block Placement

The PCB was divided into dedicated functional regions.

## Power Section

The USB Type-C input and voltage regulation circuitry were placed together to simplify power distribution and reduce power trace lengths.

---

## BM15M (BLE)

The BM15M module was placed away from power conversion circuitry and high-current traces.

Objectives:

* Reduce EMI exposure
* Improve RF performance
* Improve BLE communication reliability

Special attention was given to the antenna region to avoid signal interference.

---

## ESP32 With Bluetooth Module

The ESP32 was positioned centrally because it communicates with multiple subsystems:

* BM15M
* Raspberry Pi Zero 2W
* RS485
* SD Card

This placement minimized overall routing complexity.

---

## Raspberry Pi Zero 2W

The Raspberry Pi interface was placed near the board edge.

Benefits:

* Easy module installation
* Easy maintenance
* Simplified access to GPIO interfaces

---

## RS485 Interface

The RS485 circuitry was placed close to the communication connector.

Benefits:

* Short communication paths
* Reduced noise pickup
* Simplified field wiring

---

## SD Card Interface

The SD Card interface was placed near the ESP32 to reduce SPI routing length and improve signal integrity.

---

# Routing Strategy

The routing process followed the following priority:

1. Power Distribution
2. Ground Network
3. Communication Interfaces
4. Control Signals

---

## Power Routing

Power traces were routed first to establish reliable power distribution.

Dedicated routing paths were used for:

* 5V Rail
* 3.3V Rail

---

## Ground Routing

A continuous ground reference was maintained throughout the design wherever possible.

Objectives:

* Improve signal return paths
* Reduce electrical noise
* Improve communication reliability

---

## Communication Routing

The following communication interfaces were routed:

* UART
* SPI
* RS485

Special attention was given to minimizing unnecessary vias and excessive trace lengths.

---

# Design Outcome

The final PCB successfully integrates all required communication and processing subsystems while maintaining clear routing structure and functional separation between major hardware blocks.
