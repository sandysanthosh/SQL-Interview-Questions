Sure, here are some common SQL query interview questions along with their answers. These questions cover a range of topics including basic SQL operations, joins, subqueries, and aggregate functions.

### Basic SQL Questions

1. **What is SQL?**
   - SQL (Structured Query Language) is a standard language for managing and manipulating relational databases.

2. **How do you retrieve all the records from a table?**
   ```sql
   SELECT * FROM table_name;
   ```

3. **How do you filter records using a `WHERE` clause?**
   ```sql
   SELECT * FROM table_name WHERE condition;
   ```

### Joins

4. **What is a JOIN? Explain different types of joins.**
   - A JOIN clause is used to combine rows from two or more tables, based on a related column between them.
   - Types of joins:
     - **INNER JOIN**: Returns records that have matching values in both tables.
     - **LEFT (OUTER) JOIN**: Returns all records from the left table, and the matched records from the right table. The result is NULL from the right side, if there is no match.
     - **RIGHT (OUTER) JOIN**: Returns all records from the right table, and the matched records from the left table. The result is NULL from the left side, when there is no match.
     - **FULL (OUTER) JOIN**: Returns all records when there is a match in either left or right table.

5. **Write a query to retrieve data from two tables using an INNER JOIN.**
   ```sql
   SELECT a.column1, b.column2
   FROM table1 a
   INNER JOIN table2 b ON a.common_column = b.common_column;
   ```

### Subqueries

6. **What is a subquery and how is it used?**
   - A subquery is a query nested inside another query. It can be used in SELECT, INSERT, UPDATE, or DELETE statements or inside another subquery.
   - Example:
     ```sql
     SELECT column1
     FROM table1
     WHERE column2 = (SELECT column2 FROM table2 WHERE condition);
     ```

7. **Write a query to find employees who earn more than the average salary.**
   ```sql
   SELECT employee_id, employee_name
   FROM employees
   WHERE salary > (SELECT AVG(salary) FROM employees);
   ```

### Aggregate Functions

8. **Explain aggregate functions and provide examples.**
   - Aggregate functions perform a calculation on a set of values and return a single value. Examples include `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`.
   - Example:
     ```sql
     SELECT AVG(salary) AS average_salary FROM employees;
     ```

9. **Write a query to count the number of employees in each department.**
   ```sql
   SELECT department_id, COUNT(*) AS num_employees
   FROM employees
   GROUP BY department_id;
   ```

### Advanced SQL Questions

10. **What is a `HAVING` clause and how is it different from `WHERE`?**
    - The `HAVING` clause is used to filter records that work on aggregated results. It is used in combination with the `GROUP BY` clause.
    - `WHERE` is used to filter records before any groupings are made.
    - Example:
      ```sql
      SELECT department_id, COUNT(*)
      FROM employees
      GROUP BY department_id
      HAVING COUNT(*) > 10;
      ```

11. **Write a query to find the second highest salary from the employees table.**
    ```sql
    SELECT MAX(salary) AS second_highest_salary
    FROM employees
    WHERE salary < (SELECT MAX(salary) FROM employees);
    ```

12. **What is the difference between `UNION` and `UNION ALL`?**
    - `UNION` combines the results of two or more SELECT statements and removes duplicate rows.
    - `UNION ALL` combines the results of two or more SELECT statements without removing duplicate rows.
    - Example:
      ```sql
      SELECT column1 FROM table1
      UNION
      SELECT column1 FROM table2;

      SELECT column1 FROM table1
      UNION ALL
      SELECT column1 FROM table2;
      ```

13. **Explain the concept of indexing in SQL.**
    - Indexing is a technique to improve the performance of database queries. An index is a database object that speeds up the retrieval of rows by using a pointer.

14. **Write a query to delete duplicate rows from a table.**
    ```sql
    DELETE FROM table_name
    WHERE id NOT IN (
        SELECT MIN(id)
        FROM table_name
        GROUP BY column1, column2, ...);
    ```

15. **Explain the difference between `DELETE` and `TRUNCATE`.**
    - `DELETE` removes rows one at a time and records an entry in the transaction log for each deleted row. It can be rolled back.
    - `TRUNCATE` removes all rows from a table by deallocating the data pages used by the table. It is faster and cannot be rolled back.

These questions should give you a solid foundation for preparing for SQL interviews.


