# Question 1: Task Performance Classification

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

A system records the execution time of several tasks in milliseconds. Each task must be classified using a lower limit and an upper limit.

Write a program that classifies the tasks and counts how many belong to each category.

---

## 3. Scenario

Two execution-time limits are provided:

- `L`: Lower execution-time limit
- `H`: Upper execution-time limit

| Category | Classification Rule |
|---|---|
| Fast | Execution time is strictly less than `L` |
| Acceptable | Execution time is greater than or equal to `L` and less than or equal to `H` |
| Slow | Execution time is strictly greater than `H` |

---

## 4. Tasks to Implement

The program must perform the following tasks:

1. Read the number of tasks, `N`.
2. Read the lower execution-time limit, `L`.
3. Read the upper execution-time limit, `H`.
4. Read and store the execution times of all `N` tasks.
5. Classify every execution time.
6. Count the Fast, Acceptable, and Slow tasks.
7. Display the category counts in the specified output format.

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

* Return type: `integer`
* Return Values

| Return Value | Category | Condition |
|---:|---|---|
| `0` | Fast | `executionTime < lowerLimit` |
| `1` | Acceptable | `lowerLimit <= executionTime <= upperLimit` |
| `2` | Slow | `executionTime > upperLimit` |

The function must not read input, print output, calculate counts, or modify its arguments.

---

## 6. Input Format

The first input contains three space-separated integers:

```text
N L H
```

The second input contains `N` space-separated integers:

```text
t1 t2 ... tN
```

---

## 7. Output Format

The program must print exactly:

```text
Fast: <fast_count>
Acceptable: <acceptable_count>
Slow: <slow_count>
```

No additional prompts or explanatory messages may be printed.

---

## 8. Constraints and Assumptions

```text
1 <= N <= 1000
0 <= L <= H <= 100000
0 <= executionTime <= 100000
```

- All input values are valid integers.
- Exactly `N` execution-time values will be provided.
- Values equal to `L` or `H` are Acceptable.

---

## 9. Rules and Clarifications

* Rule 1 Lower Boundary: An execution time equal to `L` must be classified as Acceptable.
* Rule 2 Upper Boundary: An execution time equal to `H` must be classified as Acceptable.
* Rule 3 Mandatory Function Usage: `classifyTime` must be called for every execution-time value.

---

## 10. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Normal case containing all three categories | `8 50 100`<br>`45 60 120 75 40 100 140 55` | `Fast: 2`<br>`Acceptable: 4`<br>`Slow: 2` |
| 2 | Execution times equal to both limits | `5 50 100`<br>`50 100 49 101 75` | `Fast: 1`<br>`Acceptable: 3`<br>`Slow: 1` |
| 3 | All tasks are Fast | `5 50 100`<br>`10 20 30 40 0` | `Fast: 5`<br>`Acceptable: 0`<br>`Slow: 0` |
| 4 | All tasks are Slow | `4 10 20`<br>`25 30 35 40` | `Fast: 0`<br>`Acceptable: 0`<br>`Slow: 4` |
| 5 | Boundary case with zero limits | `5 0 0`<br>`0 1 0 2 0` | `Fast: 0`<br>`Acceptable: 3`<br>`Slow: 2` |
| 6 | Boundary case with one task | `1 20 40`<br>`35` | `Fast: 0`<br>`Acceptable: 1`<br>`Slow: 0` |

---

## 11. Notes

- The candidate may solve the problem using C, C++, or Python.
- The candidate must use the mandatory classification function.
- Output labels, capitalization, spacing, and ordering must match the specified output format.
