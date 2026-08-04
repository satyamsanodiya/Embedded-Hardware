# Testability Principles and Test Point Design

# Overview

After understanding the purpose of Design for Testability (DFT), the next step is learning how to make a PCB physically accessible for testing.

A PCB may function correctly electrically, but without accessible measurement locations, engineers cannot efficiently verify voltages, debug communication interfaces, program the microcontroller, or diagnose manufacturing defects.

Test points are dedicated locations on a PCB that allow engineers or automated test equipment (ATE) to probe electrical signals without disturbing the circuit.

Properly planned test points significantly reduce debugging time, simplify production testing, and improve long-term maintainability.

---

# What is a Test Point?

A test point is a dedicated exposed copper pad or plated feature on a PCB that allows measurement of an electrical signal during debugging, manufacturing, or servicing.

Instead of touching a tiny IC pin with an oscilloscope probe,

the engineer measures the signal using the test point.

Example

```

STM32 GPIO

|

|

O ← Test Point

|

|

Signal Trace

```

The test point becomes the measurement location while the actual circuit remains undisturbed.

---

# Why Test Points are Necessary

Imagine debugging a PCB where every signal exists only on fine-pitch IC pins.

Problems include:

- Oscilloscope probe cannot reach the pin.
- Probe slips and shorts adjacent pins.
- Measurements become unreliable.
- Debugging consumes excessive time.

Adding properly placed test points eliminates these issues.

---

# Objectives of Test Point Design

A well-designed PCB should allow engineers to:

- Measure power rails
- Verify reset operation
- Observe clock signals
- Debug communication buses
- Measure analog voltages
- Program the MCU
- Perform automated production testing

without modifying the PCB.

---

# When Should Test Points Be Planned?

Many beginners place test points after routing.

Professional designers plan them much earlier.

Recommended workflow

```
Circuit Design
        │
        ▼
Component Placement
        │
        ▼
Power Planning
        │
        ▼
Test Point Planning
        │
        ▼
Routing
        │
        ▼
Design Review
```

Planning test points before routing ensures that important signals remain accessible.

---

# Characteristics of a Good Test Point

A good test point should be:

✔ Easily accessible

✔ Clearly labeled

✔ Mechanically strong

✔ Free from solder mask

✔ Large enough for the intended probe

✔ Located away from tall components

✔ Easy to identify during debugging

---

# Types of Test Points

Different signals require different test points.

Typical categories include:

### Power Test Points

Used for measuring:

- VIN
- 12V
- 5V
- 3.3V
- 1.8V

Example

```
TP1

3V3
```

---

### Ground Test Points

Ground is required as the reference for almost every electrical measurement.

At least one easily accessible GND test point should always be provided.

Example

```
TP_GND
```

---

### Reset Test Point

Reset circuits are frequently checked during board bring-up.

Providing a RESET test point allows engineers to verify:

- Reset pulse
- Reset timing
- Reset stability

Example

```
TP_RST
```

---

### Clock Test Point

Clock signals are among the first signals checked when a microcontroller fails to start.

Example

```
Crystal

↓

MCU

↓

TP_CLK
```

This allows the engineer to verify oscillator operation using an oscilloscope.

---

### Communication Test Points

Communication buses often require dedicated test points.

Examples include:

- UART TX
- UART RX
- SPI CLK
- SPI MOSI
- SPI MISO
- SPI CS
- I²C SDA
- I²C SCL
- CAN TX
- CAN RX

These greatly simplify protocol analysis using a logic analyzer.

---

### Analog Test Points

Analog signals should also be accessible.

Examples include:

- Sensor output
- ADC input
- Reference voltage
- Amplifier output

These are especially important in mixed-signal systems.

---

# Power Rail Test Points

Every important supply voltage should have its own test point.

Example

```
Battery

↓

Buck Converter

↓

5V

↓

TP_5V

↓

LDO

↓

3.3V

↓

TP_3V3
```

During bring-up,

engineers verify:

✔ Voltage level

✔ Ripple

