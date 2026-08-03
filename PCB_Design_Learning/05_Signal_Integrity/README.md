# 05 - Signal Integrity

# Overview

Signal Integrity (SI) is the study of how electrical signals propagate through a PCB while maintaining their original shape, timing, and voltage levels.

In low-speed circuits, PCB traces are often treated as simple copper connections. However, as signal frequency and edge rates increase, traces begin behaving as transmission lines. At this point, PCB layout becomes just as important as the schematic itself.

Poor signal integrity can result in communication failures, timing errors, electromagnetic interference (EMI), and unreliable system behavior.

Understanding signal integrity is therefore one of the most important skills in modern PCB design.

---

# Learning Objectives

After completing this chapter, I understood:

- What Signal Integrity (SI) is
- Why SI becomes important in high-speed PCB design
- Reflection
- Ringing
- Crosstalk
- Electromagnetic Interference (EMI)
- Return Current Path
- PCB Layer Pairing
- Signal Integrity Design Practices

---

# What is Signal Integrity?

Signal Integrity refers to the quality of an electrical signal as it travels from the transmitter to the receiver.

An ideal digital signal should arrive at the receiver:

- With the correct voltage
- At the correct time
- Without distortion
- Without excessive noise

Example of an ideal signal:

```

HIGH ────────────────

LOW  ________________

```

A poor PCB layout causes the signal to become distorted.

Example:

```

HIGH ────/\~~~~\_____

LOW  ___/        \___

```

The receiver may interpret this incorrectly, leading to communication errors.

---

# Why Signal Integrity Matters

Modern digital interfaces such as:

- USB
- Ethernet
- HDMI
- DDR Memory
- PCIe
- LVDS

operate at very high switching speeds.

Even though these signals represent simple logic levels (0 and 1), they contain very high-frequency components due to their fast rise and fall times.

As switching speed increases:

- PCB trace inductance becomes significant.
- PCB trace capacitance becomes significant.
- Signal reflections occur.
- Crosstalk increases.
- EMI increases.
- Timing margins reduce.

Therefore, maintaining signal integrity becomes critical.

---

# Major Signal Integrity Problems

The most common signal integrity issues are:

- Reflection
- Ringing
- Crosstalk
- Electromagnetic Interference (EMI)
- Ground Bounce
- Timing Errors

Each of these problems is explained below.

---

# Reflection

## What is Reflection?

Reflection occurs when a signal encounters a sudden change in impedance along its transmission path.

Imagine throwing a wave along a rope.

If the rope suddenly becomes thicker, part of the wave travels forward while another part reflects backward.

Exactly the same phenomenon occurs inside PCB traces.

Example:

MCU

```
│
├──────────── Trace ───────────── Receiver
                     ↑
            Impedance Change
```

Instead of the entire signal reaching the receiver,

Part of the signal returns toward the transmitter.

```
Forward Signal  →→→→→→

←←← Reflected Signal
```

---

## Causes of Reflection

Reflection may occur due to:

- Sudden trace width changes
- Layer transitions
- Long vias
- PCB connectors
- Improper termination
- Stubs
- Split reference planes

---

## Effects of Reflection

Reflection causes:

- Overshoot
- Undershoot
- Ringing
- Timing errors
- Communication failure

---

## How to Reduce Reflection

✔ Maintain constant trace width

✔ Use controlled impedance routing

✔ Keep vias to a minimum

✔ Remove unnecessary stubs

✔ Use proper termination where required

✔ Route over continuous reference planes

---

# Ringing

## What is Ringing?

Ringing is the oscillation that appears after a signal transition.

Instead of switching cleanly,

```
HIGH ───────────

LOW ____________
```

the signal oscillates before stabilizing.

```
HIGH ──/\~~~~\____

LOW ___/
```

Ringing is usually caused by reflections.

---

## Problems Caused by Ringing

- False logic transitions

- Increased EMI

- Timing uncertainty

- Receiver errors

---

## Methods to Reduce Ringing

- Controlled impedance

- Series termination

- Reduce trace length

- Avoid impedance discontinuities

---

