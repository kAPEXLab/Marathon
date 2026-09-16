# Question 2: Longest Stable Operating Period

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

Software systems often record their operational status at regular intervals. These status records can be analysed to determine how long the system remained stable without experiencing a failure or exceeding an acceptable number of warnings.

Write a modular program that analyses a sequence of recorded status values and identifies the longest stable operating period.

---

## 3. Scenario

A software service records one operational status value every minute.

Each recorded status value can have one of the following values:

| Status Value | Meaning |
|---:|---|
| `0` | Normal operation |
| `1` | Warning |
| `2` | Failure |

A **stable operating period** is a continuous sequence of status values that satisfies all the following conditions:

1. It contains only Normal (`0`) and Warning (`1`) status values.
2. It contains at most `K` Warning values.
3. It does not contain any Failure (`2`) status value.

The program must identify the longest stable operating period.

If multiple stable operating periods have the same maximum length, the period having the smallest starting index must be selected.

---

## 4. Tasks to Implement

The program must perform the following tasks:

1. Read the number of recorded status values, `N`.
2. Read the maximum allowed number of warnings, `K`.
3. Read the sequence of `N` status values.
4. Store the status values in an array, vector, or list.
5. Determine whether each status value can be included in a stable operating period.
6. Identify all possible continuous stable operating periods.
7. Ensure that a stable period does not contain a Failure status.
8. Ensure that the number of warnings in a stable period does not exceed `K`.
9. Find the longest stable operating period.
10. Apply the specified tie-breaking rule when multiple periods have the same maximum length.
11. Determine the starting index of the selected period.
12. Determine the ending index of the selected period.
13. Count the number of warnings in the selected period.
14. Display the result in the specified output format.
15. Organize the program using the mandatory functions described below.

---

## 5. Function Details

Students must implement and use the following four functions to create a modular program.

Each function returns only one simple value.

The solution does not require:

- Pointers for returning results
- Reference parameters for returning results
- Arrays or lists as return values
- Structures
- Classes or objects
- Tuples
- Global variables

### 5.1 Function 1: Validate a Status Value

This function determines whether a status value can be considered for inclusion in a stable operating period.

- **Function Name:** `isValidStatus`
- **Arguments:** `statusValue`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `statusValue` | Integer | Input | Status value that must be checked |


- **Return Type:** Boolean

| Return Value | Meaning | Condition |
|---|---|---|
| `true` | The status is not a Failure | `statusValue` is `0` or `1` |
| `false` | The status is a Failure | `statusValue` is `2` |


-- **Function Description**

The function must:

1. Receive one integer status value.
2. Return `true` when the status value is `0` or `1`.
3. Return `false` when the status value is `2`.
4. Not read any input.
5. Not print any output.
6. Not modify the argument.


### 5.2 Function 2: Find the Starting Index

This function finds the starting index of the longest stable operating period.

- **Function Name:** `findLongestStablePeriodStart`
- **Arguments:** `statusValues`, `size`, `maxWarnings`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `statusValues` | Collection of integers | Input | Complete sequence of recorded status values |
| `size` | Integer | Input | Number of status values in the sequence |
| `maxWarnings` | Integer | Input | Maximum number of Warning values permitted in a stable period |

- **Return Type:** Integer

| Return Value | Meaning |
|---:|---|
| `0` to `size - 1` | Starting index of the longest stable operating period |
| `-1` | No stable operating period exists |

- **Function Description**

The function must:

1. Receive the complete status sequence.
2. Receive the number of status values.
3. Receive the maximum permitted warning count.
4. Find the longest stable operating period.
5. Return only the starting index of that period.
6. Return `-1` if no stable operating period exists.
7. Select the smaller starting index when multiple periods have the same maximum length.
8. Call `isValidStatus` whenever a status value is checked for Failure.
9. Not read any input.
10. Not print any output.
11. Not modify the input sequence.


### 5.3 Function 3: Find the Ending Index

This function finds the ending index of the longest stable operating period.

- **Function Name:** `findLongestStablePeriodEnd`
- **Arguments:** `statusValues`, `size`, `maxWarnings`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `statusValues` | Collection of integers | Input | Complete sequence of recorded status values |
| `size` | Integer | Input | Number of status values in the sequence |
| `maxWarnings` | Integer | Input | Maximum number of Warning values permitted in a stable period |

- **Return Type:** Integer

| Return Value | Meaning |
|---:|---|
| `0` to `size - 1` | Ending index of the longest stable operating period |
| `-1` | No stable operating period exists |

- **Function Description**

The function must:

1. Receive the complete status sequence.
2. Receive the number of status values.
3. Receive the maximum permitted warning count.
4. Find the longest stable operating period.
5. Return only the ending index of that period.
6. Return `-1` if no stable operating period exists.
7. Apply the same tie-breaking rule used by `findLongestStablePeriodStart`.
8. Call `isValidStatus` whenever a status value is checked for Failure.
9. Not read any input.
10. Not print any output.
11. Not modify the input sequence.

### 5.4 Function 4: Count Warnings in the Selected Period

This function counts the number of Warning values within a specified period.

- **Function Name:** `countWarnings`
- **Arguments:** `statusValues`, `startIndex`, `endIndex`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `statusValues` | Collection of integers | Input | Complete sequence of recorded status values |
| `startIndex` | Integer | Input | Starting index of the selected period |
| `endIndex` | Integer | Input | Ending index of the selected period |

- **Return Type:** Integer

| Return Value | Meaning |
|---:|---|
| Zero or a positive integer | Number of Warning values from `startIndex` to `endIndex`, including both indices |

- **Function Description**

The function must:

