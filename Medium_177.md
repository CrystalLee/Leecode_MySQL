# Question
177. Nth Highest Salary

https://leetcode.com/problems/nth-highest-salary/

```
CREATE FUNCTION getNthHighestSalary(@N INT) RETURNS INT AS
BEGIN
    RETURN (
        /* Write your T-SQL query statement below. */
        select
            salary as getNthHighestSalary
        from (
            select
                distinct Salary,
                dense_rank() over (order by Salary desc ) rn
            from
                Employee
            ) temp
        where
            rn = @N
    );
END
```
