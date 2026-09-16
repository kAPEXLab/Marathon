# Question 3: Production Work Order Performance Analyzer

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

Manufacturing organizations maintain digital records of production work orders. These records help engineers compare planned and actual completion times, monitor defects, and evaluate production performance.

Write a modular program that processes multiple production work-order records and generates a performance summary.

The program must use structures or classes to represent the work orders and functions to process individual records and collections of records.

---

## 3. Scenario

Each completed production work order contains the following input information:

| Field | Description |
|---|---|
| Work Order ID | Unique identification number of the work order |
| Planned Time | Planned number of hours required to complete the work order |
| Actual Time | Actual number of hours taken to complete the work order |
| Defect Count | Number of defects detected after completion |

The program must calculate and store the following additional information for every work order:

| Field | Description |
|---|---|
| Performance Score | Calculated score in the range `0` to `100` |
| Category | Performance category assigned using the calculated score |
| Validity | Indicates whether the work-order record is valid |

### Valid Work Order

A work-order record is valid when all the following conditions are satisfied:

```text
workOrderId > 0
plannedTime > 0
actualTime > 0
defectCount >= 0
```

If any of these conditions is not satisfied, the work-order record is invalid.

### Performance Score Calculation

For every valid work-order record, calculate:

```text
timeScore = (plannedTime / actualTime) * 80

defectPenalty = defectCount * 5

performanceScore = timeScore - defectPenalty
```

The calculated performance score must be limited to the range `0` to `100`.

```text
If performanceScore > 100:
    performanceScore = 100

If performanceScore < 0:
    performanceScore = 0
```

### Performance Categories

| Performance Score | Category Code | Category |
|---:|:---:|---|
| `85` to `100` | `E` | Excellent |
| `70` to less than `85` | `G` | Good |
| `50` to less than `70` | `S` | Satisfactory |
| Less than `50` | `N` | Needs Improvement |
| Invalid record | `I` | Invalid |

---

## 4. Tasks to Implement

The program must perform the following tasks:

1. Read the number of work orders, `N`.
2. Read the details of all `N` work orders.
3. Store the work orders in an array, vector, or list of structures or objects.
4. Validate every work-order record.
5. Calculate the performance score of every valid work order.
6. Limit each calculated performance score to the range `0` to `100`.
7. Assign a performance category to every valid work order.
8. Assign category code `I` to every invalid work order.
9. Update the calculated fields of every work-order record.
10. Count the total number of valid work orders.
11. Count the total number of invalid work orders.
12. Count the work orders in each performance category.
13. Calculate the average performance score of all valid work orders.
14. Find the best-performing valid work order.
15. Apply the specified tie-breaking rule when multiple work orders have the same highest score.
16. Display the overall performance summary in the specified output format.
17. Organize the program using the mandatory functions described below.

---

## 5. Data Model

Each work order must be represented using a single structure, class, or object.

### Work Order Fields

| Field | Expected Type | Input or Calculated | Description |
|---|---|---|---|
| `workOrderId` | Integer | Input | Unique identification number of the work order |
| `plannedTime` | Real Number | Input | Planned completion time in hours |
| `actualTime` | Real Number | Input | Actual completion time in hours |
| `defectCount` | Integer | Input | Number of defects detected |
| `performanceScore` | Real Number | Calculated | Performance score in the range `0` to `100` |
| `category` | Character | Calculated | Category code `E`, `G`, `S`, `N`, or `I` |
| `isValid` | Boolean | Calculated | Indicates whether the record is valid |

### Language-Specific Data Representation

| Selected Language | Required Data Representation |
|---|---|
| C | Structure |
| C++ | Structure or class |
| Python | Class |

Only basic structure or class concepts are required.

Inheritance, polymorphism, abstract classes, templates, operator overloading, and design patterns are not required.

---

## 6. Function Details

Students must implement and use the following seven functions to create a modular program.

---

### 6.1 Function 1: Validate a Work Order

This function determines whether one work-order record contains valid input data.

- **Function Name:** `isValidWorkOrder`
- **Arguments:** `workOrder`
- **Return Type:** Boolean

#### Arguments

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `workOrder` | Work-order structure or object | Input | Work-order record that must be validated |

#### Return Values

| Return Value | Meaning |
|---|---|
| `true` | All input fields of the work order are valid |
| `false` | One or more input fields are invalid |

