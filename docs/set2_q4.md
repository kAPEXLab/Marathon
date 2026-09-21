# Question 4: Longest Stable Operating Period With Warning Limit

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

A software service records its operational status at regular intervals. Write a program that identifies the longest stable operating period while allowing a limited number of warnings.

---

## 3. Scenario

The service records one status value every minute.

| Status Value | Meaning |
|---:|---|
| `0` | Normal operation |
| `1` | Warning |
| `2` | Failure |

A stable operating period:

1. Contains only Normal (`0`) and Warning (`1`) values.
2. Contains at most `K` Warning values.
3. Does not contain a Failure (`2`) value.

The values must form one continuous sequence; values cannot be skipped.

---

## 4. Tasks to Implement

The program must perform the following tasks:

1. Read the number of recorded status values, `N`.
2. Read the maximum allowed number of warnings, `K`.
3. Read and store the `N` status values.
4. Determine whether each status value can be included in a stable period.
5. Find the longest stable operating period.
6. Ensure that the warning count does not exceed `K`.
7. Apply the specified tie-breaking rules.
8. Determine the length, starting index, ending index, and warning count.
9. Display the result in the specified output format.

---

## 5. Function Details

Students must implement and use the following four functions.

### 5.1 Function 1: Validate a Status Value

* Function Name: `isValidStatus`
* Arguments: `statusValue`
* Return type: `Boolean`

The function returns `true` for status `0` or `1`, and `false` for status `2`. It must not read input, print output, or modify the argument.

### 5.2 Function 2: Find the Starting Index

* Function Name: `findLongestStablePeriodStart`
* Arguments: `statusValues, size, maxWarnings`
* Return type: `Integer`

The function returns the starting index of the selected stable period, or `-1` when no stable period exists. It must select the longest period first, then apply the fewer-warnings tie-breaker, and finally apply the smallest-starting-index tie-breaker. It must call `isValidStatus` when checking status values and must not read input, print output, or modify the input sequence.

### 5.3 Function 3: Find the Ending Index

* Function Name: `findLongestStablePeriodEnd`
* Arguments: `statusValues, size, maxWarnings`
* Return type: `Integer`

The function returns the ending index of the same selected period, or `-1` when no stable period exists. It must apply exactly the same length, warning-count, and starting-index tie-breaking rules and must not read input, print output, or modify the input sequence.

### 5.4 Function 4: Count Warnings in the Selected Period

* Function Name: `countWarnings`
* Arguments: `statusValues, startIndex, endIndex`
* Return type: `Integer`

The function counts the Warning values (`1`) between the inclusive start and end indices. It must not read input, print output, or modify the input sequence.

### 5.5 Responsibilities of the Main Program

The main program must:

1. Read and store the input values.
2. Call the two search functions.
3. Print `No stable period` if either search function returns `-1`.
4. Otherwise calculate `length = endIndex - startIndex + 1`.
5. Call `countWarnings`.
6. Print the selected period details.

---

## 6. Input Format

The first input contains two space-separated integers:

```text
N K
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
0 <= K <= N
statusValue belongs to {0, 1, 2}
```

- All input values are valid integers.
- Exactly `N` status values will be provided.
- The status values are recorded in chronological order.

---

## 9. Rules and Clarifications

* Rule 1 Normal Status: A Normal status (`0`) can be included and does not increase the warning count.
* Rule 2 Warning Status: A Warning status (`1`) can be included, but the total must not exceed `K`.
* Rule 3 Failure Status: A Failure status (`2`) cannot be included and terminates the current period.
* Rule 4 Continuous Period: All values between the starting and ending indices belong to the selected period.
* Rule 5 Tie-Breaking: Among equal-length periods, select the period with fewer warnings.
* Rule 6 Secondary Tie-Breaking: If equal-length periods also have equal warning counts, select the smallest starting index.
* Rule 7 Inclusive Indices: Both the starting and ending indices are included.
* Rule 8 Final Period: A stable period may continue through the final status value and must be evaluated.
* Rule 9 No Stable Period: If all values are Failure values, or every possible non-Failure period exceeds the warning limit, print `No stable period`.
* Rule 10 Mandatory Function Usage: All four required functions must be implemented and used.

---

## 10. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Normal case with two equal-length periods | `12 2`<br>`0 1 0 1 0 2 0 1 1 0 0 2` | `Length: 5`<br>`Start: 0`<br>`End: 4`<br>`Warnings: 2` |
| 2 | Starting index moves when warning count exceeds limit | `7 1`<br>`0 1 0 1 0 0 2` | `Length: 4`<br>`Start: 2`<br>`End: 5`<br>`Warnings: 1` |
| 3 | All statuses are Normal | `5 2`<br>`0 0 0 0 0` | `Length: 5`<br>`Start: 0`<br>`End: 4`<br>`Warnings: 0` |
| 4 | Warnings remain within the allowed limit | `6 3`<br>`0 1 1 0 1 0` | `Length: 6`<br>`Start: 0`<br>`End: 5`<br>`Warnings: 3` |
| 5 | Boundary case with warning limit zero | `7 0`<br>`0 1 0 0 2 0 0` | `Length: 2`<br>`Start: 2`<br>`End: 3`<br>`Warnings: 0` |
| 6 | Edge case: equal lengths resolved using fewer warnings | `10 2`<br>`0 1 0 0 2 0 0 0 0 2` | `Length: 4`<br>`Start: 5`<br>`End: 8`<br>`Warnings: 0` |

---

## 11. Notes

- The candidate may solve the problem using C, C++, or Python.
- A sliding-window approach is recommended but not required.
- The candidate must store the status values.
- Output labels, capitalization, spacing, and ordering must match the specified output format.
