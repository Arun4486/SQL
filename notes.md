# Data :- 
    data is a rawfact that is used to define charecterstics / attributes of an entity 
# Database :- 
    Collection of interrealated data that is accessible digitally
# DBMS :- 
    s/w used to manage DB
# types od DB : 
    1. Relational Db --> data stored in tabular formate.
        ex. mysql, postgreSQL, oracle
    2. Non-relational DB --> it stores data in more flexible ways such as documents, key-value pairs, graphs, or wide columns.
        Ex. mongoDB
# SQL :-
    Structured Query lang. by IBM
    Programming lang. used to interact with RDB. it uses CRUD to do so
    SEQUEL --> Structured nglish Query Lang.

# Table :-
    is a collection of rows and cols, 
    Col --> general info , schema, structure, feild
    row --> individual data of an entity, tupple

# Creating DB :-
```sql
create Database db_name;
use db_name;
drop DATABSE db_name;

create database if not exists db_name; -- doesn't give error only a warning that db exists already.

drop database if exists db_name;

show databases;
show tables;
```


# CREATING TABLE :-
```SQL
USE db_name;
CREATE TABLE tbl_name(
    col_1 datatype (constraint),
    col_2 datatype (constraint),
    col_3 datatype (constraint)
);

CREATE TABLE student(
    id INT PRIMARY KEY,
    name VARCHAR(40),
    age INT
)

INSERT INTO student VALUES(1, "AMAN", 21);
INSERT INTO student VALUES(2, "AKASH", 22);

-- OR

INSERT INTO STUDENT (ID, NAME, AGE) VALUES
(01, "AMAN", 21),
(02, "RAMAN", 22),
(03, "BHUVAN", 21);

SELECT * FROM student; -- * for all cols.  

```

# Datatypes :-
    1. CHAR --> string (0-255) store string of fixed length.
        Faster for data of consistent length. Useful when all values in a column have the same size.
        Ex. phone no. country name abbr, gender abbr.

    2. VARCHAR --> string (0-255) string of variable length.
        slightly slower for length check, Uses only needed space.
        Ex. Names, addresses, emails, variable text. 

    3. BLOB -->  Binary Large Object
                It is used to store large binary data like images, audio, video, PDFs, or any file in a database.
```sql
                CREATE TABLE Photos (
                id INT AUTO_INCREMENT PRIMARY KEY,
                name VARCHAR(100),
                image BLOB
                );
```
                storing in such way can make DB slow so we use reference. (links and path of a cloud storage).
    
    4. INT
    5. TINYINT --> int(-128 to 127)
    6. BIGINT
    
    7. FLOAT --> decimals with precision to 23 digits.
    8. DOUBLE --> decimals with precision 24 to 53 digits.
    9. BOOLEAN --> SQL doesn’t have a dedicated boolean type in all databases.Instead, most databases treat BOOLEAN as an alias for a numeric type (like TINYINT, BIT, or BOOL).
    10. DATE / YEAR

    11. BIT --> bit(1/2).

    SIGNED --> TINYINT (-128 to 127) both +ve and -ve.
    UNSIGNED --> TINYINT UNSIGNED ( 0 to 255) only +ve data like age salery etc. used to expand the range of datatype.

# types of sql commands :-
    1. DDL --> data definition lang.
               to define or modify the structure of database objects (tables, schemas, indexes, etc.).
               EX. create, alter, drop, truncate, rename.
    
    2. DML --> data manipulation lang. 
               Used to work with data inside tables.
               Ex. insert, update, delete.

    3. DQL --> data query lang.
               to fetch data from database.
               Ex. select.

    4. DCL --> Data control lang.
               Used to control access and permissions.
               Ex. grant, revoke.
```sql
               GRANT SELECT, INSERT ON Students TO 'user1';
               REVOKE INSERT ON Students FROM 'user1';
```
    5. TCL --> Transaction control lang.
               Used to manage transactions (group of SQL statements executed as one unit).
               Ex. commit, rollback, savepoint.
```sql
               BEGIN;
               UPDATE Students SET age = 25 WHERE id = 1;
               ROLLBACK; -- undo the change
               COMMIT;   -- confirm the change

```

# table related queries :-
    1. CREATE
    2. INSERT
    3. SELECT
    4. DROP

# Clauses :-
        are keywords that define specific conditions, filters, or behaviors in SQL statements.
        They modify queries and control how data is fetched, filtered, grouped, or sorted.

        1. WHERE → Filters rows based on a condition.
```sql
                SELECT * FROM Employees
                WHERE department = 'HR';
```

        2. ORDER BY → Sorts results in ascending (ASC, default) or descending (DESC) order.
```sql
                SELECT * FROM Employees
                ORDER BY salary DESC;
```

        3. GROUP BY → Groups rows based on column values (usually with aggregate functions like COUNT, SUM).
```sql
                SELECT department, COUNT(*) 
                FROM Employees
                GROUP BY department;
```

        4. HAVING → Applies conditions to grouped records (like WHERE but for groups).
```sql
                SELECT department, AVG(salary) 
                FROM Employees
                GROUP BY department
                HAVING AVG(salary) > 50000;
```

        5. LIMIT / TOP / FETCH → Restricts the number of rows returned.
```sql
                SELECT * FROM Employees
                LIMIT 5;
```

        6. DISTINCT → Removes duplicate rows from results.
```sql
                SELECT DISTINCT department FROM Employees;
```

        7. JOIN Clauses → Combine rows from multiple tables.
```sql
                SELECT e.name, d.department_name
                FROM Employees e
                JOIN Departments d ON e.dept_id = d.dept_id;
```
        Filtering → WHERE, HAVING
        Sorting → ORDER BY
        Grouping → GROUP BY
        Limiting → LIMIT / TOP
        Removing duplicates → DISTINCT
        Combining tables → JOIN

