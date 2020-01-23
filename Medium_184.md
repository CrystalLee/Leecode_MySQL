# Question
184. Department Highest Salary

https://leetcode.com/problems/department-highest-salary/

```
select
    Department.`Name` as Department,
    Employee.`Name` as Employee ,
    Employee.Salary as Salary
from
    Department
    join Employee on Employee.DepartmentId = Department.Id
    join
    (
    select
        DepartmentId,
        Max(Salary) Salary
    from
        Employee
    group by
        DepartmentId
    ) temp on temp.Salary = Employee.Salary
        and temp.DepartmentId = Employee.DepartmentId
  ;
```