1. Receive the complete status sequence.
2. Receive valid starting and ending indices.
3. Count the Warning values represented by `1`.
4. Include both the starting and ending indices in the count.
5. Return the warning count.
6. Not read any input.
7. Not print any output.
8. Not modify the input sequence.

### 5.5 Responsibilities of the Main Program

The main program must:

1. Read `N` and `K`.
2. Read and store the `N` status values.
3. Call `findLongestStablePeriodStart` to obtain the starting index.
4. Call `findLongestStablePeriodEnd` to obtain the ending index.
5. If either returned index is `-1`, print:

```text
No stable period
```

6. Otherwise, calculate the length as:

```text
length = endIndex - startIndex + 1
```

7. Call `countWarnings` to obtain the warning count.
8. Print the length, starting index, ending index, and warning count.

---

### 5.6 Explicit Return-Value Restrictions

The following return mechanisms are not required and must not be assumed:

- Returning an array
- Returning a list
- Returning a structure
- Returning a class or object
- Returning a tuple
- Returning values through pointer arguments
- Returning values through reference arguments

Each mandatory function returns exactly one simple value:

| Function | Return Type | Returned Information |
|---|---|---|
| `isValidStatus` | Boolean | Whether the status is not a Failure |
| `findLongestStablePeriodStart` | Integer | Starting index or `-1` |
| `findLongestStablePeriodEnd` | Integer | Ending index or `-1` |
| `countWarnings` | Integer | Number of warnings |

## 6. Input Format

The first input line contains two space-separated integers:

```text
N K
```

Where:

- `N` is the number of recorded status values.
- `K` is the maximum number of Warning values allowed in a stable operating period.

The second input line contains `N` space-separated integers:

```text
s1 s2 s3 ... sN
```

Each status value is one of the following:

```text
0 1 2
```

---

## 7. Output Format

### When a Stable Period Exists

The program must print exactly the following four lines:

```text
Length: <length>
Start: <start_index>
End: <end_index>
Warnings: <warning_count>
```

### When No Stable Period Exists

The program must print exactly:

```text
No stable period
```

### Output Requirements

- Zero-based indexing must be used.
- The starting and ending indices are inclusive.
- If multiple stable periods have the same maximum length, the period with the smallest starting index must be selected.

---

## 8. Constraints and Assumptions

```text
1 <= N <= 100000
0 <= K <= N
statusValue belongs to {0, 1, 2}
```

- All input values are valid integers.
- Exactly `N` status values will be provided.
- Every status value will be `0`, `1`, or `2`.
- Handling malformed input is not required.
- The status values are recorded in chronological order.

---

## 9. Rules and Clarifications

- **Rule 1, Normal Status:** A Normal status (`0`) can be included in a stable operating period and does not increase the warning count.
- **Rule 2, Warning Status:** A Warning status (`1`) can be included in a stable operating period, but the total warning count must not exceed `K`.
- **Rule 3, Failure Status:** A Failure status (`2`) cannot be included in a stable operating period. It terminates the current period.
- **Rule 4, Warning Limit:** If the warning count becomes greater than `K`, the starting index of the current period must be moved forward until the warning count becomes valid again.
- **Rule 5, Continuous Period:** All status values between the starting and ending indices belong to the selected period. Values cannot be skipped.
- **Rule 6, Tie-Breaking:** If multiple stable periods have the same maximum length, the period with the smallest starting index must be selected.
- **Rule 7, Zero-Based Indexing:** The first status value is at index `0`.
- **Rule 8, Inclusive Indices:** Both the starting and ending indices are included in the selected period.
- **Rule 9, Final Period:** A stable period may continue until the final status value. Such a period must also be evaluated.
- **Rule 10, No Stable Period:** If all recorded status values are Failure values, or no sequence satisfies the warning limit, the program must print `No stable period`.
- **Rule 11, Mandatory Function Usage:** All four mandatory functions must be implemented and used.

---

## 10. Test Cases

## 10. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Normal case with two equal-length periods | 12 2<br>0 1 0 1 0 2 0 1 1 0 0 2 | Length: 5<br>Start: 0<br>End: 4<br>Warnings: 2 |
| 2 | All status values are Failure values | 5 2<br>2 2 2 2 2 | No stable period |
| 3 | Complete sequence is a stable period | 6 3<br>0 1 0 1 1 0 | Length: 6<br>Start: 0<br>End: 5<br>Warnings: 3 |
| 4 | Tie-breaking based on the smallest starting index | 10 1<br>0 1 0 2 0 1 0 2 0 0 | Length: 3<br>Start: 0<br>End: 2<br>Warnings: 1 |
| 5 | Warning limit is zero | 7 0<br>0 1 0 0 2 0 0 | Length: 2<br>Start: 2<br>End: 3<br>Warnings: 0 |
| 6 | Starting index must move when the warning count exceeds the limit | 7 1<br>0 1 0 1 0 0 2 | Length: 4<br>Start: 2<br>End: 5<br>Warnings: 1 |

---

## 11. Notes

- The candidate may solve the problem using C, C++, or Python.
- The program must follow a modular design.
- All four mandatory functions must be implemented and called from the program.
- Each mandatory function must return exactly one simple value, either an Integer or a Boolean.
- No mandatory function is required to return multiple values.
- Returning an array, list, structure, record, class, object, or tuple is not required.
- Pointers, reference parameters, output parameters, and global variables are not required for returning the results.
- `isValidStatus` must return only a Boolean value.
- `findLongestStablePeriodStart` must return only the starting index of the selected period or `-1` when no stable period exists.
- `findLongestStablePeriodEnd` must return only the ending index of the selected period or `-1` when no stable period exists.
- `countWarnings` must return only the number of Warning values in the selected period.
- The main program must calculate the length of the selected period.

---
