---
title: HackerRank/Oracle SQL Project Planning
date: 2021-12-30 23:30:09
categories:
- CodingTest
tags:
- oracle
- SubQuery
---

# [HackerRank/Oracle] SQL Project Planning

📌[문제링크](https://www.hackerrank.com/challenges/sql-projects/problem) [풀이참고](https://ysyblog.tistory.com/204)

<BR>

***풀이참고 링크에 들어가셔서 보시면 됩니다.**

연속된 프로젝트를 병합하고 end_date-start_date  순으로 정렬한 쿼리를 작성하라

<BR>

-------

##  SubQuery

```sql
SELECT START_DATE, MIN(END_DATE)
FROM 
(SELECT START_DATE FROM PROJECTS WHERE START_DATE NOT IN (SELECT END_DATE FROM PROJECTS))A,
(SELECT END_DATE FROM PROJECTS WHERE END_dATE NOT IN (SELECT START_DATE FROM PROJECTS))B
WHERE START_DATE < END_DATE
GROUP BY START_DATE
ORDER BY (MIN(END_DATE) -START_DATE), START_DATE;
```

<BR>

---------

## 결과

```txt
2015-10-15 2015-10-16
2015-10-17 2015-10-18
2015-10-19 2015-10-20
2015-10-21 2015-10-22
2015-11-01 2015-11-02
2015-11-17 2015-11-18
2015-10-11 2015-10-13
2015-11-11 2015-11-13
2015-10-01 2015-10-05
2015-11-04 2015-11-08
2015-10-25 2015-10-31
```

