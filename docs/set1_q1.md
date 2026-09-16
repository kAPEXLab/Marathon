# Question 1: Task Execution Performance Analyzer

## 1. Question Details

| Attribute | Details |
|---|---|
| Difficulty | Easy |
| Supported Languages | C, C++, or Python |
| Internet Access | Not allowed |
| AI Tools | Not allowed |
| Notes or Reference Material | Not allowed |

---

## 2. Introduction

A software system executes multiple tasks and records the time required to complete each task. The execution time can be used to classify tasks into different performance categories.

Write a program that analyses the recorded execution times and generates a performance summary.

---

## 3. Scenario

The execution time of each task is recorded in milliseconds.

Two execution-time limits are provided:

- `L`: Lower execution-time limit
- `H`: Upper execution-time limit

Each task must be classified into exactly one of the following categories:

| Category | Classification Rule |
|---|---|
| Fast | Execution time is strictly less than `L` |
| Acceptable | Execution time is greater than or equal to `L` and less than or equal to `H` |
| Slow | Execution time is strictly greater than `H` |

The program must process all task execution times and generate a summary.

---

## 4. Tasks to Implement

The program must perform the following tasks:

1. Read the number of tasks, `N`.
2. Read the lower execution-time limit, `L`.
3. Read the upper execution-time limit, `H`.
4. Read the execution times of all `N` tasks.
5. Store the execution times in an array, vector, or list.
6. Classify each task as Fast, Acceptable, or Slow.
7. Count the number of tasks in each category.
8. Calculate the average execution time.
9. Find the maximum execution time.
10. Find the index of the first occurrence of the maximum execution time.
11. Display the results in the specified output format.

---

## 5. Function Details

Students must implement and use a function that classifies one execution-time value.

* Function Name: `classifyTime`
* Arguments: `executionTime, lowerLimit, upperLimit`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `executionTime` | Integer | Input | Execution time of the current task in milliseconds |
| `lowerLimit` | Integer | Input | Lower classification limit, represented by `L` |
| `upperLimit` | Integer | Input | Upper classification limit, represented by `H` |

The function does not modify any of its arguments.

* return type: `integer`
* Return Values

| Return Value | Category | Condition |
|---:|---|---|
| `0` | Fast | `executionTime < lowerLimit` |
| `1` | Acceptable | `lowerLimit <= executionTime <= upperLimit` |
| `2` | Slow | `executionTime > upperLimit` |

* Function Description

The function must:

1. Receive one execution-time value and the two classification limits.
2. Compare the execution time with the limits.
3. Return the integer code representing the appropriate category.
4. Not read any input.
5. Not print any output.
6. Not calculate category counts.
7. Not modify the supplied values.

---

## 6. Input Format

The first input contains three space-separated integers:

```text
N L H
```

Where:

- `N` is the number of tasks.
- `L` is the lower execution-time limit.
- `H` is the upper execution-time limit.

The second input contains `N` space-separated integers:

```text
t1 t2 t3 ... tN
```

Each value represents the execution time of one task in milliseconds.

---

## 7. Output Format

The program must print exactly the following six lines:

```text
Fast: <fast_count>
Acceptable: <acceptable_count>
Slow: <slow_count>
Average: <average_value>
Maximum: <maximum_value>
Maximum index: <index>
```

### Output Requirements

- The average must be displayed with exactly two digits after the decimal point.
- Zero-based indexing must be used.
- If the maximum execution time occurs more than once, the index of its first occurrence must be reported.
- No additional input prompts or explanatory messages must be printed.

For example, the program must not print messages such as:

```text
Enter the number of tasks:
Enter the execution times:
```
---

## 8. Constraints and Assumptions

```text
1 <= N <= 1000
0 <= L <= H <= 100000
0 <= executionTime <= 100000
```

- All input values are valid integers.
- Exactly `N` execution-time values will be provided.
- The lower limit `L` will never be greater than the upper limit `H`.
- Handling malformed input is not required.

---

## 9. Rules and Clarifications

* Rule 1 Lower Boundary: An execution time equal to `L` must be classified as Acceptable.
* Rule 2 Upper Boundary: An execution time equal to `H` must be classified as Acceptable.
* Rule 3 Average Calculation: The average execution time must be calculated as for `N` tasks. The calculation must produce a floating-point result.
* Rule 4 First Maximum Occurrence: If the maximum execution time occurs multiple times, the index of its first occurrence must be reported.
* Rule 5: Mandatory Function Usage: The mandatory classification function must be called for every execution-time value.

---

## 10. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Normal case containing all three categories | `8 50 100`<br>`45 60 120 75 40 100 140 55` | `Fast: 2`<br>`Acceptable: 4`<br>`Slow: 2`<br>`Average: 79.38`<br>`Maximum: 140`<br>`Maximum index: 6` |
| 2 | Execution times equal to both classification limits | `5 50 100`<br>`50 100 49 101 75` | `Fast: 1`<br>`Acceptable: 3`<br>`Slow: 1`<br>`Average: 75.00`<br>`Maximum: 101`<br>`Maximum index: 3` |
| 3 | Only one task | `1 20 40`<br>`35` | `Fast: 0`<br>`Acceptable: 1`<br>`Slow: 0`<br>`Average: 35.00`<br>`Maximum: 35`<br>`Maximum index: 0` |
| 4 | All execution times are equal | `4 10 20`<br>`15 15 15 15` | `Fast: 0`<br>`Acceptable: 4`<br>`Slow: 0`<br>`Average: 15.00`<br>`Maximum: 15`<br>`Maximum index: 0` |
| 5 | Maximum execution time occurs multiple times | `6 30 60`<br>`20 80 45 80 30 25` | `Fast: 2`<br>`Acceptable: 2`<br>`Slow: 2`<br>`Average: 46.67`<br>`Maximum: 80`<br>`Maximum index: 1` |
| 6 | All tasks are Fast | `5 50 100`<br>`10 20 30 40 0` | `Fast: 5`<br>`Acceptable: 0`<br>`Slow: 0`<br>`Average: 20.00`<br>`Maximum: 40`<br>`Maximum index: 3` |
| 7 | All tasks are Slow | `4 10 20`<br>`25 30 35 40` | `Fast: 0`<br>`Acceptable: 0`<br>`Slow: 4`<br>`Average: 32.50`<br>`Maximum: 40`<br>`Maximum index: 3` |
| 8 | Limits and execution times contain zero | `5 0 0`<br>`0 1 0 2 0` | `Fast: 0`<br>`Acceptable: 3`<br>`Slow: 2`<br>`Average: 0.60`<br>`Maximum: 2`<br>`Maximum index: 3` |

---

## 11. Notes

- The candidate may solve the problem using C, C++, or Python.
- Language-specific shortcuts are not compulsory.
- Manually implemented minimum, maximum, and traversal logic is acceptable.
- The candidate must use the mandatory classification function.
- The candidate must store the task execution times.
- Output labels, capitalization, spacing, and ordering must match the specified output format.
