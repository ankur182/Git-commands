



Here's a comprehensive list of important SQL SELECT queries ranging from beginner to advanced level. These are categorized for better understanding:


---

Beginner Level: Basic SELECT Queries

1. Select all columns from a table

SELECT * FROM employees;


2. Select specific columns

SELECT first_name, last_name FROM employees;


3. Using WHERE clause

SELECT * FROM employees WHERE department = 'Sales';


4. Using comparison operators

SELECT * FROM employees WHERE salary > 50000;


5. Using logical operators (AND, OR, NOT)

SELECT * FROM employees WHERE salary > 50000 AND department = 'HR';


6. Using BETWEEN

SELECT * FROM employees WHERE salary BETWEEN 40000 AND 60000;


7. Using IN

SELECT * FROM employees WHERE department IN ('HR', 'Sales');


8. Using LIKE

SELECT * FROM employees WHERE first_name LIKE 'A%';


9. Using IS NULL / IS NOT NULL

SELECT * FROM employees WHERE manager_id IS NULL;




---

Intermediate Level: Sorting, Grouping, Aggregation

10. ORDER BY



SELECT * FROM employees ORDER BY salary DESC;

11. LIMIT (or TOP in SQL Server)



SELECT * FROM employees ORDER BY salary DESC LIMIT 5;

12. Aggregate functions



SELECT COUNT(*) FROM employees;
SELECT AVG(salary) FROM employees;
SELECT MAX(salary), MIN(salary) FROM employees;

13. GROUP BY



SELECT department, AVG(salary) FROM employees GROUP BY department;

14. HAVING clause



SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 10;

15. Aliases



SELECT first_name AS Name FROM employees;


---

Advanced Level: Joins, Subqueries, Set Ops

16. INNER JOIN



SELECT e.first_name, d.department_name
FROM employees e
INNER JOIN departments d ON e.department_id = d.id;

17. LEFT JOIN



SELECT e.first_name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.id;

18. RIGHT JOIN



SELECT e.first_name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.department_id = d.id;

19. FULL OUTER JOIN (if supported)



SELECT e.first_name, d.department_name
FROM employees e
FULL OUTER JOIN departments d ON e.department_id = d.id;

20. Subquery (in WHERE clause)



SELECT * FROM employees
WHERE department_id = (
    SELECT id FROM departments WHERE name = 'HR'
);

21. Subquery in SELECT



SELECT first_name,
       (SELECT department_name FROM departments WHERE departments.id = employees.department_id) AS dept_name
FROM employees;

22. Correlated Subquery



SELECT first_name, salary
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE department_id = e.department_id
);

23. UNION / UNION ALL



SELECT first_name FROM employees
UNION
SELECT name FROM clients;

SELECT first_name FROM employees
UNION ALL
SELECT name FROM clients;

24. CASE WHEN



SELECT first_name,
       CASE
           WHEN salary > 100000 THEN 'High'
           WHEN salary BETWEEN 50000 AND 100000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_level
FROM employees;

25. SELECT with DISTINCT



SELECT DISTINCT department FROM employees;

26. SELECT with WINDOW FUNCTION (ROW_NUMBER, RANK)



SELECT *,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS row_num
FROM employees;


---

Would you like these in a downloadable PDF/Notion-ready format or split into practice problems?