#### Function Description

The function must:

1. Receive one work-order record.
2. Check the Work Order ID, Planned Time, Actual Time, and Defect Count.
3. Return `true` when all validation conditions are satisfied.
4. Return `false` when at least one validation condition fails.
5. Not read any input.
6. Not print any output.
7. Not modify the work-order record.

---

### 6.2 Function 2: Calculate Performance Score

This function calculates the performance score of one valid work order.

- **Function Name:** `calculatePerformanceScore`
- **Arguments:** `workOrder`
- **Return Type:** Real Number

#### Arguments

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `workOrder` | Work-order structure or object | Input | Valid work-order record whose score must be calculated |

#### Return Value

| Return Value | Description |
|---|---|
| Real number from `0` to `100` | Calculated and limited performance score |

#### Function Description

The function must:

1. Receive one valid work-order record.
2. Calculate the time score.
3. Calculate the defect penalty.
4. Calculate the performance score.
5. Limit the score to the range `0` to `100`.
6. Return the final performance score.
7. Not modify the work-order record.
8. Not read input or print output.

---

### 6.3 Function 3: Determine Performance Category

This function determines the performance category from a calculated score.

- **Function Name:** `determineCategory`
- **Arguments:** `performanceScore`
- **Return Type:** Character

#### Arguments

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `performanceScore` | Real Number | Input | Calculated performance score |

#### Return Values

| Return Value | Category |
|:---:|---|
| `E` | Excellent |
| `G` | Good |
| `S` | Satisfactory |
| `N` | Needs Improvement |

#### Function Description

The function must:

1. Receive a valid performance score.
2. Compare the score with the category limits.
3. Return the appropriate category code.
4. Not read input or print output.
5. Not modify the supplied score.

---

### 6.4 Function 4: Process One Work Order

This function validates and updates one work-order record.

- **Function Name:** `processWorkOrder`
- **Arguments:** `workOrder`
- **Return Type:** None or Void

#### Arguments

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `workOrder` | Work-order structure or object | Input and Output | Work-order record whose calculated fields must be updated |

#### Function Description

The function must:

1. Receive one work-order record.
2. Call `isValidWorkOrder`.
3. Update the `isValid` field.
4. If the work order is valid:
   - Call `calculatePerformanceScore`.
   - Store the returned score in `performanceScore`.
   - Call `determineCategory`.
   - Store the returned category code in `category`.
5. If the work order is invalid:
   - Set `performanceScore` to `0`.
   - Set `category` to `I`.
6. Not read any input.
7. Not print any output.

#### Required Argument-Passing Method

| Selected Language | Required Method |
|---|---|
| C | Pass a pointer to the work-order structure |
| C++ | Pass the work-order object by reference |
| Python | Pass the work-order object and update its attributes |

---

### 6.5 Function 5: Process All Work Orders

This function processes all stored work-order records.

- **Function Name:** `processAllWorkOrders`
- **Arguments:** `workOrders`, `size`
- **Return Type:** None or Void

#### Arguments

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `workOrders` | Collection of work-order records | Input and Output | Work-order records that must be processed |
| `size` | Integer | Input | Number of stored work-order records |

#### Function Description

The function must:

1. Receive the collection of work-order records.
2. Receive the number of records.
3. Traverse all work-order records.
4. Call `processWorkOrder` for every record.
5. Ensure that the calculated fields of every record are updated.
6. Not read any input.
7. Not print any output.

#### Required Collection Passing

| Selected Language | Required Method |
|---|---|
| C | Pass the array of structures as a function argument |
| C++ | Pass the array or vector of objects by reference |
| Python | Pass the list of objects as a function argument |

---

### 6.6 Function 6: Find the Best Work Order

This function finds the best-performing valid work order.

- **Function Name:** `findBestWorkOrder`
- **Arguments:** `workOrders`, `size`
- **Return Type:** Integer

#### Arguments

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `workOrders` | Collection of work-order records | Input | Processed work-order records |
| `size` | Integer | Input | Number of work-order records |

#### Return Values

| Return Value | Meaning |
|---:|---|
| `0` to `size - 1` | Index of the best-performing valid work order |
| `-1` | No valid work order exists |

#### Function Description

The function must:

1. Examine only valid work orders.
2. Select the work order having the highest performance score.
3. If multiple valid work orders have the same highest score, select the work order having the smaller Work Order ID.
4. Return the array, vector, or list index of the selected work order.
5. Return `-1` when no valid work order exists.
6. Not modify the collection.
7. Not read input or print output.

