# Question 3: Three-Phase Load Analyzer

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

An electrical panel distributes loads across three phases. Write a program that analyzes the distribution and identifies phase imbalance and overloaded phases.

---

## 3. Scenario

Each load record contains a load ID, a phase, and the load power in watts.

| Phase | Meaning |
|---|---|
| `A` | Phase A |
| `B` | Phase B |
| `C` | Phase C |

For every valid load record, add its power to the total of its phase. A phase is overloaded when its total power is strictly greater than the permitted phase limit.

---

## 4. Tasks to Implement

The program must:

1. Read the number of load records, `N`, and the permitted phase limit.
2. Read and store all load records.
3. Validate the phase of every record.
4. Calculate the total power and load count for each phase.
5. Find the phase with the greatest total power.
6. Calculate the difference between the greatest and smallest phase totals.
7. Count overloaded phases.
8. Display the load summary.

---

## 5. Function Details

Students must implement and use the following functions.

### 5.1 Function 1: Validate a Phase

* Function Name: `isValidPhase`
* Arguments: `phase`
* Return type: `Boolean`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `phase` | Character | Input | Phase identifier `A`, `B`, or `C` |

The function returns `true` only when `phase` is `A`, `B`, or `C`. It must not read input or print output.

### 5.2 Function 2: Find the Heaviest Phase

* Function Name: `findHeaviestPhase`
* Arguments: `phaseTotals`
* Return type: `Character`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `phaseTotals` | Array of three integers | Input | Totals for phases A, B, and C |

The function returns the phase with the greatest total power. If phases are tied, return the alphabetically smallest phase: `A` before `B` before `C`.

### 5.3 Function 3: Find the Load Difference

* Function Name: `findLoadDifference`
* Arguments: `phaseTotals`
* Return type: `Integer`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `phaseTotals` | Array of three integers | Input | Totals for phases A, B, and C |

The function returns the greatest phase total minus the smallest phase total.

### 5.4 Function 4: Count Overloaded Phases

* Function Name: `countOverloadedPhases`
* Arguments: `phaseTotals, phaseLimit`
* Return type: `Integer`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `phaseTotals` | Array of three integers | Input | Totals for phases A, B, and C |
| `phaseLimit` | Integer | Input | Permitted total per phase |

The function returns the number of phases whose total power is strictly greater than `phaseLimit`.

### 5.5 Language-Specific Argument Passing

When an argument is marked **Input and Output**, the function must update the caller's value. In C, pass a pointer and dereference it inside the function. In C++, pass the argument by reference. In Python, update the mutable object or use the language-appropriate mutable container. An output array or output count follows the same rule.

All functions must not read input or print output.

---

## 6. Input Format

The first input contains two space-separated values:

```text
N phaseLimit
```

The next `N` lines contain:

```text
loadId phase power
```

`loadId` is an integer, `phase` is `A`, `B`, or `C`, and `power` is an integer number of watts.

---

## 7. Output Format

Print exactly:

```text
Phase A total: <total_a>
Phase B total: <total_b>
Phase C total: <total_c>
Heaviest phase: <phase>
Load difference: <difference>
Overloaded phases: <count>
```

---

## 8. Constraints and Assumptions

```text
1 <= N <= 1000
0 <= phaseLimit <= 1000000
1 <= loadId <= 1000000
0 <= power <= 1000000
```

- Load IDs are unique.
- Every phase value is valid.
- All records must be processed in input order.

---

## 9. Rules and Clarifications

* Rule 1 Phase Totals: Add each load power to exactly one phase total.
* Rule 2 Empty Phase: A phase with no load records has total power `0` and count `0`.
* Rule 3 Heaviest Tie: If phase totals are equal, select `A`, then `B`, then `C`.
* Rule 4 Overload Boundary: A phase equal to `phaseLimit` is not overloaded.
* Rule 5 Load Difference: Calculate maximum total minus minimum total, including empty phases.
* Rule 6 Mandatory Function Usage: All five required functions must be implemented and used.

---

## 10. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Normal load distribution | `5 1000`<br>`101 A 400`<br>`102 B 300`<br>`103 C 500`<br>`104 A 200`<br>`105 B 250` | `Phase A total: 600`<br>`Phase B total: 550`<br>`Phase C total: 500`<br>`Heaviest phase: A`<br>`Load difference: 100`<br>`Overloaded phases: 0` |
| 2 | One phase is overloaded | `4 500`<br>`201 A 300`<br>`202 B 300`<br>`203 C 100`<br>`204 A 250` | `Phase A total: 550`<br>`Phase B total: 300`<br>`Phase C total: 100`<br>`Heaviest phase: A`<br>`Load difference: 450`<br>`Overloaded phases: 1` |
| 3 | Balanced phases | `6 100`<br>`301 A 100`<br>`302 B 100`<br>`303 C 100`<br>`304 A 100`<br>`305 B 100`<br>`306 C 100` | `Phase A total: 200`<br>`Phase B total: 200`<br>`Phase C total: 200`<br>`Heaviest phase: A`<br>`Load difference: 0`<br>`Overloaded phases: 3` |
| 4 | Only one phase has loads | `3 500`<br>`401 C 120`<br>`402 C 80`<br>`403 C 50` | `Phase A total: 0`<br>`Phase B total: 0`<br>`Phase C total: 250`<br>`Heaviest phase: C`<br>`Load difference: 250`<br>`Overloaded phases: 0` |
| 5 | Boundary case with zero power and zero limit | `3 0`<br>`501 A 0`<br>`502 B 0`<br>`503 C 0` | `Phase A total: 0`<br>`Phase B total: 0`<br>`Phase C total: 0`<br>`Heaviest phase: A`<br>`Load difference: 0`<br>`Overloaded phases: 0` |
| 6 | Boundary case with one load | `1 100`<br>`601 B 100` | `Phase A total: 0`<br>`Phase B total: 100`<br>`Phase C total: 0`<br>`Heaviest phase: B`<br>`Load difference: 100`<br>`Overloaded phases: 0` |

---

## 11. Notes

- The candidate may solve the problem using C, C++, or Python.
- No sorting is required.
- Output labels, capitalization, spacing, and ordering must match exactly.
