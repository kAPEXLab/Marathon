# Question 1: Digital Wallet Transaction Processor

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

A digital wallet processes deposits and withdrawal requests in the order received. Write a program that applies the transactions and reports the final wallet summary.

---

## 3. Scenario

The wallet has an initial balance. Each transaction contains a type and an integer amount in the smallest currency unit.

| Type | Meaning |
|---|---|
| `D` | Deposit. The amount is added to the balance. |
| `W` | Withdrawal. The amount is deducted only when the balance is sufficient. |

A withdrawal that is greater than the current balance is rejected. A rejected withdrawal does not change the balance.

---

## 4. Tasks to Implement

The program must:

1. Read the initial balance and number of transactions, `N`.
2. Read and store all transactions.
3. Process transactions in input order.
4. Count deposits, successful withdrawals, and rejected withdrawals.
5. Find the largest successful withdrawal amount.
6. Display the final summary.

---

## 5. Function Details

Students must implement and use the following two functions. Each function returns one simple value or updates only its documented output argument.

### 5.1 Function 1: Process One Transaction

* Function Name: `processTransaction`
* Arguments: `currentBalance, transactionType, amount`
* Return type: `Integer`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `currentBalance` | Integer balance | Input and Output | Current wallet balance; update it only when the transaction is accepted |
| `transactionType` | Character | Input | `D` for deposit or `W` for withdrawal |
| `amount` | Integer | Input | Non-negative transaction amount |

The function must return:

- `1` when a deposit is applied
- `2` when a withdrawal is successful
- `0` when a withdrawal is rejected

The function must update the balance through the language-appropriate method. It must not read input or print output.

### 5.2 Function 2: Find the Largest Successful Withdrawal

* Function Name: `findLargestSuccessfulWithdrawal`
* Arguments: `transactions, transactionResults, size`
* Return type: `Integer`

| Argument | Expected Type | Direction | Description |
|---|---|---|---|
| `transactions` | Collection of transactions | Input | Stored transaction records |
| `transactionResults` | Collection of integers | Input | Result code for each transaction |
| `size` | Integer | Input | Number of transactions |

The function returns the largest amount among successful withdrawals, or `0` when there are none. It must not read input, print output, or modify the stored transactions.

### 5.3 Language-Specific Argument Passing

When an argument is marked **Input and Output**, the function must update the caller's value. In C, pass a pointer and dereference it inside the function. In C++, pass the argument by reference. In Python, update the mutable object or use the language-appropriate mutable container. An output array or output count follows the same rule.

---

## 6. Input Format

The first input contains two space-separated integers:

```text
initialBalance N
```

The next `N` lines contain:

```text
transactionType amount
```

`transactionType` is either `D` or `W`. Amounts are non-negative integers.

---

## 7. Output Format

Print exactly:

```text
Final balance: <balance>
Deposits: <deposit_count>
Successful withdrawals: <successful_withdrawal_count>
Rejected withdrawals: <rejected_withdrawal_count>
Largest successful withdrawal: <amount>
```

If there are no successful withdrawals, print `Largest successful withdrawal: 0`.

---

## 8. Constraints and Assumptions

```text
0 <= initialBalance <= 1000000
1 <= N <= 1000
0 <= amount <= 1000000
```

- All transaction types are valid.
- All amounts are integer currency units.
- Transactions must be processed in their original order.

---

## 9. Rules and Clarifications

* Rule 1 Deposit: Every deposit is applied and counted.
* Rule 2 Successful Withdrawal: A withdrawal is successful when `amount <= currentBalance`.
* Rule 3 Rejected Withdrawal: A withdrawal is rejected when `amount > currentBalance`.
* Rule 4 Rejected Effect: A rejected withdrawal does not change the balance or largest successful withdrawal.
* Rule 5 Zero Amount: A zero-amount transaction is valid. A zero withdrawal is successful when processed.
* Rule 6 Mandatory Function Usage: Both required functions must be implemented and used.

---

## 10. Test Cases

| Test Case | Purpose | Exact Input | Exact Expected Output |
|---:|---|---|---|
| 1 | Normal deposits and withdrawals | `1000 5`<br>`D 500`<br>`W 200`<br>`W 900`<br>`D 300`<br>`W 400` | `Final balance: 300`<br>`Deposits: 2`<br>`Successful withdrawals: 3`<br>`Rejected withdrawals: 0`<br>`Largest successful withdrawal: 900` |
| 2 | Several successful withdrawals | `500 4`<br>`W 100`<br>`W 200`<br>`D 50`<br>`W 250` | `Final balance: 0`<br>`Deposits: 1`<br>`Successful withdrawals: 3`<br>`Rejected withdrawals: 0`<br>`Largest successful withdrawal: 250` |
| 3 | All withdrawals are rejected | `100 3`<br>`W 101`<br>`W 200`<br>`W 1000` | `Final balance: 100`<br>`Deposits: 0`<br>`Successful withdrawals: 0`<br>`Rejected withdrawals: 3`<br>`Largest successful withdrawal: 0` |
| 4 | Deposits restore the balance | `0 5`<br>`D 200`<br>`W 100`<br>`D 50`<br>`W 150`<br>`W 1` | `Final balance: 0`<br>`Deposits: 2`<br>`Successful withdrawals: 2`<br>`Rejected withdrawals: 1`<br>`Largest successful withdrawal: 150` |
| 5 | Boundary case with zero initial balance and zero amounts | `0 4`<br>`W 0`<br>`W 1`<br>`D 0`<br>`D 5` | `Final balance: 5`<br>`Deposits: 2`<br>`Successful withdrawals: 1`<br>`Rejected withdrawals: 1`<br>`Largest successful withdrawal: 0` |
| 6 | Boundary case with one transaction | `75 1`<br>`W 75` | `Final balance: 0`<br>`Deposits: 0`<br>`Successful withdrawals: 1`<br>`Rejected withdrawals: 0`<br>`Largest successful withdrawal: 75` |

---

## 11. Notes

- The candidate may solve the problem using C, C++, or Python.
- No transaction may be reordered.
- Output labels, capitalization, spacing, and ordering must match exactly.
