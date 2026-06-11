# BLE Gateway Controller

## Project Overview

This project is a custom embedded hardware platform designed to bridge wireless BLE communication, industrial RS485 networks, and Linux-based edge computing systems.

The hardware combines a Bluetooth Low Energy module, ESP32 wireless controller, Raspberry Pi Zero 2W, USB Type-C power input, and RS485 communication interface into a single integrated platform.

The primary goal of the design is to provide a communication gateway capable of collecting wireless sensor data, performing local processing, and forwarding information to industrial communication networks.

---

## Project Objectives

- Develop a compact communication gateway PCB.
- Support Bluetooth Low Energy connectivity.
- Support industrial RS485 communication.
- Provide Linux-based edge processing capability.
- Enable future cloud and IoT integration.
- Implement reliable UART-based communication between subsystems.
- Create a manufacturable PCB suitable for prototype production.

---

## System Architecture

The system consists of the following major blocks:

- USB Type-C Power Input
- Power Regulation Circuit
- BM15M BLE Module
- ESP32 Controller
- Raspberry Pi Zero 2W
- RS485 Communication Interface
- RGB Status Indicator
- SD Card Storage

---

## Design Flow

1. Requirement Analysis
2. System Architecture
3. Component Selection
4. Schematic Capture
5. PCB Layout
6. Design Verification
7. Hardware Testing

---

## Repository Structure

```text
BLE_Gateway_Controller/

├── 01_Project_Requirements/
├── 02_System_Architecture/
├── 03_Component_Selection/
├── 04_Schematic_Capture/
├── 05_PCB_Layout/
├── 06_Design_Verification/
├── 07_Testing/
├── 08_Lessons_Learned/
└── Images/