Certainly! Here are some more complex SQL interview questions that delve deeper into SQL concepts and require a good understanding of SQL queries, optimization, and advanced techniques:

1. **Write a query to find the nth highest salary from an Employees table.**

   ```sql
   SELECT DISTINCT salary
   FROM employees e1
   WHERE n = (
       SELECT COUNT(DISTINCT salary)
       FROM employees e2
       WHERE e2.salary >= e1.salary
   );
   ```

   Replace `n` with the desired rank (e.g., 3rd highest salary).

2. **Explain different types of SQL joins with examples for each.**

   - **INNER JOIN**:
     ```sql
     SELECT *
     FROM table1
     INNER JOIN table2 ON table1.common_column = table2.common_column;
     ```

   - **LEFT JOIN**:
     ```sql
     SELECT *
     FROM table1
     LEFT JOIN table2 ON table1.common_column = table2.common_column;
     ```

   - **RIGHT JOIN**:
     ```sql
     SELECT *
     FROM table1
     RIGHT JOIN table2 ON table1.common_column = table2.common_column;
     ```

   - **FULL OUTER JOIN**:
     ```sql
     SELECT *
     FROM table1
     FULL OUTER JOIN table2 ON table1.common_column = table2.common_column;
     ```

3. **Write a query to find departments with more than 10 employees and list the department name along with the number of employees.**

   ```sql
   SELECT department_name, COUNT(*) AS num_employees
   FROM departments d
   INNER JOIN employees e ON d.department_id = e.department_id
   GROUP BY department_name
   HAVING COUNT(*) > 10;
   ```

4. **Explain the difference between `UNION` and `UNION ALL` with suitable examples.**

   - **UNION**: Combines the results of two or more SELECT statements and removes duplicate rows.
     ```sql
     SELECT column1 FROM table1
     UNION
     SELECT column1 FROM table2;
     ```

   - **UNION ALL**: Combines the results of two or more SELECT statements including duplicate rows.
     ```sql
     SELECT column1 FROM table1
     UNION ALL
     SELECT column1 FROM table2;
     ```

5. **Write a query to find the top 3 departments with the highest average salary of employees.**

   ```sql
   SELECT department_id, AVG(salary) AS avg_salary
   FROM employees
   GROUP BY department_id
   ORDER BY avg_salary DESC
   LIMIT 3;
   ```

6. **Explain how you would optimize a slow-performing SQL query.**

   - Identify and create necessary indexes on columns used in `WHERE` and `JOIN` clauses.
   - Rewrite the query to minimize the number of records processed or joined.
   - Avoid using `SELECT *` and instead specify only the needed columns.
   - Use `EXPLAIN` or equivalent to analyze query execution plans and optimize based on that.

7. **Write a query to find employees who have worked for more than 5 years as of a specific date.**

   ```sql
   SELECT employee_id, employee_name
   FROM employees
   WHERE hire_date <= DATE_SUB(NOW(), INTERVAL 5 YEAR);
   ```

8. **Explain the concept of transaction in SQL. How would you ensure ACID properties in a transaction?**

   - A transaction in SQL is a sequence of one or more SQL operations that are treated as a single unit of work.
   - ACID properties are ensured using:
     - **Atomicity**: All operations in a transaction succeed or fail together.
     - **Consistency**: The database is in a valid state before and after the transaction.
     - **Isolation**: Transactions are isolated from each other until they commit.
     - **Durability**: Once a transaction commits, its changes are permanent.

9. **Write a query to find the customers who have made at least 3 orders in the last month.**

   ```sql
   SELECT customer_id, COUNT(*) AS num_orders
   FROM orders
   WHERE order_date >= DATE_SUB(NOW(), INTERVAL 1 MONTH)
   GROUP BY customer_id
   HAVING COUNT(*) >= 3;
   ```

10. **Explain the usage of window functions in SQL with an example.**

    Window functions allow you to perform calculations across a set of table rows that are related to the current row. Example:

    ```sql
    SELECT employee_id, department_id, salary,
           RANK() OVER(PARTITION BY department_id ORDER BY salary DESC) AS dept_rank
    FROM employees;
    ```

    This query ranks employees within each department based on salary.

These questions cover a range of SQL concepts and complexities commonly encountered in interviews, from advanced querying techniques to optimization and transaction management.

