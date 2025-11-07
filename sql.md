### **What is Data?**  
Data refers to raw, unorganized facts and figures, such as numbers, text, images, or symbols, that can be processed and analyzed to extract meaningful information  

---

### **What is Database?**  
A collection of related data stored in an organized way so it can be easily accessed, managed, and updated.

---
### What is DataBaseManagementSystem?  
The software that manages database operations like storage, retrieval, and security (e.g., MySQL, Oracle).  
The main types are:  
- Relational DBMS (RDBMS)  
- NoSQL DBMS (Document, Key-Value, Columnar, Graph)  

---
### What is Schema?  
The structural blueprint that defines how data is organized—tables, fields, data types, and relationships.   

---

### What is RDBMS ?    
Relational databases organize data into tables made up of rows (records) and columns (fields). They use schemas (blueprints) to define how data is structured and how different tables relate to each other.  

---
### What is NoSQL ?  
NoSQL stands for "Not Only SQL".  
It refers to a category of database systems that don’t use traditional relational tables (rows and columns) like SQL databases.  

---
### Type of Database?
###### 1) Relational Database (RDBMS)
- Data is stored in **tables (rows & columns)**.
- Uses **SQL** for queries.
- Supports relationships using **primary key / foreign key**.
- ✅ Examples: MySQL, PostgreSQL, Oracle, SQL Server, SQLite
###### 2. **NoSQL Database**
- Designed for **unstructured / semi-structured data**.
- Doesn’t always use SQL.
- Types of NoSQL DBs:
    - **Document-based** → MongoDB, CouchDB
###### 3. **Hierarchical Database**
- Data stored in a **tree-like structure (parent-child)**.
- Each child has only **one parent**.
- ✅ Example: IBM Information Management System (IMS).

---
### SQL 
SQL (Structured Query Language) is a, declarative(you describe what you want to achieve instead of explicitly writing how to do it.) programming language designed for managing relational databases. It is the primary language for tasks like data retrieval, data manipulation, and database administration.

---

### SQL VS NOSQL
**SQL** databases are relational and use tables with fixed schemas. They are great when your data is structured and relationships are important, like student records or bank transactions.
Each row in a table must follow the same schema.
Example: If the table Students(id, name, marks) is defined,
every row must have these three columns.
You cannot suddenly add a "hobbies" column for just one row.

**NoSQL** databases are non-relational and schema-less, meaning they can handle unstructured or semi-structured data. They’re useful when you need scalability and flexibility, like storing user profiles.
Each document can have a different structure (schema is flexible).
You can store extra fields for some records without affecting others.
➡️ First student has 3 fields, second student has 4 fields.
➡️ This is allowed in NoSQL but not in SQL.

---

### Database keys:
Keys are attributes (or sets of attributes) that ensure **data integrity, uniqueness, and relationships** in a database.  
They help **identify and access records efficiently**.

---

## Common Types of Keys

##### 1. **Primary Key**
- Uniquely identifies each record in a table.
- Cannot have `NULL` or duplicate values.
- Only **one primary key per table**.
-  Example: `StudentID` in a Students table.
##### 2. **Foreign Key**
- A column that **links two tables**.  
- Foreign Key always references a **candidate key** (usually Primary Key or Unique Key) in another table..
- Ensures **referential integrity**.  
-  Example: `CourseID` in `Enrollments` referencing `Courses.CourseID`.
##### 3. **Candidate Key**
- Attributes that can uniquely identify records.
- A **table can have multiple candidate keys**.
- Cannot have `NULL` or duplicates.
- One candidate key is chosen as the **primary key**.
##### 4. **Unique Key**
- Ensures column values are unique.  
- Unlike primary key, a table can have **multiple unique keys**.  
- **NULL is allowed** (but only one NULL per column).  
##### 5. **Super Key**
- Any set of attributes that uniquely identify records.  
- **Includes candidate keys plus extra attributes**.  
- Every candidate key is a super key, but not every super key is minimal.
##### 6. **Alternate Key**
- Candidate keys **not chosen** as the primary key.  
- Still unique and can serve as identifiers.

---
## Types of Constraints
##### 1. **NOT NULL**
- Ensures a column **cannot store NULL values**.  
- Every row must have a value for this column.
##### 2. **UNIQUE**
##### 3. PRIMARY KEY
##### 4. FOREIGN KEY
##### 5. **CHECK**
- Ensures values in a column meet a specific **condition**.
```sql
CREATE TABLE Employees (     Age INT CHECK (Age >= 18) );
```
##### 6. **DEFAULT**
- Assigns a **default value** if none is provided.
```sql
CREATE TABLE Employees (     Country VARCHAR(50) DEFAULT 'India' );
```

---
##### View all the databases:
```sql
SHOW databse;
```
##### Create database:

```sql
CREATE database user;
```

