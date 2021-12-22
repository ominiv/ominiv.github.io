---
title: HackerRank/Oracle Weather Observation Station 20
date: 2021-12-21 23:30:09
categories:
- CodingTest
tags:
- oracle
- ROW_NUMBER
---

# [HackerRank/Oracle] Weather Observation Station 20

📌[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-20/problem)  [풀이참고](https://yurimyurim.tistory.com/14)

  <BR>

***풀이참고 링크 들어가셔셔 보시면 됩니다.**

<BR>

## 1. ROW_NUMBER 이용

```sql
SELECT  ROUND(AVG(LAT_N),4) MEDIAN
FROM    (SELECT  LAT_N, 
        ROW_NUMBER() OVER(ORDER BY LAT_N) RN,
        COUNT(1) OVER() +1 CNT
        FROM    STATION)
WHERE RN BETWEEN FLOOR(CNT/2) AND CEIL(CNT/2);
```

<BR>

## 2.MEDIAN 함수 이용

```SQL
SELECT  ROUND(MEDIAN(LAT_N),4)
FROM    STATION;
```



