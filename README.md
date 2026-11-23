
# Single-Phase Improved Power Quality Rectifier for EV Charging

### Design and Simulation of a Single-Phase Boost PFC Converter Using PLECS

**Project Status:** Under Development  
**Simulation Software:** PLECS  
**Domain:** Power Electronics | EV Charging | Power Quality

---

## 1. Project Overview

This project focuses on the design and simulation of a **Single-Phase Improved Power Quality Rectifier for EV Charging** using a diode bridge rectifier followed by a boost converter.

The system is designed to convert a **12 V RMS AC input into a regulated 48 V DC output**, delivering approximately **24 W** to a resistive load.

The main objectives are to:

- Maintain a regulated DC output voltage.
- Investigate input power factor improvement.
- Reduce input current harmonic distortion.
- Minimise output voltage ripple.
- Study closed-loop PWM control.
- Evaluate converter performance using PLECS.

The project is currently at the simulation and design-validation stage, with a proposed hardware implementation using an ESP32 microcontroller.

---

## 2. Problem Statement

Conventional single-phase diode rectifiers with capacitive filtering can draw distorted input currents, resulting in poor power factor and increased harmonic distortion.

These issues affect power quality and may increase electrical losses.

To address these challenges, this project investigates a boost Power Factor Correction (PFC) rectifier that aims to provide a regulated DC output while improving the quality of the input current.

---

## 3. Project Objectives

1. Design a single-phase AC-to-DC rectifier.
2. Develop a boost converter for voltage regulation.
3. Obtain a regulated 48 V DC output from 12 V AC.
4. Investigate power factor improvement.
5. Analyse input current harmonic distortion.
6. Minimise DC output voltage ripple.
7. Implement closed-loop PWM-based control.
8. Evaluate converter performance through simulation.

---

## 4. System Specifications

| Parameter | Specification |
|---|---|
| Converter Topology | Diode Bridge + Boost Converter |
| Proposed Primary Supply | 230 V AC, 50 Hz |
| Proposed Transformer | 230 V / 12 V, 5 A |
| Simulation Input | 12 V RMS AC |
| Input Peak Voltage | 16.970 V |
| Target Output Voltage | 48 V DC |
| Load Resistance | 96 ohms |
| Target Output Current | 0.5 A |
| Target Output Power | 24 W |
| Boost Inductor | 1 microhenry (1 µH) |
| Output Capacitor | 100 microfarads (100 µF) |
| Switching Frequency | 100 kHz |
| Switching Period | 10 microseconds |
| Ideal Duty Cycle at Input Peak | 64.65% |
| Duty Cycle Limits | 5% to 95% |
| Simulation Software | PLECS |
| Proposed Hardware Controller | ESP32 |

**Note:** The inductor and capacitor values are from the current simulation model. Their suitability requires further verification.

---

## 5. System Architecture

### 5.1 Power Flow

    Single-Phase AC Supply
              |
              v
       Bridge Rectifier
              |
              v
         Boost Inductor
              |
              v
       Boost Converter
      (MOSFET and Diode)
              |
              v
       DC-Link Capacitor
              |
              v
         48 V DC Output
              |
              v
         96-ohm Load

### 5.2 Feedback Control

    48 V Reference Voltage
              |
              v
       Error Calculation <------ Output Voltage Feedback
              |
              v
       Feedback Controller
              |
              v
         PWM Generator
              |
              v
       MOSFET Gate Signal
              |
              v
         Boost Converter

The feedback controller compares the measured output voltage with the reference voltage and adjusts the MOSFET switching duty cycle.

---

## 6. Working Principle

### Step 1: AC Input

The proposed hardware uses a 230 V, 50 Hz AC supply stepped down to 12 V AC using a 5 A transformer.

The simulation uses a low-voltage sinusoidal AC source.

### Step 2: Rectification

A full-bridge diode rectifier converts the AC supply into a pulsating DC voltage.

### Step 3: Boost Conversion

The boost converter consists of:

- Boost inductor
- MOSFET switch
- Boost diode
- DC-link capacitor

**MOSFET ON:** The inductor stores energy.

**MOSFET OFF:** The inductor releases energy through the boost diode to the output capacitor and load.

### Step 4: Voltage Regulation

The output voltage is continuously measured and compared with the 48 V reference.

