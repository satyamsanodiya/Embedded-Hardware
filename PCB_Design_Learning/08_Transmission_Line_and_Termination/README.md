# 08 - Transmission Lines and Signal Termination

# Overview

As digital systems continue to operate at higher frequencies and faster edge rates, PCB traces can no longer be treated as ideal wires. Instead, they behave as **transmission lines**, where signal propagation, impedance matching, and reflections become critical factors.

Transmission line theory forms the foundation of High-Speed PCB Design because almost every modern interface—USB, Ethernet, HDMI, PCIe, DDR, SATA, and MIPI—depends on maintaining signal integrity while transmitting data over PCB traces.

This chapter explains transmission line theory, characteristic impedance, propagation delay, reflections, signal termination techniques, and practical PCB design strategies to ensure reliable high-speed communication.

---

# Learning Objectives

After completing this chapter, I understood:

- What a transmission line is
- Why PCB traces become transmission lines
- Signal propagation
- Characteristic impedance
- Propagation delay
- Signal reflections
- Reflection coefficient
- Transmission coefficient
- Stub effects
- Signal termination techniques
- Source termination
- End termination
- AC termination
- Differential termination
- Best PCB practices

---

# What is a Transmission Line?

A transmission line is any conductor that carries high-speed electrical signals where the physical length of the conductor becomes significant compared to the signal wavelength.

Examples include:

- PCB traces
- USB cables
- Ethernet cables
- Coaxial cables
- Twisted pair cables

Unlike ordinary wires, transmission lines possess distributed electrical properties.

Each small section of the trace contains:

- Resistance (R)
- Inductance (L)
- Capacitance (C)
- Conductance (G)

These distributed parameters determine how signals travel along the line.

---

# Why Does a PCB Trace Become a Transmission Line?

At low frequencies, electrical signals propagate almost instantaneously relative to the dimensions of the PCB.

```
MCU ---------------- LED
```

The PCB trace behaves like a simple conductor.

However, at high frequencies or with very fast rise/fall times, the signal requires measurable time to travel along the trace.

The PCB trace must now be treated as a transmission line.

The general design rule is:

> If the signal propagation delay of the trace is significant compared to the signal rise time, transmission line effects must be considered.

---

# Signal Propagation

Signals do not travel instantly through a PCB.

Instead, they propagate as electromagnetic waves.

```
MCU
 │
 │────────────►
 │
Receiver
```

The signal travels with a finite velocity determined by the PCB dielectric material.

For FR-4 PCBs, signal velocity is typically around **50–70% of the speed of light**, depending on the stackup.

---

# Characteristic Impedance

Every transmission line has a characteristic impedance (Z₀).

It depends on:

- Trace width
- Copper thickness
- Dielectric constant
- Distance to reference plane
- PCB stackup

Characteristic impedance is a property of the transmission line itself.

Typical values:

| Interface | Characteristic Impedance |
|-----------|-------------------------|
| Single-ended signal | ~50 Ω (often 45–60 Ω depending on stackup) |
| USB 2.0 Differential Pair | 90 Ω Differential |
| Ethernet Differential Pair | 100 Ω Differential |

---

# What Happens at the End of a Transmission Line?

Consider:

```
Driver
 │
 │======================== Receiver
```

If the receiver input impedance matches the characteristic impedance,

```
ZLoad = Z0
```

the signal is completely absorbed.

No reflection occurs.

---

# What is Reflection?

Suppose the signal encounters an impedance mismatch.

```
Driver

===================

Receiver

Different Impedance
```

The incoming wave cannot transfer all of its energy.

Instead,

Part of the signal continues forward.

Part reflects backward.

```
Forward Wave
────────────►

◄────────────

Reflected Wave
```

This reflected energy distorts the original waveform.

---

# Effects of Reflection

Signal reflections produce:

- Overshoot
- Undershoot
- Ringing
- Double clock edges
- Timing errors
- Data corruption
- Communication failures

These problems become increasingly severe as signal speed increases.

---

# Reflection Coefficient

Reflection depends on the relationship between:

- Characteristic Impedance (Z₀)
- Load Impedance (ZL)

