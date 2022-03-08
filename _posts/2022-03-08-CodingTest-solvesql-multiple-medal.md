---
title: SQLite/solvesql 복수 국적 메달 수상한 선수 찾기
date: 2022-03-08 00:00:01
categories:
- CodingTest
tags:
- SQLite
- 오답노트

---

# [SQLite/solvesql] 복수 국적 메달 수상한 선수 찾기

📌[문제링크](https://solvesql.com/problems/multiple-medalist/) 

복수 국적을 어떻게 체크하냐가 관건이다. 

이 문제는 `team_id` 속성을 활용해서 복수국적을 가진 운동선수 id를 뽑고 , 그 다음 조인으로 name을 추출하면된다.
2000년도 이후에 올림픽을 고려하라는데, 2000년도 포함되는 것을 명심하자

---

## solution
```sql
select name
from athletes A
inner join (
  select athlete_id,team_id, count(distinct team_id) as nation
  from records R
  left outer join games G on G.id = R.game_id 
  where G.year >= '2000' and R.medal is not null
  group by athlete_id
  having nation > 1) T on T.athlete_id = A.id
```
