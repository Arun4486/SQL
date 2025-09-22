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

    1. Create a Table
```SQL
        CREATE TABLE Employees (
        emp_id INT PRIMARY KEY,
        emp_name VARCHAR(50) NOT NULL,
        salary DECIMAL(10,2),
        dept_id INT
        );
```
        CREATE TABLE → makes a new table.

    2. Insert Data into a Table
```SQL
        INSERT INTO Employees (emp_id, emp_name, salary, dept_id)
        VALUES (1, 'Amit', 50000, 101);
```
    3. View Table Structure
```SQL
        SELECT * FROM EMP;
```
    4. Alter a Table --> 
        A. Add a new column
```SQL
                ALTER TABLE Employees
                ADD email VARCHAR(100);
```
        B. Modify a column -- to change the datatype and constraints.
```SQL
                ALTER TABLE Employees
                MODIFY salary VARCHAR(20);
```
        C. Drop a column
```SQL
                ALTER TABLE Employees
                DROP COLUMN email;
```
        D. Rename a Table
```SQL    
                ALTER TABLE Employees
                RENAME TO Staff;
```
        E. Rename a Column 
```SQL
                ALTER TABLE Employees
                CHANGE emp_name full_name VARCHAR(50);
```
    6. Drop a Table --> Deletes the whole table with data.
```SQL
        DROP TABLE Employees;
```
    7. Truncate a Table --> Removes all rows but keeps the structure.
```SQL
        TRUNCATE TABLE Employees;
```

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

# Connecting two tables with FK :-

```SQL
                        CREATE TABLE DEPT (
                        ID INT PRIMARY KEY,
                        NAME VARCHAR(20)
                        );
                        INSERT INTO DEPT (ID, NAME)
                        VALUES
                        (101, "SCIENCE"),
                        (102, "MATHS"),
                        (103, "HINDI");
                        SELECT * FROM DEPT;

                        CREATE TABLE TUTOR (
                        TUT_ID INT PRIMARY KEY,
                        NAME VARCHAR(20),
                        DEPT_ID INT,
                        FOREIGN KEY (DEPT_ID) REFERENCES DEPT (ID)
                        );
                        INSERT INTO TUTOR (TUT_ID, NAME , DEPT_ID)
                        VALUES
                        (01, "ADOM", 101),
                        (02, "BOB", 102),
                        (03, "CASSY", 103);
```
                        here DEPT table is called parent table and TUTOR table is called child table
# Cascading for FK :-
        the changes made to the key in parent table should reflect in key in the child key.
        1. ON DELETE CASCADE
        2. ON UPDATE CASCADE
```SQL
                        CREATE TABLE TUTOR (
                            TUT_ID INT PRIMARY KEY,
                            NAME VARCHAR(20),
                            DEPT_ID INT,
                            FOREIGN KEY (DEPT_ID) REFERENCES DEPT (ID)
                            ON DELETE CASCADE
                            ON UPDATE CASCADE
                            );
                        INSERT INTO TUTOR (TUT_ID, NAME , DEPT_ID)
                        VALUES
                        (01, "ADOM", 101),
                        (02, "BOB", 102),
                        (03, "CASSY", 103);

                        UPDATE DEPT
                        SET ID = 104
                        WHERE ID = 102;
                        SELECT * FROM DEPT;

                        SELECT * FROM TUTOR;
```

# Alias names -: 
                alternate name (AS)
```sql
                SELECT MAX(salary) AS highest_salary
                FROM Employees;
```

# JOINS :- 
        JOINs are used to combine rows from two or more tables based on a related column between them.
        FK is notn compulsory for joining two tables.

        1. INNER JOIN --> Returns only the rows that have matching values in both tables.
                          order of writing table A, or B doesn't matter here.
```sql
                SELECT employees.id, employees.name, departments.dept_name
                FROM employees
                INNER JOIN departments
                ON employees.dept_id = departments.id;

                -- OR 
                SELECT * 
                FROM employees as emp
                INNER JOIN departments AS dept
                ON emp.dept_id = dept.id; 
```

        2. LEFT JOIN (or LEFT OUTER JOIN) --> Returns all rows from the left table, and the matched rows from the right table. for rows where there is no match, NULL is returned for right side.
```sql
                SELECT employees.id, employees.name, departments.dept_name
                FROM employees
                LEFT JOIN departments
                ON employees.dept_id = departments.id;
```
        3. RIGHT JOIN (or RIGHT OUTER JOIN) --> Returns all rows from the right table, and the matched rows from the left table. If there is no match, NULL is returned for left side.
```sql
                SELECT employees.id, employees.name, departments.dept_name
                FROM employees
                RIGHT JOIN departments
                ON employees.dept_id = departments.id;
```
        4. FULL OUTER JOIN --> Returns all rows when there is a match in either left or right table. If no match, NULL is returned for missing side. this is not in mysql, but in oracle and postgress, to do it in sql, use UNION.
