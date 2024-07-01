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
