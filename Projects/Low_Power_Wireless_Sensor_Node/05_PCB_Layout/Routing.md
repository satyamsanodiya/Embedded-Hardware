# PCB Layout & Routing

## Overview

The PCB layout was developed to implement the low-power wireless sensor node architecture while maintaining compact dimensions, reliable power delivery, and clean signal routing.

The final board size was optimized to accommodate the PMIC, BM15M BLE module, sensor interfaces, programming header, USB Type-C connector, RGB LED indicators, and expansion interfaces while keeping routing complexity manageable.

The layout process focused on:

- Compact component placement
- Short signal paths
- Reliable power distribution
- Good grounding practices
- Ease of assembly and debugging
- Manufacturability

---

# Board Dimensions

## Objective

Minimize PCB area while preserving routing accessibility and connector usability.

## Implementation

The board dimensions were selected to balance:

- Mechanical compactness
- Sensor interface accessibility
- Battery-powered operation requirements
- Manufacturing feasibility

The resulting layout provides sufficient routing space while maintaining a compact footprint suitable for portable embedded applications.

---

# Component Placement Strategy

## PMIC Placement

The PMIC was positioned near the USB Type-C connector and battery interface.

### Reason

The PMIC acts as the central power-management device.

Placing it close to power-entry components:

- Reduces power path resistance
- Minimizes voltage drops
- Simplifies power routing
- Improves overall power integrity

---

## BM15M Placement

The BM15M BLE module was positioned to simplify connections to:

- Sensor interfaces
- RGB LEDs
- Programming header
- Expansion connectors

### Reason

The BM15M acts as the primary processing and communication element.

Placing the module centrally reduces:

- Routing congestion
- Signal path length
- Crosstalk between signals

---

## USB Type-C Placement

The USB Type-C connector was positioned near the board edge.

### Reason

This placement provides:

- Easy external access
- Cleaner mechanical integration
- Short routing distance to the PMIC

It also simplifies enclosure design in future product iterations.

---

## Programming Header Placement

The programming header was placed along the board boundary.

### Reason

This provides:

- Easy firmware programming
- Convenient debugging access
- Simplified manufacturing testing

without requiring access to internal PCB regions.

---

# Routing Strategy

## Shortest Practical Routing

Signal traces were routed using the shortest practical path.

### Benefits

- Lower parasitic capacitance
- Reduced EMI susceptibility
- Improved signal integrity
- Easier debugging

---

## Power Routing

Power traces were prioritized before signal routing.

### Objective

Maintain stable voltage delivery across the board.

### Benefits

- Reduced voltage drop
- Improved regulator stability
- Better system reliability

---

## Grounding Strategy

A continuous ground copper pour was implemented across the PCB.

### Purpose

The ground plane provides:

- Low impedance return paths
- Improved noise performance
- Better EMC behavior
- Enhanced power stability

The ground pour also helps reduce routing complexity.

---

# Trace Geometry Considerations

## Avoidance of Unnecessary Sharp Corners

Routing was performed using smooth trace transitions rather than unnecessary 90° bends.

### Reason

Although modern PCB fabrication can support 90° corners, smoother routing provides:

- Better visual inspection
- Improved manufacturing consistency
- Reduced acid-trap concerns
- Cleaner signal routing appearance

This practice follows common industry PCB layout guidelines.

---

## Routing Organization

Signal routing was organized according to functional blocks.

Examples:

- Power routing grouped together
- Sensor signals routed within sensor regions
- Programming signals routed near the debug connector

This improves design readability and future maintenance.

---

# Sensor Interface Routing

Sensor connections were routed toward the expansion side of the board.

### Benefits

- Easier external integration
- Cleaner signal separation
- Future sensor flexibility

The architecture allows different sensor combinations without redesigning the entire platform.

---

# BLE Design Considerations

Special consideration was given to the BM15M BLE module placement.

### Objectives

- Maintain reliable wireless communication
- Reduce interference from power circuitry
- Simplify RF-related layout requirements

The BLE section was kept logically separated from higher-current power routing wherever possible.

---

# Manufacturability Considerations

The PCB was designed with manufacturing and assembly in mind.

Measures included:

- Adequate component spacing
- Accessible programming connector
- Simplified assembly flow
- Clear routing organization

These decisions reduce assembly difficulty and improve serviceability.

---

# Design Verification

Before manufacturing, the PCB was verified through multiple checks.

## Electrical Verification

- Net connectivity review
- Schematic-to-PCB consistency verification
- Power rail verification

## Layout Verification

- Design Rule Check (DRC)
- Clearance verification
- Copper pour verification
- Routing review

## Mechanical Verification

- Connector accessibility
- Mounting hole placement
- Board outline verification

---

# Engineering Lessons Learned

During PCB implementation, several important layout concepts were reinforced:

- Component placement determines routing quality.
- Power routing should be planned before signal routing.
- Ground planes significantly improve return-current management.
- Compact layouts require careful placement planning.
- Early DRC verification prevents costly redesigns.

---

# Final Outcome

The completed PCB successfully integrates:

- USB Type-C power input
- Battery charging and management
- BM15M BLE module
- Sensor expansion interfaces
- RGB status indication
- Programming interface

within a compact and manufacturable embedded hardware platform.

The project provided practical experience in component placement, power distribution, grounding strategy, routing optimization, and PCB design verification using KiCad.
