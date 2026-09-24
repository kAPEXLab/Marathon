# Question 4: Industrial Equipment Event Log Analysis and Reporting System

## 1. Assignment Details

| Attribute | Details |
|---|---|
| Assessment Type | Requirements-based software development assignment |
| Difficulty | Advanced |
| Supported Languages | C, C++, or Python |
| Internet Access | Allowed |
| AI Tools | Allowed |
| Reference Material | Allowed |
| Assessment Mode | Individual |
| Input Method | CSV files |

---

## 2. Assignment Objective

You are provided with a software requirements document and a set of CSV input files.

Your task is to:

1. Study and understand the requirements.
2. Identify the required data entities and processing state.
3. Design an appropriate modular software solution.
4. Implement the solution.
5. Execute the supplied test cases.
6. Process the large assessment dataset.
7. Generate the required output files.
8. Verify the correctness and consistency of the results.

You may use internet resources, programming documentation, and AI tools.

However, you are responsible for understanding, reviewing, testing, correcting, and explaining the complete solution.

---

## 3. Business Context

An industrial facility operates multiple production machines. Each machine periodically generates event records containing:

- Operating status
- Temperature
- Vibration
- Production count
- Defect count

The machine-event file may contain several hundred thousand records.

Some records may be:

- Incomplete
- Duplicated
- Invalid
- Out of chronological order
- Associated with an unknown machine
- Operationally abnormal

The system must validate and process the records, detect operating anomalies, calculate machine-wise statistics, and generate the required reports.

---

## 4. Scope

The system shall:

1. Read machine information from `machine_master.csv`.
2. Read machine-event information from `machine_events.csv`.
3. Validate machine-master and machine-event records.
4. Reject duplicate Machine IDs and duplicate Event IDs.
5. Reject events associated with invalid or unknown machines.
6. Reject out-of-order events.
7. Detect temperature and vibration anomalies.
8. Calculate machine-wise operational statistics.
9. Generate the required CSV reports.
10. Display the overall processing summary.
11. Process a large event file efficiently.

The scope does not include:

- Graphical user interfaces
- Databases
- Hardware interfacing
- Network communication
- Real-time machine connectivity
- Cloud deployment
- Authentication or authorization
- Third-party service integration

---

# 5. Input File Specifications

## 5.1 Input File: `machine_master.csv`

The file contains the following columns:

| Column | Expected Type | Description |
|---|---|---|
| `machine_id` | Integer | Unique identification number of the machine |
| `machine_type` | Text | Type of machine |
| `minimum_temperature` | Real Number | Minimum permitted operating temperature |
| `maximum_temperature` | Real Number | Maximum permitted operating temperature |
| `maximum_vibration` | Real Number | Maximum permitted vibration level |
| `location` | Text | Machine location within the industrial facility |

### Required Header

```csv
machine_id,machine_type,minimum_temperature,maximum_temperature,maximum_vibration,location
```

---

## 5.2 Input File: `machine_events.csv`

The file contains the following columns:

| Column | Expected Type | Description |
|---|---|---|
| `event_id` | Integer | Unique identification number of the event |
| `machine_id` | Integer | Identification number of the machine generating the event |
| `timestamp` | Integer | Event time represented as elapsed seconds |
| `status` | Text | Operating status of the machine |
| `temperature` | Real Number | Recorded machine temperature |
| `vibration` | Real Number | Recorded machine vibration |
| `units_produced` | Integer | Cumulative production count |
| `defect_count` | Integer | Cumulative defect count |

### Required Header

```csv
event_id,machine_id,timestamp,status,temperature,vibration,units_produced,defect_count
```

### Permitted Status Values

```text
RUNNING
IDLE
MAINTENANCE
STOPPED
```

---

# 6. Machine-Master Validation Requirements

A machine-master record is valid only when all the following conditions are satisfied:

```text
machine_id > 0
machine_type is not empty
minimum_temperature is numeric
maximum_temperature is numeric
minimum_temperature < maximum_temperature
maximum_vibration is numeric
maximum_vibration > 0
location is not empty
```

