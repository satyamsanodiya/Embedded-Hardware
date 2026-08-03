# 06 - Controlled Impedance

# Overview

Controlled impedance is one of the fundamental requirements of High-Speed PCB Design.

As signal frequencies increase, PCB traces no longer behave as simple copper wires. Instead, they behave as **transmission lines** having a characteristic impedance determined by the PCB geometry and dielectric material.

If the characteristic impedance of a PCB trace is not controlled, signal reflections, ringing, timing errors, and communication failures can occur.

Modern high-speed interfaces such as USB, Ethernet, PCIe, HDMI, DDR, LVDS, and MIPI all require controlled impedance routing to ensure reliable data transmission.

---

# Learning Objectives

After completing this chapter, I understood:

- What impedance is
- Difference between resistance and impedance
- Why PCB traces have characteristic impedance
- What controlled impedance means
- Single-ended impedance
- Differential impedance
- Common-mode and Differential-mode signals
- Factors affecting impedance
- Why controlled impedance is important
- Basic impedance calculations
- Best routing practices

---

# What is Impedance?

Impedance is the total opposition that a circuit presents to alternating current (AC) or rapidly changing digital signals.

Unlike resistance, impedance includes the effects of:

- Resistance (R)
- Capacitance (C)
- Inductance (L)

For DC circuits:

```
Only Resistance exists.
```

For High-Speed Digital Signals:

```
Resistance
+

Inductance

+

Capacitance

↓

Impedance
```

Therefore, every PCB trace carrying a fast-changing signal has an impedance.

---

# Resistance vs Impedance

| Resistance | Impedance |
|------------|-----------|
| Opposes DC current | Opposes AC / High-Speed Signals |
| Depends only on material | Depends on PCB geometry and frequency |
| Constant value | Frequency dependent |
| Unit: Ohm (Ω) | Unit: Ohm (Ω) |

---

# Why Does a PCB Trace Have Impedance?

Many beginners think a PCB trace is simply a copper wire.

In reality, every PCB trace forms a distributed network of resistance, capacitance, and inductance.

Example:

```

Copper Trace

=====================

Air

FR4

Ground Plane

█████████████████████
```

The trace and the ground plane behave like a transmission line.

Because of this,

every signal experiences:

- Distributed capacitance
- Distributed inductance

These properties create the trace's **Characteristic Impedance (Z₀).**

---

# What is Characteristic Impedance?

Characteristic impedance (Z₀) is the impedance seen by a signal as it travels along a transmission line.

It is determined entirely by the PCB construction.

It is **NOT** measured using a multimeter.

Instead, it depends on:

- Trace Width
- Copper Thickness
- Distance to Reference Plane
- PCB Material (FR4 Dielectric Constant)
- Trace Geometry

Once these parameters are fixed,

the impedance is fixed.

---

# Why Controlled Impedance?

Imagine water flowing through a pipe.

```
Wide Pipe
──────────────

↓

Narrow Pipe
──────
```

When the pipe suddenly becomes narrow,

water flow becomes disturbed.

Exactly the same thing happens to electrical signals.

If impedance suddenly changes,

part of the signal reflects backward.

This is called **Reflection.**

---

# Signal Reflection

Ideal

```
MCU -------------------- Receiver
```

Poor Routing

```
MCU -----------||---------- Receiver
               ^
        Impedance Change
```

Part of the signal continues.

Part of the signal reflects.

Result:

- Overshoot
- Ringing
- Data Errors
- Communication Failure

---

# What is Controlled Impedance?

Controlled impedance means designing PCB traces so that their characteristic impedance remains constant throughout the signal path.

The PCB manufacturer controls impedance by carefully selecting:

- PCB Stackup
- Dielectric Thickness
- Copper Thickness

The PCB designer controls impedance by selecting:

- Trace Width
- Trace Spacing
- Layer
- Reference Plane

---

# Types of Controlled Impedance

Two major types are used.

---

# Single-Ended Impedance

A single-ended signal uses one trace referenced to ground.

Example:

```
Signal

===================

Ground Plane

███████████████████
```

Typical Values

| Interface | Typical Impedance |
|------------|-------------------|
| SPI | 50 Ω |
| UART | 50 Ω |
| GPIO | 45–60 Ω |
| Clock | 50 Ω |

Many PCB manufacturers target

**50 Ω**

although values around **45 Ω** are also common depending on the stackup.

---

# Differential Impedance

