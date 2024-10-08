# Advanced MySQL Commands 

In this section, we will cover more complex operations in MySQL 8.4. These include JOINs, subqueries, indexes, transactions, and stored procedures. Each concept will be explained with examples.

## JOINs

### Inner Join

An `INNER JOIN` returns records that have matching values in both tables.

```sql
-- Example: Inner Join between 'employees' and 'departments' tables
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.id;
```
* Here, the query selects names of employees along with their department names, only if there is a matching department_id in both tables.

### Left Join

A `LEFT JOIN` returns all records from the left table and the matched records from the right table. If no match is found, NULL values are returned for columns from the right table.

```sql
-- Example: Left Join between 'employees' and 'departments' tables
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.id;
```
* This query returns all employees and their respective departments, including those employees who do not belong to any department.

### Right Join

A `RIGHT JOIN` returns all records from the right table and the matched records from the left table. If no match is found, NULL values are returned for columns from the left table.

```sql
-- Example: Right Join between 'employees' and 'departments' tables
SELECT employees.name, departments.department_name
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.id;
```
* This query returns all departments and their respective employees, including those departments that do not have any employees.

### Full Join

MySQL does not support FULL JOIN directly. However, you can achieve it using a combination of `LEFT JOIN` and `UNION`.

```sql
-- Example: Full Join between 'employees' and 'departments' tables
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.id
UNION
SELECT employees.name, departments.department_name
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.id;
```
* This query returns all employees and departments, with NULL values where there is no match.

## Subqueries

A subquery is a query nested inside another query. They can be used in SELECT, INSERT, UPDATE, or DELETE statements.

### Subquery in SELECT

```sql
-- Example: Subquery to get the name of the department with the highest number of employees
SELECT name 
FROM departments 
WHERE id = (SELECT department_id 
            FROM employees 
            GROUP BY department_id 
            ORDER BY COUNT(*) DESC 
            LIMIT 1);
```
* This query finds the department name that has the highest number of employees.

### Subquery in FROM

```sql
-- Example: Subquery in FROM clause to calculate average salary per department
SELECT department_id, AVG(salary) 
FROM (SELECT * FROM employees WHERE salary > 30000) AS high_paid_employees 
GROUP BY department_id;
```
* This query first filters employees with a salary greater than 30000 and then calculates the average salary per department.

## Indexes

Indexes are used to speed up the retrieval of data from the database.

### Creating an Index

```sql
-- Example: Create an index on the 'name' column of the 'employees' table
CREATE INDEX idx_name ON employees(name);
```
* This command creates an index named `idx_name` on the `name` column of the `employees` table.

### Dropping an Index

```sql
-- Example: Drop the index named 'idx_name'
DROP INDEX idx_name ON employees;
```
* This command removes the `idx_name` index from the `employees` table.

## Transactions

Transactions allow multiple SQL operations to be executed as a single unit of work.

### Start a Transaction

```sql
-- Example: Start a transaction
START TRANSACTION;
```
* This command initiates a new transaction.

### Commit a Transaction

```sql
-- Example: Commit a transaction
COMMIT;
```
* This command saves all changes made during the transaction.

### Rollback a Transaction

```sql
-- Example: Rollback a transaction
ROLLBACK;
```
* This command undoes all changes made during the transaction.

### Transaction Example

```sql
-- Example: Transfer money example to demonstrate transaction
START TRANSACTION;

-- Deduct amount from sender's account
UPDATE accounts 
SET balance = balance - 100 
WHERE account_id = 1;

-- Add amount to receiver's account
UPDATE accounts 
SET balance = balance + 100 
WHERE account_id = 2;

-- Commit the transaction if both updates succeed
COMMIT;
```
* In this example, money is transferred from one account to another. If any of the updates fail, the transaction can be rolled back to maintain data integrity.

## Stored Procedures

Stored procedures are a set of SQL statements that can be stored and reused.

### Creating a Stored Procedure

```sql
-- Example: Create a stored procedure to get employee details by department
DELIMITER //
CREATE PROCEDURE GetEmployeesByDepartment(IN dept_id INT)
BEGIN
    SELECT name, position, salary 
    FROM employees 
    WHERE department_id = dept_id;
END //
DELIMITER ;
```
* This stored procedure, `GetEmployeesByDepartment`, takes a department ID as input and returns employee details for that department.

### Calling a Stored Procedure

```sql
-- Example: Call the stored procedure created above
CALL GetEmployeesByDepartment(1);
```
* This command calls the `GetEmployeesByDepartment` procedure with `1` as the department ID.

### Dropping a Stored Procedure

```sql
-- Example: Drop the stored procedure
DROP PROCEDURE IF EXISTS GetEmployeesByDepartment;
```
* This command deletes the `GetEmployeesByDepartment` stored procedure.

By understanding and using these advanced MySQL commands, you can create more efficient and powerful database operations.
