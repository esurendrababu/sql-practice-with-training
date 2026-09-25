# Phase 0 — Database Fundamentals

Before writing SQL queries, we need to understand **what a database is and how data is organized inside it**.

---

# 1. Definition

## What is a Database?

A **database** is an organized collection of data that allows us to store, manage, search, and retrieve information easily.

### Simple Example

Imagine a college needs to store student information.

Instead of maintaining hundreds of Excel files or paper records, we can store the information in a database.

For example:

```text
Student Database
│
├── Students
├── Courses
├── Teachers
└── Departments
```

The `Students` table might contain:

| student_id | student_name | age | course |
| ---------: | ------------ | --: | ------ |
|        101 | Ravi         |  20 | B.Tech |
|        102 | Sita         |  21 | B.Tech |
|        103 | Arun         |  20 | MCA    |

So, a database helps us keep related information **organized and accessible**.

---

# 2. Why Do We Need a Database?

Without a proper database, managing large amounts of data becomes difficult.

For example, imagine a company with:

```text
50,000 employees
100,000 customers
1,000,000 orders
```

Searching and maintaining this information manually would be difficult.

A database helps us:

* Store large amounts of data
* Search data quickly
* Update information
* Delete information
* Maintain relationships between data
* Reduce duplicate data
* Control access to data
* Keep data organized

---

# 3. What is a DBMS?

## Definition

**DBMS** stands for **Database Management System**.

A DBMS is software used to **create, store, manage, and access databases**.

Examples:

```text
MySQL
PostgreSQL
Oracle Database
Microsoft SQL Server
SQLite
```

Think of it like this:

```text
Database
   ↑
Managed by
   ↑
DBMS
```

For example:

```text
MySQL
   ↓
Manages
   ↓
Company Database
```

---

# 4. DBMS vs File System

Before databases became widely used, organizations often stored information in files.

For example:

```text
employees.xlsx
customers.xlsx
orders.xlsx
```

This works for small amounts of data, but becomes difficult as the organization grows.

### File System

```text
Files
 ↓
Manual organization
 ↓
Difficult relationships
 ↓
Duplicate data
 ↓
Difficult large-scale management
```

### DBMS

```text
Database
 ↓
Structured data
 ↓
Relationships
 ↓
Better data management
 ↓
Controlled access
```

### Simple Comparison

| File System                    | DBMS                            |
| ------------------------------ | ------------------------------- |
| Data stored in files           | Data stored in databases        |
| Difficult to manage large data | Designed for large data         |
| Relationships are difficult    | Relationships can be defined    |
| More duplication can occur     | Reduces unnecessary duplication |
| Limited querying               | Powerful querying               |
| Security can be limited        | Access control is available     |

---

# 5. Database vs Table

This is one of the most important concepts for beginners.

## Database

A **database** is a collection of related tables and other database objects.

For example:

```text
College Database
│
├── students
├── courses
├── teachers
└── departments
```

## Table

A **table** stores data in rows and columns.

For example:

```text
students
```

| student_id | student_name | age |
| ---------: | ------------ | --: |
|        101 | Ravi         |  20 |
|        102 | Sita         |  21 |
|        103 | Arun         |  20 |

So:

```text
Database
   ↓
Contains tables
   ↓
Tables contain data
```

---

# 6. What is a Row / Record?

A **row** represents one complete record in a table.

Example:

| student_id | student_name | age |
| ---------: | ------------ | --: |
|        101 | Ravi         |  20 |
|        102 | Sita         |  21 |

The first row:

```text
101 | Ravi | 20
```

is one record.

It represents one student.

### Easy way to remember

> **Row = One record**

For example:

```text
One student → One row
One employee → One row
One customer → One row
One order → One row
```

---

# 7. What is a Column / Attribute?

A **column** represents a particular piece of information about the data.

Example:

| student_id | student_name | age |
| ---------: | ------------ | --: |
|        101 | Ravi         |  20 |
|        102 | Sita         |  21 |

Here:

```text
student_id
student_name
age
```

are columns.

Each column describes one attribute of a student.

### Easy way to remember

