# ASSESSMENT PROBLEM STATEMENT

| Field | Details |
|---|---|
| **Question Number** | EMBPROG_MARATHON_02 |
| **Scenario** | Timer-polled heartbeat LED for IoT gateway |
| **Embedded Systems Concepts** | GPIO Input, Timer |
| **C Programming Concepts** | Loops, conditional checks |
| **Difficulty Level** | Beginner-Intermediate |

## Scenario

You're prototyping an IoT gateway status panel. A heartbeat LED should blink at 1 Hz (500 ms on/off) to show the system is alive, even if no network is connected. Students use a hardware timer and poll its update flag to schedule the blink without blocking other tasks.

## Requirements and Specifications

- **Hardware:** On-board LED on `PA5`; `TIM6` for timing.
- **Blink cadence:** Toggle every 500 ms (1 Hz).
- **Constraints:** Poll `TIM6` update flag; no interrupts.
- **Timer setup:** Clock: `TIM6` (assume 84 MHz timer clock).

## Tasks to Implement in `main`

- **GPIO init:** `PA5` as output.
- **Timer init:** Configure `TIM6` PSC/ARR for 500 ms; enable counter.

## Test Cases

| Test Case ID | Input/Condition | Expected Output |
|---|---|---|
| TC001 | System running with TIM2 started | LED toggles every 500 ms |
| TC002 | PSC/ARR misconfigured (short period) | LED blinks faster than 500 ms |
| TC003 | Timer stopped mid-run | LED remains in last state |
| TC004 | UIF not cleared in loop | LED toggles once, then stops (flag stays set) |
