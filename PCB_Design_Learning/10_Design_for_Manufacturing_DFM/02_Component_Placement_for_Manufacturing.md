# 02 - Component Placement for Manufacturing

# Overview

Component placement is one of the most critical stages of PCB design. Once the schematic is complete, the physical arrangement of components determines routing complexity, manufacturing efficiency, thermal performance, signal integrity, testability, and overall product reliability.

A well-placed PCB often requires shorter traces, fewer vias, improved heat distribution, easier assembly, and simplified debugging.

Unlike schematic design, where only electrical connectivity is considered, PCB placement must satisfy electrical, mechanical, manufacturing, and assembly requirements simultaneously.

This chapter explains professional component placement strategies used in industrial PCB design.

---

# Learning Objectives

After completing this chapter, I understood:

- Importance of component placement
- Functional component grouping
- Signal flow based placement
- Connector placement
- MCU placement
- Polarized component orientation
- Dense placement considerations
- Heat management
- Placement for manufacturability
- Assembly considerations
- Placement review checklist

---

# Why Component Placement is Important

Routing quality is largely determined by placement quality.

Good placement provides:

- Shorter signal paths
- Better signal integrity
- Lower EMI
- Easier routing
- Reduced PCB area
- Better thermal management
- Improved manufacturability
- Easier assembly
- Better debugging accessibility

Poor placement results in:

- Long traces
- Excessive vias
- Congested routing
- Increased EMI
- Difficult assembly
- Higher manufacturing cost

---

# PCB Placement Workflow

Professional placement generally follows this sequence:

```
Board Outline
      │
      ▼
Mounting Holes
      │
      ▼
Connectors
      │
      ▼
Power Supply
      │
      ▼
MCU / Main Processor
      │
      ▼
Communication ICs
      │
      ▼
Analog Circuits
      │
      ▼
Supporting Components
      │
      ▼
Passive Components
```

Large and critical components are placed first, while smaller passive components are placed later.

---

# Functional Component Grouping

Components should be grouped according to their function rather than placed randomly.

Example:

```
+------------------------------------------------+

Power Section

Battery
Protection
Buck Converter
LDO

-----------------------------------------------

Processing Section

STM32
Crystal
Flash Memory

-----------------------------------------------

Communication Section

CAN
USB
UART

-----------------------------------------------

Sensor Section

Temperature Sensor
Pressure Sensor
ADC

+------------------------------------------------+
```

Benefits:

- Cleaner routing
- Easier debugging
- Reduced noise coupling
- Better maintainability

---

# Signal Flow Based Placement

Components should follow the actual flow of signals through the circuit.

Example:

```
Power Input

↓

Protection

↓

Voltage Regulator

↓

MCU

↓

Communication Interface

↓

External Connector
```

Similarly,

```
Sensor

↓

Signal Conditioning

↓

ADC

↓

MCU

↓

Display
```

A signal-flow-based layout minimizes unnecessary routing and improves readability.

---

# Microcontroller (MCU) Placement

The microcontroller is usually the central component of the PCB.

It should be positioned so that:

- Critical interfaces have short routing paths
- Memory devices are nearby
- Clock circuitry is close
- Communication interfaces are easily accessible
- Decoupling capacitors can be placed close to VDD pins

Avoid placing the MCU too close to:

- Switching regulators
- High-current paths
- High-power components

unless recommended by the reference design.

---

# Crystal Oscillator Placement

The crystal should be placed as close as possible to the MCU oscillator pins.

```
Incorrect

Crystal ---------------- MCU

Correct

Crystal ─ MCU
```

Long crystal traces increase susceptibility to noise and may affect oscillator stability.

The crystal layout should follow the MCU manufacturer's recommendations.

---

# Decoupling Capacitor Placement

Each power pin should have its own local decoupling capacitor whenever recommended by the datasheet.

```
VDD

|

Capacitor

|

MCU
```

The capacitor should be located very close to the power pin to minimize loop inductance.

