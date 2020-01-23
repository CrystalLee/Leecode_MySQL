# Question
601. Human Traffic of Stadium

https://leetcode.com/problems/human-traffic-of-stadium/

```
SELECT
    DISTINCT S1.*
FROM
    stadium S1
    JOIN stadium S2
    JOIN stadium S3
    ON ((S1.id = S2.id - 1 AND S1.id = S3.id -2)
    OR (S3.id = S1.id - 1 AND S3.id = S2.id -2)
    OR (S3.id = S2.id - 1 AND S3.id = S1.id -2))
WHERE
    S1.people >= 100
    AND S2.people >= 100
    AND S3.people >= 100
ORDER BY S1.id
;
```

## Concept
The question was asking for 3 or more consecutive rows. For example, the table `stadium`:

| id   | visit_date | people    |
| -- | ------------ | -- |
| 1    | 2017-01-01 | 10        |
| 2    | 2017-01-02 | 109       |
| 3    | 2017-01-03 | 150       |
| 4    | 2017-01-04 | 99        |
| 5    | 2017-01-05 | 145       |
| 6    | 2017-01-06 | 1455      |
| 7    | 2017-01-07 | 199       |
| 8    | 2017-01-08 | 188       |

So the 3 consecutive date would have 3 combinations

- 1 2 3 _ _
- _ 1 2 3 _
- _ _ 1 2 3

That's why the on condition would be writen like this
