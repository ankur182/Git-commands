Let’s solve all 4 questions based on the image and instructions.


---

✅ 1. Display:

Last name in uppercase

Length of the last name

Job ID from the 4th character


SELECT 
    UPPER(last_name) AS upper_last_name,
    LENGTH(last_name) AS last_name_length,
    SUBSTR(job_id, 4) AS job_id_from_4th
FROM employees;


---

✅ 2. Display:

Employee ID

First name

Salary

Salary increased by 10% (as a whole number, column named New_Sal)


SELECT 
    employee_id,
    first_name,
    salary,
    ROUND(salary * 1.10) AS New_Sal
FROM employees;


---

✅ 3. Display:

First name

Number of months worked (rounded)

Sorted by months worked


SELECT 
    first_name,
    ROUND(MONTHS_BETWEEN(SYSDATE, hire_date)) AS months_worked
FROM employees
ORDER BY months_worked DESC;


---

✅ 4. Display:

Employee ID

Hire date formatted like "Seventeenth of June 1994 12:00:00 AM"

Salary as $15,000


SELECT 
    employee_id,
    TO_CHAR(hire_date, 'fmDdth "of" Month YYYY "12:00:00 AM"') AS "Hired On",
    TO_CHAR(salary, '$99,999') AS "Earns"
FROM employees;


---

📌 Sample Output (as shown in image for Q4):

EMPLOYEE_ID	Hired On	Earns

100	Seventeenth of June 1987 12:00:00 AM	$24,000
101	Twenty-First of September 1989 12:00:00 AM	$22,000
102	Thirteenth of January 1993 12:00:00 AM	$17,000
103	Third of January 1990 12:00:00 AM	$20,000
104	Twenty-First of May 1991 12:00:00 AM	$6,000
105	Twenty-Fifth of June 1992 12:00:00 AM	$12,000



---

Let me know if you want me to convert this into a .sql or .pdf file for submission.

