# Low Power Wireless Sensor Node

## Project Overview

This project focuses on the design and implementation of a battery-powered wireless sensor node intended for low-power environmental monitoring applications.

The device is designed around the BM15M BLE module and supports multiple sensor interfaces while maintaining long battery life through intelligent power management.

The design supports operation from either a rechargeable Li-Ion battery or USB Type-C power source.

---

## Project Objectives

- Develop a compact wireless sensing platform.
- Support multiple environmental sensors.
- Enable BLE-based wireless communication.
- Minimize overall power consumption.
- Support rechargeable battery operation.
- Provide future sensor expansion capability.

---

## Key Features

### Power System

- USB Type-C power input
- Rechargeable Li-Ion battery support
- Battery charging and power-path management
- Low-power operation using nPM1300 PMIC

### Wireless Communication

- BM15M BLE Module
- Wireless sensor data transmission
- RGB LED status indication

### Sensor Interfaces

- Temperature and Humidity Sensor
- CO2 Sensor
- Air Flow Sensor
- PIR Motion Sensor

### User Interface

- SPI Display
- RGB Status LED

### Expansion

- External I2C Interface
- Additional GPIO access

---

## Hardware Architecture

USB Type-C and Battery sources are managed by the nPM1300 PMIC.

The PMIC generates regulated system power rails which are distributed to:

- BM15M BLE Module
- Sensor Subsystems
- Display Interface
- RGB Status Indicators

Power switches are used to selectively enable sensors in order to reduce overall energy consumption.

---

## Design Tools

- KiCad 9.0
- Datasheet-Based Design Verification
- PCB Design Rule Checking (DRC)
- Electrical Rule Checking (ERC)

---

## Current Status

✔ Requirements Definition

✔ System Architecture

✔ Component Selection

✔ Schematic Capture

✔ PCB Layout

✔ Routing Complete

✔ Design Verification