---

### 6.7 Function 7: Count Work Orders by Category

This function counts work orders belonging to a specified category.

- **Function Name:** `countByCategory`
- **Arguments:** `workOrders`, `size`, `requiredCategory`
- **Return Type:** Integer

#### Arguments

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `workOrders` | Collection of work-order records | Input | Processed work-order records |
| `size` | Integer | Input | Number of work-order records |
| `requiredCategory` | Character | Input | Category code that must be counted |

#### Return Value

| Return Value | Description |
|---:|---|
| Zero or a positive integer | Number of work orders having the specified category code |

#### Function Description

The function must:

1. Traverse all processed work orders.
2. Compare each work order's category with `requiredCategory`.
3. Count the matching records.
4. Return the count.
5. Not modify the collection.
6. Not read input or print output.

---

### 6.8 Function 8: Calculate Average Performance Score

This function calculates the average performance score of all valid work orders.

- **Function Name:** `calculateAverageScore`
- **Arguments:** `workOrders`, `size`
- **Return Type:** Real Number

#### Arguments

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `workOrders` | Collection of work-order records | Input | Processed work-order records |
| `size` | Integer | Input | Number of work-order records |

#### Return Value

| Return Value | Description |
|---|---|
| Positive real number or zero | Average performance score of valid work orders |
| `0` | No valid work order exists |

#### Function Description

The function must:

1. Consider only valid work orders.
2. Calculate the sum of their performance scores.
3. Count the valid work orders.
4. Calculate and return their average score.
5. Return `0` when no valid work order exists.
6. Not modify the collection.
7. Not read input or print output.

---

### 6.9 Responsibilities of the Main Program

The main program must:

1. Read `N`.
2. Read and store all work-order records.
3. Call `processAllWorkOrders`.
4. Call `countByCategory` for category codes `E`, `G`, `S`, `N`, and `I`.
5. Calculate the valid count as:

    ```text
    validCount = excellentCount + goodCount + satisfactoryCount + needsImprovementCount
    ```

6. Use the Invalid category count as the invalid-record count.
7. Call `calculateAverageScore`.
8. Call `findBestWorkOrder`.
9. Display the overall performance summary.
10. If a valid work order exists, display the Work Order ID and score of the best work order.

---

## 7. Input Format

The first input contains one integer:

```text
N
```

Where `N` is the number of work-order records.

The next `N` input lines contain four space-separated values:

```text
workOrderId plannedTime actualTime defectCount
```

Where:

- `workOrderId` is an integer.
- `plannedTime` is a real number representing hours.
- `actualTime` is a real number representing hours.
- `defectCount` is an integer.

### Example Input Structure

```text
3
101 10 8 1
102 10 10 2
103 10 20 1
```

---

## 8. Output Format

### When at Least One Valid Work Order Exists

The program must print exactly the following nine lines:

```text
Valid work orders: <valid_count>
Invalid work orders: <invalid_count>
Excellent: <excellent_count>
Good: <good_count>
Satisfactory: <satisfactory_count>
Needs Improvement: <needs_improvement_count>
Average score: <average_score>
Best work order ID: <work_order_id>
Best work order score: <performance_score>
```

### When No Valid Work Order Exists

The program must print exactly the following eight lines:

```text
Valid work orders: 0
Invalid work orders: <invalid_count>
Excellent: 0
Good: 0
Satisfactory: 0
Needs Improvement: 0
Average score: 0.00
No valid work order
```

### Output Requirements

- The average performance score must be displayed with exactly two digits after the decimal point.
- The score of the best work order must be displayed with exactly two digits after the decimal point.
- No input prompts, debugging information, processed-record details, or additional explanatory messages must be printed.

---

## 9. Constraints and Assumptions

```text
1 <= N <= 1000

-1000000 <= workOrderId <= 1000000

-100000 <= plannedTime <= 100000

-100000 <= actualTime <= 100000

-1000 <= defectCount <= 1000
```

- Exactly `N` work-order records will be provided.
- Work Order IDs will be unique.
- Planned Time and Actual Time may be integers or real numbers.
- Valid Planned Time and Actual Time values are measured in hours.
- All inputs will be numeric.
- Handling malformed text input is not required.
- The records are not arranged by performance score.
- Work Order IDs are not required to be consecutive.

