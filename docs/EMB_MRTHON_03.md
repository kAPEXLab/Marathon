# Task 3: Diagnostic Mode (Timer Interrupt + UART)

**Problem Statement Title:** Diagnostic Mode Control via UART and Timer  
**Problem Statement ID:** EMB_MRTHON_03  
**Peripherals Used:** Timer (TIM3), UART (UART2)

---

## Scenario Introduction

During vehicle servicing, technicians often activate diagnostic modes to monitor system behavior, run tests, or verify sensor activity. These modes are typically controlled via service tools that communicate over UART and provide visual feedback through dashboard indicators.

In this task, you will simulate a diagnostic mode controller using embedded peripherals. When diagnostic mode is enabled via UART, an LED blinks once per second to indicate active status. The mode can be disabled via UART, and the system must respond to status queries and handle invalid commands gracefully.

This exercise reinforces timer-based periodic signaling, UART command parsing via interrupt, and robust state management—key skills in embedded diagnostics and service interface design.

---

## Implementation Details

**Peripheral Configuration:**

- **Timer (TIM6):** Configured for 1-second periodic interrupt
- **UART (UART2):** RX interrupt enabled for command parsing

**System Behavior:**

- On UART command 'D' → Enable diagnostic mode
  - Start timer
  - LED blinks every 1 second
  - Send ACK: DIAG ENABLED via UART

- On UART command 'X' → Disable diagnostic mode
  - Stop timer
  - LED turns OFF
  - Send ACK: DIAG DISABLED via UART

- On UART command 'S' → Send current diagnostic status
  - Respond with DIAG: ON or DIAG: OFF

- On invalid UART command → Respond with ERR: UNKNOWN CMD

- On system restart → Diagnostic mode should be OFF by default

---

## Expected Output and Test Cases

| Test Case No. | Description | Input | Expected Output (UART) | Remarks |
|---|---|---|---|---|
| TC01 | Enable diagnostic mode | 'D' | ACK: DIAG ENABLED, LED blinks | Timer active |
| TC02 | Disable diagnostic mode | 'X' | ACK: DIAG DISABLED, LED OFF | Timer stopped |
| TC03 | Status request | 'S' | DIAG: ON or DIAG: OFF | Accurate state reporting |
| TC04 | Invalid command | 'Z' | ERR: UNKNOWN CMD | Robust error handling |
| TC05 | Rapid enable/disable | Multiple 'D'/'X' | LED toggles correctly | Timer and state transitions stable |
