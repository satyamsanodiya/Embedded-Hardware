# Project Requirements

## Project Goal

Develop a compact embedded display controller capable of driving a 128×64 graphical LCD using an ESP32-S3 microcontroller while minimizing GPIO usage and PCB complexity.

The system is intended for embedded HMI applications where display visualization and user input are required.

---

## Functional Requirements

### Display Interface

The system shall support:

- 128×64 graphical LCD
- Graphical rendering capability
- Character and bitmap display

The display interface shall be implemented through an external I²C GPIO expander to reduce direct GPIO consumption from the ESP32-S3.

---

### User Input

The system shall support:

- External keypad connection
- Multiple button inputs
- User navigation capability

---

### Processing Unit

The controller shall use:

- ESP32-S3-WROOM module

The microcontroller must provide:

- Sufficient GPIO resources
- I²C communication support
- Future firmware scalability

---

### Power System

Input Supply:

- 15V DC

Generated Rails:

- 5V Rail
- 3.3V Rail

Power conversion must provide stable operation for both the display and controller.

---

## Mechanical Requirements

PCB Size:

- 93 mm × 70.5 mm

Component Placement Requirements:

- LCD connector located on top side
- Remaining components placed on bottom side
- Four mounting holes for enclosure integration

---

## Interface Requirements

### LCD Interface

Interface Method:

- MCP23017 I²C Expander

Reason:

Direct LCD connection would consume a large number of ESP32 GPIO pins.

Using an I²C expander reduces wiring complexity and preserves GPIO resources for future expansion.

---

### Keypad Interface

Dedicated connector shall be provided for external keypad attachment.

---

### Programming Interface

Programming header shall be provided for:

- Firmware upload
- Debugging
- System testing

---

## Design Constraints

- Two-layer PCB
- Low manufacturing cost
- Compact routing
- Easy assembly
- Serviceable prototype design

---

## Expected Deliverables

- Complete schematic design
- PCB layout
- Manufacturing files
- Design documentation
- Validation records
