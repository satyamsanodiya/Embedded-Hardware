# System Architecture

## Overview

The Low Power Wireless Sensor Node is designed around a BLE-enabled processing module, intelligent power management subsystem, and multiple environmental sensors.

The architecture was developed with the following objectives:

- Low power operation
- Battery-powered deployment
- Wireless communication
- Modular sensor integration
- Future expandability
- Compact PCB implementation

The system is powered through either a rechargeable Li-Ion battery or USB Type-C input and uses the nPM1300 PMIC for power management and battery charging.

---

# System Block Diagram

USB Type-C
        │
        ▼
    nPM1300
        │
    1.8V Rail
        │
        ▼
      BM15M
        │
 ┌──────┼──────┐
 ▼      ▼      ▼
Sensors RGB   Display
        │
        ▼
 External I2C Expansion

---

# Power Architecture

## nPM1300 PMIC

The nPM1300 was selected as the primary Power Management IC (PMIC).

### Reasons for Selection

### Battery Charging Support

The device integrates a complete battery charging solution for single-cell Li-Ion batteries.

This eliminates the need for a dedicated charger IC and reduces overall BOM cost.

### USB Type-C Compatibility

The PMIC supports USB-powered operation and battery charging through a USB Type-C connector.

This allows the device to operate even when no battery is connected.

### Integrated Power Path Management

The PMIC automatically manages power distribution between:

- USB Input
- Battery Source
- System Load

This provides seamless transition between power sources.

### Integrated Regulators

The PMIC contains internal regulators capable of generating stable supply rails for low-power electronics.

This significantly simplifies the power architecture.

### Low Power Operation

The PMIC is specifically designed for battery-operated wireless products.

Low quiescent current improves battery life and makes it suitable for long-duration sensing applications.

---

# Why a 1.8V System Rail?

The primary system voltage was selected as 1.8V.

### Reduced Power Consumption

Power consumption is proportional to:

P = V × I

Reducing operating voltage directly reduces overall power consumption.

For battery-operated products, lowering the system voltage significantly improves battery life.

### Native BM15M Support

The BM15M BLE module supports operation at 1.8V.

Operating the processor at its native voltage avoids unnecessary power conversion losses.

### Simplified Power Tree

Using a common low-voltage rail reduces the number of regulators required in the design.

---

# BM15M BLE Module

The BM15M module serves as the primary processing and wireless communication unit.

### Responsibilities

- Sensor data acquisition
- BLE communication
- Power management control
- User interface control
- RGB LED control

### Why BM15M?

### Integrated BLE Stack

The module provides built-in Bluetooth Low Energy functionality.

This eliminates the need for an external wireless chipset.

### Compact Design

Using a pre-certified BLE module reduces PCB complexity and development time.

### Low Power Consumption

The module is optimized for battery-powered IoT applications.

### Sufficient GPIO Resources

The module provides enough GPIOs for:

- Sensor interfacing
- Display control
- LED control
- External expansion

---

# Future Sensor Power Management Provision

Not all sensors require continuous operation.

Several sensors are only needed periodically.

Examples:

- CO2 Sensor
- Air Flow Sensor
- PIR Sensor
- Display

Keeping these devices powered continuously would increase battery consumption.

To solve this problem, dedicated power switches were introduced.

---

## Why Power Switches?

The switches allow the BM15M to selectively enable or disable sensor power.

### Benefits

### Reduced Average Current Consumption

Sensors consume power only when measurements are required.

### Extended Battery Life

Duty-cycled sensor operation significantly increases operating duration.

### Thermal Improvement

Lower average power consumption reduces heat generation.

### Flexible Sensor Management

Different sensors can be activated independently depending on system requirements.

---

# Sensor Interface Voltage Compatibility

The core system operates at 1.8V.

However, several external sensors may require:

- 3.3V
- 5V

operation.

Direct connection is not always possible.

---

## Level Shifter Requirement

When a sensor operates at a higher voltage than the BM15M I/O voltage, a level shifter must be used.

Example:

BM15M GPIO = 1.8V

Sensor Interface = 3.3V

Without level translation:

- Logic level mismatch may occur
- Communication reliability decreases
- BM15M GPIO damage may occur

---

## Typical Applications

### I2C Translation

1.8V ↔ 3.3V

Used when connecting:

- CO2 Sensors
- External Expansion Sensors

### SPI Translation

1.8V ↔ 3.3V

Used when connecting:

- Display Modules
- External Sensor Boards

### GPIO Translation

1.8V ↔ 3.3V

Used for:

- Interrupt Lines
- Control Signals

---

# RGB LED Subsystem

An RGB LED is directly connected to the BM15M module.

### Purpose

Provides immediate visual feedback regarding system status.

### Example Indications

Green:
- Device operating normally

Blue:
- BLE advertising

Yellow:
- Sensor measurement active

Red:
- Fault condition

### Why Directly Connected?

The RGB LED is frequently used and requires fast response.

Direct GPIO control simplifies firmware implementation and minimizes hardware complexity.

---

# External I2C Expansion Interface

An external I2C connector is provided.

### Purpose

Allows future sensor expansion without redesigning the PCB.

### Benefits

- Rapid prototyping
- Sensor evaluation
- Future hardware upgrades
- Debugging support

### Supported Devices

Examples include:

- Environmental sensors
- Pressure sensors
- Accelerometers
- Light sensors
- Gas sensors

---

# Design Philosophy

The architecture follows a low-power modular design approach.

Key design principles include:

- Battery-first operation
- Intelligent power management
- Wireless connectivity
- Modular sensor integration
- Expandability
- Reduced BOM complexity

This architecture provides a scalable foundation for future wireless sensing applications while maintaining low power consumption and compact PCB implementation.
