# PCB Routing and Best Practices

## Overview

After learning PCB component placement and power planning, the next step is PCB routing.

Routing is the process of creating electrical connections between components using copper traces while maintaining signal integrity, power integrity, manufacturability, and electromagnetic compatibility (EMC).

Good routing is much more than simply connecting two pins together. Every routed trace introduces resistance, inductance, capacitance, and electromagnetic effects that influence circuit performance.

During this lesson, I studied:

- PCB trace width selection
- Via structure and via types
- Power routing
- Ground routing
- Differential pair routing
- USB high-speed routing
- EMI reduction techniques
- Series termination resistors
- Ground planes and copper zones
- Return current paths
- ERC and DRC verification
- PCB routing best practices

---

# 1. PCB Trace Routing

PCB routing is the process of creating copper paths between electrical components.

Example:

```text
MCU ---------------- Sensor
```

becomes

```text
MCU ========= Sensor
      Copper Trace
```

Every copper trace behaves as an electrical conductor with its own:

- Resistance
- Inductance
- Capacitance

These parasitic effects become increasingly important as signal frequency and current increase.

---

# 2. Choosing Proper Trace Width

Trace width should always be selected according to:

- Maximum current
- Temperature rise
- Copper thickness
- PCB manufacturing capability

Example:

```text
Low Current Signal

========
0.15 mm


High Current Supply

============================
2 mm
```

A narrow trace carrying excessive current may experience:

- Excessive voltage drop
- Higher power dissipation
- Increased temperature
- Reduced reliability

Power traces should generally be much wider than signal traces.

---

# 3. Signal Routing vs Power Routing

Signal routing focuses on maintaining signal quality.

Power routing focuses on delivering current with minimum voltage drop.

Example:

```text
Signal

MCU -------- Sensor


Power

Battery ================= Buck Converter
```

Power traces are usually wider because they must carry significantly more current.

---

# 4. Current Always Flows in a Loop

A PCB trace never carries current alone.

Every current has a complete loop.

```text
Source
   │
   ▼
Forward Trace
   │
Load
   │
Return Current
   │
Ground Plane
   │
Back to Source
```

Ignoring the return path is one of the most common PCB design mistakes.

---

# 5. Ground Return Path

The return current always tries to follow the path with the lowest impedance.

For high-frequency signals, the return current usually flows directly beneath the signal trace inside the ground plane.

```text
Signal
======================>

Ground Plane
██████████████████████
<======================
```

Keeping a continuous ground plane provides the shortest and lowest-inductance return path.

---

# 6. Ground Zones and Ground Planes

A ground plane is a large continuous copper region connected to GND.

Advantages include:

- Low impedance return path
- Lower EMI
- Better signal integrity
- Reduced voltage drop
- Easier routing
- Improved heat spreading

Example:

```text
Top Layer
------------------------

Bottom Layer

██████████████████████
Continuous Ground Plane
```

Ground planes should be kept as continuous as possible.

Avoid unnecessary splits that interrupt return current.

---

# 7. Copper Pour (Ground Zone)

Instead of routing individual GND traces everywhere, unused PCB copper can be converted into a ground zone.

Example:

```text
██████████████████████████
██████ MCU ███████████████
██████████████████████████
```

Benefits:

- Lower ground impedance
- Better thermal performance
- Reduced EMI
- Improved shielding
- Less copper etching cost

---

# 8. PCB Vias

A via is a plated hole used to electrically connect copper between different PCB layers.

Example:

```text
Top Layer
-----------●--------

           │
           │ Via
           │

Bottom Layer
-----------●--------
```

---

# 9. Types of Vias

## Through Via

Connects all PCB layers.

```text
TOP
 │
 │
 │
BOTTOM
```

Most common and lowest cost.

---

## Blind Via

Connects an outer layer to an inner layer.

```text
TOP
 │
 │
Inner Layer
```

Used when routing density is high.

---

## Buried Via

Connects only internal layers.

```text
Inner Layer
 │
 │
Inner Layer
```

Not visible from outside.

Common in HDI PCB designs.

---

# 10. Via Best Practices

Use vias only when necessary.

Too many vias introduce:

- Additional inductance
- Additional resistance
- Higher manufacturing cost

For power routing, multiple vias may be placed in parallel.

```text
█████
● ● ●
█████
```

This reduces current density and improves thermal conduction.

---

# 11. High-Speed Routing

As signal frequency increases, PCB traces begin behaving like transmission lines.

Routing becomes much more sensitive to:

- Trace length
- Impedance
- Return path
- Crosstalk
- EMI

Therefore high-speed routing requires controlled layout practices.

---

# 12. Differential Pair Routing

Some communication interfaces use two complementary signals.

Examples:

- USB
- CAN
- Ethernet
- LVDS

Instead of routing one signal, two traces are routed together.

```text
======================
======================
```

These two traces form a differential pair.

Important rules:

- Equal length
- Constant spacing
- Same reference plane
- Same number of vias whenever possible

