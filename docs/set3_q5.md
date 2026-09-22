# Question 5: Industrial Motor Inspection Audit

## 1. Question Details

| Attribute | Details |
|---|---|
| Difficulty | Difficult |
| Supported Languages | C, C++, or Python |
| Internet Access | Not allowed |
| AI Tools | Not allowed |
| Notes or Reference Material | Not allowed |

---

## 2. Introduction

An industrial facility performs periodic inspections of electric motors. Each inspection records operating conditions that can be used to estimate motor health and identify motors requiring attention.

Write a modular program that processes all motor inspection records and produces an audit summary.

---

## 3. Scenario

Each inspection record contains:

| Field | Description |
|---|---|
| Inspection ID | Unique inspection number |
| Motor ID | Identification number of the motor |
| Operating Hours | Total operating hours recorded for the motor |
| Vibration | Measured vibration in millimetres per second |
| Temperature | Motor temperature in degrees Celsius |
| Oil Pressure | Measured oil pressure in PSI |

A record is valid when all the following conditions are satisfied:

```text
inspectionId > 0
motorId > 0
operatingHours >= 0
vibration >= 0
temperature >= -40
oilPressure > 0
```

Invalid records receive category `I` and a health score of `0`.

### Motor Health Score

For every valid record, calculate:

```text
vibrationPenalty = vibration * 10

temperaturePenalty = 0, when temperature <= 70
                     (temperature - 70) * 0.5, when temperature > 70

pressurePenalty = 0, when oilPressure >= 30
                 (30 - oilPressure) * 2, when oilPressure < 30

healthScore = 100 - vibrationPenalty - temperaturePenalty - pressurePenalty
```

The health score must be limited to the range `0` to `100`.

### Health Categories

| Health Score | Category Code | Category |
|---:|:---:|---|
| `85` to `100` | `G` | Good |
| `60` to less than `85` | `M` | Monitor |
| Less than `60` | `S` | Service Required |
| Invalid record | `I` | Invalid |

---

## 4. Tasks to Implement

The program must:

1. Read and store all motor inspection records.
2. Validate every inspection record.
3. Calculate and store the health score and category.
4. Count valid and invalid inspections.
5. Count inspections in each health category.
6. Calculate the average health score of valid inspections.
7. Find the valid inspection with the lowest health score.
8. Resolve equal lowest scores using the smaller Inspection ID.
9. Display the complete audit summary.

---

## 5. Function Details

### 5.1 Data Model

Each inspection must be represented using one structure, class, or object.

| Field | Expected Type | Input or Calculated |
|---|---|---|
| `inspectionId` | Integer | Input |
| `motorId` | Integer | Input |
| `operatingHours` | Real Number | Input |
| `vibration` | Real Number | Input |
| `temperature` | Real Number | Input |
| `oilPressure` | Real Number | Input |
| `healthScore` | Real Number | Calculated |
| `category` | Character | Calculated |
| `isValid` | Boolean | Calculated |

### 5.2 Mandatory Functions

Students must implement and use the following six functions.

### 5.3 Function 1: Validate an Inspection

* Function Name: `isValidInspection`
* Arguments: `record`
* Return type: `Boolean`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `record` | Inspection structure or object | Input | Record whose input fields are validated |

The function returns whether every validity condition is satisfied.

### 5.4 Function 2: Calculate Health Score

* Function Name: `calculateHealthScore`
* Arguments: `record`
* Return type: `Real Number`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `record` | Valid inspection structure or object | Input | Record used for score calculation |

The function returns the calculated score limited to `0..100`.

### 5.5 Function 3: Process All Inspections

* Function Name: `processAllInspections`
* Arguments: `records, size`
* Return type: None or Void

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `records` | Collection of inspection records | Input and Output | Records to process |
| `size` | Integer | Input | Number of records |

The function must process every record by calling `isValidInspection` and, for valid records, `calculateHealthScore`. It must store the validity, score, and category in every record. Category assignment may be implemented directly inside this function using the documented score boundaries.

### 5.6 Function 4: Count by Category

* Function Name: `countByCategory`
* Arguments: `records, size, requiredCategory`
* Return type: `Integer`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `records` | Collection of processed records | Input | Records to inspect |
| `size` | Integer | Input | Number of records |
| `requiredCategory` | Character | Input | Category to count |

The function returns the number of records with the requested category.

### 5.7 Function 5: Find the Worst Inspection

* Function Name: `findWorstInspection`
* Arguments: `records, size`
* Return type: `Integer`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `records` | Collection of processed records | Input | Records to inspect |
| `size` | Integer | Input | Number of records |

The function returns the selected record index, or `-1` when no valid record exists.

### 5.8 Function 6: Calculate Average Health

* Function Name: `calculateAverageHealth`
* Arguments: `records, size`
* Return type: `Real Number`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `records` | Collection of processed records | Input | Records whose valid scores are averaged |
| `size` | Integer | Input | Number of records |

The function returns the average health score of valid records only.

### 5.9 Language-Specific Argument Passing

When an argument is marked **Input and Output**, the function must update the caller's value. In C, pass a pointer and dereference it inside the function. In C++, pass the argument by reference. In Python, update the mutable object or use the language-appropriate mutable container. An output array or output count follows the same rule.

