# 14S Centralized Battery Management System for Electric Vehicle

## Project Overview

This project focuses on the development of a centralized Battery Management System (BMS) for a 14-series lithium-ion battery pack intended for electric vehicle applications.

The design combines a Texas Instruments battery monitoring Analog Front End (AFE) with a low-cost 32-bit microcontroller and CAN communication interface to provide battery monitoring, protection, and system control.

---

## Design Requirements

### Battery Pack

* Configuration: 14S Lithium-Ion
* Nominal Voltage: 50.4V
* Maximum Pack Voltage: 58.8V
* Continuous Current Rating: 60A

### Functional Requirements

* Individual cell voltage monitoring
* Pack voltage monitoring
* Temperature monitoring
* Cell balancing
* Short-circuit protection
* Over-current protection
* Over-voltage protection
* Under-voltage protection
* High-side charge/discharge control
* CAN-based communication interface

---

## System Architecture

### Analog Front End

* Texas Instruments BQ76940
* Cell voltage acquisition
* Protection monitoring
* Cell balancing control

### Microcontroller

* Low-cost 32-bit MCU
* Battery state monitoring
* Protection management
* CAN communication handling

### Communication

* CAN Bus interface
* Vehicle controller integration

### Power Stage

* High-side MOSFET switching
* 60A continuous current capability

---

## Current Progress

### Completed

* System requirement definition
* Architecture selection
* Component selection
* Schematic capture

### In Progress

* Footprint verification
* Component placement strategy
* PCB routing
* Design rule validation

### Planned

* PCB fabrication
* Hardware bring-up
* Firmware integration
* Protection testing
* CAN communication validation

---

## Engineering Challenges

* High-side switching implementation
* Accurate cell voltage measurement
* 60A current path layout optimization
* CAN interface robustness
* Thermal management
* PCB layout for mixed-signal circuitry

---

## Learning Objectives

* Battery Management Systems
* Analog Front End design
* High-current PCB design
* CAN communication systems
* Power electronics
* Embedded hardware development
* Hardware validation and debugging
