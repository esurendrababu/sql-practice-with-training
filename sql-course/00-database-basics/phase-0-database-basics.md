

## 🎯 What will you learn?


* What is a database?
* What is a DBMS?
* DBMS vs File System
* Database vs Table
* What is a Row / Record?
* What is a Column / Attribute?
* What is a Primary Key?
* What is a Foreign Key?
* What is NULL?
* How are tables related?
* What is the basic Relational Model?

---

# 1. What is a Database?


Imagine your college has **5,000 students**.

For every student, the college needs to store information such as:

| Student ID | Name  | Age | Department | Phone      |
| ---------- | ----- | --: | ---------- | ---------- |
| 101        | Ravi  |  20 | CSE        | 9876543210 |
| 102        | Sita  |  21 | ECE        | 9876543211 |
| 103        | Arun  |  20 | CSE        | 9876543212 |
| 104        | Priya |  22 | EEE        | 9876543213 |

Where should this information be stored?

We could store it in:

* Excel
* Text files
* CSV files
* Applications
* Or a **Database**

A **database** is an organized collection of data that allows us to store, manage, retrieve, and update information efficiently.

### Simple definition

> **Database = Organized collection of related data.**

For example:

College Database
│
├── Students
├── Faculty
├── Courses
├── Departments
└── Exams


The important word is **organized**.

A database is not just a collection of random information.

---

# 2. Why Do We Need a Database?

Let's imagine that a college stores all student information in separate Excel files.


Students.xlsx
Faculty.xlsx
Courses.xlsx
Marks.xlsx
Attendance.xlsx


Initially, this may work.

But when the college grows, problems start appearing.

### Problem 1 — Duplicate Data

The same student information may appear in multiple files.


Student ID: 101
Name: Ravi
Department: CSE


This information may appear in:

Students.xlsx
Marks.xlsx
Attendance.xlsx
Fees.xlsx


If Ravi changes his phone number, we may need to update it in multiple places.

---

### Problem 2 — Data Inconsistency

Suppose Ravi's phone number is:


Students.xlsx → 9876543210
Attendance.xlsx → 9876543299


Which one is correct?

Now our data is inconsistent.

---

### Problem 3 — Searching Becomes Difficult

Imagine having:


5,000 students
500 faculty
200 courses


Finding specific information manually becomes difficult.

---

### Problem 4 — Multiple People Need Access

At the same time:


Admin
Faculty
Students
Accounts Department
Exam Department


may need to access the same data.

We need a better system.

That's where a **DBMS** comes in.

---

# 3. What is DBMS?

**DBMS** stands for:

> **Database Management System**

A DBMS is software used to create, store, manage, retrieve, and control data in databases.

Examples:

* MySQL
* PostgreSQL
* Oracle Database
* Microsoft SQL Server
* SQLite

Think about it like this:

```text
              USER
                │
                ↓
               DBMS
                │
                ↓
             DATABASE
```

The user does not directly manage every piece of data manually.

The **DBMS manages the database**.

---

# 4. Database vs DBMS

This is an important distinction.

### Database

The **data itself**.

Example:

```text
Student 101 → Ravi → CSE
Student 102 → Sita → ECE
```

### DBMS

The **software that manages the data**.

Example:

```text
MySQL
PostgreSQL
Oracle
SQL Server
```

### Easy way to remember

> **Database = Data**
>
> **DBMS = Software that manages the data**

---

# 5. DBMS vs File System

Before databases became widely used, organizations commonly stored data in files.

For example:

```text
students.txt
employees.txt
marks.txt
```

This is called a **file-based system**.

A DBMS provides a more structured way to manage related data.

| File System                                     | DBMS                                       |
| ----------------------------------------------- | ------------------------------------------ |
| Data stored in files                            | Data stored and managed in databases       |
| Searching can become difficult                  | Efficient querying                         |
| More data duplication can occur                 | Redundancy can be controlled               |
| Relationships are difficult to manage           | Relationships can be defined               |
| Security is limited                             | User access and permissions can be managed |
| Concurrent access is difficult                  | Multiple users can work with data          |
| Backup/recovery may require separate mechanisms | DBMS provides database recovery mechanisms |

### Simple example