Machine IDs must be unique.

If the same Machine ID occurs more than once:

1. Every record containing that Machine ID must be treated as a duplicate.
2. None of those records may be used for event processing.
3. Every duplicate record must be written to `rejected_records.csv`.

Duplicate Machine IDs may occur far apart in the file.

---

# 7. Machine-Event Validation Requirements

A machine-event record is valid only when all the following conditions are satisfied:

```text
event_id > 0
machine_id > 0
timestamp >= 0
status is one of the permitted status values
temperature is numeric
vibration is numeric
vibration >= 0
units_produced is an integer
units_produced >= 0
defect_count is an integer
defect_count >= 0
defect_count <= units_produced
```

The Machine ID in the event record must refer to a valid and unique machine in `machine_master.csv`.

Event IDs must be unique.

If the same Event ID occurs more than once:

1. Every event containing that Event ID must be treated as a duplicate.
2. None of those event records may be accepted.
3. Every duplicate event record must be written to `rejected_records.csv`.

Duplicate Event IDs may occur far apart in the event file.

---

# 8. Event Acceptance Requirements

An event shall be accepted only when:

1. The record contains all required fields.
2. All fields satisfy the validation requirements.
3. The Event ID is unique.
4. The Machine ID identifies a valid and unique machine.
5. The timestamp is not earlier than the previously accepted event for the same machine.

An accepted event shall:

- Contribute to machine-wise statistics.
- Update the latest machine information.
- Be checked for temperature and vibration anomalies.

A rejected event shall not:

- Contribute to machine-wise statistics.
- Generate an operating anomaly.
- Update the previous accepted event of the machine.
- Update the latest production or defect count.

---

# 9. Out-of-Order Event Requirement

Events must be processed in the order in which they appear in `machine_events.csv`.

For each machine, compare the timestamp of the current event with the timestamp of the previously accepted event for that machine.

An event is out of order when:

```text
currentTimestamp < previousAcceptedTimestamp
```

An out-of-order event must:

- Be rejected
- Use reason code `OUT_OF_ORDER_TIMESTAMP`
- Be written to `rejected_records.csv`
- Not affect machine-wise statistics
- Not replace the previous accepted event

Events having the same timestamp are allowed.

---

# 10. Anomaly Detection Requirements

Operating anomalies apply only to accepted events.

## 10.1 Low-Temperature Anomaly

A low-temperature anomaly occurs when:

```text
temperature < minimum_temperature
```

Use anomaly code:

```text
LOW_TEMPERATURE
```

The reference value shall be the minimum permitted temperature.

---

## 10.2 High-Temperature Anomaly

A high-temperature anomaly occurs when:

```text
temperature > maximum_temperature
```

Use anomaly code:

```text
HIGH_TEMPERATURE
```

The reference value shall be the maximum permitted temperature.

---

## 10.3 High-Vibration Anomaly

A high-vibration anomaly occurs when:

```text
vibration > maximum_vibration
```

Use anomaly code:

```text
HIGH_VIBRATION
```

The reference value shall be the maximum permitted vibration.

---

## 10.4 Boundary Values

The following values are not anomalies:

```text
temperature == minimum_temperature
temperature == maximum_temperature
vibration == maximum_vibration
```

---

## 10.5 Multiple Anomalies

One accepted event may contain multiple anomalies.

Each detected anomaly must be written as a separate row in `anomalies.csv`.

If an event contains multiple anomalies, write them in the following order:

1. `LOW_TEMPERATURE` or `HIGH_TEMPERATURE`
2. `HIGH_VIBRATION`

---

# 11. Machine-Wise Statistics

For every valid and unique machine, the system shall calculate:

- Number of accepted events
- Number of `RUNNING` events
- Number of `IDLE` events
- Number of `MAINTENANCE` events
- Number of `STOPPED` events
- Average temperature
- Maximum vibration
- Latest production count
- Latest defect count
- Number of accepted events containing a temperature anomaly
- Number of accepted events containing a vibration anomaly

The latest production and defect counts shall be obtained from the last accepted event processed for the machine.