✔ Startup sequence

✔ Current consumption

---

# Ground Test Points

Ground is the reference for almost every oscilloscope or multimeter measurement.

Best practice:

Provide multiple ground test points across the PCB.

Benefits:

- Easier probing
- Shorter ground leads
- More accurate measurements
- Reduced measurement noise

---

# Reset Test Points

The RESET signal is commonly used during:

- Initial bring-up
- Firmware programming
- Fault diagnosis

A dedicated RESET test point allows engineers to verify:

- Reset pulse width
- Power-on reset
- Brown-out reset
- External reset circuit

---

# Communication Interface Test Points

Communication buses frequently require debugging.

Examples:

UART

```
TP_TX

TP_RX
```

SPI

```
TP_CLK

TP_MOSI

TP_MISO

TP_CS
```

I²C

```
TP_SCL

TP_SDA
```

CAN

```
TP_CAN_TX

TP_CAN_RX
```

These points simplify protocol verification with a logic analyzer.

---

# Analog Signal Test Points

Analog measurements require clean probe access.

Examples:

```
Pressure Sensor Output

↓

TP_PRESSURE
```

```
Temperature Sensor

↓

TP_TEMP
```

```
ADC Reference

↓

TP_VREF
```

These help verify sensor operation and analog front-end performance.

---

# Test Point Placement Guidelines

Good placement is just as important as having test points.

Professional guidelines:

✔ Place test points on the same PCB side whenever practical.

✔ Keep them accessible after assembly.

✔ Avoid placing them beneath connectors.

✔ Avoid placing them beneath large ICs.

✔ Leave enough spacing for probes.

✔ Group related test points together.

✔ Clearly identify every test point with silkscreen.

---

# Test Point Labeling

Every test point should have a meaningful reference.

Examples:

```
TP_3V3

TP_GND

TP_RST

TP_UART_TX

TP_CAN_RX

TP_TEMP
```

Avoid generic names such as:

```
TP1

TP2

TP3
```

Meaningful labels greatly simplify debugging.

---

# High-Speed Test Point Considerations

Not every signal should have a traditional test point.

Adding a test point to a high-speed signal can create:

- Impedance discontinuity
- Signal reflection
- Additional stub
- Increased EMI
- Signal degradation

Examples include:

- USB D+ / D−
- Ethernet
- PCIe
- DDR
- HDMI

If test access is required for these interfaces, follow the device or interface layout guidelines and minimize any impact on the transmission line.

---

# Common Test Point Mistakes

❌ No ground test point

❌ Missing power rail test points

❌ Test points hidden under components

❌ Poor silkscreen labeling

❌ Test points too close together

❌ No access to communication buses

❌ Adding unnecessary stubs to high-speed traces

❌ Planning test points only after routing

---

# Practical Example

Example of a professional MCU board:

```
          USB

           │

 STM32 MCU

TP_RST   TP_SWD

TP_3V3   TP_GND

TP_UART_TX

TP_UART_RX

TP_CAN_TX

TP_CAN_RX

Power Section

TP_12V

TP_5V

TP_3V3
```

Every important signal can be measured without touching fine-pitch IC pins.

---

# Engineering Checklist

Before finalizing the PCB, verify:

- [ ] Every power rail has a test point.
- [ ] Multiple GND test points are available.
- [ ] RESET signal is accessible.
- [ ] Programming interface is reachable.
- [ ] Communication buses can be monitored.
- [ ] Analog signals are accessible where needed.
- [ ] Test points are clearly labeled.
- [ ] Probe spacing is sufficient.
- [ ] High-speed interfaces follow their layout recommendations.
- [ ] Test points remain accessible after assembly.

---

# Key Takeaways

- Test points are essential for efficient debugging and manufacturing.
- Important power, reset, clock, communication, and analog signals should be accessible.
- Test points should be planned before routing begins.
- Proper placement and labeling improve development, production testing, and field servicing.
- High-speed signals require special consideration because poorly placed test points can affect signal integrity.
