# PCB Layout Design

## Objective

The objective of the PCB layout stage was to convert the validated schematic into a manufacturable and electrically robust PCB while considering high-voltage battery monitoring, CAN communication, power integrity, thermal performance, and serviceability.

---

## PCB Overview

- Board Type: 2-Layer PCB
- Board Dimensions: 100.4 mm × 69.4 mm
- Application: 14S EV Battery Management System
- AFE: BQ76940
- MCU: STM32
- Communication: CAN Bus
- Protection: Input Protection + High Side MOSFET Control

---

## Layout Strategy

The PCB was partitioned into functional blocks to minimize interference and simplify routing.

### Power Section

The power conversion stages were grouped together near the input side of the PCB.

This includes:

- Input Protection Circuit
- PI Filter
- 50V to 12V Buck Converter
- 12V to 5V Buck Converter
- 5V to 3.3V Buck Converter

Keeping these blocks close together reduces power loop area and minimizes switching noise.

---

### Battery Monitoring Section

The BQ76940 Analog Front End was placed close to the cell sense connector.

Benefits:

- Shorter cell measurement traces
- Reduced noise pickup
- Improved measurement accuracy
- Easier balancing network routing

---

### MCU Section

The STM32 microcontroller was placed centrally.

Benefits:

- Short routing to AFE
- Short routing to CAN transceiver
- Simplified SWD debugging interface
- Better signal integrity

---

### CAN Communication Section

The CAN transceiver was placed near the CAN connector.

Benefits:

- Reduced CAN trace length
- Lower EMI emission
- Improved communication reliability

---

### High Side Control Section

The high-side MOSFET driver circuit was isolated from sensitive analog measurement circuitry.

Benefits:

- Reduced switching noise coupling
- Improved battery measurement stability
- Better system safety

---

## Routing Considerations

The routing process focused on signal integrity and manufacturability.

Key considerations:

- Short signal paths where possible
- Smooth trace transitions
- Avoidance of unnecessary routing loops
- Separation of power and signal routing
- Proper decoupling capacitor placement near IC power pins

---

## Connector Selection

### Cell Monitoring Connector

A dedicated cell monitoring connector was used for all 14 cell voltage sensing lines.

This allows direct connection of battery cell taps to the BQ76940 AFE.

---

### CAN Connector

Dedicated CANH and CANL outputs were provided for external communication.

This enables integration with chargers, vehicle controllers, and external monitoring systems.

---

### SWD Programming Header

A dedicated SWD header was included.

Functions:

- Firmware programming
- Real-time debugging
- Production testing

---

### Metal Terminal Blocks

High-current metal terminal blocks were selected for battery pack and charger connections.

Reasons:

- Higher current carrying capability
- Improved mechanical strength
- Better field serviceability
- Secure wire termination
- Reduced contact resistance

Since the BMS is intended for EV battery applications, standard pin headers were not suitable for carrying pack current safely.

---

## Design for Manufacturing (DFM)

The PCB was designed while considering manufacturing constraints.

Practices followed:

- Consistent component orientation
- Adequate spacing between components
- Standard SMD package selection
- Proper mounting hole placement
- Clear connector accessibility

---

## Learning Outcomes

Through this layout design, I gained practical experience in:

- Functional PCB partitioning
- Power supply routing
- CAN interface layout
- Analog Front End integration
- High-side switching circuits
- Design for Manufacturing (DFM)
- Battery management system PCB design