File system:

```text
students.txt
marks.txt
attendance.txt
```

DBMS:

```text
College Database
│
├── Students
├── Marks
└── Attendance
```

The DBMS helps manage the relationships between these pieces of data.

---

# 6. What is a Table?

Now we come to the most important concept for SQL.

A **table** is a structured collection of related data arranged into:

* Rows
* Columns

Example:

### Students

| student_id | name  | age | department |
| ---------: | ----- | --: | ---------- |
|        101 | Ravi  |  20 | CSE        |
|        102 | Sita  |  21 | ECE        |
|        103 | Arun  |  20 | CSE        |
|        104 | Priya |  22 | EEE        |

This is a table.

Think of a table like an Excel sheet.

```text
        Students
┌────────────┬────────┬─────┬────────────┐
│ student_id │ name   │ age │ department │
├────────────┼────────┼─────┼────────────┤
│ 101        │ Ravi   │ 20  │ CSE        │
│ 102        │ Sita   │ 21  │ ECE        │
│ 103        │ Arun   │ 20  │ CSE        │
│ 104        │ Priya  │ 22  │ EEE        │
└────────────┴────────┴─────┴────────────┘
```

---

# 7. Database vs Table

A database can contain **many tables**.

For example:

```text
College Database
│
├── Students
├── Departments
├── Faculty
├── Courses
├── Enrollments
└── Marks
```

So:

> **Database = Collection of related tables and other database objects**

And:

> **Table = Collection of related records**

### Easy analogy

Think of a **college** as a database.

Inside the college, there are different departments.

```text
College
│
├── CSE
├── ECE
├── EEE
└── Mechanical
```

Similarly:

```text
Database
│
├── Students
├── Faculty
├── Courses
└── Departments
```

---

# 8. What is a Row?

A **row** represents one complete record.

Example:

| student_id | name | age | department |
| ---------: | ---- | --: | ---------- |
|        101 | Ravi |  20 | CSE        |

This entire row represents **one student**.

Therefore:

> **Row = Record**

For example:

```text
101 | Ravi | 20 | CSE
```

is one student record.

If we have 1,000 students, the table may contain approximately 1,000 student records.

---

# 9. What is a Column?

A **column** represents one type of information about the records.

Example:

| student_id | name | age | department |
| ---------: | ---- | --: | ---------- |
|        101 | Ravi |  20 | CSE        |
|        102 | Sita |  21 | ECE        |
|        103 | Arun |  20 | CSE        |

Here:

```text
student_id → Student ID information
name       → Student name information
age        → Student age information
department → Department information
```

Therefore:

> **Column = Attribute**

So:

```text
Row    → Record
Column → Attribute
```

These two terms are very important in DBMS.

---

# 10. Row vs Column

Remember this simple rule:

### Row

> **Who / Which record?**

### Column

> **What information about that record?**

Example:

```text
101 | Ravi | 20 | CSE
```

This is a **row/record**.

And:

```text
name
```

is a **column/attribute**.

---

# 11. What is a Primary Key?

Now we have an important problem.

Suppose we have:

| name | age | department |
| ---- | --: | ---------- |
| Ravi |  20 | CSE        |
| Ravi |  21 | ECE        |
| Arun |  20 | CSE        |

Can we identify a student using only the name?

No.

Because two students can have the same name.

We need something that uniquely identifies each student.

That's why we use:

> **Primary Key**

Example:

| student_id | name | age | department |
| ---------: | ---- | --: | ---------- |
|    **101** | Ravi |  20 | CSE        |
|    **102** | Ravi |  21 | ECE        |
|    **103** | Arun |  20 | CSE        |

Here:

```text
student_id
```

can uniquely identify each student.

### Simple definition

> **Primary Key = A column or combination of columns that uniquely identifies each row in a table.**

---

# 12. Primary Key Rules

A primary key should:

### 1. Be unique

```text
101
102
103
```

We should not have:

```text
101
101
```

for two different students.

### 2. Not be NULL

Every record must have a value for its primary key.

### 3. Identify one record

For example:

```text
student_id = 101
```

should identify exactly one student.

---

# 13. Why Not Use Name as Primary Key?

Consider:

