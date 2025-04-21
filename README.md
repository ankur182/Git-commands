Here are all the important SQL INSERT and CREATE TABLE queries from beginner to advanced levels:


---

1. CREATE TABLE Queries

Beginner Level

1. Basic Table Creation

CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);


2. Create Table with Primary Key

CREATE TABLE departments (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);


3. Create Table with NOT NULL and DEFAULT

CREATE TABLE users (
    user_id INT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    status VARCHAR(10) DEFAULT 'active'
);




---

Intermediate to Advanced

4. Create Table with Foreign Key

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(id)
);


5. Composite Primary Key

CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);


6. With CHECK Constraint

CREATE TABLE products (
    id INT PRIMARY KEY,
    price DECIMAL(10,2),
    CHECK (price > 0)
);




---

2. INSERT INTO Queries

Beginner Level

1. Insert a single row

INSERT INTO employees (employee_id, name, salary)
VALUES (101, 'John Doe', 60000);


2. Insert multiple rows

INSERT INTO employees (employee_id, name, salary)
VALUES 
(102, 'Jane Smith', 70000),
(103, 'Mike Brown', 50000);




---

Intermediate to Advanced

3. Insert using SELECT

INSERT INTO high_earners (employee_id, name, salary)
SELECT employee_id, name, salary
FROM employees
WHERE salary > 80000;


4. Insert with DEFAULT values

INSERT INTO users (user_id, username)
VALUES (1, 'ankur'); -- status will be 'active' as default


5. Insert NULL value

INSERT INTO employees (employee_id, name, department_id)
VALUES (104, 'Sara Lee', NULL);




---

Here’s a complete list of important SQL ALTER queries, useful for beginners to advanced levels:


---

Beginner Level: Basic ALTER Queries

1. Add a new column

ALTER TABLE employees
ADD date_of_birth DATE;


2. Rename a column (MySQL example)

ALTER TABLE employees
RENAME COLUMN first_name TO fname;


3. Modify data type of a column

ALTER TABLE employees
MODIFY salary DECIMAL(10, 2);


4. Rename a table

ALTER TABLE employees
RENAME TO staff;




---

Intermediate Level: Dropping and Adding Constraints

5. Drop a column

ALTER TABLE employees
DROP COLUMN middle_name;


6. Add a NOT NULL constraint

ALTER TABLE employees
MODIFY last_name VARCHAR(50) NOT NULL;


7. Add a DEFAULT value

ALTER TABLE employees
ALTER COLUMN bonus SET DEFAULT 1000;


8. Add a UNIQUE constraint

ALTER TABLE employees
ADD CONSTRAINT unique_email UNIQUE (email);


9. Add a PRIMARY KEY

ALTER TABLE employees
ADD PRIMARY KEY (employee_id);


10. Drop PRIMARY KEY



ALTER TABLE employees
DROP PRIMARY KEY;


---

Advanced Level: Foreign Keys & Composite Keys

11. Add a FOREIGN KEY



ALTER TABLE employees
ADD CONSTRAINT fk_department
FOREIGN KEY (department_id) REFERENCES departments(id);

12. Drop a FOREIGN KEY (MySQL example)



ALTER TABLE employees
DROP FOREIGN KEY fk_department;

13. Add composite primary key



ALTER TABLE enrollments
ADD PRIMARY KEY (student_id, course_id);

,,,,,,,,, 

Here’s a full list of important SQL DELETE queries, from beginner to advanced:


---

Beginner Level: Basic DELETE Queries

1. Delete a single row

DELETE FROM employees
WHERE employee_id = 101;


2. Delete multiple rows with a condition

DELETE FROM employees
WHERE department = 'Sales';


3. Delete all rows (without removing the table)

DELETE FROM employees;



> Note: This only removes data but keeps the table structure.



4. Delete using comparison operators

DELETE FROM employees
WHERE salary < 30000;




---

Intermediate Level: Pattern Matching & IN

5. Delete using LIKE

DELETE FROM employees
WHERE first_name LIKE 'A%';


6. Delete using IN

DELETE FROM employees
WHERE department IN ('HR', 'Support');


7. Delete using BETWEEN

DELETE FROM employees
WHERE joining_date BETWEEN '2020-01-01' AND '2021-01-01';




---

Advanced Level: DELETE with JOIN & Subquery

8. DELETE with INNER JOIN (syntax varies by DBMS; MySQL example shown)

DELETE e
FROM employees e
JOIN departments d ON e.department_id = d.id
WHERE d.department_name = 'HR';


9. DELETE using a subquery

DELETE FROM employees
WHERE department_id IN (
    SELECT id FROM departments WHERE location = 'Delhi'
);




---

Would you like to bundle SELECT + UPDATE + DELETE into a single PDF or Markdown file? Or shall I continue with INSERT queries next?

, ,,,,      

Here’s a comprehensive list of important SQL UPDATE queries from beginner to advanced, with syntax and use cases:


---

Beginner Level: Basic UPDATE Queries

1. Update a single column

UPDATE employees
SET salary = 60000
WHERE employee_id = 101;


2. Update multiple columns

UPDATE employees
SET salary = 70000, department = 'Marketing'
WHERE employee_id = 102;


3. Update all rows (use with caution)

UPDATE employees
SET bonus = 1000;




---

Intermediate Level: Conditional and Pattern-based Updates

4. Update with a condition (comparison operator)

UPDATE employees
SET bonus = 1500
WHERE salary > 50000;


5. Update using IN

UPDATE employees
SET department = 'Support'
WHERE department IN ('Helpdesk', 'Customer Service');


6. Update using LIKE

UPDATE employees
SET department = 'Admin'
WHERE department LIKE '%Admin%';


7. Update using IS NULL

UPDATE employees
SET manager_id = 1001
WHERE manager_id IS NULL;




---

Advanced Level: JOIN, Subqueries, and CASE

8. UPDATE with JOIN

UPDATE employees e
JOIN departments d ON e.department_id = d.id
SET e.salary = e.salary + 5000
WHERE d.department_name = 'Engineering';


9. UPDATE using a subquery

UPDATE employees
SET salary = salary * 1.10
WHERE department_id = (
    SELECT id FROM departments WHERE name = 'Sales'
);


10. UPDATE using CASE statement



UPDATE employees
SET bonus = CASE
    WHEN salary >= 100000 THEN 10000
    WHEN salary >= 50000 THEN 5000
    ELSE 2000
END;


---

Would you like to get DELETE queries, INSERT examples, or a downloadable cheat sheet as well?






