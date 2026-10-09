# Task 2: Engine Fault Indicator (GPIO Interrupt + UART)

**Problem Statement Title:** Engine Fault Alert with Interrupt and UART

**Problem Statement ID:** EMB_MRTHON_02

**Peripherals Used:** GPIO (Interrupt), Timer, UART

---

## Scenario Introduction

In modern automotive systems, fault indicators play a critical role in alerting drivers to engine issues. These alerts must be responsive to physical triggers and provide diagnostic feedback through communication interfaces. This task simulates an engine fault alert mechanism using embedded peripherals. A button press triggers a fault condition, indicated by a blinking LED. The fault can be cleared via UART, and the system must report its status when queried.

This exercise reinforces interrupt-driven design, timer-based periodic signaling, and UART-based diagnostics—key concepts in embedded automotive control systems.

---

## Implementation Details

### Peripheral Configuration:

- **GPIO Interrupt:** PC13 configured for falling edge interrupt (Button)

- **Timer:** Configured for 500 ms periodic interrupt (LED blinking)

- **UART:** 9600 baud, TX/RX enabled

### System Behavior:

- On **button press** → Enable fault mode (start blinking LED)

- On UART command **'C'** → Clear fault mode (stop blinking LED)

- On UART command **'S'** → Send fault status (FAULT: ON or FAULT: OFF) via UART

- Fault mode uses timer interrupt to blink LED every 500 ms

- System must remain responsive to both interrupt and UART inputs

- On system restart → Fault mode should be OFF by default

---

# Expected Output and Test Cases

| Test Case No. | Description | Input | Expected Output (UART) | Remarks |
|---------------|-------------|--------|------------------------|---------|
| TC01 | Fault via button | Button Press | LED blinks every 500 ms | Timer active |
| TC02 | Clear fault | 'C' | ACK: FAULT CLEARED | LED stops blinking |
| TC03 | Status request | 'S' | FAULT: ON or FAULT: OFF | Accurate fault reporting |
| TC04 | Rapid fault toggling | Multiple button presses and 'C' | LED responds correctly | Interrupt and UART stable |
| TC05 | Power cycle reset | System Restart | All LEDs OFF | Default state enforced |
