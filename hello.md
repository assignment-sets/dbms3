# SQL Class Notes: Table Operations and Constraints

## Table Structure

```sql
EmployeeID  FirstName  LastName  DepartmentID  Salary  HireDate
1           John       Doe       101           50000   15-Jan-2023
2           Jane       Smith     102           60000   20-Feb-2023
3           Michael    Johnson   101           55000   10-Mar-2023
4           Emily      Williams  103           52000   05-Apr-2023
5           David      Brown     102           58000   15-May-2023
6           Sarah      Jones     101           53000   20-Jun-2023
```

## Adding Constraints

### Primary Key Constraint

To add a primary key constraint after creating the table structure:

```sql
ALTER TABLE employee
ADD CONSTRAINT pk_employee PRIMARY KEY (employeeid);
```

Note: `pk_employee` is the explicitly defined name of the primary key.

### Not Null Constraint

To modify a column to be NOT NULL:

```sql
ALTER TABLE employee
MODIFY firstname NOT NULL;
```

## Inserting Data

### Using TO_DATE Function

```sql
INSERT INTO Employee (EmployeeID, FirstName, LastName, DepartmentID, Salary, HireDate)
VALUES (7, 'Davido', 'Leo', 102, 58000, TO_DATE('2024-02-28', 'YYYY-MM-DD'));

-- Alternative date format
INSERT INTO Employee (EmployeeID, FirstName, LastName, DepartmentID, Salary, HireDate)
VALUES (7, 'Davido', 'Leo', 102, 58000, TO_DATE('20-Jan-2024', 'DD-Mon-YYYY'));
```

## Modifying Table Structure

### Dropping a Column

```sql
ALTER TABLE Employee DROP COLUMN DepartmentID;
```

### Changing Column Size/Length

```sql
ALTER TABLE employee
MODIFY firstname VARCHAR2(100);
```

Important Notes:
- If a column is populated, only its length can be changed, not its datatype.
- If a column is not populated, it's possible to change its datatype.

## Creating and Using Views

```sql
CREATE VIEW emp AS
SELECT employeeid, firstname
FROM employee;
```

This creates a view named `emp` that includes only the `employeeid` and `firstname` columns from the `employee` table.

# Additional SQL Notes

## Topics to Learn

1. Join
2. Where clause
3. Relation and Foreign Key (FK)
4. Update vs Alter
5. Dual

**Note:** The `SELECT` keyword is used for column selection, while the `WHERE` clause is for row selection based on column conditions.

## Aggregate Functions

### Count

To count all rows:

```sql
SELECT COUNT(*)
FROM employee;
```

**Note:** There's a difference between `COUNT(*)` and `COUNT(DISTINCT column)`.

### Other Aggregate Functions

```sql
SELECT
    MAX(salary) AS highest_salary,
    AVG(salary) AS avg_salary,
    SUM(salary) AS total_salary
FROM employee;
```

This query demonstrates the use of:
- `MAX()`: Finds the highest salary
- `AVG()`: Calculates the average salary
- `SUM()`: Computes the total of all salaries

These functions provide summary statistics about the `salary` column in the `employee` table.
