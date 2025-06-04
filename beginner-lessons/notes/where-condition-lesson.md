# WHERE Condition Lesson

## WHERE
> Pick and filter on ***row(s)*** based on conditions

The `WHERE` clause is used to filter records in a SQL query based on specific conditions. It allows you to retrieve only the ***rows*** that meet the criteria defined in the clause, making your queries more precise and efficient. By combining `WHERE` with operators like `=`, `<`, `>`, `LIKE`, and logical conditions (`AND`, `OR`, `NOT`), you can perform powerful data filtering to extract meaningful insights from your database.

Basic Syntax:
```sql
SELECT column1, column2 
FROM table_name 
WHERE condition;
```

### Filtering Data with WHERE Clause:

You can filter data (rows) by one or more conditions, the condition must be true for a row to be included in the result set.

Example: 
```sql
SELECT * -- Return All columns
FROM employees -- From the table named employees
WHERE salary > 50000; -- Only return if salary row is greater than 50000
```

### Logical Operators in WHERE Clause:

Logical operators include (AND, OR, NOT). You can use logical operators to create more complex conditions. For example, if we continue with the previous example of only return if salary row is greater than 50000, you can add  the `AND` operator and specify another row to add another condition.

Example:
```sql
SELECT *
FROM employees
WHERE
salary > 50000
AND
department = 'Sales';
```

### Comparison Operators in WHERE Clause:

Comparison operators is another way to provide more conditions for the `WHERE` clause.
Here is a list of Comparison Operators (=, <>, >, <, >=, <=) these are used to compare values. 

Example:
```sql
SELECT product_name, unit_price
FROM products
WHERE unit_price < 50;
```

### Wildcards with WHERE Clause

Wildcard characters are used to filter for pattern matching. 

Example:
```sql
SELECT 
    *
FROM 
    customers
WHERE
    customer_name LIKE 'Joh%';
```

### NULL Vlaues and IS NULL/IS NOT NULL

A condition that can be used with WHERE clause is the NULL or IS NOT NULL operators. Great tool for identifying missing data and performing data quality checks in SQL queries. Use to effectively handle NULL values in your database and ensure data accuracy.

Example:
```sql
SELECT
    *
FROM 
    employees
WHERE
    manager_id IS NULL;
```

## IN Operator

The IN operator is a tool that simplifies SQL queries when dealing with multiple values. Specify a list of values, and the query will retrieve rows that match. 

Example:
```sql
SELECT
    *
FROM 
    products
WHERE
    (unit_price > 100 AND category IN ('Electronics', 'Appliances')) 
OR 
    (category = 'Office Supplies');
```

## BETWEEN Operator
> BETWEEN is ***inclusive***

Use the BETWEEN Operator when dealing with range-based conditions. There is also NOT BETWEEN. Use when filtering data based on:

- **Numeric Types**
  - INTEGER, SMALLINT, BIGINT
  - DECIMAL, NUMERIC
  - FLOAT, REAL, DOUBLE PRECISION

- **Date and Time Types**
  - DATE
  - TIME
  - TIMESTAMP / DATETIME

- **Character/String Types**
  - CHAR
  - VARCHAR
  - TEXT

- **Other (Database-Specific Support)**
  - BOOLEAN (e.g., PostgreSQL)
  - ENUM (e.g., MySQL)
  - UUID (e.g., PostgreSQL)

Example:
```sql
SELECT
    *
FROM 
    products
WHERE
    unit_price BETWEEN 50 AND 100;
```

## NOT Operator

The SQL NOT operator is used to reverse the result of a condition. For example, if a condition is true, applying NOT makes it false — and vice versa. It's often used with other operators like IN, BETWEEN, LIKE, or even full conditions in a WHERE clause.

Example:
```sql
SELECT
    *
FROM
    products
WHERE
    NOT price BETWEEN 10 AND 50;
```

Another example:

```sql
SELECT

    employee_id,
    first_name,
    last_name,
    department

FROM

    employees

WHERE

    department NOT IN ('Marketing', 'IT');
```