The feedback controller adjusts the PWM duty cycle to reduce the voltage error.

### Step 5: Load Supply

The regulated output is supplied to a 96-ohm resistive load.

At the target voltage, the load consumes approximately 24 W.

---

## 7. Design Calculations

### 7.1 Input RMS Voltage

Given:

- Peak input voltage = 16.970 V
- RMS voltage = Peak voltage / sqrt(2)

Calculation:

    Vrms = Vm / sqrt(2)

    Vrms = 16.970 / 1.4142

    Vrms = 12.00 V

**Result: Input RMS Voltage = 12 V**

---

### 7.2 Output Current

Given:

- Output voltage = 48 V
- Load resistance = 96 ohms

Using Ohm's Law:

    Io = Vo / R

    Io = 48 / 96

    Io = 0.5 A

**Result: Output Current = 0.5 A**

---

### 7.3 Output Power

Given:

- Output voltage = 48 V
- Output current = 0.5 A

Formula:

    Po = Vo x Io

Calculation:

    Po = 48 x 0.5

    Po = 24 W

**Result: Output Power = 24 W**

---

### 7.4 Ideal Boost Converter Duty Cycle

For an ideal boost converter:

    Vo = Vin / (1 - D)

Rearranging:

    D = 1 - (Vin / Vo)

At the peak rectified input voltage:

    Vin = 16.970 V
    Vo  = 48 V

Calculation:

    D = 1 - (16.970 / 48)

    D = 1 - 0.35354

    D = 0.64646

    D = 64.65%

**Result: Ideal Duty Cycle at Input Peak = 64.65%**

**Note:** This is an ideal estimate at the peak of the rectified AC waveform. The actual duty cycle varies during operation.

---

### 7.5 Switching Frequency and Period

Given:

    fs = 100 kHz

    fs = 100,000 Hz

Formula:

    Ts = 1 / fs

Calculation:

    Ts = 1 / 100,000

    Ts = 0.00001 seconds

    Ts = 10 microseconds

**Result: Switching Period = 10 microseconds**

---

### 7.6 Transformer Rating

Proposed transformer specifications:

- Primary voltage = 230 V AC
- Secondary voltage = 12 V AC
- Secondary rated current = 5 A

Formula:

    Apparent Power = Voltage x Current

Calculation:

    S = 12 x 5

    S = 60 VA

**Result: Transformer Rating = 60 VA**

The 5 A transformer provides additional current capacity for the proposed 24 W converter.

Actual transformer loading must be verified using RMS input current and thermal measurements.

---

### 7.7 Output Voltage Error

Reported simulation output voltage:

    Vo = 48.0368 V

Reference voltage:

    Vref = 48 V

Formula:

    Percentage Error = |Vo - Vref| / Vref x 100

Calculation:

    Error = |48.0368 - 48| / 48 x 100

    Error = 0.0368 / 48 x 100

    Error = 0.0767%

**Result: Output Voltage Error = 0.0767%**

---

## 8. Simulation Model

The system is modelled using PLECS.

### Main Components

| Component | Function |
|---|---|
| AC Voltage Source | Provides sinusoidal AC input |
| Bridge Rectifier | Converts AC into pulsating DC |
| Boost Inductor | Stores and transfers energy |
| MOSFET | Controls switching operation |
| Boost Diode | Transfers energy to output |
| DC-Link Capacitor | Smooths DC output voltage |
| Resistive Load | Represents laboratory test load |
| Feedback Controller | Regulates output voltage |
| PWM Generator | Produces MOSFET gate pulses |
| Measurement Blocks | Monitor voltage and current |

### Simulation Procedure

1. Configure the single-phase AC input.
2. Connect the diode bridge rectifier.
3. Design the boost converter circuit.
4. Set the output reference to 48 V.
5. Configure the feedback controller.
6. Generate PWM signals at 100 kHz.
7. Connect the 96-ohm resistive load.
8. Run the PLECS simulation.
9. Observe output voltage and current.
10. Evaluate ripple, power factor and THD.

---

## 9. Simulation Results

### 9.1 Output Voltage

Reported simulation output:

    Output Voltage = 48.0368 V

Target output:

    Reference Voltage = 48 V

Percentage deviation:

    Voltage Error = 0.0767%

### 9.2 Output Current

