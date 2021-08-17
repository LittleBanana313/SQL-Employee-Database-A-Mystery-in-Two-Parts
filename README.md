# SQL-Employee-Database-A-Mystery-in-Two-Parts

-- 1) List the following details of each employee: employee number, last name, first name, sex, and salary.
```
SELECT employees.emp_no, employees.last_name, employees.first_name, employees.sex, salaries.salary
FROM employees
JOIN salaries
ON employees.emp_no = salaries.emp_no;
```
