# Introduction to Databases and Database Management Systems

## Introduction to SQL

- SQL, or Structured Query Language, is a programming language used for querying and managing data in relational databases.
- The original name of SQL was Structured English Query Language.

## What is Data?

- Data can be defined as a collection of facts such as words, numbers, or pictures.
- It's a crucial asset for businesses, collected, used, and stored practically everywhere.
- Data encompasses various personal and professional information like name, address, phone number, bank account details, etc.

## What is a Database?

- A database is a program that stores data and provides functionalities for adding, modifying, and querying that data.
- There are different kinds of databases tailored to various requirements, and data can be stored in different forms.

## Relational Databases

- In a relational database, data is stored in a tabular form, organized in tables which have columns (properties of an item) and rows (instances of the item).
- A table is a collection of related entities, like a list of employees or book authors.
- In a relational database, relationships can be formed between different tables.

## Database Management System (DBMS)

- The set of software tools for managing data in the database is called a Database Management System (DBMS).
- DBMS tools control the data access, organization, and storage.
- For relational databases, it's called a Relational Database Management System (RDBMS).
- Examples of RDBMS: MySQL, Oracle Database, DB2 Warehouse, and DB2 on Cloud.

## Basic SQL Commands

- The basic building blocks for SQL include commands to:
  1. `CREATE` a table
  2. `INSERT` data to populate the table
  3. `SELECT` data from the table
  4. `UPDATE` data in the table
  5. `DELETE` data from the table

```sql
CREATE TABLE table_name (column1 datatype, column2 datatype, ...);
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
SELECT column1, column2, ... FROM table_name;
UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;
DELETE FROM table_name WHERE condition;
```

- These commands provide the basic functions required for data science and manipulating data within the database.


# Relational Databases

## What is a Relational Database?

- A relational database is a collection of data organized into a table structure.
- The tables are linked, or related, based on data common to each.
- Tables are composed of rows (records) and columns (attributes).

## Example

- A `customer` table could have columns like `Company ID`, `Company Name`, `Company Address`, and `Company Primary Phone`. Each row in this table represents a customer record.
- A `transaction` table might have columns like `Transaction Date`, `Customer ID`, `Transaction Amount`, and `Payment Method`.
- These tables can be related via the common `Customer ID` field.

## Why Use Relational Databases?

- Relational databases minimize data redundancy by defining relationships between tables.
- You can restrict database fields to specific data types and values which leads to greater consistency and data integrity.
- They provide controlled access to data and ensure enforcement of data governance standards and policies.

## SQL and Relational Databases

- SQL is used for querying data in relational databases.
- It allows processing millions of records and retrieving large amounts of data swiftly.

## Types of Relational Databases

- They range from small desktop systems to massive cloud-based systems.
- They can be open-source and internally supported, open-source with commercial support, or commercial closed-source systems.
- Examples: IBM DB2, Microsoft SQL Server, MySQL, Oracle Database, PostgreSQL, Amazon RDS, Google Cloud SQL, IBM DB2 on Cloud, Oracle Cloud, and SQL Azure.

## Advantages of Relational Databases

- **Flexibility**: SQL allows changes while the database is running and queries are happening.
- **Reduced Redundancy**: Minimizes data redundancy by storing data only once and linking to it from other tables.
- **Ease of Backup and Disaster Recovery**: Easy export and import options, continuous mirroring in cloud-based databases.
- **ACID-Compliance**: Ensures the data in the database remains accurate and consistent despite failures.

```sql
-- Example SQL Query
SELECT * FROM customer 
INNER JOIN transaction ON customer.customer_id = transaction.customer_id;
```

## Use Cases for Relational Databases

- **Online Transaction Processing (OLTP) Applications**: RDBMS can handle high rates of transaction-oriented tasks and support a large number of users.
- **Data Warehouses**: Relational databases can be optimized for Online Analytical Processing (OLAP) to analyze historical data for business intelligence.
- **IoT Solutions**: Internet of Things (IoT) solutions require speed and the ability to collect and process data from edge devices, which need a lightweight database solution.

## Limitations of RDBMS

- RDBMS doesn't handle semi-structured and unstructured data well and isn't suitable for extensive analytics on such data.
- Schemas and data types need to be identical for migration between two RDBMSs.
- Relational databases have a limit on the length of data fields, which may prevent storage of longer information.

Despite these limitations and the advent of big data, cloud computing, IoT devices, and social media, RDBMS remains the predominant technology for working with structured data.


# Database Concepts 

## Database Models 

- The relational model is the most used data model for databases due to its data independence, allowing for logical data independence, physical data independence, and physical storage independence. 
- The entity relationship (ER) model is a tool to design relational databases, proposing to view a database as a collection of entities.

## Entity-Relationship Model

- Entities are objects that exist independently of any other entities in the database. They can be a noun: person, place, or thing.
- Attributes are properties or characteristics of an entity, which provide further information about the entity. 

## Mapping Entities and Attributes to Tables

- An entity becomes a table in a relational database.
- Attributes become columns in that table. 

## Example: Library Database

