# SELECT FROM Lesson

## SELECT

The `SELECT` statement is used to retrieve data from a database. It specifies the columns you want to fetch from a table. You can select specific columns separated by commas or use * to select all columns.

Syntax:
```sql
SELECT column1, column2 
FROM table_name;
```

Example:
```sql
SELECT name, age 
FROM employees;
```

## FROM

The FROM clause specifies the table from which the data will be retrieved. It is mandatory in a SELECT statement because it tells SQL where to look for the data.

Example:
```sql
SELECT * 
FROM customers;
```

### Key Notes:

- SELECT and FROM are the foundation of SQL queries.
- You can combine SELECT with other clauses like WHERE, ORDER BY, and GROUP BY to filter, sort, and group data.

## Deeper understanding

### SELECT

- Projection:
    The SELECT clause performs projection, which means it determines which columns of data will be included in the result set. This is distinct from filtering (done by WHERE) or sorting (done by ORDER BY).

- Expression Evaluation:
    You can use expressions in the SELECT clause, such as mathematical operations, string concatenation, or function calls. For example:
    ```sql
    SELECT price * quantity AS total_cost 
    FROM orders;
    ```
    > SQL evaluates these expressions for each row in the result set.

- Column Aliases:

    Aliases allow you to rename columns in the result set for better readability or to avoid conflicts. For example:
    ```sql
    SELECT name AS employee_name
    FROM employees;
    ```

- Execution Order:

    Although SELECT appears first in the query, it is executed after the FROM clause and other clauses like WHERE. SQL processes queries in the following logical order:
    - FROM
    - WHERE
    - GROUP BY
    - HAVING
    - SELECT
    - ORDER BY

- Duplicate Rows:

    By default, SELECT does not eliminate duplicate rows. To remove duplicates, you can use `DISTINCT`:
    ```sql
    SELECT DISTINCT department
    FROM employees;
    ```

### FROM

- Table Scanning:

    The FROM clause initiates a table scan, where SQL reads the table's data. Depending on the query and database engine, this can involve:
    - Full Table Scan: Reads all rows in the table.
    - Index Scan: Uses an index to locate rows more efficiently.
    - Index Seek: Directly accesses specific rows using an index.

- Joins:

    The FROM clause can include multiple tables with JOIN operations. SQL builds a Cartesian product (cross join) first and then filters rows based on the join condition. For example:
    ```sql
    SELECT e.name, d.department_name
    FROM employees e
    JOIN departments d ON e.department_id = d.id;
    ```

- Subqueries:
    The FROM clause can include subqueries, which act as `temporary tables`. For example:

    ```sql
    SELECT avg_salary
    FROM (SELECT AVG(salary) AS avg_salary FROM employees) AS subquery;
    ```

- Optimization:

    Modern SQL engines optimize the FROM clause by analyzing indexes, statistics, and query plans to determine the most efficient way to retrieve data. 
    > This process is called ***query optimization***.

- Virtual Tables:

    When using views or subqueries, the FROM clause may reference virtual tables that are not physically stored but are computed dynamically during query execution.

## Under-the-Hood Insights

Query Execution Plan

    SQL engines generate a query execution plan to determine how to execute the query efficiently. This plan includes steps like scanning tables, applying filters, and projecting columns.

Predicate Pushdown

    SQL engines often optimize queries by pushing filters (e.g., WHERE conditions) closer to the data source during the FROM clause processing. This reduces the amount of data processed in later stages.

Parallelism

    For large datasets, SQL engines may execute parts of the query (e.g., table scans or joins) in parallel across multiple CPU cores to improve performance.

Temporary Storage

    Intermediate results (e.g., from joins or subqueries) may be stored in temporary tables or memory structures during query execution.

Cost-Based Optimization

    SQL engines use a cost-based optimizer to evaluate different query execution strategies and choose the one with the lowest estimated cost (e.g., in terms of time or resources).

## SELECT Fun Facts

1. SELECT is the Most Popular SQL Command:
    
    The `SELECT` statement is the most commonly used SQL command, making up the majority of queries in real-world applications.

2. You Can Use SELECT Without a Table:

    In some databases, you can use `SELECT` to perform calculations or return constant values without referencing a table:
    ```sql
    SELECT 1 + 1 AS result;
    ```

3. SELECT Can Include Functions:

    You can use built-in functions like `COUNT`, `SUM`, `AVG`, and even string manipulation functions directly in the `SELECT` clause:
    ```sql
    SELECT UPPER(name) AS uppercase_name
    FROM employees;
    ```

4. SELECT Doesn't Always Retrieve Data:

    In some cases, `SELECT` is used for testing or debugging queries, such as checking expressions or verifying syntax.

### FROM Fun Facts

1. FROM Can Reference Virtual Tables:

    The `FROM` clause can use subqueries or views as "virtual tables," which are computed dynamically during query execution.

2. FROM is Where Joins Happen:

    All join operations (e.g., `INNER JOIN`, `LEFT JOIN`) are defined in the `FROM` clause, making it the backbone of multi-table queries.

3. FROM Can Include Recursive Queries:

    You can use a special feature called Common Table Expressions (CTEs) to write queries that repeat themselves (recursive queries). This is useful for working with data that has a hierarchy, like a company's organizational chart or a family tree. For example, you can find all employees under a manager by repeatedly looking at relationships in the data.

4. FROM Can Handle Cartesian Products

    If you include multiple tables in the FROM clause without specifying how they are related (no JOIN condition), SQL combines every row from one table with every row from the other table. This is called a Cartesian product. It can result in a very large number of rows, so it's usually avoided unless you specifically need it. 

    ### Example of Cartesian Product

    #### Table 1 (`table1`):
    | column1 |
    |---------|
    | A       |
    | B       |

    #### Table 2 (`table2`):
    | column1 |
    |---------|
    | X       |
    | Y       |

    #### SQL Query:
    ```sql
    SELECT table1.column1, table2.column1
    FROM table1, table2;
    ```

    #### Resulting Cartesian Product:

    | table1.column1 |table2.column1 |
    |----------------|---------------|
    | A              |X              |
    | A              |Y              |
    | B              |X              |
    | B              |Y              |