```text
Ravi
Ravi
Sita
Arun
```

Names are not necessarily unique.

Instead:

```text
101 → Ravi
102 → Ravi
103 → Sita
104 → Arun
```

Now every student has a unique identifier.

This is why databases commonly use IDs.

Examples:

```text
student_id
employee_id
product_id
order_id
customer_id
```

---

# 14. What is a Foreign Key?

Now let's create another table.

### Departments

| dept_id | dept_name |
| ------: | --------- |
|       1 | CSE       |
|       2 | ECE       |
|       3 | EEE       |

And our Students table:

| student_id | name  | dept_id |
| ---------: | ----- | ------: |
|        101 | Ravi  |       1 |
|        102 | Sita  |       2 |
|        103 | Arun  |       1 |
|        104 | Priya |       3 |

Notice something?

The `dept_id` in the Students table refers to the `dept_id` in the Departments table.

```text
Departments
     │
     │ dept_id
     ↓
Students
```

This is called a **Foreign Key**.

### Simple definition

> **Foreign Key = A column that refers to a key in another table and helps establish a relationship between tables.**

---

# 15. Primary Key vs Foreign Key

| Primary Key                                  | Foreign Key                            |
| -------------------------------------------- | -------------------------------------- |
| Identifies a record                          | Connects records between tables        |
| Must uniquely identify rows                  | Values may repeat                      |
| Cannot be NULL                               | Can be NULL in appropriate designs     |
| Usually one primary key constraint per table | A table can have multiple foreign keys |
| Example: `student_id`                        | Example: `dept_id`                     |

### Easy way to remember

> **Primary Key → Who am I?**

> **Foreign Key → Which other table am I connected to?**

---

# 16. What is a Relationship?

Now we can connect tables.

We have:

### Departments

```text
1 → CSE
2 → ECE
3 → EEE
```

### Students

```text
101 → Ravi → 1
102 → Sita → 2
103 → Arun → 1
104 → Priya → 3
```

We can understand:

```text
Ravi  → CSE
Sita  → ECE
Arun  → CSE
Priya → EEE
```

The relationship is created using:

```text
Departments.dept_id
        ↓
Students.dept_id
```

---

# 17. Why Do We Use Multiple Tables?

Why not store everything in one giant table?

For example:

| student_id | student_name | dept_id | dept_name | faculty | course |
| ---------- | ------------ | ------- | --------- | ------- | ------ |

Imagine thousands of students.

We would repeatedly store:

```text
CSE
Computer Science and Engineering
```

again and again.

This creates unnecessary duplication.

Instead, we separate the information:

```text
Departments
Students
Faculty
Courses
```

and connect them using keys.

This is one of the fundamental ideas behind relational databases.

---

# 18. What is NULL?

NULL is one of the most misunderstood concepts in SQL.

Suppose we have:

| student_id | name | phone      |
| ---------: | ---- | ---------- |
|        101 | Ravi | 9876543210 |
|        102 | Sita | NULL       |

What does NULL mean?

It means:

> **The value is unknown, unavailable, or not provided.**

It does **not** necessarily mean:

```text
0
```

It does **not** mean:

```text
empty string
```

It does **not** mean:

```text
false
```

### Example

If Sita has not provided her phone number:

```text
phone = NULL
```

We don't know the phone number.

---

# 19. NULL vs 0 vs Empty

These are different concepts.

| Value  | Meaning                           |
| ------ | --------------------------------- |
| `NULL` | Unknown / missing / not available |
| `0`    | Numeric value zero                |
| `''`   | Empty string                      |
| `' '`  | Space character                   |

Example:

```text
Age = 0
```

means the value is zero.

But:

```text
Age = NULL
```

means we don't have a value.

---

# 20. Basic Relational Model

Now let's bring everything together.

A relational database organizes data into **relations**, which are commonly represented as tables.

For beginners, think:

```text
Relation ≈ Table
Tuple    ≈ Row
Attribute ≈ Column
```

Example:

### Student Relation

| student_id | name | age | dept_id |
| ---------: | ---- | --: | ------: |
|        101 | Ravi |  20 |       1 |
|        102 | Sita |  21 |       2 |
|        103 | Arun |  20 |       1 |