```sql 
                SELECT * FROM TEACHERS AS T
                LEFT JOIN COURSES AS C
                ON T.SUB = C.COURSE
                UNION
                SELECT * FROM TEACHERS AS T
                RIGHT JOIN COURSES AS C
                ON T.SUB = C.COURSE;
                -- OR
                SELECT employees.id, employees.name, departments.dept_name
                FROM employees
                FULL OUTER JOIN departments
                ON employees.dept_id = departments.id;
```
        5. CROSS JOIN --> Returns the Cartesian product of both tables (every row from table A combined with every row from table B).
```sql
                SELECT employees.name, departments.dept_name
                FROM employees
                CROSS JOIN departments;

```

        6. -- LEFT EXCLUSIVE JOIN --> gives only roes of table a, ignores the common rows.
```sql
                SELECT *
                FROM TEACHERS T
                LEFT JOIN COURSES C
                ON T.SUB = C.COURSE
                WHERE C.ID IS NULL;
```
        7.RIGHT EXCLUSIVE JOIN --> fives only rows of table be , ignores thee common rows.
```sql
                SELECT *
                FROM TEACHERS T
                RIGHT JOIN COURSES C
                ON T.SUB = C.COURSE
                WHERE T.ID IS NULL;
```

        8. FULL EXCLUSIVE JOIN --> returns the uncommon rows from both tables.
```sql
                SELECT * FROM TEACHERS T
                LEFT JOIN COURSES C
                ON T.SUB = C.COURSE
                WHERE C.ID IS NULL
                UNION
                SELECT * FROM TEACHERS T
                RIGHT JOIN COURSES C
                ON T.SUB = C.COURSE
                WHERE T.ID IS NULL;
```
        INNER JOIN → Matching rows only.
        LEFT JOIN → All from left + matched from right.
        RIGHT JOIN → All from right + matched from left.
        FULL JOIN → All rows from both sides, if a match.
        CROSS JOIN → Every combination of rows.


# UNION :-
        The UNION operator is used to combine the result sets of two or more SELECT statements.
        It removes duplicates by default (like DISTINCT).
        TO get all elements including duplicates, use UNION ALL.
        The columns in all queries must have:
                The same number of columns
                The same data types (or compatible types)
                The same order of columns
```sql
                SELECT column1, column2 FROM table1
                UNION
                SELECT column1, column2 FROM table2;
```

# SUB-QUERY :- 
        A subquery is a query inside another query.
                It is usually placed inside parentheses (...).
                It can return a single value, a single row, or multiple rows.
                It can be used in SELECT, FROM, WHERE, HAVING, etc.
```SQL
                SELECT * FROM MARKS
                WHERE SCORE > (SELECT AVG(SCORE) FROM MARKS);
```

        Types --> 
        1. Scalar Subquery (returns a single value)
```sql        
                SELECT name, salary
                FROM employees
                WHERE salary > (SELECT AVG(salary) FROM employees);
```
                Returns employees whose salary is above the average salary.

        2. Row Subquery (returns one row)
```sql        
                SELECT *
                FROM employees
                WHERE (dept_id, salary) = (SELECT dept_id, MAX(salary) 
                                        FROM employees GROUP BY dept_id LIMIT 1);
```
                Returns employee with the highest salary in a department.

        3. Table Subquery (returns multiple rows / columns)
```sql
                SELECT name
                FROM employees
                WHERE dept_id IN (SELECT id FROM departments WHERE location = 'New York');
```
                Finds employees working in departments located in New York.

        4. Subquery in FROM (Derived Table)
```sql
                SELECT dept_id, AVG(salary) as avg_salary
                FROM (SELECT * FROM employees WHERE active = 1) AS active_employees
                GROUP BY dept_id;
```
                Here the subquery acts like a temporary table.

        5. Correlated Subquery (depends on outer query)
```sql
                SELECT e1.name, e1.salary
                FROM employees e1
                WHERE salary > (SELECT AVG(e2.salary)
                                FROM employees e2
                                WHERE e1.dept_id = e2.dept_id);
```

                Finds employees whose salary is above their department’s average.

# VIEWS :- 
        A View is a virtual table based on a SQL query.
        It does not store data itself — it stores the query definition.
        When you query a view, SQL runs the underlying query and returns the result.
        basically it is abstraaction.
        it is used as a temp table, so that if you don't want someone to see the complete table
        Creating a View --
```SQL
                CREATE VIEW EmployeeView AS
                SELECT id, name, salary
                FROM employees
```
        Using a View --> 
```sql
                SELECT * FROM EmployeeView;
```
                Works just like querying a normal table.

        Updating a View --> 
```sql
                UPDATE EmployeeView
                SET salary = salary + 5000
                WHERE id = 3;
```
                Updates the employees table too.

        But if the view contains joins, group by, or aggregations, it’s usually read-only.

        Dropping a View --> 
```sql
                DROP VIEW EmployeeView;
```
        Advantages of Views --> 

                Security – restrict access to certain columns/rows.
                Simplicity – hide complex queries.
                Reusability – write query once, use it everywhere.
                Consistency – ensure all users see the same derived data.