# Data Types

## String Types

- Text is string of any length, like Python str or unicode types
- Char(n) is string of exactly n characters
- Varchar(n) is string of up to n characters

## Numeric Types

- Integer is integer value, like Python int
- Real is floating-point value, like Python float
  - Accurate up to six decimal places
- Double precision is higher-precision floating-point value
  - Accurate up to 15 decimal places
- Decimal is exact decimal value

## Date And Time Types

- Date is calendar date
  - Including year, month and day
- Time is time of day
- Timestamp is date and time together
- Timestamp with time zone is timestamp that carries time zone information
  - Type timestamp with time zone can be abbreviated to timestamptz in PostgreSQL

# Basics

`WHERE` expresses restrictions, filtering table for rows that follow particular rule, supports equalities, inequalities,and boolean operators among other things

- `WHERE species = 'gorilla'` returns only rows that have 'gorilla' as value of species column
- `WHERE name >= 'George'` returns only rows where name column is alphabetically after 'George'
- `WHERE species != 'gorilla' AND name != 'George'` returns only rows where species isn't 'gorilla' and name isn't 'George'

`LIMIT` and `OFFSET` set limit on how many rows to return in result table, optional offset clause says how far to skip ahead into results

- `LIMIT 10 OFFSET 100` will return 10 results starting with 101st

`ORDER BY` tells database how to sort results, usually according to one or more columns

- `ORDER BY species, name` sorts results first by species column, then by name within each species
- Ordering happens before limit/offset, can be used together to extract pages of alphabetized results
- Optional `DESC` modifier tells database to order results in descending order — for instance from large numbers to small ones, or from Z to A.

`GROUP BY` only used with aggregations, such as max or sum

- Without `GROUP BY` clause, `SELECT` statement with aggregation will aggregate over whole selected table(s), returning only one row
- With `GROUP BY` clause, it will return one row for each distinct value of column or expression in `GROUP BY` clause.

`HAVING` works like `WHERE` clause, but it applies after `GROUP BY` aggregations take place

```
SELECT col1, sum(col2) AS total
  FROM table
  GROUP BY col1
  HAVING total > 500 ;
```

# After Aggregating

- `WHERE` is restriction on source tables and can also not used after `GROUP BY`
- `HAVING` is restriction on result after aggregation

```
SELECT species, COUNT(*) AS num
  FROM animals
  GROUP BY species
  HAVING num=1;
```

- Would not work with `WHERE` restriction
- Alternatively sub select could be used

# Normalized Design

- In *normalized database*, relationships among tables match relationships that are really there among data
- Rules
  - Every row has same number of columns
  - There is unique key and everything in row says something about key, other columns describe something about key
  - Facts that do not relate to key belong in different tables
  - Tables should not imply relationships that do not exist
- *Denormalization* is approach to make databases fast by avoiding joins, use tools such as [indexes](https://www.postgresql.org/docs/9.4/static/sql-createindex.html) and [materialized views](https://www.postgresql.org/docs/9.4/static/sql-creatematerializedview.html)

# Subqueries

- Select from results of select query
- Subqueries can also be used in `WHERE` clause

```
SELECT name, weight
  FROM players,
  (SELECT avg(weight) AS av FROM players) AS subq
  WHERE weight < av;
```

# Functions

## Insert

- `INSERT INTO table VALUES (42, "stuff");`
  - To add row
- `INSERT INTO table (col2, col1) VALUES ("stuff", 42);`
  - To add row if values are not in same order as table columns

## Create

- User-facing code does not usually create new tables
- `≈≈` avoid blanks
- `PRIMARY KEY` as option to set column as single primary key
- In case of multi-column primary key, set `PRIMARY KEY (column1, column3)` after listing all columns in `CREATE`
  - For example use postal code and country in combination as primary key to have unique key globally since postal codes alone are similar in countries
- Tables does not necessarily need primary key
- If duplicate value is inserted in primary key, database will signal error, rollback might be required
- `REFERENCE othertablename` to ensure that certain columns only has values that refer to key of another table
  - Use `REFERENCE othertablename(column5)` if column has different name on other table
- References provide referential integrity, columns that are supposed to refer to each other are guaranteed to do so
- Columns with reference constraint is called foreign key
- Foreign key is columns or set of columns in one table that uniquely identifies rows in another table
- Table can have multiple foreign keys

```
CREATE TABLE tablename (  
  column1 TYPE [options],
  column2 TYPE PRIMARY KEY [options],
  column3 TYPE [options] NOT NULL,
  column4 TYPE REFERNCE othertablename [options])[rowrestriction];
```

```
CREATE DATABASE name
```

- `\c name` to connect to database

## Drop

- There is no confirmation before `DROP` will be executed
- Currently connected database can not be dropped

```
DROP DATABASE name [options];
```

```
DROP TABLE name [options];
```

# Views

- View is select query stored in database in way that it can be used like any other table
- Also used to display only particular columns from table with many columns
- In SQLite rows can not be updated or deleted
- In PostgreSQL rows of simple views can be updated or deleted

```
CREATE VIEW viewname AS SELECT
```

# Join

- More readable

```
SELECT ordernames.name, count(*) AS num
  FROM animals, taxonomy, ordernames
  WHERE animals.species = taxonomy.name
  AND taxonomy.t_order = ordernames.t_order
  GROUP BY ordernames.name
  ORDER BY num DESC
```

- Alternatively

```
SELECT ordernames.name, count(*) AS num
FROM (animals JOIN taxonomy
  ON animals.species = taxonomy.name)
  AS ani_tax
JOIN ordernames
  ON ani_tax.t_order = ordernames.t_order
  GROUP BY ordernames.name
  ORDER BY num DESC
```

- Left join to also show zeros, meaning if certains products have never been sold

```
SELECT products.name, products.sku, count(sales.sku) AS num
FROM products LEFT JOIN sales
  ON products.sku = sales.sku
  GROUP BY products.sku;
```

## Self Joins

- Find pairs of roommates for example

```
SELECT a.id, b.id, a.building, a.room
  FROM residences AS a, residences AS b
WHERE a.building = b.building
  AND a.room = b.room
  AND a.id < b.id -- Eliminate one out of each pair of duplicates.
  ORDER BY a.building, a.room;
```

# Resources

- [Simple Guide](http://www.bkent.net/Doc/simple5.htm) to five normal forms in relational database theory
- PostgreSQL Documentation: [PostgreSQL](https://www.postgresql.org/docs/9.4/static/index.html)
- PostgreSQL has special serial type: [PostgreSQL](https://www.postgresql.org/docs/9.4/static/datatype-numeric.html)

*To be continued*