A valid machine must appear in `machine_summary.csv` even when it has no accepted events.

---

# 12. Data-Modelling and Program-Design Requirements

The internal design of the program is not fully prescribed.

Based on your understanding of the requirements, decide:

1. Which values should be represented using individual variables.
2. Which related values should be grouped into structures, classes, records, dictionaries, or equivalent data models.
3. Which data should be stored in arrays, vectors, lists, maps, dictionaries, sets, or other collections.
4. Which processing state must be maintained separately for every machine.
5. Which values are temporary and need not be stored.
6. Which information is required for duplicate detection.
7. Which information is required for machine lookup.
8. Which information is required for report generation.
9. Which functions, methods, or modules are required.

The question does not prescribe:

- The exact number of structures or classes
- The exact fields of each structure or class
- The complete internal algorithm
- The use of one-pass or multiple-pass processing
- The storage of the complete event file in memory

The suitability, clarity, efficiency, and correctness of the selected design will be evaluated.

Creating more structures, classes, or functions does not automatically result in higher marks.

---

# 13. Modular Program Requirements

The solution must follow a modular design.

The complete processing logic must not be written entirely inside the main function.

The program must contain separate functions, methods, or modules for major responsibilities such as:

- CSV record parsing
- Record validation
- Duplicate detection
- Event processing
- Anomaly detection
- Machine-wise statistics
- Output-file generation

The candidate may create additional helper functions.

Global variables should not be used as the primary mechanism for exchanging processing results between modules.

---

# 14. Mandatory Logical Interfaces

The following are logical, language-independent interfaces.

Language-specific implementation syntax may differ, but equivalent functionality must be provided.

## 14.1 Parse Machine Record

```text
parseMachineRecord(csvRow, lineNumber) -> MachineParseResult
```

### Arguments

| Argument | Expected Type | Description |
|---|---|---|
| `csvRow` | Text | Complete CSV row containing one machine-master record |
| `lineNumber` | Integer | Physical line number in `machine_master.csv` |

### Structured Return Value

`MachineParseResult` must provide:

- Whether parsing succeeded
- Parsed machine information, when available
- Machine ID, when it can be determined
- Input line number
- Rejection reason when parsing fails

---

## 14.2 Parse Machine Event

```text
parseEventRecord(csvRow, lineNumber) -> EventParseResult
```

### Arguments

| Argument | Expected Type | Description |
|---|---|---|
| `csvRow` | Text | Complete CSV row containing one event record |
| `lineNumber` | Integer | Physical line number in `machine_events.csv` |

### Structured Return Value

`EventParseResult` must provide:

- Whether parsing succeeded
- Parsed event information, when available
- Event ID, when it can be determined
- Input line number
- Rejection reason when parsing fails

---

## 14.3 Validate Machine Record

```text
validateMachine(machineRecord) -> ValidationResult
```

### Arguments

| Argument | Expected Type | Description |
|---|---|---|
| `machineRecord` | Complete machine record | Parsed machine-master information |

### Structured Return Value

`ValidationResult` must provide:

- Whether the record is valid
- Rejection reason when invalid

Duplicate Machine ID detection may be handled separately because it requires information from multiple records.

---

## 14.4 Validate Event Record

```text
validateEvent(eventRecord, validMachines) -> ValidationResult
```

### Arguments

| Argument | Expected Type | Description |
|---|---|---|
| `eventRecord` | Complete event record | Parsed event information |
| `validMachines` | Machine collection or lookup | Valid and unique machine records |

### Structured Return Value

`ValidationResult` must provide:

- Whether the event is valid
- Rejection reason when invalid

Duplicate Event ID and out-of-order checks may be handled separately because they require additional processing context.

---

## 14.5 Detect Anomalies

```text
detectAnomalies(eventRecord, machineRecord) -> AnomalyResult
```

### Arguments

| Argument | Expected Type | Description |
|---|---|---|
| `eventRecord` | Complete event record | Current accepted event |
| `machineRecord` | Complete machine record | Machine limits and machine information |

### Structured Return Value

`AnomalyResult` must provide:

- Number of anomalies detected
- Zero, one, or more anomaly records
- Anomaly codes
- Observed values
- Reference values

---

## 14.6 Language-Specific Interpretation

### C

A C solution may use:

- Structures
- Arrays of structures
- Pointers to structures
- Structures returned from functions
- Output structures updated through pointers

At least one function must receive a pointer to a structure or processing context.

### C++

A C++ solution may use:

- Structures or classes
- Objects passed by reference
- Constant references
- Vectors or other suitable collections
- Structures, classes, or tuples as return values

At least one function must receive a record or collection by reference.

### Python

A Python solution may use:

- Classes
- Data classes
- Dictionaries
- Tuples
- Lists of records or objects
- Structured result objects

Python candidates are not expected to use pointer syntax.

---

# 15. File-Handling Requirements

The program must:

1. Read input data from the supplied CSV files.
2. Not hard-code input records.
3. Skip the heading row.
4. Ignore blank lines.
5. Remove leading and trailing spaces around individual fields.
6. Process records until the end of the file.
7. Not assume a fixed number of records.
8. Continue processing after a rejected record whenever safely possible.
9. Generate all required output files.
10. Include the specified header in every CSV output file.
11. Close all files correctly.
12. Report a file-opening error and terminate safely when an input file cannot be opened.

The supplied CSV files will use:

- A comma as the field separator
- One record per line
- No commas inside text fields
- No multiline text fields

---

# 16. Duplicate Detection Requirement

Duplicate identifiers may appear far apart in the input files.

A solution that rejects only the second and later occurrence of a duplicated identifier does not satisfy the requirements.

Every occurrence of a duplicated Machine ID or Event ID must be rejected.

The candidate may use:

- Multiple file passes
- Frequency-counting collections
- Temporary record storage
- Another correct and documented approach

The selected duplicate-detection approach must be explained in the submitted README.

---

# 17. Rejection Reason Codes

## 17.1 Machine-Master Reason Codes

| Reason Code | Meaning |
|---|---|
| `INCOMPLETE_MACHINE_RECORD` | One or more required fields are missing |
| `INVALID_MACHINE_ID` | Machine ID is missing, non-numeric, zero, or negative |
| `DUPLICATE_MACHINE_ID` | Machine ID occurs more than once |
| `MISSING_MACHINE_TYPE` | Machine type is empty |
| `INVALID_TEMPERATURE_LIMITS` | Temperature limits are non-numeric or minimum is not less than maximum |
| `INVALID_VIBRATION_LIMIT` | Maximum vibration is missing, non-numeric, zero, or negative |
| `MISSING_LOCATION` | Machine location is empty |

## 17.2 Machine-Event Reason Codes

| Reason Code | Meaning |
|---|---|
| `INCOMPLETE_EVENT_RECORD` | One or more required fields are missing |
| `INVALID_EVENT_ID` | Event ID is missing, non-numeric, zero, or negative |
| `DUPLICATE_EVENT_ID` | Event ID occurs more than once |
| `INVALID_MACHINE_ID` | Machine ID is missing, non-numeric, zero, or negative |
| `UNKNOWN_MACHINE_ID` | Machine ID does not refer to a valid and unique machine |
| `INVALID_TIMESTAMP` | Timestamp is missing, non-numeric, or negative |
| `OUT_OF_ORDER_TIMESTAMP` | Timestamp is earlier than the previously accepted event for the same machine |
| `INVALID_STATUS` | Status is not a permitted value |
| `INVALID_TEMPERATURE` | Temperature is missing or non-numeric |
| `INVALID_VIBRATION` | Vibration is missing, non-numeric, or negative |
| `INVALID_PRODUCTION_COUNT` | Production count is missing, non-numeric, or negative |
| `INVALID_DEFECT_COUNT` | Defect count is missing, non-numeric, negative, or greater than production count |

---

# 18. Validation Priority

A record may violate more than one validation requirement.

Only one primary rejection reason shall be reported.

## 18.1 Machine-Master Validation Priority

Apply the following order:

1. `INCOMPLETE_MACHINE_RECORD`
2. `INVALID_MACHINE_ID`
3. `DUPLICATE_MACHINE_ID`
4. `MISSING_MACHINE_TYPE`
5. `INVALID_TEMPERATURE_LIMITS`
6. `INVALID_VIBRATION_LIMIT`
7. `MISSING_LOCATION`

## 18.2 Machine-Event Validation Priority

Apply the following order:

1. `INCOMPLETE_EVENT_RECORD`
2. `INVALID_EVENT_ID`
3. `DUPLICATE_EVENT_ID`
4. `INVALID_MACHINE_ID`
5. `UNKNOWN_MACHINE_ID`
6. `INVALID_TIMESTAMP`
7. `OUT_OF_ORDER_TIMESTAMP`
8. `INVALID_STATUS`
9. `INVALID_TEMPERATURE`
10. `INVALID_VIBRATION`
11. `INVALID_PRODUCTION_COUNT`
12. `INVALID_DEFECT_COUNT`

The first applicable reason code must be reported.

---

# 19. Required Output Files

The program must generate:

```text
machine_summary.csv
anomalies.csv
rejected_records.csv
```

The overall processing summary must be displayed on the console.

---

# 20. Output File: `machine_summary.csv`

The file must contain one row for every valid and unique machine.

### Required Header

```csv
machine_id,machine_type,location,accepted_event_count,running_event_count,idle_event_count,maintenance_event_count,stopped_event_count,average_temperature,maximum_vibration,latest_units_produced,latest_defect_count,temperature_anomaly_count,vibration_anomaly_count
```

### Requirements

- Machine rows must appear in the same order as the valid machine records in `machine_master.csv`.
- `average_temperature` must contain exactly two digits after the decimal point.
- `maximum_vibration` must contain exactly two digits after the decimal point.
- The latest counts shall come from the last accepted event processed for the machine.

If a valid machine has no accepted events:

```text
accepted_event_count = 0
all status counts = 0
average_temperature = 0.00
maximum_vibration = 0.00
latest_units_produced = 0
latest_defect_count = 0
all anomaly counts = 0
```

---

# 21. Output File: `anomalies.csv`

### Required Header

```csv
event_id,machine_id,timestamp,anomaly_code,observed_value,reference_value
```

### Requirements

- One anomaly must be written per output row.
- One accepted event may produce multiple rows.
- Anomalies must appear in the order in which the events are accepted.
- Multiple anomalies for the same event must follow the specified anomaly order.
- Rejected events must not appear in this file.

---

# 22. Output File: `rejected_records.csv`

### Required Header

```csv
source_file,line_number,record_id,reason_code
```

Where:

- `source_file` is `machine_master.csv` or `machine_events.csv`.
- `line_number` is the physical line number, including the header row.
- `record_id` is the Machine ID or Event ID when it can be determined.
- Use `UNKNOWN` when the identifier cannot be determined.

### Output Order

Rejected records must be written in the following order:

1. Rejected machine-master records
2. Rejected event records

Within each source file, rejected records must follow their physical input-file order.

---

# 23. Console Processing Summary

The program must display exactly the following fields:

```text
Total machine records: <count>
Valid unique machines: <count>
Rejected machine records: <count>
Total event records: <count>
Accepted event records: <count>
Rejected event records: <count>
Temperature anomaly events: <count>
Vibration anomaly events: <count>
Total anomaly records: <count>
```

### Counting Requirements

- Header rows are not counted.
- Blank lines are not counted.
- Each rejected record must be counted once.
- An event containing both a temperature and vibration anomaly:
  - Counts once under `Temperature anomaly events`
  - Counts once under `Vibration anomaly events`
  - Generates two anomaly records
- `Total anomaly records` is the number of data rows written to `anomalies.csv`.

---

# 24. Sample Input Data

## 24.1 Sample `machine_master.csv`

