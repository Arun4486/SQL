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
