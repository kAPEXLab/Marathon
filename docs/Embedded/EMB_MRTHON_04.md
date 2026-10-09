# Task 4: Cabin Temperature Monitor

**Problem Statement Title:** Temperature Monitoring and Alert via ADC and UART  
**Problem Statement ID:** EMB_MRTHON_04  
**Peripherals Used:** ADC (ADC1), UART (UART2)

---

## Scenario Introduction

In automotive climate control systems, monitoring cabin temperature is essential for passenger comfort and safety. During diagnostics or runtime monitoring, embedded systems must read temperature sensors, respond to service commands, and trigger alerts when thresholds are exceeded.

This task simulates a cabin temperature monitoring system using an LM35 analog sensor. The microcontroller reads temperature via ADC and communicates with a service tool over UART. Technicians can request temperature readings, set alert thresholds, and receive automatic alerts when the cabin temperature exceeds the configured limit.

This exercise reinforces analog-to-digital conversion, UART command parsing, and threshold-based alerting—core skills in embedded diagnostics and environmental monitoring.

---

## Implementation Details

### Peripheral Configuration:

 ADC1: PA0 configured for single conversion (LM35 sensor input)

 UART2: RX interrupt enabled for command parsing

### System Behavior:

 On UART command 'T' → Read ADC, convert to temperature, send “Temp: XX°C” via UART

 On UART command 'L' → Update alert threshold (e.g., 'L' sets threshold to 70°C)

&nbsp;&nbsp;&nbsp;&nbsp;o Respond with ACK: Threshold = XX°C

 If temperature exceeds threshold → Send ALERT: Temp High! automatically via UART

 On UART command 'S' → Send current temperature and threshold status

 On UART command 'F' → Simulate sensor fault or disconnection

&nbsp;&nbsp;&nbsp;&nbsp;o Respond with Temp: 0°C or Error

 On system restart → Default threshold should be 25°C

---

## Expected Output and Test Cases

| Test Case No. | Description | Input | Expected Output (UART) | Remarks |
|--------------|-------------|--------|------------------------|---------|
| TC01 | Read temperature | 'T' | Temp: XX°C | Correct ADC conversion |
| TC02 | Set threshold | 'L' | ACK: Threshold = 25°C | Threshold updated |
| TC03 | Alert on high temp | AUTO | ALERT: Temp High! | Automatic alert |
| TC04 | Sensor disconnected | 'F' | Temp: 0°C or Error | Fault handling |
| TC05 | Threshold change test | 'R' | ACK + Temp: XX°C | Dynamic threshold applied |