The functions must not read input or print output. The collection order must be preserved.

---

## 6. Input Format

The first input contains one integer:

```text
N
```

The next `N` lines contain:

```text
inspectionId motorId operatingHours vibration temperature oilPressure
```

All input values are numeric. Real-number fields may contain decimal values.

---

## 7. Output Format

When at least one valid inspection exists, print exactly:

```text
Valid inspections: <valid_count>
Invalid inspections: <invalid_count>
Good: <good_count>
Monitor: <monitor_count>
Service Required: <service_count>
Average health: <average_health>
Worst inspection ID: <inspection_id>
Worst health score: <health_score>
```

When no valid inspection exists, print exactly:

```text
Valid inspections: 0
Invalid inspections: <invalid_count>
Good: 0
Monitor: 0
Service Required: 0
Average health: 0.00
No valid inspection
```

All real-number results must be displayed with exactly two digits after the decimal point.

---

## 8. Constraints and Assumptions

```text
1 <= N <= 1000
-100000 <= inspectionId <= 100000
-100000 <= motorId <= 100000
-100000 <= operatingHours <= 100000
-1000.0 <= vibration <= 1000.0
-100.0 <= temperature <= 300.0
-1000.0 <= oilPressure <= 1000.0
```

- Inspection IDs are not necessarily consecutive.
- Inspection IDs may be unique in valid input, but duplicate detection is not required.
- All records must remain in their original order.

---

## 9. Rules and Clarifications

* Rule 1 Validation: A record is valid only when every listed validation condition is satisfied.
* Rule 2 Invalid Record: An invalid record has category `I` and health score `0.00`.
* Rule 3 Score Limit: A health score greater than `100` becomes `100`; a score below `0` becomes `0`.
* Rule 4 Temperature Penalty: Temperature equal to `70` has no temperature penalty.
* Rule 5 Pressure Penalty: Oil pressure equal to `30` has no pressure penalty.
* Rule 6 Category Boundaries: Scores equal to `85` belong to `G`; scores equal to `60` belong to `M`.
* Rule 7 Worst Inspection: Consider valid inspections only.
* Rule 8 Tie-Breaking: Equal lowest health scores are resolved using the smaller Inspection ID.
* Rule 9 Average Health: Invalid inspections must not be included in the average.
* Rule 10 Mandatory Function Usage: All six required functions must be implemented and used.

---

## 10. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Normal mix of health categories and an invalid record | 4<br>101 1001 1000 1.0 60 40<br>102 1002 2000 2.0 80 25<br>103 1003 500 4.0 90 20<br>104 1004 -1 1.0 60 40 | Valid inspections: 3<br>Invalid inspections: 1<br>Good: 1<br>Monitor: 1<br>Service Required: 1<br>Average health: 61.67<br>Worst inspection ID: 103<br>Worst health score: 30.00 |
| 2 | Equal worst scores resolved by smaller Inspection ID | 3<br>201 2001 100 3.0 70 40<br>199 2002 100 3.0 70 40<br>205 2003 100 1.0 70 40 | Valid inspections: 3<br>Invalid inspections: 0<br>Good: 1<br>Monitor: 2<br>Service Required: 0<br>Average health: 76.67<br>Worst inspection ID: 199<br>Worst health score: 70.00 |
| 3 | All inspection records are invalid | 3<br>-1 3001 100 1.0 70 40<br>302 0 100 1.0 70 40<br>303 3003 100 1.0 70 0 | Valid inspections: 0<br>Invalid inspections: 3<br>Good: 0<br>Monitor: 0<br>Service Required: 0<br>Average health: 0.00<br>No valid inspection |
| 4 | Health score is limited to `0` and `100` | 2<br>401 4001 100 0.0 20 40<br>402 4002 100 15.0 150 1 | Valid inspections: 2<br>Invalid inspections: 0<br>Good: 1<br>Monitor: 0<br>Service Required: 1<br>Average health: 50.00<br>Worst inspection ID: 402<br>Worst health score: 0.00 |
| 5 | Exact health-category boundary values | 3<br>501 5001 100 1.5 70 40<br>502 5002 100 4.0 70 40<br>503 5003 100 5.0 70 40 | Valid inspections: 3<br>Invalid inspections: 0<br>Good: 1<br>Monitor: 1<br>Service Required: 1<br>Average health: 65.00<br>Worst inspection ID: 503<br>Worst health score: 50.00 |
| 6 | Boundary case with negative vibration invalid | 3<br>601 6001 100 -1.0 70 40<br>602 6002 100 2.0 70 40<br>603 6003 100 0.0 70 40 | Valid inspections: 2<br>Invalid inspections: 1<br>Good: 1<br>Monitor: 1<br>Service Required: 0<br>Average health: 90.00<br>Worst inspection ID: 602<br>Worst health score: 80.00 |

---

## 11. Notes

- The candidate may solve the problem using C, C++, or Python.
- The records must be represented using structures or objects.
- Invalid records must still be processed and counted.
- Sorting is not required to find the worst inspection.
- Output labels, capitalization, spacing, and ordering must match exactly.
