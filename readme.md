Sure! Here’s a comprehensive MySQL/MariaDB cheat sheet in `README.md` format. This document will cover essential commands for database management, user administration, and querying.

---

# MySQL/MariaDB Cheat Sheet

## Table of Contents

1. [Database Management](#database-management)
   - Creating a Database
   - Selecting a Database
   - Showing Databases
   - Dropping a Database
2. [Table Management](#table-management)
   - Creating a Table
   - Showing Tables
   - Describing a Table
   - Altering a Table
   - Dropping a Table
3. [Data Management](#data-management)
   - Inserting Data
   - Selecting Data
   - Updating Data
   - Deleting Data
4. [User Management](#user-management)
   - Creating a User
   - Granting Privileges
   - Showing User Privileges
   - Revoking Privileges
   - Deleting a User
5. [View Management](#view-management)
   - Creating a View
   - Selecting from a View
   - Updating Data Through a View
   - Dropping a View
   - Showing Views
   - Checking View Definition
6. [Database Queries](#database-queries)
   - Basic Queries
   - Advanced Queries
   - Joins
   - Subqueries
7. [Additional Commands](#additional-commands)
   - Backing Up a Database
   - Restoring a Database
   - Checking Database Status
   - Flushing Privileges

---

## Database Management

### Creating a Database

```sql
CREATE DATABASE database_name;
```

### Selecting a Database

```sql
USE database_name;
```

### Showing Databases

```sql
SHOW DATABASES;
```

### Dropping a Database

```sql
DROP DATABASE database_name;
```

---

## Table Management

### Creating a Table

```sql
CREATE TABLE table_name (
    column1_name column1_datatype [constraints],
    column2_name column2_datatype [constraints],
    ...
    PRIMARY KEY (primary_key_column)
);
```

**Example**:

```sql
CREATE TABLE Students (
    student_id INT AUTO_INCREMENT,
    name VARCHAR(100),
    course VARCHAR(100),
    grade DECIMAL(3, 2),
    PRIMARY KEY (student_id)
);
```

### Showing Tables

```sql
SHOW TABLES;
```

### Describing a Table

```sql
DESCRIBE table_name;
```

### Altering a Table

- **Add a Column**:

  ```sql
  ALTER TABLE table_name ADD column_name column_datatype;
  ```

- **Modify a Column**:

  ```sql
  ALTER TABLE table_name MODIFY column_name new_column_datatype;
  ```

- **Drop a Column**:

  ```sql
  ALTER TABLE table_name DROP COLUMN column_name;
  ```

### Dropping a Table

```sql
DROP TABLE table_name;
```

---

## Data Management

### Inserting Data

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

**Example**:

```sql
INSERT INTO Students (name, course, grade)
VALUES ('Alice', 'Mathematics', 89.5);
```

### Selecting Data

```sql
SELECT column1, column2, ...
FROM table_name
WHERE conditions;
```

**Example**:

```sql
SELECT name, course FROM Students WHERE grade > 75;
```

### Updating Data

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE conditions;
```

**Example**:

```sql
UPDATE Students
SET grade = 95
WHERE name = 'Alice';
```

### Deleting Data

```sql
DELETE FROM table_name
WHERE conditions;
```

**Example**:

```sql
DELETE FROM Students
WHERE name = 'Alice';
```

---

## User Management

### Creating a User

```sql
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
```

**Example**:

```sql
CREATE USER 'john'@'localhost' IDENTIFIED BY 'securepassword';
```

### Granting Privileges

```sql
GRANT privileges ON database_name.table_name TO 'username'@'host';
```

**Example**:

```sql
GRANT SELECT, INSERT ON school_db.Students TO 'john'@'localhost';
```

### Showing User Privileges

```sql
SHOW GRANTS FOR 'username'@'host';
```

**Example**:

```sql
SHOW GRANTS FOR 'john'@'localhost';
```

### Revoking Privileges

```sql
REVOKE privileges ON database_name.table_name FROM 'username'@'host';
```

**Example**:

```sql
REVOKE INSERT ON school_db.Students FROM 'john'@'localhost';
```

### Deleting a User

```sql
DROP USER 'username'@'host';
```

**Example**:

```sql
DROP USER 'john'@'localhost';
```

---

## View Management

### Creating a View

```sql
CREATE VIEW view_name AS
SELECT columns
FROM table_name
WHERE conditions;
```

**Example**:

```sql
CREATE VIEW CS_Students AS
SELECT name, course
FROM Students
WHERE course = 'Computer Science';
```

### Selecting from a View

```sql
SELECT * FROM view_name;
```

**Example**:

```sql
SELECT * FROM CS_Students;
```

### Updating Data Through a View

If the view is updatable:

```sql
UPDATE view_name
SET column_name = value
WHERE conditions;
```

**Example**:

```sql
UPDATE CS_Students
SET name = 'John Doe'
WHERE name = 'Alice';
```

### Dropping a View

```sql
DROP VIEW view_name;
```

**Example**:

```sql
DROP VIEW CS_Students;
```

### Showing Views

```sql
SHOW FULL TABLES WHERE Table_type = 'VIEW';
```

### Checking View Definition

```sql
SHOW CREATE VIEW view_name;
```

**Example**:

```sql
SHOW CREATE VIEW CS_Students;
```

---

## Database Queries

### Basic Queries

- **Selecting All Columns**:

  ```sql
  SELECT * FROM table_name;
  ```

- **Selecting Specific Columns**:

  ```sql
  SELECT column1, column2 FROM table_name;
  ```

- **Using WHERE Clause**:

  ```sql
  SELECT * FROM table_name WHERE conditions;
  ```

- **Ordering Results**:

  ```sql
  SELECT * FROM table_name ORDER BY column_name [ASC|DESC];
  ```

- **Limiting Results**:

  ```sql
  SELECT * FROM table_name LIMIT number;
  ```

### Advanced Queries

- **Group By**:

  ```sql
  SELECT column, COUNT(*)
  FROM table_name
  GROUP BY column;
  ```

- **Having Clause**:

  ```sql
  SELECT column, COUNT(*)
  FROM table_name
  GROUP BY column
  HAVING COUNT(*) > 1;
  ```

- **Joins**:

  - **Inner Join**:

    ```sql
    SELECT columns
    FROM table1
    INNER JOIN table2 ON table1.column = table2.column;
    ```

  - **Left Join**:

    ```sql
    SELECT columns
    FROM table1
    LEFT JOIN table2 ON table1.column = table2.column;
    ```

  - **Right Join**:

    ```sql
    SELECT columns
    FROM table1
    RIGHT JOIN table2 ON table1.column = table2.column;
    ```

### Subqueries

- **In a SELECT Statement**:

  ```sql
  SELECT column
  FROM table
  WHERE column IN (SELECT column FROM table WHERE conditions);
  ```

- **In a WHERE Clause**:

  ```sql
  SELECT column
  FROM table
  WHERE column = (SELECT column FROM table WHERE conditions);
  ```

---

## Additional Commands

### Backing Up a Database

```bash
mysqldump -u username -p database_name > backup_file.sql
```

**Example**:

```bash
mysqldump -u root -p school_db > school_db_backup.sql
```

### Restoring a Database

```bash
mysql -u username -p database_name < backup_file.sql
```

**Example**:

```bash
mysql -u root -p school_db < school_db_backup.sql
```

### Checking Database Status

```sql
SHOW STATUS;
```

### Flushing Privileges

```sql
FLUSH PRIVILEGES;
```

---

## Conclusion

This cheat sheet covers the essential MySQL/MariaDB commands for managing databases, tables, users, views, and querying data. These commands provide a foundation for effective database administration and data manipulation.

For more detailed information, refer to the official [MySQL Documentation](https://dev.mysql.com/doc/) or [MariaDB Documentation](https://mariadb.com/kb/en/library/documentation/).

Feel free to customize and extend this cheat sheet to suit your specific needs!

---

This should give you a comprehensive guide to most of the necessary commands you'll need when working with MySQL or MariaDB databases. If you need more details or have any specific questions, feel free to ask!