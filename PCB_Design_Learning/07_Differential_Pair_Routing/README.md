# 07 - Differential Pair Routing

# Overview

Many modern communication interfaces such as USB, Ethernet, HDMI, PCI Express, LVDS, and MIPI use **Differential Signaling** instead of transmitting data over a single conductor.

Instead of carrying information on one signal referenced to ground, differential signaling transmits the same information using two complementary signals.

The receiver detects the voltage difference between these two signals rather than measuring either signal individually with respect to ground.

Because of this operating principle, differential signaling provides excellent noise immunity, lower EMI, higher data rates, and improved signal integrity.

This chapter explains the theory behind differential signaling, differential pair routing, differential impedance, pair coupling, skew, length matching, and routing practices used in professional PCB design.

---

# Learning Objectives

After completing this chapter I understood:

- Why differential signaling is used
- Difference between single-ended and differential signaling
- Common Mode Voltage
- Differential Mode Voltage
- Differential Pair Coupling
- Differential Impedance
- Pair Skew
- Length Matching
- Differential Pair Routing Rules
- USB Differential Pair Routing
- KiCad Differential Pair Routing Workflow

---

# What is Differential Signaling?

In single-ended communication, information is transmitted using one signal referenced to ground.

Example

```

GPIO
|

====================

Ground

████████████████████

```

The receiver measures:

```

Signal − Ground

```

In differential signaling,

two signals are transmitted simultaneously.

```

D+

=====================>

D-

<=====================

```

The receiver measures

```

D+ − D-

```

instead of

```

Signal − Ground

```

This makes differential signaling significantly more immune to external noise.

---

# Why Use Differential Signaling?

Suppose electrical noise is coupled onto both PCB traces.

```

Noise

↓

D+

↓

D-

```

Since both signals receive nearly the same noise,

the receiver calculates

```

(D+ + Noise)

−

(D− + Noise)

```

The noise cancels.

Only the useful signal remains.

This phenomenon is called

**Common Mode Noise Rejection.**

---

# Single-Ended vs Differential Signaling

| Single Ended | Differential |
|--------------|--------------|
| One signal | Two complementary signals |
| Referenced to Ground | Referenced to each other |
| Higher EMI | Lower EMI |
| More susceptible to noise | Better noise immunity |
| Simpler routing | Requires matched routing |
| Suitable for lower speed | Preferred for high-speed communication |

---

# Differential Pair

A differential pair consists of two PCB traces routed together.

Example

```

USB D+

=========================>

USB D-

=========================>

```

The two traces should behave as one transmission structure.

They should never be treated as independent traces.

---

# Differential Mode Voltage

When transmitting data,

one line increases,

while the other decreases.

Example

```

D+

+0.2V

D-

-0.2V

```

Receiver measures

```

VDIFF

=

D+

−

D-

```

This is called

**Differential Mode Voltage.**

---

# Common Mode Voltage

Sometimes external interference affects both traces equally.

```

Noise

↓

D+

↓

D-

```

Both traces shift upward.

Example

```

D+

+0.6V

D-

+0.2V

```

Although both voltages changed,

their difference remains nearly unchanged.

This is

**Common Mode Voltage.**

Differential receivers reject this common-mode component.

---

# Differential Pair Coupling

The two traces intentionally interact through their electric and magnetic fields.

```

======================

<----Spacing---->

======================

```

This interaction is called

**Coupling.**

Coupling depends upon:

- Trace spacing
- Trace width
- Distance to reference plane
- PCB dielectric

Closer traces

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

# Why Maintain Constant Spacing?

If spacing changes,

coupling changes.

When coupling changes,

differential impedance changes.

When impedance changes,

reflection occurs.

Therefore,

spacing should remain constant throughout routing.

---

# Differential Impedance

Unlike single-ended routing,

differential routing has two impedance values.

Single-ended impedance

Approximately

```

45 Ω

```

Differential impedance

Approximately

```

90 Ω

```

USB 2.0 requires

```

90 Ω ±10%

Differential Impedance

```

This value depends upon PCB stackup.

---

# Pair Skew

Pair skew is the difference in arrival time between the two traces.

