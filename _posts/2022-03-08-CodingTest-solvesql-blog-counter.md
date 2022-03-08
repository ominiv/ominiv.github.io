---
title: SQLite/solvesql 일별 블로그 방문자 수 집계
date: 2022-03-08 00:00:01
categories:
- CodingTest
tags:
- SQLite

---

# [SQLite/solvesql] 일별 블로그 방문자 수 집계

📌[문제링크](https://solvesql.com/problems/blog-counter/) 

고전적인 groupby 문제다. <br> between으로 날짜범위를 체크하고 해당 날짜별 user수를 체크하자


---

## solution
```sql
select
  distinct event_date_kst as dt,
  count(distinct user_pseudo_id) as users
from
  ga
where
  event_date_kst between "2021-08-02" and '2021-08-09'
group by
  event_date_kst
order by
  dt

```
