# Question

178. Rank Scores  

https://leetcode.com/problems/rank-scores/

```
select
    Score,
    dense_rank() over(order by Score desc)  rank
from
    Scores
    ;
```
