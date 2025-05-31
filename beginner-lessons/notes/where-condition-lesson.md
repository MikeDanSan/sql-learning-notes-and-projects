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