# Component Selection

## Selection Philosophy

Component selection was performed based on the following criteria:

* Low power consumption
* Battery-powered operation
* Cost effectiveness
* Ease of integration
* Availability
* Long-term scalability
* Development simplicity

Requirements
↓
Available Options
↓
Tradeoffs
↓
Final Selection

Since the primary objective of this project was to develop a low-power wireless sensor platform, power consumption was treated as a critical design parameter during component evaluation.

---

# BM15M BLE Module

## Purpose

Provides wireless Bluetooth Low Energy communication and serves as the primary processing element of the system.

## Selection Criteria

* BLE communication capability
* Low power operation
* Compact module size
* Integrated wireless stack
* Reduced development effort

## Benefits

* Simplified wireless implementation
* Lower hardware complexity
* Suitable for battery-powered applications

---

# nPM1300 PMIC

## Purpose

Power management and battery charging.

## Selection Criteria

* Li-Ion battery charging support
* USB Type-C compatibility
* Integrated power-path management
* Low quiescent current
* Multiple power management features

## Benefits

* Simplified power architecture
* Reduced component count
* Improved battery management

## Design Impact

The PMIC eliminated the need for multiple discrete power management circuits and significantly reduced design complexity.

---

# Temperature and Humidity Sensor

## Selection Criteria

The selected sensor was required to provide:

* Low current consumption
* Digital interface compatibility
* Compact package
* Reliable environmental measurements

## Design Considerations

As the device is intended for battery-powered operation, low standby and active current consumption were prioritized over maximum measurement speed.

---

# CO2 Sensor

## Selected Device

STCC4-D-R3

Manufacturer: Sensirion

Approximate Cost: ₹500

## Purpose

Measurement of carbon dioxide concentration in the surrounding environment.

## Selection Criteria

### Low Power Consumption

CO2 sensing can significantly impact battery life.

The STCC4-D-R3 was selected because it offers a lower power profile compared to many traditional NDIR-based CO2 sensors.

### Compact Integration

Suitable for portable wireless sensing platforms.

### Digital Interface Support

Simplifies communication with the processing subsystem.

## Design Impact

The selected sensor allows environmental air-quality monitoring while maintaining the low-power design philosophy of the platform.

---

# PIR Sensor

## Selected Device

ZSBG323671

Manufacturer: Zilog

Approximate Cost: ₹70

## Purpose

Human motion detection.

## Selection Criteria

### Ultra-Low Power Operation

PIR sensors typically remain active continuously.

Therefore standby current consumption becomes a critical design parameter.

### Cost Optimization

The selected device provides a low-cost solution suitable for volume deployment.

### Simple Integration

Minimal external circuitry requirements.

## Design Impact

The sensor enables occupancy and motion detection without significantly impacting battery life.

---

# Flow Measurement Sensor

## Selected Device

MP3V5010DP

Manufacturer: NXP

Approximate Cost: ₹1000

## Purpose

Air-flow and differential pressure measurement.

## Selection Criteria

### Measurement Accuracy

Provides suitable sensitivity for low-pressure measurement applications.

### Analog Output

Allows direct interfacing with the processing subsystem.

### Industrial Reliability

Well-established sensor family with proven field usage.

## Design Impact

The sensor expands the platform beyond environmental monitoring and enables air-flow related sensing applications.

---

# SPI Display

## Purpose

Provide local visual feedback and system information.

## Selection Criteria

* SPI communication interface
* Low pin count
* Compact size
* Easy firmware integration

## Design Consideration

The display was included as an optional user interface while maintaining overall system flexibility.

---

# RGB LED

## Purpose

Visual indication of system status.

## Functions

* Power indication
* BLE status indication
* Measurement activity indication
* Fault indication

## Selection Rationale

Provides immediate feedback without requiring a display connection.

---

# External I2C Expansion Interface

## Purpose

Future sensor expansion.

## Design Philosophy

Rather than permanently integrating every possible sensor, a dedicated expansion interface was provided.

Benefits include:

* Easier experimentation
* Faster prototyping
* Reduced redesign effort
* Greater system flexibility

---

# Component Selection Summary

| Component                     | Purpose                               |
| ----------------------------- | ------------------------------------- |
| BM15M                         | BLE Communication and Processing      |
| nPM1300                       | Battery Charging and Power Management |
| Temperature & Humidity Sensor | Environmental Monitoring              |
| STCC4-D-R3                    | CO2 Measurement                       |
| ZSBG323671                    | Motion Detection                      |
| MP3V5010DP                    | Air Flow Measurement                  |
| SPI Display                   | User Interface                        |
| RGB LED                       | Status Indication                     |
| External I2C Connector        | Future Expansion                      |

---

# Selection Outcome

The final component selection aligns with the primary objective of creating a low-power, battery-operated wireless sensing platform.

Particular emphasis was placed on reducing power consumption while maintaining flexibility for future sensor integration and application expansion.
