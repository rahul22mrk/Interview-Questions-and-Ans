# SQL Interview Answers

> This document contains answers only for the SQL questions that were actually asked in my interviews.

**Companies**

- CELESTIAL SYSTEMS PRIVATE LIMITED

---

# Q1. What is the difference between Primary Key and Unique Key?

## Answer

Both **Primary Key** and **Unique Key** are used to maintain uniqueness in a table, but they have some important differences.

| Primary Key | Unique Key |
|-------------|------------|
| Uniquely identifies each row | Ensures unique values |
| Cannot contain NULL | Can contain NULL (DB dependent) |
| Only one Primary Key per table | Multiple Unique Keys allowed |
| Automatically creates a Clustered Index (MySQL/InnoDB uses PK for clustering) | Creates a Unique Index |
| Used as the main identifier | Used for alternate unique columns |

---

## Example

```sql
CREATE TABLE Employee (

    id INT PRIMARY KEY,

    email VARCHAR(100) UNIQUE,

    phone VARCHAR(20) UNIQUE

);
```

Here

- `id` → Primary Key
- `email` → Unique Key
- `phone` → Unique Key

---

## Real-world Example

Employee Table

| ID | Email | Phone |
|----|--------|-------|
|101|rahul@gmail.com|9999999999|

- Employee ID → Primary Key
- Email → Unique Key
- Phone → Unique Key

---

## Interview Tip

Remember

```
Primary Key

↓

Identity
```

```
Unique Key

↓

Uniqueness
```

---

## Quick Revision

- One Primary Key
- Multiple Unique Keys
- Primary Key → No NULL
- Unique Key → NULL allowed (depends on DB)

---

## Possible Follow-up Questions

- Can Primary Key contain NULL?
- Can a table have multiple Primary Keys?
- Can Primary Key be composite?

---

# Q2. What is Indexing in a Database?

## Answer

An Index is a database object used to improve the speed of data retrieval.

Without an index, the database performs a **Full Table Scan**, checking every row.

With an index, the database can directly locate the required rows.

---

## Example

Without Index

```
Employee Table

1000000 Records

↓

Search Email

↓

Check Every Row

↓

Slow
```

---

With Index

```
Employee Table

↓

Index

↓

Direct Lookup

↓

Fast
```

---

## SQL Example

```sql
CREATE INDEX idx_email
ON Employee(email);
```

---

## Why Use Indexes?

- Faster SELECT queries
- Faster WHERE clause
- Faster JOIN
- Faster ORDER BY
- Faster GROUP BY

---

## Disadvantages

- Extra Storage
- INSERT becomes slower
- UPDATE becomes slower
- DELETE becomes slower

Because indexes also need to be updated.

---

## Interview Tip

Indexes improve **READ** performance but slightly reduce **WRITE** performance.

---

## Quick Revision

```
Without Index

↓

Full Table Scan
```

```
With Index

↓

Direct Search
```

---

## Possible Follow-up Questions

- What data structure is used internally?

Answer

Mostly **B+ Tree**.

---

# Q3. What are the types of Indexing?

## Answer

Common types of indexes are:

- Primary Index
- Clustered Index
- Non-Clustered Index
- Unique Index
- Composite Index
- Full-Text Index

---

## 1. Clustered Index

Stores table data physically in sorted order.

Only one Clustered Index is allowed.

---

## 2. Non-Clustered Index

Stores index separately from table data.

Contains pointers to actual rows.

Multiple Non-Clustered indexes can exist.

---

## 3. Unique Index

Prevents duplicate values.

---

## 4. Composite Index

Index on multiple columns.

Example

```sql
CREATE INDEX idx_name_city

ON Employee(name, city);
```

---

## 5. Full Text Index

Used for searching large text.

Example

Searching articles or blogs.

---

## Interview Tip

If the interviewer asks only **types of indexes**, mention

- Clustered
- Non-Clustered
- Composite
- Unique

These are sufficient for most backend interviews.

---

## Quick Revision

```
Clustered

↓

Physical Data
```

```
Non-Clustered

↓

Separate Index
```

---

## Possible Follow-up Questions

- Difference between Clustered and Non-Clustered Index?

