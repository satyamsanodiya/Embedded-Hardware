# Schematic Capture

## Overview

The schematic was developed to implement the low-power wireless sensor node architecture while maintaining modularity, expandability, and ease of debugging.

The design integrates power management, battery charging, wireless communication, sensor interfaces, local user indication, and expansion capabilities into a single hardware platform.

The schematic is organized into functional blocks to simplify design review, PCB implementation, and future modifications.

---

# Power Management Block

## Objective

Provide stable power distribution for battery-operated and USB-powered operation.

## Implementation

The power subsystem is built around the nPM1300 Power Management IC (PMIC).

The PMIC manages:

* Li-Ion battery charging
* USB Type-C power input
* Power-path management
* System power generation

The PMIC serves as the central power-management element of the design.

---

# USB Type-C Interface

## Objective

Provide a standardized power input and battery charging interface.

## Implementation

The USB Type-C connector allows:

* Battery charging
* Direct system operation from USB
* Development and testing without battery connection

The connector is routed directly to the PMIC charging subsystem.

---

# Battery Interface

## Objective

Support rechargeable Li-Ion battery operation.

## Implementation

A dedicated battery connector is provided for single-cell Li-Ion battery integration.

The battery is managed by the nPM1300 charging circuitry.

Benefits:

* Portable operation
* Rechargeability
* Simplified power architecture

---

# BM15M BLE Module

## Objective

Provide wireless communication and local processing capability.

## Implementation

The BM15M acts as the central controller of the system.

Functions include:

* Sensor communication
* BLE communication
* RGB LED control
* Display control
* Expansion interface management

The BM15M forms the core processing element of the platform.

---

# Sensor Expansion Interfaces

## Objective

Allow integration of multiple environmental sensing modules.

## Implementation

Instead of permanently mounting all sensors on the PCB, dedicated interfaces were provided.

Supported sensor categories:

* Temperature and Humidity Sensors
* CO2 Sensors
* Flow Sensors
* PIR Sensors

This approach allows flexibility during development and future sensor upgrades.

---

# External I2C Interface

## Objective

Enable future expansion without PCB redesign.

## Implementation

A dedicated I2C expansion connector is provided.

This interface allows integration of:

* Environmental sensors
* Pressure sensors
* Motion sensors
* Custom expansion boards

The expansion architecture increases the long-term usability of the hardware platform.

---

# SPI Display Interface

## Objective

Provide local visualization capability.

## Implementation

A dedicated SPI interface is available for connecting a compact color display.

Potential applications include:

* Sensor visualization
* Battery information display
* Debug information
* Device configuration

The display remains optional and can be added depending on application requirements.

---

# RGB LED Interface

## Objective

Provide immediate visual feedback.

## Implementation

The RGB LED is connected directly to the BM15M.

Possible indications include:

* Device power status
* BLE connection status
* Sensor activity
* Error conditions

This simplifies debugging and improves user interaction.

---

# Communication Architecture

## BLE Communication

Wireless communication is handled by the BM15M BLE module.

The BLE interface enables:

* Sensor data transmission
* Remote monitoring
* Wireless configuration

## Local Communication

Internal communication is implemented through standard digital interfaces including:

* I2C
* SPI
* GPIO

This architecture simplifies integration of additional peripherals.

---

# Design Verification

The schematic underwent multiple design reviews before PCB implementation.

Verification activities included:

* Power rail validation
* Connector verification
* Interface verification
* Sensor connectivity review
* PMIC integration review
* ERC (Electrical Rule Check)

---

# Engineering Considerations

Several design decisions were made to support low-power operation:

* Battery-first architecture
* Integrated PMIC solution
* BLE communication
* Modular sensor interfaces
* Expandable I2C connectivity

These decisions improve system flexibility while maintaining a compact design.

---

# Design Outcome

The completed schematic successfully integrates power management, wireless communication, user interfaces, and sensor expansion capability into a unified hardware platform.

The modular structure provides a strong foundation for future firmware development and additional sensor integration.
