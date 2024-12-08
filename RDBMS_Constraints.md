## Types of Constraints in RDBMS </br>
### 1. Referential Integrity Constraint
Referential integrity ensures that foreign keys in one table correctly refer to primary keys or unique keys in another table, maintaining the relationship between tables. This ensures that relationships between tables remain consistent.

Purpose: To ensure that foreign key values in a child table must match values in the parent table or be NULL.

Example: In a database with orders and customers tables, a foreign key customer_id in the orders table must reference an existing customer_id in the customers table.

CREATE TABLE orders ( </br>
    order_id INT PRIMARY KEY, </br>
    customer_id INT, </br>
    amount DECIMAL(10, 2), </br>
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id) </br>
); </br>
In this case, every customer_id in the orders table must correspond to an existing customer_id in the customers table, ensuring referential integrity.

### 2. Entity Integrity Constraint
Entity integrity ensures that every table has a primary key, and the key must have unique and non-NULL values. This guarantees that each row in a table can be uniquely identified.

Purpose: To guarantee that every entity (record) in a table has a unique and identifiable primary key.

Example: In the employees table, emp_id can be a primary key. The emp_id must be unique for each employee and cannot be NULL.

CREATE TABLE employees ( </br>
    emp_id INT PRIMARY KEY, </br>
    name VARCHAR(50), </br>
    department VARCHAR(50) </br>
); </br>
Here, the emp_id serves as the unique identifier for each employee, ensuring entity integrity.

### 3. Enterprise Integrity Constraint
Enterprise integrity involves ensuring the correctness of business logic across an entire enterprise. This constraint deals with rules or conditions that apply across the whole database schema, enforcing specific domain rules that are valid across multiple tables or business processes.

Purpose: To apply business-specific rules and constraints that ensure the data meets enterprise-level requirements (e.g., ensuring an employee’s salary is within a specific range, or ensuring a person can’t be assigned more than one job role at a time).

Example: A constraint that limits an employee's salary range based on company policy.

CREATE TABLE employees (
    emp_id INT PRIMARY KEY, </br>
    name VARCHAR(50), </br>
    department VARCHAR(50), </br>
    salary DECIMAL(10, 2), </br>
    CHECK (salary >= 3000 AND salary <= 10000)  -- Enterprise Integrity constraint </br>
); </br>
In this case, the CHECK constraint ensures that the salary of an employee is between 3000 and 10000, which is an enterprise rule for the company.

### 4. Domain Integrity Constraint
Domain integrity ensures that the data entered into the table's columns is valid and falls within an allowable domain of values. This is typically enforced using data types, check constraints, and default values.

Purpose: To restrict the values that can be stored in a column to valid values (e.g., specific data types, ranges, or pre-defined values).

Example: In a students table, you may want to ensure that the age column only accepts positive integers or values that fall within a realistic range.

CREATE TABLE students ( </br>
    student_id INT PRIMARY KEY, </br>
    name VARCHAR(50), </br>
    age INT CHECK (age >= 18 AND age <= 100),   -- Domain Integrity constraint </br>
    gender CHAR(1) CHECK (gender IN ('M', 'F'))  -- Ensuring only 'M' or 'F' values </br>
); </br>
In this case, the age column is restricted to values between 18 and 100, and the gender column can only have values 'M' or 'F'.

Summary of Constraints:
- Referential Integrity :Ensures that foreign keys in a table refer to valid rows in another table.	FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
- Entity Integrity	  :Ensures each table has a primary key and it is unique and non-null.	PRIMARY KEY (emp_id)
- Enterprise Integrity  :Enforces business-specific rules across the enterprise.	CHECK (salary BETWEEN 3000 AND 10000)
- Domain Integrity	  :Ensures data is within the defined allowable set or range for a column.	CHECK (age BETWEEN 18 AND 100)
Each of these constraints ensures that the data stored in the database is consistent, valid, and accurate based on different levels of integrity