---

# Q4. A table is taking too much time to fetch data. How would you optimize it?

## Answer

I would troubleshoot step by step instead of directly adding an index.

---

## Step 1

Check the execution plan.

```sql
EXPLAIN
SELECT *
FROM Employee
WHERE email='rahul@gmail.com';
```

---

## Step 2

Check whether indexes exist.

If not,

create an index on frequently searched columns.

Example

```sql
CREATE INDEX idx_email
ON Employee(email);
```

---

## Step 3

Avoid

```sql
SELECT *
```

Instead

```sql
SELECT id,
       name,
       email
FROM Employee;
```

---

## Step 4

Optimize JOINs.

Use indexed columns for joins.

---

## Step 5

Avoid functions in WHERE clause.

Bad

```sql
WHERE LOWER(email)='rahul@gmail.com'
```

Better

```sql
WHERE email='rahul@gmail.com'
```

---

## Step 6

Avoid unnecessary subqueries.

---

## Step 7

Use LIMIT when required.

Example

```sql
SELECT *
FROM Employee
LIMIT 20;
```

---

## Step 8

Archive old data if the table becomes too large.

---

## Interview Tip

Never answer

```
"I'll create an index."
```

First say

```
"I'll analyze the query using EXPLAIN."
```

Then optimize.

---

## Quick Revision

```
EXPLAIN

↓

Index

↓

Avoid SELECT *

↓

Optimize JOIN

↓

LIMIT
```

---

## Possible Follow-up Questions

- What is EXPLAIN?
- Why is SELECT * bad?
- When should indexes not be created?

---

# Q5. How do you find duplicate email addresses in a table?

## Example Table

| id | email |
|----|-------------------|
|1|a@gmail.com|
|2|b@gmail.com|
|3|a@gmail.com|
|4|c@gmail.com|
|5|b@gmail.com|

---

## Query

```sql
SELECT email,
       COUNT(*) AS total

FROM Employee

GROUP BY email

HAVING COUNT(*) > 1;
```

---

## Output

| Email | Total |
|--------|-------|
|a@gmail.com|2|
|b@gmail.com|2|

---

## Interview Tip

Remember

Duplicates

↓

GROUP BY

↓

HAVING COUNT(*) > 1

---

## Quick Revision

```sql
GROUP BY

+

HAVING
```

---

## Possible Follow-up Questions

- Delete duplicate rows?
- Keep only one duplicate?

---

# Q6. What is the difference between IN and EXISTS?

## Answer

Both are used to filter records, but their execution strategy is different.

---

## IN

Compares values with a list.

Example

```sql
SELECT *

FROM Employee

WHERE department_id IN (

SELECT id

FROM Department

);
```

---

## EXISTS

Checks whether at least one matching row exists.

Example

```sql
SELECT *

FROM Employee e

WHERE EXISTS (

SELECT 1

FROM Department d

WHERE d.id=e.department_id

);
```

---

## Difference

| IN | EXISTS |
|----|---------|
| Compares values | Checks existence |
| Suitable for small result sets | Better for large result sets |
| Evaluates entire subquery | Stops after first match |
| May be slower for huge datasets | Generally faster for correlated subqueries |

---

## Real-world Example

Suppose

Employee → 10 million rows

Department → 100 rows

For very large correlated queries,

`EXISTS` is generally preferred because it stops searching once a match is found.

---

## Interview Tip

Simple Rule

```
Small Result Set

↓

IN
```

```
Large Correlated Query

↓

EXISTS
```

---

## Quick Revision

```
IN

↓

Compare Values
```

```
EXISTS

↓

Check Match
```

---

## Common Mistakes

❌ `IN` is always slower than `EXISTS`.

The optimizer may rewrite queries depending on the database engine.

---

## Possible Follow-up Questions

- EXISTS vs JOIN?
- NOT IN vs NOT EXISTS?
- Which is faster in MySQL?

---

# ✅ SQL Questions Covered

- Primary Key vs Unique Key
- What is Indexing?
- Types of Indexing
- How to optimize slow SQL queries
- Find duplicate email addresses
- Difference between IN and EXISTS

---
