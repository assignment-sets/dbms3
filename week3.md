# SQL Employee Database Guide

## 1. Table Structures

### 1.1 Employee Table

```sql
CREATE TABLE employee (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100),
    emp_email VARCHAR(100),
    emp_position VARCHAR(50),
    emp_salary DECIMAL(10, 2),
    hire_date DATE
);
```

### 1.2 Department Table

```sql
CREATE TABLE dept (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50) UNIQUE NOT NULL
);
```

## 2. Sample Data

### 2.1 Employee Data

```sql
INSERT INTO employee (emp_id, emp_name, emp_email, emp_position, emp_salary, hire_date)
VALUES
(1, 'John Doe', 'john.doe@example.com', 'Software Engineer', 75000.00, TO_DATE('2022-01-15', 'YYYY-MM-DD')),
(2, 'Jane Smith', 'jane.smith@example.com', 'Project Manager', 85000.00, TO_DATE('2021-03-22', 'YYYY-MM-DD')),
(3, 'Emily Johnson', 'emily.johnson@example.com', 'UX Designer', 68000.00, TO_DATE('2022-07-10', 'YYYY-MM-DD')),
(4, 'Michael Brown', 'michael.brown@example.com', 'Data Analyst', 72000.00, TO_DATE('2023-02-19', 'YYYY-MM-DD')),
(5, 'Linda Davis', 'linda.davis@example.com', 'HR Specialist', 69000.00, TO_DATE('2020-11-30', 'YYYY-MM-DD'));
```

### 2.2 Department Data

```sql
INSERT INTO dept (dept_id, dept_name) VALUES 
(1, 'Engineering'),
(2, 'Management'),
(3, 'Design'),
(4, 'Data Analytics'),
(5, 'Human Resources');
```

## 3. SQL Queries

### 3.1 Rename Column
```sql
ALTER TABLE employee RENAME COLUMN emp_name TO employee_name;
```

### 3.2 Update Email
```sql
UPDATE employee SET emp_email = 'demo@gmail.com' WHERE emp_id = 2;
```

### 3.3 Count Employees by Department
```sql
SELECT dept, COUNT(*) AS num_of_employees FROM employee GROUP BY dept;
```

### 3.4 Add Foreign Key and Update Department IDs
```sql
ALTER TABLE employee ADD (dept_id INT);

ALTER TABLE employee
ADD CONSTRAINT fk_dept
FOREIGN KEY (dept_id) REFERENCES dept(dept_id);

UPDATE employee e
SET e.dept_id = (
    SELECT d.dept_id
    FROM dept d
    WHERE d.dept_name = (
        CASE e.emp_position
            WHEN 'Software Engineer' THEN 'Engineering'
            WHEN 'Project Manager' THEN 'Management'
            WHEN 'UX Designer' THEN 'Design'
            WHEN 'Data Analyst' THEN 'Data Analytics'
            WHEN 'HR Specialist' THEN 'Human Resources'
        END
    )
);
```

### 3.5 Select Names Starting with J or L
```sql
SELECT emp_name FROM employee WHERE emp_name LIKE 'J%' OR emp_name LIKE 'L%';
```

### 3.6 Concatenate Name and Email
```sql
SELECT CONCAT(emp_name, emp_email) AS hello FROM employee;
```

## 4. Additional SQL Concepts

### 4.1 Wildcard Characters
SQL supports three main wildcard characters:
1. `%` - Represents zero, one, or multiple characters
2. `_` - Represents a single character
3. `[]` - Represents any single character within the brackets

### 4.2 Pipe Operator
The pipe operator `||` is used in some SQL dialects for string concatenation. For example:
```sql
SELECT emp_name || ' - ' || emp_email AS employee_info FROM employee;
```

### 4.3 UPPER and LOWER Functions
- `UPPER()`: Converts a string to uppercase
- `LOWER()`: Converts a string to lowercase

Example:
```sql
SELECT UPPER(emp_name) AS uppercase_name, LOWER(emp_email) AS lowercase_email FROM employee;
```