---

## 10. Rules and Clarifications

- **Rule 1, Valid Record:** A record is valid only when its Work Order ID, Planned Time, Actual Time, and Defect Count satisfy all validation conditions.
- **Rule 2, Invalid Record:** An invalid record must have a score of `0` and category code `I`.
- **Rule 3, Score Limit:** A calculated score greater than `100` must be changed to `100`.
- **Rule 4, Negative Score:** A calculated score below `0` must be changed to `0`.
- **Rule 5, Category Boundaries:** Scores equal to `85`, `70`, and `50` belong to categories `E`, `G`, and `S`, respectively.
- **Rule 6, Best Work Order:** Only valid work orders are considered when identifying the best work order.
- **Rule 7, Tie-Breaking:** When two valid work orders have equal highest scores, the work order with the smaller ID must be selected.
- **Rule 8, Average Score:** Invalid work orders must not be included in the average-score calculation.
- **Rule 9, Collection Order:** The original order of the work-order records must be preserved.
- **Rule 10, Mandatory Function Usage:** All eight mandatory functions must be implemented and used.

---

## 11. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Normal case with valid and invalid records | 4<br>101 10 8 1<br>102 10 10 2<br>103 10 20 1<br>104 0 5 0 | Valid work orders: 3<br>Invalid work orders: 1<br>Excellent: 1<br>Good: 1<br>Satisfactory: 0<br>Needs Improvement: 1<br>Average score: 66.67<br>Best work order ID: 101<br>Best work order score: 95.00 |
| 2 | Equal highest scores resolved using smaller Work Order ID | 3<br>201 10 10 0<br>199 10 10 0<br>205 10 20 0 | Valid work orders: 3<br>Invalid work orders: 0<br>Excellent: 0<br>Good: 2<br>Satisfactory: 0<br>Needs Improvement: 1<br>Average score: 66.67<br>Best work order ID: 199<br>Best work order score: 80.00 |
| 3 | All work-order records are invalid | 3<br>-1 10 8 0<br>302 0 5 1<br>303 10 -2 0 | Valid work orders: 0<br>Invalid work orders: 3<br>Excellent: 0<br>Good: 0<br>Satisfactory: 0<br>Needs Improvement: 0<br>Average score: 0.00<br>No valid work order |
| 4 | Performance scores limited to `0` and `100` | 2<br>401 20 10 0<br>402 10 100 30 | Valid work orders: 2<br>Invalid work orders: 0<br>Excellent: 1<br>Good: 0<br>Satisfactory: 0<br>Needs Improvement: 1<br>Average score: 50.00<br>Best work order ID: 401<br>Best work order score: 100.00 |
| 5 | Exact category boundary values | 4<br>501 85 80 0<br>502 70 80 0<br>503 50 80 0<br>504 49 80 0 | Valid work orders: 4<br>Invalid work orders: 0<br>Excellent: 1<br>Good: 1<br>Satisfactory: 1<br>Needs Improvement: 1<br>Average score: 63.50<br>Best work order ID: 501<br>Best work order score: 85.00 |
| 6 | Negative defect count makes a record invalid | 3<br>601 10 10 -1<br>602 15 10 2<br>603 10 10 5 | Valid work orders: 2<br>Invalid work orders: 1<br>Excellent: 1<br>Good: 0<br>Satisfactory: 1<br>Needs Improvement: 0<br>Average score: 77.50<br>Best work order ID: 602<br>Best work order score: 100.00 |

---

## 12. Notes

- The candidate may solve the problem using C, C++, or Python.
- All eight mandatory functions must be implemented and used.
- The work orders must be stored as structures or objects.
- The work-order collection must be passed as an argument to the required processing functions.
- C solutions must demonstrate passing a pointer to a structure to `processWorkOrder`.
- C++ solutions must demonstrate passing an object by reference to `processWorkOrder`.
- Python solutions must demonstrate passing and updating an object in `processWorkOrder`.
- Dynamic memory allocation is not required.
- Inheritance, polymorphism, templates, and other advanced OOP concepts are not required.
- Sorting is not required and should not be used to find the best work order.
- The original order of the work-order records must be preserved.
- Mandatory functions must not read input or print output.
- Output labels, capitalization, spacing, and ordering must match the specified output format.
- A linear-time solution is expected.

---
