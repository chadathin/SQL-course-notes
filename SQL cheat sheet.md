# SQL Cheat Sheet <!-- omit from toc -->

## Table of Contents<!-- omit from toc -->
- [__Utility commands__](#utility-commands)
  - [Viewing all databases](#viewing-all-databases)
  - [Changing which database you're using](#changing-which-database-youre-using)
  - [Viewing all tables in current database](#viewing-all-tables-in-current-database)
  - [Viewing a specific table](#viewing-a-specific-table)
  - [Viewing values in a table](#viewing-values-in-a-table)
- [__Databases__](#databases)
  - [Creating Databases](#creating-databases)
  - [Deleting (dropping) a database](#deleting-dropping-a-database)
- [__Tables__](#tables)
  - [Data types](#data-types)
    - [Integer](#integer)
    - [Fixed Point / Exact (`DECIMAL` and `NUMERIC`)](#fixed-point--exact-decimal-and-numeric)
    - [Floating Point / Approximate (`FLOAT` and `DOUBLE`)](#floating-point--approximate-float-and-double)
    - [CHAR and VARCHAR (Strings)](#char-and-varchar-strings)
    - [DATE, DATETIME and TIMESTAMP](#date-datetime-and-timestamp)
  - [Creating a simple table](#creating-a-simple-table)
- [Constraints, Keys and Default Values](#constraints-keys-and-default-values)
  - [Constraints](#constraints)
  - [Primary Keys](#primary-keys)
  - [Default values](#default-values)
  - [Deleting (dropping) a table](#deleting-dropping-a-table)
  - [Basic CRUD Operations (Create, Read, Update, Delete)](#basic-crud-operations-create-read-update-delete)
    - [Create](#create)
    - [Read](#read)
      - [Aliasing](#aliasing)
    - [Update](#update)
    - [Delete](#delete)
- [String Functions](#string-functions)
  - [`CONCAT()`](#concat)
  - [`SUBSTRING()` and `SUBSTR()` (synonymous)](#substring-and-substr-synonymous)
  - [`REPLACE()`](#replace)
  - [`REVERSE()`](#reverse)
  - [`CHAR_LENGTH()`](#char_length)
  - [`UPPER()` and `LOWER()` (or `UCASE` and `LCASE()`)](#upper-and-lower-or-ucase-and-lcase)
  - [`INSERT()`](#insert)
  - [`LEFT(str, n)` and `RIGHT(str, n)`](#leftstr-n-and-rightstr-n)
  - [`REPEAT(str, n)`](#repeatstr-n)
  - [`TRIM(BOTH | LEADING | TRAILING substr FROM str)`](#trimboth--leading--trailing-substr-from-str)
- [Refining Results](#refining-results)
    - [`DISTINCT`](#distinct)
  - [Sorting](#sorting)
    - [`ORDER BY`](#order-by)
    - [`LIMIT`](#limit)
    - [`LIKE` (for basic searching)](#like-for-basic-searching)
- [Aggregate Functions](#aggregate-functions)
    - [`COUNT()`](#count)
    - [`GROUP BY`](#group-by)
    - [`MIN()` and `MAX()`](#min-and-max)
    - [`MIN()` and `MAX()` with `GROUP BY`](#min-and-max-with-group-by)
    - [`SUM(col)`](#sumcol)
    - [`AVG()`](#avg)
- [`DATE`, `TIME`, and `DATETIME` data types](#date-time-and-datetime-data-types)
    - [`DATE` datatype](#date-datatype)
    - [`TIME`](#time)
    - [`DATETIME` datatype](#datetime-datatype)
    - [`TIMESTAMP` datatype](#timestamp-datatype)
    - [`CURDATE ()`, `CURTIME()`, `NOW()` functions](#curdate--curtime-now-functions)
  - [COMPARING DATES](#comparing-dates)
- [`IN()` Operator](#in-operator)
- [`CASE` statements](#case-statements)
- [Named constraints](#named-constraints)
- [`BETWEEN` operator](#between-operator)
    - [MySQL Docs](#mysql-docs)
- [`IN()` Operator](#in-operator-1)
- [`CASE` statements](#case-statements-1)
- [Named constraints](#named-constraints-1)
- [Multi-Column Checks](#multi-column-checks)
- [`ALTER TABLE`](#alter-table)
    - [To add a column](#to-add-a-column)
    - [To drop a column](#to-drop-a-column)
    - [To rename a table](#to-rename-a-table)
    - [BUT can also use `RENAME`](#but-can-also-use-rename)
    - [To rename a column](#to-rename-a-column)
    - [To modify a data type](#to-modify-a-data-type)
    - [Change an entire column](#change-an-entire-column)
    - [Add/Remove constraints](#addremove-constraints)
- [`PRIMATY KEY` \& `FOREIGN KEY`](#primaty-key--foreign-key)
- [`JOINS`](#joins)
    - [`INNER JOIN` (or just `JOIN`)](#inner-join-or-just-join)
    - [`LEFT JOIN`](#left-join)
    - [`RIGHT JOIN`](#right-join)
- [Views](#views)
- [WINDOW FUNCTIONS!](#window-functions)
    - [`OVER()`](#over)
    - [`PARTITION BY <col_name>`](#partition-by-col_name)
    - [`ORDER BY` in `OVER()`](#order-by-in-over)
- [RANK()](#rank)



## __Utility commands__
### Viewing all databases
```sql
SHOW DATABASES;
```
### *Sample output* <!-- omit from toc -->
```sql
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| pet_shop           |
| sys                |
+--------------------+
```
***
### Changing which database you're using
```sql
USE <db_name>;
```
### *Example* <!-- omit from toc -->
```sql
USE pet_shop;
```
### *Sample output* <!-- omit from toc -->
```
Database changed
```
***
### Viewing all tables in current database
```sql
SHOW TABLES;
```
### *Sample output* <!-- omit from toc -->
```sql
+--------------------+
| Tables_in_pet_shop |
+--------------------+
| cats               |
| cats2              |
| dogs               |
| quotes             |
+--------------------+
```

***

### Viewing a specific table
```sql
DESC <table_name>;
```
### *Example* <!-- omit from toc -->

```sql
DESC dogs;
```
### *Sample output* <!-- omit from toc -->
```sql
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| dogID | int         | NO   | PRI | NULL    | auto_increment |
| name  | varchar(50) | YES  |     | NULL    |                |
| breed | varchar(50) | YES  |     | NULL    |                |
| age   | int         | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
```
***
### Viewing values in a table
```sql
SELECT * FROM <table_name>;
```

### *Example* <!-- omit from toc -->
```sql
SELECT * FROM cats;
```

### *Sample output* <!-- omit from toc -->
```sql
+-------+-------------+------+
| catID | name        | age  |
+-------+-------------+------+
|     1 | Todd        | NULL |
|     2 | Blue Steele |    5 |
|     3 | Jenkins     |    7 |
|     4 | Beth        |    2 |
|     5 | Meatball    |    5 |
|     6 | Turkey      |    1 |
|     7 | Potato Face |   15 |
+-------+-------------+------+
```
***

## __Databases__

### Creating Databases
```sql
CREATE DATABASE <db_name>;
```

### *Before* <!-- omit from toc -->
```sql
SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| pet_shop           |
| sys                |
+--------------------+
```
### *Example* <!-- omit from toc -->
```sql
CREATE DATABASE runs;
```

### *After* <!-- omit from toc -->
```sql
SHOW DATABSES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| pet_shop           |
| runs               |
| sys                |
+--------------------+
```

***
### Deleting (dropping) a database
```sql
DROP DATABASE <db_name>;
```

### *Before* <!-- omit from toc -->
```sql
SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| pet_shop           |
| runs               |
| sys                |
+--------------------+
```
### *Example* <!-- omit from toc -->
```sql
DROP DATABASE runs;
```

### *After* <!-- omit from toc -->
```sql
SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| pet_shop           |
| sys                |
+--------------------+
```

***
## __Tables__

### Data types
Before diving into the creation of tables, we need a brief overview of data types.

When creating a table, one will need to define a data type for each column in their table. For instance, if one has a column `age` they may want to store a whole number in that column, and therefore would need to declare it to store an `INT`.

Below are some of the more common datatypes one will use (integer, fixed point, float/double, characters and datetime).
***
#### Integer
|Type       |Size (bytes)   |Min Signed         |Max Signed             |Min Unsigned   |Max Unsigned           |
|:---------:|:----------:   |:--------:         |:--------:             |:----------:   |:----------:           |
|SMALLINT   |   2           |   -32768          |   32767               |   0           |   65535               |
|INT        |   4           |   -2147483648     |   2147483647          |   0           |   4294967295          |
|BIGINT     |   8           |   -2<sup>63</sup> |   2<sup>63</sup>-1    |   0           |   2<sup>64</sup>-1    |

***

#### Fixed Point / Exact (`DECIMAL` and `NUMERIC`)
From [MySQL Fixed Point doc](https://dev.mysql.com/doc/refman/8.0/en/fixed-point-types.html): The DECIMAL and NUMERIC types store exact numeric data values. These types are used when it is important to preserve exact precision, for example with monetary data. In MySQL, `NUMERIC` is implemented as `DECIMAL`, so the following remarks about `DECIMAL` apply equally to `NUMERIC`.

In a `DECIMAL` column declaration, the precision and scale can be (and usually is) specified. For example: `salary DECIMAL(5,2)`. In this example, 5 is the precision and 2 is the scale. The precision represents the number of significant digits that are stored for values, and the scale represents the number of digits that can be stored following the decimal point.

Standard SQL requires that `DECIMAL(5,2)` be able to store any value with five digits and two decimals, so values that can be stored in the salary column range from -999.99 to 999.99.

If the scale is 0, `DECIMAL` values contain no decimal point or fractional part.  

***

#### Floating Point / Approximate (`FLOAT` and `DOUBLE`)
From [MySQL Floating Point doc](https://dev.mysql.com/doc/refman/8.0/en/floating-point-types.html): The FLOAT and DOUBLE types represent approximate numeric data values. MySQL uses four bytes for single-precision values and eight bytes for double-precision values.

For `FLOAT`, the SQL standard permits an optional specification of the precision (but not the range of the exponent) in bits following the keyword `FLOAT` in parentheses, that is, `FLOAT(p)`. MySQL also supports this optional precision specification, but the precision value in `FLOAT(p)` is used only to determine storage size. 

- A precision from 0 to 23 results in a 4-byte single-precision `FLOAT` column. 

- A precision from 24 to 53 results in an 8-byte double-precision `DOUBLE` column.

Because floating-point values are __approximate__ and not stored as exact values, attempts to treat them as exact in comparisons may lead to problems. They are also subject to platform or implementation dependencies. For more information, see [Section B.3.4.8, “Problems with Floating-Point Values”](https://dev.mysql.com/doc/refman/8.0/en/problems-with-float.html).

For maximum portability, code requiring storage of approximate numeric data values should use FLOAT or DOUBLE PRECISION with no specification of precision or number of digits.

***

#### CHAR and VARCHAR (Strings)
From [MySQL CHAR doc](https://dev.mysql.com/doc/refman/8.0/en/char.html): The `CHAR` and `VARCHAR` types are similar, but differ in the way they are stored and retrieved. They also differ in maximum length and in whether trailing spaces are retained.

The `CHAR` and `VARCHAR` types are declared with a length that indicates the maximum number of characters you want to store. For example, `CHAR(30)` can hold up to 30 characters.

The length of a `CHAR` column is fixed to the length that you declare when you create the table. The length can be any value from 0 to 255. When CHAR values are stored, they are right-padded with spaces to the specified length. When `CHAR` values are retrieved, trailing spaces are removed unless the `PAD_CHAR_TO_FULL_LENGTH` SQL mode is enabled.

Values in `VARCHAR` columns are variable-length strings. The length can be specified as a value from 0 to 65,535. The effective maximum length of a `VARCHAR` is subject to the maximum row size (65,535 bytes, which is shared among all columns) and the character set used. See [Section 8.4.7, “Limits on Table Column Count and Row Size”](https://dev.mysql.com/doc/refman/8.0/en/column-count-limit.html).

The following table illustrates the differences between `CHAR` and `VARCHAR` by showing the result of storing various string values into `CHAR(4)` and `VARCHAR(4)` columns. In other words, `CHAR(4)` will always store 4 bytes. `VARCHAR(4)` will store anywhere from `1+0=1` to `1+4=5` bytes, depending on how long the input is.
|Value|	CHAR(4)|	Storage Required|	VARCHAR(4)|	Storage Required|
|:--:|:--:|:--:|:--:|:--:|
|''|'    '|	4 bytes	|''	|1 byte|
|'ab'|	'ab  '	|4 bytes	|'ab'|	3 bytes|
|'abcd'|	'abcd'|	4 bytes	|'abcd'|	5 bytes|
|'abcdefgh'|	'abcd'	|4 bytes	|'abcd'	|5 bytes|
***
#### DATE, DATETIME and TIMESTAMP
From [MySQL DATETIME doc](https://dev.mysql.com/doc/refman/8.0/en/datetime.html): The `DATE`, `DATETIME`, and `TIMESTAMP `types are related. This section describes their characteristics, how they are similar, and how they differ. MySQL recognizes `DATE`, `DATETIME`, and `TIMESTAMP` values in several formats, described in [Section 9.1.3, “Date and Time Literals”](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-literals.html). For the `DATE` and `DATETIME` range descriptions, “supported” means that although earlier values might work, there is no guarantee.

The `DATE` type is used for values with a date part but no time part. MySQL retrieves and displays DATE values in `'YYYY-MM-DD'` format. The supported range is `'1000-01-01'` to `'9999-12-31'`.

The `DATETIME` type is used for values that contain both date and time parts. MySQL retrieves and displays DATETIME values in `'YYYY-MM-DD hh:mm:ss'` format. The supported range is `'1000-01-01 00:00:00'` to `'9999-12-31 23:59:59'`.

The `TIMESTAMP` data type is used for values that contain both date and time parts. `TIMESTAMP` has a range of `'1970-01-01 00:00:01' UTC` to `'2038-01-19 03:14:07' UTC`.


***
For even __more__ information on the dataypes available, please visit the [MySQL Documentation](https://dev.mysql.com/doc/refman/8.0/en/data-types.html).

Okay, now that we have all *that* out of the way, let's move on to actually *creating* tables!
***
### Creating a simple table
```sql
CREATE TABLE <name> (
    <col1> <data_type>,
    <col2> <data_type>
);
```
### *Example* <!-- omit from toc -->
```sql
CREATE TABLE dogs (
    name VARCHAR(50),
    breed VARCHAR(50),
    age INT
);
```

```sql
DESC dogs;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| name  | varchar(50) | YES  |     | NULL    |                |
| breed | varchar(50) | YES  |     | NULL    |                |
| age   | int         | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
```

***

## Constraints, Keys and Default Values

### Constraints
Probably one of the more commonly used constraints is to prevent `NULL` values. We can do this by simply using `NOT NULL` when creating a table. For example, if we peek at our `shops` table:

```sql
DESC shops;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| name  | varchar(100) | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
```
We can see the `NULL` column is `YES`, meaning it *allows* `NULL` values.

BUT, if we create a table called `runs` and prevent `NULL`:

```sql
CREATE TABLE runs (
    location VARCHAR(100) NOT NULL,
    distance FLOAT NOT NULL
    );
```
Then take a peek:
```sql
DESC runs;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| location | varchar(100) | NO   |     | NULL    |       |
| distance | float        | NO   |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+
```
We can see `NULL` is set to `NO`, meaning `NULL` is not allowed. If we try to add a record with `NULL` we get an error:

```sql
INSERT INTO runs (location, distance) VALUES (NULL, 3.1);

ERROR 1048 (23000): Column 'location' cannot be null
```
But if we provide values for both columns, it's a success:

```sql
INSERT INTO runs (location, distance) VALUES ('Chicago', 3.1);

SELECT * FROM runs;
+----------+----------+
| location | distance |
+----------+----------+
| Chicago  |      3.1 |
+----------+----------+

```
***
### Primary Keys
A Primary Key is a unique identifier for a record (row) in a table. We'll talk more about Primary and Foreign Keys later. The main thing to cover right now is how to define Primary keys. This can be done with the `PRIMARY KEY` constraint and another special constraint; `AUTO_INCREMENT`. This will automatically increment the value of the column whenever a record is added.

So, putting this all together, we can create a table named `cars` with a `PRIMARY KEY` of `carID`:

```sql
CREATE TABLE cars (
    carID INT AUTO_INCREMENT,
    brand VARCHAR(50),
    gas_mileage INT,
    PRIMARY KEY(carID)
  );
```
[Note]: When defining a `PRIMARY KEY`, stating `NOT NULL` is a bit redundant. `PRIMARY KEY`s *can not* be `NULL`.

And take a peek:
```sql
DESC cars;
+-------------+-------------+------+-----+---------+----------------+
| Field       | Type        | Null | Key | Default | Extra          |
+-------------+-------------+------+-----+---------+----------------+
| carID       | int         | NO   | PRI | NULL    | auto_increment |
| brand       | varchar(50) | YES  |     | NULL    |                |
| gas_mileage | int         | YES  |     | NULL    |                |
+-------------+-------------+------+-----+---------+----------------+
```

Now, if we add a few vehicles:
```sql
INSERT INTO cars (brand, gas_mileage) VALUES
    ("Chevrolet", 25),
    ("Toyota", 35),
    ("Ford", 8),
    ("Honda", 32);
```

And take a peek:
```sql
SELECT * FROM cars;
+-------+-----------+-------------+
| carID | brand     | gas_mileage |
+-------+-----------+-------------+
|     1 | Chevrolet |          25 |
|     2 | Toyota    |          35 |
|     3 | Ford      |           8 |
|     4 | Honda     |          32 |
+-------+-----------+-------------+
```

We can see the `PRIMARY KEY`, `carID`, automatically incremented itself each time a vehicle was added!

***
### Default values
To insert a default value, we can use `DEFAULT` and specify our default value. For example:
```sql
CREATE TABLE shoes 
  (
    brand VARCHAR(100) DEFAULT 'unnamed',
    size INT DEFAULT -1
  );
```

Now if we take a peek at our table:
```sql
DESC shoes;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| brand | varchar(100) | YES  |     | unnamed |       |
| size  | int          | YES  |     | -1      |       |
+-------+--------------+------+-----+---------+-------+
```


Or, if we insert a shoe with a `brand`, but no `size` it will enter `-1` for a size by default.
```sql
INSERT INTO shoes (brand) VALUES ('Saucony');

SELECT * FROM shoes;
+---------+------+
| brand   | size |
+---------+------+
| Saucony |   -1 |
+---------+------+
```

Similar, if we  add an entry without a `brand`.
```sql
INSERT INTO shoes (size) VALUES (12);

SELECT * FROM shoes;
+---------+------+
| brand   | size |
+---------+------+
| Saucony |   -1 |
| unnamed |   12 |
+---------+------+
```

***

### Deleting (dropping) a table
```sql
DROP TABLE <table_name>;
```

### *Example* <!-- omit from toc -->
```sql
DROP TABLE quotes;
```

### *Before* <!-- omit from toc -->
```sql
SHOW TABLES;
+--------------------+
| Tables_in_pet_shop |
+--------------------+
| cats               |
| cats2              |
| dogs               |
| quotes             |
+--------------------+
```

### *After* <!-- omit from toc -->
```sql
SHOW TABLES;
+--------------------+
| Tables_in_pet_shop |
+--------------------+
| cats               |
| cats2              |
| dogs               |
+--------------------+
```
***

### Basic CRUD Operations (Create, Read, Update, Delete)

#### Create
When we say "Create" we mean create a record. In other words, we want to `INSERT` into our table.
```sql
INSERT INTO <table_name> (<col1>, <col2>,...)
VALUES (<val1>,<val2>,...);
```
The values you are inserting must match the data types of the columns you're inserting into. For example, if we take a look at the `cats2` database:

```sql
DESC cats2;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| name  | varchar(50) | NO   |     | NULL    |       |
| age   | int         | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
```
The `name` field requires a string (no more than 50 characters long) and the `age` field requires an integer. So, we can add a cat like this:

```sql
INSERT INTO cats2 (name, age)
VALUES ('Willy', 3)
```

### *Before* <!-- omit from toc -->
```sql
SELECT * FROM cats2;
+-------+-----+
| name  | age |
+-------+-----+
| Bilbo |  19 |
+-------+-----+
```

### *After* <!-- omit from toc -->
```sql
SELECT * FROM cats2;
+-------+-----+
| name  | age |
+-------+-----+
| Bilbo |  19 |
| Willy |   3 |
+-------+-----+
```

If we try to add a type that doesn't match, we get an error:
```sql
INSERT INTO cats2 (name, age)
VALUES ('Boots', 'five');

ERROR 1366 (HY000): Incorrect integer value: 'five' for column 'age' at row 1
```
***
#### Read
This is kind of the big one. The main reason anyone uses SQL; to read information. In order to do so, we're going to `SELECT ` from tables. This will get a lot more complicated later, but for now, we're going to cover selection of all columns, specific columns, and filtering by values.

You've already seen how to select all items:
```sql
SELECT * FROM <table_name>;
```

For instance, if we look at all values in the original `cats` table (not `cats2`):

```sql
SELECT * from cats;
+-------+-------------+------+
| catID | name        | age  |
+-------+-------------+------+
|     1 | Todd        | NULL |
|     2 | Blue Steele |    5 |
|     3 | Jenkins     |    7 |
|     4 | Beth        |    2 |
|     5 | Meatball    |    5 |
|     6 | Turkey      |    1 |
|     7 | Potato Face |   15 |
+-------+-------------+------+
```
Don't worry about `catID` quite yet, we'll get to that in the Constraints and Keys section.

Now, if we want to do some filtering, we can use the `WHERE` clause:

```sql
SELECT * FROM <table_name> WHERE <condition>;
```

For instance, if we want to see all cats older than (or equal to) 5 years old:

```sql
SELECT * FROM cats WHERE age >= 5;
+-------+-------------+------+
| catID | name        | age  |
+-------+-------------+------+
|     2 | Blue Steele |    5 |
|     3 | Jenkins     |    7 |
|     5 | Meatball    |    5 |
|     7 | Potato Face |   15 |
+-------+-------------+------+
```

Or maybe we want to see all cats whose name starts with a 'B':

(More on [string comparisons and pattern matching here](https://dev.mysql.com/doc/refman/8.0/en/string-comparison-functions.html).)
```sql
SELECT * FROM cats WHERE name LIKE "B%";
+-------+-------------+------+
| catID | name        | age  |
+-------+-------------+------+
|     2 | Blue Steele |    5 |
|     4 | Beth        |    2 |
+-------+-------------+------+
```
Now, `*` allows us to select all columns, but we *can* select __specific__ columns using `SELECT`:
```sql
SELECT <co1>, <col2>, ... from <table_name>;
```

For instance, if we don't care about the `catID` we can just `SELECT` like this:

```sql
SELECT name, age FROM cats;
+-------------+------+
| name        | age  |
+-------------+------+
| Todd        | NULL |
| Blue Steele |    5 |
| Jenkins     |    7 |
| Beth        |    2 |
| Meatball    |    5 |
| Turkey      |    1 |
| Potato Face |   15 |
+-------------+------+
```

Or, we can combine our specific columns with our `WHERE` clause. For example, if we only want the `name` and `catID` of all cats five years of age or older.

```sql
SELECT catID, name FROM cats WHERE age >=5;
+-------+-------------+
| catID | name        |
+-------+-------------+
|     2 | Blue Steele |
|     3 | Jenkins     |
|     5 | Meatball    |
|     7 | Potato Face |
+-------+-------------+
```

Or, maybe we want the `name` and `age` of all cats we have an 'e' as the second letter of their name:

```sql
SELECT name, age FROM cats WHERE name LIKE "_e%";
+----------+------+
| name     | age  |
+----------+------+
| Jenkins  |    7 |
| Beth     |    2 |
| Meatball |    5 |
+----------+------+
```
##### Aliasing
If a column name is too long, or cumbersome to type every time, we can use the `AS` clause to create an alias and make that column name easier to work with. For instance, if we peek at the `employees` table:

```sql
SELECT * FROM employees;
+----+-----------+------------+-------------+-----+----------------+
| id | last_name | first_name | middle_name | age | current_status |
+----+-----------+------------+-------------+-----+----------------+
|  1 | Doe       | Jon        | NULL        |  40 | employed       |
|  2 | Wolinsky  | Mike       | NULL        |  55 | employed       |
|  3 | E         | WALL       | NULL        | 215 | employed       |
+----+-----------+------------+-------------+-----+----------------+
```

Maybe we decide `last_name` is a little annoying to have to type every time, but we still want to select it. We can use an alias like this:

```sql
SELECT last_name AS lname, age FROM employees;
+----------+-----+
| lname    | age |
+----------+-----+
| Doe      |  40 |
| Wolinsky |  55 |
| E        | 215 |
+----------+-----+
```
Notice the resultant `last_name` column is returned as `lname`, but rest assured the original column is still named `last_name` in the table.

Again, we will cover more in the Advanced CRUD section. But this will suffice, for now. 
***
#### Update
```sql
UPDATE <table_name> SET <col> = <new_value> WHERE <condition>;
```

For example, in our `employees` table:

```sql
SELECT * FROM employees;
+----+-----------+------------+-------------+-----+----------------+
| id | last_name | first_name | middle_name | age | current_status |
+----+-----------+------------+-------------+-----+----------------+
|  1 | Doe       | Jon        | NULL        |  40 | employed       |
|  2 | Wolinsky  | Mike       | NULL        |  55 | employed       |
|  3 | E         | WALL       | NULL        | 215 | employed       |
+----+-----------+------------+-------------+-----+----------------+
```
If we want to update Mike Wolinsky's age, we could so so like this:

```sql
UPDATE employees SET age = 56 WHERE last_name = 'Wolinsky';

Query OK, 1 row affected (0.00 sec)

Rows matched: 1  Changed: 1  Warnings: 0
```
Now we have:
```sql
SELECT * FROM employees;
+----+-----------+------------+-------------+-----+----------------+
| id | last_name | first_name | middle_name | age | current_status |
+----+-----------+------------+-------------+-----+----------------+
|  1 | Doe       | Jon        | NULL        |  40 | employed       |
|  2 | Wolinsky  | Mike       | NULL        |  56 | employed       |
|  3 | E         | WALL       | NULL        | 215 | employed       |
+----+-----------+------------+-------------+-----+----------------+
```
***

We DO have to be careful to include some kind of filtering or `WHERE` clause. Using `UPDATE` without it (like this):

```sql
UPDATE employees SET age=56;
```
*is* valid and will not throw an error. BUT, will update the `age` of ALL rows to reflect the new value.

To update multiple columns at once, we can use:
```sql
UPDATE <table_name> SET col1=val1, col2=val2, ... WHERE <condition>;
```

For example, if we needed to lay off Jon:
```sql
UPDATE employees SET current_status='laid off', last_name = 'gone' WHERE id=1;
```
Gives us
```sql
SELECT * FROM employees;
+----+-----------+------------+-------------+-----+----------------+
| id | last_name | first_name | middle_name | age | current_status |
+----+-----------+------------+-------------+-----+----------------+
|  1 | gone      | Jon        | NULL        |  40 | laid off       |
|  2 | Wolinsky  | Mike       | NULL        |  56 | employed       |
|  3 | E         | WALL       | NULL        | 215 | employed       |
+----+-----------+------------+-------------+-----+----------------+
```
Or if WALL E suffered a mechanical failure:
```sql
UPDATE employees SET current_status='in shop' WHERE id=3;
```
```sql
SELECT * FROM employees;
+----+-----------+------------+-------------+-----+----------------+
| id | last_name | first_name | middle_name | age | current_status |
+----+-----------+------------+-------------+-----+----------------+
|  1 | gone      | Jon        | NULL        |  40 | laid off       |
|  2 | Wolinsky  | Mike       | NULL        |  56 | employed       |
|  3 | E         | WALL       | NULL        | 215 | in shop        |
+----+-----------+------------+-------------+-----+----------------+
```
#### Delete
```sql
DELETE FROM <table_name> WHERE <condition>;
```
For example, WALL E is beyond repair and we have to scrap him:
```sql
DELETE FROM employees WHERE id = 3;
```
```sql
SELECT * FROM employees;
+----+-----------+------------+-------------+-----+----------------+
| id | last_name | first_name | middle_name | age | current_status |
+----+-----------+------------+-------------+-----+----------------+
|  1 | gone      | Jon        | NULL        |  40 | laid off       |
|  2 | Wolinsky  | Mike       | NULL        |  56 | employed       |
+----+-----------+------------+-------------+-----+----------------+
```
***
## String Functions
[MySQL String docs](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html)

### `CONCAT()`
```sql
SELECT CONCAT(str1, str2, str3) from <table_name>;

-> "str1str2str3"
```
Can concatenate values from columns
```sql
SELECT CONCAT(author_fname, ' ', author_lname) FROM books;

+-----------------------------------------+
| CONCAT(author_fname, ' ', author_lname) |
+-----------------------------------------+
| Jhumpa Lahiri                           |
| Neil Gaiman                             |
| Neil Gaiman                             |
| Jhumpa Lahiri                           |
| Dave Eggers                             |
| Dave Eggers                             |
| Michael Chabon                          |
| Patti Smith                             |
| Dave Eggers                             |
| Neil Gaiman                             |
| Raymond Carver                          |
| Raymond Carver                          |
| Don DeLillo                             |
| John Steinbeck                          |
| David Foster Wallace                    |
| David Foster Wallace                    |
+-----------------------------------------+
```
Can also use aliasing to make the column title a bit more palatable

```sql
SELECT CONCAT(author_fname, ' ', author_lname) AS Author FROM books;
+----------------------+
| Author               |
+----------------------+
| Jhumpa Lahiri        |
| Neil Gaiman          |
| Neil Gaiman          |
| Jhumpa Lahiri        |
| Dave Eggers          |
| Dave Eggers          |
| Michael Chabon       |
| Patti Smith          |
| Dave Eggers          |
| Neil Gaiman          |
| Raymond Carver       |
| Raymond Carver       |
| Don DeLillo          |
| John Steinbeck       |
| David Foster Wallace |
| David Foster Wallace |
+----------------------+
```
AND we can eliminate duplicates with `GROUP BY`:

```sql
SELECT CONCAT(author_fname, ' ', author_lname) AS Author FROM books GROUP BY Author;
+----------------------+
| Author               |
+----------------------+
| Jhumpa Lahiri        |
| Neil Gaiman          |
| Dave Eggers          |
| Michael Chabon       |
| Patti Smith          |
| Raymond Carver       |
| Don DeLillo          |
| John Steinbeck       |
| David Foster Wallace |
+----------------------+
```
Much cleaner.

Speaking of "cleaner", there is an additional concatenation function which might make that query just a *little* cleaner: `CONCAT_WS` or 'concat with separator.
```sql
SELECT CONCAT_WS(sep, str1, str2, ...) from <table_name>;
```
This will add the given separator `sep` between each string.
```sql
SELECT CONCAT_WS(' ', author_fname, author_lname) AS Author FROM books GROUP BY Author;
+----------------------+
| Author               |
+----------------------+
| Jhumpa Lahiri        |
| Neil Gaiman          |
| Dave Eggers          |
| Michael Chabon       |
| Patti Smith          |
| Raymond Carver       |
| Don DeLillo          |
| John Steinbeck       |
| David Foster Wallace |
+----------------------+
```

### `SUBSTRING()` and `SUBSTR()` (synonymous)

```sql
SELECT SUBSTRING(str, start, length);
```
Where start is the starting letter (1-indexed) and length is the length of the resultant string.

For example:
```sql 
SELECT SUBSTRING("Hello, world!",2,4);
+--------------------------------+
| SUBSTRING("Hello, world!",2,4) |
+--------------------------------+
| ello                           |
+--------------------------------+
```
We start at the 2<sup>nd</sup> letter (`e`), and we want the result to be four characters long. 

### `REPLACE()`
```sql
SELECT REPLACE(str, substr_to_replace, what_to_replace_with)
```

```sql
SELECT REPLACE('I want a job', 'want', 'need');
-> I need a job
```
Doesn't actually alter table. So we can run...
```sql
SELECT REPLACE(title, ' ', '-') FROM books;
+-----------------------------------------------------+
| REPLACE(title, ' ', '-')                            |
+-----------------------------------------------------+
| The-Namesake                                        |
| Norse-Mythology                                     |
| American-Gods                                       |
| Interpreter-of-Maladies                             |
| A-Hologram-for-the-King:-A-Novel                    |
| The-Circle                                          |
| The-Amazing-Adventures-of-Kavalier-&-Clay           |
| Just-Kids                                           |
| A-Heartbreaking-Work-of-Staggering-Genius           |
| Coraline                                            |
| What-We-Talk-About-When-We-Talk-About-Love:-Stories |
| Where-I'm-Calling-From:-Selected-Stories            |
| White-Noise                                         |
| Cannery-Row                                         |
| Oblivion:-Stories                                   |
| Consider-the-Lobster                                |
+-----------------------------------------------------+
```
BUT....
```sql
SELECT title FROM books;
+-----------------------------------------------------+
| title                                               |
+-----------------------------------------------------+
| The Namesake                                        |
| Norse Mythology                                     |
| American Gods                                       |
| Interpreter of Maladies                             |
| A Hologram for the King: A Novel                    |
| The Circle                                          |
| The Amazing Adventures of Kavalier & Clay           |
| Just Kids                                           |
| A Heartbreaking Work of Staggering Genius           |
| Coraline                                            |
| What We Talk About When We Talk About Love: Stories |
| Where I'm Calling From: Selected Stories            |
| White Noise                                         |
| Cannery Row                                         |
| Oblivion: Stories                                   |
| Consider the Lobster                                |
+-----------------------------------------------------+
```

### `REVERSE()`
Just reverses the string given to it.
```sql
SELECT REVERSE('REVERSE ME');
+-----------------------+
| REVERSE('REVERSE ME') |
+-----------------------+
| EM ESREVER            |
+-----------------------+
```

### `CHAR_LENGTH()`
Gives the length of the string as a number of chars
```sql
SELECT author_lname, CHAR_LENGTH(author_lname) FROM books;
+----------------+---------------------------+
| author_lname   | CHAR_LENGTH(author_lname) |
+----------------+---------------------------+
| Lahiri         |                         6 |
| Gaiman         |                         6 |
| Gaiman         |                         6 |
| Lahiri         |                         6 |
| Eggers         |                         6 |
| Eggers         |                         6 |
| Chabon         |                         6 |
| Smith          |                         5 |
| Eggers         |                         6 |
| Gaiman         |                         6 |
| Carver         |                         6 |
| Carver         |                         6 |
| DeLillo        |                         7 |
| Steinbeck      |                         9 |
| Foster Wallace |                        14 |
| Foster Wallace |                        14 |
+----------------+---------------------------+
```

### `UPPER()` and `LOWER()` (or `UCASE` and `LCASE()`)
Makes all letters upper-case or lower-case
```sql
SELECT 
  author_lname AS Author, 
  UPPER(author_lname) AS Upper_Case, 
  LOWER(author_lname) AS Lower_Case 
FROM 
  books 
GROUP BY 
  Author;
+----------------+----------------+----------------+
| Author         | Upper_Case     | Lower_Case     |
+----------------+----------------+----------------+
| Lahiri         | LAHIRI         | lahiri         |
| Gaiman         | GAIMAN         | gaiman         |
| Eggers         | EGGERS         | eggers         |
| Chabon         | CHABON         | chabon         |
| Smith          | SMITH          | smith          |
| Carver         | CARVER         | carver         |
| DeLillo        | DELILLO        | delillo        |
| Steinbeck      | STEINBECK      | steinbeck      |
| Foster Wallace | FOSTER WALLACE | foster wallace |
+----------------+----------------+----------------+
```
### `INSERT()`
`INSERT(str, pos, num_replace, str_to_insert)`
```sql
SELECT INSERT("Hello Bobby", 6, 0, " there");
+---------------------------------------+
| INSERT("Hello Bobby", 6, 0, " there") |
+---------------------------------------+
| Hello there Bobby                     |
+---------------------------------------+
```
In other words, start at the 6<sup>th</sup> letter (space, in this case), replace zero letters, insert ' there'. Or:
```sql
SELECT INSERT("Hello Bobby", 6, 6, " there ");
+----------------------------------------+
| INSERT("Hello Bobby", 6, 6, " there ") |
+----------------------------------------+
| Hello there                            |
+----------------------------------------+
```
In other words, start at the 6<sup>th</sup> letter (space, in this case), replace six letters (space and the entire word ' Bobby'), insert ' there '.

### `LEFT(str, n)` and `RIGHT(str, n)`
returns the n left-most and n right-most letters of str
```sql
SELECT LEFT("sentence", 3), RIGHT("sentence", 3);
+---------------------+----------------------+
| LEFT("sentence", 3) | RIGHT("sentence", 3) |
+---------------------+----------------------+
| sen                 | nce                  |
+---------------------+----------------------+
```

### `REPEAT(str, n)`
Repeats str, n times.
```sql
SELECT REPEAT('ha', 3);
+-----------------+
| REPEAT('ha', 3) |
+-----------------+
| hahaha          |
+-----------------+
```

### `TRIM(BOTH | LEADING | TRAILING substr FROM str)`

Removes either both, the leading, or the trailing substr from str. Will trim leading and trailing spaces by default.
```sql
SELECT 
  TRIM(LEADING "x" FROM 'xxxfooxxx') AS front, 
  TRIM(TRAILING "x" FROM 'xxxfooxxx') AS back,
  TRIM(BOTH "x" FROM 'xxxfooxxx') AS front_and_back;
+--------+--------+----------------+
| front  | back   | front_and_back |
+--------+--------+----------------+
| fooxxx | xxxfoo | foo            |
+--------+--------+----------------+
```

## Refining Results
#### `DISTINCT`
Eliminates duplicate values
```sql
-- Without distinct
SELECT author_lname FROM books;
+----------------+
| author_lname   |
+----------------+
| Lahiri         |
| Gaiman         |
| Gaiman         |
| Lahiri         |
| Eggers         |
| Eggers         |
| Chabon         |
| Smith          |
| Eggers         |
| Gaiman         |
| Carver         |
| Carver         |
| DeLillo        |
| Steinbeck      |
| Foster Wallace |
| Foster Wallace |
| Harris         |
| Harris         |
| Saunders       |
+----------------+
```

```sql
-- WITH distinct
SELECT DISTINCT author_lname FROM books;
+----------------+
| author_lname   |
+----------------+
| Lahiri         |
| Gaiman         |
| Eggers         |
| Chabon         |
| Smith          |
| Carver         |
| DeLillo        |
| Steinbeck      |
| Foster Wallace |
| Harris         |
| Saunders       |
+----------------+
```

Can also find distinct combinations of values.
```sql
SELECT DISTINCT author_lname, author_fname FROM books;
+----------------+--------------+
| author_lname   | author_fname |
+----------------+--------------+
| Lahiri         | Jhumpa       |
| Gaiman         | Neil         |
| Eggers         | Dave         |
| Chabon         | Michael      |
| Smith          | Patti        |
| Carver         | Raymond      |
| DeLillo        | Don          |
| Steinbeck      | John         |
| Foster Wallace | David        |
| Harris         | Dan          |
| Harris         | Freida       |
| Saunders       | George       |
+----------------+--------------+
```

### Sorting
#### `ORDER BY`
```sql
SELECT <cols...> FROM <table_name> ORDER BY <some_col> `DESC | ASC`;
```
Ascending (`ASC`) is default

```sql
SELECT book_id, author_fname, author_lname FROM books ORDER BY author_lname;
+---------+--------------+----------------+
| book_id | author_fname | author_lname   |
+---------+--------------+----------------+
|      11 | Raymond      | Carver         |
|      12 | Raymond      | Carver         |
|       7 | Michael      | Chabon         |
|      13 | Don          | DeLillo        |
|       5 | Dave         | Eggers         |
|       6 | Dave         | Eggers         |
|       9 | Dave         | Eggers         |
|      15 | David        | Foster Wallace |
|      16 | David        | Foster Wallace |
|       2 | Neil         | Gaiman         |
|       3 | Neil         | Gaiman         |
|      10 | Neil         | Gaiman         |
|      17 | Dan          | Harris         |
|      18 | Freida       | Harris         |
|       1 | Jhumpa       | Lahiri         |
|       4 | Jhumpa       | Lahiri         |
|      19 | George       | Saunders       |
|       8 | Patti        | Smith          |
|      14 | John         | Steinbeck      |
+---------+--------------+----------------+
```

Can also order by a specific column by providing a numeric argument

```sql
SELECT 
  title, author_fname, author_lname 
FROM 
  books 
ORDER BY 2;
```
Orders the selection by the second column (author_fname, in this case)

Can also sort based on multiple cols. For example:
```sql
SELECT author_fname, author_lname FROM books 
ORDER BY author_lname, author_fname;
```
Will sort by `author_lname` first, *then* `author_fname`

```sql
SELECT author_lname AS name, released_year AS year, title FROM books ORDER BY name, year;
+----------------+------+-----------------------------------------------------+
| name           | year | title                                               |
+----------------+------+-----------------------------------------------------+
| Carver         | 1981 | What We Talk About When We Talk About Love: Stories |
| Carver         | 1989 | Where I'm Calling From: Selected Stories            |
| Chabon         | 2000 | The Amazing Adventures of Kavalier & Clay           |
| DeLillo        | 1985 | White Noise                                         |
| Eggers         | 2001 | A Heartbreaking Work of Staggering Genius           |
| Eggers         | 2012 | A Hologram for the King: A Novel                    |
| Eggers         | 2013 | The Circle                                          |
| Foster Wallace | 2004 | Oblivion: Stories                                   |
| Foster Wallace | 2005 | Consider the Lobster                                |
| Gaiman         | 2001 | American Gods                                       |
| Gaiman         | 2003 | Coraline                                            |
| Gaiman         | 2016 | Norse Mythology                                     |
| Harris         | 2001 | fake_book                                           |
| Harris         | 2014 | 10% Happier                                         |
| Lahiri         | 1996 | Interpreter of Maladies                             |
| Lahiri         | 2003 | The Namesake                                        |
| Saunders       | 2017 | Lincoln In The Bardo                                |
| Smith          | 2010 | Just Kids                                           |
| Steinbeck      | 1945 | Cannery Row                                         |
+----------------+------+-----------------------------------------------------+
```
Ordered by `author_lname` first, then `released_year`!

#### `LIMIT`
Limits the number of results by a given number
```sql
SELECT author_lname, released_year FROM books LIMIT 5;
+--------------+---------------+
| author_lname | released_year |
+--------------+---------------+
| Lahiri       |          2003 |
| Gaiman       |          2016 |
| Gaiman       |          2001 |
| Lahiri       |          1996 |
| Eggers       |          2012 |
+--------------+---------------+
```
Can be used in conjuntion with a sort to find the top or bottom of a list.

```sql
SELECT 
  author_lname, released_year 
FROM 
  books
ORDER BY 
  released_year 
LIMIT
  5;
+--------------+---------------+
| author_lname | released_year |
+--------------+---------------+
| Steinbeck    |          1945 |
| Carver       |          1981 |
| DeLillo      |          1985 |
| Carver       |          1989 |
| Lahiri       |          1996 |
+--------------+---------------+
```
Finds the top 5 oldest books.

```sql
SELECT 
  author_lname, released_year 
FROM 
  books 
ORDER BY 
  released_year DESC
LIMIT 
  5;
+--------------+---------------+
| author_lname | released_year |
+--------------+---------------+
| Saunders     |          2017 |
| Gaiman       |          2016 |
| Harris       |          2014 |
| Eggers       |          2013 |
| Eggers       |          2012 |
+--------------+---------------+
```
Finds the top 5 newest books!

Can also 'slice' the results by giving two arguments
```sql
 SELECT author_lname, released_year FROM books LIMIT 3,4;
+--------------+---------------+
| author_lname | released_year |
+--------------+---------------+
| Lahiri       |          1996 |
| Eggers       |          2012 |
| Eggers       |          2013 |
| Chabon       |          2000 |
+--------------+---------------+
```
`LIMIT 3,4` means "start at the 3<sup>rd</sup> value and return 4 results"

#### `LIKE` (for basic searching)

```sql
SELECT author_lname, author_fname FROM books WHERE author_fname LIKE "%da%";
+----------------+--------------+
| author_lname   | author_fname |
+----------------+--------------+
| Eggers         | Dave         |
| Eggers         | Dave         |
| Eggers         | Dave         |
| Foster Wallace | David        |
| Foster Wallace | David        |
| Harris         | Dan          |
| Harris         | Freida       |
+----------------+--------------+
```
`%` is a wildcard and can represent any character. In other words, `%da%` indicates the `da` can come anywhere in the name.

`_` is also a *kind* of wildcard. Where `%` can represent *any number of characters*, `_` represents exactly *one* character.

```sql
SELECT title FROM books WHERE title LIKE "_h%";
+-----------------------------------------------------+
| title                                               |
+-----------------------------------------------------+
| The Namesake                                        |
| The Circle                                          |
| The Amazing Adventures of Kavalier & Clay           |
| What We Talk About When We Talk About Love: Stories |
| Where I'm Calling From: Selected Stories            |
| White Noise                                         |
+-----------------------------------------------------+
```
Returns all titles that have an `h` as the second letter!

## Aggregate Functions
[MySQL Aggregate Function docs](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html)
#### `COUNT()` 
Gives the count of selected items. For example:
```sql
SELECT COUNT(DISTINCT author_fname) AS authors FROM books;
+---------+
| authors |
+---------+
|      12 |
+---------+
```
Gives the number of unique author first names.

#### `GROUP BY`
Very useful. Groups multiple identical rows into a single row.
Can use `GROUP BY` along with `COUNT()` to get useful info, like the number duplicate `author_lname`s

```sql
SELECT author_lname, COUNT(*) FROM books GROUP BY author_lname;
+----------------+----------+
| author_lname   | COUNT(*) |
+----------------+----------+
| Lahiri         |        2 |
| Gaiman         |        3 |
| Eggers         |        3 |
| Chabon         |        1 |
| Smith          |        1 |
| Carver         |        2 |
| DeLillo        |        1 |
| Steinbeck      |        1 |
| Foster Wallace |        2 |
| Harris         |        2 |
| Saunders       |        1 |
+---------------------------+
```
`COUNT(*)` counts all rows of a selection.

#### `MIN()` and `MAX()`
Returns smallest or largest values for arguments passed.
```sql
SELECT MIN(released_year) FROM books;
+--------------------+
| MIN(released_year) |
+--------------------+
|               1945 |
+--------------------+
```
Gives the oldest release year.

But what if I want to know the `title` for the oldest `released_year`? We can use a subquery.
Kind of like assigning the return of a function to a value. To find the title and length of the longest book, we can run a subquery to find the `MAX()` number of pages, then use that result to filter with `WHERE`.
```sql
SELECT title, pages FROM books WHERE pages=(SELECT MAX(pages) FROM books);
+-------------------------------------------+-------+
| title                                     | pages |
+-------------------------------------------+-------+
| The Amazing Adventures of Kavalier & Clay |   634 |
+-------------------------------------------+-------+
```

#### `MIN()` and `MAX()` with `GROUP BY`

Say we want to find the year of an author's FIRST release for each author.
- First, we can group authors by first and last name.
```sql
SELECT 
  CONCAT(author_fname, ' ', author_lname) AS author 
FROM 
  books 
GROUP BY 
  author;
+----------------------+
| author               |
+----------------------+
| Jhumpa Lahiri        |
| Neil Gaiman          |
| Dave Eggers          |
| Michael Chabon       |
| Patti Smith          |
| Raymond Carver       |
| Don DeLillo          |
| John Steinbeck       |
| David Foster Wallace |
| Dan Harris           |
| Freida Harris        |
| George Saunders      |
+----------------------+
```
- So far, so good. Now, we have 12 'subgroups' behind the scenes. When we add in a `MIN()` or a `MAX()` it will run on each subgroup.
```sql
SELECT 
  CONCAT(author_fname, ' ', author_lname) AS author, 
  MIN(released_year) AS first_release 
FROM 
  books
GROUP BY
  author;
+----------------------+---------------+
| author               | first_release |
+----------------------+---------------+
| Jhumpa Lahiri        |          1996 |
| Neil Gaiman          |          2001 |
| Dave Eggers          |          2001 |
| Michael Chabon       |          2000 |
| Patti Smith          |          2010 |
| Raymond Carver       |          1981 |
| Don DeLillo          |          1985 |
| John Steinbeck       |          1945 |
| David Foster Wallace |          2004 |
| Dan Harris           |          2014 |
| Freida Harris        |          2001 |
| George Saunders      |          2017 |
+----------------------+---------------+
```
- Or, if we wanted to add a 'latest release', we can pop that in our `SELECT` statement as well!
```sql
SELECT 
  CONCAT(author_fname, ' ', author_lname) AS author,
  MIN(released_year) AS first_release, 
  MAX(released_year) AS latest_release 
FROM 
  books 
GROUP BY 
  author;
+----------------------+---------------+----------------+
| author               | first_release | latest_release |
+----------------------+---------------+----------------+
| Jhumpa Lahiri        |          1996 |           2003 |
| Neil Gaiman          |          2001 |           2016 |
| Dave Eggers          |          2001 |           2013 |
| Michael Chabon       |          2000 |           2000 |
| Patti Smith          |          2010 |           2010 |
| Raymond Carver       |          1981 |           1989 |
| Don DeLillo          |          1985 |           1985 |
| John Steinbeck       |          1945 |           1945 |
| David Foster Wallace |          2004 |           2005 |
| Dan Harris           |          2014 |           2014 |
| Freida Harris        |          2001 |           2001 |
| George Saunders      |          2017 |           2017 |
+----------------------+---------------+----------------+
```
#### `SUM(col)`
Returns a sum of the values in given col
For example, if we want to know how many pages each author has written, we could combine `SUM()` and `GROUP BY`.
```sql
SELECT 
  CONCAT(author_fname, ' ', author_lname) AS author, 
  SUM(pages) 
FROM 
  books 
GROUP BY 
  author;
+----------------------+------------+
| author               | SUM(pages) |
+----------------------+------------+
| Jhumpa Lahiri        |        489 |
| Neil Gaiman          |        977 |
| Dave Eggers          |       1293 |
| Michael Chabon       |        634 |
| Patti Smith          |        304 |
| Raymond Carver       |        702 |
| Don DeLillo          |        320 |
| John Steinbeck       |        181 |
| David Foster Wallace |        672 |
| Dan Harris           |        256 |
| Freida Harris        |        428 |
| George Saunders      |        367 |
+----------------------+------------+
```
#### `AVG()`
Gives average of given col. Like, if we want to know the average length of each author's books.
```sql
SELECT 
  CONCAT(author_fname, ' ', author_lname) AS author, 
  AVG(pages) 
FROM 
  books 
GROUP BY 
  author;
+----------------------+------------+
| author               | AVG(pages) |
+----------------------+------------+
| Jhumpa Lahiri        |   244.5000 |
| Neil Gaiman          |   325.6667 |
| Dave Eggers          |   431.0000 |
| Michael Chabon       |   634.0000 |
| Patti Smith          |   304.0000 |
| Raymond Carver       |   351.0000 |
| Don DeLillo          |   320.0000 |
| John Steinbeck       |   181.0000 |
| David Foster Wallace |   336.0000 |
| Dan Harris           |   256.0000 |
| Freida Harris        |   428.0000 |
| George Saunders      |   367.0000 |
+----------------------+------------+
```
## `DATE`, `TIME`, and `DATETIME` data types
[MySQL `DATETIME` docs](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-types.html)

[MySQL Date and Time Functions](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)

[MySQL `DATE_FORMAT()` docs](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format)
#### `DATE` datatype
Format: `'YYYY-MM-DD'`

#### `TIME`
Format: `'HH:MM:SS'` datatype
`TIME` values may range from '-838:59:59' to '838:59:59'

#### `DATETIME` datatype
Format: `'YYYY-MM-DD HH:MM:SS'`

#### `TIMESTAMP` datatype
Gives a `DATETIME` format of the current date and time

#### `CURDATE ()`, `CURTIME()`, `NOW()` functions
- `CURDATE()` gives current date 
  - If used with a `DATETIME` fiels, will provide `TIME` as `00:00:00`
  - e.g. `'YYYY-MM-DD 00:00:00'`
- `CURTIME()` gives current time
- `NOW()` gives current `DATETIME`

### COMPARING DATES
Can use typical operators: `<, >, <=, >=, !=`

## `IN()` Operator
[MySQL `IN()` docs](https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html#operator_in)
```sql
SELECT <col(s)> FROM <table> WHERE <item> IN(<item1>, <item2>, ...);
```

```sql
SELECT title, released_year FROM books 
WHERE author_lname IN ('Carver', 'Lahiri', 'Smith');
```

## `CASE` statements
[MySQL `CASE` docs](https://dev.mysql.com/doc/refman/8.0/en/flow-control-functions.html#operator_case)

```sql
SELECT ... CASE  
  WHEN <comparison> THEN <result>
  WHEN <comparison2> THEN <result2>
  ELSE <default>
FROM books;
```

## Named constraints
```sql
CREATE TABLE entrants (
  name VARCHAR(50),
  age INT,
  CONSTRAINT min_age_check CHECK (age >= 18)
)
```

But, it may be better/more robust to `CAST` the string as a date. e.g. [MySQL `CAST()` docs](https://dev.mysql.com/doc/refman/8.0/en/cast-functions.html#function_cast)

```sql
CAST('YYYY-MM-DD' AS DATE);
-- OR
CAST('HH:MM:SS' AS TIME);
```

Can also extract certain bits of dates and times with functions such as `DAY()` or `HOUR()`. [More on MySQL date and time functions](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)

## `BETWEEN` operator
#### [MySQL Docs](https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html#operator_between)

Looks like:
```sql
...WHERE <item> BETWEEN <lo> AND <hi>;
```
`lo` and `hi` are *inclusive*
```sql
SELECT title, pages FROM books WHERE pages BETWEEN 200 AND 300;
+--------------+-------+
| title        | pages |
+--------------+-------+
| The Namesake |   291 |
| Coraline     |   208 |
| 10% Happier  |   256 |
+--------------+-------+
```
## `IN()` Operator
[MySQL docs on `IN()`](https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html#operator_in)
```sql
SELECT title, released_year FROM books 
WHERE author_lname IN ('Carver', 'Lahiri', 'Smith');
```

## `CASE` statements
[MySQL `CASE` docs](https://dev.mysql.com/doc/refman/8.0/en/flow-control-functions.html#operator_case)

```sql
SELECT ... CASE  
  WHEN <comparison> THEN <result>
  WHEN <comparison2> THEN <result2>
  ELSE <default>
  END
FROM books;
```

## Named constraints
```sql
CREATE TABLE entrants (
  name VARCHAR(50),
  age INT,
  CONSTRAINT min_age_check CHECK (age >= 18)
)
```

## Multi-Column Checks
For checking if the *combination* of two columns is unique.
For example: A `name` does not have to be unique, and a `address` does not have to be unique, but `name` AND `address` must be unique.
```sql
CREATE TABLE companies (
    supplier_id INT AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    phone VARCHAR(15) NOT NULL UNIQUE,
    address VARCHAR(255) NOT NULL,
    PRIMARY KEY (supplier_id),
    CONSTRAINT name_address UNIQUE (name , address)
);
```

## `ALTER TABLE`
[MySQL `ALTER TABLE` docs](https://dev.mysql.com/doc/refman/8.0/en/alter-table.html)

Can be used to add/delete columns, or add/remove constraints, or just generally alter the table in almost any way.

```sql
ALTER TABLE <table_name>
[Action] <value>;
```

#### To add a column
```sql
ALTER TABLE companies
ADD COLUMN city VARCHAR(50);
```

#### To drop a column
```sql
ALTER TABLE companies
DROP COLUMN employee_age;
```

#### To rename a table
```sql
ALTER TABLE company RENAME TO companies;
```

#### BUT can also use `RENAME`
```sql
RENAME TABLE <t_name> TO <new_name>;
```

#### To rename a column
```sql
ALTER TABLE companies
RENAME COLUMN <col> TO <new_col>;
```

#### To modify a data type
```sql
ALTER TABLE <table_name>
MODIFY <col> <data_type>;

-- example
ALTER TABLE companies
MODIFY name VARCHAR(100);
```

#### Change an entire column
```sql
ALTER TABLE <t_name>
CHANGE <old_col_name> <new_col_name> <new_data_type>;

-- example

ALTER TABLE companies
CHANGE name company_name VARCHAR(255);
```
#### Add/Remove constraints
```sql
ALTER TABLE people ADD CONSTRAINT CHECK (age > 18);
```

## `PRIMATY KEY` & `FOREIGN KEY`
__Primary keys__ are unique values for each row. Very useful when dealing with table that have redundant information. For example, a customer might order the same thing twice on the same day, so the quanitity, price, username, etc are all the same. BUT the primary key is different for each order. Defined when creating a table:

```sql
CREATE TABLE customers (
  id INT AUTO_INCREMENT,
  fname VARCHAR(50),
  lname VARCHAR(50),
  email VARCHAR(100)
  PRIMARY KEY(id)
);
```
__Foreign keys__ are keys in a table that reference keys in *another* table.

For example, in our customer example, we might have another table for orders, with a foreign key that references a customer id primary key.
```sql
CREATE TABLE orders (
  id INT AUTO_INCREMENT,
  order_date DATE,
  order_total DECIMAL(6,2)
  cust_id INT,
  PRIMARY KEY(id),
  FOREIGN KEY (cust_id) REFERENCES customers(id) ON DELETE CASCADE
);
```
The `ON DELETE CASCADE` ensures that if a customer is deleted, all rows in the orders table with that customer's id will also be deleted.

## `JOINS`

Using out customer tables example, if we want to do joins using our `PRIMARY KEY` from customers and `FOREIGN KEY` from orders.

```sql
SELECT 
  CONCAT(fname, ' ', lname) AS name, order_total 
FROM
  customers
JOIN orders
ON customers.id = orders.cust_id;
```

More generally
```sql
SELECT col1, col2, col3 .. 
FROM <table1>
JOIN <table2>
ON <criteria>;
```
Can also use aggregate and `GROUP BY` functions. Can even perform more than one join in a single query.

#### `INNER JOIN` (or just `JOIN`)
Joins everything from LEFT and RIGHT tables that meet criteria.

#### `LEFT JOIN`
Joins EVERYTHING from LEFT table and only those items that meet criteria from RIGHT table. If the RIGHT table is missing anything, it ends up being NULL.


#### `RIGHT JOIN`
Just like `LEFT JOIN` except, it takes everything from the RIGHT table and tries to matech from the LEFT table.



## Views
Creates a virtual table that can be stored and queried later

```sql
CREATE VIEW <view_name> AS
<QUERY_GOES_HERE>
```

For instance if we make a `VIEW` with the query
```sql
CREATE VIEW revs AS
SELECT title, rating, CONCAT(fname, ' ', lname) AS reviewer FROM series
JOIN reviews ON reviews.series_id = series.id
JOIN reviewers ON reviews.reviewer_id = reviewers.id
ORDER BY title;
```
then run `SHOW TABLES`, `revs` shows up
```sql
SHOW TABLES;

+-----------------+
| Tables_in_tv_db |
+-----------------+
| reviewers       |
| reviews         |
| revs            |
| series          |
+-----------------+
```

`revs` is a *virtual table*. It can be queried just like any other table, but doesn't *technically* exist; we haven't actually created a whole NEW table.

Also, views can only by insertable and updateable in certain situations. So we can't necessarily expect to perform CRUD operations easily in every instance. But, we *can* do stuff like:
 ```sql
SELECT reviewer, AVG(rating) AS average_rating FROM revs GROUP BY reviewer;
+-----------------+----------------+
| reviewer        | average_rating |
+-----------------+----------------+
| Thomas Stoneman |       8.020000 |
| Wyatt Skaggs    |       7.800000 |
| Kimbra Masters  |       7.988889 |
| Domingo Cortes  |       7.830000 |
| Colt Steele     |       8.770000 |
| Pinkie Petit    |       7.250000 |
+-----------------+----------------+
 ```

## WINDOW FUNCTIONS!
[MySQL Window Function usage docs](https://dev.mysql.com/doc/refman/8.0/en/window-functions-usage.html)

[MySQL Window Function ONLY funcs docs](https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html)

#### `OVER()`
Data over which to apply an aggragate function.
```sql
-- applies AVG() fun to entire salary col
SELECT emp_no, department, salary, AVG(salary) OVER() FROM employees;
```

#### `PARTITION BY <col_name>`
Makes 'windows' which are a lot like 'groups'.
```sql
-- applies AVG() fun to entire salary data, grouped by department
SELECT emp_no, department, salary, AVG(salary) OVER(PARTITION BY department) FROM employees;
```

#### `ORDER BY` in `OVER()`
Can use `ORDER BY` inside an `OVER()` clause to re-order rows *within each window*
```sql
OVER(ORDER BY salary DESC)
```
How is this different? Using `ORDER BY` in an `OVER()` statement results in a *rolling* calculation (rolling sum, avg, min, max, etc).

```sql
SELECT
    -> emp_no,
    ->     department,
    ->     salary,
    ->     SUM(salary) OVER(PARTITION BY department) AS dept_payroll,
    ->     SUM(salary) OVER(PARTITION BY department ORDER BY salary) AS rolling_payroll
    -> FROM employees;
+--------+------------------+--------+--------------+-----------------+
| emp_no | department       | salary | dept_payroll | rolling_payroll |
+--------+------------------+--------+--------------+-----------------+
|     19 | customer service |  31000 |       326000 |           31000 |
|     15 | customer service |  38000 |       326000 |           69000 |
|     18 | customer service |  40000 |       326000 |          109000 |
|     16 | customer service |  45000 |       326000 |          154000 |
|     21 | customer service |  55000 |       326000 |          209000 |
|     20 | customer service |  56000 |       326000 |          265000 |
|     17 | customer service |  61000 |       326000 |          326000 |
|      5 | engineering      |  67000 |       569000 |           67000 |
|      2 | engineering      |  69000 |       569000 |          136000 |
|      3 | engineering      |  70000 |       569000 |          206000 |
|      1 | engineering      |  80000 |       569000 |          286000 |
|      6 | engineering      |  89000 |       569000 |          375000 |
|      7 | engineering      |  91000 |       569000 |          466000 |
|      4 | engineering      | 103000 |       569000 |          569000 |
|      8 | sales            |  59000 |       542000 |           59000 |
|     12 | sales            |  60000 |       542000 |          119000 |
|     13 | sales            |  61000 |       542000 |          241000 |
|     14 | sales            |  61000 |       542000 |          241000 |
|      9 | sales            |  70000 |       542000 |          311000 |
|     11 | sales            |  72000 |       542000 |          383000 |
|     10 | sales            | 159000 |       542000 |          542000 |
+--------+------------------+--------+--------------+-----------------+
```

## RANK()
Can use RANK() with OVER() to get the rank of any particular column.
For instance, to get the rank of salaries
```sql
SELECT emp_no, department, salary, RANK() OVER(ORDER BY salary DESC) AS salary_rank FROM employees;
+--------+------------------+--------+-------------+
| emp_no | department       | salary | salary_rank |
+--------+------------------+--------+-------------+
|     19 | customer service |  31000 |           1 |
|     15 | customer service |  38000 |           2 |
|     18 | customer service |  40000 |           3 |
|     16 | customer service |  45000 |           4 |
|     21 | customer service |  55000 |           5 |
|     20 | customer service |  56000 |           6 |
|      8 | sales            |  59000 |           7 |
|     12 | sales            |  60000 |           8 |
|     13 | sales            |  61000 |           9 |
|     14 | sales            |  61000 |           9 |
|     17 | customer service |  61000 |           9 |
|      5 | engineering      |  67000 |          12 |
|      2 | engineering      |  69000 |          13 |
|      3 | engineering      |  70000 |          14 |
|      9 | sales            |  70000 |          14 |
|     11 | sales            |  72000 |          16 |
|      1 | engineering      |  80000 |          17 |
|      6 | engineering      |  89000 |          18 |
|      7 | engineering      |  91000 |          19 |
|      4 | engineering      | 103000 |          20 |
|     10 | sales            | 159000 |          21 |
+--------+------------------+--------+-------------+
```
```sql
SELECT 
  emp_no, 
  department, 
  salary, 
  -- Gets overall company rank (no `partition`)
  RANK() OVER(ORDER BY salary DESC) AS salary_rank, 
  -- Gets rank by dept (`PARTITION BY department`)
  RANK() OVER(PARTITION BY department ORDER BY salary DESC) AS dept_rank 
FROM 
  employees;
+--------+------------------+--------+-------------+-----------+
| emp_no | department       | salary | salary_rank | dept_rank |
+--------+------------------+--------+-------------+-----------+
|     17 | customer service |  61000 |          11 |         1 |
|     20 | customer service |  56000 |          16 |         2 |
|     21 | customer service |  55000 |          17 |         3 |
|     16 | customer service |  45000 |          18 |         4 |
|     18 | customer service |  40000 |          19 |         5 |
|     15 | customer service |  38000 |          20 |         6 |
|     19 | customer service |  31000 |          21 |         7 |
|      4 | engineering      | 103000 |           2 |         1 |
|      7 | engineering      |  91000 |           3 |         2 |
|      6 | engineering      |  89000 |           4 |         3 |
|      1 | engineering      |  80000 |           5 |         4 |
|      3 | engineering      |  70000 |           7 |         5 |
|      2 | engineering      |  69000 |           9 |         6 |
|      5 | engineering      |  67000 |          10 |         7 |
|     10 | sales            | 159000 |           1 |         1 |
|     11 | sales            |  72000 |           6 |         2 |
|      9 | sales            |  70000 |           7 |         3 |
|     13 | sales            |  61000 |          11 |         4 |
|     14 | sales            |  61000 |          11 |         4 |
|     12 | sales            |  60000 |          14 |         6 |
|      8 | sales            |  59000 |          15 |         7 |
+--------+------------------+--------+-------------+-----------+
```