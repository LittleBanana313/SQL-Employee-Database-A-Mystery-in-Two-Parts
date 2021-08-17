# SQL-Employee-Database-A-Mystery-in-Two-Parts
![Alt text](Submission-Final/employeeERD.png?raw=true "Title")


**Once you have a complete database, do the following:**
1) List the following details of each employee: employee number, last name, first name, sex, and salary.
```
SELECT employees.emp_no, employees.last_name, employees.first_name, employees.sex, salaries.salary
FROM employees
JOIN salaries
ON employees.emp_no = salaries.emp_no;
```
2) List first name, last name, and hire date for employees who were hired in 1986.
``` 
-- Run the line below if formatting is not working correcting due to data type mismatch.
-- ALTER TABLE employees ALTER COLUMN hire_date TYPE date using to_date(hire_date, 'MM/DD/YYYY')
SELECT first_name, last_name, hire_date 
FROM employees
WHERE hire_date BETWEEN '1/1/1985' AND'12/30/1986'
ORDER BY hire_date;
```

3) List the manager of each department with the following information: department number, department name, the manager's employee number, last name, first name.
```
SELECT departments.dept_no, departments.dept_name, dept_manager.emp_no, employees.last_name, employees.first_name
FROM departments
JOIN dept_manager on departments.dept_no = dept_manager.dept_no JOIN employees on employees.emp_no = dept_manager.emp_no
```
4) List the department of each employee with the following information: employee number, last name, first name, and department name.
```
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees ON dept_emp.emp_no = employees.emp_no
JOIN departments ON dept_emp.dept_no = departments.dept_no;
```
5) List first name, last name, and sex for employees whose first name is "Hercules" and last names begin with "B."
```
SELECT first_name, last_name, sex
FROM employees
WHERE first_name= 'Hercules' AND last_name Like 'B%'
```
6) List all employees in the Sales department, including their employee number, last name, first name, and department name.
```
SELECT employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees ON employees.emp_no = dept_emp.emp_no
JOIN departments ON dept_emp.dept_no = departments.dept_no
WHERE departments.dept_name = 'Sales'
ORDER BY emp_no;
```
7) List all employees in the Sales and Development departments, including their employee number, last name, first name, and department name.
```
SELECT employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees ON employees.emp_no = dept_emp.emp_no
JOIN departments ON dept_emp.dept_no = departments.dept_no
WHERE departments.dept_name = 'Sales'
OR departments.dept_name = 'Development'
ORDER BY emp_no;
```
8) In descending order, list the frequency count of employee last names, i.e., how many employees share each last name.
```
SELECT employees.last_name, COUNT(employees.last_name)
FROM employees GROUP BY employees.last_name ORDER BY COUNT(employees.last_name) DESC
```
Epilogue
```
SELECT * FROM employees
WHERE emp_no= 499942
```
**Bonus**
1) Import the SQL database into Pandas. (Yes, you could read the CSVs directly in Pandas, but you are, after all, trying to prove your technical mettle.) This step may require some research. Feel free to use the code below to get started. Be sure to make any necessary modifications for your username, password, host, port, and database name:
```
from config import user, password, db_name

# Connect to database
connection_string = (f'postgresql://{user}:{password}@localhost/{db_name}')
engine = create_engine(connection_string)                     
conn = engine.connect()
```
2) Create a histogram to visualize the most common salary ranges for employees.\
![Alt text](Submission-Final/salaryfreq.png?raw=true "Title")
3) Create a bar chart of average salary by title.
![Alt text](Submission-Final/salarybytitle.png?raw=true "Title")