> **Column = Type of information**

For example:

```text
employee_id
employee_name
salary
department
```

---

# 8. Row vs Column

Students often confuse these two.

Consider:

| student_id | student_name | age |
| ---------: | ------------ | --: |
|        101 | Ravi         |  20 |
|        102 | Sita         |  21 |

### Row

```text
101 | Ravi | 20
```

Represents:

> One student

### Column

```text
student_name
```

Represents:

> Student name information

### Remember

```text
ROW
↓
One record

COLUMN
↓
One type of information
```

---

# 9. What is a Primary Key?

## Definition

A **Primary Key** is a column, or combination of columns, that uniquely identifies each row in a table.

Example:

| student_id | student_name | age |
| ---------: | ------------ | --: |
|        101 | Ravi         |  20 |
|        102 | Sita         |  21 |
|        103 | Arun         |  20 |

Here:

```text
student_id
```

can be the Primary Key.

Why?

Because every student has a unique `student_id`.

```text
101 → Ravi
102 → Sita
103 → Arun
```

No two students should have the same ID.

---

# 10. Primary Key Rules

A primary key:

* Must uniquely identify each record
* Cannot contain `NULL`
* Cannot contain duplicate values
* Can be used to identify a specific row

Example:

```text
student_id
```

is a good primary key.

But:

```text
student_name
```

may not be a good primary key because two students can have the same name.

For example:

```text
101 | Ravi
102 | Ravi
```

Names are not necessarily unique.

---

# 11. Primary Key Example

Later, when we start writing SQL, we can define a primary key like this:

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(100),
    age INT
);
```

The important part for now is:

```sql
student_id INT PRIMARY KEY
```

This tells the database:

> `student_id` uniquely identifies each student.

---

# 12. What is a Foreign Key?

## Definition

A **Foreign Key** is a column that is used to create a relationship between two tables.

Consider:

### departments

| department_id | department_name |
| ------------: | --------------- |
|            10 | IT              |
|            20 | HR              |
|            30 | Finance         |

### employees

| employee_id | employee_name | department_id |
| ----------: | ------------- | ------------: |
|         101 | Ravi          |            10 |
|         102 | Sita          |            20 |
|         103 | Arun          |            10 |

Here:

```text
departments.department_id
```

is the Primary Key.

And:

```text
employees.department_id
```

is the Foreign Key.

The relationship is:

```text
departments
    │
    │ department_id
    ↓
employees
```

This allows us to know which department an employee belongs to.

---

# 13. Primary Key vs Foreign Key

This is important.

| Primary Key                      | Foreign Key                         |
| -------------------------------- | ----------------------------------- |
| Uniquely identifies a row        | Creates a relationship              |
| Usually belongs to its own table | Refers to another table             |
| Cannot be NULL                   | Can be NULL depending on the design |
| Cannot contain duplicates        | Can contain duplicate values        |

Example:

```text
departments
----------------
department_id ← Primary Key


employees
----------------
department_id ← Foreign Key
```

---

# 14. What is NULL?

`NULL` means:

> **No value / unknown / not available**

It does **not** mean:

```text
0
```

It does **not** mean:

```text
empty string ''
```

It means there is no value stored for that field.

Example:

| employee_id | employee_name | manager_id |
| ----------: | ------------- | ---------: |
|         101 | Ravi          |       NULL |
|         102 | Sita          |        101 |

Here:

```text
Ravi → manager_id = NULL
```

This could mean Ravi currently has no manager recorded.

---

# 15. NULL vs 0 vs Empty String

These are different.

```text
NULL
→ No value

0
→ Numeric value zero

''
→ Empty text
```

Example:

```text
salary = 0
```

means the salary value is zero.

But:

```text
salary = NULL
```

means the salary is unknown/not available.

---

# 16. What is a Relationship Between Tables?

A relationship defines how data in one table is connected to data in another table.

Example:

```text
departments
     │
     │ department_id
     ↓
employees
```

A department can have multiple employees.

For example:

```text
IT
│
├── Ravi
├── Arun
└── Kiran
```

This is a relationship between:

```text
Department
      ↓