```csv
machine_id,machine_type,minimum_temperature,maximum_temperature,maximum_vibration,location
101,Cutting,20.0,80.0,6.0,LineA
102,Welding,25.0,100.0,8.0,LineA
103,Packing,15.0,60.0,4.0,LineB
104,Drilling,20.0,75.0,5.0,LineC
104,Drilling,20.0,78.0,5.5,LineD
105,Inspection,70.0,30.0,3.0,LineB
```

## 24.2 Sample `machine_events.csv`

```csv
event_id,machine_id,timestamp,status,temperature,vibration,units_produced,defect_count
10001,101,100,RUNNING,55.5,3.2,100,2
10002,101,110,RUNNING,85.0,6.0,110,3
10003,102,105,IDLE,45.0,2.1,80,1
10004,101,105,RUNNING,60.0,3.0,105,2
10005,103,90,RUNNING,15.0,4.0,40,1
10006,999,100,RUNNING,45.0,2.0,20,0
10007,102,115,RUNNING,50.0,3.0,90,2
10007,102,120,RUNNING,52.0,3.2,95,2
10008,102,125,ACTIVE,55.0,3.0,100,2
10009,103,100,RUNNING,61.0,4.5,50,2
10010,103,110,RUNNING,55.0,3.5,45,3
10011,103,120,RUNNING,50.0,3.0,60,61
```

---

# 25. Expected Sample Output

## 25.1 Expected `machine_summary.csv`

```csv
machine_id,machine_type,location,accepted_event_count,running_event_count,idle_event_count,maintenance_event_count,stopped_event_count,average_temperature,maximum_vibration,latest_units_produced,latest_defect_count,temperature_anomaly_count,vibration_anomaly_count
101,Cutting,LineA,2,2,0,0,0,70.25,6.00,110,3,1,0
102,Welding,LineA,1,0,1,0,0,45.00,2.10,80,1,0,0
103,Packing,LineB,3,3,0,0,0,43.67,4.50,45,3,1,1
```

## 25.2 Expected `anomalies.csv`

```csv
event_id,machine_id,timestamp,anomaly_code,observed_value,reference_value
10002,101,110,HIGH_TEMPERATURE,85.0,80.0
10009,103,100,HIGH_TEMPERATURE,61.0,60.0
10009,103,100,HIGH_VIBRATION,4.5,4.0
```

## 25.3 Expected `rejected_records.csv`

```csv
source_file,line_number,record_id,reason_code
machine_master.csv,5,104,DUPLICATE_MACHINE_ID
machine_master.csv,6,104,DUPLICATE_MACHINE_ID
machine_master.csv,7,105,INVALID_TEMPERATURE_LIMITS
machine_events.csv,5,10004,OUT_OF_ORDER_TIMESTAMP
machine_events.csv,7,10006,UNKNOWN_MACHINE_ID
machine_events.csv,8,10007,DUPLICATE_EVENT_ID
machine_events.csv,9,10007,DUPLICATE_EVENT_ID
machine_events.csv,10,10008,INVALID_STATUS
machine_events.csv,13,10011,INVALID_DEFECT_COUNT
```

## 25.4 Expected Console Output

```text
Total machine records: 6
Valid unique machines: 3
Rejected machine records: 3
Total event records: 12
Accepted event records: 6
Rejected event records: 6
Temperature anomaly events: 2
Vibration anomaly events: 1
Total anomaly records: 3
```

---

# 26. Supplied Test Cases

