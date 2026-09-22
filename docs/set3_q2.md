# Question 2: Circular Array Reordering

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

A monitoring system stores readings in an array. Because the reporting cycle starts at a different position, the array must be rotated to the right before the summary is generated.

---

## 3. Scenario

A right rotation by one position moves the last element to index `0` and shifts every other element one position to the right. A right rotation by `K` positions repeats this operation `K` times.

After rotation, the program must report the reordered array, its minimum value, and the first index of that minimum value.

---

## 4. Tasks to Implement

The program must:

1. Read `N`, `K`, and the array values.
2. Normalize `K` when it is greater than `N`.
3. Rotate the array to the right by `K` positions.
4. Find the minimum value in the rotated array.
5. Find the first index of that minimum value.
6. Display the rotated array and summary.

---

## 5. Function Details

Students must implement and use the following four functions.

### 5.1 Function 1: Normalize the Rotation

* Function Name: `normalizeRotation`
* Arguments: `rotation, size`
* Return type: `Integer`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `rotation` | Integer | Input | Requested right-rotation count |
| `size` | Integer | Input | Number of array values |

The function returns `rotation % size`. It must not read input or print output.

### 5.2 Function 2: Rotate the Array

* Function Name: `rotateRight`
* Arguments: `values, size, rotation`
* Return type: None or Void

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `values` | Array of integers | Input and Output | Array to rotate in place |
| `size` | Integer | Input | Number of values |
| `rotation` | Integer | Input | Normalized right-rotation count |

The function must update the array by rotating it to the right by `rotation` positions. It must not read input or print output.

### 5.3 Function 3: Find the Minimum

* Function Name: `findMinimum`
* Arguments: `values, size`
* Return type: `Integer`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `values` | Array of integers | Input | Rotated array |
| `size` | Integer | Input | Number of values |

The function returns the smallest value in the array. It must not read input, print output, or modify the array.

### 5.4 Function 4: Find the First Index

* Function Name: `findFirstIndex`
* Arguments: `values, size, requiredValue`
* Return type: `Integer`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `values` | Array of integers | Input | Rotated array |
| `size` | Integer | Input | Number of values |
| `requiredValue` | Integer | Input | Minimum value to locate |

The function returns the first index containing `requiredValue`. It must not read input, print output, or modify the array.

### 5.5 Language-Specific Argument Passing

When an argument is marked **Input and Output**, the function must update the caller's value. In C, pass a pointer and dereference it inside the function. In C++, pass the argument by reference. In Python, update the mutable object or use the language-appropriate mutable container. An output array or output count follows the same rule.

---

## 6. Input Format

```text
N K
v1 v2 ... vN
```

`K` is a non-negative integer.

---

## 7. Output Format

Print exactly:

```text
Rotated: <value1> <value2> ... <valueN>
Minimum: <minimum_value>
Minimum index: <index>
```

---

## 8. Constraints and Assumptions

```text
1 <= N <= 1000
0 <= K <= 100000
-100000 <= value <= 100000
```

- All input values are valid integers.
- The original array must be modified into the rotated order.

---

## 9. Rules and Clarifications

* Rule 1 Rotation Direction: Rotation is to the right.
* Rule 2 Large Rotation: Use `K % N` as the effective rotation.
* Rule 3 Zero Rotation: A rotation of zero leaves the array unchanged.
* Rule 4 First Minimum: If the minimum occurs multiple times, report its first index after rotation.
* Rule 5 Mandatory Function Usage: All four required functions must be implemented and used.

---

## 10. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Normal right rotation | `5 2`<br>`10 20 30 40 50` | `Rotated: 40 50 10 20 30`<br>`Minimum: 10`<br>`Minimum index: 2` |
| 2 | Rotation by one position | `4 1`<br>`8 3 6 2` | `Rotated: 2 8 3 6`<br>`Minimum: 2`<br>`Minimum index: 0` |
| 3 | Repeated minimum values | `6 3`<br>`5 1 4 1 8 2` | `Rotated: 1 8 2 5 1 4`<br>`Minimum: 1`<br>`Minimum index: 0` |
| 4 | Negative and positive values | `5 4`<br>`-3 7 -1 5 2` | `Rotated: 7 -1 5 2 -3`<br>`Minimum: -3`<br>`Minimum index: 4` |
| 5 | Boundary case with rotation greater than array size | `3 8`<br>`4 2 9` | `Rotated: 2 9 4`<br>`Minimum: 2`<br>`Minimum index: 0` |
| 6 | Boundary case with one value and zero rotation | `1 0`<br>`-7` | `Rotated: -7`<br>`Minimum: -7`<br>`Minimum index: 0` |

---

## 11. Notes

- The candidate may solve the problem using C, C++, or Python.
- Sorting the array is not required.
- Output labels, capitalization, spacing, and ordering must match exactly.