##### Use the current dabase:

```sql
USE user;
```
###### See the tables present in the database:

```sql
SHOW tables;
```
###### DROP DATABASE:
```sql
Drop database user;
```
---

#### SQL Commands
### DDL - Data Definition Language
Data Definition Language (DDL) commands allow us to define and manage a schema in SQL. In a nutshell, a schema in SQL is a blueprint that defines how data is organized in a database.
All commands of DDL are auto committed that means it permanently save changes in database. 
1.) **Create** :  create a new table
```sql
CREATE TABLE <table_name> (
    <column_name> data_type constraints,
)
```
```sql
CREATE TABLE IF NOT EXIST <table_name> (
    <column_name> data_type constraints,
)
```
2.) **Alter Table** : An `ALTER` statement is a `DDL` T-SQL that modifies a table definition.
- **Add a new column**
```sql
ALTER TABLE table_name
ADD column_name datatype;
```
- **Add multiple columns**
```sql
ALTER TABLE table_name
ADD (
    column1 datatype,
    column2 datatype
);
```
- **Add a primary key constraint**
```sql
ALTER TABLE table_name
ADD CONSTRAINT pk_name PRIMARY KEY (column_name);
```
- **Add a foreign key constraint**
```sql
ALTER TABLE table_name
ADD CONSTRAINT fk_name FOREIGN KEY (column_name)
REFERENCES other_table(other_column);
```
- **Add a unique constraint**
```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name UNIQUE (column_name);
```
- **Add a default constraint**
```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name DEFAULT default_value FOR column_name;
```

**3.) DROP**
- **Drop a Column**
```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```
- **Drop a Constraint**
```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```
- **Drop Database**
```sql
Drop database db_name
```
- **Drop Table**: delete the entire table, including its structure and data
```sql
Drop table table_name
```
ALTER → MODIFY (or ALTER COLUMN)
Used to **change datatype, size, or NULL/NOT NULL property** of a column.
- **Change Data Type**
```sql
ALTER TABLE table_name
MODIFY column_name new_datatype;
```
- **Add NOT NULL**
```sql
ALTER TABLE Employees
MODIFY Salary DECIMAL(10,2) NOT NULL;
```
Constraints cannot be Modified, they need to be deleted and added again in the correct format

ALTER → RENAME
- **Rename Table**
```sql
ALTER TABLE old_table_name
RENAME TO new_table_name;
```
- **Rename Column**
```sql
ALTER TABLE table_name
RENAME COLUMN old_name TO new_name
```
---
### Truncate 
Remove all the row from the table but table structure still exist 
```sql
TRUNCATE table Table_name
```
---
### DATA MANIPULATION LANGUAGE
It includes the SQL commands that can be used to _**manage data stored in the database.**_ This includes inserting, updating, and deleting data. Examples of DML statements include **SELECT, INSERT, UPDATE, DELETE**
-  **INSERT:** Used to add new rows (records) to a table.
```sql
for single value 

INSERT Into table_name (col_name1,col_name2....) values (val1, val2 ...)

for multiple value 
INSERT INTO table_name (col1, col2)
VALUES 
(val1, val2),
(val3, val4);

```
- **UPDATE** :  is a DML command in SQL used to update existing records in the table. We need to specify which records we want to update using the WHERE condition.

```sql : update one col
UPDATE table_name
SET column1 = value1
WHERE condition;

#update multiple col
UPDATE Employees
SET Department = 'IT', Salary = 70000
WHERE Name = 'Fatima';

```
- **Delete** 
Used to **remove records** from a table.
```sql
DELETE FROM table_name
WHERE condition;

#removing multiple record
DELETE FROM dependents WHERE dependent_id IN (1, 2, 3);
```
Delete all records (but keep table structure)
```sql
DELETE FROM table_name;
```

---
### DATA QUERY LANGUAGE 

DQL is focused on querying and retrieving data from tables. The primary command is SELECT.
- **SELECT**: statement allows you to retrieve data from one or more tables.
```sql
SELECT
  select_list
FROM
  table_name;

select all columns data 

SELECT * FROM table_name;
```
-  FROM: Specifies the table(s) from which to retrieve data.
- WHERE: Filters the rows based on specified conditions.

**Comparison operators** 

| Operator | Meaning               |
| -------- | --------------------- |
| =        | Equal to              |
| <> (!=)  | Not equal to          |
| <        | Less than             |
| >        | Greater than          |
| <=       | Less than or equal    |
| >=       | Greater than or equal |

**Logical Operator** : use with where to filter rows