The reflection coefficient is represented by:

Γ (Gamma)

General behavior:

- Perfect impedance match → No reflection
- Open circuit → Large positive reflection
- Short circuit → Large negative reflection

The closer the load impedance is to the transmission line impedance, the smaller the reflection.

---

# Stub Effects

A stub is an unwanted branch connected to the main signal path.

Example:

```
Signal

======================

            |

            |

          Stub
```

The stub behaves like a small transmission line.

It creates:

- Reflections
- Impedance discontinuities
- Ringing

Long stubs should therefore be avoided in high-speed PCB routing.

---

# What is Signal Termination?

Termination is the process of matching the transmission line impedance to reduce signal reflections.

Its purpose is:

- Improve signal integrity
- Reduce ringing
- Reduce overshoot
- Improve communication reliability

---

# Source Termination

A resistor is placed close to the signal driver.

```
MCU

│

[33Ω]

│

================ Receiver
```

Advantages:

- Simple
- Low cost
- Reduces reflections returning to the source
- Common in SPI, GPIO, clocks, and many digital interfaces

---

# End (Parallel) Termination

A resistor is placed near the receiver.

```
MCU

==================

Receiver

│

50Ω

│

GND
```

Advantages:

- Excellent impedance matching
- Reduces reflections at the load

Disadvantage:

- Continuous power consumption

---

# AC Termination

An RC network is placed near the receiver.

```
Signal

│

R

│

C

│

GND
```

Advantages:

- Lower DC power consumption
- Effective for high-speed digital signals

---

# Differential Termination

Differential interfaces terminate the pair using a resistor between the two signal lines.

```
D+

==================

120Ω

==================

D-
```

Examples:

- CAN Bus
- RS-485
- LVDS

The resistor value depends on the characteristic differential impedance of the interface.

---

# Choosing the Correct Termination

Termination depends on:

- Interface standard
- Driver characteristics
- Receiver characteristics
- PCB trace length
- Signal frequency
- Rise/Fall time

The correct termination method should always follow the device datasheet or interface specification.

---

# PCB Design Practices

✔ Maintain controlled impedance.

✔ Avoid unnecessary stubs.

✔ Keep signal paths short.

✔ Minimize vias.

✔ Match impedance along the entire path.

✔ Place termination close to the recommended device (source or load, depending on the interface).

✔ Follow manufacturer layout recommendations.

---

# Common Beginner Mistakes

❌ Treating high-speed traces as ordinary wires.

❌ Ignoring transmission line effects.

❌ Using arbitrary resistor values for termination.

❌ Leaving long stubs.

❌ Changing trace width unnecessarily.

❌ Ignoring PCB stackup.

❌ Placing termination far from the recommended location.

---
# Knowledge Check

### Q1. What is a transmission line?

### Q2. When should a PCB trace be treated as a transmission line?

### Q3. What determines the characteristic impedance of a PCB trace?

### Q4. Why do signal reflections occur?

### Q5. What are the effects of signal reflection?

### Q6. What is a stub, and why is it undesirable in high-speed routing?

### Q7. What is the purpose of signal termination?

### Q8. Compare source termination and parallel termination.

### Q9. Why is AC termination used instead of a simple parallel resistor in some applications?

### Q10. Why does USB require controlled impedance even if the PCB trace is only a few centimeters long?

### Q11. How does impedance matching improve signal integrity?

### Q12. Why should termination resistor values come from the interface specification or device datasheet rather than being chosen arbitrarily?

# Real Applications

Transmission line theory is essential in:

- USB
- Ethernet
- HDMI
- PCI Express
- DDR Memory
- SATA
- LVDS
- High-speed SPI
- FPGA interfaces

---

# Key Takeaways

- High-speed PCB traces behave as transmission lines.
- Characteristic impedance is determined by PCB geometry and dielectric properties.
- Impedance mismatches produce signal reflections.
- Reflections degrade signal integrity and communication reliability.
- Proper signal termination minimizes reflections.
- Selecting the correct termination strategy depends on the interface and system requirements.
- Good PCB layout and proper impedance control work together to achieve reliable high-speed communication.
