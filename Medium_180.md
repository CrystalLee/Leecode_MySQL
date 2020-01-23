# Question

180. Consecutive Numbers

https://leetcode.com/problems/consecutive-numbers/

```
/* Write your T-SQL query statement below */

SELECT
    distinct a.Num ConsecutiveNums
FROM
    Logs a
    JOIN Logs b ON a.Id + 1 = b.Id
    JOIN Logs c ON a.Id + 2 = c.Id
WHERE
    a.Num = b.Num
    and b.Num = c.Num
;
```
