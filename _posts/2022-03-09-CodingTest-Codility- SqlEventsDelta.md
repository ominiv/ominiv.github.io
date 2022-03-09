---
title: PostgreSQL/Codility SqlEventsDelta
date: 2022-03-09 00:00:01
categories:
- CodingTest
tags:
- Codility
- PostgreSQL
---

# [PostgreSQL/Codility] SqlEventsDelta

📌[문제링크](https://app.codility.com/programmers/trainings/6/sql_events_delta/) 

event_type이 2회 이상인 경우, 가장 최근 날짜 value - 그 다음 날의 value 차이를 구하는 문제다.

Codility 는 Oracle를 지원하지 않는다;; <br>
조금 당황했다.. SQLite 의 경우 `row_number()`를 지원하지 않아서 PostgreSQL로 풀었다. 

---

## solution
```sql
select  event_type, sum(prev)-sum(next)
from    (select B.event_type , 
        case 
        when B.RN = 1 then value
        end as prev,
        case 
        when B.RN = 2 then value
        end as next
        from (select A.event_type, A.value, A.time, row_number() over(partition by A.event_type order by A.time desc )as RN
            from (select *
                from events
                where event_type in (
                    select distinct event_type
                    from events
                    group by event_type
                    having count(*)>=2) -- event_type 2개 이상인 경우 추출
                ) A 
            ) B -- row_number 로 evnet_type 별 번호 매김
        ) C -- event_type 별 prev, next 열 추가
group by event_type
order by event_type
```

## 다른사람 풀이 LEAD 함수 이용
LEAD를 이용하면 쿼리가 한결 간단해진다. 

```sql
select  B.event_type, B.result as value
from    (select A.event_type, A.value - lead(A.value) over(partition by A.event_type order by A.event_type) as result
        from (select event_type, value, time, row_number() over(partition by event_type order by time desc) as RN
            from events
            where event_type in (
                select distinct event_type
                from events
                group by event_type
                having count(*) >=2) -- event_type 2개 이상인 경우 추출
            ) A --row_number 로 evnet_type 별 번호 매김
        where A.RN <=2) B --lead로 두행간의 값차이 구함 , 1행과 2행만 필요하므로 R.RN <= 2 조건절 추가
where B.result is not null 
order by B.event_type
```
