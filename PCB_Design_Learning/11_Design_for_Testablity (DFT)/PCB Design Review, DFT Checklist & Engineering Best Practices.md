# PCB Design Review, DFT Checklist & Engineering Best Practices

# Overview

A PCB design should never be sent for fabrication immediately after routing is complete. Even if the schematic is correct and the PCB passes ERC and DRC, many practical issues may still exist that affect manufacturability, assembly, testing, debugging, and long-term reliability.

Professional hardware companies therefore perform a **PCB Design Review**, where engineers systematically inspect the design before releasing manufacturing files.

The objective is to detect problems early, reduce costly redesigns, improve production yield, and ensure that the PCB is ready for fabrication, assembly, testing, and field maintenance.

---

# Learning Objectives

After completing this chapter, I understood:

- Importance of PCB design review
- Review process before fabrication
- Footprint verification
- Component orientation review
- Routing verification
- Signal congestion review
- Test point verification
- SWD/JTAG verification
- 3D inspection
- Manufacturing output verification
- Final engineering checklist

---

# Why PCB Design Review is Necessary

A PCB may successfully pass:

✔ ERC

✔ DRC

but still contain problems such as:

- Wrong footprint
- Incorrect connector orientation
- Missing mounting holes
- Inaccessible SWD connector
- Poor test point placement
- Silkscreen hidden under components
- Mechanical interference
- Difficult assembly
- Poor thermal performance

These issues are usually discovered during manual design review rather than automated software checks.

---

# Engineering Review Flow

A professional review process typically follows this sequence:

```
Schematic Review
        │
        ▼
Footprint Review
        │
        ▼
Component Placement Review
        │
        ▼
Routing Review
        │
        ▼
Power Integrity Review
        │
        ▼
Signal Integrity Review
        │
        ▼
DFM Review
        │
        ▼
DFT Review
        │
        ▼
Mechanical Review
        │
        ▼
ERC / DRC
        │
        ▼
3D Inspection
        │
        ▼
Gerber Generation
```

Each stage focuses on a different aspect of the PCB.

---

# Footprint Verification

One of the most common causes of PCB redesign is selecting the wrong footprint.

Verify:

✔ Package matches the datasheet

✔ Pin numbering is correct

✔ Pad dimensions are correct

✔ Thermal pad dimensions are correct

✔ Orientation matches schematic symbol

✔ Manufacturer recommended footprint is used

Example:

```
STM32

LQFP64

↓

Verify

64 Pads

Pin-1

Pad Pitch

Body Size
```

Never assume a downloaded library footprint is correct—always compare it with the manufacturer's recommended land pattern.

---

# Component Placement Review

Before routing, verify:

✔ Functional blocks are grouped logically.

✔ Signal flow is clear.

✔ MCU is centrally located.

✔ Crystal is close to the MCU.

✔ Decoupling capacitors are close to power pins.

✔ High-power components are separated from sensitive analog circuits.

✔ Connectors are accessible.

✔ Mechanical constraints are satisfied.

Good placement reduces routing complexity and improves electrical performance.

---

# Component Orientation Review

Check that:

✔ Pin-1 indicators are visible.

✔ Similar ICs have consistent orientation.

✔ Polarized capacitors have consistent polarity.

✔ Diodes are correctly oriented.

✔ LEDs have consistent polarity.

✔ Connectors face the correct direction.

✔ Silkscreen markings are readable.

Consistent orientation simplifies assembly, AOI inspection, and maintenance.

---

# Routing Review

Review every routed signal.

Verify:

✔ Short signal paths

✔ Controlled impedance where required

✔ Proper differential pair routing

✔ Continuous ground reference

✔ No unnecessary vias

✔ Wide power traces

✔ Minimal loop area

✔ No acute angles

✔ No disconnected copper

---

# Signal Congestion Review

Areas with excessive routing density often create manufacturing and reliability issues.

Check for:

- Excessive vias
- Narrow routing channels
- Closely spaced traces
- Poor return current paths

If congestion is severe, consider improving placement rather than forcing difficult routing.

---

# Power Distribution Review

Verify:

✔ Wide power traces

✔ Continuous power planes

✔ Proper decoupling

✔ Short supply paths

✔ Low impedance return path

✔ Stable power distribution network (PDN)

---

# Thermal Review

Identify heat-generating components:

- Buck converters
- MOSFETs
- Linear regulators
- Power resistors

Verify:

✔ Copper area for heat spreading

