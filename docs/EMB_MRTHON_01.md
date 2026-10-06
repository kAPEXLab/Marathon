# Problem Statement Title: Bidirectional LED Pattern

## Problem Statement ID: EMB_MRTHON_01

## Peripheral Used: GPIO

---

## Scenario

In embedded automotive dashboards, visual sequences often indicate system status or transitions. This task simulates a bidirectional LED pattern using a single push-button and five GPIO-controlled LEDs. The system should alternate between two distinct patterns based on successive button presses, mimicking a startup and shutdown animation.

---

## Implementation Details

### Peripheral Configuration:

- **GPIO Input:** PC13 configured as input with pull-down resistor (Button)

- **GPIO Outputs:** PA0 to PA4 configured as push-pull outputs (LEDs 1 to 5, left to right)

### System Behavior:

- On **first button press** → Turn ON LEDs one by one from left to right (PA0 → PA4) with 200ms delay between each

- On **second button press** → Turn OFF LEDs one by one from right to left (PA4 → PA0) with 200ms delay between each

- Alternate behavior on every subsequent press (toggle between ON-left-to-right and OFF-right-to-left)

- Apply software debounce to ensure reliable button detection

- On system restart → All LEDs should remain OFF until button is pressed

---

# Expected Output and Test Cases

| Test Case No. | Description | Input Sequence | Expected LED Behavior | Remarks |
|--------------|-------------|----------------|----------------------|---------|
| TC01 | First button press | Single press | LEDs turn ON one by one from PA0 → PA4 | Debounce applied |
| TC02 | Second button press | Single press | LEDs turn OFF one by one from PA4 → PA0 | Pattern alternates correctly |
| TC03 | Multiple alternating presses | Press → wait → press → repeat | LEDs toggle ON/OFF in correct sequence each time | No overlap or glitches |
| TC04 | Rapid button presses | Pressed rapidly 5 times | Only 2 valid toggles executed (ON then OFF) | Debounce 
