# Question 3: Longest Operating Period Status Summary

## 1. Question Details

| Attribute | Details |
|---|---|
| Difficulty | Medium |
| Supported Languages | C, C++, or Python |
| Internet Access | Not allowed |
| AI Tools | Not allowed |
| Notes or Reference Material | Not allowed |

---

## 2. Introduction

A software service records its operational status at regular intervals. Write a program that identifies the longest continuous operating period that does not contain a failure and summarizes the statuses within that period.

---

## 3. Scenario

The service records one status value every minute.

| Status Value | Meaning |
|---:|---|
| `0` | Normal operation |
| `1` | Warning |
| `2` | Failure |

A stable operating period contains only Normal (`0`) and Warning (`1`) values. A Failure (`2`) ends the current period.

---

## 4. Tasks to Implement

The program must perform the following tasks:

1. Read the number of recorded status values, `N`.
2. Read and store the `N` status values.
3. Determine whether each status value can be included in a stable period.
4. Find the longest continuous period without a Failure.
5. Apply the smallest-starting-index tie-breaking rule.
6. Determine the length, starting index, and ending index.
7. Count the Normal and Warning statuses in the selected period.
8. Display the result in the specified output format.

---

## 5. Function Details

Students must implement and use the following five functions.

### 5.1 Function 1: Validate a Status Value

* Function Name: `isValidStatus`
* Arguments: `statusValue`
* Return type: `Boolean`

The function returns `true` when `statusValue` is `0` or `1`, and `false` when it is `2`. It must not read input, print output, or modify the argument.

### 5.2 Function 2: Find the Starting Index

* Function Name: `findLongestStablePeriodStart`
* Arguments: `statusValues, size`
* Return type: `Integer`

The function must find the longest continuous period without a Failure and return its starting index. It must apply the smallest-starting-index tie-breaker, use `isValidStatus`, and return `-1` when no stable period exists. It must not read input, print output, or modify the input sequence.

### 5.3 Function 3: Find the Ending Index

* Function Name: `findLongestStablePeriodEnd`
* Arguments: `statusValues, size`
* Return type: `Integer`

The function must find the ending index of the same longest continuous period selected by `findLongestStablePeriodStart`. It must apply the same tie-breaking rule, use `isValidStatus`, and return `-1` when no stable period exists. It must not read input, print output, or modify the input sequence.

### 5.4 Function 4: Count Warnings

* Function Name: `countWarnings`
* Arguments: `statusValues, startIndex, endIndex`
* Return type: `Integer`

The function must count the Warning values (`1`) from `startIndex` through `endIndex`, including both indices. It must not read input, print output, or modify the input sequence.

### 5.5 Function 5: Count Normal Statuses

* Function Name: `countNormalStatuses`
* Arguments: `statusValues, startIndex, endIndex`
* Return type: `Integer`

The function must count the Normal values (`0`) from `startIndex` through `endIndex`, including both indices. It must not read input, print output, or modify the input sequence.

### 5.6 Responsibilities of the Main Program

The main program must:

1. Read and store the status values.
2. Call `findLongestStablePeriodStart` and `findLongestStablePeriodEnd` to identify the selected period.
3. Print `No stable period` when no valid period exists.
4. Otherwise determine the selected period's length and ending index.
5. Call `countWarnings` and `countNormalStatuses` for the selected period.
6. Print the length, indices, and status counts.

---

## 6. Input Format

The first input contains one integer:

```text
N
```

The second input contains `N` space-separated integers:

```text
s1 s2 ... sN
```

---

## 7. Output Format

When a stable period exists, print exactly:

```text
Length: <length>
Start: <start_index>
End: <end_index>
Normal: <normal_count>
Warnings: <warning_count>
```

When no stable period exists, print exactly:

```text
No stable period
```

Zero-based indexing must be used. The start and end indices are inclusive.

---

## 8. Constraints and Assumptions

```text
1 <= N <= 100000
statusValue belongs to {0, 1, 2}
```

- All input values are valid integers.
- Exactly `N` status values will be provided.
- The status values are recorded in chronological order.

---

## 9. Rules and Clarifications

* Rule 1 Normal Status: A Normal status (`0`) can be included in a stable period.
* Rule 2 Warning Status: A Warning status (`1`) can be included in a stable period.
* Rule 3 Failure Status: A Failure status (`2`) cannot be included and terminates the current period.
* Rule 4 Continuous Period: All values between the starting and ending indices belong to the selected period.
* Rule 5 Tie-Breaking: Equal-length periods are resolved by selecting the smallest starting index.
* Rule 6 No Stable Period: If all values are Failure values, print `No stable period`.
* Rule 7 Selected Period Summary: The selected period must report its Normal and Warning counts.
* Rule 8 Mandatory Function Usage: All five required functions must be implemented and used.

---

## 10. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Two periods with different lengths | `10`<br>`0 1 0 2 0 1 0 2 0 0` | `Length: 3`<br>`Start: 0`<br>`End: 2`<br>`Normal: 2`<br>`Warnings: 1` |
| 2 | Complete sequence is stable | `6`<br>`0 1 0 1 1 0` | `Length: 6`<br>`Start: 0`<br>`End: 5`<br>`Normal: 3`<br>`Warnings: 3` |
| 3 | Longest period occurs near the beginning | `9`<br>`2 0 0 1 0 2 1 0 0` | `Length: 4`<br>`Start: 1`<br>`End: 4`<br>`Normal: 3`<br>`Warnings: 1` |
| 4 | Several stable periods with different lengths | `11`<br>`0 0 2 1 1 0 2 0 1 0 0` | `Length: 4`<br>`Start: 7`<br>`End: 10`<br>`Normal: 3`<br>`Warnings: 1` |
| 5 | Boundary case with all Failure values | `5`<br>`2 2 2 2 2` | `No stable period` |
| 6 | Boundary case with one Normal status | `1`<br>`0` | `Length: 1`<br>`Start: 0`<br>`End: 0`<br>`Normal: 1`<br>`Warnings: 0` |

---

## 11. Notes

- The candidate may solve the problem using C, C++, or Python.
- The candidate must store the status values.
- The selected period must be summarized using the required counting functions.
- Output labels, capitalization, spacing, and ordering must match the specified output format.