In relational-model terminology:

```text
Table      → Relation
Row        → Tuple
Column     → Attribute
```

These terms will appear frequently in DBMS examinations.

---

# 21. Putting Everything Together

Let's build a simple mental model.

```text
                    COLLEGE DATABASE
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ↓                ↓                ↓
     DEPARTMENTS       STUDENTS          COURSES
          │                │                │
          │                │                │
          └───────┐        │        ┌───────┘
                  │        │        │
                  └────────┴────────┘
                       RELATIONSHIPS
```

### Departments

```text
dept_id
dept_name
```

### Students

```text
student_id
name
age
dept_id
```

### Courses

```text
course_id
course_name
credits
```

The keys allow us to connect these tables.

---

# 22. The Big Picture

At this point, remember these relationships:

```text
Database
   │
   ├── contains
   ↓
 Tables
   │
   ├── contain
   ↓
 Rows + Columns
   │      │
   │      └── Column = Attribute
   │
   └── Row = Record
```

And:

```text
Primary Key
     │
     └── uniquely identifies a row
```

```text
Foreign Key
     │
     └── connects one table with another
```

And:

```text
NULL
  │
  └── value is unknown / unavailable / not provided
```

---

# 23. One Simple Real-World Example

Imagine an online shopping application.

There are thousands of customers.

### Customers

```text
customer_id
name
email
phone
```

### Products

```text
product_id
product_name
price
```

### Orders

```text
order_id
customer_id
order_date
```

### Order Items

```text
order_id
product_id
quantity
```

Now we have relationships:

```text
CUSTOMER
   │
   │ customer_id
   ↓
ORDER
   │
   │ order_id
   ↓
ORDER_ITEM
   │
   │ product_id
   ↓
PRODUCT
```

This is the type of structure that real applications use.

Later, SQL will allow us to ask questions such as:

```text
Which customers placed orders?

Which products were purchased?

How many products were sold?

What is the total order amount?

Which customer spent the most?

Which products have never been purchased?
```

We will answer these questions using **SQL**.

---

# 24. Quick Revision

Before moving to SQL, you should be able to answer these questions.

### Q1. What is a database?

**Answer:**
An organized collection of related data.

### Q2. What is a DBMS?

**Answer:**
Software used to create, manage, store, retrieve, and control data in databases.

### Q3. Give examples of DBMS.

**Answer:**

```text
MySQL
PostgreSQL
Oracle
SQL Server
SQLite
```

### Q4. What is a table?

**Answer:**
A structured collection of related data organized into rows and columns.

### Q5. What is a row?

**Answer:**
A row represents one record.

### Q6. What is a column?

**Answer:**
A column represents an attribute or type of information.

### Q7. What is a primary key?

**Answer:**
A column or combination of columns that uniquely identifies each row.

### Q8. What is a foreign key?

**Answer:**
A column that references a key in another table and establishes a relationship between tables.

### Q9. What is NULL?

**Answer:**
NULL represents a missing, unknown, or unavailable value.

### Q10. What is the relationship between a database and a table?

**Answer:**
A database can contain multiple related tables.

---

# 25. Before Moving to SQL

Make sure you can understand this diagram:

```text
                         DATABASE
                            │
             ┌──────────────┼──────────────┐
             │              │              │
             ↓              ↓              ↓
        DEPARTMENTS      STUDENTS       COURSES
             │              │              │
             │              │              │
             │        ┌─────┴─────┐        │
             │        │           │        │
             │        ↓           ↓        │
             │    PRIMARY KEY  FOREIGN KEY │
             │        │           │        │
             └────────┴───────────┴────────┘
                       │
                       ↓
                  RELATIONSHIP
```

If this diagram makes sense, you are ready to start SQL.

---

# 🚀 Next Phase

Now we can finally ask:

> **How do we create these tables and work with the data?**

The answer is:

# SQL

In the next phase, we will learn:

```text
CREATE
INSERT
SELECT
UPDATE
DELETE
```

Then we will gradually move to:

```text
WHERE
Functions
GROUP BY
HAVING
JOINS
Subqueries
Views
Set Operations
```

**Don't memorize SQL commands yet.**

First understand the database.

Then SQL becomes much easier.
