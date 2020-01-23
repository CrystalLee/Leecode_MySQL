# Question
185. Customers Who Never Order

https://leetcode.com/problems/department-top-three-salaries/
1. Official Solution

```
SELECT
    d.Name AS 'Department',
    e1.Name AS 'Employee',
    e1.Salary
FROM
    Employee e1
        JOIN
    Department d ON e1.DepartmentId = d.Id
WHERE
    3 > (SELECT
            COUNT(DISTINCT e2.Salary)
        FROM
            Employee e2
        WHERE
            e2.Salary > e1.Salary
                AND e1.DepartmentId = e2.DepartmentId
        )
;
```

2. My Accepted Answer on MySQL server

```
with temp as (
select  
    Name,
    Salary,
    DepartmentId,
    dense_rank() over(partition by DepartmentId  order by DepartmentId, salary desc) as rn
from
    employee
)
select
    Department.Name Department,
    temp.Name Employee,
    temp.Salary Salary
from    
    temp
    join Department on Department.Id = temp.DepartmentId
where
    rn <=3
Order by
    Department.Name,
    Salary DESC
    ;
```

3. My initial Solution on MySQL (Not Accepted)

```
# Write your MySQL query statement below
select
    distinct Employee.`Name` as Employee ,
    Department.`Name` as Department,  
    temp.Salary as Salary
from
    Department
    join Employee on Employee.DepartmentId = Department.Id
    join (
        select
            distinct Salary ,   
            DepartmentId
        from
            Employee
        where
            DepartmentId = 1
        order by
            Salary DESC
        limit 3

    ) temp
        on temp.DepartmentId = Department.Id
        and temp.Salary = Employee.Salary
UNION ALL
select
    distinct Employee.`Name` as Employee ,
    Department.`Name` as Department,  
    temp.Salary as Salary
from
    Department
    join Employee on Employee.DepartmentId = Department.Id
    join (
        select
            distinct Salary ,   
            DepartmentId
        from
            Employee
        where
            DepartmentId = 2
        order by
            Salary DESC
        limit 3

    ) temp
        on temp.DepartmentId = Department.Id
        and temp.Salary = Employee.Salary
;



```
