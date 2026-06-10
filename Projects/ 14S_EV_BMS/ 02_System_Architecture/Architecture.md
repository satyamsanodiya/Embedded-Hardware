# System Architecture and Design Decisions

## Overview

The objective of this project is to design a centralized Battery Management System (BMS) for a 14-series lithium-ion battery pack intended for electric vehicle applications.

Target specifications:

* 14S Li-Ion Battery Pack
* Nominal Voltage: 50.4V
* Maximum Voltage: 58.8V
* Continuous Current: 60A
* CAN-Based Communication
* High-Side Charge/Discharge Control

---

# Analog Front End Selection

## Selected Device

Texas Instruments BQ76940

## Reason for Selection

The BQ76940 was selected as the primary Analog Front End (AFE) because it supports battery packs ranging from 3 to 15 series-connected lithium-ion cells, making it suitable for the 14S architecture used in this project.

Additional advantages include:

* Integrated cell voltage monitoring
* Cell balancing support
* Protection monitoring
* I²C communication interface
* Internal low-dropout regulator (REGOUT)

The integrated regulator output is used to power the low-power section of the system, allowing the microcontroller to remain active while the main system power stage is disabled.

This architecture enables low-power standby operation and allows the MCU to control the system wake-up sequence through the external buck converter.

---

# Microcontroller Selection

## Selected Device

STM32 32-bit Microcontroller

## Reason for Selection

The STM32 family was selected due to its low cost, wide industry adoption, and availability of integrated communication peripherals.

Key requirements satisfied:

* Native CAN controller support
* I²C communication with the BQ76940
* Low-power operating modes
* Sufficient GPIO resources
* Extensive development ecosystem

The MCU performs:

* Cell monitoring management
* Protection decision making
* CAN communication handling
* Charge and discharge control
* System diagnostics and fault reporting

---

# CAN Communication Architecture

## Reason for CAN Implementation

The Battery Management System is intended for electric vehicle applications where reliable communication between the battery pack, charger, motor controller, and vehicle control unit is critical.

CAN was selected because it provides:

* High noise immunity
* Differential signaling
* Multi-node communication capability
* Built-in error detection
* Robust operation in electrically noisy environments

Compared to UART-based communication, CAN offers significantly greater reliability in automotive and high-current power systems.

The CAN interface will be used for:

* Charger communication
* Battery status reporting
* Fault reporting
* Future vehicle network integration

---

# High-Side Switching Architecture

## Design Choice

High-side charge and discharge control.

## Reason for High-Side Switching

High-side switching was selected to improve system safety and fault isolation capability.

By disconnecting the positive battery terminal, the load side remains isolated from the battery pack during fault conditions.

Advantages include:

* Improved fault protection
* Better system isolation
* Reduced risk during maintenance
* Common automotive industry practice
* Safer charger and load disconnection

The BMS controls dedicated charge and discharge MOSFETs through a gate-driver stage, allowing the battery pack to be disconnected during:

* Over-current conditions
* Short-circuit events
* Over-voltage events
* Under-voltage events
* Thermal faults

---

# Current Measurement Strategy

Pack current measurement is implemented using a low-resistance shunt resistor.

Measured current data is used for:

* Over-current protection
* Short-circuit detection
* Battery diagnostics
* Future SOC estimation development

---

# Power Supply Architecture

The battery pack voltage is converted through a buck converter to generate the system supply rails.

The low-power MCU domain can remain powered through the BQ76940 regulator output, enabling standby monitoring while minimizing overall power consumption.

This architecture supports low quiescent current operation and improves battery storage life during idle conditions.

---

# Design Goals

The architecture was developed with the following objectives:

* Low cost
* High reliability
* Automotive-oriented communication
* Safe fault handling
* Low standby power consumption
* Scalable firmware development
* Ease of future feature expansion
 