|**Operator**|**Meaning**|
|---|---|
|[ALL](https://www.sqltutorial.org/sql-all/)|Return true if all comparisons are true|
|[AND](https://www.sqltutorial.org/sql-and/)|Return true if both expressions are true|
|[ANY](https://www.sqltutorial.org/sql-any/)|Return true if any one of the comparisons is true.|
|[BETWEEN](https://www.sqltutorial.org/sql-between/)|Return true if the operand is within a range|
|[EXISTS](https://www.sqltutorial.org/sql-exists/)|Return true if a subquery contains any rows|
|[IN](https://www.sqltutorial.org/sql-in/)|Return true if the operand is equal to one of the value in a list|
|[LIKE](https://www.sqltutorial.org/sql-like/)|Return true if the operand matches a pattern|
|[NOT](https://www.sqltutorial.org/sql-not/)|Reverse the result of any other Boolean operator.|
|[OR](https://www.sqltutorial.org/sql-or/)|Return true if either expression is true|
|[SOME](https://www.sqltutorial.org/sql-any/)|Return true if some of the expressions are true|

##### Auto Increment
When designing a table, we often use the surrogate [primary key](https://www.sqltutorial.org/sql-primary-key/) whose values are sequential integers generated automatically by the database system.
For example, if the value of the first row is 1, then the value of the second row is 2, and so on.

```sql
CREATE TABLE leave_requests (
    request_id INT AUTO_INCREMENT,
    employee_id INT NOT NULL,
);
```
**Alias**: aliases that give columns temporary names during the execution of the query.
When designing database tables, you may use abbreviations for the column names to keep them short. For example:
- The `so_no` stands for sales order number.
- The `qty` stands for quantity.
```sql
column_name AS alias_name
```
**Aliases for expressions**
```sql
SELECT
  first_name,
  last_name,
  salary * 1.1 AS new_salary
FROM
  employees;
```

**SOME COMMON MISTAKE**
```sql
SELECT
  first_name,
  last_name,
  salary * 1.1 AS new_salary
FROM
  employees
WHERE
  new_salary > 5000

#Unknown column 'new_salary' in 'where clause'
because order of evaluation is 
FROM > WHERE > GROUP BY > HAVING > SELECT DISTINCT > ORDER BY >  TOP: at the time it evaluates the `WHERE` clause, the database doesn’t have the information of the `new_salary` column alias. So it issued an error.
-----------------------------------------------------------------

SELECT
  first_name,
  last_name,
  salary * 1.1 AS new_salary
FROM
  employees
ORDER BY
  new_salary;

WORKS : FROM > SELECT > ORDER BY
```
**Table Alias**
```sql
SELECT
  e.first_name,
  e.last_name
FROM
  employees AS e;
```

**BETWEEN**: operator checks if a value is within a range of values.
```sql
Where salary BETWEEN 2500 AND 2900 ORDER BY

------------------------------------------
WHERE salary NOT BETWEEN 2500 AND 2900
```
**IN**
```sql
SELECT
  first_name,
  last_name,
  job_id
FROM
  employees
WHERE
  job_id IN (8, 9, 10)
ORDER BY
  job_id;
```

#### LIKE 
The `LIKE` operator returns `true` if a value matches a pattern or `false` otherwise.
SQL provides you with two wildcard characters to construct a pattern:

-  `%` percent wildcard matches zero, one, or more characters
-  `_` underscore wildcard matches a single character.

```sql
where colname LIKE pattern

where colname NOT LIKE pattern
```

|Expression|Meaning|
|---|---|
|LIKE `'Kim%'`|match a string that starts with `Kim`|
|LIKE `'%er'`|match a string that ends with `er`|
|LIKE `'%ch%'`|match a string that contains `ch`|
|LIKE `'Le_'`|match a string that starts with `Le` and is followed by one character e.g., `Les`, `Len`…|
|LIKE `'_uy'`|match a string that ends with `uy` and is preceded by one character e.g., `guy`|
|LIKE `'%are_'`|match a string that includes the string `are` and ends with one character.|
|LIKE `'_are%'`|match a string that includes the string `are`, starts with one character and ends with any number of characters.|
---
#### IS NULL 
To test if a value is `NULL` or not, you use the `IS NULL` operator:
```sql
expression IS NULL

expression IS NOT NULL
```
---
#### LIMITING ROWS
- **Distinct** 
		To select the distinct values from a column of a table
```sql
	SELECT DISTINCT
	  column1
	FROM
	  table_name;
```
- **Limit**
		To limit the number of rows returned by a [SELECT](https://www.sqltutorial.org/sql-select/) statement
	```sql
	SELECT
	  column_list
	FROM
	  table1
	LIMIT
	  row_count
	OFFSET
	  row_to_skip;
```
 The `LIMIT row_count` determines the number of rows (`row_count`) returned by the query.
 The `OFFSET row_to_skip` clause skips the `` `row_to_skip` `` rows before beginning to return the rows.
```
 
- **FETCH**
	`OFFSET FETCH` clause which has a similar function to the `LIMIT` clause. The `OFFSET FETCH` clause allows you to skip the first `N` rows in a result set before starting to return rows.
	
E.g Fetching first five row
```sql
SELECT
  first_name,
  salary
FROM
  employees
FETCH FIRST 5 ROWS ONLY;
```
---
### ORDER BY
The `ORDER BY` clause allows you to sort the result set by one or more sort expressions in ascending and/or descending order.
```sql
SELECT
  select_list
FROM
  table_name
ORDER BY
  sort_expression [ASC | DESC];
```
The `ORDER BY` clause allows you to sort the rows in the result set by multiple expressions. In this case, you need to use a comma-separated list of sort expressions in the `ORDER BY` clause:

```sql
SELECT
  select_list
FROM
  table_name
ORDER BY
  sort_expression_1 [ASC | DESC],
  sort_expression_2 [ASC | DESC];
```
---
### Sorting NULLs
In SQL, `NULL` is a marker that indicates missing data or unknown value. `NULL` is special because you cannot compare it with any value.
If you want to sort rows by a column that has `NULL`, you can have an option to place `NULL`s before or after other regular values.
```sql
ORDER BY sort_expression NULLS FIRST
ORDER BY sort_expression NULLS LAST
```

---

#### GROUP BY
The `GROUP BY` clause allows you to group rows based on values of one or more columns. It returns one row for each group.
```sql
SELECT
  column1,
  column2,
  column4, X not allowed as col4 is neither in group by nor in aggregate
  aggregate_function (column3)
FROM
  table_name
GROUP BY
  column1,
  column2;
```
In the SELECT clause, you can only use:  
- Columns that appear in the GROUP BY list  
- Aggregate functions (like COUNT(), SUM(), AVG(), MAX(), MIN() etc.)  
you often use the `GROUP BY` clause with an aggregate function such as MIN, MAX, AVG, SUM or COUNT to calculate a measure that provides the information for each group.

---  

#### AGGREGATE FUNTIONS

- **AVG**  - calculates the average value of a set.
```sql
AVG([ALL|DISTINCT] expression)
```
```sql
SELECT
  AVG(salary) average_salary
FROM
  employees;
-----
average_salary 
---------------- 
7845.45

------------------------------------
SELECT
  ROUND(AVG(DISTINCT salary), 2) average_salary
FROM
  employees;
```
AVG function with GROUP BY clause
```sql
SELECT
  department_id,
  ROUND(AVG(salary), 2) average_salary
FROM
  employees
GROUP BY
  department_id
ORDER BY
  average_salary;
```
- **COUNT** - returns the number of rows returned by a query.
```sql
COUNT([ALL | DISTINCT] expression);
```
```sql
COUNT(*)
The `COUNT(*)` function returns the number of rows in a table in a query. It counts duplicate rows and rows that contain null values.
-------------
SELECT
  COUNT(*)
FROM
  employees
WHERE
  job_id = 9;
```
---
#### TRICK: how to decide which columns go into `GROUP BY` and which use aggregate functions:

- If a column appears **without an aggregate function** (like `department_id`), it **must** be in the `GROUP BY`.
- If a column appears **inside an aggregate function** (`COUNT`, `SUM`, `AVG`, `MAX`, etc.), it does **not** need to be in `GROUP BY`.

**Purpose of `GROUP BY`**
You use `GROUP BY` when:
- You want to **group rows** by one or more columns.
- Then, apply an **aggregate function** (like total, average, min, max, etc.) for each group.
Average salary per department: means group karna hai dept and avg(salary)
- All non-aggregated columns in `SELECT` → must appear in `GROUP BY`.
- Aggregated columns (`SUM`, `COUNT`, `AVG`, `MIN`, `MAX`) → do not go into `GROUP BY`.
---
- **MAX** : allows you to find the maximum value in a set of values.
```sql
SELECT
  MAX(salary)
FROM
  employees;
```
- **MIN** :  returns the minimum value in a set of values.
```sql
SELECT
  MIN(salary) min_salary
FROM
  employees;
```
- **SUM** : returns the sum of all or distinct values. We can apply the `SUM` function to the numeric column only.
```sql
SELECT
  SUM(salary) total_salary
FROM
  employees;
```
---

### HAVING
The GROUP BY clause groups rows of a result set into groups. To specify a condition for filtering groups, you use a `HAVING` clause.
If you use a `HAVING` clause without a `GROUP BY` clause, the `HAVING` clause behaves like a where clause.
```sql
SELECT
  column1,
  column2,
  aggregate_function (column3)
FROM
  table1
GROUP BY
  column1,
  column2
HAVING
  group_condition;
```
---
#### HAVING VS WHERE 

The WHERE clause applies a condition to rows before the rows are summarized into groups by the `GROUP BY` clause. However, the `HAVING` clause applies a condition to the groups after the rows are grouped into groups.
Therefore, it is important to note that the `HAVING` clause is applied after whereas the `WHERE` clause is applied before the `GROUP BY` clause.

---
### CAST : 
The CAST() function converts a value (of any type) into the specified datatype.
```sql
SELECT CAST(150 AS CHAR);
SELECT CAST("2017-08-29" AS DATE);
```
---
### COALESCE()
Handle null values and return them as non-null values
The COALESCE function works as follows:
- It evaluates the expressions in the order they are provided.
- It returns the value of the first non-null expression.
- If all expressions are null, it returns null

Using coalesce to retplace null values

|student_id|student_name|grade|
|---|---|---|
|1|Alice|85|
|2|Bob|NULL|
|3|Carol|92|
|4|Dave|NULL|
|5|Eve|78|

```sql
SELECT student_id, student_name, COALESCE(grade, 'N/A') AS final_grade
FROM Students;
```

|student_id|student_name|final_grade|
|---|---|---|
|1|Alice|85|
|2|Bob|N/A|
|3|Carol|92|
|4|Dave|N/A|
|5|Eve|78|

---
### JOINS
SQL JOINs are used to combine rows from two or more tables based on a related column between them. This allows for the retrieval of data that is distributed across multiple tables

1 **.) INNER JOIN**
If the `condition` is `true`, the `INNER JOIN` merges the rows from both tables to form a single row and includes it in the final result set.
```sql
SELECT
  column1,
  column2
FROM
  table1
  INNER JOIN table2 ON condition;
```
```sql
SELECT
  employee_id,
  name,
  department_name
FROM
  employees
  INNER JOIN departments ON departments.department_id = employees.department_id;
```
Joining 3 tables 
```sql
SELECT
  column1,
  column2,
  column3
FROM
  table1
  INNER JOIN table2 ON condition1
  INNER JOIN table3 ON condition2;
```
2.) **LEFT JOIN**
Left JOINs return all rows from the first table and only those in the second table that match.
```sql
SELECT
  column1,
  column2
FROM
  left_table
  LEFT JOIN right_table ON condition;
```
always includes all rows from the left table.
3.) **RIGHT TABLE**
Left JOINs return all rows from the Right table and only those in the left table that match.
```sql
SELECT
  column1,
  column2
FROM
  left_table
  RIGHT JOIN right_table ON condition;
```
4.) **SLEF JOIN**
A self-join is a join that compares the rows within the same table. You can use a join to compare rows within the same table. In this case, you join a table to itself that forms a self-join.
```sql
SELECT
  select_list
FROM
  table1 t1
  INNER JOIN table1 AS t2 ON t1.column1 = t2.column2;
```
**IMP example is find the manager of user**
In the `employees` table:
- The `employee_id` serves as a unique identifier for each employee.
- The `manager_id` represents the `employee_id` of the manager to whom the current employee reports. If the `manager_id` is `NULL`, it means the employee is the CEO, without a manager.
```sql
SELECT
  e.first_name employee,
  m.first_name manager
FROM
  employees e
  LEFT JOIN employees m ON m.employee_id = e.manager_id
ORDER BY
  manager NULLS FIRST;
  ```

  employee   |  manager
-------------+-----------
 Valli       | Alexander
 Diana       | Alexander
 Bruce       | Alexander
 David       | Alexander
 Guy         | Den
 Karen       | Den
 Alexander   | Lex
 Irene       | Matthew
 
 5.) **FULL OUTER JOIN**
 A `FULL OUTER JOIN` is a combination of a `[LEFT JOIN] and a `[RIGHT JOIN]
 ```aql
 SELECT
  column1,
  column2
FROM
  table1
  FULL JOIN table2 ON condition;
```
6.) **CROSS JOIN**
The `CROSS JOIN` clause merges every row from the first table (`table1`) with every row in the second table (`table2`). It returns a result set that includes all possible combinations of the rows in both tables.
```sql
SELECT
  first_name,
  program_name
FROM
  employees
  CROSS JOIN trainings
ORDER BY
  first_name;
```
---
### SET OPERATION
1.) **UNION**
The `UNION` operator allows you to combine the result sets of two SELECT statements into a single result set.
The `UNION` operator removes duplicate rows from the combined result set, to retain the duplicate rows, you can use the **`UNION ALL`** operator
```sql
SELECT 
    column1, column2
FROM
    table1 
UNION
SELECT 
    column3, column4
FROM
    table2;
```
- The same number of columns selected
- The same number of column expressions
- The same data type and have them in the same order

2.) **INTERSECTION**
The `INTERSECT` operator finds the common rows of the result sets of two SELECT statements.
```sql
SELECT
  column1,
  column2
FROM
  table1
INTERSECT
SELECT
  column1,
  column2
FROM
  table2;
```
the `INTERSECT` operator removes duplicate rows from the final result set.

3.) **MINUS**
The `MINUS` operator returns only the rows that appear in the result set of the first `SELECT` statement but not the second.
```sql
SELECT
  column1,
  column2
FROM
  table1 
MINUS
SELECT
  column1,
  column2
FROM
  table2;
```

---
### INDEX
An index in SQL is a schema object that improves the speed of data retrieval operations on a table.
- Works by creating a separate data structure that provides pointers to the rows in a table. Which makes it faster to look up rows based on specific values.

In SQL, it speeds up **search queries** (`SELECT`, `WHERE`, `JOIN`, `ORDER BY`) by creating a data structure (usually a B-Tree or Hash) on the column(s).
```sql
CREATE INDEX index_name  
ON TABLE table_name(colname,col2name);

-----------------------------------------------------------
CREATE UNIQUE INDEX index_name
on table_name (column_name);

```

**Which columns should have an index?**
You don’t index everything — indexes take extra memory and slow down INSERT/UPDATE/DELETE (because the index also needs updating).  
So, apply indexes wisely:
1. **Primary Key / Unique columns** → automatically indexed.
2. **Foreign keys** → indexing them speeds up joins.
3. Columns used often in `WHERE` conditions.
4. Columns used in join.
5. Columns used in `ORDER BY` or `GROUP BY`.

**Avoid indexing**
- Columns with very few unique values or more null (e.g., `gender` with only `M/F`).
- Very small tables (index won’t help).
- Columns that are updated very frequently (index maintenance slows down inserts/updates).
DROP
```sql
DROP INDEX index_name ON table_name
```

**What happens when you create an index on a column (like networth)?**  
The database creates a separate data structure (usually a B-tree or hash table).  
This index stores:
- The values of the indexed column (networth) in sorted order (if B-tree).
- A pointer (mapping) to the actual rows in the main table.  

So it’s not making a whole new "table" like we normally think, but a special lookup structure that works like a mini table.  

| ID | Name    | Age | Networth |
| -- | ------- | --- | -------- |
| 1  | Alice   | 25  | 50K      |
| 2  | Bob     | 30  | 80K      |
| 3  | Charlie | 28  | 20K      |

If we create an index on Networth, the DB internally makes something like:  

Index on Networth (B-tree style):
| Networth | Pointer to Row |
| -------- | -------------- |
| 20K      | Row 3          |
| 50K      | Row 1          |
| 80K      | Row 2          |

```sql
SELECT * FROM Customers WHERE Networth = 50K;

```
Without index → DB scans all rows (O(n) time).

With index → DB goes to the index, finds 50K quickly (O(log n) with B-tree), then jumps straight to the matching row in the main table.  

---

### FOREIGN KEY
- A foreign key is a column in a table that is a reference to the primary key of another table.
- It is used to establish a relationship between two tables, ensuring data integrity and consistency.

The table with the foreign key is called child table, the table with the primary key is called the parent table or referenced table.
```sql
-- Parent Table
CREATE TABLE Dep (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);

-- Child Table
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    DepartmentID INT,
    FOREIGN KEY (DepartmentID) REFERENCES Dep(DepartmentID)
);
```
##### Violations
- Insert/update child with a non-existent parent.
- Delete parent while children exist (unless CASCADE).
- Modify parent PK without handling child.
- Drop/disable FK carelessly.

When you try to delete a row that is **referenced by a foreign key in another table**, SQL will usually block the deletion because of **referential integrity**.
There are **three main ways** to handle this situation:
##### 1. **Delete the child rows first (manual delete)**

You must first delete all rows in the child table (the one with the foreign key) that reference the parent row.
```sql
-- Suppose orders has a foreign key referencing customers(customer_id)

-- First delete from child table
DELETE FROM orders WHERE customer_id = 5;

-- Then delete from parent table
DELETE FROM customers WHERE customer_id = 5;

```
##### 2. **Use ON DELETE SET NULL (or SET DEFAULT)**
If you want the foreign key in the child table to be set to `NULL` (or a default value) instead of deleting the row:
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id) ON DELETE SET NULL
);
```
##### 3. **CASCADE KEY**
   - Cascading refers to the behavior that occurs when you perform certain operations on a parent table that has associated child tables with foreign key relationships.
   - Cascade actions define **what should happen to the child records when certain operations are performed on the parent record**
   - When a CASCADE action is specified for a foreign key, it means that changes made to the referenced primary key in the parent table will automatically propagate to the child table with the foreign key.ds.
-  **ON UPDATE CASCADE** → If the parent key changes, the child key updates too.    
- **ON DELETE CASCADE** → If a parent row is deleted, related child rows are also deleted.
```sql
CREATE TABLE Customers (
  customer_id INT PRIMARY KEY,
  name VARCHAR(50)
);

CREATE TABLE Orders (
  order_id INT PRIMARY KEY,
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES Customers(customer_id) ON DELETE CASCADE
);
INSERT INTO Customers VALUES (1, 'Alice');
INSERT INTO Orders VALUES (101, 1), (102, 1);
DELETE FROM Customers WHERE customer_id = 1;
--Automatically, orders `101` and `102` will also be deleted (no manual delete needed).
```

---

### **What is cursor**   
A cursor in SQL is a database object that allows you to retrieve, manipulate, and process rows one at a time from a result set. Work with stored procedures where you need to handle data one record at a time.  
In SQL, a SELECT statement retrieves the entire result set at once — it’s like printing the whole array using System.out.println(arr).  
A cursor, on the other hand, lets you process rows one by one — just like using a for loop and printing each element individually with System.out.println(arr[i]).  
<img width="1222" height="343" alt="image" src="https://github.com/user-attachments/assets/64817137-651e-4374-b67e-ca5acdd5204a" />

---
### **What is Sql injection ?**  
SQL Injection is a common web security vulnerability where an attacker injects malicious SQL code into an input field to manipulate or access the database.  
Think of a website's database as a secure vault and a login form as the guard who asks for your name and password.  
```sql
SELECT * FROM users WHERE username = 'bob' AND password = 'bobspassword123';
```
The attacker enters this into the username field:  
**Username: ' OR 1=1 - -**  
**Password**: (they leave this blank)  
The website (which is poorly secured) builds this new, malicious command:  
```sql i/p(' OR 1=1 --)
SELECT * FROM users WHERE username = '' OR 1=1 --' AND password = '';
---
- WHERE username = '' — the attacker's first ' closes the username string, leaving it empty.
- OR 1=1 — always true, so the WHERE becomes true for every row.
- -- — starts a comment, so the rest (' AND password = '...') is ignored.
- Result: the DB runs effectively SELECT * FROM Users WHERE 1=1; → returns all users.
```
<img width="1570" height="682" alt="image" src="https://github.com/user-attachments/assets/4a4e97f4-8849-4a69-9140-3f08c02be51c" />

---  

### TRANSACTION
A transaction is a sequence of one or more SQL statements that are executed as a single unit of work. Transactions are used to ensure that database operations are performed in a consistent and reliable manner.
Let’s say we want to Insert, Update, or even Delete data from one or more database tables, the Transaction function can help us group together all of these operations as a single unit of work.
#### Properties of transaction
a) **Atomicity** - this ensure either the transaction occur completely or it does not occur at all (all the previous operations are rolled back to their former state.)  
	- If money is deducted from A but not credited to B (due to a failure), the whole transaction **rolls back**.
	- Ensures **no partial transactions** occur.  
b) **Consistency** - ensure the database remains consistent before and after transaction. Database moves from one valid state to another valid state.  
	- If Account A had ₹2000 and B had ₹1000, after transferring ₹500:
	- A → ₹1500, B → ₹1500 (Total = ₹3000, same as before).  
c) **Isolation** - ensures that multiple transaction can occur simultaneously without causing any inconsistency. enables transactions to operate independently of and transparent to each other.  
	- If Account A has ₹2000, and two transfers of ₹500 and ₹1000 happen simultaneously, isolation ensures final balance is **₹500**, not something wrong like **₹1500 or ₹1000**.  
d) **Durability** - ensures that changes after committing successful  transaction are saved. Ensures that the result or effect of a committed transaction persists in case of a system failure.  
	- Once the transaction is **committed**, changes are permanent, even if the system crashes.  
	- If transfer succeeds and a power failure occurs immediately, the updated balances are still stored.  

1.) **BEGIN TRANSACTION** → Starts a new transaction.
```sql
BEGIN TRANSACTION;
```
2.) **COMMIT TRANSACTION** → Saves changes permanently if everything succeeds.
```sql
COMMIT;
```
3.) **ROLLBACK TRANSACTION** → Cancels changes and restores previous state if an error occurs.
```sql
ROLLBACK;
```
EXAMPLE
```slq
BEGIN TRANSACTION;

UPDATE Accounts
SET balance = balance - 500
WHERE account_id = 101;

UPDATE Accounts
SET balance = balance + 500
WHERE account_id = 202;

-- If no errors, save changes
COMMIT;

-- If error occurs, rollback
ROLLBACK;

```

---

### NORMALIZATION
Normalization is the process of organizing data in a database into smaller, related tables to:
- **Remove redundancy** (duplicate data)
- **Avoid anomalies** (update, insert, delete problems)
- **Improve data integrity** (data stays accurate and consistent)

📌 Imagine an Unnormalized table (0NF):

<img width="537" height="190" alt="image" src="https://github.com/user-attachments/assets/76879c2a-e25c-4e00-8e29-b7d3424eb749" />  

**Data redundancy** means the same information is stored in multiple places.
- eg In the table above, the information that "CS101" is "Intro to CS" repeated for every student enrolled in that course.  If thousands of students take CS101, this redundant data would consume significant storage.

An **update anomaly** occurs when you update information in one place but fail to update it in all the other places it's repeated, leading to inconsistent data.
- eg Suppose the course name is changes fron intro to cs to fundamental of cs., you would need to find every single record for every student enrolled in CS101 and change.

An **insertion anomaly** happens when you can't add a new piece of information to the database because another, unrelated piece of information is missing.
- eg Imagine the university wants to add a new course, "PHY350 - Quantum Mechanics" .You cannot add this course to the Student_Enrollment table until at least one student enrolls. The table's structure requires a StudentID to create a row, so there's no way to store information about a course that currently has zero students.

A **deletion anomaly** is the unintentional loss of data that occurs when you delete a different piece of data.
- eg <img width="821" height="277" alt="image" src="https://github.com/user-attachments/assets/9068b118-87a9-4c93-9e14-134ccc262a9a" />


---
### NORMAL FORM 
Normalization is achieved in stages, each called a Normal Form (NF). Each level builds on the previous one, further reducing redundancy and anomalies.
## 1NF 
A table is 1NF when 
- Each cell holds a single, indivisible (atomic) value. You can't have a list of items in one cell.
- Each record is unique, usually accomplished by having a primary key.
- <img width="894" height="557" alt="image" src="https://github.com/user-attachments/assets/2edb5a8e-461b-4aa4-ab28-a6bb7c6d0c60" />

**Problem in 1NF → Why We Need 2NF**
- Redundancy - The Name is repeated for every course. If Alice takes 5 courses, her name “Alice” is repeated 5 times.
- Update Anomaly- If Alice’s name changes to “Alice Brown”, we must update all rows where her name appears.
- Insert Anomaly- If a new student registers but hasn’t chosen any course yet, we can’t insert them without leaving Course empty.

### 2NF  
Rule of 2NF:  
- Table must already be in 1NF.
- No partial dependency → Non-key columns should depend on the whole primary key, not just part of it.  
In our table, the composite primary key is (StudentID, Course).  
Name depends only on StudentID, not on the whole key.  
That’s a partial dependency ❌.  
<img width="837" height="572" alt="image" src="https://github.com/user-attachments/assets/7e6c27af-5fa8-4d49-b0be-f00ef9308525" />

**Problem in 2NF**
<img width="905" height="537" alt="image" src="https://github.com/user-attachments/assets/f24396c8-8b39-4d6a-ada4-51612f14484b" />  
Here Phone depends on Instructor not on the Primary Key.  

### 3NF
- Table must already be in 2NF.
- No transitive dependency → Non-key columns should depend only on the primary key.
<img width="918" height="649" alt="image" src="https://github.com/user-attachments/assets/abeb2c2c-52b7-485b-af42-18018649a1bb" />

Why this is better?  
No repetition of instructor phone numbers.  
If Dr. Smith’s phone number changes, update it in one place only.  
Cleaner, less redundant, and follows 3NF rules.  
**Problem in 3NF**
In a functional dependency X → Y,  
X is the determinant (because the value of X determines Y).  
Example:  
If Instructor → Course, then Instructor is the determinant.  
3NF fixes most redundancy issues, but it still allows certain anomalies (insertion, update, deletion) when:
A non-prime attribute (not part of any candidate key) depends on a non-key attribute.  
In short, 3NF allows some situations where a determinant is not a key.  
Functional dependencies here:  
(StudentID → Course, Instructor)  (fine, StudentID is a key)   
Instructor → Course  (problem: Instructor is NOT a key)  
Here, Instructor is the determinant, but it’s not a candidate key (because many students can have the same instructor).  
Insertion anomaly  
You hire Dr. White to teach English.  
Can you add him?  No.  
Why? Because the table needs a StudentID, but no student has enrolled yet.   
So you can’t insert the fact that "Dr. White teaches English".  

### BCNF
A table is in BCNF if:
- It is in 3NF.
- Every determinant is a candidate key (handles anomalies not covered in 3NF).
It says: “For every dependency X → Y, X must be a candidate key.”
This removes all anomalies that 3NF can’t fully solve.
<img width="636" height="609" alt="image" src="https://github.com/user-attachments/assets/de1f0a6f-7ffb-4fb8-9a7e-722005527d04" />

---
### Denormalization
Denormalization is the process of intentionally combining normalized tables back together (or introducing some redundancy) to improve read performance of the database.  
**Why do we need it?**
In real systems, data is read much more often than it’s written.  
Normalized databases often require multiple joins to get useful info.  
Too many joins = slower queries.  
Denormalization avoids extra joins by keeping data together   

--- 