Employees
```

---

# 17. Types of Relationships

The common relationships are:

```text
1. One-to-One
2. One-to-Many
3. Many-to-Many
```

---

## One-to-One

One record in Table A is related to one record in Table B.

Example:

```text
Person
  ↓
Passport
```

One person has one passport.

---

## One-to-Many

One record in Table A can be related to many records in Table B.

Example:

```text
Department
     ↓
Employees
```

One department can have many employees.

```text
IT
├── Ravi
├── Arun
└── Kiran
```

This is one of the most common relationships.

---

## Many-to-Many

Many records in Table A can be related to many records in Table B.

Example:

```text
Students
    ↕
Courses
```

One student can take multiple courses.

One course can have multiple students.

Usually, a third table is used to manage this relationship:

```text
students
    ↓
enrollments
    ↓
courses
```

---

# 18. Basic Relational Model

A relational database stores data in **tables** and connects related tables using keys.

Example:

```text
                College Database
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
      Students      Courses     Departments
          │
          ↓
      Enrollments
```

Tables contain:

```text
Rows
 +
Columns
```

Relationships are created using:

```text
Primary Keys
      +
Foreign Keys
```

---

# 19. Simple Real-World Example

Imagine an online shopping application.

We may have:

```text
customers
products
orders
```

### Customers

| customer_id | customer_name |
| ----------: | ------------- |
|           1 | Ravi          |
|           2 | Sita          |

### Products

| product_id | product_name | price |
| ---------: | ------------ | ----: |
|        101 | Laptop       | 60000 |
|        102 | Mouse        |  1000 |

### Orders

| order_id | customer_id | product_id |
| -------: | ----------: | ---------: |
|     5001 |           1 |        101 |
|     5002 |           2 |        102 |

Relationships:

```text
customers
    ↓
customer_id
    ↓
orders
    ↓
product_id
    ↓
products
```

Later, SQL JOINs will allow us to combine this information.

---

# 20. Best Practices

Even at the fundamentals stage, students should develop good habits.

### Use meaningful table names

Good:

```text
employees
departments
customers
orders
```

Avoid unclear names such as:

```text
t1
data1
abc
```

### Use meaningful column names

Good:

```text
employee_id
employee_name
department_id
```

Instead of:

```text
id1
name1
dpt
```

### Identify the Primary Key

Every important table should have a clear way to identify its records.

### Understand relationships

Before writing queries, ask:

> How are these tables connected?

---

# 21. Common Errors / Misunderstandings

### 1. Thinking a database and table are the same

Incorrect:

```text
Database = Table
```

Correct:

```text
Database
   ↓
Contains tables
```

---

### 2. Thinking a row and column are the same

Remember:

```text
Row
→ Record

Column
→ Attribute
```

---

### 3. Thinking NULL means zero

Incorrect:

```text
NULL = 0
```

Correct:

```text
NULL
→ No value / unknown
```

---

### 4. Using a non-unique column as a Primary Key

For example:

```text
employee_name
```

may not be unique.

Two employees can have the same name.

An employee ID is usually more suitable:

```text
employee_id
```

---

### 5. Confusing Primary Key and Foreign Key

Remember:

```text
Primary Key
→ Identifies a record

