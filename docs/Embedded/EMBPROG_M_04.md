# ASSESSMENT PROBLEM STATEMENT

| Field | Details |
|---|---|
| **Question Number** | EMBPROG_MARATHON_04 |
| **Scenario** | ADC-polled LM35 temperature alarm with threshold and smoothing |
| **Embedded Systems Concepts** | ADC, UART |
| **C Programming Concepts** | functions |
| **Difficulty Level** | Intermediate |

## Real-world Project Scenario

You’re developing a thermal safety monitor for a 3D printer enclosure. The LM35 sensor feeds the Nucleo; if the enclosure exceeds 40°C, a warning LED turns on.

Students implement ADC polling, temperature conversion, and simple smoothing to avoid flicker. They also add a small hysteresis to provide stable alarm behavior in fluctuating conditions.

## Requirements and Specifications

- **Hardware:** LM35 output connected to PA0 (ADC1 IN0); LED on PA5.
- **Sensor model:** LM35 outputs 10 mV/°C (e.g., 0.45 V ≈ 45°C).
- **ADC config:** 12-bit, single conversion mode, Vref = 3.3 V, sample time adequate for source impedance.

- **Computation:**
  - Temperature in °C = `(ADC_value × 3.3 / 4096) / 0.01`.
  - Use a moving average over last N samples (e.g., N=8) to smooth readings.

- **Thresholding:**
  - Turn LED on when averaged Temp > 25°C.
  - Add hysteresis: turn LED off when Temp < 25°C.

## Tasks to Implement in `main`

- **GPIO init:** PA5 as output.

- **ADC init:** ADC1 channel 0 on PA0; single conversion; right-aligned; appropriate sample time.

- **Acquisition loop:**
  - Start conversion; poll EOC; read DR.
  - Update moving average buffer; compute averaged temperature.
  - Apply hysteresis logic: >25°C → LED on; <25°C → LED off.

- **Optional:** Add a simple LED blink (slow) when sensor disconnected (near 0 V) or readings invalid.

## Test Cases

| Test Case ID | Temp (°C) | Averaging State | Expected LED |
|---|---:|---|---|
| TC001 | ~25 | Stable | Off |
| TC002 | > 25°C | Stable | LED ON |
| TC003 | < 25°C | Stable | LED off |