---

# 13. USB High-Speed Routing

USB D+ and D− form a differential pair.

Example:

```text
USB Connector

D+
======================

D-
======================
```

Good routing practices include:

- Keep traces short
- Route both signals together
- Maintain constant spacing
- Avoid unnecessary vias
- Avoid sharp bends
- Route over a continuous ground plane
- Keep away from noisy switching circuits

Following these practices helps preserve signal integrity and reduces EMI.

---

# 14. 45° Routing vs 90° Routing

Instead of sharp corners,

Avoid:

```text
──────┐
      │
```

Prefer:

```text
──────╲
       ╲
```

or

```text
──────╱
```

45° routing generally provides smoother routing and is preferred in modern PCB design tools.

---

# 15. Avoiding Noise During Routing

Good routing minimizes noise coupling.

General practices include:

- Keep analog and digital sections separated
- Keep switching regulators away from analog circuits
- Keep high-current traces away from sensitive signals
- Keep crystal traces short
- Keep clock lines away from noisy power circuits
- Avoid routing over split ground planes
- Minimize loop area
- Keep return paths continuous

---

# 16. Reducing EMI Using Series Resistors

Fast switching edges generate higher-frequency harmonics, increasing EMI.

A small resistor placed in series near the driver slows the edge slightly.

Example:

```text
MCU

GPIO ----[33Ω]------ Signal
```

Benefits:

- Reduced ringing
- Reduced overshoot
- Reduced undershoot
- Lower EMI
- Improved signal quality

The resistor should be placed close to the signal source.

---

# 17. Crosstalk

Two parallel traces can couple energy into each other.

Example:

```text
Signal A
==================

Signal B
==================
```

If spacing is too small, Signal A can induce unwanted voltage in Signal B.

To reduce crosstalk:

- Increase spacing
- Route over a solid ground plane
- Minimize long parallel runs
- Use proper layer stackup

---

# 18. Power Integrity During Routing

Power routing should minimize:

- Voltage drop
- Loop inductance
- Noise

Good practices include:

- Wide power traces
- Short current paths
- Proper decoupling capacitor placement
- Solid power planes where possible

---

# 19. Ground Integrity

Ground should never be treated as "just another wire."

A poor ground layout can cause:

- Ground bounce
- ADC errors
- Communication failures
- Clock instability
- Increased EMI

A continuous ground plane provides the best reference for both digital and analog circuits.

---

# 20. Electrical Rule Check (ERC)

ERC verifies the logical correctness of the schematic.

Typical checks include:

- Unconnected pins
- Missing power connections
- Output-to-output conflicts
- Incorrect pin types

ERC is performed before PCB layout begins.

---

# 21. Design Rule Check (DRC)

DRC verifies whether the PCB layout follows manufacturing and electrical design rules.

Typical checks include:

- Minimum trace width
- Minimum spacing
- Via size
- Copper clearance
- Silkscreen overlap
- Component clearance
- Board edge clearance

DRC should always pass before PCB fabrication.

---

# 22. Routing Workflow

A systematic routing workflow helps produce cleaner and more reliable layouts.

```text
Complete Component Placement
            ↓
Review Power Paths
            ↓
Review Ground Planes
            ↓
Route Critical Signals
            ↓
Route Differential Pairs
            ↓
Route Clock Signals
            ↓
Route Analog Signals
            ↓
Route Remaining Signals
            ↓
Create Ground Zones
            ↓
Run ERC
            ↓
Run DRC
            ↓
Final Review
```

---

# 23. Common Routing Mistakes

- Routing before completing placement
- Using unnecessarily narrow power traces
- Ignoring current return paths
- Breaking the ground plane
- Placing decoupling capacitors far from IC pins
- Excessive use of vias
- Routing differential pairs with unequal lengths
- Long parallel traces causing crosstalk
- Sharp 90° corners
- Ignoring ERC and DRC warnings

---

# 24. Engineering Checklist

Before generating Gerber files, verify:

- [ ] Critical components are correctly placed
- [ ] Power traces are sized appropriately
- [ ] Ground plane is continuous
- [ ] Return paths are uninterrupted
- [ ] Differential pairs are matched
- [ ] USB routing follows differential pair rules
- [ ] High-current traces are sufficiently wide
- [ ] Number of vias is minimized
- [ ] Ground zones are properly connected
- [ ] Series resistors are placed where required
- [ ] ERC passes without critical errors
- [ ] DRC passes without violations

---

# Key Learning

PCB routing is not simply drawing copper connections between components.

Every trace, via, and plane influences current flow, signal integrity, power integrity, thermal performance, and electromagnetic compatibility.

A successful PCB layout is achieved by understanding how electricity physically travels through the board, ensuring that both forward and return current paths are short, continuous, and low impedance.

By applying proper routing practices, a PCB becomes more reliable, easier to manufacture, and capable of supporting high-speed embedded systems with minimal noise and EMI.