Foreign Key
→ Connects tables
```

---

# 22. Interview Questions

### Beginner

1. What is a database?
2. Why do we need a database?
3. What is DBMS?
4. Give examples of DBMS.
5. What is the difference between a file system and DBMS?
6. What is a table?
7. What is a row?
8. What is a column?
9. What is a record?
10. What is an attribute?

### Keys

11. What is a Primary Key?
12. What are the properties of a Primary Key?
13. What is a Foreign Key?
14. What is the difference between Primary Key and Foreign Key?
15. Can a Foreign Key contain duplicate values?

### Relationships

16. What is a relationship between tables?
17. What is a one-to-one relationship?
18. What is a one-to-many relationship?
19. What is a many-to-many relationship?
20. Why do we need Foreign Keys?

### NULL

21. What is NULL?
22. Is NULL equal to zero?
23. Is NULL equal to an empty string?
24. Why can a column contain NULL?

---

# 23. Exercises

## Exercise 1 — Identify Database Objects

Consider:

```text
College Database
```

with:

```text
students
teachers
courses
departments
```

Identify:

1. Database
2. Tables
3. Possible rows
4. Possible columns

---

## Exercise 2 — Identify Rows and Columns

Consider:

| employee_id | employee_name | department | salary |
| ----------: | ------------- | ---------- | -----: |
|         101 | Ravi          | IT         |  45000 |
|         102 | Sita          | HR         |  50000 |
|         103 | Arun          | IT         |  55000 |

Answer:

1. How many rows?
2. How many columns?
3. What is one record?
4. What is the `salary` column?
5. Which column could be the Primary Key?

---

## Exercise 3 — Identify the Keys

Consider:

### departments

| department_id | department_name |
| ------------: | --------------- |
|            10 | IT              |
|            20 | HR              |

### employees

| employee_id | employee_name | department_id |
| ----------: | ------------- | ------------: |
|         101 | Ravi          |            10 |
|         102 | Sita          |            20 |

Identify:

1. Primary Key in `departments`
2. Primary Key in `employees`
3. Foreign Key in `employees`
4. Relationship between the two tables

---

## Exercise 4 — Identify the Relationship

Identify the relationship:

### A

```text
Department → Employees
```

### B

```text
Person → Passport
```

### C

```text
Students ↔ Courses
```

Choose:

```text
One-to-One
One-to-Many
Many-to-Many
```

---

## Exercise 5 — NULL

Consider:

| employee_id | employee_name | manager_id |
| ----------: | ------------- | ---------: |
|         101 | Ravi          |       NULL |
|         102 | Sita          |        101 |
|         103 | Arun          |        101 |

Answer:

1. Which employee has a NULL `manager_id`?
2. Does NULL mean zero?
3. Does NULL mean an empty string?
4. What could NULL represent in this example?

---

# 24. Real Project Example

## Project: Employee Management System

Imagine we are building an Employee Management System.

We need to store:

```text
Employee information
Department information
```

So we create two tables:

```text
departments
        │
        │ department_id
        ↓
employees
```

### Department Table

```text
departments

department_id
department_name
```

Example:

| department_id | department_name |
| ------------: | --------------- |
|            10 | IT              |
|            20 | HR              |
|            30 | Finance         |

### Employee Table

```text
employees

employee_id
employee_name
department_id
salary
```

Example:

| employee_id | employee_name | department_id | salary |
| ----------: | ------------- | ------------: | -----: |
|         101 | Ravi          |            10 |  45000 |
|         102 | Sita          |            20 |  50000 |
|         103 | Arun          |            10 |  55000 |

Here:

```text
departments.department_id
        ↓
Primary Key

employees.department_id
        ↓
Foreign Key
```

The relationship is:

```text
Department
    │
    │ One
    ↓
Employees
    │
    │ Many
    ↓
Many employees can belong to one department
```

Later in the course, we will use SQL `JOIN` to combine these tables and answer questions such as:

```text
Which department does Ravi work in?

How many employees are in IT?

What is the average salary of each department?
```

---

# 25. Phase 0 — Quick Revision

```text
Database
→ Collection of organized data

DBMS
→ Software used to manage databases

Table
→ Stores data in rows and columns

Row / Record
→ One complete record

Column / Attribute
→ One type of information

Primary Key
→ Uniquely identifies a record

Foreign Key
→ Connects related tables

NULL
→ No value / unknown value

Relationship
→ Connection between tables
```

### The complete picture

```text
                    DATABASE
                       │
              ┌────────┼────────┐
              ↓        ↓        ↓
           Table     Table     Table
              │        │        │
              ↓        ↓        ↓
            Rows     Rows     Rows
              │
           Columns
              │
        ┌─────┴─────┐
        ↓           ↓
   Primary Key   Foreign Key
                    │
                    ↓
              Relationships
```

> **Before learning SQL commands, understand how data is organized. Once students understand databases, tables, rows, columns, keys, NULL, and relationships, SQL becomes much easier to learn.**