A differential signal consists of two traces carrying equal and opposite signals.

Example:

```
USB D+

====================

USB D-

====================
```

Instead of referencing only ground,

the two traces interact with each other.

This interaction is called **Coupling.**

Typical Differential Interfaces

- USB

- Ethernet

- PCIe

- HDMI

- LVDS

- CAN FD

Typical Differential Impedance

```
90 Ω
```

for USB 2.0.

---

# Common Mode vs Differential Mode

Differential Pair

```
D+

↑

D-
```

When one line goes HIGH,

the other goes LOW.

Receiver measures

```
D+

minus

D-
```

This is called

**Differential Mode.**

---

Noise affecting both lines equally

```
Noise

↓

D+

↓

D-
```

is called

**Common Mode Noise.**

Since both traces receive the same noise,

the receiver subtracts the signals,

causing the common noise to cancel.

This is one of the biggest advantages of differential signaling.

---

# Factors Affecting Impedance

Characteristic impedance depends upon several PCB parameters.

## 1. Trace Width

Increasing trace width

↓

Decreases impedance.

Reducing trace width

↓

Increases impedance.

---

## 2. Distance to Ground Plane

Greater distance

↓

Higher impedance

Smaller distance

↓

Lower impedance

---

## 3. Dielectric Constant (Er)

Different PCB materials produce different impedance values.

FR4

Typical Er

≈ 4.2–4.5

---

## 4. Copper Thickness

Thicker copper slightly changes impedance.

---

## 5. Differential Pair Spacing

Closer spacing

↓

More coupling

↓

Lower Differential Impedance

Wider spacing

↓

Less coupling

↓

Higher Differential Impedance

---

# How is Impedance Calculated?

PCB designers normally do not calculate impedance manually.

Instead, they use:

- KiCad PCB Calculator
- Saturn PCB Toolkit
- Polar SI9000
- PCB Manufacturer Stackup Calculator

Inputs:

- PCB Thickness
- Dielectric Height
- Copper Thickness
- Trace Width
- Trace Spacing
- Dielectric Constant

Outputs:

- Single-ended impedance

- Differential impedance

---

# Controlled Impedance in KiCad

KiCad includes an impedance calculator where the designer enters:

- Stackup
- Copper thickness
- Trace width
- Trace spacing
- Dielectric thickness

The calculator determines the required trace geometry to achieve the target impedance.

Example

Target:

```
USB Differential Pair

90 Ω
```

KiCad calculates

Required Trace Width

Required Pair Spacing

---

# Best Practices

✔ Keep impedance constant.

✔ Maintain uniform trace width.

✔ Maintain constant pair spacing.

✔ Keep traces over solid ground planes.

✔ Minimize layer transitions.

✔ Avoid routing across plane splits.

✔ Follow PCB manufacturer's impedance stackup.

✔ Use KiCad impedance calculator before routing.

---

# Common Beginner Mistakes

❌ Thinking impedance is the same as resistance.

❌ Ignoring PCB stackup.

❌ Changing trace width during routing.

❌ Inconsistent differential pair spacing.

❌ Routing over split planes.

❌ Using arbitrary trace widths.

❌ Not communicating impedance requirements to PCB manufacturer.

---
# Knowledge Check

### Q1. What is the difference between resistance and impedance?

### Q2. Why do PCB traces behave as transmission lines?

### Q3. What is characteristic impedance?

### Q4. Which PCB parameters affect impedance?

### Q5. Why is controlled impedance important in USB?

### Q6. Explain single-ended impedance with an example.

### Q7. Explain differential impedance with an example.

### Q8. What is common-mode noise?

### Q9. Why does differential signaling provide better noise immunity?

### Q10. Why should trace width remain constant throughout the routing?

### Q11. Why should impedance be calculated before routing?

### Q12. Which PCB tools can be used to calculate controlled impedance?

# Real Applications

Controlled impedance is required in:

- USB

- Ethernet

- PCIe

- HDMI

- DisplayPort

- DDR Memory

- LVDS

- MIPI

- High-Speed ADCs

- High-Speed DACs

---

# Key Takeaways

- Every high-speed PCB trace behaves as a transmission line.
- Characteristic impedance depends on PCB geometry.
- Controlled impedance minimizes signal reflections.
- Single-ended signals are referenced to ground.
- Differential signals use two coupled traces.
- Differential signaling improves noise immunity.
- PCB stackup and trace geometry must be planned before routing.
