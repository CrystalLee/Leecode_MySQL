# Question
262. Trips and Users

https://leetcode.com/problems/trips-and-users/

```
# Write your MySQL query statement below

select
    Request_at Day,
    round(sum(if (Status like '%cancel%', 1, 0)) / count(Id),2) 'Cancellation Rate'
from
    Trips
    join Users client on client.Users_Id = Trips.Client_Id
        and client.Banned ='No'
    join Users driver on driver.Users_Id = Trips.Driver_Id
        and driver.Banned ='No'
where
    Request_at between '2013-10-01' and '2013-10-03'
group by
    Request_at
;
```