- The `book` entity might have attributes like `title`, `author`, `edition`, `year`, and these attributes would become columns in the `book` table in the database.
- Each `book` can be written by different `authors` , each library can have different `books`

## Data Types

- Each attribute stores data values of different formats, such as characters (`char`, `varchar`), numbers (`int`, `decimal`), and timestamps (`date`, `time`). 

## Keys

- Each table is assigned a primary key, which uniquely identifies each row (tuple) in a table, preventing duplication of data and providing a way to define relationships between tables.
- Tables can also contain foreign keys, which are primary keys from other tables, creating a link between the tables.

```sql
-- Example Table Creation for Book Entity
CREATE TABLE Book (
    ISBN CHAR(13) PRIMARY KEY,
    Title VARCHAR(255),
    Edition INT,
    YearWritten INT
);
```

## Learning Outcomes

- Advantage of the relational model: logical and physical data independence and storage independence.
- Difference between an entity and an attribute: Entities are independent objects in a database and attributes are their characteristics.
- Function of primary keys: They uniquely identify a specific row in a table and prevent duplication of data.



# Lesson Summary: Overview

## SQL (Structured Query Language)
- Designed for managing data in relational databases.
- Essential for handling structured data.
- Basic statements:
  - `CREATE TABLE`
  - `INSERT`
  - `SELECT`
  - `UPDATE`
  - `DELETE`

## Data 
- Defined as a collection of facts, which can be represented through words, numbers, or pictures.

## Database
- Repository of data.
- Provides functionality for:
  - Adding data.
  - Modifying data.
  - Querying data.

## Relational Databases
- Store tabular data as collections of related items.
- Organized into columns (item properties) and rows (items).
- Ideal for optimized storage, retrieval, and processing of large data volumes.
- Entity-Relationship Model is used for design:
  - Entities translate to tables.
  - Attributes translate to columns.

## RDBMS (Relational Database Management System)
- Mature and well-documented technology.
- Benefits include:
  - Flexibility in data management.
  - Reduced data redundancy.
  - Ease of backup and disaster recovery.
  - ACID compliance (Atomicity, Consistency, Isolation, Durability).



#  SELECT Statement 

In this video, you'll grasp how to retrieve data from relational database tables using the `SELECT` statement. We will delve into selecting columns, utilizing predicates, and incorporating the `WHERE` clause with diverse comparison operators.

## SELECT Statement
- **Purpose**: Not only for storing data but facilitating its retrieval.
- **Key Component of DML**: `SELECT` is a crucial Data Manipulation Language (DML) statement, pivotal for reading and modifying data.
- **Query Structure**: It's referred to as a query, yielding a result set or result table upon execution.
- **Basic Syntax**: `SELECT * FROM table_name`.

## Practical Example: Book Entity
- **Table Creation & Data Insertion**: For instance, in a `book` table created based on a book entity, data rows are added using `INSERT`.
- **Data Viewing**: `SELECT * FROM book` allows viewing of all data rows and columns in the `book` table.
- **Selective Column Retrieval**: You may opt to retrieve all rows for select columns only, e.g., `SELECT book_id, title FROM book`.

## WHERE Clause & Predicates
- **Function**: The `WHERE` clause restricts the result set, working in tandem with a predicate (a condition that evaluates to true, false, or unknown).
- **Example**: To find the title of a book with `book_id = 'B1'`, use: `SELECT book_id, title FROM book WHERE book_id = 'B1'`.

## Comparison Operators
- Supported by relational database management systems:
  - `= (Equal To)`
  - `> (Greater Than)`
  - `< (Less Than)`
  - `>= (Greater Than or Equal To)`
  - `<= (Less Than or Equal To)`
  - `<> (Not Equal To)`

## Recap
- Mastered the use of the `SELECT` statement for data retrieval, including column selection and `WHERE` clause utilization.
- Understand the role of predicates and various comparison operators in refining result sets.
- You’re now equipped to retrieve specific columns and limit result sets based on conditions.




# COUNT, DISTINCT, LIMIT

## Key Expressions
1. **`COUNT`**
   - **Purpose:** Retrieves the number of rows matching query criteria.
   - **Example:**
     ```sql
     SELECT COUNT(*) FROM tablename;
     ```
     For a table `MEDALS` with column `COUNTRY`:
     ```sql
     SELECT COUNT(COUNTRY) FROM MEDALS WHERE COUNTRY='CANADA';
     ```

2. **`DISTINCT`**
   - **Purpose:** Removes duplicate values from a result set, providing unique values.
   - **Example:**
     ```sql
     SELECT DISTINCT columnname FROM tablename;
     ```
     For unique countries that received gold medals in `MEDALS` table:
     ```sql
     SELECT DISTINCT COUNTRY FROM MEDALS WHERE MEDALTYPE = 'GOLD';
     ```

3. **`LIMIT`**
   - **Purpose:** Restricts the number of rows retrieved, useful for large datasets.
   - **Example:**
     ```sql
     SELECT * FROM tablename LIMIT 10;
     ```
     For retrieving rows from `MEDALS` table for year 2018:
     ```sql
     SELECT * FROM MEDALS WHERE YEAR = 2018 LIMIT 5;
     ```

