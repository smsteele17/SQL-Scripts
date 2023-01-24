# SQL_Scripts
SQL scripts 

--Using PARTITION BY with an INNER JOIN--

SELECT 
    first_name, 
    last_name, 
    gender, 
    salary, 
    COUNT(gender) OVER (PARTITION BY gender) AS total_gender
FROM employee_demogrpahics AS dem
JOIN employee_salary AS sal 
    ON dem.employee_id = sal.employee_id 



--Using CASE Statements for employee raises--

SELECT
    first_name, 
    last_name, 
    job_title,
    salary
CASE
    WHEN job_title = 'Salesman' THEN salary + (salary * .10)
    WHEN job_title = 'Accountant' THEN salary + (salary * .07)
    WHEN job_title = 'HR' THEN salary + (salary * .05)
    ELSE salary + (salary * .03)
END AS salary_after_raise
FROM employee_demographics AS dem
JOIN employee_salary AS sal
    ON dem.employee_id = sal.employee_id
ORDER BY salary DESC



--Using CTE (Common Table Expressions)--

WITH CTE_employee AS
(SELECT first_name, last_name, gender, salary,
	COUNT(gender) OVER (PARTITION by gender) as total_gender,
	AVG(salary) OVER (PARTITION by gender) as avg_salary
FROM employee_demographics AS emp
JOIN employee_salary AS sal
	ON emp.employee_id = sal.employee_id
WHERE salary > '45000'
)
SELECT *
FROM CTE_employee 



--Using GROUP BY with an OUTER JOIN--

SELECT
    first_name, 
    last_name, 
    job_title, 
    salary, 
    COUNT(job_title) AS employees_per_job
FROM employee_demogrpahics AS dem
FULL JOIN employee_salary AS sal 
    ON dem.employee_id = sal.employee_id 
WHERE salay > 52000
GROUP BY job_title



--Using SUBQUERIES in the SELECT Statement--

SELECT employee_id, salary (
    SELECT AVG(salary) 
    FROM employee_salary) AS all_avg_salary
FROM employee_salary



--Using SUBQUERIES in the WHERE Statement--

SELECT employee_id, job_title, salary
FROM employee_salary
WHERE employee_id IN (
    SELECT employee_id
    FROM employee_demographics
    WHERE age > 30)



--Using UNION--

SELECT 
    first_name, 
    last_name, 
    job_title,
    salary
FROM employee_demographics
UNION
SELECT 
    first_name, 
    last_name, 
    job_title,
    salary
FROM employee_warehouse_demographics
ORDER BY salary DESC

--






