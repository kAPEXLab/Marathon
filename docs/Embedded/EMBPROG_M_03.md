# ASSESSMENT PROBLEM STATEMENT

| Field | Details |
|---|---|
| **Question Number** | EMBPROG_MARATHON_03 |
| **Scenario** | UART-polled command interface for remote LED control |
| **Embedded Systems Concepts** | UART2 Communication (TX/RX), Timer6, GPIO Output |
| **C Programming Concepts** | string parsing, switch-case, command handling |
| **Difficulty Level** | Intermediate |

## Scenario

You’re building a remotely managed lab indicator light. A PC dashboard sends commands to the Nucleo over virtual COM to control the LED.

Students implement a minimal UART protocol: sending `'1'` turns the LED on, `'0'` turns it off. The system continuously polls the UART receive status to react to commands.

## Requirements and Specifications

- **Hardware:** LED on PA5; USART2
- **Protocol:** ASCII `'1'` → LED ON, `'0'` → LED OFF; ignore other characters.
- **Baud rate:** 9600, 8N1.

## Tasks to Implement in `main`

- **GPIO init:** PA5 as output.
- **UART init:** Configure USART2 at 9600 8N1; enable transmitter/receiver.
- **Loop:** Poll RXNE; on data,

## Test Cases

| Test Case ID | Input/Condition | Expected Output |
|---|---|---|
| TC001 | Receive `'1'` | LED turns on |
| TC002 | Receive `'0'` | LED turns off |
| TC003 | Receive `'x'` or newline | LED unchanged |
| TC004 | Continuous stream `'1010'` | LED toggles accordingly |
| TC005 | No incoming data | LED remains in last state |