# Aggregate Functions :-
        Aggregate functions perform a calculation on a set of values and return a single value.
        They are mostly used with GROUP BY and HAVING clauses.

        1. COUNT() → Counts number of rows.
```sql
                SELECT COUNT(*) AS total_employees
                FROM Employees;
```

        2. SUM() → Adds up values in a column.
```sql
                SELECT SUM(salary) AS total_salary
                FROM Employees;
```

        3. AVG() → Returns the average of values.
```sql
                SELECT AVG(salary) AS average_salary
                FROM Employees;
```

        4. MIN() → Finds the smallest value.
```sql
                SELECT MIN(salary) AS lowest_salary
                FROM Employees;
```

        5. MAX() → Finds the largest value.
```sql
                SELECT MAX(salary) AS highest_salary
                FROM Employees;
```
        Using with GROUP BY
                Aggregate functions often pair with GROUP BY to calculate per group:
```sql
                SELECT department, COUNT(*) AS total_employees, AVG(salary) AS avg_salary
                FROM Employees
                GROUP BY department;
```
        GENERAL ORDER OF COMMANDS --> 
            1. SELECT 
            2. FROM
            3. WHERE
            4. GROUP BY
            5. HAVING
            6. ORDER BY
```SQL
            SELECT CITY 
            FROM STUDENTS
            WHERE GRADE = "A"
            GROUP BY CITY
            HAVING MAX(MARKS) >= 93
            ORDER BY CITY;
```

# Key :- 
    are constraints that ensure the uniqueness, relationship, and integrity of data in a database table.
     

# Type of keys :-
    1. PRIMARY KEY --> a column or set of cols that Uniquely identifies each record/row in a table. 
                       I can not be null,
                       only one PK per table. 
    3. FOREIGN KEY --> Establishes a relationship between two tables.
                       Refers to the primary key of another table.
                       can be mupltiple FK, 
                       can have duplicate and null values.
                       Maintains referential integrity.
                       REFERENTIAL INTEGRITY => It ensures that a foreign key value in one table always points to an existing primary key in another table.
                                                Prevents orphan records (foreign keys that don’t match any primary key).
```sql
                        CREATE TABLE Students (
                        student_id INT PRIMARY KEY,
                        name VARCHAR(50)
                        );

                        CREATE TABLE Enrollments (
                        enrollment_id INT PRIMARY KEY,
                        student_id INT,
                        course VARCHAR(50),
                        FOREIGN KEY (student_id) REFERENCES Students(student_id)
                        );

``` 
                        Enrollments.student_id must exist in Students.student_id.
                        You cannot insert a record in Enrollments with a student_id that doesn’t exist in Students.

    3. UNIQUE KEY -->   Ensures all values in a column are unique.
                        Allows NULL values (but only one per column).
                        A table can have multiple unique keys.
```sql
                        CREATE TABLE Users (
                        user_id INT PRIMARY KEY,
                        email VARCHAR(100) UNIQUE
                        );
                        -- email must be unique for each user.
```
    4. CANDIDATE KEY -->A column (or group of columns) that can uniquely identify a row.
                        Every candidate key can become a primary key, but only one is chosen.
                        If a table has both email and phone as unique, both are candidate keys.
    
    5. COMPOSITE KEY -->A key formed by two or more columns together to uniquely identify a record.
```sql
                        CREATE TABLE Enrollments (
                        student_id INT,
                        course_id INT,
                        PRIMARY KEY (student_id, course_id)
                        );
```
    6. ALTERNATE KEY -->Any candidate key that is not chosen as the primary key.
                        If both email and phone can uniquely identify users, and you choose email as primary → then phone is an alternate key.
    
    7. SUPER KEY -->    A set of one or more columns that can uniquely identify a record.
                        Primary key + Candidate keys + Alternate keys are all super keys.
                        In Students(student_id, email), both {student_id}, {email}, {student_id, email} are super keys.

    Primary Key → Main unique identifier.
    Foreign Key → Links tables.
    Unique Key → Ensures uniqueness but allows null.
    Candidate Key → Possible primary keys.
    Composite Key → Multi-column primary key.
    Alternate Key → Candidate key not chosen.
    Super Key → Any unique identifier set.

# UPDATE :-
        is used to modify existing records in a table.
```SQL
        UPDATE table_name
        SET column1 = value1,
        column2 = value2,
        ...
        WHERE condition;
```

# DELETE :-
        used to remove rows from a table.
```SQL
        DELETE FROM students
        WHERE CITY = "DELHI";
```


# OPERATORS :-
            1. ARITHMATIC OP
            2. LOGICAL OP --> AND, OR, NOT, IN, BETWEEN, LIKE, ALL, ANY
```SQL
                SELECT * FROM STUDENTS WHERE MARKS BETWEEN (80 AND 90);

                SELECT * FROM STUDENTS WHERE CITY IN ("DELHI", "MUMBAI");

                SELECT * FROM STUDENTS WHERE CITY NOT IN ("DELHI", "MUMBAI");
```
            3. BITWISE OP
            4. COMPARISION OP
            Examples : 
                1. Arithmetic Operators → +, -, *, /, %
```sql
SELECT salary + 500 AS new_salary
FROM employees;
```
                2. Comparison Operators → =, != or <>, >, <, >=, <=
```sql
SELECT *
FROM employees
WHERE salary > 30000;
```
                3. Logical Operators → AND, OR, NOT
```sql
SELECT *
FROM employees
WHERE department = 'HR' AND salary > 25000;
```
                4. Special Operators → BETWEEN, IN, LIKE, IS NULL
```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```  
