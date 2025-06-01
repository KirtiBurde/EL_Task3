# EL_Task3

1. Setting the Database

use company;

Meaning:
This tells the SQL system to use the "company" database for all upcoming queries.

 2. SELECT Queries

These are used to retrieve data from a table.

Query 1:

select * from employee;

Meaning:
Get all columns and all rows from the employee table.
The result includes:

Employee ID, First Name, Last Name, Gender, Address, Job ID, Salary, and Department ID.


Query 2:

select * from department;

Meaning:
Get all columns and all rows from the department table.


Query 3:

select first_name, salary from employee order by salary desc;

Meaning:
Get only the first_name and salary columns from the employee table, and sort the results by salary in descending order (highest salary first).



 3. WHERE Clause

The WHERE clause is used to filter rows based on a condition.

Query 1:

select * from employee where salary<70000;

Meaning:
Get all employees whose salary is less than 70,000.

Query 2:

select first_name, salary from employee where salary>70000;

Meaning:
Show only the first name and salary of employees who earn more than 70,000.

  4. ORDER BY Clause

select emp_id, department_id, first_name, job_id, salary 
from employee 
order by salary desc;

✅ Explanation :

select emp_id, department_id, first_name, job_id, salary
→ This part tells the database to fetch these specific columns from the employee table.

from employee
→ You're telling the database which table to get the data from. In this case, it's the employee table.

order by salary desc
→ This is the important part. You're sorting the data based on the salary column.

desc means descending order, so the highest salary comes first.

 5. GROUP BY Clause
 
Query1:
select department_id, sum(salary) from employee group by department_id;

This SQL query is doing the following:

1:select department_id, sum(salary):

You are selecting two things:

department_id from each employee record.

The sum of salaries of all employees in each department.

2:from employee:

The data is being pulled from a table named employee.

3:group by department_id:

This groups the data by department_id, so that you can perform aggregate functions (like sum) on each group (i.e., each department).

Query 2:
SELECT department_id, COUNT(emp_id)
FROM employee
GROUP BY department_id;

Explanation:

SELECT department_id, COUNT(emp_id): This query selects each unique department_id from the employee table and counts how many employees (emp_id) are in each department.

FROM employee: The data is being pulled from the employee table.

GROUP BY department_id: This groups the data by each department_id, so the COUNT(emp_id) is calculated per department.

 6. INNER JOIN

SELECT manager_name, first_name, Department_name 
FROM employee e 
INNER JOIN department d ON e.department_id = d.department_id;


---

✅ Explanation of the Query

FROM employee e: You are using the employee table and giving it an alias e.

INNER JOIN department d: You're joining this with the department table, which is given alias d.

ON e.department_id = d.department_id: This condition links the two tables based on the department_id field which is common to both.


The INNER JOIN ensures that only records with matching department_id in both tables are returned.

SELECT manager_name, first_name, Department_name: This selects:

manager_name from the employee table,

first_name from the employee table,

Department_name from the department table.

 7. LEFT JOIN 


The SQL LEFT JOIN Query:

select e.*, d.department_name
from employee as e
left join department as d on e.department_id = d.department_id;