Using the reported output voltage:

    Io = Vo / R

    Io = 48.0368 / 96

    Io = 0.50038 A

**Calculated Output Current = 0.5004 A**

### 9.3 Output Power

Formula:

    Po = Vo x Io

Calculation:

    Po = 48.0368 x 0.50038

    Po = 24.0368 W

**Calculated Output Power = 24.04 W**

### 9.4 Performance Summary

| Parameter | Result |
|---|---|
| Reference Voltage | 48 V |
| Reported Output Voltage | 48.0368 V |
| Output Voltage Error | 0.0767% |
| Calculated Output Current | 0.5004 A |
| Calculated Output Power | 24.04 W |
| Input Power Factor | To be measured |
| Input Current THD | To be measured |
| Output Voltage Ripple | To be evaluated |
| Converter Efficiency | To be calculated |

**Note:** The output voltage is a reported simulation reading. Current and power are calculated using the specified resistive load.

Improved power factor and reduced THD remain design objectives until verified through simulation measurements.

---

## 10. Proposed Hardware Implementation

The proposed hardware setup includes:

1. 230 V / 12 V, 5 A step-down transformer
2. Full-bridge diode rectifier
3. Boost inductor
4. Power MOSFET
5. Boost diode
6. Output capacitor
7. ESP32 microcontroller
8. Voltage sensing circuit
9. Current sensing circuit
10. MOSFET gate driver
11. Resistive load
12. Electrical protection components

The ESP32 is proposed for PWM generation, voltage regulation and electrical parameter monitoring.

The prototype is intended for controlled indoor laboratory testing.

---

## 11. Performance Evaluation

The converter will be evaluated using the following parameters.

### Output Voltage Regulation

Measures how closely the output follows the 48 V reference.

### Output Voltage Ripple

Measures fluctuations in the DC output voltage.

### Input Power Factor

Evaluates how effectively the converter draws real power from the AC supply.

### Total Harmonic Distortion (THD)

Measures harmonic distortion in the input current waveform.

### Conversion Efficiency

Formula:

    Efficiency (%) = (Output Power / Input Power) x 100

Efficiency will be calculated after measuring the actual input power.

---

## 12. Applications

- Power electronics laboratory experiments
- Boost converter design
- AC-to-DC conversion studies
- Power factor correction research
- PWM-based voltage regulation
- EV charging power-conversion education
- Converter simulation and analysis

---

## 13. Future Scope

- Optimise the boost inductor and output capacitor.
- Verify the converter's conduction mode.
- Implement digital control using ESP32.
- Develop input-current shaping control.
- Measure input power factor and current THD.
- Evaluate conversion efficiency.
- Study voltage sag and swell conditions.
- Add overvoltage and overcurrent protection.
- Build and test a laboratory hardware prototype.

---

## 14. Tools and Technologies

| Tool | Purpose |
|---|---|
| PLECS | Power electronics simulation |
| Power Electronics | Converter design |
| PWM | Switching control |
| Feedback Control | Output voltage regulation |
| ESP32 | Proposed hardware control |
| HTML/CSS | Project website |
| GitHub | Version control and documentation |

---

## 15. Project Status

**Current Stage: Design and Simulation**

### Documented Work

- [x] Problem definition
- [x] System architecture
- [x] Initial boost converter model
- [x] Preliminary design calculations
- [x] Closed-loop voltage control approach
- [x] Initial output-voltage simulation result

### Pending Work

- [ ] Validate input source frequency
- [ ] Optimise boost inductor and capacitor
- [ ] Measure input power factor
- [ ] Calculate input current THD
- [ ] Evaluate output voltage ripple
- [ ] Calculate converter efficiency
- [ ] Implement and test hardware

---

## 16. Project Portfolio

**Project Website:**

https://sites.google.com/kletech.ac.in/pfc/home

---

## 17. Institution

**KLE Technological University**

Department of Electrical and Electronics Engineering

---

## 18. Disclaimer

This project is intended for academic and educational purposes.

The converter represents a laboratory-scale AC-to-DC power conversion system and is not a complete or certified EV battery charger.

Practical implementation requires electrical isolation, component-rating verification, protection circuits and safe testing procedures.

---

## License

This project is intended for academic and educational use.

A license may be added to the repository to define permissions for reuse and distribution.
