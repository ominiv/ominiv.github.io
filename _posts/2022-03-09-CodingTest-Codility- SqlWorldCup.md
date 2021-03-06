---
title: PostgreSQL/Codility SqlWorldCup
date: 2022-03-09 00:00:01
categories:
- CodingTest
tags:
- Codility
- PostgreSQL
---

# [PostgreSQL/Codility] SqlWorldCup

๐[๋ฌธ์ ๋งํฌ](https://app.codility.com/programmers/trainings/6/sql_world_cup/) 

matches ํ์ด๋ธ์ ๊ฐ ์ถ๊ตฌ๊ฒฝ๊ธฐ์์์ ๊ณจ์๊ฐ ์ ํ์๋ค. <br> ๊ฒฝ๊ธฐ๊ฒฐ๊ณผ๊ฐ ๋์ ์ธ ๊ฒฝ์ฐ, ๋ ํ์๊ฒ 1์ ์ฉ ๋ถ๊ณผํ๊ณ  ํ ํ์ด ์ด๊ธด๊ฒฝ์ฐ, ์ด๊ธดํ์ด๊ฒ 3์ ์ ๋ถ๊ณผํ๋ค.

๋๋ with์ ์ 3๊ฐ๋ฅผ ๋ง๋ค์ด์ teams ํ์ด๋ธ๊ณผ joinํ๋ ๋ฐฉ๋ฒ์ ์ ํํ๋ค.
- tie1 table : ๊ฒฝ๊ธฐ๊ฒฐ๊ณผ๊ฐ ๋์ ์ธ ๊ฒฝ์ฐ, host_team์ ๋ ํด์ผํ  ์ ์ 
- tie2 table : ๊ฒฝ๊ธฐ๊ฒฐ๊ณผ๊ฐ ๋์ ์ธ ๊ฒฝ์ฐ, guest_team์ ๋ ํด์ผํ  ์ ์ 
- win table : ์ด๊ธด ํ์ด ์๋ ๊ฒฝ์ฐ, ๊ฐ ํ์ ๋ํด์ผํ  ์ ์ 

---

## solution
```sql
with tie1 as (select F.host_team, sum(F.cnt) as num
from (select A.host_team, 1 as cnt
from (SELECT  match_id, host_team, guest_team, host_goals, guest_goals,case
        when host_goals = guest_goals then 1
        else 3
        end as score,
        case
        when host_goals > guest_goals then host_team
        when host_goals < guest_goals then guest_team
        else NULL
        end as winner
        from matches ) A
where winner is null) F -- ๊ฒฝ๊ธฐ๊ฒฐ๊ณผ๊ฐ ๋์ ์ธ ๊ฒฝ์ฐ, host_team์ ๋ ํด์ผํ  ์ ์ 
group by F.host_team),
tie2 as (select F.guest_team, sum(F.cnt) as num
from (select A.guest_team, 1 as cnt
from (SELECT  match_id, host_team, guest_team, host_goals, guest_goals,case
        when host_goals = guest_goals then 1
        else 3
        end as score,
        case
        when host_goals > guest_goals then host_team
        when host_goals < guest_goals then guest_team
        else NULL
        end as winner
        from matches ) A
where winner is null) F
group by F.guest_team), -- ๊ฒฝ๊ธฐ๊ฒฐ๊ณผ๊ฐ ๋์ ์ธ ๊ฒฝ์ฐ, guest_team์ ๋ ํด์ผํ  ์ ์ 
win as (select A.winner, sum(A.score) as num
from (SELECT  match_id, host_team, guest_team, host_goals, guest_goals,case
        when host_goals = guest_goals then 1
        else 3
        end as score,
        case
        when host_goals > guest_goals then host_team
        when host_goals < guest_goals then guest_team
        else NULL
        end as winner
from matches) A
group by A.winner) -- ์ด๊ธด ํ์ด ์๋ ๊ฒฝ์ฐ, ๊ฐ ํ์ ๋ํด์ผํ  ์ ์ 
-- teams, win, tie1, tie2 join
select R.team_id, R.team_name, R.sumv1 + R.sumv2 + R.sumv3 as num_points
from (select team_id, team_name, 
case when win.num is null then 0 else win.num end as sumv1,
case when tie1.num is null then 0 else tie1.num end as sumv2,
case when tie2.num is null then 0 else tie2.num end as sumv3
from teams
left outer join win on teams.team_id=win.winner
left outer join tie1 on teams.team_id=tie1.host_team
left outer join tie2 on teams.team_id=tie2.guest_team) R
order by num_points desc, R.team_id

```