# Crosstalk

## What is Crosstalk?

Crosstalk is unwanted electromagnetic coupling between adjacent PCB traces.

Example

```
Clock Trace
=====================

Victim Trace
=====================
```

The switching clock induces noise onto the neighboring trace.

---

## Types of Crosstalk

### Capacitive Coupling

Occurs due to electric field interaction.

---

### Inductive Coupling

Occurs due to magnetic field interaction.

---

## Effects

- Noise

- Data corruption

- Jitter

- Communication errors

---

## Reducing Crosstalk

✔ Increase spacing between traces

✔ Reduce parallel routing distance

✔ Route adjacent layers orthogonally

✔ Use continuous ground planes

✔ Separate noisy signals from sensitive analog signals

---

# Electromagnetic Interference (EMI)

## What is EMI?

EMI is unwanted electromagnetic energy emitted by high-speed switching circuits.

Every fast-changing current produces electric and magnetic fields.

If not controlled, these fields radiate into surrounding circuits.

---

## Common EMI Sources

- USB

- Clock signals

- SPI

- Ethernet

- Switching regulators

- Long PCB traces

---

## Effects

- Communication errors

- Noise coupling

- Regulatory compliance failure

- Reduced product reliability

---

## EMI Reduction Techniques

✔ Solid ground plane

✔ Small loop area

✔ Decoupling capacitors

✔ Series resistors

✔ Controlled impedance routing

✔ Shielding

✔ Proper layer stackup

---

# Return Current Path

One of the most important concepts in high-speed PCB design is the return current path.

Many beginners assume current always returns through the shortest distance.

This is incorrect.

High-frequency current returns through the path of **lowest impedance**.

Example:

```
Signal

========================>

Ground Plane

<<<<<<<<<<<<<<<<<<<<<<<<
```

The return current flows directly underneath the signal trace.

This minimizes loop area.

---

# Why Small Loop Area is Important

Smaller loop area means:

- Lower EMI

- Lower inductance

- Better signal integrity

- Reduced noise

---

If the signal crosses a split ground plane,

```
Signal
======================>

Ground Plane

██████ Gap ███████

Return Current

<<<<<<<<<<<
          \
           \
            <<<<<<
```

the return current must detour around the gap.

This creates:

- Large loop area

- Higher EMI

- More noise

- Signal distortion

---

# PCB Layer Pairing

Correct Layer Pairing

```
Signal

Ground
```

Incorrect

```
Signal

Power

Signal
```

Every high-speed signal should have a solid reference plane immediately adjacent to it.

---

# Signal Integrity Design Guidelines

✔ Maintain continuous ground planes

✔ Avoid split reference planes

✔ Keep high-speed traces short

✔ Route differential pairs together

✔ Minimize vias

✔ Keep return current continuous

✔ Maintain consistent trace width

✔ Reduce parallel routing

✔ Keep clocks isolated

✔ Plan PCB stackup before routing

---
# Knowledge Check

### Q1. What is Signal Integrity?

### Q2. Why is Signal Integrity more important in high-speed circuits than low-speed circuits?

### Q3. What causes signal reflection?

### Q4. What is ringing, and how is it related to reflection?

### Q5. Explain the difference between capacitive and inductive crosstalk.

### Q6. Why does a solid ground plane improve signal integrity?

### Q7. Why does a split ground plane increase EMI?

### Q8. What path does high-frequency return current follow?

### Q9. Why should high-speed traces have a continuous reference plane?

### Q10. List five PCB layout practices that improve signal integrity.

# Real Applications

Signal integrity is critical in:

- USB

- Ethernet

- DDR Memory

- PCIe

- HDMI

- DisplayPort

- MIPI

- FPGA boards

---

# Key Takeaways

- PCB traces behave as transmission lines.

- Signal quality depends heavily on PCB layout.

- Reflection is caused by impedance discontinuities.

- Crosstalk occurs due to electromagnetic coupling.

- High-speed return current follows the path of lowest impedance.

- Ground planes play a major role in maintaining signal integrity.

- Good PCB layout is essential for reliable high-speed communication.
