# ASSESSMENT PROBLEM STATEMENT

| Field | Details |
|---|---|
| **Question Number** | EMBPROG_MARATHON_01 |
| **Scenario** | GPIO toggle for device power indicator |
| **Embedded Systems Concepts** | GPIO Input/Output, Pin Configuration, Button Polling |
| **C Programming Concepts** | Loop, debouncing logic |
| **Difficulty Level** | Beginner |

## Scenario

You're building a small bench power supply with a front-panel **"Power" button** and **five status LEDs**. Students wire the button to a GPIO input and drive the LEDs from GPIO outputs on the Nucleo board. Each button press toggles the device state: when **"on,"** the LEDs run through a sequence of patterns; when **"standby,"** all LEDs are off. This simulates a real control panel interaction without interrupts or debounce.

## Requirements and Specifications

- **Hardware:** Five LEDs connected to GPIO pins (e.g., `PA5`, `PB0`, `PB1`, `PB5`, `PC0`) and a push button (e.g., `PC13`).
- **Behaviour:**
  - Each press toggles the supply state.
  - **On state:** LEDs cycle through explicit patterns using `for` loops.
  - **Standby state:** LEDs remain off.
  - Holding the button does not retrigger.

## Explicit LED Patterns

Students must implement at least these four patterns:

1. **Blink All Together**
   - All LEDs ON -> delay -> all OFF -> delay -> repeat.

2. **Chase/Running Light**
   - Turn LEDs on one by one from LED1 -> LED5, then off in the same order.

3. **Ping-Pong**
   - LEDs light from LED1 -> LED5, then reverse LED5 -> LED1.

4. **Alternate Flash**
   - LEDs 1, 3, 5 ON while LEDs 2, 4 OFF -> delay -> swap states.

## Tasks to Implement in `main`

- **GPIO init:** Configure all five LED pins as outputs; `PC13` as input with pull-up.
- **Loop:** Poll button; detect edge from released -> pressed (no debounce).
- **Action:**
  - If **"on,"** cycle through the LED patterns using nested `for` loops and delays.
  - If **"standby,"** keep all LEDs off.

## Test Cases

| Test Case No. | Input/Condition | Expected Output |
|---|---|---|
| TC001 | First press (short, >1s) | LEDs enter pattern sequence (start with Blink All) |
| TC002 | Second press (short, >1s) | All LEDs off (standby) |
| TC003 | Button held for 2 seconds | LEDs stay in last state (no retrigger) |
| TC004 | No press | LEDs unchanged |
