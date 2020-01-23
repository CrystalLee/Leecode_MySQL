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

2. Soluton in discussion

```
select
    d.Name as Department,
    a. Name as Employee,
    a. Salary
from (
  select  
      Employee.*,
      dense_rank() over (partition by DepartmentId order by Salary desc) as DeptPayRank
  from
      Employee
) a
join
  Department d
  on a. DepartmentId = d. Id
where
  DeptPayRank <=3
;
```

3. My Solution (Not Accepted)


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