Test-case folders are available at [https://github.com/kAPEXLab/Marathon/blob/881638803e596b4000054503fb692dd6085aadd1/testcase.zip](https://github.com/kAPEXLab/Marathon/blob/881638803e596b4000054503fb692dd6085aadd1/testcase.zip).

Each test-case folder may contain:

```text
machine_master.csv
machine_events.csv
expected_machine_summary.csv
expected_anomalies.csv
expected_rejected_records.csv
expected_console_output.txt
```

The purpose of each test case will not be stated.

You must analyse the requirements and determine the conditions exercised by each test case.

---

# 27. Test-Case Execution Guidelines

For every supplied test case:

1. Use the supplied `machine_master.csv` and `machine_events.csv`.
2. Do not modify the input files.
3. Execute the program.
4. Verify that all three output files are generated.
5. Verify the console summary.
6. Compare generated outputs with the supplied expected outputs.
7. Compare:
   - File name
   - Header and column order
   - Number of rows
   - Row order
   - Field values
   - Reason codes
   - Anomaly codes
   - Decimal formatting
   - Summary counts
8. Identify the first mismatch, if any.
9. Determine whether the mismatch is related to:
   - CSV parsing
   - Validation
   - Validation priority
   - Duplicate detection
   - Machine lookup
   - Timestamp ordering
   - Anomaly detection
   - Statistics
   - Output ordering
   - Output formatting
10. Correct the implementation.
11. Re-run the failed test.
12. Re-run previously passed tests after every correction.

The candidate must not:

- Modify the expected output files.
- Hard-code the output of a test case.
- Add conditions based on test-case names or numbers.
- Assume that visible test cases cover every possible condition.

---

# 28. Test-Case Verification Guidelines

While analysing the supplied test cases, verify that:

- All occurrences of a duplicated Machine ID are rejected.
- All occurrences of a duplicated Event ID are rejected.
- Invalid and unknown machines cannot receive accepted events.
- A rejected event does not affect machine statistics.
- An out-of-order event does not replace the previous accepted event.
- Boundary temperature values are not treated as anomalies.
- Boundary vibration values are not treated as anomalies.
- One accepted event can generate multiple anomaly records.
- Anomalies follow the specified order.
- A valid machine without accepted events still appears in the summary.
- Decimal formatting is correct.
- Output rows appear in the required order.
- Summary counts are consistent with detailed output files.

Students may use AI tools to suggest additional tests, but the correctness of AI-generated test data and expected results must be independently reviewed.

---

# 29. Test-Case Analysis Table

Complete the following table:

| Test Case | Conditions Identified | Initial Status | First Mismatch | Correction Made | Regression Tests Performed | Final Status |
|---:|---|---|---|---|---|---|
| 1 |  | Pass/Fail |  |  |  | Pass/Fail |
| 2 |  | Pass/Fail |  |  |  | Pass/Fail |
| 3 |  | Pass/Fail |  |  |  | Pass/Fail |
| 4 |  | Pass/Fail |  |  |  | Pass/Fail |
| 5 |  | Pass/Fail |  |  |  | Pass/Fail |
| 6 |  | Pass/Fail |  |  |  | Pass/Fail |

If a test passes during the first execution, enter `Not Applicable` in the mismatch and correction columns.

---

# 30. Output Consistency Requirements

The generated outputs must satisfy:

```text
Valid unique machines + Rejected machine records
=
Total machine records
```

```text
Accepted event records + Rejected event records
=
Total event records
```

```text
Accepted event records
=
Sum of accepted_event_count in machine_summary.csv
```

```text
Total anomaly records
=
Number of data rows in anomalies.csv
```

```text
Every rejected input record must appear exactly once
in rejected_records.csv
```

```text
No rejected event may contribute to
machine_summary.csv or anomalies.csv
```

```text
No duplicate Event ID may be accepted
```

```text
No event belonging to an invalid, duplicate,
or unknown machine may be accepted
```

---

# 31. Required Deliverables

Submit:

1. Complete source code.
2. Generated `machine_summary.csv`.
3. Generated `anomalies.csv`.
4. Generated `rejected_records.csv`.
5. Captured console processing summary.
6. Completed test-case analysis table.

---

# 32. Important Notes

- The solution may be implemented using C, C++, or Python.
- Input data and expected outputs must not be hard-coded.
- The complete program logic must not be placed inside one function.
- The mandatory logical interfaces must be implemented with equivalent behaviour.
- Additional helper functions, methods, classes, or modules may be created.
- Appropriate structures, classes, records, dictionaries, collections, and algorithms must be selected by the candidate.
- Operating anomalies do not automatically make an event invalid.
- Rejected records must not affect statistics or anomalies.
- The original input-file order must be preserved in applicable outputs.
- A solution that works only for the sample data will not be considered complete.
- The evaluator may ask the candidate to explain or modify part of the solution.
