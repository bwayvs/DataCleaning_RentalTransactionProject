# README: SQL Rental Transaction and Financial Reporting Query

This document provides an overview of SQL queries I designed for financial reporting, demonstarting a myriad of SQL skills. This README highlights some of the core competencies embedded in the code. To see the entire code, please see the subsequent files.

## Table of Contents

1. [Conditional Aggregation](#conditional-aggregation)
2. [Date Manipulations](#date-manipulations)
3. [String Formatting](#string-formatting)
4. [Joins](#joins)
5. [Case Statements](#case-statements)
6. [Union All](#union-all)

### Conditional Aggregation

The code makes extensive use of conditional aggregation, which allows for specific aggregations based on certain conditions.

**Example:**
```sql
SUM(CASE
     WHEN EXTRACT(MONTH FROM transaction_date) = 1 AND
          EXTRACT(YEAR FROM transaction_date) = 2009 THEN
     CASE
       WHEN cl.common_lookup_type = 'DEBIT'
       THEN t.transaction_amount
       ELSE t.transaction_amount * -1
     END
 END) AS "JANUARY"
```

### Date Manipulations

Manipulating and extracting data based on dates is a frequent requirement in SQL. The code leverages the `EXTRACT` function to pull out specific components of a date.

**Example:**
```sql
EXTRACT(MONTH FROM transaction_date) = 1
```

### String Formatting

Formatting is essential for the presentation of data, especially in financial reports. The query utilizes the `TO_CHAR` and `LPAD` functions to format numbers.

**Example:**
```sql
LPAD(TO_CHAR
    (SUM(...),'99,999.00'),10,' ') AS "FEBRUARY"
```

### Joins

Joining tables is a fundamental SQL skill, allowing for the combination of rows based on related columns between two or more tables. 

**Example:**
```sql
FROM transaction t INNER JOIN common_lookup cl
ON t.transaction_type = cl.common_lookup_id
```

### Case Statements

The code frequently uses `CASE` statements for conditional logic, both within the `SELECT` and `GROUP BY` clauses.

**Example:**
```sql
CASE
  WHEN t.transaction_account = '111-111-111-111' THEN 'Debit'
  WHEN t.transaction_account = '222-222-222-222' THEN 'Credit'
END
```

### Union All

The `UNION ALL` operator is used to combine the result sets of two or more SELECT statements.

**Example:**
```sql
SELECT 'Total' as "TRANSACTION_ACCOUNT", ...
...
UNION ALL
...
```