Example

Wrong

```

D+

=====================

D-

==============================

```

One signal arrives earlier.

Receiver sees distorted data.

---

Correct

```

D+

====================

D-

====================

```

Both arrive simultaneously.

---

# Why Length Matching Matters

Equal length ensures:

- Same propagation delay
- Same timing
- Better eye diagram
- Reliable communication

Length matching is especially important for

- USB

- Ethernet

- LVDS

- DDR

---

# Differential Pair Routing Rules

Professional routing practices include:

✔ Route both traces together.

✔ Maintain constant spacing.

✔ Maintain constant width.

✔ Match lengths.

✔ Minimize vias.

✔ Route above continuous ground plane.

✔ Avoid routing across plane splits.

✔ Keep differential pair away from noisy circuits.

✔ Avoid sharp bends.

✔ Avoid unnecessary stubs.

---

# Layer Changes

Whenever possible,

avoid changing PCB layers.

Every via introduces:

- Small impedance discontinuity
- Additional inductance
- Reflection
- Manufacturing complexity

If a layer change is unavoidable,

both traces should transition together.

---

# Differential Pair Bends

Avoid

90°

```

────────┐

        │

```

Preferred

45°

```

────────╲

         ╲

```

Best

Arc

```

────────)

```

Smooth bends help maintain more consistent impedance.

---

# Reference Plane

A differential pair should always be routed above

a continuous reference plane.

```

USB D+

======================

USB D-

======================

Ground Plane

██████████████████████

```

Never cross

- Plane splits

- Plane gaps

- Disconnected reference planes

---

# USB Differential Pair Routing

USB uses

```

D+

D-

```

Typical routing strategy

```

USB Connector

↓

ESD Protection

↓

USB Differential Pair

↓

USB-UART Controller

```

Design Rules

✔ Keep pair short.

✔ Keep spacing constant.

✔ Route together.

✔ Minimize vias.

✔ Keep away from switching regulator.

✔ Maintain 90 Ω differential impedance.

✔ Keep over solid ground plane.

---

# KiCad Differential Pair Routing

KiCad supports interactive differential pair routing.

Workflow

1.

Define Net Classes

↓

2.

Specify

- Width

- Gap

↓

3.

Assign Differential Pair

↓

4.

Use Interactive Router

↓

5.

Length Tune

↓

6.

Run DRC

---

# Common Routing Mistakes

❌ Different trace lengths

❌ Different number of vias

❌ Variable spacing

❌ Crossing split planes

❌ Sharp corners

❌ Routing close to switching regulators

❌ Breaking return current path

❌ Forgetting impedance calculations

---
# Knowledge Check

### Q1. What is differential signaling?

### Q2. Why is differential signaling preferred over single-ended signaling?

### Q3. Explain Common Mode Voltage.

### Q4. Explain Differential Mode Voltage.

### Q5. What is differential impedance?

### Q6. Why does USB require a 90 Ω differential impedance?

### Q7. Why should differential pair spacing remain constant?

### Q8. What is pair skew?

### Q9. Why should differential pair lengths be matched?

### Q10. Why should differential pairs always be routed above a solid ground plane?

### Q11. Why should both traces use the same number of vias?

### Q12. List five routing rules for USB differential pairs.

# Real Applications

Differential routing is used in:

- USB

- Ethernet

- HDMI

- DisplayPort

- PCI Express

- SATA

- LVDS

- CAN FD

- MIPI

---

# Design Checklist

Before completing differential routing:

- [ ] Differential impedance calculated
- [ ] Pair spacing maintained
- [ ] Trace widths constant
- [ ] Lengths matched
- [ ] Same number of vias
- [ ] Continuous ground plane
- [ ] No plane splits
- [ ] Pair isolated from noisy circuits
- [ ] DRC passed
- [ ] Length tuning completed

---

# Key Takeaways

Differential signaling improves communication reliability by transmitting complementary signals whose voltage difference carries information. Proper differential pair routing requires controlled impedance, constant spacing, matched lengths, continuous reference planes, and careful PCB layout. Following these principles minimizes EMI, improves signal integrity, and enables reliable high-speed communication.
