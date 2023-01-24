# SQL_Scripts
SQL scripts 

--Using PARTITION BY with an INNER JOIN & ALIASES--

SELECT 
    first_name, 
    last_name, 
    gender, 
    salary, 
    COUNT(gender) OVER (PARTITION BY gender) AS total_gender
FROM employee_demogrpahics AS dem
JOIN employee_salary AS sal 
    ON dem.employee_id = sal.employee_id 

-- Using GROUP BY with an OUTER JOIN & Aliasing

SELECT
    first_name, 
    last_name, 
    job_title, 
    salary, 
    COUNT(job_title) AS employees_per_job
FROM employee_demogrpahics AS dem
JOIN employee_salary AS sal 
    ON dem.employee_id = sal.employee_id 
GROUP BY job_title
