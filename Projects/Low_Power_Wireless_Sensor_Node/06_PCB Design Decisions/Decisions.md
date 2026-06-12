# PCB Design Decisions

| Design Decision | Reason |
|---------------|---------|
| PMIC placed near USB-C connector | Minimized power-path length and voltage drop |
| BM15M placed centrally | Reduced routing complexity and signal lengths |
| Programming header placed at board edge | Easier debugging and firmware updates |
| Ground copper pour used | Improved return-current paths and reduced noise |
| Short routing paths used | Improved signal integrity and reduced EMI susceptibility |
| Smooth trace routing preferred | Improved readability and manufacturing consistency |
| Modular sensor connectors provided | Allowed future sensor expansion without PCB redesign |
| Compact board dimensions selected | Reduced overall system size while maintaining manufacturability |

# Design Challenges & Lessons Learned

## Overview

During the development of this low-power wireless sensor node, several engineering challenges were encountered across power management, sensor integration, PCB layout, and system architecture.

Documenting these challenges helped improve the final design and provided valuable experience for future embedded hardware projects.

---

# Challenge 1: Power Budget Optimization

## Problem

The system was intended to operate from a rechargeable battery while supporting:

- BLE communication
- Multiple environmental sensors
- RGB indication
- External display support

Without proper power planning, battery life could be significantly reduced.

## Solution

A dedicated Power Management IC (nPM1300) was selected to provide:

- Battery charging
- Power path management
- System regulation

Low-power sensors and peripherals were selected wherever possible to reduce overall system current consumption.

## Lesson Learned

Power architecture should be planned before component selection because it influences every subsystem in the design.

---

# Challenge 2: Sensor Expansion Flexibility

## Problem

The final sensor combination could change during development.

Directly integrating all sensors onto the PCB would reduce future flexibility.

## Solution

Dedicated sensor interfaces were provided instead of permanently fixing every sensor on the board.

This allows:

- Easy sensor replacement
- Future expansion
- Faster prototyping

## Lesson Learned

Modular hardware architectures significantly increase product flexibility.

---

# Challenge 3: Compact PCB Layout

## Problem

The board needed to remain compact while integrating:

- PMIC
- BM15M BLE module
- USB Type-C interface
- Battery connector
- Programming header
- Sensor interfaces

## Solution

Component placement was planned before routing.

Critical blocks were positioned according to signal flow and power flow.

## Lesson Learned

Good component placement solves most routing problems before routing even begins.

---

# Challenge 4: Reliable Power Distribution

## Problem

Power rails had to be distributed across the PCB without excessive voltage drop or noise.

## Solution

Power traces were routed before signal traces.

The PMIC was placed close to the USB Type-C connector and battery interface to minimize power-path length.

## Lesson Learned

Power routing should always be prioritized over signal routing.

---

# Challenge 5: Ground Return Path Management

## Problem

Poor grounding can introduce noise and reduce system reliability.

## Solution

A continuous ground copper pour was implemented across the PCB.

This improved:

- Return current paths
- Signal integrity
- Noise immunity

## Lesson Learned

Ground design is just as important as signal routing.

---

# Challenge 6: Manufacturability

## Problem

A design may function electrically but still be difficult to manufacture or assemble.

## Solution

Attention was given to:

- Connector accessibility
- Programming header accessibility
- Component spacing
- PCB organization

## Lesson Learned

A good PCB design must be both functional and manufacturable.

---

# Key Engineering Takeaways

This project provided practical experience in:

- Power management design
- Battery-powered systems
- BLE-enabled embedded hardware
- Sensor integration
- Schematic capture
- PCB layout and routing
- Design verification
- Hardware documentation

---

# Future Improvements

Potential future enhancements include:

- Additional environmental sensors
- Improved power monitoring
- Dedicated battery fuel gauging
- Custom enclosure integration
- Wireless firmware update capability

---

# Final Reflection

This project strengthened my understanding of embedded hardware development by exposing me to the complete design flow:

Requirements → Architecture → Component Selection → Schematic Capture → PCB Layout → Verification

The experience reinforced the importance of structured design methodology, documentation, and engineering trade-off analysis during hardware development.
