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

📌[문제링크](https://app.codility.com/programmers/trainings/6/sql_world_cup/) 

matches 테이블엔 각 축구경기에서의 골수가 적혀있다. <br> 경기결과가 동점인 경우, 두 팀에게 1점씩 부과하고 한 팀이 이긴경우, 이긴팀이게 3점을 부과한다.

나는 with절을 3개를 만들어서 teams 테이블과 join하는 방법을 선택했다.
- tie1 table : 경기결과가 동점인 경우, host_team에 더 해야할 점수 
- tie2 table : 경기결과가 동점인 경우, guest_team에 더 해야할 점수 
- win table : 이긴 팀이 있는 경우, 각 팀에 더해야할 점수 

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
where winner is null) F -- 경기결과가 동점인 경우, host_team에 더 해야할 점수 
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
group by F.guest_team), -- 경기결과가 동점인 경우, guest_team에 더 해야할 점수 
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
group by A.winner) -- 이긴 팀이 있는 경우, 각 팀에 더해야할 점수 
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
