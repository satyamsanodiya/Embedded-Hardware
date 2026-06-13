# PCB Layout Design

## Overview

The PCB layout was developed with a focus on compact board dimensions, manufacturability, signal integrity, and ease of assembly.

A major project requirement was to fit all supporting circuitry on the bottom layer while keeping the graphical LCD interface on the top side. This approach simplifies display mounting and allows direct user interaction without increasing the overall board size.

The final PCB was implemented as a two-layer design using standard PCB manufacturing rules.

---

## Board Dimension Constraints

### Objective

The board dimensions were predefined by mechanical constraints and enclosure requirements.

### Design Approach

Since the available PCB area was limited, component placement and routing had to be optimized carefully.

Special attention was given to:

- Efficient component placement
- Routing density
- Connector accessibility
- Display alignment
- Manufacturing feasibility

The design process prioritized functional grouping of components before routing began.

---

## Component Placement Strategy

### Functional Block Placement

Components were arranged according to their function rather than purely by available space.

This resulted in shorter routing paths and improved signal organization.

### Placement Groups

| Block | Placement Purpose |
|---------|---------|
| Power Supply Circuit | Near power input connector |
| ESP32-S3 | Central position |
| MCP23017 | Close to ESP32 and LCD connector |
| LCD Connector | Board edge for display mounting |
| Programming Header | Easily accessible for development |
| Keypad Headers | Edge-mounted for external access |

This placement strategy reduced unnecessary signal crossings and improved routing efficiency.

---

## Bottom-Side Assembly Strategy

### Objective

Minimize mechanical interference with the graphical display.

### Design Decision

All active and passive components were placed on the bottom side of the PCB.

Only the LCD connector remained on the top side.

### Benefits

- Simplified display installation
- Better mechanical stability
- Reduced assembly complexity
- Cleaner top-side appearance
- Easier enclosure integration

This approach is commonly used in commercial display controller boards.

---

## LCD Placement Strategy

### Objective

Provide reliable mounting for the 128×64 graphical LCD.

### Design Decision

The LCD connector was positioned directly beneath the display mounting area.

### Reasoning

The LCD connector location was selected before routing to ensure proper mechanical alignment.

Benefits:

- Reduced signal path length
- Easier display installation
- Improved structural stability
- Lower routing congestion

---

## MCP23017 Placement Strategy

### Objective

Reduce routing complexity between the GPIO expander and LCD interface.

### Design Decision

The MCP23017 was positioned close to the display connector.

### Reasoning

The MCP23017 provides most of the LCD control and data signals.

Placing it near the LCD connector:

- Reduces trace length
- Improves signal organization
- Simplifies routing
- Minimizes PCB congestion

This follows a common PCB design principle:

> Components that communicate heavily should be placed physically close together.

---

## ESP32 Placement Strategy

### Objective

Serve as the central controller of the system.

### Design Decision

The ESP32-S3 was placed near the center of the PCB.

### Reasoning

The ESP32 communicates with:

- MCP23017
- Programming interface
- Power circuitry
- User input peripherals

A central location minimizes average trace length and allows cleaner signal distribution throughout the board.

---

## Passive Component Package Selection

### Resistor Package Selection

**Selected Package:** 0603 (1608 Metric)

#### Reasoning

Although smaller packages such as 0402 were available, 0603 resistors were selected because they provide:

- Easier manual soldering
- Easier inspection
- Better rework capability
- Higher assembly reliability

For prototype and educational hardware, 0603 offers an excellent balance between compactness and manufacturability.

---

### Capacitor Package Selection

**Selected Package:** 0603 (1608 Metric)

#### Reasoning

Using the same package size for most passive components:

- Simplifies assembly
- Reduces inventory complexity
- Minimizes placement errors
- Improves manufacturing consistency

This is a common industry practice in low-to-medium complexity designs.

---

## Routing Strategy

### Objective

Maintain signal integrity while achieving complete connectivity within the available board area.

### Design Rules Followed

- Short signal paths wherever possible
- Minimal layer transitions
- Consistent routing directions
- Clean return paths
- Manual routing approach

### Design Considerations

Power traces were routed first, followed by signal traces.

Critical communication lines were routed with minimal unnecessary bends to improve routing clarity and signal quality.

---

## Avoidance of 90-Degree Corners

### Design Decision

Routing was performed using 45-degree trace transitions wherever practical.

### Reasoning

Although modern PCB fabrication processes can handle 90-degree corners, 45-degree routing offers:

- Cleaner layout appearance
- Better professional design practices
- Improved manufacturing aesthetics
- More consistent routing style

This routing method is widely adopted in commercial PCB layouts.

---

## Via Usage Strategy

### Objective

Reduce manufacturing complexity and maintain signal continuity.

### Design Approach

Vias were used only when necessary.

Excessive layer transitions were avoided because they:

- Increase manufacturing complexity
- Introduce routing discontinuities
- Add parasitic capacitance and inductance

The layout was optimized to minimize overall via count.

---

## Power Routing Considerations

### Objective

Provide stable voltage delivery to all subsystems.

### Design Approach

Power traces were routed with larger widths than signal traces.

This reduces:

- Voltage drop
- Resistive losses
- Localized heating

The power distribution network was completed before routing low-current digital signals.

---

## Grounding Strategy

### Objective

Provide a low-impedance return path for all circuits.

### Design Approach

Ground connections were kept short and direct.

Special attention was given to:

- Decoupling capacitor placement
- Ground continuity
- Return current paths

This improves overall system stability and reduces susceptibility to noise.

---

## Design for Manufacturing (DFM)

### Objective

Ensure the PCB can be manufactured and assembled reliably.

### Considerations

- Standard component packages used
- Adequate component spacing maintained
- Silkscreen readability preserved
- Connector orientation verified
- Assembly accessibility considered

These practices help reduce assembly errors and improve production yield.

---

## Key Engineering Decisions

### Why 0603 Components?

- Easier hand soldering
- Easier debugging
- Better rework capability
- Good balance between size and manufacturability

### Why Keep LCD on the Top Layer?

- Simplifies mechanical mounting
- Improves user accessibility
- Reduces enclosure complexity

### Why Place MCP23017 Near LCD?

- Reduces routing complexity
- Shortens LCD signal traces
- Improves PCB organization

### Why Place ESP32 Centrally?

- Optimizes routing to all peripherals
- Reduces average trace length
- Improves layout balance

### Why Avoid Excessive Vias?

- Cleaner routing
- Improved manufacturability
- Reduced parasitic effects

---

## Layout Summary

The PCB layout was developed using industry-standard placement and routing practices while satisfying strict board-size constraints.

The final design achieves:

- Compact board dimensions
- Bottom-side component assembly
- Top-side display mounting
- Efficient routing structure
- Manufacturable two-layer PCB design
- Clean and maintainable layout architecture

The design demonstrates practical PCB layout techniques including component placement optimization, routing discipline, manufacturability considerations, and hardware integration for embedded display-control applications.
