# Question

626. Exchange Seats

https://leetcode.com/problems/exchange-seats/

```
select
    row_number() over (order by new_id asc) id,
    student
from
    (select
        cast(
            case when mod(id,2) = 0 then id-1
            else id+1
            end
     as int) new_id,
        student
    from
        seat
    order by
        new_id asc
     ) temp
     ;

```

Origin `seat` table

|    id   | student |
|---------|---------|
|    1    | Abbot   |
|    2    | Doris   |
|    3    | Emerson |
|    4    | Green   |
|    5    | Jeames  |


Output table

|    id   | student |
|---------|---------|
|    1    | Doris   |
|    2    | Abbot   |
|    3    | Green |
|    4    | Emerson   |
|    5    | Jeames  |
