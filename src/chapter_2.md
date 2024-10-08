# Basic MySQL Commands

This section covers fundamental MySQL operations such as creating databases and tables, inserting data, querying data, updating data, and deleting data. Each command will be presented with detailed explanations and corresponding examples.

## Creating a Database

To begin using MySQL, the first step is to create a database. A database is a container that holds tables and other objects.

```sql
-- Create a new database named 'example_db'
CREATE DATABASE example_db;

-- Use the newly created database
USE example_db;
```

## Creating a Table

Tables are structures within a database that store data in rows and columns. Let's create a simple table named `users`.

```sql
-- Create a table named 'users' with three columns: id, name, and email
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY, -- 'id' is an integer that auto-increments and serves as the primary key
    name VARCHAR(255) NOT NULL,        -- 'name' is a variable character field with a maximum length of 255, and cannot be null
    email VARCHAR(255) NOT NULL UNIQUE -- 'email' is a unique field that cannot be null
);
```

## Inserting Data

To populate the table with data, use the `INSERT INTO` statement.

```sql
-- Insert a new user into the 'users' table
INSERT INTO users (name, email) VALUES ('John Doe', 'john.doe@example.com');

-- Insert another user
INSERT INTO users (name, email) VALUES ('Jane Smith', 'jane.smith@example.com');
```

## Querying Data

To retrieve data from the table, use the `SELECT` statement.

```sql
-- Select all columns and rows from the 'users' table
SELECT * FROM users;

-- Select specific columns from the 'users' table
SELECT name, email FROM users;

-- Use a WHERE clause to filter records
SELECT * FROM users WHERE name = 'John Doe';
```

## Updating Data

To modify existing data in the table, use the `UPDATE` statement.

```sql
-- Update the email address of the user with name 'John Doe'
UPDATE users
SET email = 'john.new@example.com'
WHERE name = 'John Doe';
```

## Deleting Data

To remove data from the table, use the `DELETE` statement.

```sql
-- Delete the user with name 'Jane Smith'
DELETE FROM users
WHERE name = 'Jane Smith';

-- Delete all records from the 'users' table
DELETE FROM users;
```

By following these basic commands, you can perform essential operations in MySQL. These steps lay the foundation for more advanced database management and querying techniques.
