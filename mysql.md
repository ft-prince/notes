MySQL Cheat List
===

This cheat sheet is designed to quickly understand the main concepts involved in [MySQL](https://mysql.com), and provides the most commonly used SQL statements for your reference.

getting Started
---

### introduce
<!--rehype:wrap-class=row-span-3-->

MySQL is a relational database (Relational Database Management System). A relational database consists of one or several tables, such as a table as shown below

----

```bash
    name ▼ key ▼ column (col)
┌┈┈┈┈┬┈┈┈┈┈┈┈┈┬┈┈┈┈┈┈┬┈┈┈┈┈┈┈┐
┆ id ┆ name ┆ uid ┆ level ┆ ◀ header
├┈┈┈┈┼┈┈┈┈┈┈┈┈┤┈┈┈┈┈┈┤┈┈┈┈┈┈┈┤
┆ 1 ┆ mysql ┆ 0 ┆ 3 ┆
├┈┈┈┈┼┈┈┈┈┈┈┈┈┤┈┈┈┈┈┈┤┈┈┈┈┈┈┈┤
┆ 2 ┆ redis ┆ 12 ┆ 1 ┆ ◀ row
└┈┈┈┈┴┈┈┈┈┈┈┈┈┴┈┈┈┈┈┈┴┈┈┈┈┈┈┈┘
    redis ▲ value
```

----

- `Header` The name of each column
- `Column(col)` A collection of data with the same data type
- `Row` Each line is used to describe specific information about a person/thing
- `value(value)` Row specific information, each value has the same data type as the column
- `Key(key)` is a method used to identify a specific person/thing and is unique

### Log in to MySQL

```shell
#Default username <root>, -p is the password,
# ⚠️No spaces required after parameters
mysql -h 127.0.0.1 -u <username> -p <password>
mysql -D database name -h host name -u user name -p
mysql -h <host> -P <port number> -u <user> -p [db_name]
mysql -h <host> -u <user> -p [db_name]
```

### common
<!--rehype:wrap-class=row-span-3-->

#### DatabaseDatabase

:-|:-
:-|:-
`CREATE DATABASE` db `;` | `Create` database
`SHOW DATABASES;` | `List` databases
`USE` db`;` | `switch` to database
`CONNECT` db `;` | `switch` to database
`DROP DATABASE` db`;` | `Delete` database

#### TableTable

:-|:-
:-|:-
`SHOW TABLES;` | List the tables of the current database
`SHOW FIELDS FROM` t`;` | List fields of table
`DESC` t`;` | Display table structure
`SHOW CREATE TABLE`t`;` | Show create table sql
`TRUNCATE TABLE`t`;` | Delete all data in the table
`DROP TABLE`t`;` | Delete table

#### Process

:-|:-
:-|:-
`show processlist;` | List processes
`kill` pid`;` | Kill process

### View MySQL information

```shell
# Display various information about the current mysql version
mysql> status;
# Display the current mysql version information
mysql> select version();
# Check MySQL port number
mysql> show global variables like 'port';
```

### Exit MySQL session

```bash
mysql> exit
```

Exit `quit;` or `\q;` has the same effect

### Backup

Create backup

```sql
mysqldump -u user -p db_name > db.sql
```

Export database without schema

```shell
mysqldump -u user -p db_name --no-data=true --add-drop-table=false > db.sql
```
<!--rehype:className=wrap-text -->

Restore backup

```shell
mysql -u user -p db_name < db.sql
```

MySQL example
------

### Manage forms

Create a new table with three columns

```sql
CREATE TABLE t (
    id INT,
    name VARCHAR DEFAULT NOT NULL,
    price INT DEFAULT 0
    PRIMARY KEY(id)
);
```

Delete table from database

```sql
DROP TABLE t;
```

Add new columns to table

```sql
ALTER TABLE t ADD column;
```

Delete column c from table

```sql
ALTER TABLE t DROP COLUMN c ;
```

Add constraints

```sql
ALTER TABLE t ADD constraint;
```

Delete constraints

```sql
ALTER TABLE t DROP constraint;
```

Rename table from t1 to t2

```sql
ALTER TABLE t1 RENAME TO t2;
```

Rename column c1 to c2

```sql
ALTER TABLE t1 RENAME c1 TO c2;
```

Change the data type of column c1 to datatype

```sql
ALTER TABLE t1 MODIFY c1 datatype;
```

Delete all data in table

```sql
TRUNCATE TABLE t;
```

### Query data from the table

Query the data in columns c1 and c2 from the table

```sql
SELECT c1, c2 FROM t
```

Query all rows and columns in a table

```sql
SELECT * FROM t
```

Query data and filter rows using conditions

```sql
SELECT c1, c2 FROM t
WHERE condition
```

Query different rows in table

```sql
SELECT DISTINCT c1 FROM t
WHERE condition
```

Sort the result set in ascending or descending order

```sql
SELECT c1, c2 FROM t
ORDER BY c1 ASC [DESC]
```

Skip the offset of the row and return the next n rows

```sql
SELECT c1, c2 FROM t
ORDER BY c1
LIMIT n OFFSET offset
```

Group rows using aggregate functions

```sql
SELECT c1, aggregate(c2)
FROM t
GROUP BY c1
```

Filter groups using the HAVING clause

```sql
SELECT c1, aggregate(c2)
FROM t
GROUP BY c1
HAVING condition
```

### Query from multiple tables
<!--rehype:wrap-class=row-span-2-->

Internally connect t1 and t2

```sql
SELECT c1, c2
FROM t1
INNER JOIN t2 ON condition
```

Left join t1 and t1

```sql
SELECT c1, c2
FROM t1
LEFT JOIN t2 ON condition
```

Right connect t1 and t2

```sql
SELECT c1, c2
FROM t1
RIGHT JOIN t2 ON condition
```

Perform a full outer join

```sql
SELECT c1, c2
FROM t1
FULL OUTER JOIN t2 ON condition
```

Generates the Cartesian product of rows in a table

```sql
SELECT c1, c2
FROM t1
CROSS JOIN t2
```

Another way to perform a cross-connect

```sql
SELECT c1, c2
FROM t1, t2
```

Join t1 to itself using INNER Join clause

```sql
SELECT c1, c2
FROM t1 A
INNER JOIN t1 B ON condition
```

Using SQL operators, merge rows from two queries

```sql
SELECT c1, c2 FROM t1
UNION [ALL]
SELECT c1, c2 FROM t2
```

Returns the intersection of two queries

```sql
SELECT c1, c2 FROM t1
INTERSECT
SELECT c1, c2 FROM t2
```

Subtract one result set from another result set

```sql
SELECT c1, c2 FROM t1
MINUS
SELECT c1, c2 FROM t2
```

Use pattern matching %query_row_

```sql
SELECT c1, c2 FROM t1
WHERE c1 [NOT] LIKE pattern
```

Query rows in list

```sql
SELECT c1, c2 FROM t
WHERE c1 [NOT] IN value_list
```

Query rows between two values

```sql
SELECT c1, c2 FROM t
WHERE c1 BETWEEN low AND high
```

Check if the value in the table is NULL

```sql
SELECT c1, c2 FROM t
WHERE c1 IS [NOT] NULL
```

### Using SQL constraints

Set c1 and c2 as primary keys

```sql
CREATE TABLE t(
    c1 INT, c2 INT, c3 VARCHAR,
    PRIMARY KEY (c1,c2)
);
```

Set column c2 as foreign key

```sql
CREATE TABLE t1(
    c1 INT PRIMARY KEY,  
    c2INT,
    FOREIGN KEY (c2) REFERENCES t2(c2)
);
```

Make the values ​​in c1 and c2 unique

```sql
CREATE TABLE t(
    c1 INT, c1 INT,
    UNIQUE(c2,c3)
);
```

Make sure the values ​​in c1>0 and c1>=c2

```sql
CREATE TABLE t(
  c1 INT, c2 INT,
  CHECK(c1> 0 AND c1 >= c2)
);
```

The setting value in column c2 is not NULL

```sql
CREATE TABLE t(
     c1 INT PRIMARY KEY,
     c2 VARCHAR NOT NULL
);
```

### change the data

Insert a row into the table

```sql
INSERT INTO t(column_list)
VALUES(value_list);
```

Insert multiple rows into table

```sql
INSERT INTO t(column_list)
VALUES (value_list),
       (value_list), …;
```

Insert rows from t2 into t1

```sql
INSERT INTO t1(column_list)
SELECT column_list
FROM t2;
```

Update all rows in column c1 with new values

```sql
UPDATEt
SET c1 = new_value;
```

Update the values ​​in columns c1 and c2 that match the condition

```sql
UPDATEt
SET c1 = new_value,
        c2 = new_value
WHERE condition;
```

Delete all data in table

```sql
DELETE FROM t;
```

Delete a subset of rows in a table

```sql
DELETE FROM t
WHERE condition;
```

### Management view
<!--rehype:wrap-class=row-span-2-->

Create a new view consisting of c1 and c2

```sql
CREATE VIEW v(c1,c2)
AS
SELECT c1, c2
FROM t;
```

Create a new view with selected options

```sql
CREATE VIEW v(c1,c2)
AS
SELECT c1, c2
FROM t;
WITH [CASCADED | LOCAL] CHECK OPTION;
```

Create a recursive view

```sql
CREATE RECURSIVE VIEW v
AS
select-statement -- anchor part
UNION [ALL]
select-statement; -- recursive part
```

Create temporary view

```sql
CREATE TEMPORARY VIEW v
AS
SELECT c1, c2
FROM t;
```

Delete view

```sql
DROP VIEW view_name;
```

### Manage triggers

Create or modify a trigger

```sql
CREATE OR MODIFY TRIGGER trigger_name
WHEN EVENT
ON table_name TRIGGER_TYPE
EXECUTE stored_procedure;
```

####WHEN

:-|:-
:-|:-
`BEFORE` | Called before the event occurs
`AFTER` | Called after the event occurs

#### EVENT

:-|:-
:-|:-
`INSERT` | Called for INSERT
`UPDATE` | Call UPDATE
`DELETE` | Call DELETE

####TRIGGER_TYPE

:-|:-
:-|:-
`FOR EACH ROW` | -
`FOR EACH STATEMENT` | -

### Manage index

Create indexes on c1 and c2 of t table

```sql
CREATE INDEX idx_name
ON t(c1,c2);
```

Create unique indexes on c3 and c4 of the t table

```sql
CREATE UNIQUE INDEX idx_name
ON t(c3,c4)
```

Delete index

```sql
DROP INDEX idx_name;
```

MySQL data types
----------

### Strings

| - | - |
|-------------|--------------------------------|
| `CHAR` | String (0 - 255) |
| `VARCHAR` | String (0 - 255) |
| `TINYTEXT` | String (0 - 255) |
| `TEXT` | String (0 - 65535) |
| `BLOB` | String (0 - 65535) |
| `MEDIUMTEXT` | String (0 - 16777215) |
| `MEDIUMBLOB` | String (0 - 16777215) |
| `LONGTEXT` | String (0 - 4294967295) |
| `LONGBLOB` | String (0 - 4294967295) |
| `ENUM` | One of preset options |
| `SET` | Selection of preset options |

### Date & time

| Data Type | Format |
|-------------|------------------------|
| `DATE` | yyyy-MM-dd |
| `TIME` | hh:mm:ss |
| `DATETIME` | yyyy-MM-dd hh:mm:ss |
| `TIMESTAMP` | yyyy-MM-dd hh:mm:ss |
| `YEAR` | yyyy |

### Numeric

| - | - |
|------------------|---------------------------------- ----------------------------------|
| `TINYINT x` | Integer (-128 to 127) |
| `SMALLINT x` | Integer (-32768 to 32767) |
| `MEDIUMINT x` | Integer (-8388608 to 8388607) |
| `INT x` | Integer (-2147483648 to 2147483647) |
| `BIGINT x` | Integer (-9223372036854775808 to 9223372036854775807) |
| `FLOAT` | Decimal (precise to 23 digits) |
| `DOUBLE` | Decimal (24 to 53 digits) |
| `DECIMAL` | "DOUBLE" stored as string |

See also
---

- [SQL basic tutorial](http://www.w3school.com.cn/sql/index.asp) _(w3school.com.cn)_
- [SQL statement tutorial](http://www.1keydata.com/cn/sql/sql-count.php) _(1keydata.com)_
- [21 Minutes MySQL Basic Entry](https://jaywcjlove.github.io/mysql-tutorial/21-minutes-MySQL-basic-entry.html) _(jaywcjlove.github.io)_
