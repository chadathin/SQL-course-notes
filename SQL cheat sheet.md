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
  - [Deleting (dropping) a table](#deleting-dropping-a-table)
  - [Basic CRUD Operations (Create, Read, Update, Delete)](#basic-crud-operations-create-read-update-delete)
    - [Create](#create)
    - [Read](#read)
    - [Update](#update)
    - [Delete](#delete)



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
-- After running: DESC dogs;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| name  | varchar(50) | YES  |     | NULL    |                |
| breed | varchar(50) | YES  |     | NULL    |                |
| age   | int         | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
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
SHOW TABLEs;
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
***
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

Again, we will cover more in the Advanced CRUD section. But this will suffice, for now. 
***
#### Update


***
#### Delete