Avoid placing decoupling capacitors on the opposite side of the board unless necessary.

---

# Connector Placement

Connectors define how the PCB interacts with the outside world.

General guidelines:

- Place near board edges
- Ensure mechanical accessibility
- Maintain sufficient clearance for mating connectors and cables
- Consider enclosure constraints
- Keep associated circuitry nearby

Example:

```
Board Edge

USB Connector

CAN Connector

Power Connector
```

---

# Polarized Component Orientation

Polarized components include:

- Electrolytic Capacitors
- Diodes
- LEDs
- ICs
- Connectors
- MOSFETs

Whenever practical, components of the same type should have a consistent orientation.

Example:

```
✔ All IC Pin-1 indicators face the same direction.

✔ Electrolytic capacitor positive terminals point consistently.

✔ Diode cathodes aligned consistently.
```

Benefits:

- Easier assembly
- Reduced placement errors
- Faster inspection
- Simplified maintenance

---

# Dense Component Placement

High component density reduces PCB size but introduces manufacturing challenges.

Potential problems include:

- Difficult soldering
- Limited routing space
- Thermal accumulation
- Inspection difficulty
- Rework challenges

When designing compact boards, maintain adequate spacing according to the PCB manufacturer's assembly guidelines.

---

# Heat Management During Placement

Components that dissipate significant power should be considered early in placement.

Examples:

- Buck converters
- Linear regulators
- MOSFETs
- Power resistors

Good practices:

- Provide airflow where applicable
- Use copper areas for heat spreading
- Avoid placing heat-sensitive components nearby
- Consider thermal vias if required

---

# Logical Placement of Passive Components

Passive components should generally be placed close to the devices they support.

Example:

```
MCU

↓

Decoupling Capacitor

↓

Ground Via
```

Similarly:

- Pull-up resistors should be close to the associated signal.
- Current-limiting resistors should be close to LEDs.
- Bootstrap components should be close to the regulator or driver IC.

---

# Component Accessibility

Consider future servicing and debugging.

Avoid placing:

- Jumpers beneath large components
- Test points under connectors
- Programming headers in inaccessible areas

Important connectors and headers should remain easily accessible after assembly.

---

# Mechanical Considerations

Placement should account for:

- Mounting holes
- Board edges
- Keepout zones
- Enclosure dimensions
- Component height restrictions
- Cable routing

Electrical placement alone is not sufficient.

---

# Placement Review Checklist

Before routing begins, verify:

- Functional blocks grouped logically
- Signal flow is intuitive
- MCU centrally positioned
- Crystal close to MCU
- Decoupling capacitors adjacent to power pins
- Connectors located at board edges
- High-power components separated from sensitive circuits
- Component orientation consistent
- Mechanical constraints satisfied
- Adequate spacing for assembly
- Thermal considerations addressed

---

# Common Placement Mistakes

❌ Placing components without considering signal flow

❌ Long traces between related components

❌ Crystal placed far from MCU

❌ Decoupling capacitors located far from VDD pins

❌ Random orientation of polarized components

❌ Connectors placed away from board edges

❌ Ignoring enclosure dimensions

❌ Crowding components without considering assembly

❌ Placing heat-generating components next to temperature-sensitive devices

---

# Practical Applications

Proper component placement is essential in:

- Battery Management Systems (BMS)
- Motor Controllers
- IoT Devices
- Industrial Automation
- Medical Electronics
- Automotive ECUs
- High-Speed Communication Boards
- RF Modules

---

# Key Takeaways

Component placement is far more than arranging parts on a PCB. It establishes the foundation for routing, signal integrity, manufacturability, thermal performance, and assembly quality.

Professional PCB designers first understand circuit functionality, then organize components into logical functional blocks, follow signal flow, consider manufacturing constraints, and finally optimize placement before beginning routing.

Good placement reduces routing complexity, improves electrical performance, lowers production cost, and results in a more reliable and maintainable PCB.