## Summary
- **Expressions Covered:** `COUNT`, `DISTINCT`, `LIMIT`.
- These expressions are vital for crafting efficient SQL `SELECT` statements.
- Each function serves a specific purpose in data retrieval and manipulation processes.




# INSERT Statement 

## Overview
- The `INSERT` statement is used for populating a relational database table with data.
- Part of Data Manipulation Language (DML) statements, which are used to read and modify data.
  
## Syntax of INSERT Statement
```sql
INSERT INTO TableName (ColumnName1, ColumnName2, ...) VALUES (Value1, Value2, ...);
```
- `TableName`: The name of the table where data will be inserted.
- `(ColumnName1, ColumnName2, ...)`: List of columns in the table.
- `(Value1, Value2, ...)`: Corresponding values for the columns listed.

## Example
To add data for "Raul Chong" with the following details:
- Author_ID: A1
- Last Name: Chong
- First Name: Raul
- Email: RFC@IBM.com
- City: Toronto
- Country: CA

The `INSERT` statement would be:
```sql
INSERT INTO Author (Author_ID, LastName, FirstName, Email, City, Country) 
VALUES ('A1', 'Chong', 'Raul', 'RFC@IBM.com', 'Toronto', 'CA');
```

## Important Points
- The number of values provided must equal the number of columns specified.
- You can insert multiple rows in one statement by separating each row of values with a comma.

## Example of Multiple Row Insert
Inserting two rows, one for "Raul Chong" and one for "Rav Ahuja":
```sql
INSERT INTO Author (Author_ID, LastName, FirstName, Email, City, Country) 
VALUES 
('A1', 'Chong', 'Raul', 'RFC@IBM.com', 'Toronto', 'CA'),
('A2', 'Ahuja', 'Rav', 'RA@IBM.com', 'New York', 'US');
```

## Summary
- `INSERT` statement is used for adding data to SQL tables.
- Ensure the number of values matches the number of columns.
- Insert multiple rows by separating value sets with commas.



# UPDATE and DELETE Statements 

## Overview
- **`UPDATE`** and **`DELETE`** statements are used for altering and removing data in tables.
- Both are part of Data Manipulation Language (DML) statements.
- **Important:** The `WHERE` clause is crucial to avoid updating or deleting all rows in a table.

## UPDATE Statement

### Syntax
```sql
UPDATE TableName SET ColumnName=Value WHERE Condition;

### Example
- Update author with `Author_ID` of `A2` from "Rav Ahuja" to "Lakshmi Katta":
  ```sql
  UPDATE AUTHOR SET LASTNAME='KATTA', FIRSTNAME='LAKSHMI' WHERE AUTHOR_ID='A2';
  ```
### Note
- Without `WHERE` clause, **all rows** will be updated.

## DELETE Statement

### Syntax
```sql
DELETE FROM TableName WHERE Condition;
```
### Example
- Delete authors with `Author_ID` `A2` and `A3`:
  ```sql
  DELETE FROM AUTHOR WHERE AUTHOR_ID IN ('A2', 'A3');
  ```
### Note
- Without `WHERE` clause, **all rows** will be deleted.

## Summary
- `UPDATE` Statement: Used to modify existing data in a table based on a condition.
- `DELETE` Statement: Removes rows from a table based on a condition.
- The `WHERE` clause is imperative to ensure only specific rows are altered or deleted.

# Module 1 Lesson 2 Summary

## Key Takeaways

### Introduction to SQL
- **SQL** (Structured Query Language) is a powerful language used to query and manage data.
- Essential for working with structured data, facilitating relations among different entities and variables.

### SQL SELECT Statement
- The `SELECT` statement retrieves data from a table.
- A basic `SELECT` statement syntax: 
  ```sql
  SELECT * FROM TableName;
  
- The output from a `SELECT` query is known as a **Result Set or Result Table**.

### SQL INSERT Statement
- `INSERT` statement adds new rows to a table.
- Basic syntax for `INSERT`:
  ```sql
  INSERT INTO TableName (ColumnName) VALUES (values);
  ```
- The number of values in the `VALUES` clause must match the number of specified columns.

### SQL UPDATE Statement
- `UPDATE` statement modifies existing data in a table.
- Basic syntax for `UPDATE`:
  ```sql
  UPDATE TableName SET ColumnName=Value WHERE Condition;
  ```
- Used for reading and modifying data based on specific conditions.

### SQL DELETE Statement
- `DELETE` statement removes rows from a table based on specified conditions.
- Basic syntax for `DELETE`:
  ```sql
  DELETE FROM TableName WHERE Condition;
  ```

### Importance of WHERE Clause
- `WHERE` clause is crucial, defining the specific rows to be acted upon by `SELECT`, `DELETE`, or `UPDATE` statements.
- Without a `WHERE` clause, operations might affect all rows in the table, leading to unintended data modification or loss.

## Conclusion
- Understanding these basic SQL statements provides a foundation for data querying and management in relational databases.
- Practice using `SELECT`, `INSERT`, `UPDATE`, and `DELETE` statements with attention to the `WHERE` clause for precise data manipulation.

