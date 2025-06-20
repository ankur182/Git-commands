Here's the solution to the lab exercise on "Using Subqueries to Solve Queries" from your image.


---

✅ 1. Last name and salary of employees in the same department as Nancy

SELECT last_name, salary
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM employees
    WHERE first_name = 'Nancy'
);


---

✅ 2. Employees whose salary is greater than the average salary

SELECT employee_id, last_name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);


---

✅ 3. Last name, department number, salary of employees in location ID 1400

SELECT last_name, department_id, salary
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location_id = 1400
);


---

✅ 4. Last name, department number, salary of employees who report to Hunner

SELECT last_name, department_id, salary
FROM employees
WHERE manager_id = (
    SELECT employee_id
    FROM employees
    WHERE last_name = 'Hunner'
);


---

✅ 5. Last name, job ID, and manager ID of employees in the Marketing department

SELECT last_name, job_id, manager_id
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM departments
    WHERE department_name = 'Marketing'
);


---

✅ 6. Last name, department ID, and salary of employees whose department ID and salary match any employee earning a commission

SELECT last_name, department_id, salary
FROM employees
WHERE (department_id, salary) IN (
    SELECT department_id, salary
    FROM employees
    WHERE commission_pct IS NOT NULL
);


---

Let me know if you want an ER diagram or want to test these on a sample database like Oracle HR schema.

