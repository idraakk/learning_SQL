# SQL Notes

## Database Operations

```sql
CREATE DATABASE temp1;  
CREATE DATABASE IF NOT EXISTS temp1; -- another method  
DROP DATABASE temp1;  
DROP DATABASE IF EXISTS temp1; -- another method  
```

## Creating and Using a Database

```sql
CREATE DATABASE college;  
USE college;  
```

## Table Schema (Design)

```sql
CREATE TABLE student (  
  id INT PRIMARY KEY,  
  name VARCHAR(50),  
  age INT NOT NULL  
);  
```

## Viewing Databases and Tables

```sql
SHOW DATABASES;  
SHOW TABLES; -- from the database that we USE  
```

## Dropping a Table

```sql
DROP TABLE student;  
```

## Creating a Table with Constraints

```sql
CREATE TABLE student (  
  roll_no INT PRIMARY KEY,  
  name VARCHAR(50)  
  -- or  
  -- PRIMARY KEY (id, name)  
  -- if combination is a primary key  
);  
```

### Constraints
- `NOT NULL`
- `UNIQUE`
- `PRIMARY KEY`
- `DEFAULT` - to set default value of a column
```sql
  salary INT DEFAULT 50000
```
- `CHECK` - eg:
```sql
  age INT CHECK (age >= 18)  
  CONSTRAINT age_check_constraint_name CHECK (age >= 18 AND city = "Delhi")  
```

## Inserting Data into a Table

```sql
INSERT INTO student  
(roll_no, name)  
VALUES  
(101, "Arjun"),  
(102, "Karan");  

INSERT INTO student VALUES (103, "Ram");  
```

## Selecting Data
```sql
SELECT * FROM student;  
```

## Creating a Table with Foreign Key

```sql
CREATE TABLE courses (  
  roll INT,  
  student_name VARCHAR(50),  
  course_name VARCHAR(50),  
  FOREIGN KEY (roll) REFERENCES student(roll_no)  
);
```

Note: A foreign key must reference a primary key or a unique column in the parent table. It can be `NULL` or `NOT NULL`, `UNIQUE` or `NOT UNIQUE`.

## Selecting Specific Data

```sql
SELECT * FROM courses;  
SELECT roll_no FROM student;  
SELECT DISTINCT roll_no FROM student;  
```

## Clauses and Operators

### Clauses
- `WHERE`
- `LIMIT` - sets limit to the number of rows
- `ORDER BY` - ASC or DESC
- `GROUP BY` - generally used with aggregate functions
```sql
   SELECT city, count(name) FROM student GROUP BY city ORDER BY count(name) DESC;  
```
  Will give every city followed by the number of names with that city.  
```sql  
  SELECT city, name, count(roll_no) FROM student GROUP BY city, name ORDER BY count(name) DESC;  
```
  Would have given an error if both city and name were not added to `GROUP BY`.  
- `HAVING` - Generally used with `GROUP BY` because it is a condition after and for `GROUP BY`
```sql
  SELECT city, COUNT(roll_no)  
  FROM student  
  GROUP BY city  
  HAVING MAX(marks) > 90;
```

### General Order of Clauses

```sql
SELECT column(s)  
FROM table  
WHERE condition  
GROUP BY column(s)  
HAVING condition  
ORDER BY column(s) ASC;
``` 

## Examples of Select Statements

```sql
SELECT * FROM student WHERE roll_no > 101 AND name = "Ram";  
SELECT * FROM student WHERE roll_no BETWEEN 101 AND 103;  
SELECT * FROM student WHERE name IN ("Arjun", "Karan");  
SELECT * FROM student WHERE name NOT IN ("Arjun", "Karan");  
SELECT * FROM student LIMIT 3;  
SELECT * FROM student WHERE roll_no > 101 LIMIT 1;  
SELECT * FROM student WHERE roll_no > 101 ORDER BY roll_no ASC LIMIT 2;  
```sql

## Aggregate Functions

- `COUNT()`
- `MAX()`
- `MIN()`
- `SUM()`
- `AVG()`

### Example
```sql
SELECT MAX(roll_no) FROM student;
```
