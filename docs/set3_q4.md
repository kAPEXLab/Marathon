# Question 4: Voltage Waveform Analyzer

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

A data acquisition system records voltage samples from an electrical waveform at equal time intervals. Write a program that calculates basic waveform measurements.

---

## 3. Scenario

The input contains signed real-number voltage samples in chronological order. The program must calculate:

- Root mean square voltage
- Maximum sample
- Minimum sample
- Peak-to-peak voltage
- Number of zero crossings

The root mean square value is calculated as:

```text
RMS = square root of ((v1 * v1 + v2 * v2 + ... + vN * vN) / N)
```

A zero crossing is counted when two consecutive samples change sign, including a transition from a negative value to zero or from a positive value to zero. A pair containing zero and a value with the same non-negative or non-positive side is not counted twice.

---

## 4. Tasks to Implement

The program must:

1. Read and store `N` voltage samples.
2. Calculate the RMS voltage.
3. Find the maximum sample.
4. Find the minimum sample.
5. Calculate peak-to-peak voltage as maximum minus minimum.
6. Count zero crossings using consecutive samples.
7. Display the waveform summary.

---

## 5. Function Details

Students must implement and use:

### 5.1 Function 1: Calculate RMS

* Function Name: `calculateRms`
* Arguments: `samples, size`
* Return type: `Real Number`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `samples` | Array of real numbers | Input | Voltage samples |
| `size` | Integer | Input | Number of samples |

The function returns the square root of the mean of the squared samples. It must not read input, print output, or modify the samples.

### 5.2 Function 2: Find Maximum Sample

* Function Name: `findMaximumSample`
* Arguments: `samples, size`
* Return type: `Real Number`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `samples` | Array of real numbers | Input | Voltage samples |
| `size` | Integer | Input | Number of samples |

The function returns the largest sample value.

### 5.3 Function 3: Find Minimum Sample

* Function Name: `findMinimumSample`
* Arguments: `samples, size`
* Return type: `Real Number`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `samples` | Array of real numbers | Input | Voltage samples |
| `size` | Integer | Input | Number of samples |

The function returns the smallest sample value.

### 5.4 Function 4: Count Zero Crossings

* Function Name: `countZeroCrossings`
* Arguments: `samples, size`
* Return type: `Integer`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `samples` | Array of real numbers | Input | Voltage samples in chronological order |
| `size` | Integer | Input | Number of samples |

For each adjacent pair `(previous, current)`, count one crossing when:

```text
previous < 0 and current >= 0
```

or:

```text
previous > 0 and current <= 0
```

The function must not read input, print output, or modify the samples.

### 5.5 Language-Specific Argument Passing

When an argument is marked **Input and Output**, the function must update the caller's value. In C, pass a pointer and dereference it inside the function. In C++, pass the argument by reference. In Python, update the mutable object or use the language-appropriate mutable container. An output array or output count follows the same rule.

All four functions must be implemented and used.

---

## 6. Input Format

The first input contains one integer:

```text
N
```

The second input contains `N` space-separated real numbers:

```text
v1 v2 ... vN
```

---

## 7. Output Format

Print exactly:

```text
RMS: <rms_value>
Maximum: <maximum_value>
Minimum: <minimum_value>
Peak-to-peak: <peak_to_peak_value>
Zero crossings: <crossing_count>
```

All real-number results must be displayed with exactly two digits after the decimal point.

---

## 8. Constraints and Assumptions

```text
1 <= N <= 10000
-100000.0 <= voltageSample <= 100000.0
```

- Samples are recorded at equal time intervals.
- All input values are valid real numbers.
- At least one sample is provided.

---

## 9. Rules and Clarifications

* Rule 1 RMS: Square every sample before calculating the mean.
* Rule 2 Peak-to-Peak: Calculate `maximum - minimum`.
* Rule 3 Negative Values: Negative voltage samples are valid and must not be discarded.
* Rule 4 Zero Crossing: Use only adjacent samples.
* Rule 5 Zero Sample: A transition from negative to zero counts; a transition from positive to zero counts.
* Rule 6 No Duplicate Count: A single adjacent pair contributes at most one crossing.
* Rule 7 Mandatory Function Usage: All four required functions must be implemented and used.

---

## 10. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Mixed positive and negative samples | `5`<br>`0 1 -1 2 -2` | `RMS: 1.41`<br>`Maximum: 2.00`<br>`Minimum: -2.00`<br>`Peak-to-peak: 4.00`<br>`Zero crossings: 3` |
| 2 | All samples are positive | `4`<br>`1 2 3 4` | `RMS: 2.74`<br>`Maximum: 4.00`<br>`Minimum: 1.00`<br>`Peak-to-peak: 3.00`<br>`Zero crossings: 0` |
| 3 | Samples pass through zero | `5`<br>`-2 -1 0 1 2` | `RMS: 1.41`<br>`Maximum: 2.00`<br>`Minimum: -2.00`<br>`Peak-to-peak: 4.00`<br>`Zero crossings: 1` |
| 4 | Alternating polarity | `4`<br>`-3 3 -3 3` | `RMS: 3.00`<br>`Maximum: 3.00`<br>`Minimum: -3.00`<br>`Peak-to-peak: 6.00`<br>`Zero crossings: 3` |
| 5 | Boundary case with one zero sample | `1`<br>`0` | `RMS: 0.00`<br>`Maximum: 0.00`<br>`Minimum: 0.00`<br>`Peak-to-peak: 0.00`<br>`Zero crossings: 0` |
| 6 | Boundary case with fractional samples | `3`<br>`0.5 -0.5 0.5` | `RMS: 0.50`<br>`Maximum: 0.50`<br>`Minimum: -0.50`<br>`Peak-to-peak: 1.00`<br>`Zero crossings: 2` |

---

## 11. Notes

- The candidate may solve the problem using C, C++, or Python.
- The mathematical calculations must use floating-point arithmetic.
- Output labels, capitalization, spacing, and ordering must match exactly.
