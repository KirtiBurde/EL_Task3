# EL_Task3

1. Setting the Database

use company;

Meaning:
This tells the SQL system to use the "company" database for all upcoming queries.

**2. SELECT Queries**

These are used to retrieve data from a table.

QUERY 1:

select * from employee;

Meaning:
Get all columns and all rows from the employee table.
The result includes:

Employee ID, First Name, Last Name, Gender, Address, Job ID, Salary, and Department ID.


QUERY 2:

select * from department;

Meaning:
Get all columns and all rows from the department table.


QUERY 3:

select first_name, salary from employee order by salary desc;

Meaning:
Get only the first_name and salary columns from the employee table, and sort the results by salary in descending order (highest salary first).



**3. WHERE Clause**

The WHERE clause is used to filter rows based on a condition.

QUERY 1:

select * from employee where salary<70000;

Meaning:
Get all employees whose salary is less than 70,000.

QUERY 2:

select first_name, salary from employee where salary>70000;

Meaning:
Show only the first name and salary of employees who earn more than 70,000.

**4. ORDER BY Clause**

select emp_id, department_id, first_name, job_id, salary 
from employee 
order by salary desc;

Explanation :

select emp_id, department_id, first_name, job_id, salary
→ This part tells the database to fetch these specific columns from the employee table.

from employee
→ You're telling the database which table to get the data from. In this case, it's the employee table.

order by salary desc
→ This is the important part. You're sorting the data based on the salary column.

desc means descending order, so the highest salary comes first.

 **5. GROUP BY Clause**
 
QUERY 1:
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

QUERY 2:
SELECT department_id, COUNT(emp_id)
FROM employee
GROUP BY department_id;

Explanation:

SELECT department_id, COUNT(emp_id): This query selects each unique department_id from the employee table and counts how many employees (emp_id) are in each department.

FROM employee: The data is being pulled from the employee table.

GROUP BY department_id: This groups the data by each department_id, so the COUNT(emp_id) is calculated per department.

 **6. INNER JOIN**

SELECT manager_name, first_name, Department_name 
FROM employee e 
INNER JOIN department d ON e.department_id = d.department_id;

Explanation of the Query

FROM employee e: You are using the employee table and giving it an alias e.

INNER JOIN department d: You're joining this with the department table, which is given alias d.

ON e.department_id = d.department_id: This condition links the two tables based on the department_id field which is common to both.


The INNER JOIN ensures that only records with matching department_id in both tables are returned.

SELECT manager_name, first_name, Department_name: This selects:

manager_name from the employee table,

first_name from the employee table,

Department_name from the department table.

 **7. LEFT JOIN**


The SQL LEFT JOIN Query:

select e.*, d.department_name
from employee as e
left join department as d on e.department_id = d.department_id;

 Explanation:

What is a LEFT JOIN?

A LEFT JOIN returns all records from the left table (employee) and the matching records from the right table (department).

If there is no match in the department table, the result will still include the row from employee but will return NULL for columns from department.


Tables Involved:

employee table (aliased as e)

department table (aliased as d)


Join Condition:

on e.department_id = d.department_id;

This means: match rows in both tables where the department_id fields are the same.

 **8. RIGHT JOIN** 

RIGHT JOIN Query:

select * 
from employee as e 
right join department as d 
on e.department_id = d.department_id;

Explanation:

What does RIGHT JOIN do?

A RIGHT JOIN returns:

All records from the right table (department), and

The matching rows from the left table (employee).

If there’s no matching row in the employee table, you’ll still get the department row, but with NULLs for the employee columns.


Tables Involved:

employee (aliased as e)

department (aliased as d)


Join condition:

e.department_id = d.department_id

So, this joins each employee to their department by department_id.

**9. SUBQUERIES** 

QUERY 1:
select * 
from employee 
where salary > (select avg(salary) from employee);

Explanation:

This query does the following:

1:Inner Query (Subquery):

select avg(salary) from employee

This calculates the average salary of all employees in the employee table.

2: Outer Query:

select * from employee 
where salary > (result of subquery)

This retrieves all columns of employees whose salary is greater than the average salary.
  
QUERY 2:
select first_name, 
       (select avg(salary) from employee) as avg_salary 
from employee 
limit 5;

Explanation:

1: Subquery:

(select avg(salary) from employee)

This calculates the average salary of all employees from the employee table.

It's a scalar subquery—it returns a single value, not a list or table.

2: Outer Query:

select first_name, (subquery) as avg_salary from employee limit 5;

This selects the first name of each employee and also includes the average salary (same for all rows).

It only returns the first 5 rows due to the LIMIT 5 clause.

 **10. AGGREGATE FUNCTIONS** 
**QUERY 1:SUM**

select department_id, sum(salary) 
from employee 
group by department_id;

Explanation:

This SQL query calculates the total salary for each department in the employee table. Here's a breakdown of the components:

department_id: The column used to group the data. Each department will be treated separately.

sum(salary): An aggregate function that computes the sum of salaries within each group (i.e., department).

from employee: Refers to the table from which data is being queried.

group by department_id: Groups the records based on department so that aggregate functions like SUM apply to each group individually.

**QUERY 2:COUNT**

select department_id, count(emp_id)
from employee
group by department_id;

Explanation:

This query uses the COUNT() aggregate function. Here's a breakdown:

department_id: The column by which you're grouping employees.

count(emp_id): Counts how many employee records exist per department.

from employee: Pulls data from the employee table.

group by department_id: Groups employees based on their department so the COUNT() applies to each group.

 **11. VIEW**

Create a view named 'employee_G'
create view employee_G as
select emp_id, first_name, salary
from employee
where gender="F";

✅ What this does:

1. View Creation: The statement creates a view named employee_G.

2. Selected Columns: It selects the columns emp_id, first_name, and salary.

3. Source Table: Data is taken from the table named employee.

4. Filter Condition: It includes only those records where the gender column is equal to "F" (i.e., Female employees).

 **Querying the View**

select * from employee_G;

This statement retrieves all the data from the employee_G view that was just created.

 **12. OPTIMIZING QUERIES** 

select * from employee
where gender = "M"
order by salary;

Explanation:

1: select * from employee:

Retrieves all columns from the employee table.


2: where gender = "M":

Filters the data to only include male employees (M stands for male).


3: order by salary:

Sorts the filtered male employees in ascending order of salary (from lowest to highest).