✔ Thermal vias (if required)

✔ Adequate spacing from heat-sensitive components

✔ Airflow considerations

---

# Test Point Review

Verify that all important signals are accessible.

Examples:

```
TP_5V

TP_3V3

TP_GND

TP_RST

TP_UART_TX

TP_UART_RX

TP_CAN_TX

TP_CAN_RX
```

Check:

✔ Probe accessibility

✔ Proper spacing

✔ Clear silkscreen labels

✔ Accessible after assembly

---

# SWD / JTAG Review

Ensure the debug interface is production-ready.

Verify:

✔ Header location

✔ Pinout

✔ Ground reference

✔ Target voltage reference

✔ NRST connection

✔ Mechanical accessibility

✔ Correct orientation

The debug connector should remain accessible even after the PCB is installed inside its enclosure whenever practical.

---

# 3D Mechanical Inspection

Before fabrication, inspect the PCB using the CAD tool's 3D viewer.

Verify:

✔ Component height

✔ Connector alignment

✔ Mounting hole clearance

✔ Mechanical interference

✔ Board edge clearance

✔ Enclosure compatibility

Many mechanical problems become obvious only in the 3D model.

---

# Design Rule Verification

Perform final verification using:

## ERC

Checks:

- Missing connections
- Pin conflicts
- Power connections

## DRC

Checks:

- Trace width
- Clearance
- Via sizes
- Copper spacing
- Silkscreen overlap

Resolve all critical violations before generating manufacturing files.

---

# Manufacturing Output Verification

Before sending the design to the PCB manufacturer, verify that all required production files have been generated correctly.

Typical outputs include:

```
Gerber Files

Drill Files

Bill of Materials (BOM)

Pick & Place (Centroid) File

Assembly Drawing

Fabrication Drawing

3D Model (Optional)

PDF Schematic
```

Open the Gerber files in a Gerber viewer to confirm:

✔ Copper layers

✔ Silkscreen

✔ Solder mask

✔ Drill locations

✔ Board outline

Never send manufacturing data without reviewing the generated outputs.

---

# Common Design Review Mistakes

❌ Wrong footprint

❌ Incorrect connector orientation

❌ Missing programming header

❌ Missing test points

❌ Decoupling capacitors too far from IC

❌ Split return paths

❌ Unreadable silkscreen

❌ Forgotten mounting holes

❌ Skipping Gerber verification

---

# Final Engineering Checklist

Before releasing the PCB:

## Schematic

- [ ] ERC passed
- [ ] Component values verified
- [ ] Net names verified

## PCB Placement

- [ ] Functional grouping complete
- [ ] Signal flow verified
- [ ] Component orientation consistent

## Routing

- [ ] DRC passed
- [ ] Controlled impedance reviewed
- [ ] Differential pairs verified
- [ ] Ground return paths checked

## Power

- [ ] Decoupling capacitors placed correctly
- [ ] Power traces sized appropriately
- [ ] Thermal considerations reviewed

## DFM

- [ ] Fabrication limits satisfied
- [ ] Footprints verified
- [ ] Silkscreen reviewed
- [ ] Component spacing acceptable

## DFT

- [ ] Test points available
- [ ] SWD/JTAG connector verified
- [ ] Programming access confirmed
- [ ] Test points labeled

## Mechanical

- [ ] Board outline verified
- [ ] Mounting holes verified
- [ ] 3D inspection completed

## Manufacturing

- [ ] Gerbers reviewed
- [ ] Drill files verified
- [ ] BOM checked
- [ ] Pick & Place file generated
- [ ] Assembly drawings completed

---

# Lessons Learned

Throughout this learning journey, I realized that PCB design is far more than drawing traces between components.

A successful PCB must satisfy multiple engineering disciplines simultaneously:

- Electrical Design
- Signal Integrity
- Power Integrity
- Thermal Management
- Mechanical Design
- Design for Manufacturing (DFM)
- Design for Testability (DFT)
- Production Readiness

Considering these aspects early in the design process significantly improves reliability, manufacturability, and product quality while reducing development cost and redesign effort.

---

# Key Takeaways

- PCB design is an iterative engineering process, not just a routing task.
- A structured design review is essential before fabrication.
- Footprint, placement, routing, DFM, DFT, and mechanical verification are equally important.
- Automated checks such as ERC and DRC are necessary but cannot replace an engineering review.
- Reviewing manufacturing outputs before sending them to the PCB vendor helps prevent costly fabrication errors.
