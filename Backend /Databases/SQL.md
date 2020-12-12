# MySQL Commmands

## Frequently Used

`SELECT` perhaps the most important statement - fetches data
`DISTINCT` filters for unique values
`WHERE` filtering for a condition

```
SELECT DISTINCT column_name(s)
FROM table_name
WHERE column_name operator value;
```

## Altering the database

`ALTER TABLE` adds columns to table in database

```
ALTER TABLE table_name
ADD column_name datatype;
```

`CREATE TABLE` creates new table in database

```
CREATE TABLE table_name (
  column_1 datatype,
  column_2 datatype,
  column_3 datatype
);
```

`DELETE` remove rows from table

```
DELETE FROM table_name
WHERE some_column = some_value;
```

`INSERT` add new row to table

```
INSERT INTO table_name (column_1, column_2, column_3)
VALUES (value_1, 'value_2', value_3);
```

`UPDATE` edit rows in a table

```
UPDATE table_name
SET some_column = some_value
WHERE some_column = some_value;
```

## Operators / Clause

`

`AND` operator combining conditions, `OR` where either condition is true

```
SELECT column_name(s)
FROM table_name
WHERE column_1 = value_1
  AND column_2 = value_2;
  OR  column_3 = value_3;

```

`AS` renaming column or table with an alias

```
SELECT column_name AS alias
FROM table_name;
```

`WITH` lets you store result into temporary table using an alias

```
WITH temporary_name AS (
   SELECT *
   FROM table_name)
SELECT *
FROM temporary_name
WHERE column_name operator value;
```

`CASE` creating different outputs under different conditions

```
SELECT column_name,
  CASE
    WHEN condition THEN 'Result_1'
    WHEN condition THEN 'Result_2'
    ELSE 'Result_3'
  END
FROM table_name;
```

`LIKE` matching pattern used with WHERE

```
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;
```

`LIMIT` specify max number of rows for result (will take from the top)

```
SELECT column_name(s)
FROM table_name
LIMIT number;
```

## JOIN

`INNER JOIN` returns rows when there is a match in both tables.

`LEFT JOIN`: returns all rows from the left table, even if there are no matches in the right table. (OUTER JOIN)

`RIGHT JOIN`: returns all rows from the right table, even if there are no matches in the left table. (OUTER JOIN)

`FULL JOIN`: It combines the results of both left and right outer joins.

```
SELECT column_name(s)
FROM table_1
JOIN table_2
  ON table_1.column_name = table_2.column_name;
```

## Aggregate Functions

`AVG` average value for numeric column

```
SELECT AVG(column_name)
FROM table_name;
```

`COUNT` counts number of rows where column name is not NULL

```
SELECT COUNT(column_name)
FROM table_name;
```

`SUM` sum of all values in column

```
SELECT SUM(column_name)
FROM table_name;
```

`MIN`/`MAX` smallest/largest value in column

```
SELECT MAX(column_name)
FROM table_name;
```

`HAVING` WHERE clause for aggregation

```
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > value;
```

## End clauses

`GROUP BY` clause with SELECT used only with aggregation to group data

```
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name;
```

`ORDER BY` sort result alphabetically or numerically

```
SELECT column_name
FROM table_name
ORDER BY column_name ASC | DESC;
```
